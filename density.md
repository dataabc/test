title: R语言之density函数
date: 2014-12-08 23:02:14
tags: R
keywords: R, R语言, density
description: R语言之density函数
---
<img src="{%view%}2014-12-08-density.jpg{%suffix%}" alt=""></img>
&emsp;&emsp;density英文含义为“密度”，R语言中density()函数自然就是求数据密度的了。
&emsp;&emsp;density()函数的形式为density(x,...),其中x为数据，“...”代表其它的参数，有兴趣的同学可以自己研究。
&emsp;&emsp;在官方文档举的例子中，x的值为c(-20,rep(0,98),20),实质上就是一个向量，包含一个-20，一个20和98个零。通过density(x)函数，可以计算出向量x的密度。density()函数通常和plot()函数结合使用，用来画数据的密度图，形式如下：
&emsp;&emsp;plot(density(x))
&emsp;&emsp;其中x中的实际值为横坐标，对应的密度为纵坐标。

原创文章如转载，请注明本文链接:<http://cognize.me/2014/12/08/density/>