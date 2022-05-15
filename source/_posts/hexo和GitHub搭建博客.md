---
title: hexo和GitHub搭建博客
date: 2021-05-16 17:49:57
tags: hexo
categories: Learn
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211114222455.png
---
一直想要利用GitHub Page来搭建一个博客，但是GitHub Page只支持静态页面，没法使用有后台的博客框架，了解之后发现有静态博客框架，大概就是把markdown格式的博文写好之后，一个命令就可以生成html的页面，非常方便，还可以根据自己的喜好进行深度的自定义设置。
<!-- more -->
### 基本操作

#### 安装hexo
hexo是基于node.js的静态博客框架，安装前应该先安装node.js，安装完成后应该是自动安装了npm的。

```bash
$ npm install -g hexo-cli
```

#### hexo基础操作

+ 初始化Blog

```bash
hexo init <flord>
```

+ 新建博文

```bash
hexo new 
```

+ 生成页面

```bash
hexo g
```

+ 本地部署

```bash
hexo s
```