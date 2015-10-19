title: 安装最新版hexo(hexo 3)
date: 2015-07-27 20:55:40
tags: hexo
keywords: hexo, hexo3,安装hexo
description: 安装最新版hexo，即hexo 3
---
虽然本篇的主题是安装hexo 3，但是因为某些插件及符号无法在hexo中使用，如emoji表情插件无法使用；&#123;% %&#125;符号无法使用，致使无法用 [《Hexo图床管理》](http://cognize.me/2015/07/22/tuchuang/ "《Hexo图床管理》")的方法进行图床管理。因此我重新退回了hexo 2.8.3版本。但是，事物总是在发展，沉舟侧畔千帆过，病树前头万木春，新版本肯定会取代旧版本，如果各位想要安装最新版的hexo，请继续往下看。
<!--more-->
事实上，hexo官网给出了最新版hexo的安装教程：
```shell
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
在shell中运行上述代码就可以安装最新版的hexo，但是当我们将写好的博客上传到github或gitcafe等空间时（即运行hexo d时），可能会出现“ERROR Deployer not found: github”的错误，解决方法如下：
1. 将我们hexo根目录下的config文件中的如下代码：
```yaml
deploy:
  type: github
  repository: xxxxx
  branch: xxxx
```用git替换type中的值github
2.运行npm install hexo-deployer-git --save
3.最后运行hexo d，就可以将我们的博客提交到博客托管空间。


原创文章如转载，请注明本文链接:<http://cognize.me/2015/07/27/installhexo3/>