layout: post
title: R语言中判断两个对象是否相等
tags: R
filename: r-identical
date: 2015-08-25 20:34:00
keywords: R
description:
---
在R语言中可以使用identical函数或者all.equal函数判断两个对象是否相同，例如：
假设x、y是R中我们要比较的对象，
identical(x,y)
若x等于y，返回TRUE；若x不等于y，则返回FALSE。<!--more-->
all.equal(x,y)
若x等于y，返回TRUE；若x不等于y，则返回不相等的原因。
identical和all.equal函数都可以判断两个对象是否相等。identical比较数据的内在关系，如果对象是严格相同的返回TRUE，否则返回FALSE。all.equal用来判断两个对象是否“近似相等”，返回结果为TRUE或者对二者差异的描述。后一个函数在比较数值型变量时考虑到了计算过程中的近似。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2015/08/25/r-equal>
