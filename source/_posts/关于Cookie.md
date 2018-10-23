---
title: 关于Cookie
date: 2018-06-07 18:38:15
tags: HTTP
categories: HTTP
---
# 0.前置

- Cookie Session Cache-Control 这三个是响应头，响应头，响应头。

# 1.cookie
## I.定义
### i.维基说的
- Cookie（复数形态Cookies），中文名称为“小型文本文件”或“小甜饼”，指某些网站为了辨别用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。
- 由网景公司的前雇员卢·蒙特利在1993年3月发明。最初定义于RFC 2109。
- 目前使用最广泛的 Cookie标准却不是RFC中定义的任何一个，而是在网景公司制定的标准上进行扩展后的产物。

### ii.简化一点
1. Cookie 是浏览器访问服务器后，服务器传给浏览器的一段数据。
2. 浏览器需要保存这段数据，不得轻易删除。
3. 此后每次浏览器访问该服务器，都必须带上这段数据。

## II.作用
### i.识别用户身份
- A用户 注册登陆了 `a.com`， `a.com` 的服务器返回给 A用户 一段数据，包含用户名密码各种东西
- B用户 打开 `a.com` ， `a.com` 的服务器看了一眼数据库发现没有 B用户 的数据，就让 B用户 去注册登录，然后返回给 B用户 它的账户信息
- 这样，`a.com` 就可以清楚的区分 A用户 和 B用户 了。
### ii.记录历史
- 假设一个用户进入一个购物网站，加了两件商品到购物车
- 这时 JS 改写cookie，将这两件商品记录在下来(假设`[{"userId":"Oracle","stuff":"2"}]`)
- 假设用户摇摆不定，过了两三天
- 依然可以看见这两件商品躺在购物车里，因此浏览器不会无缘无故删除这个 Cookie

## III.特点

1. 服务器通过 Set-Cookie 响应头设置 Cookie
2. 浏览器得到 Cookie 之后，每次请求都要带上 Cookie
3. 服务器读取 Cookie 就知道登录用户的信息(email)

## IV.问题

1. 我在 Chrome 登录了，用 Safari 访问， Safari 会带上 Cookie 吗     
    // No

2. Cookie 存在哪        
    // Windows 存在 C 盘的文件里

3. Cookie 这张票能作假吗        
    // 用户在 Application 里随便改
    // document.cookie 乱改(HttpOnly下不可以)

4. Cookie 存在有效期吗
    // 默认有效期20分钟左右
    // 后端可以强制设置有效期
    [具体要看这个](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie)

5. Cookie 会随着域名分组吗
    // 会，Cookie按域名分组，一个域名只能带上自己域名的Cookie

## V.cookie登录的相关流程

```
                      Server                   users
                        |                        | 
                        |         post           | 打开 sign-up 注册
                        |      <===========      |
               写数据库  ||     email pw1 pw2     || 
            <===========|                        | 
              email pw  |         注册成功        ||
                        |      ===========>      |
                        |                        |
                        |          post          |  打开 sign-in 登入
                        |      <===========      |
                        |        email pw        |
                        |                        |
                        |                        |
                        |      ===========>      |
                        |     SetCookie,email    |
                        |                        |
                        |       带上cookie       || 打开首页
                        |      <===========      |
                        |          GET           |
              读cookie  ||                       ||
      email: 1@xxx.com  |                        |
    user=find-by email  |                        |
 user{email,pw,birthD}  |                        |
 index.html(填入对应pw)  ||                       ||
                        ↓          响应          ↓↓
                        ↓      -----------→      ↓
```

**这就是cookie的工作流程**

# Cookie 的那些小故事
## Cookie 的分类
### 默认级别
- 指的是没有设置有效时间的Cookie
- 默认的情况下只要关闭了浏览器，Cookie也会被销毁
- Cookie存在于浏览器的内存中，当关闭了浏览器Cookie就销毁了
### 持久级别
- 指的是有有效时间的Cookie
- 这种Cookie的内容不是保存在浏览器的内存中，将Cookie的内容保存（持久化）到硬盘上。
- 这个时候，关闭浏览器，再次打开浏览器会加载硬盘上的文件，从而Cookie中的数据就不会丢失。

## Cookie 的数据大小
浏览器存放的Cookie的大小和个数是有限制的。

- 浏览器一般只允许存放300个Cookie
- 每个站点最多可以存放20个Cookie
- 老版本浏览器中，每个Cookie的大小限制为4KB
## Cookie操作
- ``

## 其他的小Tip

- 一个Cookie只用标识一种信息，至少含有一个标识该信息的名称和值。
- 一个web站点可以给一个浏览器发送多个Cookie。一个web浏览器可以存储多个web站点的Cookie
- 需要手动删除持久性Cookie，可以将Cookie的有效时长设置为0.必须注意：删除Cookie时候，path必须一致，否则无法删除

**常用API**

|API|作用|
|:---:|:---:|
|cookie.setMaxAge(30)|设置最大生命周期。秒为单位，为0时表示立即删除该cookie，负数表示不存储该cookie|
|response.addCookie()|增加cookie(写回到浏览器),参数为cookie的名字|
|encodeURIComponent()|用它可以使cookie的值不包含任何逗号分号和空格|
|decodeURIComponent()|可以用来识别邮箱里的@符号|