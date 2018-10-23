---
title: jQuery-始
date: 2018-04-26 19:04:47
tags: JS
categories: JavaScript
---
别看jQuery mobile

# 1.如何自己实现一个jQuery

## I.找兄弟
```
<body>
    <ul>
        <li id="item1">选项1</li>
        <li id="item2">选项2</li>
        <li id="item3">选项3</li>
        <li id="item4">选项4</li>
        <li id="item5">选项5</li>
    </ul>
    <script>
        function getSiblings(node){
            var allChildren = item3.parentNode.children
            var array = {length: 0}
            for(let i=0; i<allChildren.length; i++){
                if(allChildren[i]  !== node){
                array[array.length] = allChildren[i]
                array.length += 1
                }
            }
            return array
        }
        getSiblings(item3)  //找兄弟（不包括自己）就完成了
    </script>
</body>
```

## II.改class

```
        function addClass(node, classes) {
            for (let key in classes) {
                var value = classes[key]
                if (value) {
                    item3.classList.add(key)
                } else {
                    item3.classList.remove(key)
                }
            }
        }
        addClass(item3, { a: true, b: false, c: true })     //改class就完成了
```

优化一下？

```
        function addClass(node, classes) {
            for (let key in classes) {
                var value = classes[key]
                var methodName = value ? 'add' : 'remove'
                node.classList[methodName](key)
            }
        }
        addClass(item3, { a: true, b: false, c: true })     //改class就完成了
```

## III.如何优化代码

### i.如果出现类似的代码，就存在优化的可能

## IV.命名空间
辛辛苦苦封装的函数，得找个方法调用吧
所以找一个别人没取过的名字
然后放进去，既避免了覆盖变量，又可以方便调用

```
window.oracleDOM = {}
oracleDOM.getSiblings = function addClass(node, classes) {
    for (let key in classes) {
        var value = classes[key]
        if (value) {
            item3.classList.add(key)
        } else {
            item3.classList.remove(key)
        }
    }
}

oracleDOM.addClass = function (node, classes) {
    for (let key in classes) {
        var value = classes[key]
        var methodName = value ? 'add' : 'remove'
        node.classList[methodName](key)
    }
}

oracleDOM.getSibling(item3)
oracleDOM.addClass(item3,['a','b','c'])
```

### i.还是感觉调用很麻烦？
加到原型链里面去

#### 找兄弟：

```
Node.prorotype.getSiblings = function getSiblings(node){
    var allChildren = this.parentNode.children
    var array = {length: 0}
    for(let i=0; i<allChildren.length; i++){
        if(allChildren[i]  !== this){
        array[array.length] = allChildren[i]
        array.length += 1
        }
    }
    return array
}
item3.getSiblings()
```

这里面把node替换成this，使node作为第一个参数传进去。
所以item3.getSiblings()可以将item3作为第一个参数传进去

#### 加Class：

```
Node.prototype.addClass = function (classes) {
    for (let key in classes) {
        var value = classes[key]
        var methodName = value ? 'add' : 'remove'
        this.classList[methodName](key)
    }
}

item3.addClass(['a','b','c'])
```

第一个参数node替换为this，在第五行的`node.classList`由调用时开头的`item3`传入

#### 什么？看不懂这个this？

```
item3.getSiblings.call(item3)
//相当于 item3.getSiblings()
item3.addClass.call(item3, ['a','b','c'])
//相当于 item3.addClass(['a','b','c'])
```

用call把第一个参数写出来是不是就清楚了
**不吃糖，好理解，吃糖，写的爽。**

### ii.覆盖原型是不是有点不太好？

#### 通过jQuery这个容器来封装他？


```
window.jQuery = function(node){         //名字改成jQuery
    return{
        getSiblings: function(){
            var allChildren = node.parentNode.children      //这时候node不是this了
            var array = {length: 0}                             //因为现在用的是node2
            for(let i=0; i<allChildren.length; i++){
                if(allChildren[i]  !== node){
                    array[array.length] = allChildren[i]
                    array.length += 1
                }
            }
            return array
        },
        addClass: function(classes){
            for (let key in classes) {
            var value = classes[key]
            var methodName = value ? 'add' : 'remove'
            node.classList[methodName](key)             //这里也要改成node了
            } 
        }
    }
}

var node2 = jQuery(item3)
node2.getSiblings()
node2.addClass(['a','b','c'])
```

所以jQuery框架就是这个思路，封装函数，随时调用，返回新对象。

# 2.jQuery其实还要厉害一点

## I.功能还是多

### i.不但能传节点，还能传别的

