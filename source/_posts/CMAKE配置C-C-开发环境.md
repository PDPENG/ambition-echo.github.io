---
title: VS code + clangd + Clang + CMAKE配置C/C++开发环境
date: 2021-12-10 12:34:52
tags: [C,vscode]
categories: Tips
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/1639111789400%E7%94%BB%E6%9D%BF%201.png
---
结合B站大佬的方法，不用WSL在vscode中配置C/C++开发环境

<!-- more -->

参考B站up主的视频[使用 VS Code + Clangd + CMake 搭建 C/C++开发环境](https://www.bilibili.com/video/BV1sW411v7VZ)来进行配置。

B站大佬的配置方法很好，但是在Windows下用WSL来进行开发终究还是有点麻烦，而且wsl运行的内存占用，快赶上一些大型IDE了，这样的话配置vscode不就没有必要了吗，为什么不直接使用Clion或者VS呢。

所以找到这些软件尝试不用WSL在windows下配置C/C++开发环境，但最后发现虽然LLVM有windows版本，但是要用到Visual Studio，~~于是放弃clang，直接用MinGW来配置。~~

今天偶尔发现一个网站[winlibs](https://winlibs.com)，提供默认不使用MSVC的Clang版本，下载试了试，真的是太香了。

***这样一来就可以不用WSL，完美在windows本地实现B站大佬的开发环境配置***

# 安装软件

用到的软件/插件(直接点击链接下载安装即可)：

软件：

- [Visual Studio Code](https://code.visualstudio.com/)
- [CMake](https://cmake.org/download/)
- ~~[MinGW](https://www.mingw-w64.org/downloads/)~~(可以直接用打包好的LLVM就不用下载MinGW了)
- [LLVM](https://winlibs.com/)
- [Ninja](https://github.com/ninja-build/ninja/releases)

插件：

- [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
- [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)
- [CodeLLDB](https://github.com/vadimcn/vscode-lldb/releases)

某些官网或者github上不去可以直接在蓝奏云下载：

[打包下载地址](https://wwd.lanzouo.com/b02olvw6h)

密码:9uaq



## 安装vscode

一路next

## 安装cmake

![image-20211210172019994](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210172019994.png)

下载```.msi```格式的安装包来安装。

注意安装时勾选将cmake添加到path。

## 安装编译器

到[winlibs](https://winlibs.com/)直接下载，按网站的说法这个打包在windows下提供了完整的编译器环境。

至于下载哪个版本，可以参照网站的说明。

> Traditionally the MinGW-w64 compiler used MSVCRT as runtime library, which is available on all versions of Windows.
>
> Since Windows 10 Universal C Runtime (UCRT) is available as an alternative to MSVCRT. Universal C Runtime can also be installed on earlier versions of Windows (see: [Update for Universal C Runtime in Windows](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c)).
>
> Unless you are targetting older versions of Windows, UCRT as runtime library is the better choice, as it was written to better support recent Windows versions as well as provide better standards conformance (see also: [Upgrade your code to the Universal CRT](https://docs.microsoft.com/en-us/cpp/porting/upgrade-your-code-to-the-universal-crt?view=msvc-160)).

大概意思就是说，首选下载ucrt版本。

![image-20211216222317595](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216222317595.png)

下载对应的包含LLVM的版本。

由于网站好像是在github托管的，可能会有上不去或者下载慢的问题，可以下载我存在网盘的：[百度网盘](https://pan.baidu.com/s/1l-xWd83b_836LJbYM68gSA) 提取码: uppb 

下载完成后，直接解压到要安装的路径下，再将其中的```bin```文件夹添加到环境变量即可。

![image-20211216223133463](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216223133463.png)

## 安装Ninja

下载之后将文件夹解压到一个固定位置之后，将文件夹添加到环境变量即可，由于是cmake在用，也可以直接把```ninja.exe```直接放到cmake安装目录下的```bin```文件夹下,就不用单独添加环境变量了。

## 安装clangd

由于winlibs打包的编译器中有与之匹配的clangd，就在```bin```文件夹中，所以不需要单独安装，直接用即可。

## 安装vscode插件

vscode中的插件，CMake Tools和clangd可以直接在vscode中搜索安装，没有问题，只是clangd与C/C++插件不兼容，要注意不要安装C/C++插件。

对于CodeLLDB，在vscode中安装大概率会下载失败，可以直接到github页面去下载```.vsix```文件手动安装.

### 安装方法：

打开vscode，按F1，输入vsix，出现从VSIX安装，点击后选择下载的```.vsix```文件即可安装成功。

![image-20211210173926386](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210173926386.png)

# 配置C/C++项目

## 项目结构

新建一个文件夹作为项目目录，在目录下新建几个文件：

目录结构如下：

```
├─src
│  ├─Template.c
│  └─Template.h
├─CMakeLists.txt
└─main.c
```

在```src```目录中是自定义的头文件

## CMake

打开vscode设置，在cmake设置中找到Generator，将其指定为Ninja：

![image-20211210180528993](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210180528993.png)

CMakeLists.txt文件内容如下

```cmake
cmake_minimum_required(VERSION 3.20)
project(Template C)

set(CMAKE_C_STANDARD 23)

add_executable(${CMAKE_PROJECT_NAME}
        main.c
        src/Template.c
        )

target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
        src
        )
```

cmake_minimum_required()定义CMake最低版本为3.20

project()定义项目名称和项目类型

set(CMAKE_C_STANDARD 23)规定项目使用的C语言标准为C23

再下面两部分规定了项目包含的源文件以及include文件夹。

保存文件，会自动生成一个```build```文件夹。

## launch.json

这时候按F5来调试程序，会自动在```.vscode```目录下生成一个```launch.json```文件。

将里面的内容改成如下所示：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "lldb",
            "request": "launch",
            "name": "Debug",
            "program": "${command:cmake.launchTargetPath}",
            "args": [],
            "cwd": "${workspaceFolder}"
        }
    ]
}
```

## clangd配置

打开vscode设置，在扩展中找到clangd，添加如下选项：

![image-20211210180255946](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210180255946.png)

1. 由于clangd需要读取cmake生成的compile-commands.json文件，所以需要指定其路径
2. 设置clangd代码提示显示参数类型
3. 设置从不导入头文件

# 测试程序

编写简单的测试程序：

- main.c

```c
#include "Template.h"
#include <stdio.h>

int main() {
    template x;
    x.a = 1;
    x.b = 2;
    printf("%d %d", x.a, x.b);
}
```



- Template.c

```c
#include "Template.h"
```



- Template.h

```c
typedef struct {
  int a;
  int b;
} template;
```



clangd的代码提示正常，按住ctrl点击头文件可以跳转。

![image-20211210180048976](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210180048976.png)

添加断点调试也没有问题。

![image-20211210180732375](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210180732375.png)

# 设置运行及调试快捷键

为了方便运行，可以添加自定义快捷键，实现像code runner插件那样的运行体验。

## 运行

按F1，输入cmake，找到运行但不调试，点击右边的齿轮按钮来自定义快捷键。

![image-20211210181108443](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211210181108443.png)

点击左边的编辑后输入要绑定的快捷键之后回车，这里就绑定为ctrl+alt+n，跟code runner一样，为了不发生冲突，找到code runner的运行快捷键，右键更改when表达式，填入如下：

```C
editorLangId != 'c' && editorLangId != 'cpp'
```

这样，code runner的快捷键就不会在编写C/C++时生效了。

## 调试

默认的调试快捷键为F5，很方便，但为了符合习惯，将其改为ctrl+alt+m，方法同上，这一快捷键与code runner中的停止运行冲突，感觉这个快捷键没什么用，直接删了。

到此配置完成，源代码编辑完成后可以ctrl+alt+n运行，ctrl+allt+m调试，不影响code runner运行python之类的。