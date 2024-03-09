---
date: 2024-03-05
authors:
  - lzliangzh
ping: true
---



# 如何更新 1ntersection 的文件

使用 `rsync` 来更新。特别注意 `<local>` 和`<remote>` 别写反了！

```
rsync -avur --progress --delete ~/myServer/files root@10.6.76.177:/var/snap/nextcloud/common/nextcloud/data/website/
```