```
window.jQuery = function(nodeOrSelector){
    let node
    if(typeof nodeOrSelector === 'string'){             //让传入参数还能是个选择器
        node = document.querySelector(nodeOrSelector)
    }else{                                                  //内容审查
        node = nodeOrSelector
    }

    return{
        getSiblings: function(){
            var allChildren = node.parentNode.children  
            var array = {length: 0}
            for(let i=0; i<allChildren.length; i++){
                if(allChildren[i]  !== node){
                    array[array.length] = allChildren[i]
                    array.length += 1
                }
            }
            return array
        },
        addClass: function(classes){
            for (let key in classes) {
                var value = classes[key]
                var methodName = value ? 'add' : 'remove'
                node.classList[methodName](key)         //这里node用到了闭包哟
            } 
        }
    }
}

var node2 = jQuery('#item3')            //传入一个选择器
node2.getSiblings()
node2.addClass(['red','b','c'])             //改这个选择器对应标签的class
```

#### 这期间发生了什么？

使用`jQuery`调用字符串`#item3`
内容审查发现他是字符串
找到相应节点
`node`作为容器保存这个节点

`jQuery`返回一个`对象`
对象有两个key：`getSiblings`和`addClass`

调用`getSiblings`
调用`addClass`
发现`addClass`获取了一个数组（`['red','b','c']`）以后遍历这个数组
之后不停地在`node`上添加classList
这个`node`就是刚才容器保存的节点

#### 不信你写个别的选择器试试？

```
var node2 = jQuery('ul > li:nth-child(3)')            //传入一个选择器
node2.getSiblings()
node2.addClass(['blue','b','c'])   
```

### ii.我想通过选择器选好几个怎么办？

那可能要变了个大样了

```
window.jQuery = function(nodeOrSelector){
    let nodes = {}
    if(typeof nodeOrSelector === 'string'){
        let temp = document.querySelectorAll(nodeOrSelector)    //希望得到一个伪数组
        for(let i=0; i<temp.length; i++){                    //不想要NodeList的属性
            nodes[i] = temp[i]                            //遍历容器一个一个加进去
        }
        nodes.length = temp.length
    }else if(nodeOrSelector instanceof Node){               //考虑只有一个节点的情况
        nodes = {0:nodeOrSelector, length: 1}
    }

    nodes.addClass = function(classes){                  //调用addClass
        for (let key in classes) {                      //遍历class
            var value = classes[key]
            var methodName = value ? 'add' : 'remove'
            for(let i=0; i<nodes.length; i++){
                nodes[i].classList[methodName](key)      //逐步的放在伪数组的每一项里
            }
        } 
    }
    nodes.getText = function(){                         //加个功能，获取文本
        var texts = []
        for(let i=0; i< nodes.length; i++){               //遍历后塞进去
            texts.push(nodes[i].textContent)
        }
        return texts                                    //返回文本
    }
    nodes.setText = function(text){                     //再加个功能，设置文本
        for(let i=0; i<nodes.length; i++){
            nodes[i].textContent = text          //把传进去的参数text赋予textContent
        }
    }
    //////////////////jQuery不喜欢写get和set所以合并成text/////////////////////
    
    nodes.text = function(text){
        if(text === undefined){                         //如果没传参数
            var texts = []                            //说明是想获取text
            for(let i=0; i< nodes.length; i++){
                texts.push(nodes[i].textContent)
            }
            return texts
        }else{                                          //给了参数
            for(let i=0; i<nodes.length; i++){        //说明是想设置text
                nodes[i].textContent = text
            }
        }
    }

    return nodes
}

var node2 = jQuery('ul > li')
node2.addClass(['blue'])
var text = node2.text()     //不给参数 === 获取
node2.text('hi')                //给了参数 === 设置

```

# 3.看看jQuery的文档吧

`<script src="//code.jquery.com/jquery-2.1.1.min.js"></script>`
引入jQuery的库，就可以调用它的API了

## I.API
[超多API](http://api.jquery.com)

### i.可以几个连着用

x.onclick = function(){
    nodes.removeClass('red').addClass('green')
}

让大家喜爱的**链式操作**


## II.jQuery厉害在哪里

1.兼容性好，1.7兼容到IE6，现在放弃兼容了...
2.还有动画、AJAX等模块，DOM操作只是一小部分
3.功能强大，功能丰富
4.jQuery使用了`prototype`还有需要了解`new`

## III.$()的几种用法

### i.$(object)
传入一个object，将该对象封装到jQuery对象中并返回

### ii.$(callback)
传进去参数是函数的时候，在document对象上绑定一个ready事件监听函数，当DOM结构加载完成的时候执行

```
$(function(){
})
//以上代码和下面的效果是一样的
$(document).ready(function(){
    ...//代码
})
```

### iii.$(jQuery object)
传进去的参数是一个jQuery对象的时候，则创建该jQuery对象的一个副本并返回。副本与传入jQuery对象的引用完全相同的元素

### iv.$()
什么都不传，返回一个空jQuery对象，属性length: 0 
可以用来复用jQuery对象：
创建空jQuery对象，需要时先手动修改其中元素，再调用jQuery方法。避免重复创建jQuery对象。
