layout: post
title: hexo禁用特定文章的评论（论做笔记的重要性）
tags: hexo
filename: hexoComment
date: 2014-11-06 16:15:41
keywords: hexo
description:
---
今天，看到有网友问我如何禁用hexo特定博客的评论功能，因为我以前用过一次该功能，问了回答他，我凭着记忆中的代码专门试了该功能，可是死活不能禁止评论。想找以前的文档也没找到，google了半天也没有找到答案。最终，还是凭着自己的猪脑子记了起来。<!--more-->
方法如下，只要在markdown的题头加入comments: false即可。如，你的原文可能如下：
     ```markdown
title: 标题
date: 2014-11-06 20:46:29
---
正文
```
改成如下的格式即可：
```markdown
title: 标题
date: 2014-11-06 20:46:29
comments: false
---
正文
```
PS:博客文章在hexo\source\_posts路径下，那些.md文件就是我们的博客文件

原创文章如转载，请注明本文链接:<http://www.cognize.me/2014/11/06/{{ filename }}>