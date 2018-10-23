---
title: 用JS做一个AJAX
date: 2018-05-11 02:26:47
tags: AJAX
categories: HTTP
---
# 0.AJAX 的所有功能
- 客户端的JS发起请求（浏览器上的）
- 服务端的JS发送响应（Node.js上的）

## I.JS 可以设置任意请求 header 吗?
- 第一部分 request.open('get', '/xxx')
- 第二部分 request.setHeader('content-type','x-www-form-urlencoded')
- 第四部分 request.send('a=1&b=2')

## II.JS 可以获取任意响应 header 吗？
- 第一部分 request.status / request.statusText
- 第二部分 request.getResponseHeader() / request.getAllResponseHeaders()
- 第四部分 request.responseText

## 所有功能都给了JS

```
服务端              request(4)           客户端
Node.js        <=================       chrome
               =================>
                   response(4)
```

# 1.回调

```
call a function
call a function back
```

## I.回调的问题
每个程序员的回调名不一样
封装习惯也不一样。
不能每个库都去看文档吧。

## II.Promise

```
function xxx(){
    return new Promise((f1, f2) => {
        doSomething()
        setTimeout(()=>{
            // 成功就调用 f1，失败就调用 f2
        },3000)
    })
}

xxx().then(success, fail)

// 链式操作
xxx().then(success, fail).then(success, fail)
```

如果需要对结果多次处理，那么就多`then`几个

成功就是第一个参数，失败就是第二个参数，还能进行链式操作。
是不是统一了标准
这就是`promise`的意义

其中第一个`then`的处理结果`return`出来，交给第二个`then`处理

### i.注意

如果`Response Headers`中的`Content-type`
为`text/json`。 
`jQuery`就会自动用`JSON`去`parse`一下

### ii.promise的模式

```
window.Promise = function(fn){
    // .....
    return{
        then: function(){}
    }
}
```