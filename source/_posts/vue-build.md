---
title: vue如何打包上线
tags: vue
type: categories
categories: vuejs
copyright: true
description: 关于vue开发完后怎样把需要的代码上传到服务器呢
date: 2019-02-03 11:46:46
---


**vue的项目如何上线**
vue的官方都说了，这个框架只是做了view这一层，所以并不是把这些开发完的东西直接拷贝到服务器上，而且需要打包为静态文件上传服务器的。

##过程
**首先需要修改一下配置文件再打包**，很多人都是遇到过打包后运行一片空白等等问题，这些问题主要就是路径的问题，所以需要修改config下面的index.js这个配置文件里选项：

```
assetPublicPath: './'
productionSourceMap: false
```
第一个要修改的就是静态文件的路径，打包后静态文件就在当前目录下，所以修改为./。
第二个是环境设置为生产环境

修改好后打开cmd运行下面的命令打包即可：
`npm run build`

---
看教程，看视频

##参考原文
[vue.js项目打包上线](https://blog.csdn.net/crazywoniu/article/details/74065721)