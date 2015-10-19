layout: post
title: linux下短暂的改变ip
tags: linux
filename: linuxchangeip
date: 2014-10-11 15:29:02
keywords: linux
description:
---
linux 改变IP,代码如下：
ifconfig eth0 192.168.1.18
以上代码可以改变IP地址，系统重启后ip就会重新变回原值。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/11/{{ filename }}>