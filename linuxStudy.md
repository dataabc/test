layout: post
title: Linux学习记录
tags: linux
filename: linuxStudy
date: 2014-08-18 10:32:39
keywords: linux
description:
---
1.查找文件及目录的命令：find。
例如：find / -name filename或find -name filename 可以查找这个系统中名为filename的文件及目录。
2.貌似whereis只能查询程序名的搜索，其它文件不起作用。<!--more-->
3.关于cp的用法。
      cp  源文件路径 目标文件路径
貌似绝对路径和相对路径都可以，也可以混合使用。（其它命令应该也同理吧）,若复制的文件为目录，要加-r。
4.文档压缩。
    用gzip xxxxx/xxx/xxx(文档路径)可以将其压缩，用gzip -d xxxxx/xxx/xxx(文档路径)可以将其解压，但是它们都会使原文档消失。
    用gzip -c xxxxx/xxx/xxx > yyy/yyy/yyy可以将文档压缩到yyy/yyy/yyy处，并保留原文档；
    用gzip -dc xxxxx/xxx/xxx > yyy/yyy/yyy可以将文档解压到yyy/yyy/yyy处，并保留原文档。
">"是定向输出到文件，如果文件不存在，就创建文件；如果文件存在，就将其清空
  bzip2的用法和gzip一样。 
5.文档打包
  压 缩:tar -jcv -f filename.tar.bz2 要被压缩的档案或目录名称
  查 询:tar -jtv -f filename.tar.bz2
  解压缩:tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录
  推荐用法：tar -jpcv -f 你起的文档名.tar.bz2 源文档名（也可写作tar -jpcvf 你起的文档名.tar.bz2 源文档名）
  因为bzip2的压缩比要好于gzip，所以推荐上述用法，其中j表示解压的是tar.bz2,若解压后缀为tar.gz则应换成z，v显示正在操作的文档，p表示备份数据的原本
与属性,c表示进行的是打包操作，所以最简短的打包语句应该是：tar -jcf 你起的文件名.tar.bz2 源文档名
  另外，可以同时压缩多个文档 ：
tar -jpcv -f 你起的文档名.tar.bz2 源文档名1 源文档名2 ... 源文档名N
 个人理解：c:compress压缩，其它t、x未知。6.文档解压缩
语句：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录
上述语句是解压filename.tar.bz2的文档，但是它可能非常大，我们只需要里面的其中一个文档，因此只需要解压该文档
语句：tar -jxv -f filename.tar.bz2 -C 要解压的文档的目录

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/08/18/{{ filename }}>