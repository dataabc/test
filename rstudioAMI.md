layout: post
title: 利用Amazon EC2解决RStudio中文乱码问题
tags: [R,RStudio,Amazon EC2]
filename: rstudioAMI
date: 2015-08-07 17:05:06
keywords: R,RStudio,Amazon EC2,乱码
description:
---
最近，喜迎Windows升级，笔记本从win8.1升到了win10，win10虽然有着酷炫的外观以及高质量的性能，但是某些工具仍然出现了不兼容的情况。就是其中一个。我安装的是最新版的RStudio(0.99.467版)，在安装时安装界面就是乱码，凭着超强的第六感，完成了安装，但是中文却是乱码。举个例子：
<!--more-->输入：> print(“R语言”)
输出：[1] “RÓïÑÔ”
网上的方法如：Tools—>Global Options—>Default text encoding—>UTF-8都试了，无效。方法各种无效，RStudio各种乱码，真是万念俱灰啊{% emoji-block %}:sob::sob::sob:{% endemoji-block %}。
后来经大神 [Ryo Eng®](http://cos.name/cn/profile/ryo/ "Ryo Eng®")帮助，发现了Amazon EC2可以解决RStudio问题。说白了就是，因为我的电脑系统问题，不能正常使用RStudio，但是我们可以通过Amazon EC2使用其它系统正常的电脑运行RStudio。
Amazon EC2（EC2，Elastic Compute Cloud）是一个让使用者可以租用云端电脑运行所需应用的系统。EC2借由提供Web服务的方式让使用者可以弹性地运行自己的Amazon机器映像档，使用者将可以在这个虚拟机器上运行任何自己想要的软件或应用程式。提供可调整的云计算能力。它旨在使开发者的网络规模计算变得更为容易。
需要提前说明的是，本教程使用的是Amazon EC2的免费版，新注册用户可以免费套餐，免费期为一年，一年之后会根据用户的使用量收费。如果各位介意使用一年后的收费问题，后面的部分就没必要看了，可以再去寻找其它方法。关于Amazon EC2的注册非常简单，步骤如同我们平常注册账号一样，如果不懂，请自行google。
利用Amazon EC2解决RStudio中文乱码问题具体步骤如下：
1.假设你已经成功注册了Amazon EC2，那么呈现在你面前的应该是如下画面：
<img src="{%rplot%}RStudioAMI-2015-8-7-1.png{%suffix%}" alt=""></img>
2.点击"EC2"链接，进入“EC2控制面板”界面。
<img src="{%rplot%}RStudioAMI-2015-8-7-2.png{%suffix%}" alt=""></img>
3.点击“启动实例”。因为当前我们还没有创建实例，所以会提示要我们创建实例，点击“社区AMI”，在搜索框里输入“RStudio”,按回车键，系统就会列出所有包含RStudio软件的系统，这里我选择第四个（因为它的RStudio版本是最新的），单击选择，进入“选择实例类型”界面。
<img src="{%rplot%}RStudioAMI-2015-8-7-3.png{%suffix%}" alt=""></img>
4.这里我选择第一个——t2.micro（因为它是免费的），单击“下一步”，进入“配置实例”界面。
<img src="{%rplot%}RStudioAMI-2015-8-7-4.png{%suffix%}" alt=""></img>
5.单击“下一步”，进入“添加存储”界面。
6.单击“下一步”，进入“标签实例”界面
7.单击“下一步”，进入“配置安全组”界面。安全组名称写“RStudio”，类型选"HTTP"，会出现警告信息，忽略之，点击"启动和审核"，进入"审核"界面。
<img src="{%rplot%}RStudioAMI-2015-8-7-7.png{%suffix%}" alt=""></img>
8.点击"启动"。
<img src="{%rplot%}RStudioAMI-2015-8-7-8.png{%suffix%}" alt=""></img>
9.会弹出对话框，让用户选择密钥，选择"在没有密钥对的情况下继续"，选上"我确认无法连接到此实例，除非我已经知道内置于AMI中的密码"，点击"启动实例"启动实例。
<img src="{%rplot%}RStudioAMI-2015-8-7-9.png{%suffix%}" alt=""></img>
10.点击"查看实例"查看实例。
<img src="{%rplot%}RStudioAMI-2015-8-7-10.png{%suffix%}" alt=""></img>
11.如下，就是实例的详细信息，不过我的大部分信息都被我划掉了，你们看不到，你们看不到{% emoji-block %}:ghost:{% endemoji-block %}，下图中的"共有DNS"值是一个网址，转到该网址，就进入了RStudio登录界面。
<img src="{%rplot%}RStudioAMI-2015-8-7-11.png{%suffix%}" alt=""></img>
12.第一次登录默认的Username和Password都是"rstudio"，输入之，登录。
<img src="{%rplot%}RStudioAMI-2015-8-7-12.png{%suffix%}" alt=""></img>
13.登录成功就会出现RStudio界面，看着很像本地的RStudio，但它只需要浏览器就可以运行了，不需要安装R,不需要安装RStudio。很简单是不是{% emoji-block %}:sunglasses:很方便是不是:sunglasses:{% endemoji-block %}。
<img src="{%rplot%}RStudioAMI-2015-8-7-13.png{%suffix%}" alt=""></img>
14.建议修改登录密码。选中"passwd()"，点击"Source"，按照提示修改登录密码，重新登录，试一下中文：
输入：> print(“我很聪明是不是？”)
输出：[1] “是的，你很聪明”
输出是中文有木有{% emoji-block %}:hankey:{% endemoji-block %}，没有乱码有木有{% emoji-block %}:relaxed:{% endemoji-block %}
15.Enjoy it{% emoji-block %}:clap::clap::clap:{% endemoji-block %}
参考文章：[RStudio Server Amazon Machine Image (AMI)](http://www.louisaslett.com/RStudio_AMI/ "RStudio Server Amazon Machine Image (AMI)")

原创文章如转载，请注明本文链接:<http://www.cognize.me/2015/08/07/{{ filename }}>