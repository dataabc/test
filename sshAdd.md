layout: post
title: 执行ssh-add时出现Could not open a connection to your authentication agent
tags: 
filename: sshAdd
date: 2015-01-02 16:35:31
keywords:
description:
---
执行ssh-add ~/.ssh/rsa
 报标题上的错误
先执行  eval `ssh-agent`  （是～键上的那个`） 再执行 ssh-add ~/.ssh/rsa成功
ssh-add -l 就有新加的rsa了

原创文章如转载，请注明本文链接:<http://www.cognize.me/2015/01/02/{{ filename }}>