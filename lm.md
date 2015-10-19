title: R语言之lm函数
date: 2014-11-19 23:54:12
tags: R
keywords: R, R语言, lm, lm函数
description: R语言之lm函数
---
<img src="{%view%}2014-11-19-lm.jpg{%suffix%}" alt=""></img>
&nbsp;&nbsp;&nbsp;&nbsp;**lm()**是R语言中经常用到的函数，用来拟合回归模型。它是拟合线性模型最基本的函数。
&nbsp;&nbsp;&nbsp;&nbsp;**lm()**格式如下：
>    myfit<-lm(formula,data)

&nbsp;&nbsp;&nbsp;&nbsp;其中，formula指要拟合的模型形式，data是一个数据框，包含了用于拟合模型的数据。结果对象（本例中是myfit）存储在一个列表中，包含了所拟合模型的大量信息。表达式（formula）形式如下：
>   Y~X1+X2..Xn

&nbsp;&nbsp;&nbsp;&nbsp;举个例子，我们依次在R中输入以下代码：
> a<-c(1,2,3,4,5)
> b<-c(2,4,6,8,10)
> mydata<-data.frame(a,b)

 &nbsp;&nbsp;&nbsp;&nbsp;上面的意思是我们分别定义了a,b两个向量，并赋值，然后把它们都加到了数据框mydata中。
&nbsp;&nbsp;&nbsp;&nbsp;我们想要知道向量a和向量b之间有什么关系，虽然我们一眼就能看出向量b对应的数值是a的2倍，但是计算机并不知道啊。我们仅仅以一个简单的例子来说明问题。
&nbsp;&nbsp;&nbsp;&nbsp;为了弄清楚，我们然后输入以下代码：
> myfit<-lm(a<-b)
> summary(myfit)

&nbsp;&nbsp;&nbsp;&nbsp;然后系统就会打印出myfit的一些参数，其中包括以下内容：
>   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Estimate
>(Intercept)1.12347e-15
>b          5.00000e-01

&nbsp;&nbsp;&nbsp;&nbsp;这里的1.12347e-15表示1.12347乘以10的-15次方，是一个很小的数值，同理，5.00000e-01表示的就是5.00000乘以10的-1次方，为0.5.
所以a,b的关系可表示为：

> a=0.00000000000000112347+0.5*b

&nbsp;&nbsp;&nbsp;&nbsp;预测值与实际值很相似。这里仅仅是一个简单的例子，它还可以扩展到多个参数，具体的情况大家可以探索。
&nbsp;&nbsp;&nbsp;&nbsp;因此本人正在读《R语言实践》，所以引用了书中的很多内容，在此说明。
&nbsp;&nbsp;&nbsp;&nbsp;最后，如果各位发现本文有任何错误，欢迎指正，谢谢阅读。


原创文章如转载，请注明本文链接:<http://cognize.me/2014/11/19/lm/>