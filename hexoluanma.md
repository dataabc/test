layout: post
title: 解决hexo博客的乱码问题
tags: hexo
filename: hexoluanma
date: 2014-10-31 16:07:21
keywords: hexo
description:
---
将博客文件保存为UTF-8即可解决问题。
方法：<!--more-->
    1.将博客文件保存为UTF-8
     用记事本打开本地的博客文件“xxx.md”，然后点“另存为”，“编码(E):”选择“UTF-8”，
点击“保存”，替换原文件。
    2.重新生成，部署，博客乱码即消除。
	```shell
hexo g
hexo d
```

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/31/{{ filename }}>