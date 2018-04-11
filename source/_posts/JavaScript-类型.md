---
title: JavaScript-类型
date: 2018-04-11 10:10:04
tags: JS
---
# 1.首先要搞清楚什么是内存
干吗用的？存东西用的。通电存东西，断电就GG。
外存没有内存快
最快的外存不就是SSD嘛，因为它能接近内存的速度。
机械硬盘，就很容易坏，十年基本就坏了。
SSD，不容易坏，但是一坏就全坏了。
## I.它是怎么工作的
### i.举个例子
假设内存有2G
开机
操作系统 512M
浏览器 1G （浏览器真的很占内存）
假设浏览器两个页面

```
页面1（100M）
        HTML+CSS+JS+网络HTTP+其他 
页面2（100M）
        ...
```

假设JS分到了100M
我们写了一个`var a = 1`
小心翼翼分成两个大区

```     
代码区
        a
        
数据区
        1
```

如果写复杂点

```
var a = 1
var b = 'Oracle'
b = a
var o = {
        name:'Oracle',
        age: 24
}
var c = true
o.gender = 'male'
var o2 = {
        name: 'Protoss'
}
o2 = o
第一步：变量提升，把var都放在前面
之后依次执行
```

其实数据区也分为两个——
Stack（栈）和Heap（堆）

```
Stack（栈内存）
        a:64位浮点数储存a
        b:64位浮点数储存b
        b=a:把a存的东西，覆盖到b上
        c:第一位为1后面全是0存一个true
        var o ={}:存一个地址ADDR 100 //去Heap（堆内存）找
        o.gender = 'male':找到o的地址（ADDR 100）把它加进去。
        var o2 = {}:和o一样存一个地址ADDR 200
        o2 = o: 和b = a的操作一样，不一样的是把o的地址给o2
                o2的ADDR 200变成了ADDR 100


Heap（堆内存）
        ADDR 100
                name:'Oracle'
                age: 24
                /////////////
                gender: 'male'
        ADDR 200
                name:'protoss'
```

这一套操作
### ii.数据
数字：64位
字符：16位（ES3）
值：
**简单**:存Stack
**复杂**(obj):存Heap地址（还是存在Stack里面）
### iii.引用
object存入ADDR 100
就可以称object是对象的**引用**
所有变量和对象的**关系**，都是**引用关系**
### iv.存在对象问题的时候，走一遍i里的流程就清楚了
PS：连续赋值从右往左顺序拆开写。
## II.垃圾回收
GC
如果一个`对象`**没有被引用**
它就是**垃圾**
将被回收
### i.例

```
var a = {name:'a'}
var b = {name:'b'}
a = b
```

这时候，b和a指向了同一个ADDR
那么a原来的ADDR就变成了垃圾
**没人罩着，就要被干掉...**
### ii.IE有个BUG
如果把页面关了(body没了，他引用的地址断了)
地址之间互相引用，但不和外部联系
他们本应该被清掉
但是（尤其IE6）IE里，你只要不关掉整个IE，他们会一直存着。
垃圾一直存着...内存boom。
所以需要在页面关闭之前执行：

```
window.onunload = function(){
        document.body.onclick = null
}
//然而需要把所有的监听的函数都设为null，需要写很多行。
```

这就是传说中的——内存泄漏：
由于浏览器的BUG,使得该被标记为垃圾的东西，没有被标记为垃圾。
# 2.深拷贝？浅拷贝？
## I.深拷贝

```
var a = 1
var b = a
b = 2
//a = 1不改变
```

b的改变不影响a
这就是深拷贝
基本类型 赋值 就是深拷贝
## II.浅拷贝

```
var a = {
        name: 'a'
}
var b = a
b.name = 'b'
a.name // 也是b了
```

指向同一个ADDR改变地址对应的内容后
a也变了。
这就是浅拷贝。
# 3.类型互相转换
## I.方法
### i.转字符串`.toString`
`null`不可以，会报错
`undefined`不可以，会报错
`object`并不能得到想要的`key:value`只会得到`[obj,Obj]`

我们热爱的`console.log`就是这个原理
如果你`console.log`的东西不是字符串，他会自动加上一个`toString`

#### `.toString`太长了老司机怎么转的？
数字：加上一个空字符串就好了。
`1 + ''`
布尔：加上一个空字符串就好了。
`true + ''`
顺序可反。
而且`'' + null`和`'' + undefined`也可以哟

#### 这时候就引出一个问题
`1+1`等于2
`1 + '1'`算什么
加号会优先加相同类型的东西，所以他会先把数字变成字符串。

#### 全局方法`window.String()`
把不是字符串的东西，变成字符串。（可以变`null`和`undefined`）

#### 所以最方便的转字符串方法是加上一个空字符串

### ii.转布尔`Boolean()`
字符串:  `Boolean(1) //true`
        `Boolean(0) //false`
        `Boolean(2) //true`
        `Boolean( ) //true`
null:   `Boolean(null) //false`
undefined: `Boolean(undefined) //false`
对象:    `Boolean({}) //true`
        `Boolean({name:'Oracle'})  //true`

#### 这个API好长...
`!`可以取反
那么取反两次不就是原来的吗

```
!!null //false
!!0 //false
!!{} //true
!!{name:'Oracle'} //true
```

#### 所有类型都可以变成布尔但是好难记哦
只有五个特殊的
number： 只有两个是false`0`和`NaN`
String： 只有空字符串是`false`其他全是`true`
null： 就一个值，`false`
undefined：就一个值`false`
object：都是`true`所有的数组和函数

也就是有五个`falsy`值
`0` 
`NaN` 
`''` 
`null` 
`undefined`
还有个`false`因为他本来就是`false`
### iii.转number
#### 朴实方法`Number('1')`
#### 全局方法`parseInt('1',10)`
`10`代表是看做十进制转换
但是`parseInt('011')  //11`
因为后面的参数没写，所以当成10进制。
用它转非数字`parseInt('s') //NaN`
数字非数字混合 `parseInt('1s') //1`
所以得到他的规则：从头开始解析能解析的，一旦遇到不能解析的，就返回。
#### 有浮点数的话`parseFloat('1.23')`
`parse`是解析
#### `'1'-0`骚方法（最常用）
任何一个东西-0就会得到一个`number`
#### 取正`+ '1'`更骚的方法
负数也可以取正？`+ '-1'`这个是可以的，结果还是`-1`。
### iv.转object
