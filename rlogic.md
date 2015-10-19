title: R中的逻辑运算符&, &&, |, ||
date: 2015-06-11 21:33:15
tags: R
---
注：本文为转载，原文地址：*http://blog.qiuworld.com:8080/archives/2921*
在R中，逻辑运算符(logical operator)有!, &, &&, |, ||, xor, isTRUE等等。

问题：&与&&, |与||有什么区别呢？它们是否是一致的呢？

答：否。我们将&和|称为短逻辑符，&&及||称为长逻辑符。长逻辑符只比较左边和右边的第一个元素，而短逻辑符会比较所以的。我们来看示例：
<!--more-->
```r
> a<-c(TRUE, FALSE, TRUE, FALSE)
> b<-c(FALSE, FALSE, TRUE, TRUE)
> c<-c(TRUE, FALSE, FALSE, FALSE)
> a & b
[1] FALSE FALSE  TRUE FALSE
> a && b
[1] FALSE
> a & c
[1]  TRUE FALSE FALSE FALSE
> a && c
[1] TRUE
> a | b
[1]  TRUE FALSE  TRUE  TRUE
> a || b
[1] TRUE
> a | c
[1]  TRUE FALSE  TRUE FALSE
> a || c
[1] TRUE
```