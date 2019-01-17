---
title: css布局合集
type: categories
copyright: true
date: 2019-01-16 10:38:25
tags: [css,flex伸缩盒子,grid网格布局,Multi-column多列布局]
categories: css布局
description: 在使用swiper中看到使用的flex布局，突然想全面整理了解css的动态和最新流行的技术。这里将自己工作中使用到的css布局方法整理归纳出来，不想每次去百度啦！
---
## 写在前列

布局是CSS中一个重要部分，本文总结了CSS布局中的常用技巧，包括常用的水平居中、垂直居中方法，以及单列布局、多列布局的多种实现方式（包括传统的盒模型布局和比较新的flex布局实现），希望能给需要的小伙伴带来一些帮助。

### 目录
1. 传统布局
> 圣杯布局
2. 多列布局
3. flex布局
4. grid布局
### 传统布局

#### 居中布局
居中在布局中很常见，假设DOM文档结构如下，子元素要在父元素中居中：

```
<div class="parent">
    <div class="child"></div>
</div>
```
1. 水平居中

* 子元素为行内元素：对父元素设置`text-align:center`;
* 子元素为定宽块状元素: 设置左右`margin值为auto`;
* 子元素为不定宽块状元素: 设置子元素为`display:inline`,然后在父元素上设置`text-align:center`;
* 通用方案: flex布局，对父元素设置`display:flex;justify-content:center`;

2. 垂直居中

* 父元素一定，子元素为单行内联文本：设置父元素的height等于行高line-height；
* 父元素一定，子元素为多行内联文本：设置父元素的display:table-cell或inline-block，再设置vertical-align:middle;（这里有错误）；
* 子元素块级垂直居中： 代码如下，

