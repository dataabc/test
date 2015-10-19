title: R语言读取EXCEL文件的各种方法
date: 2015-06-29 21:27:31
tags: R
keywords: R, R语言, R读EXCEL, EXCEL
description: R语言读取EXCEL文件的各种方法
---
注：本文为转载，原文地址：*http://www.biostatistic.net/thread-35-1-1.html*

R语言读取EXCEL文件的各种方法
最近初学R语言，在R语言读入EXCEL数据格式文件的问题上遇到了困难，经过在网上搜索解决了这一问题，下面归纳几种方法，供大家分享：
<!--more-->
第一：R中读取excel文件中的数据的路径：

假定在您的电脑有一个excel文件，原始的文件路径是：D:\work\data\1，如果直接把这个路径拷贝到R中，就会出现错误，原因是：\是escape character（转义符），&#92;&#92;才是真正的\字符，或者用/因此，在R中有两种方法读取该路径：
1：在R中输入一下路径：D:&#92;&#92;work&#92;&#92;data&#92;&#92;1
2：在R中输入一下路径：D:&#92;&#92;work&#92;&#92;data&#92;&#92;1

第二：R中读取excel文件中的数据的方法：

read.table(),read.csv(),read.delim()直接读取EXCEl文件时，都会遇到一下问题：“在读取‘.xls’的TableHeader时遇到不完全的最后一行”。解决的方法有以下几种：假如文件1.1中是一个6乘以2的矩阵，元素为：
  
1 23 
2 24 
3 25 
4 26 
5 27 
6 28 

方法1：xls另存为csv格式然后用read.csv：
具体过程如下：
```r
> data<-read.csv("D:\\work\\data\\1.csv")
> data
  X1 X23
1  2    24
2  3    25
3  4    26
4  5    27
5  6    28
> data<-read.csv("D:\\work\\data\\1.csv",header = F)
> data
  V1    V2
1  1 23333
2  2    24
3  3    25
4  4    26
5  5    27
6  6    28
> data<-read.csv("D:\\work\\data\\1.csv",header = T)
> data
  X1 X23333
1  2    24
2  3    25
3  4    26
4  5    27
5  6    28
```
也就是说header = T（TURE）是默认的状态，在这默认状态下，输出的data矩阵是一个5乘以2的矩阵，第一行作为了data的名字，如果header = F（FALSE），则会现实原始的矩阵结果。
  
方法2：xls另存为txt格式然后用read.table：
如例子所示：
```r
> data<-read.table("D:\\work\\data\\1.txt",header = T)
> data
  X1 X23
1  2  24
2  3  25
3  4  26
4  5  27
5  6  28
> data<-read.table("D:\\work\\data\\1.txt",header = F)
> data
  V1 V2
1  1 23
2  2 24
3  3 25
4  4 26
5  5 27
6  6 28
```

方法3：打开EXCEL，全选里面的内容，点击复制，然后在R中输入一下命令：

data <- read.table("clipboard", header = T, sep = '\t')
结果如下所示：
```r
> data <- read.table("clipboard", header = T, sep = '\t')
> data
  X1 X23
1  2  24
2  3  25
3  4  26
4  5  27
5  6  28
> data <- read.table("clipboard", header = F, sep = '\t')
> data
  V1 V2
1  1 23
2  2 24
3  3 25
4  4 26
5  5 27
6  6 28
```
使用这种方法的时候一定要注意复制！剪切板里面没有内容是无法运行的！以上是三种方法，如果还有别的更好的，请大家补充，谢谢！