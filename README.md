# test
<img src="http://7xknyo.com1.z0.glb.clouddn.com/view/2015-7-22-tuchuang.jpg?imageView2/1/w/751/h/464" alt=""></img>
好久没有访问自己的博客了，当最近打开时，猛然一惊，博客中的图片都为无法显示的状态，刚开始以为是自己的网速不行，后来在写文章添加图片时才发现，我图床所在的存储平台进行了改版，以前的图片链接地址都失效了，导致我博客中的图片无法显示。以前的博客可是有很多图片的，要是一个个的更改图片地址真的是个大工程。
<!--more-->
后来，终于找到了方法(注意：该方法只在hexo 2版本时有效)。
Hexo支持Markdown写作，所以我们在为博客添加图片时，都是采用如下格式：
\!\[](<http://xxx.com/bucketName/pictureName.jpg>)或者&lt;img src="<http://xxx.com/bucketName/pictureName.jpg>" alt="">&lt;/img>
从上面可以看出，我们的地址包含两部分，一部分是图片所在仓库的地址（<http://xxx.com/bucketName/>）,另一部分是图片的名字（pictureName.jpg），仓库地址是我们注册某个存储平台时该平台提供的，而后一部分是我们真实的图片名字，是我们自己提供的。
一旦该存储平台失效，我们的图片链接也会跟着失效。然后，我们会寻找新的可用的存储平台，然后将图片迁移过去。怎么迁移呢？
1.上传我们的图片；
2.将我们博客中的图片地址改为新的地址。
但是，问题是，如果我们博客中有很多很多图片，难道我们要一个文档一个文档的修改地址吗？无疑，这样做工作量是很大的。
但是，如果这样呢：
1.我们先在博客中定义图片仓库的地址（如：<http://xxx.com/bucketName>）,并将其复制给某个全局变量pictureAdress；
2.我们在添加图片时地址使用pictureAdress+pictureName.jpg的形式;
一旦，我们使用的存储平台失效了，即pictureAdress目前的值失效了，我们只需要修改pictureAdress，赋予它新的图片仓库地址就可以啦。虽然这个过程也要上传图片，但是在更改文档时，只需要修改pictureAdress就可以了，并不需要一个图片地址一个图片地址的修改了，是不是简单很多了。
具体方法如下：
在本地的hexo中，找到你现在所用的主题目录，打开其中的”scripts“文件夹，然后创建一个.js文件（文件名任意，如mypicture.js等），在里面添加如下内容：
<pre>
hexo.extend.tag.register('plant', function(args, content){
  var id = args[0];
  return 'http://plant.xxx.com';
});
hexo.extend.tag.register('animal', function(args, content){
  var id = args[0];
  return 'http://animal.xxx.com';
});
</pre>
注意：上面的”<http://plant.xxx.com>“和”<http://animal.xxx.com>“即代表了pictureAdress的值，上面只是写了两个函数，一个代表某存储中植物图片库的地址，另一个代表了某存储中动物图片库的地址，大家可以根据自己的情况对库的数量进行增删。在我们写文章添加图片时，要加上这个库地址，比如我想添加一个苹果树的图片，它在存储平台的真实地址是"<http://plant.xxx.com/apple.jpg>"，为了显示该图片，我们应该这么写：
<pre>
&lt;img src="&#123;%plant%&#125;/apple.jpg" alt="">&lt;/img>
</pre>
因为&#123;%plant%&#125;代表了<http://plant.xxx.com>，&#123;%plant%&#125;/apple.jpg就代表了"<http://plant.xxx.com/apple.jpg>"这个真实地址。一旦我们使用的存储平台失效了，我们只需要将图片上传到新平台，然后将&#123;%plant%&#125;的值改为新平台给我们的地址<http://plant.yyy.com>就可以啦。
注意：因为hexo3不支持&#123;% %&#125;的写法，因此该方法只在hexo 2时有效。
参考文章：*http://www.winterland.me/2013/11/bae-imbed/*

