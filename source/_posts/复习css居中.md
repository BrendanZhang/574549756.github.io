---
title: 复习css居中
date: 2018-09-03 04:00:39
tags: CSS
categories: CSS
---

# 0.如何居中？

最近写样式的时候用到很多需要居中的情况。
本着不应该抱着 flex 用一辈子的心态，复习一下　 CSS 居中。

# 1.水平居中

## I.内联元素

父级元素身上写　`text-align: center`

## II.块级元素

```
margin: 0 auto
```

# 2.垂直居中

## I.tabel 自带功能

```
<table class="parent">
    <tr>
        <td class="child">
            blablablablabla
        </td>
    </tr>
</table>
```

`table` 标签自带 content 居中的功能。

## II.伪类

```
<div class="parent">
    <div class="child">
        blablablablabla
    </div>
  </div>
```

```
.parent{
  height: 600px;
  text-align: center;
}

.child{
  display: inline-block;
  width: 300px;
  vertical-align: middle;
}

.parent:before{
  content:'';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
.parent:after{
  content:'';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
```

-   通过伪类设置 `100%` 高度和 `display: inline-block` 属性使子元素居中
-   拿伪类占坑

## III.假装自己是个 table

```
<div class="table">
    <div class="td">
        <div class="tr">
            <div class="child">
                blablablablabla
            </div>
        </div>
    </div>
</div>
```

```
div.table{
  display: table;
  height: 600px;
}

div.tr{
  display: table-row;
}

div.td{
  display: table-cell;
  vertical-align: middle;
}
```

-   通过 `display: table` `display:table-cell` 来假装自己是个表格
-   这样确实可以居中

## IV. 绝对定位强行移过去

### i.用 margin 修正

```
<div class="parent">
    <div class="child">
        blablabla
    </div>
</div>
```

```
.parent{
  height: 600px;
  position: relative;
}
.child{
  width: 300px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -150px;
  height: 100px;
  margin-top: -50px;
}
```

-   这种方法就比较粗暴了
-   绝对定位定位 `.child`
-   然后用 `margin` 修正绝对定位的偏移

### ii.用 transform 修正

```
.parent{
  height: 600px;
  position: relative;
}
.child{
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
}
```

-   做法同上，大同小异
-   由于绝对定位会以元素的左上角为定位点
-   所以用 `transform` 各偏移一半即可修正

### iii. 脱离文档流后 margin: auto

```
.parent{
  height: 600px;
  position: relative;
}
.child{
  position: absolute;
  width: 300px;
  height: 200px;
  margin: auto;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
```

-   绝对定位上下左右定位皆为　０
-   `margin:auto` 实现居中

## V.flex

-   这个就不用多说了
-   `justify-content` `align-items` 这些都用烂了

# 3.选择器优先级

-   选择器越具体，优先级越高。(#xxx 肯定比.xxx 优先)
-   同优先级，写在后面的覆盖前面的
-   !important; 优先级最高。一般不用。(如果滥用这个，那么还有什么意义呢？大家都用等于没用)

# 4.BFC

-   `overflow: hidden` 可以清除浮动(但是一般用 `.clearfix` 来清除浮动)
-   `overflow: hidden` 可以取消父子 `margin` 合并(子元素的 margin 把父元素挤下去。)
-   为了解决 `margin` 合并，可以使用 `padding-top: 0.1px;`(因为 BFC 的副作用有点多)

# 5.如何清除浮动

1. `overflow:hidden` 可以，不推荐。
2. `clearfix` 可以，这么写在父元素上：

```
.clearfix::after{
    content: '';
    display:block;
    clear:both;
}
/*兼容IE*/
.clearfix{
    zoom:1;
}
```
