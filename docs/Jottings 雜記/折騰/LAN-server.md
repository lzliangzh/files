---
date: 2024-01-29
authors: [lzliangzh]
tags: 
  - 折騰
---



# PC/Mac 与 Android Termux 互传实现

一些小小的网络尝试，主要是基于 ssh(还有 scp 命令) 的上传下载。

<!-- more -->

## 0\.允许 Termux 访问手机文件

手机 App 默认只能访问自己的据，如果要访问手机的存储，需要请求权限。

```bash
$ termux-setup-storage
```

执行上面的命令以后，会跳出一个对话框，询问是否允许 Termux 访问手机存储，点击"**允许**"。

这会在当前目录下生成一个`storage`子目录，它是手机存储的符号链接，后文下载文件就是到这个目录去下载。

`storage`目录下有一个`shared`文件夹，这个文件夹映射着手机的主目录。

## 玩法1.架设 Server

通过 Node.js 运行 HTTP Server，使得局域网内的其他设备可以通过子啊浏览器访问本机 IP，来下载本机服务器上的文件。

在此之前，先安装 Node.js。

```bash
$ apt install nodejs
```

然后，把 npm 的源换成淘宝镜像，保证网速。

```bash
$ npm config set registry https://registry.npmmirror.com
```

安装 npm 模块`http-server`。

```bash
$ npm install -g http-server
```

然后，运行 Server。

```bash
$ http-server
```

正常情况下，命令行会提示 Server 已经在 8080 端口运行了，并且还会提示外部可以访问的 IP 地址。

## 玩法2.配置 ssh 、 ssh 连接

首先，安装好 ssh。在 Termux 中安装好 ssh，使用`pkg install openssh`。PC/Mac 一般预装有 ssh。

对于 Termux，安装好后，一定要给 Termux 设置用户密码。

```bash
$ passwd
```

然后，在\*\*准备被连接的终端 B \*\*上，启动 ssh 服务。注意：默认端口为22。

```bash
$ sshd -p [端口]
```

在 Windows 终端上，如果输入`ssh`/`sshd`报错，则应该是没有安装 OpenSSH 服务的缘故。以 Windows 10 终端为例，`Win+S`搜索打开「可选服务」，安装「OpenSSH 服务端」；完成后，同样搜索打开「服务」，将 OpenSSH SSH Server 启动方式改为自动；然后，在 Powershell 中输入：

```powershell
net start sshd
sshd -p 1105
net stop sshd # 关闭 ssh 端口
```

在 Mac/linux 终端上，往往会出现`sshd re-exec requires execution with an absolute path `的错误。通过`whereis sshd`找到`sshd`的绝对路径后，将`sshd`替换为绝对路径`/usr/sbin/sshd`，又出现`sshd: no hostkeys available -- exiting.`错误。最终发现是权限不够造成的。因此，改为输入下面的指令，启动 ssh 服务：

```bash
$ sudo /usr/sbin/sshd -p [端口]
```

在**待连接服务器的终端 A** 上，输入

```bash
$ ssh username@serverip
$ ssh -p [端口] username@serverip # 非默认端口时
```

其中，username是你的登录账户，serverip是你的服务器IP地址。如果你的服务器监听的是非默认端口（默认端口为22），则需要在连接时指定端口号。这样**终端 A 就连接上服务器 B 了。**

> 查询当前终端所使用的公网 IP
>
> ```bash
> curl cip.cc
> ```

## 玩法3.ssh 下载与上传

在SSH下载服务器文件的命令格式为：

```bash
$ scp username@serverip:/path/to/remote/file /path/to/local/directory
```

SSH上传本地文件的命令格式为：

```bash
$ scp /path/to/local/file username@serverip:/path/to/remote/directory
```

需要注意的是，SSH下载和上传文件均需要对服务器登录账户有读写权限。如果在下载或者上传文件时提示权限不足，则需要修改文件的权限或者使用管理员账户进行操作。