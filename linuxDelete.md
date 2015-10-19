layout: post
title: linux删除同一个文件夹下的所有文件，不包括文件夹
tags: linux
filename: linuxDelete
date: 2014-09-20 14:58:12
keywords: linux
description:
---
1.进入改文件夹
2.执行以下命令：
find . -type f | xargs /bin/rm -f

-type 后面的 f 表示普通文件

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/09/20/{{ filename }}>