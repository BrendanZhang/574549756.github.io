---
title: JavaScript-数组
date: 2018-04-23 03:44:38
tags:  JS
categories: JavaScript
---
# 1.标准库

```
Object()
String()
Number()
Array()
Boolean()
Function()
```

这些东西。

# 2.new
除了`Object`
其他类型加上`new`
都会变成对应的对象（`复杂类型`）。

不加new返回的是`基本类型`

# 3.Array
`人类`：数组就是数据的有序集合
`JS`：数据就是原型链中有 Array.prototype 的对象(用Array构造出来的对象)
## I.他的一些属性
### new
因为它是对象，所以加不加`new`都一样。
### 它存在不一致性

```
var a = Array(3)    //length = 3
var a = Array(3,3)      //0:3,1:3,length: 2
```

是不是很坑，它传一个参数和传两个参数的功能是不一样的
传一个参数的时候仅代表它的长度。
## II.伪数组
原型链中没有Array.prototype

```
function f(1,2,3){
    console.dir(arguments)
}
//argument就是一个伪数组    长得像数组，但是__proto__直接指向Object.Prototype
```

## III.API
### i..forEach()

```
a = ['a','b','c','d']
a.forEach( function(x,y){        //接受参数是一个函数
    console.log('value', x)     //函数必定有两个参数
    console.log('key', y)        
} )
```

在写出`a.forEach`的时候，`a`这个数组已经被当做参数传进去了（想象成`this`）
### ii..sort
排序用的，一般内置的排序是快排
但是如何让JS知道你要`顺序`还是`倒序`呢？

```
a = [4,3,6,8,1,2,43,5]
a.sort(function(x,y){       //传入一个函数，函数必须有两个参数
    return x-y            //返回值必须是0 正数 负数
} )                         //0表示相等，位置相同 正数表示前一个大，放后面 负数表示前一个放前面。
```

这里可以得出，改变顺序和倒序只需要改变`return`后面的`x-y`或`y-x`就可以了
所以排完以后不是你想要的时候**换一下就行了**
### iii..join

```
a = [1,2,3]
a.join('逗号')   //"1逗号2逗号3"
a.join(',')         //"1,2,3"
```

干吗用的，加我一个用的。
### iv..concat
干嘛用的？
连起来用的

**一般用法：**

```
var a = [1,2,3]
var b = [4,5,6]
var c = a.concat(b)      //c = [1,2,3,4,5,6]
```

用来连接数组

**特殊用法：**

```
var a = [1,2,3]
var b = a.concat([])    //b = [1,2,3]

//这时候 a === b   //false
    //所以这是一种复制数组的方法
//b是一个和a数组内容相同的不同数组（ADDR不一样）
```

用来复制数组。
### v..map
和`forEach`几乎一样
区别在于`.map`有返回值
`forEach`返回`undefined`

```
var a = [1,2,3]
a.map(function(value,key){
    return value * 2
})

//[2,4,6]
    //也可以这么写，好看一点：
a.map(value => value * 2)
```

**映射**
一波操作以后，`a`还是没有变化
**return**
想return什么就return什么
对象什么的都可以。
### vi..filter
**过滤**

```
a = [1,2,3,4,5,6,7,8,9,10]
a.filter(function(value, key){
    return value >= 5
})
//[5, 6, 7, 8, 9, 10]
```

**拿来判断奇偶也可以**

```
a = [1,2,3,4,5,6,7,8,9,10]
a.filter(function(value, key){      
    return value % 2 === 0      //能被2整除的数
})
//[2, 4, 6, 8, 10]
```

### vii..reduce
**减少**

```
//求和用
a = [1,2,3,4,5,6,7,8,9]
a.reduce(function(sum,n){   //参数是个函数(必须两个参数)和一个初始项
    return sum + n              //把之前的项和当前项相加，返回下一次遍历的结果
},0)                        //遍历一遍以后得到总和
// 45
a.reduce((sum,n)=> sum + n , 0)
```

#### map可以用reduce表示

```
a = [1,2,3]
a.reduce(function(arr,n){   //之前项是arr，当前项是n
    arr.push(n*2)               //把当前项的两倍push进数组
    return arr              //返回到初始项(空数组)
}[])                            //遍历一遍以后填满空数组
// [2,4,6]
```

#### filter可以用reduce表示

```
a = [1,2,3,4,5,6,7,8,9,10]
a.reduce(function(arr,n){   //之前项是arr，当前项是n
    if(n % 2 === 0){            //是不是偶数？是偶数就到碗里来
        arr.push(n)         //偶数推进去
    }
    return arr                  //返回到数组
}[])                        //遍历一遍后填满空数组
```

# 4.Function

```
var f = function(a,b){
    return a+b
}

/////////用构造函数构造出来//////

var f = new Function('a', 'b', 'return a+b')        //把所有参数一字排开
//var f = new Function('参数', '参数', '构造体') 

//加不加new都一样 
```

## I.函数