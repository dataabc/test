layout: post
title: C#创建XML文件
tags: C#
filename: CsharpCreateXML2
date: 2014-10-21 16:00:23
keywords: C#
description:
---
要创建xml文件，需要在C#程序头下引入两行代码：
using System.Xml;
using System.Xml.Linq;
<!--more-->
主要代码：
```csharp
XElement xElement = new XElement(
                new XElement("TaskList",
                    new XElement("Task",
                                    new XElement("节点1", "节点1内容"),
                                    new XElement("节点2", "节点2内容"),
                                    new XElement("节点3", "节点3内容"),
                                    new XElement("节点4", "节点4内容"),
                                    new XElement("节点5", "节点5内容"),
                                    new XElement("节点6", "节点6内容"),
                                    new XElement("节点7", "节点7内容"),
                                    new XElement("节点8", "节点8内容"),
                                    new XElement("节点9",
                                      new XElement("节点9子节点", new XAttribute("value", "内容"))
                                                )
                               )
                        )
                );
            XmlWriterSettings settings = new XmlWriterSettings();
            settings.Encoding = new UTF8Encoding(false);
            settings.Indent = true;
            XmlWriter xw = XmlWriter.Create(@"xmlpath", settings);//要生成的xml的具体路径，包括xml文件名
            xElement.Save(xw);
            xw.Flush();
            xw.Close();
```

参考文章：http://www.cnblogs.com/zery/p/3362480.html