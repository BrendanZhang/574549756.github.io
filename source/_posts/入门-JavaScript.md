---
title: 入门-JavaScript
date: 2018-04-02 22:50:06
tags: JavaScript
categories: JavaScript
---
Uncaught SyntextError: Unexpected tokken ]
没有被处理的语法错误： 不可预知的字符串 ]
which means：浏览器觉得这里不应该有一个中括号。

```
mainXXX.onkeypress = function(random){
 console.log('我发现你输入了一个键')
}
```

localStorage

```
localStorage.setItem('uuu', JSON.stringify(hash))//每次变化就存下来
```

存在浏览器的storage里面
`var hashInLocalStorage = JSON.parse(localStorage.getItem('uuu') || '')`
取出localStorage中uuu对应的hash

inline元素中间有回车本应该有个空隙
JavaScript生成的inline元素是没有空隙的
就会紧紧贴在一起

vh是指的视口高度（屏幕大小）`viewport height`
盖住当前元素（做到自适应）`background-size: cover;`

网站根目录`/favicon.ico`
访问网站的`logo`
有时候网站没在这里放icon，那只能用到`http://favicon.byi.pw/?url=相应网址`

`元素名.previousSibling`
获取元素名上一个元素

`.onerror`
发生错误以后执行