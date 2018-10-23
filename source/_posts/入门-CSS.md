---
title: 入门-CSS
date: 2018-03-24 19:29:24
tags: CSS
categories: CSS
---
## 1.CSS（Cascading Style Sheets）层叠样式表
### I.诞生与发展
#### i.两个人发明CSS
哈肯·维姆·莱（Håkon Wium Lie）提出CSS的最初建议（1994）
伯特·波斯(Bert Bos)当时正在设计一个叫"Argo"的浏览器，他们决定一起合作设计CSS。
#### ii.W3C接管CSS
1997年初，W3C内成立CSS工作组
#### iii.CSS 2.1
1998年5月，删除了2.0中基本不被支持的内容和增加了一些已有的浏览器的扩展内容。
最受欢迎，支持最广泛的CSS。Which means：从IE 5.5支持CSS 2.1。
做前端，低于IE 8，不看，不管，不测试。Why?淘宝是这样的。而且现在的电脑，IE 11起好吗？
#### iv.CSS3
2011年开始。什么？CSS 3这么久了吗？对的，就是这么久。
·CSS选择器leval 3
·CSS媒体查询leval 3
·CSS Color leval 3
他们三个模块被统称为CSS 3。详情请点击[CSS文档](https://www.w3.org/Style/CSS/specs.en.html)内容超级多。
#### v.CSS 4？
不会有CSS 4。只有各个模块leval 4
前端每18个月难度翻一倍...
#### vi.Tips:
·LESS CSS：简化过后功能更多的CSS语言
·SASS：同上，比上面的功能还多
·PostCSS：一种CSS处理程序，纠错之类的
三个周边工具，逼格超高。

### II.如何学习
#### i.MDN
老朋友了不多介绍了。
可以看可以查

#### ii.CSS-Tricks
SNIPPETS标签下的代码片段
有效果以及代码。
这个网站里面有各种CSS的奇淫技巧（真是一个贴切的名字）。
善用搜索引擎可以搜一切技巧。前提：英语水平。

#### iii.博客
阮一峰CSS
张鑫旭CSS（CSS大神，精通精通精通CSS）

#### iv.Coderops
炫酷的CSS效果，超Cooooooooooooool。
按钮，加载条，各种。他为了表达CSS能做很多事情。
基本一周出一个特效。

#### v.《CSS揭秘》
CSS技巧，有汉化。八个章节，讲了很多基础特效。

---
**规范文档是最强的，如果把文档研究透了，那太强了。**

## 2.自己敲一敲

### I.内联样式
`<body style="background-color: black">里面是内容</body>`
`<h1 style="text-align: center; color: white;">内联样式</h1>`
在标签里面写CSS样式。也称为Style属性

### II.但是这样标签好长呀
```
<head>
    <style>
        body{
          background-color: gray;
        }
    </style>
</head>
```
没问题，在头部加`<style>`标签就可以。

### III.那style多了头部是不是会超级长
```
<head>
   <link rel="stylesheet" href="./a.css">
</head>
```
引入外部样式就可以
**CSS文件也可以引入CSS**
`@import url(./需要引入的CSS.css);`
在用a的时候先引入b

### IV.float和clearfix
```
<ul style="list-style: none; margin: 0; padding: 0;" class="clearfix"> //class之前为了去掉默认样式中的点和margin以及padding
    <li style="float:left;">内容</li>
</ul>
```
想让表格的子元素横着排，给子元素加`style="float:left;"`但是这时候有BUG
所以在父元素加`class="clearfix"`
```
.clearfix::after{
    content: '';
    display: block;
    clear: both;
}
```
还可以用什么呢？让块横着排的方法？
有一个叫做`display: inline-block;`可以让块像内联元素一样排列了。
**但是，建议还是用`float`吧**

### V.第一个选择器`>`
表达了一个左边是父，右边是子。
**HTML默认字体大小：16px**

### VI.padding的缩写
顺时针，上右下左。

### VII.一个元素的高度是由什么决定的？
#### **由内容决定**
**`<div>`高度由其内部文档流元素的高度综合决定。**
##### **文档流**：
文档内元素的流动方向。
##### **流动方向**：
**内联元素**从左至右流动，若流动受到阻碍（例如宽度不够），则换行继续从左往右流。
**块级元素**自上而下流动，每个块占一行(管你宽度多少他就不用)。
##### Tips:
tip1：内联元素在宽度不够的时候如果有border，他不会在另起一行的部分加上border，而会截断这个border。
tip2：中文会截断换行，英文如果不空格，打死不换行。
如果你希望英文也会截断，请加入一个属性`word-break:break-all;`默认为`word-break:break-word`
如果你希望他一直不断`word-break:keep-all;`了解一下。
中文网站推荐：`word-break:break-all;`
#### **那么`<span>`这种内联元素的高度由什么决定呢？**
##### 字体设计（基线）
基线 上部 下部
对齐是基于基线的。
我们常说的`font-size: 100px;`指的是字体（注意是字体）的最高点和最低点的竖直距离。
但为什么把字放在`<span>`里面加上border会比字体本身高度要多出来呢？
**因为**:这个字体设计的**建议行高**，就是字体大小的倍数（例如100px大小的字体，span高度140，那么建议高度就是1.4）
###### 这时候怎么破呢？
改它的行高系数呗`line-height: 1.2;`把他系数固定就好了。

##### 那么有多个`<span>`的`<div>`的高度怎么说？
一旦涉及到内联元素，div的高度就玄学了呀。
字体小的时候`<div>`可以用line-height来控制高度，想要确定的高度就拿padding凑凑吧。
有时候迫不得已...定死height这个属性，可能会出现无穷无尽的问题（很难维护之类的）。
所以`display: inline-block;`之后通过改变padding的方式改变宽高好一点。
**`inline-block`状态下不会合并外边距。**这时候可能下面会有一条诡异的空隙
这时候需要`vertical-align: top;`
`<span>`是不接受宽高这个属性的。

### 感觉再不练Grid布局，真的就要累死人了。
早就有grid布局插件了。

### VIII`position`
#### `position: fixed;`
可以脱离文档流。相对于屏幕脱离文档流。
这时候他飘了，不像一个正常规则下的排列了，只能`width: 100%;`这种巨坑把它卡死...后面又是好多大坑。
#### `background-position`
`background-position: center center;`可以让背景图片在`<div>`里面居中
但是很多时候由于图片过大导致超出div范围所以加入`background-size: cover;`属性使其自适应。
同样，在`<div>`加入属性`max-width: 800px`则会使div在800px以内缩放自适应。
`margin-left：auto;`
`margin-right:auto;`即可水平居中。
#### `position: absolute`绝对定位
和`position: fixed`不同的是
`absolute`可以相对父级（或以上）元素有`position: relative;`的第一个元素相对定位。
在我发现footer在到处飘的时候通过它绝对定位(需要设置width left right)

### IX.如何用CSS画个三角玩玩。
```
div{
    border: 10px solid red;
    width: 0px;
    height: 0px;
    border-top-color:black;
    border-right-color:blue;
    border-left-color:green;
}
```
现在我们有四个三角形
```	
div{
    border: 10px solid red;
    width: 0px;
    height: 0px;
    border-top-color:black;
    border-right-color:blue;
    border-left-color:green;
    border-top-width:0px;
}
```
现在我们有三个长得不一样的三角形了。
```
div{
    border: 100px solid transparent;
    width: 0px;
    height: 0px;
    border-top-color:transparent;
    border-right-color:transparent;
    border-left-color:red;
    border-top-width:0px;
}
```
把不需要的三角形部分透明就OK了呀。那么top和right的color属性也不需要了。
#### i.CSS 3的属性
##### 线性渐变：`linear gradient`
他有相应的生成工具：`ultimate CSS Gradient Generator`[Google it](http://www.colorzilla.com/gradient-editor/).


#### ii.CSS tricks shape
[这个网站教你用CSS画画](https://css-tricks.com/examples/ShapesOfCSS/)

#### iii.iconfont
[这个网站是找图标的](http://iconfont.cn/)
svg需要记住三个属性
`width`宽
`height`高（需要和宽一起变化）
`fill`颜色（这是svg的语法,用来改变svg图标的颜色）