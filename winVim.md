title: windows下gvim中文乱码解决方案
date: 2015-04-02 21:20:36
tags: vim
---
注：本文为转载，原文地址：*<http://rongmayisheng.com/post/windows下gvim中文乱码解决方案>*

网罗了一些网上的解决windows下gvim中文乱码的解决方案，都试了一遍，可惜都不能完全解决我的所有问题，最后我综合一下网上的两种方案，得到了最后完全解决我的中文乱码问题的方案，配置很简单，就是把下面的配置直接copy到C:Program Files (x86)Vim_vimrc文件的开头。（下面第一行配置可以把gvim的字符弄得好看一点）
<!--more-->
```xml
set guifont=Consolas:h12:cANSI
set encoding=utf-8
set fileencodings=utf-8,chinese
set termencoding=utf-8
if has("win32")
set fileencoding=chinese
else
set fileencoding=utf-8
endif
"解决菜单乱码
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
"解决consle输出乱码
language messages zh_CN.utf-8
```
---
###更新：
上面的代码是在win8.1测试的，可以解决乱码问题，现在我的系统是win10，添加上述代码仍然会有乱码，后来终于找到了解决方法，如下：
再在上述代码下添加字体设置即可，即：
```xml
"设置字体
"set guifont=楷体:h10:cGB2312
set guifont=KaiTi:h10:cGB2312
```
