---
title: "[博客维护]Jsdelivr CDN的图片缓存更新的解决方案"
date: 2022-03-09 22:20:36
tags: [git,Github,日常学习]
categories: 博客维护
description: "[第9篇]本篇记录一下我为了让Jsdelivr CDN能及时更新我更改过的博客图片所尝试的努力和最后的解决方案。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/blog.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/9-keep-cdn-pics-updated.jpg
---

# 序言

我在我的[第二篇博文][1]中曾经提到过为了加速世界各地的人访问博客图片的速度，我们需要使用`Jsdelivr`的`CDN`服务，但`CDN`在带来一些便捷的同时也带来了`一些问题`。比如如果我们对远程仓库中的某些图片做了`修改`(而不是添加一个新的图片)，这种情况下`Jsdelivr`的缓存文件却可能`不会马上被更新`，所以我们需要使用一些方法使我们修改后的图片能实时反映在我们的网站中，本篇就记录一下我尝试的方法和最终的解决方案。

# 正文

要搞清楚图片缓存不能按时更新的主要原因，首先先要了解一下`Jsdelivr`到底是怎么运作的。我在第二篇文章里简单地介绍过他的基本原理就是将上传的资料缓存在各地的边缘服务器中，然后每次链接被请求时直接从距离请求最近的服务器中响应请求。而从`JSdelivr`的官网中我们可以看到它具体的实现方法如下图所示：

![JSdelivr工作原理图](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/post_img/infographics.png)

可以注意到`Jsdelivr`除了拥有我们之前介绍的缓存服务器以外还有一项功能，是由`亚马逊`提供的`S3云储存服务`。根据其官方的介绍：

> We use a permanent S3 storage to ensure all files remain available even if GitHub goes down, or a repository or a release is deleted by its author. Files are fetched directly from GitHub only the first time, or when S3 goes down.

可以想象他们的做法是每当`Github`中发布新的`release`之后马上将新的资产复制至`S3空间`，这样即使`GitHub崩溃`或者`原作者删除掉仓库或release`这些已经存储的文件也不会丢失，只有`S3崩溃`的时候他们才会再从`GitHub`拉数据。这个做法第一眼看就知道是利弊共存的。显然他们的做法保证了数据的可用性，但随之而来的问题就是更改数据的成本增加了，我的每次更改都要同步到S3，而似乎`Jsdelivr`在这点上做得并不好，我估计可能和他们备份和引用方式的底层逻辑有关，导致他们实时同步数据的成本非常高。

## 清除缓存

在网上看了一些[其他人的分享][3]，大多数人都会介绍使用`endpoint purge`调用`Jsdelivr`缓存清除功能的方法，来强制刷新缓存。具体用法只是在浏览器中将需要引用的`Jsdelivr`链接前的`cdn`替换为`purge`然后发送请求就会让`Jsdelivr`将该链接的缓存强制刷新。但似乎现在这个功能已经被禁用了，在`Jsdelivr`的官网上我没有看到任何类似的记录，仅仅只有[一个页面][4]表明`Jsdelivr`正在开发清除缓存的工具。

从[别的博主的博文][5]中可以看到，如果要使用前面提到的`Purge方法`可能需要向-dak@prospectone.io发邮件请求，但我自己并没有在文档中找到这句话，可能是在`Jsdelivr`的`API文档`中吧。但总之`Purge`这个方法现在也是没有那么方便了，只能看有生之年能不能等到这个官方工具出炉了，先想想还有没有别的方法。

## 引用版本号

其实一般对文件加版本号的引用方法其实非常稳定，也即：

> `https://cdn.jsdelivr.net/gh/user/repo@version/file`

但这个方法比较麻烦的地方在于，我们一般是用`Typora`来插入图片，然后使用提前设置好的`Jsdelivr`链接地址来引用图片，但`Typora`并不知道你接下来的版本号是多少，所以如果用这种方法的话你还需要在每次引用图片后再手动在每个图片链接中加入版本号，这就非常麻烦了。而[官方文档][2]提供的另一个更`consistent`的方式：

