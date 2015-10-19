layout: post
title: R语言的计算中去除NA
tags: R
filename: rNA
date: 2014-11-16 16:26:58
keywords: R
description:
---
在R语言中，当我们在对数组计算时，经常会遇到这种情况。比如，
x<-c(1,2,3,NA,4,5)
y<-sum(x)<!--more-->
因为x中有NA，所以当对x进行sum操作时，y会被赋值为NA，那如何才能在计算时去除NA的干扰呢？
y<-sum(x,na.rm=TRUE)
通过在函数中加“na.rm=TRUE”即可，书中说很多函数都可以用这个方法去除NA的干扰，大家可以试一下。

如果想要去除数据中的NA，可以这样：
newdata<-na.omit(olddata)

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/11/16/{{ filename }}>