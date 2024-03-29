---
title: Windows下Aria2下载器最佳配置
date: 2021-12-11 16:47:42
tags: aria2
categories: Tips
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/1639212516820d6dd3810f72506d006d3f23c67acd5a7.jpeg
---
Windows下Aria2下载器最佳配置
<!-- more -->

# 下载安装

最好不要在乱七八糟的地方下载别人打包的，就用官方的自己配置就好。

在github下载最新版：

[aria2下载地址](https://github.com/aria2/aria2/releases)

软件不需要安装，下载好之后直接解压到自己要安装的目录即可

# 软件配置

在安装目录下新建两个文件：

会话文件```aria2.session```,建立空文件即可。

配置文件```aria2.conf```:

填入如下内容，可以根据需求自己更改，主要就改

- 会话文件路径：```input-file```和```save-session```,根据实际情况填写。
- 默认下载路径：```dir```
- 访问密钥：```rpc-secret```,也就是一些地方连接时候需要的token。

```yaml
## '#'开头为注释内容, 选项都有相应的注释说明, 根据需要修改 ##
## 被注释的选项填写的是默认值, 建议在需要修改时再取消注释  ##

## 进度保存相关 ##

# 从会话文件中读取下载任务
input-file=D:\SoftWares\Aria2\aria2.session
# 在Aria2退出时保存`错误/未完成`的下载任务到会话文件
save-session=D:\SoftWares\Aria2\aria2.session
# 定时保存会话, 0为退出时才保存, 需1.16.1以上版本, 默认:0
#save-session-interval=60

## 文件保存相关 ##

# 文件的保存路径, 默认: 当前启动位置
dir=D:\Dir\download
# 启用磁盘缓存, 0为禁用缓存, 需1.16以上版本, 默认:16M
#disk-cache=32M
# 文件预分配方式, 能有效降低磁盘碎片, 默认:prealloc
# 预分配所需时间: none < falloc ? trunc < prealloc
# falloc和trunc则需要文件系统和内核支持
# NTFS建议使用falloc, EXT3/4建议trunc, MAC 下需要注释此项
#file-allocation=none
# 断点续传
continue=true

## 下载连接相关 ##

# 最大同时下载任务数, 运行时可修改, 默认:5
#max-concurrent-downloads=5
# 同一服务器连接数, 添加时可指定, 默认:1
max-connection-per-server=16
# 最小文件分片大小, 添加时可指定, 取值范围1M -1024M, 默认:20M
# 假定size=10M, 文件为20MiB 则使用两个来源下载; 文件为15MiB 则使用一个来源下载
min-split-size=10M
# 单个任务最大线程数, 添加时可指定, 默认:5
split=32
# 整体下载速度限制, 运行时可修改, 默认:0
#max-overall-download-limit=0
# 单个任务下载速度限制, 默认:0
#max-download-limit=0
# 整体上传速度限制, 运行时可修改, 默认:0
#max-overall-upload-limit=0
# 单个任务上传速度限制, 默认:0
#max-upload-limit=0
# 禁用IPv6, 默认:false
#disable-ipv6=true
# 连接超时时间, 默认:60
#timeout=60
# 最大重试次数, 设置为0表示不限制重试次数, 默认:5
#max-tries=5
# 设置重试等待的秒数, 默认:0
#retry-wait=0

## RPC相关设置 ##

# 启用RPC, 默认:false
enable-rpc=true
# 允许所有来源, 默认:false
rpc-allow-origin-all=true
# 允许非外部访问, 默认:false
rpc-listen-all=true
# 事件轮询方式, 取值:[epoll, kqueue, port, poll, select], 不同系统默认值不同
#event-poll=select
# RPC监听端口, 端口被占用时可以修改, 默认:6800
#rpc-listen-port=8280
# 设置的RPC授权令牌, v1.18.4新增功能, 取代 --rpc-user 和 --rpc-passwd 选项
rpc-secret=666666
# 设置的RPC访问用户名, 此选项新版已废弃, 建议改用 --rpc-secret 选项
#rpc-user=<USER>
# 设置的RPC访问密码, 此选项新版已废弃, 建议改用 --rpc-secret 选项
#rpc-passwd=<PASSWD>
# 是否启用 RPC 服务的 SSL/TLS 加密,
# 启用加密后 RPC 服务需要使用 https 或者 wss 协议连接
#rpc-secure=true
# 在 RPC 服务中启用 SSL/TLS 加密时的证书文件,
# 使用 PEM 格式时，您必须通过 --rpc-private-key 指定私钥
#rpc-certificate=/path/to/certificate.pem
# 在 RPC 服务中启用 SSL/TLS 加密时的私钥文件
#rpc-private-key=/path/to/certificate.key

## BT/PT下载相关 ##

# 当下载的是一个种子(以.torrent结尾)时, 自动开始BT任务, 默认:true
#follow-torrent=true
# BT监听端口, 当端口被屏蔽时使用, 默认:6881-6999
listen-port=51413
# 单个种子最大连接数, 默认:55
#bt-max-peers=55
# 打开DHT功能, PT需要禁用, 默认:true
enable-dht=false
# 打开IPv6 DHT功能, PT需要禁用
#enable-dht6=false
# DHT网络监听端口, 默认:6881-6999
#dht-listen-port=6881-6999
# 本地节点查找, PT需要禁用, 默认:false
#bt-enable-lpd=false
# 种子交换, PT需要禁用, 默认:true
enable-peer-exchange=false
# 每个种子限速, 对少种的PT很有用, 默认:50K
#bt-request-peer-speed-limit=50K
# 客户端伪装, PT需要
peer-id-prefix=-TR2770-
user-agent=Transmission/2.77
# 当种子的分享率达到这个数时, 自动停止做种, 0为一直做种, 默认:1.0
seed-ratio=0
# 强制保存会话, 即使任务已经完成, 默认:false
# 较新的版本开启后会在任务完成后依然保留.aria2文件
#force-save=false
# BT校验相关, 默认:true
#bt-hash-check-seed=true
# 继续之前的BT任务时, 无需再次校验, 默认:false
bt-seed-unverified=true
# 保存磁力链接元数据为种子文件(.torrent文件), 默认:false
bt-save-metadata=true
```

# 开机后台运行

在安装目录新建```start.vbs```文件，右键编辑填写以下内容：

```vbscript
CreateObject("WScript.Shell").Run "D:\Softwares\Aria2\aria2c.exe --conf-path=D:\Softwares\Aria2\aria2.conf",0,True
```

注意更改其中的```aria2c.exe```与```aria2.conf```的实际路径。

然后将这一文件复制到```C:\Users\用户名\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\```目录下即可开机启动，注意该脚本有可能会被杀毒软件删除，要将其添加到白名单。

# 浏览器插件

由于aria2是在后台运行的，为了方便查看下载进度，可以安装一个浏览器插件：

edge：[安装地址](https://microsoftedge.microsoft.com/addons/detail/aria2-for-edge/jjfgljkjddpcpfapejfkelkbjbehagbh)

chrome：[下载地址](https://www.extfans.com/productivity/mpkodccbngfoacfalldjimigbofkhgjn/)

安装完成后对扩展进行一些设置：

![image-20211211170918454](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211211170918454.png)

完成后保存，插件图标如果是这样说明连接成功：![image-20211211171017386](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211211171017386.png)

到此aria2下载器配置完成，可以完全接管浏览器下载任务，在使用某些网盘脚本时也可以一键发送到aria2进行下载。

下载文件测试：

![image-20211211171614891](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20211211171614891.png)