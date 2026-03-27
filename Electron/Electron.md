## 第一部分：简介

https://www.electronjs.org/zh/

使用HTML、CSS、JavaScript，来构建跨平台的桌面应用程序。 

跨平台：win  linux mac .

哪些流行的工具使用了此技术：  vscode  githubDesktop  qq腾讯

 一款应用广泛的跨平台的桌面应用开发框架。

 Electron 的本质是结合了Chromium与Nodejs.

  Chromium和Chrome的关系，就是浏览器是基于开源的Chromium开发而成。

![](.\img\1.png)



![](.\img\2.png)



### Electron 简介

Electron 是一个**开源跨平台桌面应用开发框架**，由 OpenJS 基金会维护。它将 **Chromium 浏览器内核**与 **Node.js 运行时**深度整合，让开发者能用熟悉的 **HTML、CSS、JavaScript** 技术栈，一次编写、多平台（Windows、macOS、Linux）原生运行。

### 核心特点

- **跨平台**：一套代码可打包成 Windows、macOS、Linux 安装包。
- **Web 技术栈**：前端开发者无需学习新语言，直接复用 Web 开发经验。
- **原生能力**：借助 Node.js 可访问文件系统、系统 API、创建托盘、发送通知、调用硬件等。
- **成熟生态**：大量工具（如 Electron Forge、Electron Builder）与社区支持。

### 用 Electron 能做什么

Electron 几乎能做所有类型的桌面软件，以下是主流场景与知名案例：

#### 1. 代码编辑器 / IDE

- **VS Code**（微软）、**Atom**（GitHub）、**Sublime Text 插件生态**、**WebStorm 同类工具**。

#### 2. 即时通讯 / 协作工具

- **Slack**、**Discord**、**Signal**、**Microsoft Teams 客户端**、**Zoom 桌面版**。

#### 3. 笔记 / 文档 / 知识管理

- **Notion**、**Obsidian**、**语雀桌面端**、**为知笔记**。

#### 4. 设计 / 原型 / 协作工具

- **Figma 桌面端**、**Loom**、**Canva 桌面版**、**Principle**。

#### 5. 开发工具 / API 调试

- **Postman**、**GitHub Desktop**、**MongoDB Compass**、**Docker Desktop**。

#### 6. 媒体 / 音乐 / 网盘

- **网易云音乐桌面版**、**百度网盘**、**Spotify 早期客户端**、**腾讯视频桌面端**。

#### 7. 游戏 / 娱乐 / 直播

- **itch.io 客户端**、**Twitch 桌面版**、轻量级独立游戏客户端。

#### 8. 企业软件 / 管理后台

- 内部 CRM、ERP、数据看板、运维工具、自动化脚本桌面化。

#### 9. AI 助手 / 大模型客户端

- **Claude 桌面版**、**ChatGPT 第三方客户端**、本地 AI 模型管理工具。

------

简单说：只要你能用网页实现界面，Electron 就能把它变成**带系统级能力的桌面软件**，且一次开发、全平台可用。



## 第二部分：语法和构建

####  运行环境

要开发 Electron 应用，您需要安装 [Node.js](https://nodejs.org/en/download/) 运行环境和它的包管理器 npm。 我们推荐安装最新的长期支持 (LTS) 版本。

要检查 Node.js 是否已被安装，您可以在运行 `node` 和 `npm` 命令时，加上 `-v` 参数。 如果已安装，它们应当会输出对应的版本。

```sh
$ node -v
v16.14.2
$ npm -v
8.7.0
```

### 初始化 npm 项目

Electron 应用基于 npm 搭建，以 package.json 文件作为入口点。 首先创建一个文件夹，然后在其中执行 `npm init` 初始化项目。

```
mkdir my-electron-app && cd my-electron-app
npm init
```



你的package.json

```
{
  "name": "electron-demo",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}

```

```
npm install electron --save-dev
```

增加一条script命令

```
{
"script":{
 "start":"electron ."
}
}
```



**主进程  和 渲染进程的通信方法**

![](.\img\3.png)



























