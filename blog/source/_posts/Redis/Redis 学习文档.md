---
title: Redis 学习文档.md
tags:
- Redis
categories:
- Redis
top_img: https://s2.loli.net/2023/03/05/fiI8uWCs2kSJXHM.webp
cover: https://s2.loli.net/2023/03/05/fiI8uWCs2kSJXHM.webp
---

## redis-cli

### 连接到远程

```shell
redis-cli -h remoteAddr -p port
```

### 查看当前主节点

```shell
sentinel get-master-addr-by-name masterName
```

