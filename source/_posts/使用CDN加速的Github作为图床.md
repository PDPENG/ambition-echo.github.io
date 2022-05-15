---
title: 使用CDN加速的Github作为图床
date: 2021-12-15 22:20:50
tags: [picgo,github]
categories: Tips
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211215230811.png
---
使用CDN加速的Github作为图床。
<!-- more -->

> 本文全部图片均使用CDN加速的GitHub作为图床

写博客免不了要用到图床，想要搭建免费的图床，一般就两个选择，github或者gitee，但是这二者各自有各自的优缺点，gitee由于是国内的，访问速度快，但是空间限制比较大，而且单个图片的大小限制也很难受，github虽然没有这些限制，但是由于种种原因，访问速度非常慢。

为了解决这个问题，我们可以使用CDN加速的github作为图床。

访问[jsDelivr - A free, fast, and reliable CDN for open source](https://www.jsdelivr.com/)可以看到，这个网站提供对GitHub的CDN加速服务：

![image-20211216104925942](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216104925942.png)

只要按照这一格式访问你的github仓库中的资源，访问速度就会非常快：

```
https://cdn.jsdelivr.net/gh/用户名/仓库名/文件路径
```

这样一来，我们就可以把github作为图床，然后使用图片时使用这样的链接就可以了。

# 使用PicGo

为了方便上传图片到图床，可以下载PicGo，全平台支持，非常方便。

![image-20211216105305955](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216105305955.png)

要在PicGo中使用Github作为图床，需要手动设置。

填写如下选项：

![image-20211216105511591](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216105511591.png)

- 仓库名就是新建的作为图床仓库名称，注意格式：用户名/仓库名
- 分支名默认为main
- Token需要到GitHub的setting中生成，权限只需要勾选repo

即可

![image-20211216105739131](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216105739131.png)

最后，需要设置自定义域名为```https://cdn.jsdelivr.net/gh/用户名/仓库名```,这样默认复制的图片链接就是经过CDN加速的链接了。

设置完成后即可测试上传图片了。

# 使用Typora

使用Typora编写MarkDown时，为了方便的插入图片，可以在设置中开启图片自动上传。使用这一功能的前提是已经配置好了PicGo。

![image-20211216110150350](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216110150350.png)

设置好PicGo路径之后，验证图片上传选项，上传成功就可以开始使用了，这样设置之后，在编写MarkDown时，只要将图片直接在文章中粘贴，就可以自动上传然后生成MarkDown格式的链接，非常方便。

![image-20211216110425381](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216110425381.png)

# 使用utools

有时候不需要在MarkDown中插入，只是单纯的需要获取上传后的链接，可以直接复制后按PicGo的快捷键Ctrl+Shift+P，但这个快捷键还是不太方便，可以编写utools的自动化脚本：

在utools中按照插件```自动化助手```

打开后点击我的自动化，新建自动化

编写如下代码：

```javascript
if (ENTER.type === 'files') {
  if (!utools.copyImage(ENTER.payload[0].path)) return
}
utools.simulateKeyboardTap('p', 'ctrl', 'shift')
```

然后设置关键字：

![image-20211216110844499](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216110844499.png)

保存后就可以使用了

使用方法：

1. 截图后复制到剪切板，按对应按键呼出utools超级面板后点击上传到图床：
![image-20211216111016011](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216111016011.png)
2. 在资源管理器中点击图片文件，然后呼出utools超级面板，点击上传到图床：

![image-20211216111211581](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211216111211581.png)



至此就可以愉快的使用Github作为图床啦！

