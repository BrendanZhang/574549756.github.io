---
title: canvas画板
date: 2018-04-05 11:35:09
tags: canvas
categories: HTML
---
## 1.尝试用div画画
```
// 按下去鼠标
    doucment.onmousedown = function(){
        console.log(x)
    }
//动鼠标
	document.onmousemove = function(){
    	console.log(y)
    }
//松开鼠标
	document.onmouseup = function(){
    	console.log(1)
    }
```
### 最好单独用div
	`<div id="canvas"></div>`
### 那么上面代码优化为
```
    var div = document.getElementById('canvas')
    //按下鼠标
    div.onmousedown = function(x){
    	var x = a.clientX
        var y = a.clientY
        var divA = document.createElement('div')
        divA.style = "width: 6px; height: 6px;"+"background:black; border-radius: 3px;"
        div.appendChild(divA)
        "position: absolute; left: "+(x-3) +"px;" + "top: "+(y-3)+"px;"
    }
    //动鼠标
    div.onmousemove = function(y){
    	
    }
    //松开鼠标
    div.onmouseup = function(z){
    	console.log(1)
    }
```
### 小技巧（Flag）
通过一个变量`var painting = false`
全局变量的时候默认为false
在按下去鼠标的时候`painting = true`
移动鼠标div将其作为判断条件，如果 `if(painting){}`如果painting存在则继续
在松开鼠标的时候改变变量painting为false

## **2.然而做了这么多，他画画还是断断续续的，所以告诉我们画画不能用div，要用canvas**
### canvas不能用CSS控制宽高
```
context.strokesStyle描边
context.strokeRect(xx,yy,xxx,yyy)初始坐标，结束坐标
context.fillStyle = '颜色';填充
context.fillStyle(xx,yy,xxx,yyy)初始坐标，结束坐标

context.clearRect(xx,yy,xxx,yyy)初始坐标，宽度，高度（清除）
```
### 圆弧
```
context.arc(x,y,半径,起始角度,结束角度,顺时针或者逆时针(默认顺时针，anticlockwise逆时针));
//注意这里的结束角度不是度数，而是用元周率度量的所以要用Math.PI就是180度Math.PI/2就是90度
```
除了矩形都要context.beginPath()一下

canvas里面的坐标都是想对于canvas的而不是想对于视口的，所以要修正他。
### 如何创建补间
```
var context = xxx.getContext('2d')
context.beginPath();
context.moveTo(0,0) //起点
context.lineWidth = 5  //宽度
context.lineTo(200,0)  //终点
context.stroke()  //
context.closePath() //闭合
```
### 获取用户视口的宽高的方法（这个是最简单的了）
```
var pageWidth = document.documentElement.clientWidth
var pageHeight = document.documentElement.clientHeight
yyy.width = pageWidth
yyy.height = pageHeight
//获取用户视口尺寸
```
```
window.onresize = funtion(){
  var pageWidth = document.documentElement.clientWidth
  var pageHeight = document.documentElement.clientHeight
  yyy.width = pageWidth
  yyy.height = pageHeight
}
//改变宽高时，同步宽高。
//resize事件来改变宽高
```
## 3.如何让移动端也用上呢？
### 需要一个特性检测
```
if(document.body.ontouchstart !== undefined){
	//如果存在说明他是触屏设备
}else{
	如果不存在，那么说明不是触屏设备，监听鼠标操作是正确的。
}
```
### 触屏是支持多点触控的
所以touch时间需要把用户滑动的手指都用数组储存起来
放在touches里面，所以找坐标的工作要交给`var x = aaa.touchs[0].clientX`以及`var y = aaa.touch[0].clientY` 

## 4.补充点功能
### 改变画笔颜色
#### I.首先让图标变好看点
我们需要`iconfont.cn`搞点图标玩玩
把搞到的图标代替button按钮
设置id便于选择器选择。
```
<svg id="pen" class="icon">
	<use xlink:href="#icon-pencil"></use>
</svg>
<svg id="eraser" class="icon">
	<use xlink:href="#icon-eraser"></use>
</svg>
```
CSS
```
.actions{
	position: fixed;
	top: 0;
	left: 0;
}
.actions svg.active{
	fill: red;
}
```
那么在js中调用active状态，通过`classList.remove('')`和`classList.add('')`来添加和移除相应class
```
var eraserEnabled = false
pen.onclick = function(){
	eraserEnabled = false;
	pen.classList.add("active")
	eraser.classList.remove("active")
}
eraser.onclick = function(){
	eraserEnabled = true
	eraser.classList.add("active")
	pen.classList.remove("active")
}
```
