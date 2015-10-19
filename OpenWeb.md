layout: post
title: 利用C#打开新的特定的网页
tags: C#
filename: OpenWeb
date: 2014-09-06 10:53:15
keywords: C#
description:
---
网上很多利用C#打开新的特定的网页都是关于Web程序的，可如果用的是Windows又该如何打开网页呢？方法如下：
                System.Diagnostics.Process.Start("xxxxxx");//其中“xxxxxx”代表要打开的网址或本地文件的路径，当然也可以是其它的文件，如"/xxxx/**.doc"，则打开的是doc文件。
原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/09/06/{{ filename }}>