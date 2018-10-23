---
title: 入门-CSS-II
date: 2018-03-27 18:00:56
tags: CSS
categories: CSS
---
## 1.伪类
### I.从`::before`和`::after`讲起
```
div::before{
  content:‘&’
}
div::after{
  content:'$'
}
```
这样div的内容的前后就会被加上`&`和`$`。
而且他还能加各种属性。
### II.还记得那只太极吗？
CSS:
```
body{
  background-color: #444;
}
.balance{
  width:200px;
  height:200px;
  border-radius: 50%;
  background: linear-gradient(to bottom, #ffffff 0%,#ffffff 50%,#000000 51%,#000000 100%); 
  position: relative;
  margin:100px auto;
}
.dark{
  width: 100px;
  height: 100px;
  border-radius:50%;
  background: black;
  position: absolute;
  top: 25%;
  left:0;
}
.light{
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: white;
  position: absolute;
  top: 25%;
  left:50%;
}
.dark .l1{
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: white;
  position:absolute;
  top: 40px;
  left: 40px;
}
.light .dr{
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: black;
  position: absolute;
  left: 40px;
  top: 40px;
}
```
HTML:
```
<div class="balance">
  <div class="light">
      <div class="dr"></div>
  </div>
  <div class="dark">
      <div class="l1"></div>
  </div>
</div>
```
很长对不对？
CSS:
```
body{
  background-color: #444;
}
.balance{
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: linear-gradient(to bottom, #ffffff 0%,#ffffff 50%,#000000 51%,#000000 100%); 
  position: relative;
  margin:100px auto;
}
.balance::before{
  content: '';
  width: 20px;
  height: 20px;
  border-radius:50%;
  border: 40px solid black;
  background: white;
  position: absolute;
  top: 25%;
  left:0;
}
.balance::after{
  content: '';
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: black;
  position: absolute;
  border: 40px solid white;
  top: 25%;
  left:50%;
}
```
HTML:
`<div class="balance"></div>`
是不是短了很多？
只需要加上`::before`伪类之后在属性里添加`content: '';`甚至不需要加`display:block;`
为什么要用伪类呢？因为可以少写很多<div>这边就少写了两个。
### III.在设置margin、padding的时候不希望表格ol或者ul的边上的li设置到。
选择器的nth-child(第几个li)属性
可以单独规定第几个li元素的属性。
例：
	
    section.Portfolio> nav >ol > li:nth-child(1){
    margin-left:0
    }
这样第一个`<li>`就没有margin-left了。
什么？`nth-child(1)`写起来太麻烦？
你试试写`first-child`也可以。
那么单独设定几个怎么做？
`nth-child(even)`奇数项
`nth-child(odd)`偶数项

