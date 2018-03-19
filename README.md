# vueAdminlte 商用前后端分离项目模板

[![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://github.com/Coding/WebIDE/blob/master/LICENSE) [![Build Status](https://travis-ci.org/Coding/WebIDE.svg?branch=master)](https://travis-ci.org/Coding/WebIDE) [![Docker Stars](https://img.shields.io/docker/stars/webide/webide.svg)](https://hub.docker.com/r/webide/webide 'DockerHub') [![Docker Pulls](https://img.shields.io/docker/pulls/webide/webide.svg)](https://hub.docker.com/r/webide/webide 'DockerHub')

README: [English](https://github.com/Coding/WebIDE/blob/master/README.md) | [中文](https://github.com/Coding/WebIDE/blob/master/README-zh.md)

## 项目logo

![vueAdminlte](https://raw.githubusercontent.com/Coding/WebIDE/gh-pages/screenshots/workspace.png)

## 软件环境

WebIDE Frontend 需要 node v6.x 作为编译运行环境（可以避免很多奇怪的错误），使用 yarn 做包管理工具，做构建工具使用 webpack 和 babel

WebIDE-Frontend-Webjars & WebIDE-Backend 项目依赖 maven3 和 java8

运行该项目需要至少 512MB 的内存空间。在编译、运行项目前，请保证环境依赖已被正确配置。

## 项目简介

Coding WebIDE(https://ide.coding.net) 是 Coding 自主研发的在线集成开发环境 (IDE)。用户可以通过 WebIDE 创建项目的工作空间, 进行在线开发, 调试等操作。同时 WebIDE 集成了 Git 代码版本控制, 用户可以选择 Coding、GitHub、BitBucket、GitLab 等任意的代码仓库。 WebIDE 还提供了分享开发环境的功能, 用户可以保存当前的开发环境, 分享给团队的其他成员。

## 技术栈

vue + adminlte + element + nuxt + j2ee

## 功能特色

全功能 Web Terminal
语法加亮
代码补全
主题切换
分割视图
VIM／Emacs 模式
实时预览

## 模块说明

* WebIDE-Frontend WebIDE 前端项目
* WebIDE-Frontend-Webjars webjar 项目，用于将 WebIDE 前端打包成 webjar
* WebIDE-Backend WebIDE 后端项目

## 如何运行

### 克隆项目

```bash
git clone git@git.coding.net:coding/WebIDE.git
```

### client

* 开发

```bash
gitbook install
gitbook serve
```

* 发布

```bash
gitbook build
```

### server

* 修改默认配置

```bash
backend/src/main/resources/application.properties
```

包括用户、项目、数据库等配置，可以通过修改配置定制服务：

```bash
SPACE_HOME: 存放 workspace 的目录，默认为 ~/.coding-ide/workspace
server.port: 应用启动的端口
USERNAME: 用户名，git 提交时会使用该值作为 user.name，默认为 coding。
EMAIL: 用户邮箱，git 提交时会使用该值作为 user.email，默认为 coding@coding.net
AVATAR: 用户头像
CODING_IDE_HOME: 应用数据存放目录，默认为 ~/.coding-ide
```

### 部署

* 守护进程

```bash
npm install pm2 -g
pm2 start app.js
```

* nginx配置

```javascript
upstream code.kudingyu.com {
  server 172.17.0.83:8002;
}
server {
        listen 80;
        server_name code.kudingyu.com;

        location / {
                proxy_pass http://code.kudingyu.com;
                index index.html index.htm;
        }
        location ^~ /api/ {
                rewrite ^/api/(.*)$ /$1 break;
                proxy_pass http://172.17.0.83:8001;
                proxy_redirect off;
                proxy_set_header  Host  172.17.0.83;
                proxy_set_header  X-Real-IP  $remote_addr;
                proxy_set_header  X-Forwarded-For  $proxy_add_x_forwarded_for;
        }
}
```

## 接口API

* [GitHub API](https://developer.github.com/v3/)

## 引文

- [RESTful Service API 设计最佳工程实践和常见问题解决方案](http://www.jianshu.com/p/cf80d644727e)
- [Best Practices for Designing a Pragmatic RESTful API](http://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
- [Best practices for API versioning?](https://stackoverflow.com/questions/389169/best-practices-for-api-versioning)
- [10 Best Practices for Writing Node.js REST APIs](https://blog.risingstack.com/10-best-practices-for-writing-node-js-rest-apis/)
- [JWT](https://jwt.io/)

## 版权

江苏传智播客教育科技股份有限公司 &nbsp;版权所有Copyright 2006-2018, All Rights Reserved

## 其他

我们推荐使用 Markdown 编写你的 README，请最好注意排版问题以增加文档可读性，推荐阅读 Coding 的 《文案排版规范》。
