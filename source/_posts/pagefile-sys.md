---
title: pagefile.sys
tags: windows system
categories: 系统
description: 为了腾出更多空间给C盘，把虚拟内存从C盘移到到D盘，很多人不会弄，下面我叫大家如何弄。虚拟内存的移动和替换。也就是pagefile.sys的删除替换
date: 2019-01-03 17:05:47
---

# 如何把虚拟内存从C盘移到D盘(pagefile.sys移动)
---
<!-- more -->
## Step 1 显示虚拟内存文件pagefile.sys

1. 大家打开C盘，是看不到这个文件的。因为是系统保护和隐藏文件。双重保护起来了。
![c盘](https://imgsa.baidu.com/exp/pic/item/bd7faf3533fa828b99f0e655f81f4134960a5a71.jpg '系统盘')

2. 修改文件选项和搜索选项
![修改文件选项和搜索选项](https://imgsa.baidu.com/exp/w=480/sign=e005cf4d3cdbb6fd255be42e3925aba6/1f178a82b9014a9047dc3d0bac773912b21beea2.jpg '')

3. 查看里面，把 系统保护隐藏文件  和   显示隐藏文件 都如图弄好了。
![](https://imgsa.baidu.com/exp/w=480/sign=5dfb31b86209c93d07f20fffaf3cf8bb/7a899e510fb30f24d64b97b5cd95d143ac4b03b6.jpg)

4. 确定
![](https://imgsa.baidu.com/exp/w=480/sign=0283934254da81cb4ee682c56267d0a4/8326cffc1e178a8216ec0416f303738da877e8b0.jpg)

5. 显示隐藏文件
![](https://imgsa.baidu.com/exp/w=480/sign=0fcf9aac2d34349b74066f8df9eb1521/8c1001e93901213f92ec356a51e736d12e2e95ac.jpg)

6. 这时候显示出来了
![](https://imgsa.baidu.com/exp/w=480/sign=e5dad5d64ac2d562f208d1e5d71090f3/18d8bc3eb13533fade69e898add3fd1f40345bac.jpg)

7. 大小正好和物理内存条大小一样的。
![](https://imgsa.baidu.com/exp/w=480/sign=67e9a542b24543a9f51bfbc42e168a7b/0bd162d9f2d3572cc52fe76a8f13632763d0c3b3.jpg)


## Step 2 D盘创建虚拟内存文件

1. 我的电脑   右键属性  然后  高级系统设置
2. 点击“高级”，然后：设置
3. 再次“高级”，更改
4. 按照图片的顺序一步步弄好
![](https://imgsa.baidu.com/exp/w=480/sign=cda83676f236afc30e0c3e6d8318eb85/4d086e061d950a7bccef35720fd162d9f3d3c9aa.jpg)
5. 这时候D盘就成功创建了虚拟内存了。
6. 大小也可以看到。

## Step 3 修改（删除）C盘虚拟内存

1. 安装图片位置，一步步来1234
![](https://imgsa.baidu.com/exp/w=480/sign=8552d7a4770e0cf3a0f74ff33a46f23d/b17eca8065380cd78423d85ba444ad3459828142.jpg)
2. 重启电脑，然后开机后，发现C盘的虚拟内存文件pagefile.sys文件不见了，C盘变大了。也就是说成功了。虚拟内存现在变成在了D盘了。推荐设置物理内存大小1.45倍的大小在D盘就行。
