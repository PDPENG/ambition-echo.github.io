---
title: hexo+github+github actions打造完美博客
date: 2021-11-12 19:33:43
tags: [hexo,github,action]
categories: learn
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/e4d8c3d4149df4f2a91850f7d22f6511.jpeg
---
从零开始搭建一个属于自己的功能完备的博客。

<!-- more -->

之前利用hexo和GitHub Page搭建了博客，博客部署利用的是Travis CI，最近发现github的actions功能跟Travis CI一样，甚至更强大，用起来也特别非常方便，这还用第三方的干嘛，直接迁移到github，顺便重新换个博客主题，从头搭建一下博客。

github部署博客，利用的是github仓库的page功能，github page只能部署静态网页，虽说有很多限制，但是他免费啊，这样就不用自己租服务器。只能部署静态页面，那就用部署静态博客嘛，用hexo生成不也很方便。

# 什么是静态博客

静态博客就是只有静态页面的博客，什么是静态页面呢，静态页面不是说这个页面不能动，而是说这个网页没有后台，静态网页是实实在在保存在服务器上的文件，每个网页都是一个独立的文件。更新页面就得手动更新html文件，像一些博客的评论功能，这就是典型的动态页面才有的功能，虽说理论上不能用，但总有些奇奇怪怪的办法，这个后面再说。

# 静态博客网页生成器

要搭建静态博客，就得利用静态博客生成器，总不能每篇博文都手写html,这种生成器很多，我用的是比较流行的hexo,还是挺好用的。

了解了这些就可以开始搭建博客了。

# 开始搭建博客

## 用到的工具

- git
- nodejs（hexo是基于nodejs,这个必须要装的）
- npm

## 安装git

windows到git官网下载最新版安装即可。

linux通过软件包管理工具安装即可。

git的安装、配置以及基本操作可以看廖雪峰的教程，还是很详细的。[传送门](https://www.liaoxuefeng.com/wiki/896043488029600)

## 安装nodejs

nodejs也是安装最新版就好，最新版的nodejs是自带npm的直接可以用。

## 安装hexo

由于npm的下载速度一般都很慢，所以换到淘宝镜像源使用。

命令行输入以下命令切换淘宝镜像源：

```bash
npm config set registry https://registry.npmmirror.com
```

然后就可以直接用npm安装hexo了，命令行输入以下命令：

```bash
npm install hexo-cli -g
```

安装完成后就可以开始搭建博客了

## 初始化博客

安装好hexo之后就可以用命令来初始化博客了。

首先命令行转到你要存放博客的文件夹

然后命令行执行以下命令：

```bash
hexo init <folder>
cd <folder>
npm install
```

其中```<folder>```是你存放博客的文件夹名字。

这样就新建好了一个博客，现在博客文件夹的目录结构大概是这样的：

```bash
.     
├── _config.yml
├── package.json
├── package-lock.json
├── node_modules                                                     
├── scaffolds
│   ├── draft.md
│   ├── post.md
│   └── page.md
├── source
│   └── _posts
└── themes
```

其中```_config.yml```是博客的配置文件，博客的一些基本设置，都在这里面保存。

还有```package.json```和```package-lock.json```这两个文件是随配置文件自己更新的，不用动他，也不要去动他。

文件夹```node_modules```里面存放的是hexo及一些其他模块，也不用动。

文件夹```scaffolds```里面放的是文章模板，你新建一片文章的时候实际上就是从这里复制了一份，这里的模板是可以自定义的。

文件夹```source```里面放的就是我们的博文了，博文都是用markdown来写的，编辑博文的时候只要编辑source里面的markdown文章即可，hexo可以自动帮你生成并渲染成html页面。

文件夹```theme```里面可以放主题文件，hexo官网提供了很多主题可以下载。

## 接着对博客进行一些基本设置

打开编辑```_config.yml```文件

各部分配置文件的作用注释都有说明，先改一些基本的设置。

网站设置

|       参数        | 作用                                                         |
| :---------------: | ------------------------------------------------------------ |
|    ```title```    | 网站标题                                                     |
|  ```subtitle```   | 网站子标题                                                   |
| ```description``` | 网站描述                                                     |
|  ```keywords```   | 关键字                                                       |
|   ```author```    | 作者                                                         |
|  ```language```   | 网站语言，简体中文一般设置为zh-CN或zh-Hans                   |
|  ```timezone```   | 网站时区，默认使用电脑的时区，也可以设置为```Asia/Shanghai``` |

## 新建一篇博文

现在，可以新建一篇博文了，命令行执行：

```bash
hexo new post hello_hexo
```

执行完成后会发现在```source```文件夹下的```_posts```中多了一个叫```hello_hexo.md```的文件。

现在打开这个文件开始写点什么。

新建的文章，打开之后是跟你设置的模板一样的，默认是这样的：

![image-20211112213425173](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211112213425173.png)

开头这一段是文章的基本信息，在后面接着写博文即可，信息中的```tags```是文章标签，可以添加一个或多个标签。多个标签用方括号括起来，像这样```[tag1,tag2]```。

## 生成静态页面

写完博客之后，保存文件，然后再命令行执行一下命令：

```bash
hexo generate
```

执行完成后，hexo便将博文构建成了静态的博客网站，可以发现目录下多了一个叫```public```的文件夹，这里面就是构建好的静态网站的全部文件，博文更新后可以重新生成，重新生成前先将之前生成的文件清理掉。

```bash
hexo clean
```

执行完成后，生成的文件就全部清理了，```public```文件夹不见了，现在就可以重新执行generate来生成了。

## 本地部署

现在所有文件都还在本地，要想预览博客的样子，可以进行本地部署。

```bash
hexo server
```

接着访问默认的4000端口就可以预览博客了。

![image-20211112214709481](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211112214709481.png)

