---
title: setTimeout模拟setInterval
date: 2018-06-06 20:17:00
tags: JS
categories: JavaScript
---
# 0.一个问题

```
var duration = 20

setInterval(()=>{
    //要执行的代码
},duration)
```

- 这段代码中`setInterval`读了一次变量`duration`的值
- 之后`setInterval`再也不会读这个值了
- 就算我后面改了`duration`的值，他也不会再读了
- 这使得`setInterval`不能达到控速的目的

# 1.一个小技巧，模拟setInterval()

```
/* 
* body里有个div。
* id="output"
*/

let n = 0

let n = 0
let id = setInterval(()=>{
    n+=1
    output.innerText = n
    if(n>=10){
        window.clearInterval(id)
    }
},500)
```

```
let n = 0
let id = setTimeout(function fn(){
    n += 1
    output.innerText = n
    setTimeout(fn, 500)     //这句话是精髓:打出来一次以后，延时500,再次调用fn
},500)
```

**他们俩可以达到一样的效果**

## I.加个中断吧

```
let n = 0
let id = setTimeout(function fn(){
    n += 1
    output.innerText = n
    if(n<10){
        setTimeout(fn, 500)   //如果n<10，就调用fn，否则，什么也不做
    }
},500)
```

加个判断条件砸掉定时器，是不是很灵活
并不需要`window.clearInterval(id)`

# 2.总结
- 所有`setInterval`都可以改写成`setTimeout`
- 通过在`setTimeout`内部增加`setTimeout(fn,500)`达到重复调用的作用
- 以此达到模拟`setInterval`的作用