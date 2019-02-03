---
title: webpack
tags:
  - webpack
  - 打包工具
type: categories
categories: webpack
copyright: true
description: webpack的使用方法研究和构建项目实践
date: 2019-01-22 10:25:45
---

##简介
Webpack 是一个前端资源加载/打包工具。它将根据模块的依赖关系进行静态分析，然后将这些模块按照指定的规则生成对应的静态资源。
`Webpack`可以将多种静态资源`js、css、less`转换成一个静态文件，减少了页面的请求。

##原理
储备知识： CommonJS 规范，es6规范，

##安装
最新版本 `npm install --save-dev webpack`
特定版本 `npm install --save-dev webpack@<vesion>`

使用 webpack v4+ 版本，你还需要安装 CLI。
`npm install --save-dev webpack-cli`

>建议局部安装
当你在本地安装 webpack 后，你能够从 node_modules/.bin/webpack 访问它的 bin 版本。

Note：
1.首先查看是否安装有全局webpack, webpack-cli; `webpack -v` `webpack-cli`; 先卸载webpack，`npm uninstall webpack -g` ...
2.`npm init -y` 创建默认的package.json文件
3.局部安装webpack 根目录>`npm i webpack -D`
4.局部安装server 根目录>`npm i webpack-dev-server -D`
5.`npm install --save-dev webpack-cli`
6.检查是否安装好`node_modules/.bin/webpack 访问它的 bin 版本`
7.请cmd管理员身份安装---

[参考教程](https://webpack.docschina.org/guides/getting-started/)

---

webpack 受到版本影响  具体不同的版本使用方法有出入等以后再研究研究

发现安装4.29.0是会出现警告 fsevent模块系统问题
之后安装所有的模块都会出现npm error
错误内容如下：

```
D:\wamp64_3.1.7\www\web-project\node_modules>npm install --save-dev style-loader css-loader
npm ERR! path D:\wamp64_3.1.7\www\web-project\node_modules\fsevents\node_modules
npm ERR! code EPERM
npm ERR! errno -4048
npm ERR! syscall scandir
npm ERR! Error: EPERM: operation not permitted, scandir 'D:\wamp64_3.1.7\www\web-project\node_modules\fsevents\node_modules'
npm ERR!  { Error: EPERM: operation not permitted, scandir 'D:\wamp64_3.1.7\www\web-project\node_modules\fsevents\node_modules'
npm ERR!   stack: 'Error: EPERM: operation not permitted, scandir \'D:\\wamp64_3.1.7\\www\\web-project\\node_modules\\fsevents\\node_modules\'',
npm ERR!   errno: -4048,
npm ERR!   code: 'EPERM',
npm ERR!   syscall: 'scandir',
npm ERR!   path: 'D:\\wamp64_3.1.7\\www\\web-project\\node_modules\\fsevents\\node_modules' }
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\Administrator\AppData\Roaming\npm-cache\_logs\2019-02-02T10_33_26_198Z-debug.log
```

---

[问题1](https://stackoverflow.com/questions/46929196/how-to-solve-npm-install-throwing-fsevents-warning-on-non-mac-os)

[问题2](https://stackoverflow.com/questions/40671567/npm-install-fsevents-errors/42938398#42938398)

参考操作`npm install --no-optional`，感觉也没什作用

具体解决方法，等认真学习webpack4后再看了------


**参考教程**
[入门Webpack，看这篇就够了](https://www.jianshu.com/p/42e11515c10f)