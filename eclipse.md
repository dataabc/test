layout: post
title: 在eclipse中以本地的方式安装插件
tags: eclipse
filename: eclipse
date: 2014-10-09 15:20:30
keywords: eclipse
description:
---
在eclipse中有很多方式安装插件，但是因为有的必须要联网，而我们有的工作机恰恰没有网络，怎么办呢？我们可以通过
本地的方式在eclipse安装插件。<!--more-->
      首先，你要先在有网络的计算机上把你要安装的插件下载下来，比如我要在eclipse安装StatET 插件，所以我下载了名为
site-statet-03.04.00.zip的文件。然后在eclipse安装文件夹下你会发现有一个dropins文件夹，把site-statet-03.04.00.zip
拷贝进去，解压，会出现很多文件，如feature文件夹、plugins文件夹等，在这里只保留feature文件夹和
plugins文件夹，其余的删除，重启eclipse，即可。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/09/{{ filename }}>