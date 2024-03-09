---
date: 2024-01-24
authors: [lzliangzh]
tags: 
  - 折騰
---



# 倒腾札记: Android Termux 环境下 ubuntu 安装、配置与用法

想要把手机变成小主机，毕竟安卓也是基于 Linux 的，无意间发现安卓手机上可以用 Android Termux 弄成衣蛾

<!-- more -->

## ubuntu 安装

1. 安装 F-droid 开源商店
2. 从 F-droid 中下载 Termux 和 AnLinux
3. 按照 AnLinux 提示安装 ubuntu
4. 安装 KDE 桌面环境（Xfce4 似乎会出错？）

## ubuntu 配置与用法

1. 建议新建管理员账户并使用之，尽量不使用 root 账户。root 账户也要记得修改密码并记住。
2. **安装基本软件**：Chromium, WPS Office, VSCode, Sougoupinyin。都要挑选 arm64 版本。 WPS Office, VSCode 安装顺利。
   1. `sudo apt-get install <package_name>` 安装源里的软件包，`sudo dpkg -i` 安装本地下载的 deb 包， `aptitude` 强大的软件包管理器
   2. `sudo apt-get remove/autoremove <package_name>` 删除
   3. `sudo apt-get -f install` 或 `sudo apt --fix-broken install` 自动化解决依赖关系问题
   4. `wget/curl/git clone` 下载网络上的文件
3. **踩坑：**
   1. 由于 anlinux 安装的 ubuntu 不知为何 snap 一直无法安装，而像 Firefox, Chromium 等浏览器等类应用，如果只通过命令行安装，就需要使用 snap，因此要换种思路，下载 .deb 包并使用 deb 包管理器 `dpkg -i` 安装。
   2. 此外，发现对于 Ubuntu 22.04 (maybe not LTS) 及其所配置的源，Firefox & Chromium 最新版的 .deb 包安装过程中均会出现依赖关系问题（部分软件包版本较老）。尝试使用 `sudo apt-get -f install` 解决，发现电脑要求删除；尝试使用 `sudo apt --fix-broken install` 无果；尝试使用 `sudo apt-get update` 却无法自动升级（应该是源里的包最新就到这个版本）；换 Tsinghua 源、UTSC 源均无果。
   3. 无奈只能寻找老版本软件包。安装成功了。
   4. ==**总结**：电脑要求删除就别硬钢了！说明依赖关系电脑自动化程序解决不了了。尝试换低版本的 deb 包==
   5. **注意**：dpkg 后加 --ignore-depends 可以忽略依赖【慎用】
4. 配置基于 fctix 的 搜狗输入法【尚未完成】。

## Termux Linux 基础命令

### Termux 软件包管理

除了`apt`命令，Termux 还提供`pkg`命令进行软件包管理。

```bash
# 安装软件包
$ pkg install [package name]

# 卸载软件包
$ pkg uninstall [package name]

# 列出所有软件包
$ pkg list-all
```

