---
title: Linux
date: 2021-08-20 16:53:15
tags: Linux
categories: Learn
cover: https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/2021-11-13_14-26%20(2).png
---
Linux与Unix可以说是父子关系，学习了Linux，Unix也可以很容易上手，Mac OS是类Unix系统。
<!-- more -->

# 1 Linux简介

## 1.1 UNIX简介

Linux与Unix可以说是父子关系，学习了Linux，Unix也可以很容易上手，Mac OS是类Unix系统。

## 1.2 Linux简介

### Linux内核

Linux内核是Linux系统的核心，是有linus与其团队联合开发与管理的，在其官方网站[The Linux Kernel Archives](https://www.kernel.org/)发布各个版本的内核，都是开源的，任何人都可以在这内核的基础上进行开发，发布自己的发行版。

### Linux发行版

Linux发行版是各个公司在Linux内核的基础上进行开发发行的操作系统，这些操作系统的底层都是一样的Linux内核，所以都是Linux操作系统，主流的发行版分为两个分支，`Readhat`和`Debian`,国内做的比较好的发行版有基于Ubuntu的优麒麟和`deepin`深度操作系统。

![image-20210819232508265](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210819232508265.png)

## 1.3 安装Linux

### 磁盘分区

分区分为主分区、扩展分区，逻辑分区，主分区加扩展分区最多只能有四个，扩展分区最多只能有一个，扩展分区不存储数据，只用来包含逻辑分区，这些限制不是系统的限制，而是硬盘的限制。

![image-20210820001501844](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210820001501844.png)

例如图，1，2，3为主分区，4为扩展分区，5，6为逻辑分区。

### 格式化

硬盘分区后还是不能写入数据，还得进行格式化才可以。

我们通常所说的格式化是`高级格式化`，又叫`逻辑格式化`，它是指用用户指定的`文件系统`，在磁盘的特定区域写入特定数据用来存储文件目录表，分配表等数据，用来在磁盘中高效地读写数据。

常见的文件系统：Windows可以识别的文件系统（FAT16,FAT32,NTFS）,Linux可以识别的文件系统（EXT2,EXT3,EXT4）

### 硬件设备文件名

在Windows中，一块硬盘经过分区，格式化之后，只要分配盘符就可以正常使用，但在Linux系统中还需一个步骤，就是建立`硬件设备文件名`。

在Linux中有一个概念，所有的硬件都是文件，在Linux的根目录下有一个`dev`文件夹，这里面存储了所有的硬件设备文件。

![image-20210820002804794](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210820002804794.png)

例如上图中`/dev/hda`就表示IDE接口的第一块硬盘，`/dev/sdb`表示SATA接口的第二块硬盘，依次类推。

除此之外，每块硬盘的每个分区都需要 建立设备文件名，硬盘的分区直接再其后面加数字即可，如`/dev/hda1`表示IDE接口的第一块硬盘的第一个分区。

以上这些设备文件名都是固定的，系统自动检测的，不需要自己设置，只需看懂即可。

### 分区表示

比较常用的分区方法

<img src="https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210820003812839.png" alt="image-20210820003812839" style="zoom: 50%;" />

分一个主分区，一个扩展分区，其他的全部为逻辑分区，无论有几个主分区，第一个逻辑分区编号一定是5，因为1-4这四个编号只能给主分区和扩展分区使用。另外，分区编号也是系统自动检测的。

### 挂载

Linux系统中的挂载，相当于Windows系统中的分配盘符，但不同的是，Linux中指定的是挂载点，且有一定要求。

必须挂载：

- `/`（根目录）
- `swap`（虚拟内存，最多2G即可）

推荐挂载：

- `/boot`（启动分区，200M足矣）

给分区挂载好之后分区就可以正常使用了。

### 文件系统结构

Linux系统的文件系统结构与Windows不同，Windows中的不同盘符是相互独立，相互并列的，在硬盘上也是如此体现，但在Linux中不是这样。

<img src="https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210820004810014.png" alt="image-20210820004810014" style="zoom:33%;" />

如图所示是Linux的文件结构，根目录是最高一级目录，其下有一级目录，一级目录下又有二级目录，但与Windows不同的是，比如说`/boot`是/根目录下的一级目录，但是在硬盘上，`/boot`是有独立的硬盘空间的，不占`/`分区的空间。

<img src="https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210820005050748.png" alt="image-20210820005050748" style="zoom:50%;" />

## 1.4 远程管理Linux

### 查询/更改IP地址

- 查询IP

```shell
$ ifconfig
```

`ifconfig`命令可以显示当前机器的所有网卡信息，其中就有IP地址。

执行效果：

```shell
$ ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.24.134.178  netmask 255.255.240.0  broadcast 172.24.143.255
        inet6 fe80::215:5dff:fee6:971e  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:e6:97:1e  txqueuelen 1000  (Ethernet)
        RX packets 368  bytes 38952 (38.9 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 13  bytes 1006 (1.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

其中eth0就表示本机的第一块网卡，lo表示本机，如上：`172.24.134.178`就是本机的IP地址，而`127.0.0.1`是本地地址，也就是`localhost`

- 更改IP地址

```shell
$ ifconfig eth0 192.168.2.155
```

### 远程连接

远程连接服务器时，只要输入正确的IP地址并用正确的用户名密码登录，即可远程管理Linux系统。

## 1.5 Linux各目录作用

![image-20210821173605287](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210821173605287.png)

![image-20210821173520761.png](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210821173520761.png) 

![image-20210821173820628](https://cdn.jsdelivr.net/gh/ambition-echo/img_bed/img/image-20210821173820628.png)



# 2 Linux基本操作

 ## 2.1 Linux命令格式

Linux作为一个主要在服务器上运行的操作系统，其强大之处在于它的命令行`shell`，类似与Windows中的`cmd`和`powershell`。学习Linux就是学习`shell`的基本操作。

- Linux命令的基本格式：

- ```shell
  命令 -[选项] [参数] 
  ```

## 2.2 Linux常用命令

### 2.2.1 目录处理命令

#### 查看所有文件：ls

- `ls`命令
- 查看当前目录
- 选项：-a(查看所有文件，包括隐藏文件)  -l(显示文件详细信息)  -d(查看目录属性) -i(显示i节点) -h(人性化显示，即智能显示文件大小)
- 格式：ls -[选项] 路径

```shell
$ ls -l
```

例如执行该命令可以查看当前目录下所有文件的详细信息。

#### 切换目录：cd

- `cd` 命令
- 切换当前目录
- 格式：cd [目录]
- 特别的，`.`表示当前目录，`..`表示当前目录的上一级目录。

```shell
$ cd /home/workspace
```

切换到/home/workspace目录下

```shell
$ cd ..
```

返回上一级目录

#### 创建目录：mkdir

- `mkdir`命令
- 创建目录
- 选项：-p(递归创建)
- 格式：mkdir -[选项] 目录名称

```shell
$ mkdir workspace
```

在当前目录下创建一个workspace目录

```shell
$ mkdir -p worespace/code/python
```

在当前目录下递归创建多级目录

#### 显示当前所在目录：pwd

- `pwd`命令
- 显示当前所在目录

#### 删除空目录：rmdir

- `rmdir`命令
- 删除空目录
- 格式：rmdir [目录]

```shell
$ rmdir python
```

注意：该命令只能删除空目录，如果目标目录非空，则会报错。这点限制也导致这一命令基本没什么用。

#### 复制文件或目录：cp

- `cp`命令
- 复制文件或目录
- 选项：-r(复制目录) -p(保留文件属性)
- 格式：cp -[选项] [原文件或目录] [目标目录]

```shell
$ cp -r /home/workspace/python /home
```

此外，cp命令还可以在复制的同时进行重命名，只需要在目标目录下写要更改的名字即可，但是感觉这一操作没有必要，既然要复制，为啥还要改名，没什么用。

#### 剪切/重命名：mv

Linux下剪切和重命名是同一个命令，由于可以在复制或剪切的同时改名，所以重命名就相当于在将文件剪切到当前目录下的同时改名。

- `mv`命令
- 剪切/重命名
- 格式：mv [原文件或目录] [目标目录]

```shell
$ mv python /root
```

```shell
$ mv python java
```

#### 删除目录或文件：rm

由于rmdir功能的限制，只能删除空目录，没有什么实际意义，`rm`命令可以完全替代`rmdir`命令来进行删除操作。

- `rm`命令
- 删除
- 选项：-r(删除目录) -f(强制执行)
- 格式：rm [选项] [路径]

```shell
$ rm main.c
```

删除当前目录下的main.c 文件

```shell
$ rm -rf /*
```

从删库到跑路。。。。

### 2.2.2 文件处理命令

#### 新建文件：touch

- `touch`命令
- 新建文件
- 格式：touch [文件路径]

注意，文件名最好不要有空格，否则使用非常麻烦，需要用`""`括起来。

```shell
$ touch main.py
$ touch "my java project.java"
```

#### 显示文件内容：cat

- `cat`命令
- 显示文件内容
- 选项：-n(显示行号)
- 格式： cat [文件路径]

```shell
$ cat -n /etc/issue
1  Ubuntu 20.04.2 LTS \n \l
2
$
```

#### 分页显示文件内容：more/less

上一条命令`cat`用来显示短文件没问题，但是特别长的文件，会一直向下拉到最后，只显示最后一屏，中间内容无法查看，这时候就得用`more`命令。

- `more`命令
- 分页显示文件内容
- 格式：more [文件路径]
- 操作：
- - 翻页：空格或f
  - 换行：Enter
  - 退出：q或Q

```shell
$ more /etc/services
#Network services, Internet style
#
#Note that it is presently the policy of IANA to assign a single well-known
#port number for both TCP and UDP; hence, officially ports have two entries
#even if the protocol doesn't support UDP operations.
#
#Updated from https://www.iana.org/assignments/service-names-port-numbers/service-names-p
--More--(2%)
```



可以发现，more命令不支持向上翻页，因此又有一个`less`命令,操作方法与more一模一样，只不过添加加了`page up`和`up`向上翻页的功能。除此之外，`less`命令还提供了搜索功能，在`:`后输入`/[搜索内容]`即可,按`n`查找下一处。

#### 显示文件前几行：head

- `head`命令
- 显示文件前几行
- 格式：head -n [行数] [文件路径]

#### 显示文件后几行：tail

- `tail`命令
- 显示文件后几行
- 选项：-f(动态更新末尾内容)
- 格式：tail -n [行数] [文件路径]

注意：head和tail一样，不指定行数时默认为十行，

### 2.2.3 链接命令

#### 生成链接文件：ln

- `ln`命令
- 生成链接文件
- 选项：-s(生成`软链接`)
- 格式：ln -s [原文件] [目标文件]

#### 软链接

通过实际操作不难发现，软链接非常类似于Windows的快捷方式，软链接文件非常的小，且明确指示了链接导向，这就是软链接的特点。

#### 硬链接

与软链接不同，硬链接更类似于复制，而且是`cp -p`的保留文件属性的复制，除此之外，他与复制的不同之处在于，硬链接文件可以与原文件同步更新。而且，即使原文件丢失，硬链接文件依然可以访问。

- 硬链接不能跨分区
- 硬链接通过i节点来识别
- 不能针对目录使用

### 2.2.4 权限管理命令

#### 权限的rwx表示

- r 读取权限
- w 写入权限
- x 执行权限

在Linux中每个文件对于不同的用户有不同的权限，用户分为三类：

- u 所有者
- g 所属组
- o 其他用户

所以一个文件的完整权限通常由9个字符表示，如`rw-r--r--`。

#### 权限的数字表示

- r---4
- w---2
- x---1

这样表示之后，每种用户所对应的权限可以用一个数字来表示，如一个文件的权限为741，表示所有者拥有rwx所有权限，所属组拥有rw权限，其他用户拥有x权限。

#### 改变文件权限：chmod

- `chmod`命令
- 改变文件访问权限
- 选项：-R(递归修改)(即更改所有子目录及其文件的权限)
- 格式：chmod [{ugoa}{+-=}{rwx}] [文件或目录]或chmod [数字权限] [文件或目录]

```shell
$ chmod g+w main.py
#给所属组添加w权限
$ chmod 755 main.py
#将权限更改为 rwxr-xr-x
```

#### 改变文件或目录的所有者：chown

- `chown`命令
- 改变文件或目录所有者
- 格式：chown [用户] [文件或目录]

```shell
$ chown user1 main.c
#将main.c文件的所有者改为user1
```

#### 查看缺省权限：umask

缺省权限即创建文件或目录时默认的权限，一般目录的缺省权限为rwxr-xr-x,但是对于文件都没有x权限，因此是rw-r--r--。

- `umask`命令
- 查看缺省权限
- 选项：-S(以rwx格式显示权限)
- 格式：umask -S

```shell
$ umask
0022
$ umask -S
u=rwx,g=rx,o=rx
```

### 2.2.5 文件搜索命令

#### 文件搜索：find

- `find`命令
- 搜索文件
- 选项：`-name`(按文件名搜索，*匹配任意字符，？匹配单个字符) `-iname`(不区分大小写) `-size`(根据文件大小查找，+表示大于，-表示小于，=表示等于，单位是数据块，一个数据块是0.5k) `-user`(根据所有者查找) `-group`(根据所属组查找)  `-amin`(访问时间，-表示之内)  `-cmin`(文件属性被修改的时间) `-mmin`(文件内容被修改的时间) `-a`(and) `-o`(or) `-type`(根据文件类型查找，f文件，d目录，l软链接文件) `-ok`(对查找结果进行操作，`-ok 命令 {}/;`) `-inum`(根据i节点查找)
- 格式：find [搜索范围] [选项] [匹配条件]

```shell
$ find /etc -name *init*
#在/etc目录下查找包含init的文件
$ find / -size +204800
#在根目录下查找大于100M的文件
$ find / -user root
#在根目录下查找所有者是root的文件
$ find /home -group root
#在/home目录下查找所属组是root的文件
$ find / -amin -5
#在根目录查找5分钟内访问过的文件
$ find /etc -name *init* -ok ls -l {}\;
#在/etc目录下查找包含init的文件并显示详细信息
```

#### 快速搜索：locate

- `locate`命令
- 基于索引快速搜索
- 选项：`-i`(不区分大小写)
- 格式：locate [文件名]
- 更新索引：`updatedb`

```shell
$ locate inittab
```

#### 查找命令所在目录：which

### 2.2.6 帮助命令

#### 查看命令或配置文件帮助：man

- `man`命令
- 查看命令或配置文件帮助
- 格式：man [命令或配置文件名称]

注意，查看配置文件帮助信息时不能写文件的绝对路径，直接写文件名即可。

```shell
$ man ls
LS(1)                User Commands               LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about the FILEs (the current
nual page ls(1) line 1 (press h for help or q to quit)
```

#### 查看shell内置命令帮助：help

- `help`命令
- 查看shell内置命令帮助
- 格式：help [命令]

```shell
$ help help
help: help [-dms] [pattern ...]
    Display information about builtin commands.
    Displays brief summaries of builtin commands.  If PATTERN is
    specified, gives detailed help on all commands matching PATTERN,
    otherwise the list of help topics is printed.
    Options:
      -d        output short description for each topic
      -m        display usage in pseudo-manpage format
      -s        output only a short usage synopsis for each topic matching
                PATTERN
    Arguments:
      PATTERN   Pattern specifying a help topic
    Exit Status:
    Returns success unless PATTERN is not found or an invalid option is given.
```

### 2.2.7 用户管理命令

#### 添加用户：useradd

#### 设置密码：passwd



### 2.2.8 压缩-解压命令

### 2.2.9 网络命令

### 2.2.10 关机重启命令

#### 关机重启：shutdown

- `shutdown`命令
- 选项：`-h`(关机) `-r`(重启) `-c`(取消前一个命令)
- 格式：shutdown [选项] [时间]

```shell
$ shutdown -h now
#立即关机
$ shutdown -h 20:30
#设置在20:30关机
```

# 3 Vim基本操作

### 3.1 常用操作  

### 3.2 使用技巧

# 4 软件包管理

# 5 shell编程





