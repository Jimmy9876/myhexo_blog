---
title: 用vue.js开发一个TodoList(1)
copyright: true
date: 2017-05-27 12:26:09
tags: vue.js
---

> 这几天，开始静下心来学习下vue.js，准备用vue.js开发一个TodoList，在学习的过程中把学习进度实时记录下来

## 介绍

Vue.js（读音 /vjuː/，类似于 **view**） 是一套构建用户界面的**渐进式框架**。与其他重量级框架不同的是，Vue 采用自底向上增量开发的设计。Vue 的核心库只关注视图层，它不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[单文件组件](https://cn.vuejs.org/v2/guide/single-file-components.html)和 [Vue 生态系统支持的库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用程序提供驱动。

## 安装

### 兼容性

Vue.js 不支持 IE8 及其以下版本，因为 Vue.js 使用了 IE8 不能模拟的 ECMAScript 5 特性。 Vue.js 支持所有[兼容 ECMAScript 5 的浏览器](http://caniuse.com/#feat=es5)。

Vue.js 提供一个[官方命令行工具](https://github.com/vuejs/vue-cli)，可用于快速搭建大型单页应用。该工具提供开箱即用的构建工具配置，带来现代化的前端开发流程。只需几分钟即可创建并启动一个带热重载、保存时静态检查以及可用于生产环境的构建配置的项目，运行如下命令安装:

```Shell
# 全局安装 vue-cli
$ npm install --global vue-cli
# 创建一个基于 webpack 模板的新项目
$ vue init webpack 你的项目名
# 安装依赖，走你
$ cd 你的项目名
$ npm install
```

在这里，如果显示`npm`命令`command not found`请安装一下[node.js](https://nodejs.org/en/download/)

如果觉得运行`npm install`慢，请打开终端运行如下界面，让`npm`走淘宝镜像。

```Shell
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

之后凡遇到`npm`命令的时候换成`cnpm`代替，就会快很多。

👉[✨镜像网址✨](http://npm.taobao.org)👈

安装成功运行

```Shell
npm run dev
```

浏览器出现如下页面

![Markdown](http://i4.buimg.com/1949/88ed3c8b8f0ccffd.png)

至此就安装成功了，接下来可以一步一步开发一个TodoList项目了。项目实时更新于[我的GitHub](https://github.com/Jimmy9876/TodoList)

