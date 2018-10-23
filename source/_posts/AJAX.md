---
title: AJAX
date: 2018-05-09 08:21:28
tags: Ajax
categories: HTTP
---
# 0.关于发送请求
## I.如何发送请求

- 用`form`可以发送请求，但是会刷新页面或新开页面
- 用`a`可以发`GET`请求，但是也会刷新页面或新开页面
- 用`img`可以发`GET`请求，但是只能以图片的形式展示
- 用`script`可以发`GET`请求，但是只能以脚本的形式运行
- 用`link`可以发`GET`请求，但是只能以`CSS`、`favicon`的形式展示

**有没有一种方法可以：**
- `GET`、`POST`、`PUT`、`DELETE`请求都可以做到
- 想用什么形式展示就以什么形式展示

## II.伟大的巨硬(Microsoft)
- 在IE5率先在`JS`中引入`ActiveX`对象（API），使得JS可以直接发起HTTP请求。
- 随后`Mozilla`、`Safari`、`Opera`也跟进了，命名`XMLHttpRequest`，并被纳入`W3C`规范

### i.结果巨硬飘了
- 巨硬认为自己的`IE6`已经无敌了，所以解散了开发小组
- 给了`chrome`巨大的机会（现在反超IE，占有量达到40%）

### ii.Google Gmail展示了网页的体验也可以那么好
页面不刷新，仅局部更新
网页的体验强了，很多事情不需要使用软件来完成了。
前端程序员开始专心于JavaScript
所以还是要感谢伟大的巨硬的`ActiveX`

# 1.AJAX
Jesse James Garrett
将异步的`JavaScript`和`XML`这两项技术
称为`AJAX`
- `async`异步
- `JavaScript`我们热爱的JS
- `and`和
- `XML`XML

## I.技术要点

- 使用`XMLHttpRequest`发送请求
- 服务器返回`XML`格式的字符串（现在都用`JSON`）
- `JS`解析`XML`，并更新局部页面

**需要知道如何使用`原生JS`来发送`AJAX`请求**

## II.格式

```
myButton.addEventListener('click', (e)=>{
    let request = new XMLHttpRequest()   //声明一个XMLHttpRequest对象
    request.onreadystatechange = ()=>{      //监听状态改变，尽量往上放
        console.log(request.readyState)
    }
    request.open('GET', '/xxx')    //配置request 'Method', 'url', '是否异步'后三个一般不传默认就行
    request.send()
})
```

### i.readystate
当前请求的状态


|值|状态|描述|
|:---:|:---:|:---:|
|0|UNSENT（未打开）|代理被创建，但尚未调用 open() 方法。|
|1|OPENED（未发送）|open() 方法已经被调用。send（）方法还未被调用|
|2|HEADERS_RECEIVED（已获取响应头）|send() 方法已经被调用，并且头部和状态已经可获得。|
|3|LOADING（正在下载响应体）|下载中； responseText 属性已经包含部分数据。|
|4|DONE（请求完成）|整个请求过程已经完毕（请求，已经把响应 下载完毕）|

### ii.request.status
请求得到的响应状态码

`>= 200`请求成功
`>= 300`浏览器会再发一个新的请求
`>= 400`请求失败

# 2.JSON
这是一种语言
JSON（**J**ava**S**cript **O**bject **N**otation）
是一种由**Douglas Crockford**构想和设计、轻量级的**数据交换语言**
该语言以易于让人阅读的文字为基础，用来传输由属性值或者序列性的值组成的数据对象。

- Douglas和Brandon互相不爽...
- Douglas抄JS写了个JSON
- Douglas写了本蝴蝶书告诉我们JS哪里哪里很毒瘤。明着diss...

## I.JSON vs JS

- JSON 没有抄 function 和 undefined
- JSON 的字符串首尾必须是 ""
- JSON 对象：{"name":"Oracle"} JS 对象： {name: 'Oracle'}

|JS|JSON|
|:---:|:---:|
|undefined|没有|
|null|null|
|['a','b']|["a","b"]|
|function fn(){}|没有|
|{name: 'Oracle'}|{"name":"Oracle"}|
|'Oracle'|"Oracle"|
|var a = {};a.self = a|搞不定（没有变量这个东西）|
|`{__proto__}`|没有原型链|

## II.为什么用JSON

```
//服务器
else if (path === '/xxx'){
        response.statusCode = 200
        response.setHeader('Content-type', 'text/xml;charset=utf-8')
        response.write(`
        {
            "note":{
                "to": "James Raynor"
                "from": "Sarah Kerrigan"
                "heading": "Message"
                "body": "For Im the queen of blades.Vengeance shall be mine."
            }
        }
        `)//返回一个字符串，这个字符串，凑巧刚好符合JSON对象语法
        // 这不是对象这不是对象这不是对象
        response.end()
    }
```
tigongde
tigongde
```
let string = request.responseText       //把JSON字符串放进容器
let object = Window.JSON.parse(string)      //这个 JSON.parse 是浏览器提供的

//把符合JSON语法的字符串，转换成JS中对应的值
```

这时候，前端希望用和 JS 比较像的 JSON ，而放弃使用 XML 了

# 3.同源策略与CORS跨域
## I.同源策略
只有 域名+端口+协议 一模一样才允许发 AJAX 请求

1. `http://baidu.com` 可以向 `http://www.baidu.com` 发 AJAX 请求吗？   ——NO
2. `http://baidu.com：80` 可以向 `http://baidu.com：81` 发 AJAX 请求吗？    ——NO

为什么？
你试试`http://www.12306.cn`和`http://12306.cn`是不是同一个网站

- 浏览器不能冒险呀，不能让你AJAX各种读用户数据呀。

浏览器必须保证：
- 只有 域名+端口+域名 一模一样才允许发 AJAX 请求

## II.CORS跨域
**C**ross-**O**rigin **R**esource **S**haring
跨          站         资源          共享

除了JSONP还有个别的方法
CORS可以：告诉浏览器，我们俩是兄弟呀，别阻止他。


给你要访问的网站的后端打个电话商量一下。让他在相应接口加一条：

```
response.setHeader('Access-Control-Allow-Origin', '你想允许哪个域名+端口+协议')
```

你们就可以愉快的玩耍了

### 为什么要用CORS
因为 `JSONP` 不能发 `POST` 呀


