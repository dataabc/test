title: Q-Q图
date: 2014-11-21 23:45:20
tags: R
---
<img src="{%view%}2014-11-21-qq.jpg{%suffix%}" alt=""></img>
&emsp;&emsp;Q-Q图: 比较已知样本的分布和猜测分布的图, 猜测的概率分布通常为正态分布。
比如猜测样本是正态分布的，则有：
假设样本有n个，则用标准正态分布函数获取n个分位值。
取法:
<!--more-->
<img src="{%rplot%}/2014-11-21-qq-2.jpg{%suffix%}" alt=""></img>
&emsp;&emsp;将样本和这个n个值都从小到大排列，一一对应。这样就能获得n对坐标。标准正态分布函数生成的值作x，样本值作y，则可在直角坐标系中绘制出n个点。
&emsp;&emsp;如果所有点连成的线越接近 直线 y=x,那么就能说样本分布越近似猜测的分布。

原文地址：*http://blog.csdn.net/rav009/article/details/38019267*
