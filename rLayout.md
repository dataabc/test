layout: post
title: R语言layout函数学习笔记
tags: R
filename: rLayout
date: 2014-11-15 16:21:53
keywords: R
description:
---
今天学习了R的layout()函数。该函数的一般形式为layout(mat)。对照英文的R文档，这个mat看了好些晨光也没明白是怎么回事。它是否这样说的： <!--more-->    
mat: 
a matrix object specifying the location of the next N figures on the output device.  Each value in the matrix must be or a positive integer.  If N is the largest positive integer in the matrix, then the integers {1, ..., N-1} must also appear at least once in the matrix.
主要是对这个the next N figures不明白。经过一番google终于搞清楚了。mat元素的数量决定了一个output device被等分成几份，为了方便我把一份叫做一个格子。这样mat内的每个元素根据他们的行列序号对应一个格子。而元素本身的值代表它属于第几个figure。举例来看。layout(matrix(c(1,2,3,0,2,3,0,0,3),nr=3)) matrix有9个元素，具有这样的形式：
       [,1] [,2] [,3]
[1,]    1    0    0
[2,]    2    2    0
[3,]    3    3    3
把这个矩阵传入layout函数，我们就能得到这样的output device
<img src="{%rplot%}2014-11-15-R-layout.jpg" alt=""></img>
如此，figure1占据了左上角的一个格子，第二行的前两个格子属于figure2，figure3占满最下一行的三个格子。为了醒目，figure1，2，3分别标记了黄绿红颜色。在输出figure时，会按照先后顺序，将figure绘制在与其顺序相同的区域内。在我的这个例子内，就是按照黄色区域，绿色区域，红色区域的顺序。当然你可以通过更改matrix，使得各个figure按照你需要出现在不同区域，不一定按照从上到下或从左到右的传统顺序。

转载地址：http://wangqian-bio.blog.163.com/blog/static/416609212012521114111142/