## 2.动画`@keyframes`
### I.这个很容易敲错
其实keyframes动画也是有生成器的。这里举个例子。
```
@keyframes spin{
  from{
    transform: rotate(0deg)
  }
  to{
    transform: rotate(360deg)
  }
}
```
这里设置了动画的内容
之后在想让他这么动的元素里面加上
```
.balance{
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: linear-gradient(to bottom, #ffffff 0%,#ffffff 50%,#000000 51%,#000000 100%); 
  position: relative;
  margin:100px auto;
  animation-duration: 3s; //动画时间： 3s
  animation-name: spin;  //动画名称：spin（就是上面@keyframes后面的名字）
  animation-iteration-count: infinite;  //这行代码规定了动画循环进行
  animation-timing-function: linear;  //这行动画规定了动画线性播放（就是匀速）
}
```
#### i.除此之外还有`transition`属性
用来做一些小的变化`transition: all 0.3s; //表达了指定元素的一切变化的都加上transition变化属性，时间为0.3s`
### II.所以还是找Generator吧
[这个是奇怪的动画的网站](http://www.theappguruz.com/tag-tools/web/CSSAnimations/)

## 3.传说中的布局
### I.左右布局
#### i.通过定位的方法
HTML：
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
<div class="box1">
  <div class="left">这边定宽</div>
  <div class="right">这边自适应</div>
</div>
</body>
</html>
```
CSS：
```
.box1{
  position: relative;
  width: 100%;
  height: 100px;
}
.box1 .left{
  position: absolute;
  width: 100px;
  height: 100%;
  background-color: red;
}

.box1 .right{
  margin-left: 100px;
  width: 100%;
  height: 100%;
  background-color: black;
  }
```
通过定位属性以父元素box1为`position:relative`左边红盒子绝对定位吸附父元素。
右侧黑盒子用`margin-left: 100px;`让出红盒子的位置，同时`width: 100%;`来占据剩下的空间。来完成根据宽度自适应。

#### ii.通过float浮动
HTML:
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
<div class="box1" clearfix>
  <div class="left">这边浮动</div>
  <div class="right">这边自适应</div>
</div>
</body>
</html>
```
CSS:
```
.clearfix::after{
  content: '';
  display: block;
  clear: both;
}
.box1 .left {
  float: left;
  width: 100px;
  height: 100px;
  background-color: red;
}
.box1 .right {
  margin-left: 100px;
  height: 100px;
  background-color: black;
  display: inline-block;
  vertical-align: top;  //修复上面那行造成的裂隙。
}
```
通过让左侧红盒子添加`float: left;`脱离文档流（记得在父元素加clearfix伪类以防高度坍塌）
同时右侧黑框`margin-left: 100px;`空出左侧红盒子的位置。
这时候有个小问题：
###### 1.红盒子已经浮动了
那么黑盒子会无视红盒子的位置尽量占满一整行。那它可能会覆盖红盒子呀。
###### 2.有个叫做BFC的盒子：
①若浮动元素的块状兄弟元素为BFC，则不会占满一整行，而是根据浮动元素的宽度，占据该行剩下的宽度，避免与浮动元素重叠。
②浮动元素与其块状BFC兄弟元素之间的margin可以生效，这将继续减少兄弟元素的宽度。
③为了让黑盒子把红盒子的位置让出来，我们选择触发BFC：
`float`的值不为`none`
`position`的值不为`static`或者`relative`
`display`的值为`table-cell`, `table-caption`, `inline-block`, `flex`, 或者 `inline-flex`中的其中一个。
`overflow`的值不为`visible`
**这样就做到了左右两边：红盒子不定宽，黑盒子自适应。**

### II.传说中的圣杯布局
HTML:
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
  <div class="box" clearfix>
    <div class="middle">middle</div>   //顺序，先中再左右。
    <div class="left">left</div>
    <div class="right">right</div>
  </div>
</body>
</html>
```
css:
```
.clearfix::after{    //清除浮动伪类
  content: '';
  display: block;
  clear: both;
}
.box{
  padding:  0 100px;  //最外层给红黄两个盒子留宽度
  height: 100px;
}
.box .middle {
  float: left;
  width: 100%;
  height: 100%;
  background-color: black;
}
.box .left {
  float: left;
  width: 100px;
  margin-left: -100%;
  background-color: red;
  position: relative;
  left: -100px;    //往左边推出去
  height: 100%;
}
.box .right {
  float: left;
  width: 100px;
  margin-left: -100px;
  background-color: yellow;
  position: relative;
  right: -100px;    //往右边推出去
  height:100%;
}
```
给最外面的`box`加`padding`让出左右红黄盒子的位置。
给红黄盒子添加`position: relative;`让黑盒子不会受到他们俩位置变化的影响。
### III.关于居中
#### i.让图片居中
```
  background: url("wallhaven-w-min.jpg") no-repeat center center ;
	background-size: cover;
```
#### ii.让div水平居中
```
	margin-left:auto;
	margin-right:auto;
```
#### iii.内联元素居中：
给内联元素的父元素加:`text-align:center;`
如果不是内联元素，但是想让它居中怎么办？
`display:inline-block`了解一下。但是但是但是加完以后下面会有诡异的裂隙，所以需要：
`vertical-align: top;`

#### iv.让div在父级元素中绝对居中
父级元素加：`position:relative; `
子元素(需要对齐的div):
```
div{
 	position: absolute;
 	top: 0;
 	left: 0;
 	bottom: 0;
 	right: 0;
 	margin: auto;
}
```

## 4.写点别的
### I.`src`和`href`有啥子区别？
在写`link`的时候，必须要写`href`
在`<a>`标签的时候用`href`
在写`script`的时候，必须要写`src`
在写`img`的时候，必须要写`src`
在写`iframe`的时候，必须要写`src`

如果一定要区别的话`href`一般指的外部文档
`src`会嵌入文档里
**其实没什么规律...就是记住，多用就行**