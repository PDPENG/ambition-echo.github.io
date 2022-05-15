---
title: Git学习笔记
date: 2021-07-20 10:27:36
tags: Git
categories: Learn
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211114222337.png
---
Git是一个优秀的版本控制系统，熟练使用Git可以极大地方便我们的工作。
<!-- more -->
### 安装Git

windows下直接在官网下载安装最新版即可，只是安装时记得勾选add to path

### 系统设置

初次安装git后需要完成一些简单的设置：
#### 设置用户姓名
```git config --global user.name "Your Name"```
#### 设置用户邮箱
```git config --global user.email "email@example.com"```

这两个设置只是为了在多人协作时辨识你的身份，并不是用来登录任何东西，所以随意设置即可。
#### 生成SSH
第1步：创建SSH Key。在用户主目录下，看看有没有```.ssh```目录，如果有，再看看这个目录下有没有```id_rsa```和```id_rsa.pub```这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```ssh-keygen -t rsa -C "youremail@example.com"```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到```.ssh```目录，里面有```id_rsa```和```id_rsa.pub```两个文件，这两个就是SSH Key的秘钥对，```id_rsa```是私钥，不能泄露出去，```id_rsa.pub```是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

至此，你的SSHkey就添加到了github仓库中，你就可以往远程仓库推送了。

### 创建版本库

```git init```命令可以在当前目录下创建一个版本库。

命令执行完成后，当前文件夹下会多一个名为```.git```的文件夹，当然，他是隐藏的，没必要也最好不要去动他。

### 添加到暂存区

```git add <file>```命令可以将文件添加到暂存区

### 提交版本

```git commit -m "massage"```命令将当前暂存区的所有修改提交到版本库，成为一个新的版本

### 查看工作区状态

```git status```命令可以显示当前工作区的状态

### 查看版本提交记录

```git log```命令可以显示所有提交的版本及其massage，便于查看和回退

### 版本回退

```git reset --hard HEAD^``` 回退到上一个版本

```git reset --hard <版本号>``` 回退到某一个版本