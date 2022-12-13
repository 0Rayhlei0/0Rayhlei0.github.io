---
title: "[博客维护] 使用Typora和PicGo简单便捷地编辑带图博文"
date: 2022-02-12 17:50:16
tags: [Typora,PicGo,GitHub,日常学习]
categories: 博客维护
description: "[第2篇]本文介绍了如何使用Markdown编辑器Typora及配套图片管理软件PicGo便捷地编辑和管理博文。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/blog.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/2-typora_picgo_config.jpg
---

# 序言

网站已经搭好了，但是怎么样编辑并且发布文章呢？我们知道网站中的文章都是作者按照排版需求使用Markdown语法写出.md后缀文件(既Markdown文件)并以此生成相应的html文件供浏览器读取展示，而插入图片的方法却只能使用路径引用的方法非常繁琐。本文将介绍在Hexo框架下发博文的方法，以及如何使用md编辑器[Typora][1]与图床管理软件[PicGo][2]来简单便捷地编辑图文。

# 正文

## 创建博文

先介绍一些在Hexo中发文的基础知识。

### Hexo框架下博文的保存

在我们安装的[Hexo][3]的根目录下与Hexo有关的分别是下面四个，他们的作用分别如下：

- **scaffolds:** 模板文件夹，保存了草稿，页面和文章这三类md文件的模板，新建的该类文件内容将与模板一致。
- **source:** 保存网站内容的文件夹，其中的`_post`子文件夹即是保存md格式博文的文件夹。`source文件夹`中的所有可渲染文件(例如markdown和html)都将被渲染并被放入`public文件夹`，其他类型文件则会被直接复制。
- **public:** 保存网站原码的文件夹，这个文件夹中的内容将被推出并托管在`GitHub Pages`上形成网页。
- **theme:** 保存Hexo主题文件的文件夹，Hexo会同时基于网站内容和主题文件来生成相应的静态文件。

也就是说我们的博文其实就是保存在`source/_post`文件夹中的md文件，即创建txt文件后改后缀成md，只要在文件开头---分隔符内(即`front-matter`)写上必要的配置如标题，日期等，这个md文件便会被识别渲染为一篇博文。

### Hexo新建页面/博文命令

即使只要放入md文件即可被渲染成网页，Hexo依然提供了更方便的创建新页面或博文的方法：

```bash
$ hexo new [layout] <title> #layout若不填则自动按post模板创建，title将同时被用于文件名和frontmatter中的title参数
```

hexo命令创建三类文件的方式分别如下：

- **Page(页面)**: 在`source`文件夹下创建一个指定名称的路径，并在里面创建一个index.md文件，该文件中内容将显示在页面上。
- **Draft(草稿)**: 在`source/_drafts`文件夹中创建一个草稿，该文件不会被展示在页面上，但可以被用`hexo pubilish [layout] <filename>`命令发布。
- **Post(博文)**: 若`new`命令没有指定`layout`则将默认创建该类型，此类型被创建在`source/_post`文件夹中，会被直接渲染为博文。

## 使用Typora和PicGo编辑博文

知道了Hexo下发博的基本知识，现在终于来到正题，如何方便快捷地编辑一篇图文并茂的博文呢？我的选择是Typora与其绑定的图床管理软件PicGo Core。

### Typora是什么

Typora是一款专门用来编辑Markdown文件的编辑软件，他的最大特点便是”所见即所得“。在这个软件中你可以使用markdown语法来调整你的文章展示，而你写下的格式语法会被Typora直接转换为渲染后的效果。这样作者就可以很方便地一边编辑一边调整最终成稿。

### PicGo是什么

简单来说，PicGo是一个用于快速上传图片至图床并获取图片URL链接地工具。一直以来在md文件中插入并管理图片都是一个非常麻烦的工作，你需要将你需要使用的图片放在本地或图床上，并在md文章中引用这些地址来实现图片地展示。但现在Typora中置入了PicGo Core的工具让你可以以可视化的方式简单方便地插入图片在你的博文中。

### 具体如何配置

虽然PicGo支持的图床相当多，但大部分图床都有各种各样的限制或收费。而我个人选择的则是GitHub作为我的图床，因为在建站时创建的远程仓库刚好可以直接拿来用作图床，除了文章内使用的图片，其他包括top_img或封面等都可以很方便地上传至这些远程仓库用来引用。

#### 配置Typora

从Typora的上方选项中依次打开`格式→图像→全局图像设置`，然后会进入下图的界面，按图片中的设置配置打勾：

![按图中方式配置](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220214215927465.png)

选择插入图片时`上传图片`，下方下拉选单选择`PicGo-Core(command line)`，这时可以直接`下载或更新`。安装好`PicGo`后就需要配置图床了。

#### 配置图床

为方便我选择的是GitHub的远程仓库作为我的图床，大家可以按照PicGo的[官方文档][4]生成该远程仓库的token用于使PicGo可以获得访问该仓库的权限。获得这个token之后我们就可以开始填写PicGo的配置文件，用户可以在命令行中输入`picgo set uploader`来进入交互式命令行：

