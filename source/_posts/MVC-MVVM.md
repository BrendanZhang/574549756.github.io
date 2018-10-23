---
title: MVC?MVVM!
date: 2018-06-30 22:40:50
tags: JS
categories: 框架
---

# 0.猜猜看 Vue 为什么叫 Vue

-   Vue 代替了 MVC 里的 View
-   Vue 这单词是法语

# 1.axios

-   Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。
-   就是个 AJAX 库

## I.axios 是什么

```
$.ajax({
    url: './xxx',
    method: 'post'
})

$.post('/xxx',data)
$.get('/xxx')
```

### i.axios 怎么用 AJAX 的？

```
axios.get('/user?ID=xxx')
    .then(function(response){
        console.log(response)
    })
    .catch(function(error){
        console.log(error)
    })

axios.post()
axios.put()
axios.patch()
axios.delete()

////////// 真的是基于 Promise //////////
```

-   比 jQuery.ajax 功能更多
-   除了 ajax 功能之外，就没有其他功能了（更专注）

### ii.还用 jQuery 吗？

-   AJAX 可以用 axios
-   DOM 操作可以用 Vue

## II.axios 怎么用

### i.interceptors

`interceptor n.拦截机;`
但是它可能不像它的名字那样直截了当。

```
axios.interceptors.response.use(function(response){
    let config = response.config
    let {method, url, data} = config

    let {config: {url,method,data}} = response
    // 这一行等于上面两行 (es6的技巧)

    return response
})
```

-   `axios.interceptors.response.use`
    -   在真正返回`response`之前拦截一下
-   执行一个函数，处理一下`response`
    -   再返回`response`

### ii.Object.assign(target,data)

-   `target`是修改目标
-   `data`是修改内容
-   可以执行链式操作
    -   `Object.assign(target,data1,data2)`
    -   如果有重复则`data2`会覆盖`data1`

# 2.Vue 的双向绑定

`<input v-model="text"/>`

-   `text`就会因用户输入的内容而映射到内存
-   且`text`也会因为内存中的`text`值而渲染到页面中

## I.那么 Vue 就是自动化的 MVC

-   `Vue`省去了渲染操作
-   `Vue`省去了`Control`的大量操作，通过操作数据来操作页面

## II.jQuery 是不是可以退休了

-   AJAX 操作可以用`axios`完成
-   DOM 操作在`Vue`下仅需要进行数据操作

# 3.MVVM

**Model-View-ViewMode**

要编写可维护的前端代码绝非易事。我们已经用 MVC 模式通过 koa 实现了后端数据、模板页面和控制器的分离，但是，对于前端来说，还不够。

-   Model: 数据模型层——数据
-   View: 视图模板层——用户界面
-   ViewMode： 视图模块层——取代了 MVC 的 Controller，传达视图和数据绑定通信；Model 中的数据状态
