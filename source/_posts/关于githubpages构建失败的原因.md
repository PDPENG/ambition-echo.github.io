---
title: 关于githubpages构建失败的原因
date: 2021-05-16 22:45:54
tags: hexo
categories: Tips
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/20211114221405.png
---
今天在写了两篇博文后推送到github，hexo的构建顺利通过了，在本地服务器测试也没有任何问题，但是github pages页的build就是会报错，而且没有任何提示，查看[官方文档](https://docs.github.com/cn/pages/setting-up-a-github-pages-site-with-jekyll/troubleshooting-jekyll-build-errors-for-github-pages-sites#invalid-highlighter-language)后终于排查到了问题所在。
<!-- more -->

看到文档所列的问题，第一眼就感觉到是markdown的代码块的问题，因为前一篇文章的latex代码在本地测试时高亮没有问题，但在推送后确没有正常高亮，这就不难发现hexo构建时对代码高亮的处理与markdown不是互通的。

查看我新发布的两篇博文，一篇中用了 bash 高亮，另一篇用了markdown高亮，鉴于初始文章中用过bash高亮，所以极有可能githubpages不支持markdown的高亮，更改之后，果然构建成功了。

所以遇到问题查官方文档，总是有点用的