引用博文：[利用vertical-align:middle垂直居中](https://www.jianshu.com/p/dea069fecb62);
```
<div class="parent5 box">
    <!-- 不能水平居中 -->
    <div class="child5">
        多行内联文本垂直居中写法
    </div>
    <div class="help"></div><!--可以试试伪类-->
</div>

.parent5 {
    width:100px;
    height:100px;
}
.child5 {
    display: inline-block;
    vertical-align: middle;
    width: 80px;
    overflow:hidden;
}

.parent5 .help {
    width: 0;
    height: 100%;
    display: inline-block;
    vertical-align: middle;
}

```

* 子元素块状元素:设置子元素position:fixed（absolute），然后设置margin:auto(无效); 或者当子元素定宽度时，父级元素使用position:relative;子元素使用position:absolute;margin-top:负一半宽度;top:50%; 
* 通用方案: flex布局，给父元素设置{display:flex; align-items:center;}


**演示代码**

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>居中布局</title>
    <style>
        .box {
            width: 100px;
            height: 100px;

            border: 1px solid red;
        }

        .header,
        .footer {
            width: 100%;
            height: 80px;
            background-color: bisque;
        }

        .layout {
            max-width: 1200px;
            margin: auto;
        }

        .layout {
            display: flex;
            justify-content: space-around;
        }

        .parent1 {
            text-align: center;
        }

        /* .parent2 {
            margin: auto;
        } */
        .child2 {
            width: 50px;
            margin: auto;
        }

        .parent3 {
            text-align: center;
        }

        .child3 {
            display: inline;

        }

        .parent4 {
            display: flex;
            justify-content: center;
        }

        .child5 {
            display: inline-block;
            vertical-align: middle;
            width: 80px;
        }

        .parent5 {
            text-align: center;
        }

        .parent5::after {
            width: 0;
            height: 100%;
            display: inline-block;
            vertical-align: middle;
            content: '';
            margin-right: -5px;
            /* 水平居中有5个像素的误差 */
        }

        /* .parent5 .help {
            width: 0;
            height: 100%;
            display: inline-block;
            vertical-align: middle;
        } */

        .parent6 {
            display: flex;
            align-items: center;
        }
    </style>
</head>

<body>
    <div class="header">
        <div class="layout">
            头部内容
        </div>
    </div>
    <div class="content">
        <div class="layout">
            <div class="parent1 box">
                <!-- <div class="child"></div> -->
                <span class="child1">行内元素demo1</span>
            </div>
            <div class="parent2 box">
                <div class="child2">
                    我是块级元素定宽
                </div>
            </div>
            <div class="parent3 box">
                <div class="child3">
                    我是块级元素不定宽
                </div>
            </div>
            <div class="parent4 box">
                <div class="child4">
                    flex
                </div>
            </div>

            <div class="parent5 box">
                <!-- 不能水平居中 -->
                <div class="child5">
                    多行内联文本垂直居中写法
                </div>
                <!-- <div class="help"></div> -->
            </div>

            <div class="parent6 box">
                <div class="child6">
                    多行垂直居中写法
                </div>
            </div>
        </div>
    </div>
    <div class="footer">
        <div class="layout">
            底部内容
        </div>
    </div>

</body>

</html>
```

**效果图**
![效果图](http://plf3trb76.bkt.clouddn.com/layout_demo1.png)

#### 单列布局
单列布局有两种方式：一种是header、content、footer宽度都相同，其一般不会占满浏览器的最宽宽度，但当浏览器宽度缩小低于其最大宽度时，宽度会自适应；一种是header、footer宽度为浏览器宽度，但content以及header和footer里的内容却不会占满浏览器宽度。

* 对于第一种，对header、content、footer统一设置width或max-width，并通过margin:auto实现居中。

代码部分
```
<!-- html部分 -->
<div class="layout">
  <div id="header">头部</div>
  <div id="content">内容</div>
  <div id="footer">尾部</div>
</div>
<!-- css部分 -->
.layout{
  /*   width: 960px; *//*设置width当浏览器窗口宽度小于960px时，单列布局不会自适应。*/
    max-width: 960px;
    margin: 0 auto;
}
```

* 对于第二种，header、footer的内容宽度为100%，但header、footer的内容区以及content统一设置max-width，并通过margin:auto实现居中。

代码部分
```
<!-- html 代码部分 -->
<div id="header">
    <div class="layout">头部</div>
</div>
<div id="content" class="layout">内容</div>
<div id="footer">
    <div class="layout">尾部</div>
</div>
<!-- css 部分 -->
#header,#footer {
    width:100%;
}
.layout {
    max-width: 1200px;
    margin: auto;
}
```
#### 二列&三列布局

![多列布局示意图](http://plf3trb76.bkt.clouddn.com/muti-cols.png)

* 二列布局的特征是侧栏固定宽度，主栏自适应宽度。
* 三列布局的特征是两侧两列固定宽度，中间列自适应宽度。

对于传统的实现方法，主要讨论上图中前三种布局，经典的带有侧栏的二栏布局以及带有左右侧栏的三栏布局，对于flex布局，实现了上图的五种布局。

##### float+margin

设置两个侧栏分别向左向右浮动，中间列通过外边距给两个侧栏腾出空间，中间列的宽度根据浏览器窗口自适应。

```
<div id="content">
    <div class="sub">sub</div>
    <div class="extra">extra</div>
    <div class="main">main</div>
</div>
<!-- 对两边侧栏分别设置宽度，并对左侧栏添加左浮动，对右侧栏添加有浮动。
对主面板设置左右外边距，margin-left的值为左侧栏的宽度，margin-right的值为右侧栏的宽度。 -->
.sub{
    width: 100px;
    float: left;
}
.extra{
    width: 200px;
    float: right;
}
.main{
    margin-left: 100px; 
    margin-right: 200px;
}
```

> `note:`
1.注意DOM文档的书写顺序，先写两侧栏，再写主面板，更换后则侧栏会被挤到下一列（圣杯布局和双飞翼布局都会用到）
2.这种布局方式比较简单明了，但缺点是渲染时先渲染了侧边栏，而不是比较重要的主面板。

* 二列的实现方法:如果是左边带有侧栏的二栏布局，则去掉右侧栏，不要设置主面板的margin-right值，其他操作相同。反之亦然。

##### position+margin

 通过绝对定位将两个侧栏固定，同样通过外边距给两个侧栏腾出空间，中间列自适应。

```
<!-- 1.对两边侧栏分别设置宽度，设置定位方式为绝对定位。
2. 设置两侧栏的top值都为0，设置左侧栏的left值为0， 右侧栏的right值为0。
3. 对主面板设置左右外边距，margin-left的值为左侧栏的宽度，margin-right的值为右侧栏的宽度。 -->
<div class="sub">left</div>
<div class="main">main</div>
<div class="extra">right</div>
.sub, .extra {
    position: absolute;
    top: 0; 
    width: 200px;
}
.sub { 
    left: 0;
}
.extra { 
    right: 0; 
}
.main { 
    margin: 0 200px;
}
```

>`note:`
1.与上一种方法相比，本种方法是通过定位来实现侧栏的位置固定。
2.如果中间栏含有最小宽度限制，或是含有宽度的内部元素，则浏览器窗口小到一定程度，主面板与侧栏会发生重叠。
3.如果是左边带有侧栏的二栏布局，则去掉右侧栏，不要设置主面板的margin-right值，其他操作相同。反之亦然。

##### 圣杯布局(float + 负margin + padding + position)

原理说明：
主面板设置宽度为100%，主面板与两个侧栏都设置浮动，常见为左浮动，这时两个侧栏会被主面板挤下去。通过负边距将浮动的侧栏拉上来，左侧栏的负边距为100%，刚好是窗口的宽度，因此会从主面板下面的左边跑到与主面板对齐的左边，右侧栏此时浮动在主面板下面的左边，设置负边距为负的自身宽度刚好浮动到主面板对齐的右边。为了避免侧栏遮挡主面板内容，在外层设置左右padding值为左右侧栏的宽度，给侧栏腾出空间，此时主面板的宽度减小。由于侧栏的负margin都是相对主面板的，两个侧栏并不会像我们理想中的停靠在左右两边，而是跟着缩小的主面板一起向中间靠拢。此时使用相对布局，调整两个侧栏到相应的位置。

```
<div id="bd">         
    <div class="main"></div>        
    <div class="sub"></div>        
    <div class="extra"></div>  
