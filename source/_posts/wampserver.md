---
title: wampserver
type: categories
copyright: false
date: 2019-01-18 12:21:28
tags: [wampserver配置方法, wampserver]
categories: wampserver
description: 很久之前在公司的电脑上安装了wampserver，但不管怎么配置Apache中的httpd.conf文件始终都无法用其他设备访问到该服务器。。今天突然想重新研究一下，突然设置成功了。仅仅写帖子来记录一下这一时刻，为之后的安装找到正确的方法。
---

**简介**

对于一个码农来说，搭建环境是必须会用到的！但搭建环境也不是件容易的事情，特别是对于新手同学来说！因此在这里跟大家介绍我作为一名新手在使用的方便好用的PHP服务器架设软件，那就是wampserver，这款软件在安装的过程中就已经把Apache、MySQL、PHP继承好了，而且也做好了相应的配置，除此之外，还加上了SQLitemanager和Phpmyadmin，省去了很多复杂的配置过程，让我们能把更多的时间放在程序开发上。更值得高兴地是这款软件也是完全免费的。重要提示：基本上每一步更改配置文件的操作结束之后，均在重启了相应服务之后才会生效，也就是说如果想要修改立即生效的话，必须在修改完毕保存之后重新启动一下相应的服务！

### 下载

版本 wampserver3.1.7
>
    Server Configuration
    Apache Version:
    2.4.37  - Documentation
    Server Software:
    Apache/2.4.37 (Win64) PHP/7.2.14 - Port defined for Apache: 80
    PHP Version:
    7.2.14  - Documentation


[下载地址](https://sourceforge.net/projects/wampserver/)  安装方法就不介绍了，可以参考[wampserver安装](https://www.cnblogs.com/believerp/p/6885686.html)

### 配置

安装好了之后，首先配置允许被其他局域网设备可访问。具体配置如下：

1. 配置Apache，httpd.conf文件

![图片1](http://plf3trb76.bkt.clouddn.com/image/wampserver/httpdconf6.png)

![图片2](http://plf3trb76.bkt.clouddn.com/image/wampserver/httpdconf4.png)

![图片3](http://plf3trb76.bkt.clouddn.com/image/wampserver/httpdconf3.png)

![图片4](http://plf3trb76.bkt.clouddn.com/image/wampserver/httpdconf2.png)

![图片5](http://plf3trb76.bkt.clouddn.com/image/wampserver/httpdconf1.png)

2. 修改httpd-vhosts.conf文件

![vhosts](http://plf3trb76.bkt.clouddn.com/image/wampserver/vhost_confg.png)

3. 检查路径

查看localhost进去后文件的路径是否正确，如果不正确需要修改文件路径。进入文件目录的index.php文件，
按照图中进行修改。

![indexphp](http://plf3trb76.bkt.clouddn.com/image/wampserver/indexphp.png)

4. 修改完成后检查其他设备是否能在局域网内访问。

访问地址为ipv4地址 如：192.168.15.168；检查是否处在同一局域网查看ip的前三段是否一致。
如果访问什么都不显示，可能的原因是设置防火墙的关系。需要关闭防火墙。
![防火墙](http://plf3trb76.bkt.clouddn.com/image/wampserver/firewall.png)

修改后再访问如果出现以下信息
> "403 Forbidden: You don't have permission to access / on this server".

请重复 1、2步骤 再试；

5. 关于配置文件默认目录

在httpd.conf中修改Documentroot；Directory； 同时在wampmanager.ini和wampmanager.tpl修改默认配置。

[修改参考](https://jingyan.baidu.com/article/22fe7ced1ca16b3003617f7c.html)


### 总结

本文完。