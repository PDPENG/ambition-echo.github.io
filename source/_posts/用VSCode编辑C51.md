---
title: 用VSCode编辑C51
date: 2021-05-24 21:17:29
tags: [C51,vscode]
categories: Tips
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211114222001.png
---
一般情况下，我们用keil软件编写C51程序，然后通过keil编译生成.hex文件，之后再用STC提供的烧录软件来进行烧录，整个过程非常繁琐，而且keil软件编写代码的体验极差，界面难看不能自定义，代码补全功能也一言难尽。而vscode作为万能的代码编辑器，能否用它来代替keil呢，肯定是可以的。
<!-- more -->
### 用到的软件/插件
+ vscode
+ Embedded IDE(vscode插件):打开keil项目，提供C51代码高亮及自动补全。
+ Keil5:虽然是用vscode来进行开发，但是编译还是得用keil里面的编译器。
+ stcgal:通过命令行进行烧录  
通过Python3进行安装：```pip install stcgal --user```

### 插件配置
Embedded IDE可以创建其特有的项目，也可以导入keil项目，要用其编译C51程序，还需要设置编译器路径，只要设置工具链路径为keil安装目录下的TOOL.INI就可以。

![image-20211112110234770](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211112110234770.png)

至此，已经可以用vscode开发C51程序，并进行编译了，但是还没法完成烧录，要完成烧录，就需要stcgal了，安装好stcgal之后，在Embedded IDE设置中选择烧录方式为stcgal，使用其默认配置就好。

### 最终效果
至此，可以在vscode中完成C51程序的编辑，编译，烧录的一站式开发。

