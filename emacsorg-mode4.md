layout: post
title: 只管去做—用emacs的org-mode做时间管理(4.完结)
tags: emacs
filename: emacsorg-mode4
date: 2014-09-13 14:46:07
keywords: emacs
description:
---
GTD(只管去做)是我在搜索org-mode时无意中看到的，其实也是粗粗看了一下，可能远未得精髓，但还是挺喜欢这套理论的，包括org-mode也挺合我品味，不仅用来做日常计划，还读书笔记、学习计划和学习笔记都用它了。
<!--more-->
至于我写的这份笔记，其实每篇写得都很仓促的，很大程度是为了完成任务而写的，哪位觉得写得太烂的请见谅。也许后续我会根据理解的加深重写一下。

关于GTD，原书和更多的资料可以从褪墨中找到，如果你对这个感兴趣，还是建议你去通读原著。至于org-mode，我觉得还是很强大的，自己用M-x org-info可看帮助，各位尽可以发挥自己的创造力和想象力来灵活运用。

当然你还可以将GTD结合其它理论来完善自己的系统，比如结合富兰克林自我修炼表格，将其第一列改成你每日反省或每周反省的项目。至于要反省的内容，就看你自己了，比如你要改变你自私残忍的性格(开玩笑了)，或者你要改变作息，那都可以写上。另外也可像富兰克林一样，每段时间应特别重点关注其中一项，等等。

最后说一下org-mode是可以导出为html或text的(还有xoxo格式其实也是html，自己试试看吧)。但默认的html样式实在不怎样，好在可自定义，先在.emacs上加：
```html
(defcustom org-export-html-style
"" ""
  :group 'org-export-html
  :type 'string)
```
然后输出的html就可以用自定义的css了，以下只是个示例：
wheer.css:
```html
html {font-family: Times, serif;font-size: 12pt;}
.title,.author { display:none; }
.todo { color: red; }
.done { color: green; }
.timestamp { color: grey }
.timestamp-kwd { color: CadetBlue }
.tag { background-color:lightblue; font-weight:normal }
.target { background-color: lavender; }
pre {border: 1pt solid #AEBDCC;background-color: #F3F5F7;
    padding: 5pt;font-family: courier, monospace;}
table { border-collapse: collapse; }
td, th {vertical-align: top;border: 1pt solid #ADB9CC;}
h2{ margin: 5px 0 10px 0;background-color: #AEC5CE; font-size:1.5em;}
h3{ margin: 0px 0px 5px 0;padding: 5px 5px 5px 10px;
    font-size:1.2em; border-top: solid 1px #9AB7C2;
    border-bottom: solid 1px #9AB7C2; font-variant: small-caps; }
h4{ color: black; margin: 3px 0px 5px 0px;
  padding: 3px 5px 3px 15px; font-size: 1em;}
h5{ color: black; margin: 3px 0px 3px 0px;
  padding: 3px 5px 3px 25px; font-size: 1em;}
p{ margin:0px 10px 0px 18px; }
```

转载地址：http://blog.chinaunix.net/uid-342902-id-2416129.html