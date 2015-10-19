layout: post
title: 解决linux下“XX不在 sudoers 文件中。此事将被报告"的问题
tags: linux
filename: linuxsudoers
date: 2014-09-17 14:55:40
keywords: linux
description:
---
今天在Linux下用sudo命令，突然遇到问题，输入sudo相关命令侯提示如下：
        XX不在 sudoers 文件中。此事将被报告。<!--more-->
       其中"XX"为我的用户名，经过网络搜索，终于找到了解决方法，需要切换到root,以下只提供shell输入内容：
      1.chmod 740 /etc/sudoers
      2.sudo gedit /etc/sudoers
      3.找到# Allow members of group sudo to execute any command
               %sudo    ALL=(ALL) ALL
      在下面添加一行，如下
                     xx       ALL=(ALL) ALL  (将此处的XX修改为出现改问题的用户名！）
					 
原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/09/17/{{ filename }}>