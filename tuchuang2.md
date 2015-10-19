layout: post
title: Hexo图床管理(二)
tags: [hexo,图床]
filename: tuchuang2
date: 2015-08-03 15:48:20
keywords: hexo,图床
description:
---
<img src="2015-8-3-tuchuang2.jpg" alt=""></img>
前一段时间写了一篇[《Hexo图床管理》](http://www.cognize.me/2015/07/22/tuchuang/ "《Hexo图床管理》")，今天终于派上了用场，今天刚从某存储转到七牛云存储，还有很多话说。
<!--more-->
[《Hexo图床管理》](http://www.cognize.me/2015/07/22/tuchuang/ "《Hexo图床管理》")的大体思路是在我们主题目录下的”scripts“文件夹中创建一个.js文件（文件名任意，如mypicture.js等），在里面添加如下内容：
```javascript
hexo.extend.tag.register('plant', function(args, content){
  var id = args[0];
  return 'http://plant.xxx.com';
});
```
然后，以后写文章插入图片时不再使用```markdown
![](http://plant.xxx.com/pictureName.jpg)
```的形式，而是以```html
<img src=”&#123;%plant%&#125;/pictureName.jpg” alt=””></img>
```的形式替代之，以后如果更换图床，只需要更改那个.js文件就可以，不明白的同学可以去看一下[《Hexo图床管理》](http://www.cognize.me/2015/07/22/tuchuang/ "《Hexo图床管理》")。
现在，我把图床搬家到了七牛云存储，发现了更多可以优化的地方。
七牛提供了“图片处理”的功能，可以为我们的图片瘦身，还可以增加我们的水印，真的非常方便。要知道，我以前使用的原图大小一般都在2M左右，甚至更大，但是通过定制图片的格式，大小能减小到几十KB，大大提高了博客的访问速度。
网上很多关于七牛图片处理的教程都是新建图片样式，自定义图片的分辨率、图片质量等信息，假设新建的样式叫"newStyle"，我们要使用新样式只需要在原图片地址后加入"-newStyle"就好，例如，我之前插入图片都是如下格式：
```html
&lt;img src="&#123;%plant%&#125;/apple.jpg" alt="">&lt;/img>
```
现在，为了使用新样式，我必须使用如下方式插入图片：
```html
&lt;img src="&#123;%plant%&#125;/apple.jpg-newStyle" alt="">&lt;/img>
```
这种做法不错，但是对我来说有几个弊端：
1.七牛云存储支持链接后加“-样式名”的格式，但是很多图床并不支持，如果你想以后更换其它图床的话，为了图片正常显示，你必须把每个链接后的“-样式名”去掉，非常麻烦；
2.万一以后你突然不满意现在的样式，你很可能要再新建样式，然后将文章的旧样式替换成新样式，如果你希望很多图片都用这种样式，还是要一篇篇的修改，非常麻烦。
为了解决上述问题，我们可以再在.js文件中添加如下代码：
```javascript
hexo.extend.tag.register('suffix', function(args, content){
  var id = args[0];
  return '?imageView2/1/w/751/h/464';
});

```
其中，751代表新建图片的宽度(px)，464代表图片的高度(px)，大家可以根据自己的喜好设定。
然后使用如下代码插入图片：
```html
&lt;img src="&#123;%plant%&#125;/apple.jpg&#123;%suffix%&#125;" alt="">&lt;/img>
```
这样输出的图像就是一副宽751高464的图像，如果大家想要输出原图或者迁入其它图床，只需要return ''即可。
这样，大家就可以通过更改.js文件随心所欲的控制输出图片的大小格式了。当然，大家也可以在.js文件中定义多种样式，根据图片不同调用不同的格式。
如何通过.js文件添加水印我还没有找到方法，相信聪明的各位一定会找到。更多详细的图片格式设置，大家请参考：<a href="http://developer.qiniu.com/docs/v6/api/reference/fop/image/imageview2.html" rel="nofollow">七牛基本图片处理</a>。
另外，安利一下七牛云存储，确实不错，如果大家仅仅在找图床，强力推荐之。如果大家还没有七牛的账号，欢迎通过[我的邀请链接](https://portal.qiniu.com/signup?code=3lftkxs9jj42a)注册{% emoji smile %}，如果你成为标准会员，我将得到5G的下载流量{% emoji blush %}。
原创文章如转载，请注明本文链接:<http://www.cognize.me/2015/08/03/{{ filename }}>