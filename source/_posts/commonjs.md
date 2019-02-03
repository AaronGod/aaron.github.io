---
title: commonjs
tags:
  - commonjs
  - commonjs规范
  - 前端打吧写法
type: categories
categories: commonjs
copyright: true
description: 关于打包前的写法说明
date: 2019-02-03 11:46:09
---

#CommonJS规范
[教程参考](http://javascript.ruanyifeng.com/nodejs/module.html)

CommonJS规范的提出，主要是为了弥补JavaScript没有标准的缺陷
浏览器不兼容CommonJS的根本原因，在于缺少四个Node.js环境的变量
>module
>exports
>require
>global


CommonJS模块规范主要分为三部分：**模块引用、模块定义、模块标识**。

##模块引用
**使用require(模块名称)方法**
**带路径和不带路径**
require的参数仅仅是模块名字的字符串，没有带有路径，引用的是所在当前目录下的node_modules目录下相应的模块。如果当前目录没有node_modules目录或者node_modules目录里面没有安装对应的模块，便会报错
如果要引入的模块在其他路径，就需要使用到相对路径或者绝对路径

##模块定义
module对象：在每一个模块中，module对象代表该模块自身。
export属性：module对象的一个属性，它向外提供接口。

函数要能被其他模块使用，就需要暴露一个对外的接口，export属性用于完成这一工作。
XX.XXX(ag1,ag2...);
本文件的变量（require('暴露的模块名称')）.引用模块中的方法（）。

##模块标识
模块标识指的是传递给require方法的参数，必须是符合小驼峰命名的字符串，或者以 . ，.. ，开头的相对路径，或者绝对路径

##CommonJS模块规范的好处
CommonJS模块规范很好地解决变量污染问题，每个模块具有独立空间，互不干扰，命名空间等方案与之相比相形见绌。
CommonJS规范定义模块十分简单，接口十分简洁。
CommonJS模块规范支持引入和导出功能，这样可以顺畅地连接各个模块，实现彼此间的依赖关系。


参考教程：

[CommonJS规范](http://javascript.ruanyifeng.com/nodejs/module.html)

[简要理解CommonJS规范](https://blog.csdn.net/u012443286/article/details/78825917)

[浏览器加载 CommonJS 模块的原理与实现](http://www.ruanyifeng.com/blog/2015/05/commonjs-in-browser.html)

浏览器中不支持 commonjs的写法，故需要进行转化。
可以了解一下这篇文章。[如果不了解 npm 和 ES6 模块，那就看过来](http://web.jobbole.com/87536/) 

commonjs，AMD，CMD规范 简单解析[浅析JS模块规范：AMD，CMD，CommonJS](https://www.jianshu.com/p/09ffac7a3b2c)

