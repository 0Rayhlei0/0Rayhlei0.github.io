---
title: "[博客维护]基于Hexo框架搭建个人网站的实现记录"
date: 2022-02-10 22:50:59
tags: [Hexo,GitHub,Git,日常学习]
categories: 博客维护
description: "[第1篇]本文介绍了我跟随枫叶的详细教程成功搭建本网站的过程中的一些心得以及需要注意的点。"
top_img: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/blog_img/blog.jpg
cover: https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics@latest/cover_img/1-blogsetupnotes.jpg
---

# 序言

从很久以前就想搭一个自己的网站，分享并且记录自己的一些日常工作和学习的过程和成果，此篇作为我的第一篇文章，就先分享一下我跟随[枫叶][1]的详细教功搭建本博客网站的一些心得体会。

# 正文

本网站的搭建过程与枫叶教程中的基本一致，下面我就分篇讲一讲我作为一个“网络”小白在读教程的过程中遇到的一些问题，以及查询资料后我的理解。

## 关于第二篇Git安装的问题

Git本身是一个免费开源的分布式版本控制系统(Distributed version control system), Git的主要作用是我们通过此版本控制系统提交文件至仓库，由该系统为提交的文件打上版本号，然后每次提交仓库时根据版本号知道哪些文件需要更新哪些可以不用改动。需要记录的几个定义，需要强调的是以下基于我查到的资料和我自己的理解，有理解不对的地方还请大神指正：

- 本地仓库与远程仓库：分别指建立在本地和互联网服务器内的文件夹
- 分布式与集中式版本控制系统：分布式系统（如Git）同时具有本地及远程仓库，提交文件时先提交至本地仓库，有网络时再提交至服务器上的远程仓库。集中式系统（如SVN）只配有远程仓库，提交文件时直接提交到远程仓库。
- 在此步骤中，GitHub既是远程仓库，是一个网络文件夹。我们主要使用Git作为同步本地仓库和远程仓库的工具。

## 关于第三篇绑定GitHub并提交文件

跟随步骤进行时有两点需要注意：

### Git的username和email的配置

首次提交文件时需要向远程仓库声明本机器的名字和Email地址，即使用：

```bash
$ git config --global user.name "yourusername"
$ git config --global user.email "youremailaddress@xxx.com"
```

根据[这篇文章][2]的描述，这个username可以是任何你想要附在你的提交文件上的一个“标记”，它不需要和你的版本控制用户名（例如你的GitHub用户名）一致。之所以要在首次提交之前输入这个信息就是为了给你的提交打上“标记", 一旦你的提交被创建，它的“著作权”就已经和你填写的这两条信息绑定，不能再被更改。

此处以我自己的理解是该名字和Email地址其实对于我们真正要做的事情并没有实质作用或影响，只不过是向远程仓库提交了一个象征这个本地仓库的一个符号，提交后即可以使用下方命令查看配置是否成功上传。

```bash
$ git config -l
```

之所以强调要查看这个配置的原因是因为在枫叶的教程中给出的代码有**少许错误**：

![教程中的代码没有带空格](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220210235741955.png)

没有这个空格不会有任何报错，同时也不会有任何效果，我当时因为不知道这个小错误，还以为username与email都成功设置了，导致Git一直无法成功commit而找不到原因，需要注意。

### 从Master换成Main的掩耳盗铃

枫叶教程中多次提及的GitHub的默认分支Master，[查询][3]后发现原来这个默认的Master分支已经在2020年10月1日起被GitHub改成了Main，其原因竟是因为要避讳可能引起人们联想到奴隶制的词汇，为了这种自欺欺人的原因导致多少人的麻烦。

#### push文件时的命令

回到正题，因为分支名的改动，文件commit至本地仓库后应使用

```bash
$ git push origin main
```

将本地仓库提交至远程仓库，这其中origin是远程主机(即GitHub)的名字,而main则是我们仓库的默认分支名。

#### 初始化本地仓库时要做的修改

在实际操作中我还发现了这个改动导致git隐藏的一个地雷，那就是当我们用枫叶第三篇博客中提到的第二种git方法提交文件时，使用`git init`将不会初始化到我们想要的main分支，而是默认创建了master分支。这将直接导致我们之后使用`git push origin main`推至远程仓库时会报错，因为我们的本地仓库根本就不是main。

![image-20220213115508276](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220213115508276.png)

