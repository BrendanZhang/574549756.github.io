---
title: JSONP
date: 2018-05-07 20:09:31
tags: JSONP
categories: HTTP
---
# 0.有些个名词

## 跨域
跨域指在受到浏览器同源策略限制时（即不在同一个域下）跨域访问资源的一系列相关操作。
所谓跨域，或者异源，是指主机名（域名）、协议、端口号只要有其一不同，就为不同的域（或源）。浏览器中有一个基本的策略，叫同源策略，即限制“源”自己的脚本只能操作“同源”页面的DOM。（不然不乱套了，你的脚本改我的网站怎么办）

### js中的跨域
对于一段`JavaScript`脚本来说，其“源”与它存储的地址无关，而取决于脚本被加载的页面（我这里调用jQuery的库就可以用呀）
除了`<script>`，还有`<img>`、`<iframe>`、`<link>`等都具有跨域加载资源的能力。

## SRJ
Server Rendered Javascript
服务器返回的JS
在AJAX出现之前想出的不刷新页面但更新局部页面的方案
发送一个`script`之后`remove`这个`script`

# 1.什么是JSONP

JSON + padding = JSONP

```
${query.callback}.call(undefined,/*从这里开始*/{
    "success": true,
    "left": ${newAmount}
}/*到这里结束是JSON*/)

//头和尾分别是左右padding
```

同理String + padding = StringP

如果按照他的作用命名的话应该叫做：动态标签跨域请求

## I.用文字描述一下它是什么

请求方： frank.com 的前端程序员（浏览器）
响应方： jack.com 的后端程序员

~~以下functionName均表示要执行的函数名~~

### i.请求方创建script.src指向响应方，同时传一个查询参数 ?callbackName = functionName

```
script.src = 'http://jack.com:8002/pay?callback=' + functionName
```

### ii.响应方根据查询参数callbackName，构造形如：
    1.functionName.call(undefined,'你要的数据')
    2.functionName('你要的数据')
    这种响应

### iii.浏览器接收到响应
就会执行`functionName.call(undefined,'你要的数据')`

### iv.请求方得到了他要的数据

**这就是JSONP的过程**

## II.约定
### i.callbackName
统一叫做`callback`
### ii.functionName会用随机数
每个网站都得想个名字是不是很麻烦
所以用随机数：
避免函数名重复

```
let functionName = 'frank' + parseInt(Math.random()*100000)
window[functionName] = function(result){
    //里面改你的dom内容
}
script.src = 'http://jack.com:8002/pay?callback=' + functionName
document.body.appendChild(script)
script.onload = function(e){
    e.currentTarget.remove()
    delete window[functionName]     //反正这个函数只用一次，用完再用就再创建呗
}
script.onerror = function(){
    alert('fail')
    e.currentTarget.remove()
    delete window[functionName]         //用完干掉，成功失败都要干掉哟。
}
```

**用随机数然后用完干掉是为了不污染全局变量**

# 2.jQuery怎么说的？

```
$.ajax({
    url:"http://jack.com:8002/pay",
    dataType: "jsonp",
    success: function( response ){
        if(response === 'success'){
            amount.innerText = amount.innerText - 1
        }
    }
})
```

`callback`呢？
jQuery帮你传了
函数呢？
jQuery帮你造了

要管的只有：成功以后执行什么。

## 然而这个不是ajax
`.ajax`这个方法是个动态script

# 3.JSONP为什么不支持POST请求

因为JSONP是通过**动态创建script**的方法进行的，
而script**只能**发送GET请求不能发送POST请求。