</div> 

    布局步骤:

    三者都设置向左浮动。

    设置main宽度为100%，设置两侧栏的宽度。

    设置 负边距，sub设置负左边距为100%，extra设置负左边距为负的自身宽度。

    设置main的padding值给左右两个子面板留出空间。

    设置两个子面板为相对定位，sub的left值为负的sub宽度，extra的right值为负的extra宽度。

.main {        
    float: left;       
    width: 100%;   
 }  
 .sub {       
    float: left;        
    width: 190px;        
    margin-left: -100%;               
    position: relative;  
    left: -190px;  
}   
.extra {        
    float: left;        
    width: 230px;        
    margin-left: -230px; 
    position: relative; 
    right: -230px;  
 }
#bd {        
    padding: 0 230px 0 190px;   
 }


```

> NOTE: 
1.DOM元素的书写顺序不得更改。
2.当面板的main内容部分比两边的子面板宽度小的时候，布局就会乱掉。可以通过设置main的min-width属性或使用双飞翼布局避免问题。
3.二列的实现方法.如果是左边带有侧栏的二栏布局，则去掉右侧栏，不要设置主面板的padding-right值，其他操作相同。反之亦然。

##### 双飞翼布局(float + 负margin + margin)

>原理说明：
双飞翼布局和圣杯布局的思想有些相似，都利用了浮动和负边距，但双飞翼布局在圣杯布局上做了改进，在main元素上加了一层div, 并设置margin,由于两侧栏的负边距都是相对于main-wrap而言，main的margin值变化便不会影响两个侧栏，因此省掉了对两侧栏设置相对布局的步骤。

```
<div id="main-wrap" class="column">
      <div id="main">#main</div>
</div>
<div class="sub"></div>        
<div class="extra"></div>


布局步骤:
1. 三者都设置向左浮动。
2. 设置main-wrap宽度为100%，设置两个侧栏的宽度。
3. 设置负边距，sub设置负左边距为100%，extra设置负左边距为负的自身宽度。
4. 设置main的margin值给左右两个子面板留出空间。

.main-wrap {        
    float: left;       
    width: 100%;   
 }  
 .sub {       
    float: left;        
    width: 190px;        
    margin-left: -100%;   
}   
.extra {        
    float: left;        
    width: 230px;        
    margin-left: -230px; 
 }
