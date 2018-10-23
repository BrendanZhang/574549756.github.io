---
title: JavaScript-对象
date: 2018-04-12 15:46:37
tags: JS
categories: JavaScript
---
# 1.全局对象
## I.window（global）
标准里他叫做global
浏览器上他叫做window
是一个对象
### i.属性
例：

```
global.parseInt
global.parseFloat
```

### ii.属性分为两类
如果函数是`window.`那么这个`window.`可以省掉，毕竟它是全局函数。
#### ECMAScript规定要有的
比如

```
parseInt
parseFloat
Number()
String()
Boolean()
Object()
```

必须得有
#### 私有的（浏览器私有的）
比如

```
alert（弹框提示）
prompt（用户填写）
confirm（用户确认）
console（开发者打印）
document(能对文档做的所有操作)DOM(w3c制定)
history(浏览器操作)BOM
```


都是浏览器自己实现的

# 2.简单类型与对象的区别
## I.Number()
### 方法
#### var n = 1
但是它不能.toString
#### var n = new Number(1)
这个方法很少人用...

```
1=>{valueOf():1,} //把1转变成对象
```
历史遗留问题

#### 如何写的简单同时又可以用.toString呢？
临时转换：

```
temp = new Number(n)
temp.toString()
拿到对象里的值再输出
然后去除temp的ADDR
对象内容被回收
END
```

所以在：

```
var n = 1
n.toString() //发生了一次temp的转换
```

**JS之父做的操作**

## II.String()
操作和Number()一样
### 记几个API吧

|API|作用|备注|
|:---:|:---:|:---:|
|.charAt(n)|获取第n位的字符|n为第几位|
|.charCodeAt(n)|获取某一个索引对应的字符的编码|n为第几位。|
|(数字).toString(进制数)|将数字转换为制定进制数|可以和`.charCodeAt(n)`组合使用|
|concat()|连接两个字符串|`字符串1.concat(字符串2)`和命令行的`cat`是不是兄弟|
|endsWith()|一个字符串以什么结尾||
|.trim()|去掉两边的空格|`字符串.trim()`|
|.slice|切片，保留指定位|`目标字符串.slice(0,2)`仅保留前两位（这两个数字包前不包后）|
|.replace|替换|`字符串.replace('要换谁','换成谁')`|

## III.Bullean()
里面东西超少

```
toString
valueOf
```

## IV.null和undefined没有对应的函数
## V.object
之前都是基本类型
现在到了对象

```
var o1 = {}
var o2 = new Object()
// 他俩都是空的，但是。
o1 === o2 //false
// 回到前面ADDR和对象的关系，o1和o2的地址不一样，就算内容一样，也不相等。
```

所以，直接用`var o1 = {}`吧，他俩没差，还少敲几个字符。你又不是敲java。

## VI.总结一下
他们都有`toString()`和`valueOf()`
那岂不是很占内存
可不可以都用同一个`toString()`和`valueOf()`

如何让他们都指向同一个`toString()`和`valueOf()`呢？

### JS向你掏出来了一只`__proto__`

# 3.原型
## 举个例子

```
var o1 = new object()
o1.name = 'oracle'
o1.age = '24'
//////////////////
o1 ADDR 200:
name: oracle
age: 24
...
__proto__:ADDR 100 //用__proto__指向共用属性
//////////////////
ADDR 100(共用属性):
...
toString: A10
valueOf: A11
...
```

他们都指向共用属性，检查一下？

```
o1 === o2 //false
//因为他们是不同对象
o1.toString === o2.toString //true
//但他们的.toString都指向共用属性
```

## I.那么简单类型的共用属性呢？
想象一棵树，根部是`object`的共有属性。

### i.比如number
`var n = nwe Number(1)`
这里面的`toString`和`obj`里的不一样耶。他都可以转进制数。
而且他还有别的`.toFixed`什么的

首先，number会指向一个number才有的共用属性：

```
...
toFixed
toExponential
toString
...
__proto__: Object //这一层再放一个__proto__去找所有对象的共用属性
```

然后在number的共用属性里面，找对象的共用属性
**自己用不一样的，再从别处引用一样的**

## II.这就是原型链
从它的类型到它的类型的共用属性在到对象的共用属性，一条链过去，一路都是节点。

### i.prototype
如果一个哈希没有被引用的话，他会被浏览器垃圾回收（没大哥罩着就要被干掉）
那么共用属性在没人引用的时候，就是prototype在引用他。

从现在起，把共用属性这个词，换成**原型**。

```
Object.prototype
var o1 = {}
o1.__proto__ === Object.prototype  //true
```

这样就清晰了，它们一直以来，引用的是谁。
### ii.Number.prototype
了解到`number`属性自己的原型里面还有引用对象的原型，做个测试：

```
var n1 = new Number(1)
n1.__proto__ === Number.prototype //true
n1.__proto__.__proto__  === Object.prototype  //true
```

那么我们就可以理解为什么
`n1.hasOwnProperty('2')  //false`
n1可以调用他第一层`__proto__`里没有的`.hasOwnProperty`了
因为会一层一层的找，第一层找不到找第二层。
**这条链子在JS引擎开启的时候就连上了**

## III.`__proto__`和`prototype`有什么区别

```
String.prototype   //是 String 的共用属性的引用（不让共用属性被清理）
s.__proto__   //是 String 的共用属性的引用（真的是要用它）
```

### i.形式上呢？
var 接对象 = new 接函数(也是对象)

```
var 对象 = new 函数()
对象.__proto__ === 函数.prototype
```

那么我们可以说他们的区别：
`__proto__`是对象的属性
`prototype`是函数的属性

## IV.特殊的function
找寻本源：

```
Object.__proto__ === Object.prototype //false
Object.__proto__ === Function.prototype
//true
```

问题来了，我们把`__proto__`当成链
把`prototype`当成锚

`Function`本身也是一个`Function`对象

```
var Function = new Function()
Function.__proto__ === Function.prototype   //true
//他自己是Function对象，我要通过Function对象会指向Function函数。
```

思考一下，是不是先有鸡还是先有蛋的问题。
并不是，我有一个`Function.prototype`才可以调用这个函数构造`Function对象`。
但是它本身已经存在了，为什么要构造自己，所以`Function.__proto__`会指向自己。

同理`看似Object.prototype`是大BOSS，谁都指向他。
其实他也是通过`Function.prototype`构造的，也就是说是`Function`是`Object`的**构造函数**。

**有没有一种垂帘听政的感觉**
