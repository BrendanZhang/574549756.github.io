---
title: JavaScript-记了两个API
date: 2018-04-16 21:28:55
tags: JS
---

# 1.关于JS找兄弟

```
    <script>
        setTimeout(function(){
                siteWelcome.classList.remove('active')
        },3000)

        window.onscroll = function(){
            if(window.scrollY > 0){
                topNavBar.classList.add('sticky')
            }else{
                topNavBar.classList.remove('sticky')                
            }
        }
        let aTags = document.getElementsByClassName('menuTigger')
        for(let i=0; i<aTags.length; i++){
            aTags[i].onmouseenter = function(x){
                let a = x.currentTarget
                let brother = a.nextSibling             //这种找兄弟...真的毛病多。
                while(brother.tagName !== 'UL'){   //nodeType去查文档，表达了不同元素节点。 1是元素节点 3是文字 PS:为什么大写UL，因为brother.tagName会返回一个大写的UL。
                    brother = brother.nextSibling    //递归找节点，不是节点继续找。
                }
                brother.classList.add('active')
            }
            aTags[i].onmouseleave = function(x){
                let a = x.currentTarget
                let brother = a.nextSibling
                while(brother.tagName !== 'UL'){
                    brother = brother.nextSibling
                }
                brother.classList.remove('active')
            }
        }
    </script>
```


# 2.关于不找兄弟直接监听父级元素

```
        let liTags = document.getElementsByClassName('menuTigger')
        for(let i=0; i<liTags.length; i++){
            liTags[i].onmouseenter = function(x){
                let li = x.currentTarget
                let brother = li.getElementsByTagName('ul')[0]
                brother.classList.add('active')
            }
            liTags[i].onmouseleave = function(x){
                let li = x.currentTarget
                let brother = li.getElementsByTagName('ul')[0]
                brother.classList.remove('active')
            }
        }
```

# 3.既然a和ul都要active，那我为什么不把他们的父元素active呢？

```
        let liTags = document.getElementsByClassName('menuTigger')
        for(let i=0; i<liTags.length; i++){
            liTags[i].onmouseenter = function(x){
                x.currentTarget.classList.add('active')
            }
            liTags[i].onmouseleave = function(x){
                x.currentTarget.classList.remove('active')            
            }
        }
```

# 4.不想每个都加.menuTigger那么我们就加个选择器吧

```
        let liTags = document.querySelectorAll('nav.menu > ul > li')
        for(let i=0; i<liTags.length; i++){
            liTags[i].onmouseenter = function(x){
                x.currentTarget.classList.add('active')
            }
            liTags[i].onmouseleave = function(x){
                x.currentTarget.classList.remove('active')            
            }
        }
```

给nav一个.menu的class然后给他一个选择器，其中`querySelectorALL`就可以啦

# 5.关于调整锚点

```
        let aTags = document.querySelectorAll('nav.menu > ul > li > a')
        for(let i = 0; i<aTags.length; i++){
            aTags[i].onclick = function(x){
                x.preventDefault()          //阻止默认动作
                let a = x.currentTarget
                a.getAttribute('href')   //用户写什么，打什么。不像a.href是带http协议的。
                console.log(a.getAttribute('href'))
            }
        }
```

## 需要获取div距离顶部的距离
`getBoundingClientRect`这个api可以返回一组矩形集合（数组）
一组用于描述边框的只读属性（left top right bottom）单位px
除了width和heigth外的属性都相对于视口左上角位置而言。

计算边界矩形时，会考虑视口区域（或其他可滚动元素）内的滚动操作which means:
滚动的时候这个值会变，不是计算页面顶部而是计算视口顶部。
**不想让他变的话：**
给top和left加上当前滚动位置：`window.scrollX`和`window.scrollY`这样获取与当前滚动位置无关的常量值。
为兼容请使用：`window.pageXOffset`和`window.pageYOffset`

## 这个才是我们需要的
`element.offsetTop`

```
        let aTags = document.querySelectorAll('nav.menu > ul > li > a')
        for(let i = 0; i<aTags.length; i++){
            aTags[i].onclick = function(x){
                x.preventDefault()          //阻止默认动作
                let a = x.currentTarget
                let href = a.getAttribute('href') //'#siteAbout'
                let element = document.querySelector(href)
                let rect = element.getBoundingClientRect()
                let top = element.offsetTop
                window.scrollTo(0,top-80)
            }
        }
```

# 6.总结一下

```
setTimeout()        //设置延迟
window.onscroll //滚动时触发
window.scrollY      //获取滚动高度
document.querySelectorALL()   //接收一个选择器，获取选择器的所有元素
.onmouseenter   //鼠标进入元素的时候触发函数
.onmouseleave       //鼠标离开元素的时候触发函数
.preventDefault //调用它就不会有默认的动作了
.getAttribute()     //获取用户在元素上写的原文（不加HTTP协议）
document.querySelector()      //只会获取到第一个元素
.offsetTop      //获取元素距离页面顶部的像素数。
window.scrollTo(X,Y)    //滑动到某个位置X：左右 Y：上下。改成0就是不会划。
```
