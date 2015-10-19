layout: post
title: 解决R语言中出现“could not find function vcov.”的问题
tags: R
filename: rVcov
date: 2014-11-20 16:33:14
keywords: R
description:
---
先说解决方法：
把list(....)换成xlevels=list(....)即可。
<!--more-->
     今天在看《R语言实战》，有一个例子用到了effects包中的effect函数，明明是按书上的例子写的，可是
偏偏就是不对，运行plot(effect(“hp:wt”, fit, list(wt = c(2.2, 3.2, 4.2))), multiline = TRUE) 时，老是
报“could not find function vcov.”的错误，于是我运行
？effect  命令
      在帮助文档看到了“vcov.”这个参数，又发现了一个“xlevels”的参数的例子和list(wt = c(2.2, 3.2, 4.2))
很像，只是它多了一个xlevels.
       我怀疑R把list(wt = c(2.2, 3.2, 4.2))当成了vcov了，而它又不是vcov.，所以导致程序出错。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/11/20/{{ filename }}>