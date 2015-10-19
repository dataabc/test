layout: post
title: 安装 purcell 的emacs.d 配置文件
tags: emacs
filename: purcellemacs
date: 2014-09-09 11:04:55
keywords: emacs
description:
---
安装前注意一定要以一般用户的身份安装，以root身份安装会导致安装失败。<!--more-->
1、确保安装了git和subversion，ubuntu: apt-get install git  ;apt-get install subversion;
centos: yum install git ; yum install subversion;
2、在用git clone下载<https://github.com/purcell/emacs.d>的配置
git clone <https://github.com/purcell/emacs.d.git>  ~/.emacs.d
3、删除原来的.emacs文件
4、在.emacs.d 目录下执行  
git submodule update --init
5、若是成功，emacs重启会自动安装相应插件；若是失败而且没有提示信息，我碰到一种可能：将/root/.emacs.d 拷贝到 /home/主机名字/.emacs.d


转载地址：http://www.cnblogs.com/bigbigtree/archive/2013/03/08/2950942.html
