## Hexo + GitHub Pages搭建自己的博客

参考：

## Hexo搭建步骤

1. 安装Git
2. 安装Node.js
3. 安装Hexo
4. GitHub创建个人仓库
5. 生成SSH添加到GitHub
6. 发布文章
7. 设置个人域名

### 1.安装Git

### 2.安装Node.js

### 3.安装 Hexo 

```
  npm install hexo-cli -g
  依旧用hexo -v查看一下版本
```

### 接下来初始化一下hexo

```
hexo init myblog   //myblog是项目名字
```

```
cd myblog //进入这个myblog文件夹
npm install

```

## 新建完成后，指定文件夹目录下有：

#### 启动

- node_modules: 依赖包
- public：存放生成的页面
- scaffolds：生成文章的一些模板
- source：用来存放你的文章
- themes：主题
- ** _config.yml: 博客的配置文件**

```
hexo g   生成public
hexo server

```

打开hexo的服务，在浏览器输入localhost:4000就可以看到你生成的博客了。

大概长这样：

![1593847115694](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1593847115694.png)

使用ctrl+c可以把服务关掉。

### 4.1GitHub创建个人仓库

主要是使用GitHub Pages

建立个人仓库， 建立后生成SSH添加到GitHub，作用是建立本地git仓库和你远程github上的仓库之间的联系。

#### 2. 将hexo部署到GitHub

首先将hexo和GitHub关联起来也就是将hexo生成的文章部署到GitHub上，打开站点配置文件 `_config.yml`，翻到最后，修改为YourgithubName就是你的GitHub账户

```
deploy:
  type: git
  repo: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master

```

这个时候需要先安装deploy-git ，也就是部署的命令,这样你才能用命令部署到GitHub。

```
npm install hexo-deployer-git --save

```

然后

```
hexo clean   清除了你之前生成的东西
hexo generate    生成静态文章  重新编译
hexo deploy   部署文章

```

其中 hexo clean清除了你之前生成的东西，也可以不加。
hexo generate 顾名思义，生成静态文章，可以用 hexo g缩写
hexo deploy 部署文章，可以用hexo d缩写

注意deploy时可能要你输入username和password。

得到下图就说明部署成功了，过一会儿就可以在http://yourname.github.io 这个网站看到你的博客了！！


### *****     踩坑了…………

就是下面这一段配置 _config.yml中

```
deploy:
  type: git
  repo: https://github.com/lyx/lyx.github.io.git
  branch: master
```

第一个问题：reop地址：这一块，在每次hexo deploy 部署的时候都会报错，github上没有变化。

解决查看   https://blog.csdn.net/liuyongshun2/article/details/54629087

 于是调整了一下代码缩进，改了一下仓库命名。lyx.github.io.git

第二个问题：我的一直报[github Repository not found 解决办法](https://www.cnblogs.com/zqyw/p/10988018.html)

https://www.cnblogs.com/zqyw/p/10988018.html

查看后，重新填了一下github账号和密码。

```
$ git credential-manager uninstall
```

```
$ git credential-manager install
解决办法如下,然后再执行git pull就会让你输入账号密码。就可以正常使用啦。
```

### 4.3 ok  接下来可以试着写第一篇博客...

新建一个空文章，输入以下命令，会在项目 \Hexo\source\_posts 中生成 文章标题.md 文件，文章标题根据需要命名

```
 $ hexo n "文章标题"
```

也可以直接在 \Hexo\source\_posts 目录下右键鼠标新建文本文档，改后缀为 .md 即可，这种方法比较方便

```javascirpt
---
layout: 页面布局（配合主题文档使用）
title: 文章名称
date: 文章日期
comments: 文章是否开启评论
photos: 文章封面图（仅部分主题支持）
tags: 
  - 文章标签一
  - 文章标签二
categories: 文章分类
description: 文章描述，即要在首页显示的摘要（仅部分主题支持）
---

这里是摘要

<!-- more -->

这里是正文

注意：description 和 <!-- more --> 方式显示摘要二选一即可，部分主题不支持description，每个配置英文冒号后面要空一格，不同主题配置有所差异，具体要参考主题文档

```

当我们用编辑器写好文章后，可以使用以下命令将其推送到服务器上

```
 $ hexo g  
 $ hexo d
或者是或者将两个命令合二为一输入以下命令：
 $ hexo d -g 

```

### 4.4 为博客更换自己喜欢的主题

  进入主题页面  挑选一个喜欢的主题    https://hexo.io/themes/

next为例

第一步：下载next主题包。
使用`terminal`，进入到我们Hexo的安装包下面。我的安装包，叫做`blog`。因此，我输入下述代码

```
$ cd blog
```

然后进入`themes`包

```
$ cd themes
```

接着，我们输入下面的代码

```
$ git clone https://github.com/theme-next/hexo-theme-next next
```

其中`https://github.com/theme-next/hexo-theme-next`是我们需要下载的主题的地址，`next`是我们将其放在的文件夹名字中。接着，会出现下面的代码提示。

![img](https://img-blog.csdnimg.cn/20190423154754464.png)

提示我们`done`，就说明，这个步骤操作完成了。

第二步：修改`_config.yml`文件内容。
在我们hexo安装包中找到`_config.yml`安装包，用编译器打开（vs code或者sublime）。
command + F 查找 `theme`将原来默认的主题 `landscape`改为 `next`。修改好的代码参考下图：

第三步：部署步骤！
接下来，我们先来预览一下，我们主题更换的效果

![1593858564452](C:\Users\luyunxiao\AppData\Roaming\Typora\typora-user-images\1593858564452.png)

借用大佬的界面。我的太难看了  我再换一个.....



一顿操作下来虽然有点儿累，但看见拥有了自己的博客还是非常有成就感的，人生就是需要折腾，那么现在就开始你的创作之旅吧！

文中涉及参考资料如有侵权请联系我删除！

参考博客：

https://blog.csdn.net/qq_36759224/article/details/82121420?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522159384405219195265929353%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=159384405219195265929353&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v3-5-82121420.pc_ecpm_v3_pc_rank_v3&utm_term=Github+Pages+hexo

https://lvan-zhang.github.io/



碰到的新问题



1. 每次部署都需要从新添加账号和密码

git中用来配置账号授权信息主要是靠credential配置项的helper节点来控制。

把你当前的本地仓库删了，重新&nbsp;git clone&nbsp;，记得使用&nbsp;SSH。比如&nbsp;git clone git@github.com:HmyBmny/hmybmny.github.io.git&nbsp;，这样才能使用&nbsp;SSH。

title: LYX · BLOG

subtitle: 'I am the danger'

description: 'I'm not in danger,I am the danger.'

keywords: node

author: lyx

language: en

timezone: '