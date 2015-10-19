layout: post
title: R语言中seq函数的用法
tags: R
filename: rSeq
date: 2014-10-12 15:33:50
keywords: R
description:
---
seq(from,to,length),
该函数的意思是生成一组数字，从from开始，到to结束，每两个数间的间隔是length,如
seq(2,10,2),会生成一组数：2 4 6 8 10
<!--more-->

seq(from,to,length.out=by)表示生成一组从from到to的数量为num的数
by = ((to - from)/(length.out - 1))
附seq的其它用法：
seq(from, to)
seq(from, to, by= )
seq(from, to, length.out= )
seq(along.with= )
seq(from)
seq(length.out= )

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/12/{{ filename }}>