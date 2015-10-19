layout: post
title: 解决gvim在win10下乱码的问题
tags: [vim]
filename: win10Gvim
date: 2015-08-16 16:31:46
keywords: vim
description:
---
今天在win10上安装了gvim，发现中文乱码，于是按照我以前的文章《[windows下gvim中文乱码解决方案](http://cognize.me/2015/04/02/winVim/ "windows下gvim中文乱码解决方案")》进行了设置，但是发现仍然有乱码，后来发现通过设置字体可以解决，方法是在gvim的安装目录找到_vimrc文件，在里面加入如下代码：<!--more-->
```xml
"设置字体
"set guifont=楷体:h10:cGB2312
set guifont=KaiTi:h10:cGB2312
"设置字符集
set encoding=GBK
set ambiwidth=double
set fileencoding=utf-8
set fileencodings=utf-8,ucs-bom,cp936,gb18030,utf-16,big5,gbk,ucs-bom,cp936,latin1
set encoding=GBK
set ambiwidth=double
set fileencoding=utf-8
set fileencodings=utf-8,ucs-bom,cp936,gb18030,utf-16,big5,gbk,ucs-bom,cp936,latin1
```
原创文章如转载，请注明本文链接:<http://www.cognize.me/2015/08/16/{{ filename }}>
