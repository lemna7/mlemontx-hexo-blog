## 下载 node

[hexo 文档](https://hexo.io/zh-cn/docs/)
[node 下载](https://nodejs.org/dist/)
在 hexo 文档，开始使用 -> 概述中查看 node 版本进行下载...
我使用的是 `12.13.0`，如果下载的是安装版直接安装即可，否则需要配置环境变量。

## npm 相关

### ERROR

```txt
问题：
npm : 无法将“npm”项识别为 cmdlet、函数、脚本文件或可运行程序的名称。

解决方法：
权限不足，用管理员运行软件。
```

### 更改 npm 源

查看现在的源

```shell
npm get registry
```

更改为淘宝源

```shell
npm config set registry https://registry.npm.taobao.org
```

## 搭建 hexo 环境

### 安装 hexo 脚手架

新建博客目录：我这里是 github 仓库名 `mlemontx.github.io`，进入目录 `cmd` 执行改命令...

```cmd
npm install -g hexo-cli
```

### 安装 hexo

```cmd
npm install hexo
```

## 建站

### ERROR

```text
问题：
hexo : 无法加载文件 D:\Environment\node\node-v12.13.0-win-x64\hexo.ps1，因为在此系统上禁止运行脚本。

解决：
管理员身份运行 power shell
输入：set-ExecutionPolicy RemoteSigned
```

### 初始化

1. 初始化
```cmd
hexo init blog
```

2. 配置

`_config.yml` 文件

### 本地运行

安装服务

```shell
npm install hexo-server --save
```

**ps: 以下命令需要 blog，也就是 hexo init blog 下的目录执行**

生成静态文件

```shell
hexo g
```

本地运行

```shell
hexo s
```

推送到 github

安装部署包

```shell
npm install hexo-deployer-git --save
```

在 `_config.yml` 中配置以下...

```yml
deploy:  
  type: git  
  repo: https://github.com/<username>/<project>  
  # example, https://github.com/hexojs/hexojs.github.io  
  branch: master
```

配置完成后执行以下命令...

```shell
hexo d
```