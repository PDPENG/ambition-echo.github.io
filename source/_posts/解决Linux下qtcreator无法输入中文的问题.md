---
title: 解决Linux下qtcreator无法输入中文的问题
date: 2022-02-08 20:42:25
tags: [Qt,QtCreator]
categories: Tips
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20220208204737212.png
---
在Ubuntu上安装fcitx5之后发现，QtCreator无法输入中文了。
<!-- more -->

## 原因

由于Ubuntu下Qtcreator默认只支持了ibus,所以新安装fcitx5或者fcitx无法在qtcreator中输入中文。

需要自己手动编译fcitx5官方的qt插件

[官方仓库](https://github.com/fcitx/fcitx-qt5)：https://github.com/fcitx/fcitx-qt5

## 注意事项

github上还有一个仓库叫fcitx5-qt,千万不要编译这个，两个仓库差不多，我也不知道区别，但是实测这个仓库编译之后不能解决问题。

## 解决步骤

### 克隆仓库

```bash
git clone https://github.com/fcitx/fcitx-qt5
cd fcitx-qt
```

### 修改CMakeLists.txt文件

**注意！要根据实际情况来改，看你的qtcreator是用什么版本的qt编译的**

在qtcreator-帮助-aboutqtcreator中查看

![image-20220208205639939](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20220208205639939.png)

如果是qt5编译的，则在CMakeLists.txt中找到

```option(ENABLE_QT5 "Enable Qt5" Off)```改为```option(ENABLE_QT5 "Enable Qt5" On)```

如果是qt5编译的，则在CMakeLists.txt中找到

```option(ENABLE_QT5 "Enable Qt6 im module" Off)```改为```option(ENABLE_QT5 "Enable Qt6 im module" On)```

### 创建编译目录

```bash
mkdir build
cd build
```

### 开始编译

在build目录下编译

```bash
cmake .. -DCMAKE_PREFIX_PATH=qt安装目录/6.2.3/gcc_64 -DENABLE_LIBRARY=false
```

config成功之后直接

```bash
make -j8
```

编译完成之后，可以在build目录下找到```qt6/platforminputcontext/libfcitxplatforminputcontextplugin-qt6.so```

这就是我们要的文件

把他复制到这两个地方：

1. qt安装目录/Tools/QtCreator/lib/Qt/plugins/platforminputcontexts(qtcreator就可以输入中文了)
2. qt安装目录/6.2.3/gcc_64/plugins/platforminputcontexts(你用qt6编译的程序中就可以输入中文了)

