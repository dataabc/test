layout: post
title: emacs的org-mode下查看TODO、DONE等事件列表
tags: emacs
filename: emacsorg-modeCheck
date: 2014-09-14 14:49:45
keywords: emacs
description:
---
昨天想练习一下org-mode的时间管理功能，于是就写了几个TODO事件，按照网上的教程，按下C-c a t，希望能查看TODO事件，结果老是显示不出来，
只显示如下两行代码：<!--more-->
              　　Global list of TODO items of type: ALL
              　　Available with `N r': (0)[ALL]
除了上述两行提示外，再也没有其它内容，不过我尝试了几次都是这个结果，于是问了[《一年成为emacs高手》](http://blog.csdn.net/redguardtoo/article/details/7222501 "《一年成为emacs高手》")的作者[redguardtoo](http://my.csdn.net/redguardtoo "redguardtoo")，经过大神的指导终于发现，原来我没有定义 org-agenda-files,于是乎搜索之，终于找到了解决问题的方法。方法如下：
###1.在.emacs中加上如下代码：

       (setq org-agenda-files (list "~/doc/org/myfile1.org"
                                  “~/doc/org/myfile2.org”  ))
注意：双引号中的地址为我所写的org文件的地址,代码中可以写多个地址，每个地址用双引号括起来，大家可以将地址换成自己的org文件地址。
因为我的emacs的配置用的是Purcell的配置，没有.emacs文件，而且如果创建了.emacs，就会将Purcell的配置给替换调，为了使用大神的配置并且可以使用org-mode,我在.emacs.d文件夹中发现了一个custom.el文件，将上述代码加入custom.el中。

###2.查询TODO事件

按下C-c a t,此时，根据提示，若输入“0 r”，列出的是所有的事件，按下“1 r”列出的是TODO事件，按下“2 r”列出的是“STARTED”事件，......以此类推，可以查看各种我们想要查看的事件。

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/09/14/{{ filename }}>