.main {    
    margin: 0 230px 0 190px;
}
```

> NOTE
1.圣杯采用的是padding，而双飞翼采用的margin，解决了圣杯布局main的最小宽度不能小于左侧栏的缺点。
2.双飞翼布局不用设置相对布局，以及对应的left和right值。
3.通过引入相对布局，可以实现三栏布局的各种组合，例如对右侧栏设置position: relative; left: 190px; ,可以实现sub+extra+main的布局。
4.二列实现方法。如果是左边带有侧栏的二栏布局，则去掉右侧栏，不要设置main-wrap的margin-right值，其他操作相同。反之亦然。

**demo code**

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>多列布局</title>
    <style>
        .layout {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header,
        .footer {
            height: 50px;
            background-color: aquamarine;
        }

        .test1>.sub {
            float: left;
        }

        .test1>.extra {
            float: right;
        }

        .sub {
            width: 100px;
        }

        .extra {
            width: 100px;
        }

        .main {
            margin-left: 100px;
            margin-right: 100px;
        }

        .test2 {
            position: relative;
        }

        .test2>.sub {
            position: absolute;
            left: 0;
            top: 0;
        }

        .test2>.extra {
            position: absolute;
            top: 0;
            right: 0;
        }

        .test3 {
            padding: 0 100px;
            overflow: hidden;
        }

        .test3>.main {
            width: 100%;
            min-width: 100px;
            /*设置一个最小宽度*/
            margin: 0;
            /*消除之前设置的margin值*/
        }

        .test3>.main,
        .test3>.sub,
        .test3>.extra {
            float: left;
        }

        .test3>.sub {
            margin-left: -100%;
            position: relative;
            left: -100px;
            /*自身宽度*/
        }

        .test3>.extra {
            margin-left: -100px;
            position: relative;
            right: -100px;
            /*自身宽度*/
        }

        .test4 {
            overflow: hidden;
            /*清除浮动*/
        }

        .test4>.main-wrap {
            float: left;
            width: 100%;
        }

        .test4>.sub {
            float: left;
            margin-left: -100%;
        }

        .test4>.extra {
            float: left;
            margin-left: -100px;
        }

        .test4>.main {
            margin: 0;
        }
    </style>
</head>

<body>
    <div class="layout">
        <div class="header">头部</div>
        <div class="content">
            内容
            <div class="test" style="margin-top:20px;">
                <div class="test1">
                    <div class="sub">左边</div>
                    <div class="extra">右边</div>
                    <div class="main">中间</div>
                </div>
                <hr>

                <div class="test2">
                    <div class="sub">左边</div>
                    <div class="main">中间</div>
                    <div class="extra">右边</div>
                </div>

                <hr>
                <br>
                <p>圣杯布局</p>
                <div class="test3">
                    <div class="main">中间</div>
                    <div class="sub">左边</div>
                    <div class="extra">右边</div>
                </div>
                <hr>
                <br>
                <p>双飞翼布局</p>
                <div class="test4">
                    <div class="main-wrap">
                        <div class="main">中间</div>
                    </div>
                    <div class="sub">左边</div>
                    <div class="extra">右边</div>
                </div>
            </div>
        </div>
        <hr>
        <br>
        <div class="footer">底部</div>
    </div>
</body>
</html>
```

**效果图**
![demo2 效果图](http://plf3trb76.bkt.clouddn.com/layout_demo2.png)

### flex布局

[阮一峰的博客——flex语法](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
[阮一峰的博客——flex布局案例](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

### grid布局

简介
> CSS Grid 布局是 CSS 中最强大的布局系统。与 flexbox 的一维布局系统不同，CSS Grid 布局是一个二维布局系统，也就意味着它可以同时处理列和行。通过将 CSS 规则应用于 父元素 (成为 Grid Container 网格容器)和其 子元素（成为 Grid Items 网格项），你就可以轻松使用 Grid(网格) 布局。


[玩转grid布局](https://www.imooc.com/article/43143)

[CSS Grid 布局完全指南(图解 Grid 详细教程)](https://www.css88.com/archives/8510)

### Multi-column多列布局

[多列布局(multi-column)](https://blog.csdn.net/weixin_42663701/article/details/81485936)

[CSS3多列布局（Multi-column）](https://blog.csdn.net/weixin_39141044/article/details/82432866)
#### 总结
传统的布局方法基于盒状模型，依赖 display属性 + position属性 + float属性，逻辑相对复杂，对于实现一些特殊效果，例如垂直居中，尤其复杂繁琐。而flex布局中的flex容器可以根据实际可用空间动态调整子元素的宽高比和顺序，使元素能够尽可能地利用可用空间，同时也能通过缩小来避免超出。flex布局提供了一套简便、完整、响应式的布局方案。

参考博文： https://segmentfault.com/a/1190000008789039  http://www.imooc.com/wenda/detail/254035  https://www.w3cplus.com/css/guide-css-layout.html  https://www.cnblogs.com/autismtune/p/5202065.html  https://www.css88.com/book/css/properties/multi-column/columns.htm