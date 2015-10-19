title: C#检测计算机上是否安装了某些软件
date: 2015-02-01 17:33:55
tags: C#
keywords: C#, 检测软件, 软件安装
description: C#检测计算机上是否安装了某些软件
---
<img src="{%view%}2015-2-1-software.jpg{%suffix%}" alt=""></img>
&emsp;&emsp;有时候，我们需要知道，我们的计算机上安装了什么软件，我们当然知道，问题是如何让我们的程序也知道呢？下面的方法仅对部分软件有效，一些软件无法检测。那对什么软件有效呢？请继续往下看。
首先，引入头文件。
<pre><code>using System.Runtime.InteropServices;</code></pre>
然后，输入如下代码即可。
<!--more-->
<pre><code>
static void Main()
{
    StringBuilder result = new StringBuilder();
    for (int index = 0; ; index++)
    {
        StringBuilder productCode = new StringBuilder(39);
        if (MsiEnumProducts(index, productCode) != 0)
        {
            break;
        }
        foreach (string property in new string[] { "ProductName", "Publisher", "VersionString", })
        {
            int charCount = 512;
            StringBuilder value = new StringBuilder(charCount);
            if (MsiGetProductInfo(productCode.ToString(), property, value, ref charCount) == 0)
            {
                value.Length = charCount;
                result.AppendLine(value.ToString());
            }
        }
        result.AppendLine();
    }
    Console.WriteLine(result.ToString());
}      
[DllImport("msi.dll", SetLastError = true)]
static extern int MsiEnumProducts(int iProductIndex, StringBuilder lpProductBuf);
[DllImport("msi.dll", SetLastError = true)]
static extern int MsiGetProductInfo(string szProduct, string szProperty, StringBuilder lpValueBuf, ref int pcchValueBuf);
</code></pre>
&emsp;&emsp;C#直接运行该代码即可。运行之（Ctrl+F5）,程序会列出计算机上已经安装的软件及其相关信息，但是有些已安装软件却无法显示。如果你需要检查的软件就在结果列表里，那么恭喜你，你可以直接调用本程序；否则，你只能另寻它法了。下面的文字只是针对前者的，所以如果你的情况属于后者，就不必往下看啦。
&emsp;&emsp;所有的结果信息都保存在result.ToString()里，我们可以对这个字符串进行操作。我的思路如下：
<pre><code>
   if(result.ToString().Contains("SoftwareName"))
     return true;
   else
     return false;
</code></pre>
&emsp;&emsp;我的思路很简单，就是判断结果文件中是否包含某些关键字。如，我要检测是否安装了Python，SoftwareName可以替换成Python。总之，我们只要替换成要检测的软件独一无二且出现在result.ToString()中的信息就好。



原创文章如转载，请注明本文链接:<http://cognize.me/2015/02/01/software/>