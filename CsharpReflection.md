layout: post
title: C#动态加载dll或exe类库(即C#反射)
tags: C#
filename: CsharpReflection
date: 2014-10-21 15:55:39
keywords: C#
description:
---
头部引用代码如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;//一般前四行代码在我们创建程序时自动生成，我们只需要加入本行代码即可
```<!--more-->
主要代码如下：
```csharp
Assembly ass = Assembly.LoadFile(@"D:\mydll.dll");//我们要调用的dll或exe文件路径
Type tp = ass.GetType("namepace.class");  //获取类名，必须 命名空间+类名
Object obj = Activator.CreateInstance(tp);  //建立实例
MethodInfo meth = tp.GetMethod("mymethod");  //获取要调用的方法
meth.Invoke(obj, new string[] {"args1","args2"});//Invoke调用方法,"{}"里为方法需<span style="font-family: Arial, Helvetica, sans-serif;">要的参数</span>
```

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/21/{{ filename }}>