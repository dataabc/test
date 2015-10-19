title: Windows服务（C#）显式运行exe程序
date: 2015-02-11 19:08:00
tags: [C#,WindowsService]
keywords: C#, WindowsService, 运行exe
description: Windows服务（C#）显式运行exe程序
---
<img src="{%view%}2015-2-11-Windowsservice.jpg{%suffix%}" alt=""></img>
&emsp;&emsp;一般来讲，用C#运行某个.exe程序，我们都会这样写：
<pre><code>Process.Start("xxx.exe")</code></pre>
&emsp;&emsp;其中，“xxx.exe”表示我们要运行的exe的路径，Process.Start()函数有多种重载，我们这里不再赘述。大多数程序都可以通过以上的代码运行exe程序，但是当我们把我们的“控制台应用程序”转成“Windows服务”后，就会出现问题。
<!--more-->
&emsp;&emsp;事实上，在“Windows服务”中，上述代码还是可以运行exe程序的，但是我们看不到。在“控制台应用程序”中，我们可以看到被执行的exe程序，但是到了“Windows服务”中，该exe变成了后台执行，无法与用户进行交互。
原因如下：
&emsp;&emsp;默认情况下，服务是运行在session0下的，与普通的应用程序不在一个session，所以不能互动，但是我们可以利用函数“CreateProcessAsUser”来创建应用程序session下的进程，从而调用外部exe。
Windows服务（C#）显式运行外部exe程序源代码如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Security;
using System.Diagnostics;
using System.Runtime.InteropServices;
namespace SngjIPS_WindowsService
{
    class UserProcess
    {   #region Structures
        [StructLayout(LayoutKind.Sequential)]
        public struct SECURITY_ATTRIBUTES
        {
            public int Length;
            public IntPtr lpSecurityDescriptor;
            public bool bInheritHandle;
        }
        [StructLayout(LayoutKind.Sequential)]
        public struct STARTUPINFO
        {
            public int cb;
            public String lpReserved;
            public String lpDesktop;
            public String lpTitle;
            public uint dwX;
            public uint dwY;
            public uint dwXSize;
            public uint dwYSize;
            public uint dwXCountChars;
            public uint dwYCountChars;
            public uint dwFillAttribute;
            public uint dwFlags;
            public short wShowWindow;
            public short cbReserved2;
            public IntPtr lpReserved2;
            public IntPtr hStdInput;
            public IntPtr hStdOutput;
            public IntPtr hStdError;
        }
        [StructLayout(LayoutKind.Sequential)]
        public struct PROCESS_INFORMATION
        {
            public IntPtr hProcess;
            public IntPtr hThread;
            public uint dwProcessId;
            public uint dwThreadId;
        }
        #endregion
        #region Enumerations
        enum TOKEN_TYPE : int
        {
            TokenPrimary = 1,
            TokenImpersonation = 2
        }
        enum SECURITY_IMPERSONATION_LEVEL : int
        {
            SecurityAnonymous = 0,
            SecurityIdentification = 1,
            SecurityImpersonation = 2,
            SecurityDelegation = 3,
        }
        enum WTSInfoClass
        {
            InitialProgram,
            ApplicationName,
            WorkingDirectory,
            OEMId,
            SessionId,
            UserName,
            WinStationName,
            DomainName,
            ConnectState,
            ClientBuildNumber,
            ClientName,
            ClientDirectory,
            ClientProductId,
            ClientHardwareId,
            ClientAddress,
            ClientDisplay,
            ClientProtocolType
        }
        #endregion
        #region Constants
        public const int TOKEN_DUPLICATE = 0x0002;
        public const uint MAXIMUM_ALLOWED = 0x2000000;
        public const int CREATE_NEW_CONSOLE = 0x00000010;
        public const int IDLE_PRIORITY_CLASS = 0x40;
        public const int NORMAL_PRIORITY_CLASS = 0x20;
        public const int HIGH_PRIORITY_CLASS = 0x80;
        public const int REALTIME_PRIORITY_CLASS = 0x100;
        #endregion
        #region Win32 API Imports
        [DllImport("kernel32.dll", SetLastError = true)]
        private static extern bool CloseHandle(IntPtr hSnapshot);
        [DllImport("kernel32.dll")]
        static extern uint WTSGetActiveConsoleSessionId();
        [DllImport("wtsapi32.dll", CharSet = CharSet.Unicode, SetLastError = true), SuppressUnmanagedCodeSecurityAttribute]
        static extern bool WTSQuerySessionInformation(System.IntPtr hServer, int sessionId, WTSInfoClass wtsInfoClass, out System.IntPtr ppBuffer, out uint pBytesReturned);
        [DllImport("advapi32.dll", EntryPoint = "CreateProcessAsUser", SetLastError = true, CharSet = CharSet.Ansi, CallingConvention = CallingConvention.StdCall)]
        public extern static bool CreateProcessAsUser(IntPtr hToken, String lpApplicationName, String lpCommandLine, ref SECURITY_ATTRIBUTES lpProcessAttributes,
            ref SECURITY_ATTRIBUTES lpThreadAttributes, bool bInheritHandle, int dwCreationFlags, IntPtr lpEnvironment,
            String lpCurrentDirectory, ref STARTUPINFO lpStartupInfo, out PROCESS_INFORMATION lpProcessInformation);
        [DllImport("kernel32.dll")]
        static extern bool ProcessIdToSessionId(uint dwProcessId, ref uint pSessionId);
        [DllImport("advapi32.dll", EntryPoint = "DuplicateTokenEx")]
        public extern static bool DuplicateTokenEx(IntPtr ExistingTokenHandle, uint dwDesiredAccess,
            ref SECURITY_ATTRIBUTES lpThreadAttributes, int TokenType,
            int ImpersonationLevel, ref IntPtr DuplicateTokenHandle);
        [DllImport("kernel32.dll")]
        static extern IntPtr OpenProcess(uint dwDesiredAccess, bool bInheritHandle, uint dwProcessId);
        [DllImport("advapi32", SetLastError = true), SuppressUnmanagedCodeSecurityAttribute]
        static extern bool OpenProcessToken(IntPtr ProcessHandle, int DesiredAccess, ref IntPtr TokenHandle);
        #endregion
        public static string GetCurrentActiveUser()
        {
            IntPtr hServer = IntPtr.Zero, state = IntPtr.Zero;
            uint bCount = 0;
            // obtain the currently active session id; every logged on user in the system has a unique session id  
            uint dwSessionId = WTSGetActiveConsoleSessionId();
            string domain = string.Empty, userName = string.Empty;
            if (WTSQuerySessionInformation(hServer, (int)dwSessionId, WTSInfoClass.DomainName, out state, out bCount))
            {
                domain = Marshal.PtrToStringAuto(state);
            }
            if (WTSQuerySessionInformation(hServer, (int)dwSessionId, WTSInfoClass.UserName, out state, out bCount))
            {
                userName = Marshal.PtrToStringAuto(state);
            }
            return string.Format("{0}\\{1}", domain, userName);
        }
        /// <summary>  
        /// Launches the given application with full admin rights, and in addition bypasses the Vista UAC prompt  
        /// </summary>  
        /// <param name="applicationName">The name of the application to launch</param>  
        /// <param name="procInfo">Process information regarding the launched application that gets returned to the caller</param>  
        /// <returns></returns>  
        public static bool StartProcessAndBypassUAC(String applicationName, String command, out PROCESS_INFORMATION procInfo)
        {
            uint winlogonPid = 0;
            IntPtr hUserTokenDup = IntPtr.Zero, hPToken = IntPtr.Zero, hProcess = IntPtr.Zero;
            procInfo = new PROCESS_INFORMATION();
            // obtain the currently active session id; every logged on user in the system has a unique session id  
            uint dwSessionId = WTSGetActiveConsoleSessionId();
            // obtain the process id of the winlogon process that is running within the currently active session  
            Process[] processes = Process.GetProcessesByName("winlogon");
            foreach (Process p in processes)
            {
                if ((uint)p.SessionId == dwSessionId)
                {
                    winlogonPid = (uint)p.Id;
                }
            }
            // obtain a handle to the winlogon process  
            hProcess = OpenProcess(MAXIMUM_ALLOWED, false, winlogonPid);
            // obtain a handle to the access token of the winlogon process  
            if (!OpenProcessToken(hProcess, TOKEN_DUPLICATE, ref hPToken))
            {
                CloseHandle(hProcess);
                return false;
            }
            // Security attibute structure used in DuplicateTokenEx and CreateProcessAsUser  
            // I would prefer to not have to use a security attribute variable and to just   
            // simply pass null and inherit (by default) the security attributes  
            // of the existing token. However, in C# structures are value types and therefore  
            // cannot be assigned the null value.  
            SECURITY_ATTRIBUTES sa = new SECURITY_ATTRIBUTES();
            sa.Length = Marshal.SizeOf(sa);
            // copy the access token of the winlogon process; the newly created token will be a primary token  
            if (!DuplicateTokenEx(hPToken, MAXIMUM_ALLOWED, ref sa, (int)SECURITY_IMPERSONATION_LEVEL.SecurityIdentification, (int)TOKEN_TYPE.TokenPrimary, ref hUserTokenDup))
            {
                CloseHandle(hProcess);
                CloseHandle(hPToken);
                return false;
            }
            // By default CreateProcessAsUser creates a process on a non-interactive window station, meaning  
            // the window station has a desktop that is invisible and the process is incapable of receiving  
            // user input. To remedy this we set the lpDesktop parameter to indicate we want to enable user   
            // interaction with the new process.  
            STARTUPINFO si = new STARTUPINFO();
            si.cb = (int)Marshal.SizeOf(si);
            si.lpDesktop = @"winsta0\default"; // interactive window station parameter; basically this indicates that the process created can display a GUI on the desktop  
            // flags that specify the priority and creation method of the process  
            int dwCreationFlags = NORMAL_PRIORITY_CLASS | CREATE_NEW_CONSOLE;
            // create a new process in the current user's logon session  
            bool result = CreateProcessAsUser(hUserTokenDup,        // client's access token  
                                            applicationName,        // file to execute  
                                            command,                // command line  
                                            ref sa,                 // pointer to process SECURITY_ATTRIBUTES  
                                            ref sa,                 // pointer to thread SECURITY_ATTRIBUTES  
                                            false,                  // handles are not inheritable  
                                            dwCreationFlags,        // creation flags  
                                            IntPtr.Zero,            // pointer to new environment block   
                                            null,                   // name of current directory   
                                            ref si,                 // pointer to STARTUPINFO structure  
                                            out procInfo            // receives information about new process  
                                            );
            // invalidate the handles  
            CloseHandle(hProcess);
            CloseHandle(hPToken);
            CloseHandle(hUserTokenDup);
            return result; // return the result  
        }
    }
 }
```
调用如下：
```csharp
UserProcess.PROCESS_INFORMATION pInfo = new UserProcess.PROCESS_INFORMATION();
UserProcess.StartProcessAndBypassUAC("xxx.exe", string.Empty, out pInfo);
```
<font color="red">注意，该程序一定要写在“Windows服务”程序的代码中才有效，如果您把本程序代码写在“控制台应用程序”中运行是没有任何效果的。</font>
参考文章：*http://bbs.csdn.net/topics/390431360*
*http://chinaforce2008.blog.163.com/blog/static/32284182013112644445536/*


原创文章如转载，请注明本文链接:<http://cognize.me/2015/02/11/windowsservice/>