这时我们要将这个本地仓库分支名改成我们想要推至的远程仓库，并且最好顺道把`git init`的默认分支也改成main，毕竟GitHub的默认分支都已经改成main了。然后你就可以继续按照教程快乐上传各种文件了。

```bash
$ git branch -M main #这个命令可以将你当前所在的本地仓库分支名改成-M后面这个参数"main"
$ git config --global init.defaultBranch main #将默认分支名改成main，可以用git config -l查看是否更改成功
```

### 为什么要提交到GitHub?

我们之所以要将文件提交至GitHub的远程仓库其实是因为其提供的一项服务[GitHub Pages][4]， 这项服务使用户可以创建和托管其自己的个人网站，每个GitHub账号只允许创建一个网站，这也是我们要用创建名称为`“用户名.github.io”`的仓库这样的方式来启用这项服务的原因。

## 关于第五篇安装node.js和Hexo

node.js简单来说就是JavaScript的一种运行环境，而npm则是node.js的包管理器 (package manager)，使用npm可以自动根据各个需要模块的依赖关系快速下载安装需要的所有依赖的包并管理，本篇中安装node.js的直观原因就是为了能在命令行中使用npm。

### 设置文件夹权限

本篇中需要注意的一点是，设置npm的路径和环境变量时在nodejs文件夹中创建的两个node_cache和node_global文件夹需要在各自的属性中给与用户所有权限，否则会导致npm报错。

![给予用户完全控制权限](https://cdn.jsdelivr.net/gh/0Rayhlei0/Pics/post_img/image-20220211002517309.png)

### Hexo是什么？

根据Hexo的[官方文档][5]，Node.js与Git都是使用Hexo的必要条件，而Hexo本身则是一个免费的博客框架，换句话说既是已经写好的“网站积木”，有了Hexo我们就不需要完全重新设计搭建网站，被古老的html语言折磨，而可以用已有的积木搭出我们想要的网站的样子，主流的博客框架除了Hexo还有与GitHub Pages绑定的Jekyll，尽管看到不少网友鼓吹Jekyll的便捷，但我看着网上大部分由Hexo搭建的博客网站想想大概人类的本质就是口嫌体直罢。

关于Hexo相关的命令有：

```bash
$ hexo init [folder] # 该命令在提供的文件夹下初始化一个网站，如果没有提供文件夹路径则在当前路径初始化。完成导入hexo-starter到目标文件夹并安装依赖包。
$ hexo g # 等同于 hexo generate，该命令将文件夹中的资源文件生成部署网站用的静态文件，这也是我们刚刚提到的Hexo最重要的作用，将积木搭成城堡的一步。
$ hexo s # 等同于hexo server，启动本地服务器。该命令用于预览已经做出的更改，但不会推送至远程仓库部署，使用该命令不需要hexo g即可默认从http://localhost:4000/本地预览网站的样子。
$ hexo clean # 该命令用于清除缓存文件db.json和已经生成的静态文件Public, hexo g之前最好先运行此命令以免造成generate的文件出现难以预估的问题。
$ hexo d #等同于hexo deploy，使用此命令将目前文件夹中的静态文件部署到设定的仓库（网站）。
```

# 最后

感谢枫叶大佬的详细介绍才使得我一个完全没有接触过类似东西的人得以在几天内忙里偷闲搭起了这样一个网站，像是有了一个小小的自己的空间，非常感激。即使第六篇之后，也就是网站的主题选择我没有像枫叶大佬一样选择Next主题，而是用了目前看起来更新更符合我审美的[Butterfly][6]，我也依然在配置Hexo的主题文件等等问题上很大程度上参考了大部分第八篇的内容。

另外必须给大家推荐我现在使用的这个主题, 这是最符合我审美并且自由度相当高的一款主题，网站上有相当详细的文档，大家配置主题的时候跟着文档走就可以完成大部分的网站配置了。

[第1篇]

[1]: https://zhuanlan.zhihu.com/p/102592286?tdsourcetag=s_pctim_aiomsg	"从零开始搭建个人博客（超详细)"
[2]: https://careerkarma.com/blog/git-config/	"How to Set Up Git Using git config"
[3]: https://blog.csdn.net/j3T9Z7H/article/details/108898310	"今天开始，GitHub将启用main作为默认分支名，master将成为历史！"
[4]: https://docs.github.com/en/pages	"GitHub Pages Documentation"
[5]: https://hexo.io/docs/	"Hexo Documentation"
[6]: https://butterfly.js.org/	"Butterfly Documentation"
