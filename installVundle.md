title: 使用vundle进行插件管理
date: 2015-04-02 21:34:09
tags: vim
---
注：本文为转载，原文地址：*http://www.jianshu.com/p/mHUR4e*
vundle是一款用于管理vim插件的插件。在Linux下，vundle的安装方法如下：
###**1.　安装vim（如果你还没有安装的话）**
###**2.　在home目录下创建.vim文件夹和.vimrc文件**
###**3.　下载安装vundle**
<!--more-->
<pre><code>
$ git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
</code></pre>
###**4.　编辑如下内容到.vimrc文件**
<pre><code>
set nocompatible               " be iMproved
 filetype off                   " required!
 set rtp+=~/.vim/bundle/vundle/
 call vundle#rc()
 " let Vundle manage Vundle
 " required! 
 Bundle 'gmarik/vundle'
 " My Bundles here:
 &#35;以后你想安装什么插件可以写在下面
 "
 " original repos on github 
 &#35;如果你的插件来自github，写在下方，只要作者名/项目名就行了
 Bundle 'tpope/vim-fugitive' #如这里就安装了vim-fugitive这个插件
 Bundle 'Lokaltog/vim-easymotion'
 Bundle 'rstacruz/sparkup', {'rtp': 'vim/'}
 Bundle 'tpope/vim-rails.git'
 " vim-scripts repos
 &#35;如果插件来自 vim-scripts，你直接写插件名就行了
 Bundle 'L9'
 Bundle 'FuzzyFinder'
 " non github repos
 &#35;如使用自己的git库的插件，像下面这样做
 Bundle 'git://git.wincent.com/command-t.git'
 " git repos on your local machine (ie. when working on your own plugin)
 Bundle 'file:///Users/gmarik/path/to/plugin'
 " ...
 filetype plugin indent on     " required!
 &#35;下面是 vundle的一些命令代会会用到
 "
 " Brief help
 " :BundleList          - list configured bundles
 " :BundleInstall(!)    - install(update) bundles
 " :BundleSearch(!) foo - search(or refresh cache first) for foo
 " :BundleClean(!)      - confirm(or auto-approve) removal of unused bundles
 "
 " see :h vundle for more details or wiki for FAQ
 " NOTE: comments after Bundle command are not allowed..
 &#35;这里可以写一些你自己的配置</code></pre>
###**5.　安装你的插件**
（1）保存退出当前的vim
（2）重新打开vim，输入命令:BundleInstall,然后就开始安装你的插件了。
###**6.　如何移除插件**
（1）编辑.vimrc文件移除的你要移除的插件行
（2）保存退出当前的vim
（3）重新打开vim，输入命令:BundleClean。

