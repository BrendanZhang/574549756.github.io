---
title: 入门-CSS
date: 2018-03-24 19:29:24
tags: CSS
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

    <head>
      <style>
        body{
          background-color: gray;
        }
      </style>
    </head>

没问题，在头部加`<style>`标签就可以。

### III.那style多了头部是不是会超级长

    <head>
      <link rel="stylesheet" href="./a.css">
    </head>

引入外部样式就可以
**CSS文件也可以引入CSS**
`@import url(./需要引入的CSS.css);`
在用a的时候先引入b

### IV.float和clearfix
    <ul style="list-style: none; margin: 0; padding: 0;" class="clearfix"> //class之前为了去掉默认样式中的点和margin以及padding
      <li style="float:left;">内容</li>
    </ul>
想让表格的子元素横着排，给子元素加`style="float:left;"`但是这时候有BUG
所以在父元素加`class="clearfix"`

    .clearfix::after{
      content: '';
      display: block;
      clear: both;
    }

### V.第一个选择器`>`
表达了一个左边是父，右边是子。
**HTML默认字体大小：16px**

### VI.padding的缩写
顺时针，上右下左。