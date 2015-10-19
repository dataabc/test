layout: post
title: R语言之for循环
tags: R
filename: rFor
date: 2014-10-16 15:35:34
keywords: R
description:
---
假设有一个向量t，我们要对它进行for循环操作，则语句为：
<!--more-->
for(i in 1:length(t))
......（这里写具体的操作）
      其中，length(t)表示向量t的长度，1：length(t)表示1到向量长度之间的数列，如向量t长度为10，
则i会在1到10之间取值。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/10/16/{{ filename }}>