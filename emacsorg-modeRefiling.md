layout: post
title: emacs之org-mode的转接（Refiling）
tags: emacs
filename: emacsorg-modeRefiling
date: 2014-09-23 15:05:17
keywords: emacs
description:
---
　　据说emacs的org-mode是最好的任务管理器，心向往之，于是最近学了一段时间。作为小白，我不敢说它是最好的，只能说
它是适合我的。<!--more-->
　　看了很多org-mode的教程，思想大体相似，就算创建几个.org的文件，如task.org、finished.org、project.org等，分别存放
要完成的任务、已完成的任务以及要做的项目等信息。比如我把一些公司的工作等任务写到了task.org中，等到有的任务完成了，
就把改任务转移到finished.org中。当初我以为是自己手动的把task.org中的那个任务剪切了，然后在打开finished.org，并将内容
粘贴到finished.org中，实现任务的转换。现在想起来，觉得自己的想法它可笑了，太低效了。
　　其实,org-mode中提供了不同任务的转接功能。我们通过快捷键可以轻松的完成同一个文件在不同标题下的转接以及在不同文件
间的转接。本功能的英文原称是Refiling，即转接。
　　关于转接功能，网上的资料很少，大都是一代而过。经过不断的寻找与尝试，我终于找到了配置的源代码，我们只需要将其拷贝
到配置文件中即可使用。如果你用的emacs中有.emacs文件，将源地貌直接拷贝到.emacs上即可。我用的是Steve Purcell的配置，
并没有.emacs文件，如果添加.emacs文件为使Steve Purcell的配置失效，但我们可以在custom.el中配置，将配置代码加入custom.el
即可。
　　配置代码如下：

代码1：
```html
(setq org-agenda-files (list "~/doc/org/inbox.org"
                             "~/doc/org/task.org"
                             "~/doc/org/finished.org"
                             "~/doc/org/project.org"))
```



代码2：
```html
; Targets include this file and any file contributing to the agenda - up to 9 levels deep
(setq org-refile-targets (quote ((nil :maxlevel . 9)
                                 (org-agenda-files :maxlevel . 9))))

; Use full outline paths for refile targets - we file directly with IDO
(setq org-refile-use-outline-path t)

; Targets complete directly with IDO
(setq org-outline-path-complete-in-steps nil)

; Allow refile to create parent tasks with confirmation
(setq org-refile-allow-creating-parent-nodes (quote confirm))

; Use IDO for both buffer and file completion and ido-everywhere to t
(setq org-completion-use-ido t)
(setq ido-everywhere t)
(setq ido-max-directory-size 100000)
(ido-mode (quote both))
; Use the current window when visiting files and buffers with ido
(setq ido-default-file-method 'selected-window)
(setq ido-default-buffer-method 'selected-window)
; Use the current window for indirect buffer display
(setq org-indirect-buffer-display 'current-window)

;;;; Refile settings
; Exclude DONE state tasks from refile targets
(defun bh/verify-refile-target ()
  "Exclude todo keywords with a done state from refile targets"
  (not (member (nth 2 (org-heading-components)) org-done-keywords)))

(setq org-refile-target-verify-function 'bh/verify-refile-target)
```

      
　　上述代码分为两部分，第一部分可以让你能够查看任务。加入第一部分后，按下C-c a t,会列从所有的任务，再按下C-c a t的基础上，再按下1-r,会
显示所有TODO的事务，按下2-r会显示所以STARTED的事务，等等，大家可以自己探索。在源代码中，大家要将那些.org文件的地址换成自己的文件
地址。
　　上述第二部分，大家可以直接拷贝，无需修改。再加入代码后，大家可以加鼠标放到一个事务上，按C-c C-w,屏幕的下方就会显示出所有.org文件名
与其事务名的组合，大家可以用左右键选择要转移到的目的地。如，我的鼠标在“** 买书”上，按下C-c C-w，用左右箭头选择“购物/（inbox.org）”，按下
回车键，就可以将当前文件中的这个“买书”项转移到inbox.org文件的“购物”项下，达到了不同文件键内容转接的目的，当然同一个文件下也可以进行转接。

参考文章：http://doc.norang.ca/org-mode.html#Refiling
