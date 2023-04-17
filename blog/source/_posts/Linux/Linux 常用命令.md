---
title: Linux 常用命令
date: 2023/03/01
tags:
  - Linux
categories:
  - 技术
  - Linux
top_img: https://s2.loli.net/2023/03/04/dCMLXSRH4F87qhV.webp
cover: https://s2.loli.net/2023/03/04/dCMLXSRH4F87qhV.webp
---

## 清空文件

### rm 命令

会直接删除文件，需谨慎

```shell
rm -rf file_name
```

### echo 命令

使用 `echo` 命令时，文件中会有一个空行

```shell
echo "" > file_name
```

### cat 命令（推荐）

会直接清空文件

```shell
cat /dev/null > file_name
```
