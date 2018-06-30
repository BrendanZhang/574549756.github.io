---
title: MVC?MVVM!
date: 2018-06-30 22:40:50
tags: JS
---

# 0.猜猜看 Vue 为什么叫 Vue

-   Vue 代替了 MVC 里的 View
-   Vue 这单词是法语

# 1.axios 是什么

-   Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。
-   就是个 AJAX 库

## 1.我们用 jQuery 的时候这么用 AJAX

```
$.ajax({
    url: './xxx',
    method: 'post'
})

$.post('/xxx',data)
$.get('/xxx')
```

## 2.axios 怎么用 AJAX 的？

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

## 3.还用 jQuery 吗？

-   AJAX 可以用 axios
-   DOM 操作可以用 Vue
 