其实，`pkg`的[底层](https://github.com/termux/termux-packages/issues/2151#issuecomment-486184252)就是`apt`，只是运行前会执行一次`apt update`，保证安装的是最新版本。所以，`apt install sl`基本等同于`pkg install sl`。

Termux 支持的软件包清单，可以到[这里](https://github.com/termux/termux-packages/tree/master/packages)查看。

### Termux Linux 基础命令 (Ed. 1)

cd：(切换)
vim:(创建文件）   vi：编辑文件
bc：（计算器）quit：退出计算器
mkdir：（创建目录）   mkdir -p：递归建立目录
rmdir：（删除目录）
arch：（显示处理器X86）
hostname：（显示系统名称）
who：（显示目前登陆用户的信息）
cat：（查看文件）  more：（查看全部内容）
ls：（查看当前目录或文件）
pwd：（显示当前位置）
date：（显示当前日期和时间）
logout：（注销）
reboot；（重启）   init 6 :(重启）
inito：（关机）
rm:(删除） rm -rf：（删除任何文件）
echo：（回显内容）
touch：（创建文件）   touch  。 。 。：（创建在同意目录下多个文件）
wc -l：（查看文件数量或文件行数）
tail：（查看文件倒数十列）    
tac:(文件倒序）
head：（查看文件前十行）  head -。：（加-几就显示几行）
grep：（过滤）  参考：cat 123 | grep 我在家
passwd：（更改用户密码)  passwd root:(指定更改用户密码）
df：（查看磁盘使用情况）
top：（查看内存，CPU性能）
Netstat：（显示各种网络相关信息）  （光驱）（目录）
mount：（挂载本地文件或磁盘） 参考：mount/dev/sr0 /opt
Umount：（删除挂载）
free：（查看内存使用情况）  （文件名）（目录名）
mv：（移动文件或目录）  参考：mv 123 nihao   （ 参数）    （   文 件 名    )
find:(查找）   参考：find 路径 -name ifcfg-eth0
su:(切换用户）
EXIT:(退出登录）
userdel：（删除用户） 参考：userdel 123
graupadd：（创建组名）
groupdel：（删除组）
iostat：（查看磁盘状态）（导出）（文件名）（安装包）
sz：（导出文件）   参考：sz 123 lrzsz
yum install：（安装软件包）
tar xvf 文件名·tar·gz ：（解压） nginx：（服务安装包）
Unzip：（解压以zip结尾的文件）
ps -Aux：（查看当前运行的进程）
wget：（下载）wget 下载东西的链接
du：（查看文件或目录大小）
kill：（杀掉） 参考：kill 1231
clear：（清屏）（月）（年）
cal：（显示日历）    参考：cal 4 2016
cp：（复制）    （属性）   ( 文    件   名 ）
chmod：（修改文件权限）  参考： chmod 357 123.txt  （文件名） 
chwon：（修改文件属主属组）  参考：chown 123：321  123 
 （属主）（属组） 

### Linux中一些基础命令 (Ed. 2)
(1) pwd：显示当前所在位置的绝对路径

(2) cd+路径：切换当前工作位置

(3) cd . ：退回到当前位置

(4) cd .. ：退回到上一层

(5) ls：默认显示当前位置当前目录下的内容

(6) clear ：清屏，相当于翻页

(7) cd ~ ：直接进入到当前用户的家目录

(8) cd - ：切换到上一次所在位置，在两个位置间来回切换

(9) mkdir + 文件名：创建一个目录（文件夹）

(10) touch + 文件名：创建一个普通文件

(11) man ：查看帮助手册 （1）代表命令（2）代表系统调用（3）代表库函数

    例：man printf ：查询命令printf
      man 3 printf ：查询库函数printf

(12) rm：删除文件（删除目录文件用 rm -r）

      rmdir 目录名：删除空目录
      rm -r 目录名 ：删除非空目录

(13) cp：拷贝文件

    拷贝普通文件： cp 源文件的路径+文件名 目的路径
    拷贝目录文件： cp -r 源目录文件路径+目录名 目的路径
    拷贝+重命名：  cp 源文件路径+文件名 目的文件+文件名

思考：cp -r 目录文件 tmp1 执行两次，两次结果为何不同？

代码示例：



第一次执行 tmp1目录文件不存在，所以是拷贝dir123文件并重命名为tmp1；第二次执行已经存在tmp1文件，将tmp1当成路径，将dir123拷贝到tmp1目录下

(14) mv：剪切文件

    移动普通文件：mv 源文件路径+文件名 目的路径
    移动目录文件：与移动普通文件一样，不需要加-r
    剪切并重命名： mv 源文件路径+文件名 目的路径+新文件名
    重命名：mv 源文件路径+文件名 源文件路径+新文件名

(15) find：查找

    find 搜索路径 -name 文件名（按文件名搜索）
    find 搜索路径 -cmin -n(搜索过去几分钟内修改的文件)
    find 搜索路径 -ctime -n（搜索过去几天内修改的文件）

(16) grep：在文件中过滤出包含制定字符串的行

    grep 字符串 文件名

(17) | ：管道命令

    将前一个命令的输出结果作为后一个命令的输入，一般与过滤结合使用。例：ls | grep test

ls \bin | grep sh

(18) wc :统计文件中单词的个数（-w），字符的个数（-c），行数（-l）

        wc -w 文件名 wc -c 文件名  wc -l 文件名

(19) su :切换用户

      sudo su ：切换为管理员   退出：exit
      su 用户名：切换为其他用户  退出：exit

(20)关机与重启

      shut down -h now ：立刻关机
      halt：关机  init 0 ：关机
      shut down -r now ：立即重启
      reboot：重启    init 6 ：重启

(21) 查看系统运行级别

      0:关机  1:单用户模式 2:多用户无网络服务  3:完全的多用户 文本界面  4.未定义或自定义  5.图形化界面  6.重启

(22) 其他命令及小知识点

     1.tab补全,按上下键查阅执行过的命令
      2.ctrl - 调小窗口  ctrl +shift+ + 调大窗口
      3.Ctrl+Alt: 释放鼠标
      4.history: 查看终端的所有的历史命令