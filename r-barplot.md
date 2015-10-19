title: R语言中barplot函数的用法
date: 2015-07-18 16:59:37
tags: R
keywords: R, R语言, barplot, barplot函数
description: R语言中barplot函数的用法
---
barplot函数在R中是一个画条线图的函数。
最简单的用法，即当参数为一个向量时，用法如例子所示：
<!--more-->
```r
> mydata<-c(1,2,3,4,5)
> barplot(mydata)
```
结果如下图所示：
<img src="{%rplot%}2015-7-18-r-barplot.png{%suffix%}" alt=""></img>
结果图形的x轴被分成了五份，因为mydata中一共有五个数据，y轴则对应了每个数据的具体数值。

另外，稍复杂的用法是参数为矩阵的情况，用法如下：

```r
> mydata<-data.frame(aaa=c(1,2,3),bbb=c(2,4,6))
> barplot(as.matrix(mydata))
```
结果如下图所示：
<img src="{%rplot%}2015-7-18-r-barplot2.png{%suffix%}" alt=""></img>
结果图形的x轴被分成两部分，因为mydata一共有两个元素，即aaa和bbb，x轴的默认表情就是mydata的列名，而每列中的数据依次叠加在一起，高度为各自的数值。如果想将数据中每列的图形分开，可以使用参数beside，即：
```r
> barplot(as.matrix(mydata),beside=T)
```
结果如下图所示：
<img src="{%rplot%}2015-7-18-r-barplot3.png{%suffix%}" alt=""></img>
此时每列的图形并列排列。
此外，barplot函数中还包含col、names.arg等参数，其中col用来控制图像的颜色、names.arg用来设置x轴标签，具体用法大家可自行探索。



原创文章如转载，请注明本文链接:<http://cognize.me/2015/07/18/r-barplot/>