layout: post
title: 解决hexo一个奇怪的错误
tags: hexo
filename: msysgiterror
date: 2015-08-22 21:13:08
keywords: hexo
description:
---
其实说是“解决hexo一个奇怪的错误”并不恰当，因为错并不在hexo。<!--more-->

我的hexo一直是部署在笔记本上，前几天笔记本硬盘坏了，等换上新的SSD以后，按照以前的步骤重新部署hexo,但是总是会出现“Permission denied (publickey). fatal: Could not read from remote repository.”和“Please make sure you have the correct access rights and the repository exists.”的错误，起初我以为是SSH公钥配置错误，但是在Git Bash里输入“ssh -T git@gitcafe.com
”却又可以出现“Hi xxxx! You've successfully authenticated, but GitCafe does not provide shell access.”的正确提示，反复试了几次，结果都一样{% emoji-block %}:sob::sob::sob:{% endemoji-block %}

后来，在[某论坛](http://v2ex.com/t/215055#reply20 "某论坛")发现一个网友和我的错误一模一样，但是他也没有解决的方法，就在刚刚我又去看了一下网友发的那个帖子，眼前忽然一亮{% emoji-block %}:open_mouth::open_mouth::open_mouth:{% endemoji-block %}

<img src="{%other%}2015-8-22-msysgiterror.jpg" alt=""></img>

{% emoji-block %}我注意到，我们运行环境是惊人的一样，用了相同版本的msysgit，出现了相同的错误提示，而网上所的教程中msysgit的版本都是另一个版本，会不会是msysgit版本的问题呢？我陷入了深深的思考......:monkey_face::monkey_face::monkey_face:{% endemoji-block %}

后来，我在<http://pan.baidu.com/s/1o6miNZ8>下载了旧版的msysgit，竟然可以正确运行，没有错误，没有错误，没有错误......{% emoji-block %}:ghost::ghost::ghost:{% endemoji-block %}

所以，该错误是由msysgit引起的，有相同错误的童鞋安装[旧版本的msysgit](http://pan.baidu.com/s/1o6miNZ8 "旧版本的msysgit")就可以解决该问题。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2015/08/22/{{ filename }}>