> Omit the version completely or use "latest" to load the latest one (not recommended for production usage)
> `https://cdn.jsdelivr.net/gh/jquery/jquery@latest/dist/jquery.min.js`
> `https://cdn.jsdelivr.net/gh/jquery/jquery/dist/jquery.min.js`

去掉版本号或者将版本号用`latest`替代就可以固定引用`最新版本的release`，但实际使用后发现这个方法依然不太稳定，`新release`的文件的确可以无缝访问，但如果是旧文件修改后，使用这个方法依然可能导致直接引用旧文件。`所以看起来Jsdelivr只从文件名判断一个文件是不是已经存在了S3空间中。`

## 解决办法

既然`Jsdelivr`是从`文件名`判断是否更新缓存，那么其实最直接的更新缓存的方法就是`改文件名`了。我使用的方法是把所有文件链接改成`@latest`版本，这样每次引用的版本都会是最新版本，但如果对过去已经上传过的图片要做更改，那可以在更改后的文件中加上一些更改的`备注信息`，例如`a_picture.png`改成`a_picture_v1.png`再上传，这样对文件链接的修改也仅只是增加的`_v1部分`，加上修改图片本身就是相对不常有的操作，所以这个方法已经足以解决我的问题了。

## 一个疑惑

在尝试解决这个问题的中途我曾经尝试过`删除以前的release和tag`的方法，当时我对`Jsdelivr`的运作方法还不是很了解，以为删除了已经发布的`release`就可以彻底解决链接至旧文件的问题。现在虽然知道这个方法不可行，但中途出现了一个现象却开始让我对`Jsdelivr`的业务逻辑产生了一些疑惑。

这个问题就是我曾经以`v1.0.2`的版本号发布过一个`release`,后来我删除了这个`release`并且以相同的`v1.0.2`这个`tag`发布了一个新的`release`，其他都非常正常，我可以在`新的v1.0.2`中访问一些`旧的v1.0.2`中没有加入过的文件，但其中有一张我修改过的图，却一直显示的是`旧v1.0.2`中的内容，即使我反复确认过`新的v1.0.2`中这张图的名称完全没有改变，而且内容也确实与旧版本不同，但如果在版本号中加入`@v1.0.3`(我已经删掉的版本)却可以找到新加的图片。

而当我使用官网提供的查看`Jsdelivr`目录的方式(`https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/`)进入目录时却发现这里并`没有v1.0.3版本`，而`v1.0.2`中那张修改过的图片也确实是`旧版`。

这些奇怪的现象让我确实难以理解`Jsdelivr`的逻辑究竟是如何。难道它按`链接`保存`单个文件`后储存在某个空间中作为`base`，然后从`新的release`中对比各个文件的链接然后`逐个更新`至这个`base`中？那即使是这样他也可以实现将`同名文件`用`新release中的版本`替代啊。希望以后对`Jsdelivr`的使用增加能解决我的这个疑惑。

# 最后

这篇文章主要是记录了`Jsdelivr`使用相关的一些知识和经过研究对这个CDN服务和逻辑的一些了解与猜测，最后更新缓存图片的解决方案其实让我有些不太满意，但想着官方清除缓存的工具都快出来了，那就再等等吧。

[第9篇]


[1]: http://raylei.space/2022/02/12/2-typora_picgo_config/	"使用 Typora 和 PicGo 简单便捷地编辑带图博文"
[2]: https://www.jsdelivr.com/	"Jsdelivr website"
[3]: https://www.tgee.cn/jsdelivr-cdn.html	"Jsdelivr CDN 缓存清除"
[4]: https://www.jsdelivr.com/tools/purge	"Jsdelivr Purge Tool"
[5]: https://blog.juanertu.com/archives/cbcd1946.html	"解决 jsdelivr 缓存问题的几个办法"

