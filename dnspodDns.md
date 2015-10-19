layout: post
title: 用dnspod进行DNS解析出错的解决方案
tags: 
filename: dnspodDns
date: 2014-11-03 16:11:37
keywords:
description:
---
这是dnspod提供的记录值：
f1g1ns1.dnspod.net.
f1g1ns2.dnspod.net.
在作DNS解析时，需要将域名的nameservers指向这两个值，如果出错，去掉最后那个“.”，
即可。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/11/03/{{ filename }}>