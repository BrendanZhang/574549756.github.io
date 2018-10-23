---
title: JavaScript-函数
date: 2018-04-23 03:48:49
tags: JS
categories: JavaScript
---
函数就是一段可以反复调用的代码块。
# 1.函数的五种声明方式：
## I.具名函数

```
function f(x,y){
    return x+y
}
f.name // 'f'
```

.name就是函数名

## II.匿名函数

```
var f
f = function(x,y){
    return x+y
}
f.name //'f'
```

.name就是变量名

如果要声明匿名函数，必须把它给一个变量

## III.具名函数赋值

```
 var f
 f = function f2(x,y){ return x+y }
 f.name // 'f2'
 console.log(f2) // undefined
```

.name随具名函数的函数名

和具名函数的区别： `f.name`是他相应具名函数的名字。
`console.log(f)`的时候，会报错,因为js会找不到`f2`
就很蠢：**这就是它的不一致性**
这是个作用域问题：
`function f2(){}`中的`f2`只能作用于花括号内

## IV.window.Function

```
var f = new Function('x','y','return x+y')
f.name // anonymous
```

.name 是`anonymous` 他他娘的是匿名的，名字叫`匿名的`

很不常用
所有的部分用字符串表示，字符串可以拼起来，也可以在里面加变量。

## V.箭头函数

```
var f = (x,y) => {
     return x+y
 }
 var sum = (x,y) => x+y
 var n2 = n => n*n
```

.name 是变量名

**只有一个参数**，不需要圆括号
如果**只有一句话**，不需要花括号也不需要return(也不能返回对象)
**多句话**的时候，用**分号**隔开

箭头函数是匿名的（没看到地方写名字呀）

# 2.调用函数
调用： call
## I.函数是如何储存在内存里的

```
new Function('x','y','return x+y')  //这时候栈里面存了地址ADDR
//堆里存了函数的内容：
name:   //名字，他叫匿名的
params: ['x','y']   //参数
fbody: 'return x+y'     //函数体
__proto__:指向函数，里面有个call
```

`eval：把字符串当代码执行`

```
f.call = function(){
    return window.evaleval（f.functionBody）
}
f(){
    return window.eval(f.functionBody)
}
```

可以理解为：f指的是这个对象
f.call()指的是执行这个对象的函数体

**可以执行代码的对象被叫做函数**

## II.f(1,2)和f.call(undefined,1,2)
f.call()才是硬核（hardcore）调用
贴心的f()语法糖

不吃糖的选手一定喜欢玩黑魂
不吃糖才能更加从容的了解this

## III.如何使用call

```
function f(x,y){
    return x+y
}
f.call(undefined,1,2)   //3
//第一个参数写undefined，从第二个参数开始传
```

# 3.this? arguments?

```
f.call(undefined,1,2) //3
//这时候好玩了，第一个参数就是this
//第二第三个参数就是arguments
```
## I.规律
1.call的第一个参数可以用this得到
2.call的后面的参数可以用arguments得到

```
f = function(){
    console.log(this)
    console.log(arguments)
}
f.call(undefined,1,2,3)
```
arguments会打出参数（除了第一个）组成**伪数组**
**普通模式下：**
如果this是undefined，浏览器会自动把this变成window(潜规则)
**严格模式下：**
this是什么他就打什么。

**所以，this就是call的第一个参数**

为何JS一定要this，一定要new。因为：**要长得像JAVA**

# 4. call stack
## I.调用队栈

```
function a (){
    console.log('a')
    return 'a'
}
function b(){
    console.log('b')
    return 'b'
}
function c(){
    console.log('c')
    return 'c'
}
a.call()
b.call()
c.call()
```

先进后出：
先a.call()再console.log('a')
然后console.log('a')抹
a.call()最后被抹掉

**先进入call stack的后出去**

## II.递归

```
function sum(n){
    if(n =+ 1){
        return 1
    }else{
        return n + sum.call(undefined, n-1)
    }
}

sum.call(undefined, 5)  //5 + sum(4)
//sum(10)  //10 + sum(9)
//sum(4)  //4 + sum(3)
```

求sum(5)的时候发现要找sum(4)
求sum(4)的时候发现要求sum(3)
...
一路找到sum(1)
之后一个一个抹掉，出来到sum(5)

## III.什么叫Stack Overflow
栈溢出

```
function sum(n){
    if(n =+ 1){
        return 1
    }else{
        return n + sum.call(undefined, n-1)
    }
}

sum.call(undefined, 1000000)
```

如果栈的长度没有1000000就会爆栈

chrome里压stack是有上限的

同时Stack Overflow是个网站，专门讨论bug的

