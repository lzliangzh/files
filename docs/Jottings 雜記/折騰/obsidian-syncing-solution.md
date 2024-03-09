---
date: 2024-01-23
authors: [lzliangzh]
tags: 
  - 折騰
---



# obsidian/git/gitee 三端笔记同步解决方案

<!-- more -->

## 准备工作：获取 SSH 公钥并在 gitee 配置

获取手机、电脑的 SSH 公钥，添加到所创建的 gitee 私有仓库

**电脑端**：在命令行中输入`ssh-keygen -t rsa -C "你的邮箱"`，然后连续输入三个回车，在 `Your public key has been saved in` 后显示的是公钥的存储位置。打开 .ssh 文件夹，用记事本打开 .pub 文件，将刚刚生成的公钥文件复制到 gitee 设置公钥处，并给公钥添加标题即可。

**手机端**：在设置页面，点击「SSH Keys」>「+」，新建 SSH 密钥，然后编写一个文件的名称然后生成key

## 手机上传下载

1. 在设置界面的「Root storage location for repos」如下图，这个位置用于存放 Android 设备上 Obsidian 笔记的路径（位置要记住、到时候obsidian方便选择存储位置，他两才能在同个位置），记得要自己去设置一个文件夹为他的存放目录。
2. 回到主页面，点击右上角“+”号 Clone Repository，Remote URL 为 gitee 地址，Local Path 为步骤 1 设置的路径。点击克隆即可，这个时候就会把Git上的笔记仓库缓存到你一开始设置的「Root storage location for repos」地址上了

## 电脑上传下载

1. 如果是第一次使用的话需要输入用户名和邮箱

   ```
   git config --global user.name '你的用户名'
   git config --global user.email'你的邮箱'
   ```

   这里只是在你提交的时候仓库会留下记录，告诉仓库是谁提交的，可以不用和注册时使用的email相同。如果不确定自己之前有没有设置用户名和邮箱可以用`git config --list`查看。
2. 把终端引入到想要共享的文件夹中，输入

   ```
   git init
   ```

   可以看到此时生成了一个 .git 文件夹
3. 将数据提交到暂存区

   ```
   git add .
   ```
4. 将暂存区的内容提交到本地仓库，并添加备注

   ```
   git commit -m "备注内容"
   ```
5. 创建本地仓库与远程仓库的连接

   ```
   git remote add origin 远程 git/gitee 仓库地址
   ```
6. 将文件上传到远程仓库

   ```
   git push -u origin main:master
   ```
   1. 这里使用的`-u` 的作用是，如果第一次 push 的时候使用了 `-u`，那之后再 push 的时候就可以直接用 git push，后面的不用写了。
   2. `origin` 是「**远程库别名**」，`main:master`是「**本地分支名∶远程库分支名**」。当本地分支名和远程库分支名名称不同时，需要两边都指明，否则会持续出现如下等错误

      ```
      fatal: Need to specify how to reconcile divergent branches...
      ========================
      error: src refspec master does not match any
      error: failed to push some refs to 'https://gitee.com/giteeliangz/notes-by-obsidian-android'
      ```