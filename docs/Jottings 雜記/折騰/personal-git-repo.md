---
date: 2024-01-23
authors: [lzliangzh]
tags: 
  - 折騰
---



# 个人 Git 仓库使用设置

## 目标
* 将旧手机 iQOO 3 用作个人 Git 仓库服务器，实现私有化。
* （不一定能实现）将服务器接入公网，实现真远程访问。

<!-- more -->

## 实现方式

### 服务器设置

 1. 用 AnLinux 在 Android Termux 上安装 ubuntu
 2. 设置`./start-ubuntu`自启动：

    ```bash
    $ cd /data/data/com.termux/files/usr/etc/
    $ vim termux-login.sh
    # 添加语句： ./start-ubuntu
    ```
3. 进入 ubuntu 后，安装`vim, git, ssh`等必要的包。如果安装出现类似`code (1)`的错误，则先`apt update`+`apt upgrade`，后安装。
   
4. 新建用户 git 并设置密码，（然后编辑`/etc/passwd`使 git 无法访问终端，提高安全性---此操作似乎有问题）。注意：设置密码一定要在阻断终端之前！
   ```bash
   $ su git
   # 按要求设置密码
   $ exit
   $ vim /etc/passwd
   # 将文档中 git:x:1000.../bin/bash 改成 .../bin/git-bash
   ```

5. 移动到想要作为远程 Repo 的目录，输入以下指令初始化并赋权
   ```bash
   $ sudo git init --bare .
   $ chown -R git:git /root/repository/mainRepo #也就是目录
   ```

6. 启动 ssh 服务 **（第一次操作以后，只需要管理 ssh 即可）**
   ```bash
   $ /usr/sbin/sshd -p 端口号
   # 如果出现无法访问某目录，则尝试访问之，如无则手动创建，如有则手动赋权
   ```
   > 对于 ssh 服务的管理
   > 
   > 1. 启动 ssh 服务：除了上面的指令，还可以用如下指令实现。但不知端口设置如何。
   > ```bash
   > $ service ssh start # 要关闭，就用 stop
   > ```
   > 2. 查看 ssh 服务状态
   > ```bash
   > $ service ssh status
   > ```

至此，服务器的设置结束，该终端已被设置为可用的 git 服务器。

### 客户端访问

```bash
$ git clone ssh://git@serverip:port/path
```