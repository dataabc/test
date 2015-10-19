layout: post
title: 用emacs的org-mode写日记
tags: emacs
filename: emacsorg-modeNote
date: 2014-09-24 15:09:16
keywords: emacs
description:
---
在配置文件中加入如下代码：
<!--more-->
```html
(define-key global-map "\C-cc" 'org-capture)

(setq org-capture-templates
      '(("t" "Todo" entry (file+headline "~/doc/org/task.org" "Tasks")
         "* TODO %?\n %i\n %a")
        ("j" "Journal" entry (file+datetree "~/doc/org/journal.org")
         "* %?\nEntered on %U\n %i\n %a")))
```

将代码中的.org文件替换成自己的文件目录即可。

然后在emacs中按下C-c c即可出现选择界面，选择“j”，就会出现文字输入框，输入日记的内容，
按C-c C-c，日记就自动保存在了我们的文件中，按照上面的配置，我的日记会保存在journal.org
文件中。并且日记是按时间分类的，非常方便。
原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/09/24/{{ filename }}>