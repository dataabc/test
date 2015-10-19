layout: post
title: R语言中因子(factor)转换成数值型(numeric)的问题
tags: R
filename: rFactorToNumeric
date: 2014-10-18 15:43:11
keywords: R
description:
---
一直觉得只要是数字，不管是什么类型的，都可以通过as.numeric()函数转换为对应的numeric类型的数字，例如
x<-“123”，x为character类型，而as.numeric(x)则为numeric类型的123。但是因子(factor)类型却不一样。<!--more-->
      a<-factor(c(100,200,300,301,302,400,10))，它们的值分别为100 200 300 301 302 400 10，然而
as.numeric(a)对应的值并非100 200 300 301 302 400 10，而是2 3 4 5 6 7 1。因子(factor)转换成数值型(numeric)
的规则是这样的：

     一共有n个数，那么转换后的数字就会在1——n中取值，数字最小的取一，次小的取二，以此类推。
     那么如何让因子(factor)类型里的数值转换对应的数值型呢？
     mean(as.numeric(as.character(factorname)))
     mean(as.numeric(levels(factorname)[factorname]))
     以上代码都可以实现将因子(factor)类型里的数值转换对应的数值型，思路都是先转换成字符型然后再转换成数值型。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/18/{{ filename }}>