layout: post
title: emacs的org-mode模式的链接
tags: emacs
filename: emacsOrg-modeLink
date: 2014-09-10 11:08:00
keywords: emacs
description:
---
关于org-mode的链接，有以下几种方式
1.自动链接<!--more-->
    对于符合链接规则的内容，org-mode会自动将其视为链接，如
http://www.astro.uva.nl/~dominik  
file:/home/dominik/images/jupiter.jpg 

在链接后加::可对其定位，如：
file:~/code/main.c::255　　进入到 255 行
file:~/xx.org::My Target　　找到目标‘<<My Target>>’
file:~/xx.org/::#my-custom-id　　查找自定义 id 的项

 2.显示链接
例如：你想链接到
&#42;&#42; 标题2        (注意：&#42;和文字之间有空格，空格数量大于等于一即可)
你可以这么写：
[[标题2]]
上述的[[标题2]]即变成了链接,你也可以这么写：
[[标题2][标题2的描述]]
这样更详细

3外部链接
&lt;&lt;flagname&gt;&gt;：改标记为链接的标记符，其中flagname是我为标记取的名字，你也可以取其它名字
[[flagname]]：改标记为链接记号，当用户输入完改标记后，它就会变成一个链接，链接到名字和它相同的标记处，因为[[flagname]]和&lt;&lt;flagname&gt;&gt;有相同的名字，故点击[[flagname]]生成的标记就可以转到&lt;&lt;flagname&gt;&gt;处。当然，我们也可以这样写：[[flagname][flagname的描述]]。

注：本文参考自：http://higrid.net/c-art-orgmode_basic.htm