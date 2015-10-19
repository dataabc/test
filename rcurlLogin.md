title: 利用R包RCurl登录新浪微博
date: 2015-07-21 17:00:40
tags: R
keywords: R, R语言, RCurl, 登录新浪微博,登录微博,模拟登录
description: 利用R包RCurl模拟登录新浪微博
---
准备工作

在火狐浏览器上安装插件“Live http headers”，重启浏览器。
在火狐浏览器上手动登录新浪微博。
手动成功登录后，鼠标右键单击“查看页面信息”，弹出如下信息：
<!--more-->
<img src="{%rplot%}2015-7-21-RCurlLogin.png{%suffix%}" alt="弹出框"></img>
选择“Headers”,点击“save as”，将内容保存为"weibo"。打开下载好的"weibo"，你会发现内容分为
两部分，即“Request Headers”和“Response Header”。这里我们只需要“Request Headers”的信息，
将内容：
<pre>
Host: xxx
User-Agent: xxx
Accept: xxx
Accept-Language: xxx
Accept-Encoding: xxx
Referer: xxx
Cookie: xxx
Connection: xxx
</pre>
修改成程序需要的格式即可，具体形式在代码中会详述。

Coding
<pre>
require(RCurl)
myHttpheader<- c(
"Host"="xxx",
"User-Agent"="xxx",
"Accept"="xxx",
"Accept-Language"="xxx",
"Accept-Encoding"="xxx",
"Referer"="xxx",
"Cookie"="xxx",
"Connection"="xxx"
)#本段代码对应“weibo”文件中的“Request Headers”，“xxx”换成大家文件中的真实值
d =debugGatherer()
cHandle<- getCurlHandle(httpheader=myHttpheader,followlocation=1,
          debugfunction=d$update,verbose=TRUE)
temp<- getURL("http://d.weibo.com/",curl=cHandle,.encoding="gbk")
grep("yourWeiboName",temp)#"yourWeiboName"请替换成大家真实的微博用户名，大小写一定要一致
</pre>
运行上述代码，如果登录成功，会返回结果“1”，否则为“integer(0)”。
当然，本代码也可以用来登录其它网站，方法相同，大家可以自己尝试。
参考文章：*http://cos.name/cn/topic/17816/*
*http://www.xueningzhu.com/用rcurl登录人人网/*


原创文章如转载，请注明本文链接:<http://cognize.me/2015/07/21/rcurlLogin/>