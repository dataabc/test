title: R语言读取XML文件
date: 2015-07-12 17:46:30
tags: R
keywords: R, R语言, 读取XML ,R读取XML
description: R语言读取XML文件
---
首先要加载需要的R包，没有安装的童鞋要提前安装。
```r
> library(RCurl)        # 加载R包
> library(XML)
```
本文以读取在线xml文件*http://www.w3school.com.cn/example/xdom/books.xml*为例。
<!--more-->
```r
> url<-"http://www.w3school.com.cn/example/xdom/books.xml"  #注，也可以为url复制本地文件的路径
> doc<-xmlTreeParse(getURL(url),useInternal = TRUE)    #获取文件
```
该xml文件中存储了很多"book"的信息，假如我们想读取第一本书的"title"的值,方法如下：
```r
> xpathSApply(doc, "/bookstore/book[1]/title", xmlValue)
```
或者
```r
> xpathSApply(doc, "//book[1]/title", xmlValue)
```
如果函数中填的是完整的节点路径（如"/bookstore/book[1]/title"），则要在节点名称前加"\";如果函数中填的不是完整节点路径（如第二种方法），路径中的第一个节点是几级节点，该节点前就要加几个"\"，因为"book"为二级节点，所以其前加两个"\"，最终的路径形式为："//book[1]/title"。因为在"bookstore"节点下有很多"book"节点，而我们想要读取的是第一步的"title"值，所以"book"节点后要加下标，即"book[1]"。如果不加下标，会读取所有book节点的title信息。

如果我们想要读取第一个"book"节点子节点"title"中属性"lang"的值，方法如下：
```r
> title<-getNodeSet(doc, "/bookstore/book[1]/title")
> lang<-sapply(title, xmlGetAttr, "lang")
```
或者  
```r
> title<-getNodeSet(doc, "//book[1]/title")
> lang<-sapply(title, xmlGetAttr, "lang")
```

原创文章如转载，请注明本文链接:<http://cognize.me/2015/07/12/rreadxml/>