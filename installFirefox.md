title: Centos下安装或更新Firefox浏览器
date: 2015-03-26 19:34:44
tags: linux
keywords: linux, Centos, Firefox,安装Firefox
description: Centos下安装或更新Firefox浏览器
---
Centos安装或更新Firefox浏览器，步骤如下：
1.根据系统版本（32位或64位）下载对应的Firefox安装包，如果软件的版本与系统版本不一致，会报错。
2.tar -jxv -f filename.tar.bz2 -C /usr/lib64
其中，filename.tar.bz2代表Firefox的安装包，运行时替换成实际的安装包即可
3.cd /usr/lib64/firefox
4../firefox-bin


原创文章如转载，请注明本文链接:<http://cognize.me/2015/03/26/installFirefox/>