![image-20220214234833095](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220214234833095.png)

用方向上下键移动，回车选中github，然后命令行会分别要求你输入需要的参数以生成配置文件，填写完成后在命令行中继续输入`picgo use uploader`并选择刚刚配置的uploader来完成配置。按要求完成好后生成的配置文件如下，当然你也可以直接按Typora中的`打开配置文件`按钮或直接去到系统用户目录下`.picgo/config.json`中手动填入配置，但鉴于出错的可能性比较大，更推荐自动生成配置文件：

```json
{
  "picBed": {
    "current": "github",
    "uploader": "github",
    "transformer": "path",
    "github": {
      "repo": "username/reponame",//填入你的github仓库的用户名/仓库名
      "branch": "branchname", //填入分支名
      "token": "tokentokentoken",//填入github token
      "path": "post_img/",//填入需要上传到的文件夹路径
      "customUrl": ""
    }
  },
  "picgoPlugins": {}
}
```

此时你就已经在Typora中配置好了图床，按一下Typora中的`验证图片上传选项`按钮，显示验证成功，这时你就可以直接截图粘贴至你正在Typora中编辑的博文，Typora会自动帮你完成上传图片至图床并返回图片链接至你粘贴图片的位置的操作。

![image-20220215000247746](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220215000247746.png)

#### 使用图床

除了使用Typora的自动上传功能以外，我们也可以直接手动利用我们的GitHub来作为我们的图床使用，在本地仓库中放入需要使用的文件或图片，然后对他们使用 `add commit push`三部曲推至远程仓库(由于本地仓库不会自动更新Typora上传至远程仓库中的图片，因此如有改动，在add前还需要先将远程仓库的改动pull至本地仓库，以免报错)，然后便可以使用`raw.githubusercontent.com`后接文件在github中的路径便可以直接访问该文件的raw (即未处理版本)文件。

---

以下内容为2022年2月19日补充

## 使用Jsdelivr加速图床

由于一直在香港且只在自己的电脑上测试，并没有意识到GitHub作为图床使用的一个重要缺点，那就是当内地用户访问网站时使用`raw.githubusercontent.com`链接会导致图片裂开...在苦恼了几分钟以为要把所有链接换成其他内地付费的图床时我找到了`JSDelivr`这个解决办法。

其实使用`JSDelivr`的链接是我刚刚开始查找图片链接方法时就注意到了的，但由于发现`GitHub`的raw链接可以实时展现图片而不需要release版本blabla，也就没有继续看稍微麻烦一些的`JSDelivr`，现在看来是福不是祸，是祸躲不过啊。

#### Jsdelivr是什么？

参考[这篇文章][5]我们知道`JSDelivr`是`内容分发网络(Content Delivery Network, i.e. CDN)` 的提供商之一，简单来说既是将特定网站的资源分布至各地网络，然后该资源被请求时即从距离请求最近的服务器回应该请求，从而达到加速资源访问的目的。

#### 如何在Typora中设置JSDelivr？

首先要注意的是前文中提到`PicGo`的配置文件中有一个之前未提及的`customUrl`项，设定该项即可将上传图片后返回的链接自定义到`JSDelivr`的链接从而使用其服务。具体来说是改成：

> "customUrl": "https:// cdn.jsdelivr.net/gh/用户名/仓库名"   #注意去掉网址中间的空格

经过我的测试，发现在Typora中粘贴图片可以正常上传至`GitHub仓库`，但返回的链接却不能正确显示图片。这个原因我猜测是因为是我们没有将上传的图片release，因此这时JSDelivr还无法获得获取我们上传的资源，按照[这篇文章][6]的方式发布后，图片就可以用`JSDeliver`的链接访问了。

最后一点小备注，在release步骤中填写的Tag也就是版本号，如果在仓库名和文件夹名中间加入这个Tag名，即可访问该版本的资源，如果不加这个版本号则是默认访问最新的版本资源。

> https:// cdn.jsdelivr.net/gh/用户名/仓库名/{% label 版本号%}/文件路径   #注意去掉网址中间的空格

---

# 最后

现在作为完全小白的我终于可以快乐而没有顾忌地发文章了，一切麻烦的事情都交给Typora。

[第2篇]

[1]: https://typora.io/	"Typora Website"
[2]: https://picgo.github.io/PicGo-Core-Doc/zh/guide/config.html#picbed-tcyun 	"PicGo-Core Documentation"
[3]: https://hexo.io/docs/setup	"Setup for Hexo"
[4]: https://picgo.github.io/PicGo-Doc/zh/guide/config.html#github%E5%9B%BE%E5%BA%8A	"PicoGo Configuration on GitHub图床"

[5]: https://www.dazhuanlan.com/charmsky/topics/1636035	"前端 使用JSDelivr加速加载Github资源"
[6]: https://www.cnblogs.com/yu-du-chen/p/12109065.html	"jsdelivr的使用"

