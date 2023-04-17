---
title: Node.js 初体验
date: 2023/04/16
updated: 2023/04/17
tags:
  - Node
categories:
  - 技术
  - Node
---

## 一、使用背景

我们公司使用的 taf 微服务框架，很多服务都用到了 Node.js，这就需要我们对 Node.js 有足够的了解。

## 二、什么是 Node.js 呢

> [Node.js 入门教程](http://dev.nodejs.cn/learn)

Node.js 是能够在服务器端运行 JavaScript 的开放源代码、跨平台执行环境。Node.js 由 OpenJS Foundation （原为 Node.js Foundation，已与 JS Foundation 合并）持有和维护，亦为 Linux 基金会的项目。Node.js 采用 Google 开发的 V8 执行代码，使用事件驱动、非阻塞和异步输入输出模型等技术来提高性能，可优化应用程序的传输量和规模。这些技术通常用于资料密集的即时应用程序。

Node.js 大部分基本模块都用 JavaScript 语言编写。在 Node.js 出现之前，JavaScript 通常作为客户端程序设计语言使用，以JavaScript 写出的程序常在用户的浏览器上执行。Node.js 的出现使 JavaScript 也能用于服务端编程。Node.js 含有一系列内置模块，使得程序可以脱离 Apache HTTP Server 或 IIS，作为独立服务器执行。

## 三、前置知识


### 3.1 JS

JS 这里不多说，用到即查 MDN。

> [官网：MDN 中文网](https://developer.mozilla.org/zh-CN/)

### 3.2 NPM

#### 3.2.1 NPM 介绍

NPM（全称 Node Package Manager，即 "node包管理器"）是 Node.js 默认的、用 JavaScript 编写的软件包管理系统。

> [文档：Node 中文网](http://dev.nodejs.cn/learn/an-introduction-to-the-npm-package-manager) <br>
  [官网：NPM](https://www.npmjs.com/)

#### 3.2.2 NPM 常用命令

**安装所有依赖**

如果项目具有 package.json 文件，则：

```shell
npm install
```

它会在 node_modules 文件夹（如果尚不存在则会创建）中安装项目所需的所有东西。

**安装单个软件包**

```shell
npm install <package-name>
```

命令标志：
- --save 安装并添加条目到 package.json 文件的 dependencies。
- --save-dev 安装并添加条目到 package.json 文件的 devDependencies。

区别主要是，devDependencies 通常是开发的工具（例如测试的库），而 dependencies 则是与生产环境中的应用程序相关。

当投入生产环境时，如果输入 npm install 且该文件夹包含 package.json 文件时，则会安装它们，因为 npm 会假定这是开发部署。

需要设置 --production 标志（npm install --production），以避免安装这些开发依赖项。

**更新软件包**

```shell
npm update
npm update <package-name>
```

npm 会检查所有软件包是否有满足版本限制的更新版本。

**运行任务**

```shell
npm run <task-name>
```

```json
{
  "scripts": {
    "start-dev": "node lib/server-development",
    "start": "node lib/server-production"
  }
}
```

#### 3.2.3 NPM 将包安装到哪里

**本地安装**

`npm install lodash`

软件包会被安装到当前文件树中的 node_modules 子文件夹下。

在这种情况下，npm 还会在当前文件夹中存在的 package.json 文件的 dependencies 属性中添加 lodash 条目。


**全局安装**

`npm install -g lodash`

在这种情况下，npm 不会将软件包安装到本地文件夹下，而是使用全局的位置。

Windows 安装位置：`C:\Users\YOU\AppData\Roaming\npm\node_modules`

#### 3.2.4 package.json

package.json 文件是项目的清单。 它可以做很多完全互不相关的事情。 例如，它是用于工具的配置中心。 它也是 npm 和 yarn 存储所有已安装软件包的名称和版本的地方。

```json
{
  "name": "test-project",
  "version": "1.0.0",
  "description": "A Vue.js project",
  "main": "src/main.js",
  "private": true,
  "scripts": {
    "dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "test": "npm run unit",
    "lint": "eslint --ext .js,.vue src test/unit",
    "build": "node build/build.js"
  },
  "dependencies": {
    "vue": "^2.5.2"
  },
  "devDependencies": {
    "autoprefixer": "^7.1.2",
    "babel-core": "^6.22.1",
    "babel-eslint": "^8.2.1",
    "babel-helper-vue-jsx-merge-props": "^2.0.3",
    "babel-jest": "^21.0.2",
    "babel-loader": "^7.1.1",
    "babel-plugin-dynamic-import-node": "^1.2.0",
    "babel-plugin-syntax-jsx": "^6.18.0",
    "babel-plugin-transform-es2015-modules-commonjs": "^6.26.0",
    "babel-plugin-transform-runtime": "^6.22.0",
    "babel-plugin-transform-vue-jsx": "^3.5.0",
    "babel-preset-env": "^1.3.2",
    "babel-preset-stage-2": "^6.22.0",
    "chalk": "^2.0.1",
    "copy-webpack-plugin": "^4.0.1",
    "css-loader": "^0.28.0",
    "eslint": "^4.15.0",
    "eslint-config-airbnb-base": "^11.3.0",
    "eslint-friendly-formatter": "^3.0.0",
    "eslint-import-resolver-webpack": "^0.8.3",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-vue": "^4.0.0",
    "extract-text-webpack-plugin": "^3.0.0",
    "file-loader": "^1.1.4",
    "friendly-errors-webpack-plugin": "^1.6.1",
    "html-webpack-plugin": "^2.30.1",
    "jest": "^22.0.4",
    "jest-serializer-vue": "^0.3.0",
    "node-notifier": "^5.1.2",
    "optimize-css-assets-webpack-plugin": "^3.2.0",
    "ora": "^1.2.0",
    "portfinder": "^1.0.13",
    "postcss-import": "^11.0.0",
    "postcss-loader": "^2.0.8",
    "postcss-url": "^7.2.1",
    "rimraf": "^2.6.0",
    "semver": "^5.3.0",
    "shelljs": "^0.7.6",
    "uglifyjs-webpack-plugin": "^1.1.1",
    "url-loader": "^0.5.8",
    "vue-jest": "^1.0.2",
    "vue-loader": "^13.3.0",
    "vue-style-loader": "^3.0.1",
    "vue-template-compiler": "^2.5.2",
    "webpack": "^3.6.0",
    "webpack-bundle-analyzer": "^2.9.0",
    "webpack-dev-server": "^2.9.1",
    "webpack-merge": "^4.1.0"
  },
  "engines": {
    "node": ">= 6.0.0",
    "npm": ">= 3.0.0"
  },
  "browserslist": ["> 1%", "last 2 versions", "not ie <= 8"]
}
```

- version 表明了当前的版本。
- name 设置了应用程序/软件包的名称。
- description 是应用程序/软件包的简短描述。
- main 设置了应用程序的入口点。
- private 如果设置为 true，则可以防止应用程序/软件包被意外地发布到 npm。
- scripts 定义了一组可以运行的 node 脚本。
- dependencies 设置了作为依赖安装的 npm 软件包的列表。
- devDependencies 设置了作为开发依赖安装的 npm 软件包的列表。
- engines 设置了此软件包/应用程序在哪个版本的 Node.js 上运行。
- browserslist 用于告知要支持哪些浏览器（及其版本）。

#### 3.2.5 package-lock.json

该文件旨在跟踪被安装的每个软件包的确切版本，以便产品可以以相同的方式被 100％ 复制（即使软件包的维护者更新了软件包）。

这解决了 package.json 一直尚未解决的特殊问题。 在 package.json 中，可以使用 semver 表示法设置要升级到的版本（补丁版本或次版本），例如：

- 如果写入的是 〜0.13.0，则只更新补丁版本：即 0.13.1 可以，但 0.14.0 不可以。
- 如果写入的是 ^0.13.0，则要更新补丁版本和次版本：即 0.13.1、0.14.0、依此类推。
- 如果写入的是 0.13.0，则始终使用确切的版本。

案例：
  1. 我们投顾服务 TgUserServer 里有个包版本是 `package.json schedule-log:^1.0.3`，我们 `npm i` 的时候升级到了 `package-lock.json 1.0.10`，由于包作者的不严谨，没有向后兼容导致错误。所以要看准确的版本信息要看 `package-lock.json`。

#### 3.2.6 其它命令

**查看 npm 包安装的版本**

list 查看已安装包的最新版本，-g 查看全局安装包：

```shell
npm list
npm list -g
npm view [package_name] version
```

**将所有 Node.js 依赖包更新到最新版本**

发觉软件包的新版本：

```shell
npm outdated
```

这些更新中有些是主版本。 运行 npm update 不会更新那些版本。 主版本永远不会被这种方式更新，因为它们（根据定义）会引入重大更改，npm 希望为你减少麻烦。

若要将所有软件包更新到新的主版本，则全局地安装 npm-check-updates 软件包：

```shell
npm install -g npm-check-updates
ncu -u
npm update
```

**npm 版本控制**

语义版本控制的概念很简单：所有的版本都有 3 个数字：x.y.z。

- 第一个数字是主版本。
- 第二个数字是次版本。
- 第三个数字是补丁版本。

当发布新的版本时，不仅仅是随心所欲地增加数字，还要遵循以下规则：

- 当进行不兼容的 API 更改时，则升级主版本。
- 当以向后兼容的方式添加功能时，则升级次版本。
- 当进行向后兼容的缺陷修复时，则升级补丁版本。

npm 设置了一些规则，可用于在 package.json 文件中选择要将软件包更新到的版本（当运行 npm update 时）。

- ^: 只会执行不更改最左边非零数字的更新。 如果写入的是 ^0.13.0，则当运行 npm update 时，可以更新到 0.13.1、0.13.2 等，但不能更新到 0.14.0 或更高版本。 如果写入的是 ^1.13.0，则当运行 npm update 时，可以更新到 1.13.1、1.14.0 等，但不能更新到 2.0.0 或更高版本。
- ~: 如果写入的是 〜0.13.0，则当运行 npm update 时，会更新到补丁版本：即 0.13.1 可以，但 0.14.0 不可以。
- \>: 接受高于指定版本的任何版本。
- \>=: 接受等于或高于指定版本的任何版本。
- <=: 接受等于或低于指定版本的任何版本。
- <: 接受低于指定版本的任何版本。
- =: 接受确切的版本。
- -: 接受一定范围的版本。例如：2.1.0 - 2.6.2。
- ||: 组合集合。例如 < 2.1 || > 2.6。
- 可以合并其中的一些符号，例如 1.0.0 || >=1.1.0 <1.2.0，即使用 1.0.0 或从 1.1.0 开始但低于 1.2.0 的版本。
- 无符号: 仅接受指定的特定版本（例如 1.2.1）。
- latest: 使用可用的最新版本。

**卸载软件包**

若要卸载之前在本地安装（在 node_modules 文件夹使用 npm install <package-name>）的软件包：

```shell
npm uninstall <package-name>
```

如果使用 -S 或 --save 标志，则此操作还会移除 package.json 文件中的引用；

如果程序包是开发依赖项（列出在 package.json 文件的 devDependencies 中），则必须使用 -D 或 --save-dev 标志从文件中移除：

```shell
npm uninstall -S <package-name>
npm uninstall -D <package-name>
```

如果该软件包是全局安装的，则需要添加 -g 或 --global 标志：

```shell
npm uninstall -g <package-name>
```

## 四、使用 Node.js 做 Web 服务开发

> [lean node 项目地址](https://github.com/mlemontx/mlemontx-demo-node)

### 4.1 下载 Node.js

> [Node.js 下载](https://nodejs.cn/download/)

### 4.2 Node.js 和 浏览器的区别

**相同点：**
1. 浏览器和 Node.js 都使用 JavaScript 作为其编程语言。
2. 浏览器是 JavaScript 在客户端的运行环境，Node是 JavaScript 在服务端的运行环境。

**不同点：**
1. 在 Node 中没有浏览器提供的 document、window 对象，但提供了 global 对象。
2. 在 Node 中 this 指向 global，在浏览器中 this 指向 window。
3. 在 Node 中可以选择某个版本去运行JavaScript，但浏览器不行，无法主动选择浏览器环境。
4. 在 Node 中使用 CommonJS 模块系统，在浏览器遵循的 ES Modules 标准。
5. 在 Node 中使用 require()，在浏览器中使用 import。
6. 目的不同，NodeJS 的作者说，他创造 NodeJS 的目的是为了实现高性能 Web 服务器，但浏览器中的 JavaScript 更多的是为了提供操作的交互。
7. Event Loop的不同。

### 4.3 Node.js 命令

#### 4.3.1 运行

```shell
node app.js
```

#### 4.3.2 停止

```shell
ctrl c
```

### 4.4 Node.js 模块

#### 4.4.1 导入和导出模块

require 导入：

```js
// a.js
// 导出一个对象，对象中的信息就会被暴露
module.exports = {
    name:"onion",
    act(){
        console.log("之前我没得选，现在我想做一个好人")
    },
    age:24
}


// b.js
const info = require("./a.js")
console.log(info.age) // 24
console.log(info.name) // onion
info.act();
// 或者使用解构赋值
const {name} = require("./a.js") // 只接受name的值
console.log(name) // onion
```

exports 导出：

```js
exports.name = "onion";
exports.age = 25;
exports.act = function () { console.log("以前我没得选，现在我想做一个好人"); };
```

#### 4.4.2 核心模块（内置模块）

1. fs 模块是对文件进行操作。
2. path 模块是对文件路径进行处理。
3. http 模块主要用于搭建 HTTP 服务端和客户端，使用 HTTP 服务器或客户端功能必须调用 http 模块。

### 4.5 Express 框架

Node.js 是一个底层平台，在平台之上出来了一系列的框架，这里我用的是 `Express`，不做过多的解释。

> [Express 官方文档](http://expressjs.com/en/starter/installing.html)

跟着文档继续进行学习即可。