# 5.作用域（scope）

## I.tree

```
var a = 1
function f1(){
    var a = 2
    f2.call()
    console.log(a)
    
    function f2(){
        var a = 3
        console.log(a)
    }
}

f1.call()
console.log(a)
```

```
            全局作用域（window/global）
                        |
    f1的作用域                         变量a
        |
 变量a      f2的作用域
               |
             变量a
```

如果把`var a = 2`改成`a = 2`JS会优先认为这是个赋值
JS会在上一级作用域找，找到了就用这个a—— **就近原则**
什么时候`a = 2`算声明全局？
在找到最后也没找到`a`的时候

## II.声明提升

```
var a = 1
function f1(){
                    //var a 应该在这里
    f2.call()   
    console.log(a)
    var a = 2           //变量提升： 先把它拆开看 var a 和 a = 2。 a = 2在这里
    
    function f2(){  //这里也有
        var a = 3       //这里也有
        console.log(a)  
    }
}

f1.call()
console.log(a)
```

拿到代码先提升**声明**部分
声明部分声明部分声明部分
改装完毕后它是这样的：

```
var a = 1
function f1(){
    var a               //提升声明
    function f2(){          //函数声明就不是声明了吗？也要提升
        var a           //提升声明
        a = 3
        console.log(a)
    }
    f2.call()
    console.log(a)
    a = 2
}
f1.call()
console.log(a)
```

所以调用f1以后`a`是什么？
赋值在console.log后面，f2的作用域又碰不到
那只有undefined咯

作用域仅代表变量**是哪个**
不表达变量的**值**

```
<ul>
    <li>选项1</li>
    <li>选项2</li>
    <li>选项3</li>
    <li>选项4</li>
    <li>选项5</li>
    <li>选项6</li>    
</ul>


var liTags = document.querySelectorAll('li')
for(var i=0; i<liTags.length; i++){
    
    liTags[i].onclick = function(){
        console.log(i)  //这个i是多少
    }
}

console.log(i)
```

i还是那个i

```
var liTags
var i
liTags = document.querySelectorAll('li')
for(var i=0; i<liTags.length; i++){
    
    liTags[i].onclick = function(){
        console.log(i)  //这个i是多少
    }
}

console.log(i)
```

遍历之后才是点击，结果是6

**只要它不是当场执行，都有可能变。**

# 6.闭包（Closure）

如果一个函数，使用了它范围外的变量，那么这个（函数+这个变量）就叫做闭包。

# 7.全局变量可耻！

```
<script>
function(){
    var parent = document.querySelector('#self')
    console.log(parent)
}.call()
</script>
```

parent是个全局变量，直接声明赋值会覆盖它
所以我们希望在用这个函数的局部变量——立即调用

就是声明一个匿名函数，然后立即调用。只是为了用局部变量

## I.浏览器会认为这是个语法错误
所以需要一些小技巧来改一下↓这一坨

```
<script>
function(){
    var parent = document.querySelector('#self')
    console.log(parent)
}.call()
</script>
```

### i.括号

```
<script>
(function(){
    var parent = document.querySelector('#self')
    console.log(parent)
}.call())
</script>
```

### ii.括号写在调用之前

```
<script>
(function(){
    var parent = document.querySelector('#self')
    console.log(parent)
}).call()
</script>
```

### iii.符号
负号
因为不需要这个值，只是为了这个局部变量
为了让浏览器知道：现在不是在声明一个函数，而是在声明并调用求值

```
<script>
-function(){
    var parent = document.querySelector('#self')
    console.log(parent)
}.call()
</script>
```

同理`+`也可以咯

```
<script>
-function(){
    var parent = document.querySelector('#self')
    console.log(parent)
}.call()
</script>
```

那`!`取反 `~`二进制的取反都可以

只要触发，让浏览器明白这不是一个声明而是一个立即执行函数，就可以。浏览器就不报错。 

## II.为了解决这个问题，我们有了`let`

```
<script>
{
    let parent = document.querySelector('#self')
    console.log(parent)
}
</script>
```

用一个代码块来把它框起来，这时候不能用`var`因为：
`var`这个东西只认函数，有函数就认没函数就创建全局变量。
但是`let`不一样，它的作用域就在这个代码块里面

做个试验

```
<script>
{
    var parent = document.querySelector('#self')  
}
console.log(parent)
</script>
```

**这时候，有一个变量提升**

```
<script>
var parent
{
    parent = document.querySelector('#self')  
}
console.log(parent)
</script>
```

这没办法呀，`var`就这样跑出去声明了一个全局变量，因为块包不住它。

### i.伟大的es6特性