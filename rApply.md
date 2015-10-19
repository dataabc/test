layout: post
title: R语言对行或列执行某函数
tags: R
filename: rApply
date: 2014-11-16 16:30:47
keywords: R
description:
---
R语言对行或列执行某函数用
apply(x,MARGIN,FUN,...);
<!--more-->
x为数据对象，MARGIN是维度的下标，MARGIN=1表示行，MARGIN=2表示列，FUN是我们要用的函数，
“...”包括了其它我们想传的参数。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/11/16/{{ filename }}>