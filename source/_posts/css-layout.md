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
* 父元素一定，子元素为多行内联文本：设置父元素的display:table-cell或inline-block，再设置vertical-align:middle;
* 子元素块状元素:设置子元素position:fixed（absolute），然后设置margin:auto; 或者当子元素定宽度时，父级元素使用position:relative;子元素使用position:absolute;margin-left:负一半宽度;left:50%; 
* 通用方案: flex布局，给父元素设置{display:flex; align-items:center;}

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

1. **float+margin**。设置两个侧栏分别向左向右浮动，中间列通过外边距给两个侧栏腾出空间，中间列的宽度根据浏览器窗口自适应。
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

2. **position+margin**。 通过绝对定位将两个侧栏固定，同样通过外边距给两个侧栏腾出空间，中间列自适应。
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



参考博文： https://segmentfault.com/a/1190000008789039  http://www.imooc.com/wenda/detail/254035  https://www.w3cplus.com/css/guide-css-layout.html  https://www.cnblogs.com/autismtune/p/5202065.html  https://www.css88.com/book/css/properties/multi-column/columns.htm