---
title: Git 文档
tags: 
    - Git
categories: 
    - Git
top_img: https://s2.loli.net/2023/03/04/QOXpB1aPdmvrsDc.webp
cover: https://s2.loli.net/2023/03/04/QOXpB1aPdmvrsDc.webp
---

## 配置 Git

### 设置用户名和邮箱

```shell
git config --global user.name "mlemontx"
git config --global user.email "mlemontx@example.com"
```

### 查看配置信息

```shell
git config -l
git config --list
```

### 移除凭证

```shell
git config --global --unset credential.helper
```

出现以下错误可以尝试使用该命令（拉取代码时输入用户名和 token）：

```shell
remote: repositorysitory not found.
```

## 获取远程仓库

### 克隆远程仓库

```shell
git clone https://github.com/username/repository.git
```

## 管理远程仓库

### 添加远程仓库

`git remote add` 命令采用两个参数：

-   远程名称（例如 `origin`）
-   远程 URL（例如 `https://github.com/username/repository.git`）

```shell
git remote add origin https://github.com/username/repository.git
```

### 查看当前的远程库

```shell
git remote -v
```

### 更改远程仓库的 URL

```shell
git remote set-url origin https://github.com/username/new_repository.git
```

### 重命名远程仓库

`git remote rename` 命令采用两个参数：

-   现有远程名称（例如 `origin`）
-   远程的新名称（例如 `destination`）

```shell
git remote rename origin destination
```

### 删除远程仓库

```shell
git remote remove origin
git remove rm origin
```

## 管理分支

### 查看分支

#### 查看本地已经存在的分支（当前分支会用`*`标记）
```shell
git branch
```

#### 查看本地和远程的所有分支（`remotes/` 开头表示远程分支）：

```shell
git branch -a
```

### 本地分支关联远程分支

```shell
git branch --set-upstream-to=origin/remote_branch your_branch
```

## ERROR

```txt
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
```

原先的密码凭证从2021年8月13日开始就不能用了，必须使用个人访问令牌（personal access token），就是把密码替换成 token！

每次管理远程分支都要输入用户名和 token，怎么办？
更改远程仓库的 URL 为 `https://<token>@github.com/username/repository.git`

```shell
git remote set-url origin https://<token>@github.com/username/repository.git
```