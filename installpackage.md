title: R语言之本地安装R包
date: 2014-11-20 22:59:01
tags: R
keywords: R, R语言, 安装R包 ,本地安装R包
description: R语言之本地安装R包
---
<img src="{%view%}2014-11-20-installpackage.jpg{%suffix%}" alt=""></img>
&emsp;&emsp;因为有时，我们的计算机可能没有联网，不能通过网络的方式安装R包，我们只能本地安装。
&emsp;&emsp;本地安装（windows版）的步骤如下：
1.下载我们要安装的包文件。
&emsp;&emsp;我们可以从R语言的网站（*http://cran.r-project.org*）下载包文件，也可以直接google搜索关键字，找到下载地址。
2.将包文件(xxx.zip)安装到R上。
&emsp;&emsp;打开R的程序（废话），你会发现在R界面的上方有一对功能按钮，点“Packages”选择“Install packages(s) from local zip files”，然后我们找到我们下载到的R包，双击之，安装完成。
3.每次在使用该包时，别忘了加载该包（library(xxx)即可）。


原创文章如转载，请注明本文链接:<http://cognize.me/2014/11/20/installpackage/>