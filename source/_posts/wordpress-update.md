---
title: wordpress升级
tags:
  - wordpress
  - wordpress迁移
  - wordpress升级
type: categories
categories: wordpress
copyright: true
description: 迁移和升级wordpress构建的网站
date: 2019-02-03 11:47:29
---


网站blog需要改版，之前版本使用wordpress3.5搭建。现在趁着改版blog，进行blog升级--wordpress5.0.3版本。开始的一窍不通，只有到处google了，唉...

---
##下载文件到本地服务器（wampsever）
为保证直接升级会带来未知的error，故先将网站迁移到本地。在本地的环境下测试和升级。
下载blog文件下的所有文件；
在数据库中导出所有wordpress相关的数据--导入到本地的数据库中；

##安装和修改数据

在你喜欢的浏览器中访问wp-admin/install.php 以便启动安装程序.
1. 如果你在根目录下安装WordPress,，你应该访问: http://example.com/wp-admin/install.php
2. 如果你将WordPress安装在子目录blog下，你应该访问: http://example.com/blog/wp-admin/install.php

修改 `wp-config.php`

修改数据库中 `wp-option`

##升级worpress
登录内容管理，升级wordpress。
步骤参照官方文档即可。


##参考文章
[如何完美更换WordPress网站的域名](https://jingyan.baidu.com/article/375c8e19c0fb5925f3a2296c.html)

[升级 WordPress](https://codex.wordpress.org/zh-cn:%E5%8D%87%E7%BA%A7_WordPress)

[升级 WordPress 进阶](https://codex.wordpress.org/zh-cn:%E5%8D%87%E7%BA%A7_WordPress_%E8%BF%9B%E9%98%B6)

[安装](https://codex.wordpress.org/zh-cn:%E5%AE%89%E8%A3%85WordPress)
