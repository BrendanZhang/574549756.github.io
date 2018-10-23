---
title: Session、LocalStorage、Cache-Control
date: 2018-06-15 17:39:25
tags: HTTP
categories: HTTP
---

# 0.Session

## I.如何阻止用户篡改Cookie 

### Cookie
Cookie 是 session 的依赖

- 服务器通过`Set-Cookie`给客户端一串字符串
- 客户端每次访问相同域名的网页时，必须带上这段字符串
- 客户端要在一段时间内保存这个`Cookie`
- Cookie 默认在用户关闭页面后就失效，后台代码可以任意设置 `Cookie` 的过期时间
这家伙不占内存

### Session
一般来说，Session 是基于 Cookie 实现的

- 服务器通过`Cookie`给客户端一个`SessionId`（随机数）
- 客户端访问服务器的时候，服务器读取`SessionId`
- 服务器里的一小块内存（对象）保存了所有`session`
- 这块内存（哈希表）就是服务器上所有`session`
- 服务器就通过`SessionId`读取对应的用户信息（id、email）
- 以此获取用户的隐私信息

`sessionId`是个随机数，所以用户不能通过该随机数来获取其他用户的隐私信息。
**这样，`session`就可以阻止用户随便改Cookie**

缺点：占内存......
用户多了就占很大的内存。

**前端永远不要读/写cookie**
你有LocalStorage

# 1.LocalStorage
这是 HTML5 提供的 API
实质是一个 hash
session 是服务器上的 hash
LocalStorage 是浏览器上的 hash

1. LocalStorage 和 HTTP 无关
2. HTTP 不会带上 LocalStorage 的值
3. 只有相同域名的页面才能互相读取 LocalStorage（没有同源那么严格）
4. 每个域名 LocalStorage 最大存储量 5Mb 左右 （每个浏览器不一样）
5. 常用场景：记录没有提示过的用户（没有用的信息，不能记录密码）
6. LocalStorage 理论上永久有效，除非用户清理缓存（cookie及其他网站数据）
## API

|API|作用|
|:---:|:---:|
|clear|清除所有|
|**getItem**|取值用的|
|**removeItem**|删除相应LocalStorage|
|**setItem**|只能存string|

## SessionStorage（会话存储）
和LocalStorage基本一样，唯一不一样的是最后一点。

1. SessionStorage 和 HTTP 无关
2. HTTP 不会带上 SessionStorage 的值
3. 只有相同域名的页面才能互相读取 SessionStorage
4. 每个域名 SessionStorage 最大存储量 5Mb 左右 （每个浏览器不一样）
5. **SessionStorage 在用户关闭页面（Session结束[会话结束]）后就失效**

# 2.缓存控制Cache-Control
在请求头中加入`response.setHeader('Cache-Control','max-age=30')`
请求缓存控制，30秒内不再请求
可以让浏览器在重复请求的时候调用缓存
加快打开速度
**web优化相关**
## I.更新缓存
- js 和 css 一般设置 10 年缓存
- 服务器要更新 js 和 css 的时候怎么办
- 但是，只有**相同**的**url**才会利用之前的缓存
- 所以只要稍微让 url 不一样就可以
- 加一个查询参数就可以了
- `./css/default.css?v=2/`
- 加了点点东西，但是 url 变了，所以会不使用之前的缓存。
- 重新请求

## II.为什么首页不能设置Cache-Control
- chrome不允许在设置首页缓存
- 如果首页设置缓存
- 页面一旦更新，用户无法获取最新版本
- 如果你设置一天或者几个小时，巨大风险

# 3.Expires
如果设置了 `max-age` 或者 `s-max-age` 指令的`Cache-Control`响应头，那么`Expires`头就会被忽略

`Cache-Control`是新的头
`Expires`是以前用的。

## I.语法

```
response.SetHeaders('Expires', 'Sat, 16 Jun 2018 20:02:34 GMT')
```

Expires 接一个 GMT 时间。
表示缓存的过期时间。
所以他和`Cache-Control`的区别是
前者规定过期日期
后者规定过期时间

有没有一种有`效期至`和`保质期`的感觉

- 但是`有效期至`如果写错了岂不是巨大风险
- 所以我们有了`保质期`
- `Cache-Control`从现在开始计时 

# 4.ETag
这是用来给文件一个版本号的东东。

## I.MD5
讯息摘要演算法
拿来校验文件的

- 他把文件变成字符串
- 如果内容改变了
- 那么这个字符串和原来的字符串差别很大
- 改变的差异越小，那么字符串差异就越大

node.js 有 md5 的库

## II.Etag如何工作

```
let fileMd5 = md5(string)
response.setHeader('ETag', fileMd5)        
if (request.headers['if-none-match'] === fileMd5) {
    //没有响应体，只有响应头
    response.statusCode = 304
} else {
    //有响应体
    response.write(string)
}
response.end()
```

- 这时候，请求头里会多出一个`If-None-Match: 相应的md5`
- 如果这个`If-None-Match`的值和`md5`匹配
- 那么说明不需要重新下载
- 返回 304 表达：没改过
- 如果有变化，那么再响应

### i.使用场景

- 帖子更新
- 为每个帖子页面生成唯一的ETag，在其未改变时，查看话题属性比较ETag就能避免刷新帖子。

## III.和缓存的区别
缓存：
- 直接不请求
- 从内存里拿

ETag:
- 正常发请求
- 匹配 MD5
- 如果匹配，则不下载(响应体为空)response.setHeader('Cache-Control','max-age=30')

### i.缓存和ETag哪个更优？
理论上，缓存更好
因为节省了请求时间，更加迅速

# 5.Last-Modified
- Last-Modified是一个响应头
- 其中包含源头服务器认定的资源做出修改的日期及时间
- 它通常被用作一个验证器来判断接收到的或者存储的资源是否彼此一致
- 由于精确度比 `ETag` 要低，所以这是一个备用机制
- 包含有  If-Modified-Since 或 If-Unmodified-Since 首部的条件请求会使用这个字段。

`response.SetHeaders('Last-Modified', 'Sat, 16 Jun 2018 20:02:34 GMT')`

- 服务端发给客户端一个最后修改的时间
- 客户端匹配最后修改时间
- 然后请求

## I.If-Modified-Since
- 条件式请求头
- 服务器只在所请求的资源在给定的日期时间之后对内容进行过修改的情况下才会将资源返回
- 状态码为 200
- 如果请求的资源从那时起未经修改
- 那么返回一个不带有消息主体的 304 响应
- 而在 Last-Modified 首部中会带有上次修改时间。

**如果和`If-None-Match`同时出现，则会被忽略**

## II.If-Unmodified-Since
- 条件式请求头
- 只有当资源在指定的时间之后没有进行过修改的情况下，服务器才会返回请求的资源
- 如果所请求的资源在指定的时间之后发生了修改，那么会返回 412 (Precondition Failed) 错误