---
date: 2024-02-02
authors: [lzliangzh]
tags: 
  - 折騰
---



# 易用的 Linux/Unix 终端

终端里常用的软件，以及常用 GUI 软件在 Terminal 下的平替。可供查询。

<!-- more -->

## 常规用法

| 常规用法 | 应用 |
| ---------------- | --- |
| 可视化的文件管理器 | ranger |
| 多彩的文本编辑器 | nano(写作)，vim(编程) |
| 多彩的 Markdown 查看器 | glow |
| 邮件收发 | mutt,msmtp,fetchmail,procmail 组合 |
| 网页浏览 | lynx 或者一个基于 docker 的可视化浏览器(github) |
| 人工智慧支持 | tgpt(github) |
| 词典翻译 | wd(无道词典, github) |
| 科学知识 | clash |
| 微信命令行版本 | wechatcmd |
| 微信聊天记录总结机器人 | ？ |
| 网易云音乐（基于Web端）| musicfox |
| 图片、pdf显示 | viu, 或者 lslx 项目|
| 文字版pdf转html并显示 | pdf2html + w3m |
| 表格处理 | sc |

自动补齐插件: aspell

文字版pdf转html，效果并不太好，而且html也是纯文本。比较难受的点是，这样转换出来的html断行是非常不自动的。最好还是找到「电子书」格式的电子书（一般有能转换pdf版本的电子书，都有更「数位化」格式），用 
Calibre 软体下的`ebook-convertor [Input File] [Output File]`解包为多个 html 文件来阅读（如 epub 等）。

## 网络连接

| 网络用法 | 应用 |
| --- | --- |
| 显示当前局域网 IP、公网动态 IP | curl cip.cc 与 ifconfig |
| 开启服务器功能 | (1)作为局域网内下载服务器：http-server; (2)利用 ssh + scp 作为上传 & 下载服务器; (3)作为git服务器 |
| 作为备份服务器 | 用 `rsync -r` 进行（初次）差异备份，`rsync -avur --progress --delete <local> <remote>`<br />参考：https://www.cnblogs.com/sunsky303/p/11775432.html |


## 系统检测
| 监测项目 | 应用 |
| --- | --- |
| 全局监测 | conky, top, powertop(功耗) |
| 网速 | speedtest-cli, 运行 speedtest 命令；nload |


## 一些 Github 项目地址

| Github 项目 | 地址 |
| --- | --- |
| 基于 docker 的可视化浏览器 | (在 Mac 上要首先安装 colima 进入虚拟 ubuntu 环境，即运行前两行代码) |
| tgpt | https://github.com/aandrew-me/tgpt, curl -sSL https://raw.githubusercontent.com/aandrew-me/tgpt/main/install \| bash -s /usr/local/bin | 
| wd | https://github.com/maxzhx/WuDaoDictionary，但由于是爬虫技术，所以可能不太稳定 |
| wechatcmd | go get -u github.com/liushuchun/wechatcmd |
| musicfox | brew install anhoder/go-musicfox/go-musicfox |
| lsix 项目 | 操作方法微信简介(见下) |

---

注释

[1]

```
brew install docker colima
colima start
docker run --rm -ti fathyb/carbonyl https://github.com/fathyb/carbonyl
```

[2] lsix 项目——操作方法微信公众号简介：https://mp.weixin.qq.com/s?__biz=MzU3NTgyODQ1Nw==&mid=2247485577&idx=1&sn=481418e5efdfd0b06095c6e07d890628&chksm=fd1c700fca6bf9194a6657ab06562f4f0890967d7491880804d0c9aa08a983ee1ab14a4daf34&token=1994080286&lang=zh_CN#rd

[3] which <package_name>: 寻找软件包所在地

[4] 非 Homebrew 安装的包，如何卸载 Uninstalling?

```
sudo rm $(which tgpt)
```

