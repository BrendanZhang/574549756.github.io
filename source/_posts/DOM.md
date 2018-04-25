---
title: DOM
date: 2018-04-25 19:02:01
tags: DOM
---

# 1.DOM是什么

Document Object Model
XML文档
把文档变成对象的一种模型

## I.DOM标准
`Element`对象：`body` `head` `meta` `title` `script` `h1` `h2` `p`这些都是`Element`对象
`Text`对象专门指文本：`span` 之类的
`Document`对象：`html`因为它是用`Document`构造出来的
`Comment`对象：注释

而他们原型链的顶端叫做`Node`
就像我们熟知的`Object.prorotype`

每一个标签都有它相应的构造函数，浏览器看到标签就用对应的构造函数给它构造出一个对应的内存中的对象。

           构造函数
页面中节点  ========>  对象

# 2.Node的接口
就像讨论Object.prototype一样
需要注意`Node`也是一种`object`

因为超级多，记几个单词然后：
`child`/`children`/`parent`
`node`
`first`/`last`
`next`/`previous`
`sibling`/`siblings`
`type`
`value`/`text`/`content`
`inner`/`outer`
`element`
互相组合

## I.childNodes
所有的子节点（不是子元素）
所以一旦有回车，就会得到一个text

所以想要所有标签请使用`children`

`nextSibling`是下一个兄弟节点（有回车也会返回text）

`nextElementSibling`才是下一个兄弟标签（就是兼容性不好）

导致这一堆奇怪问题的原因:`DOM`不是设计来给`HTML`用的，是给`XML`用的，所以不是很配套。

## II.常用接口

|接口|作用|备注|
|:---:|:---:|:---:|
|childNodes|所有子节点||
|firstChild|第一个子节点|
|innerText|内容文本|IE加的那点料，在小于等于IE11中修改`innerText`会移除当前元素的子节点，且永久性破坏所有后代文本节点|
|lastChild|最后一个子节点|
|nextSibling|下一个节点|
|nodeName|节点名称|（获取的是大写除了svg）|
|nodeType|节点类型|1:element 3:text 8:comment 9:document 10:DOCTYPE 11:DocumentFragment|
|nodeValue|value是一个包含当前节点的值的字符串（如果有的话）。||
|outerText|是一个非标准的属性。作为一个获得器，它返回与Node.innerText一致的值|作为一个设置器，它将删除当前节点并将其替换为给定的文本。|
|ownerDocument|会返回当前节点的顶层的 document 对象|返回祖先|
|parentElement|父级元素||
|parentNode|父级节点|和上面那位作用不一样吗？|
|previousSibling|上一个兄弟节点||
|textContent|内容文本|FF和Opera加的那点料,会获取所有元素内容，包括`<script>`和`<style>`|

# 3.方法
|方法|作用|
|:----:|:----:|
|appendChild()|将一个节点添加到指定父节点的子节点列表末尾。|
|cloneNode()|拷贝节点，可选深拷贝或浅拷贝|
|contains()|判断传入的节点是否为该节点的后代节点。|
|hasChildNodes()|一个元素是否有子节点|
|insertBefore()|把一个东西插入一个东西的前面|
|isEqualNode()|两个节点是否相等|
|isSameNode()|两个节点是否是同一个节点`===`|
|removeChild()|（从页面）干掉辣个子节点（但是他还在内存里）|
|replaceChild()|替换子节点 （被替换的还在内存里）|
|normalize()|常规化|

## I.cloneNode()

`var dupNode = node.cloneNode(deep)`

deep是可选参数，是否采用深拷贝。如果为true，则该节点的所有后代节点也都会被克隆，如果为false，则只克隆该节点本身

### 深拷贝和浅拷贝

深拷贝和浅拷贝只针对Object，Array这种复杂类型
简单来说，浅复制只复制一层对象的属性，而深复制则递归复制了所有层级。

## II.normalize()

```
var wrapper = document.createElement("div");

wrapper.appendChild(document.createTextNode("part 1")); //俩都是文本
wrapper.appentChild(document.createTextNode("part 2"));

//这时候 wrapper.childNodes.length === 2
//wrapper.childNodes[0].textContent === "part 1"
//wrapper.childNodes[1].textContent === "part 2"

wrapper.normalize();

//常规化以后 wrapper.childNodes.length === 1
wrapper.childNodes[0].textContent === "Part 1 Part 2"
```

使这个 拆成两部分的文本合在一起了。（把不合常规的常规化）

## III.学习方法

1.他写的什么就是什么意思，看懂单词就明白它是干嘛的了
2.看懂单词还是不知道怎么用？查MDN吧...

把该记的特殊的记住就可以了。

# 4.Document接口

|接口|作用|备注|
|:---:|:---:|:---:|
|anchors|获取页面`<a>`标签|`H5已弃用`。由于向后兼容的原因，该属性只返回那些拥有`name`属性的`a`元素，而不是拥有`id`属性的`a`元素|
|body|获取`<body>`元素||
|characterSet|就是`char`（字符）字符编码|`document.characterSet`看它的字符编码是什么|
|childElementCount|返回一个无符号长整型数字，表示给定元素的子元素数|
|children|获取子元素咯|`document`是`html`的父级哟，但`html`还是根元素|
|doctype|就是`!DOCTYPE`协议咯|
|documentElement|返回文档对象的根元素|`HTML`文档的<html>元素|
|domain|域名||
|fullscreen||
|head|头部|
|hidden|是否被隐藏？|返回布尔值|
|images|获取页面中所有`<img>`标签|
|links|获取页面中所有`<a>`标签|
|location|返回一个 Location 对象|包含有文档的 URL 相关的信息，并提供了改变该 URL 和加载其他 URL 的方法。|
|onxxxxxxxx|当xxx时的事件监听|`onclick` `onmousemove` `onmousedown` 之类的|
|origin|源||
|plugins|检测用户有没有开启插件||
|readyState|检测用户是否是否下载完毕||
|referrer|引荐者|发请求的时候，浏览器要告诉服务器，它是通过什么渠道进来的。服务器可以通过`referrer`来拒绝为其他网站提供服务|
|scripts|获取所有`script`标签|
|scrollingElement|正在滚动的元素|
|styleSheets|获取所有CSS||
|title|获取所有`<title>`|
|visibilityState|获取页面是否被显示（当前标签是否被激活）|返回布尔值|

## I.方法
|方法|作用|备注|
|:---:|:---:|:---:|
|close()|关闭文档|关闭向当前文档的数据写入，想要打开要使用document.open()|
|createDocumentFragment()|创建一个DocumentFragment||
|createElement()|创建由tagName 指定的HTML元素||
|createTextNode()|创建一个文本节点||
|execCommand()|执行一个命令|允许命令操纵可编辑区域的内容，主要用于富文本编辑器，相关内容查mdn|
|exitFullscreen()|退出全屏||
|getElementById()|通过`id`获取元素||
|getElementsByClassName()|通过`class`名获取元素||
|getElementsByName()|通过`name`属性获取元素||
|getElementsByTagName|通过`标签名`获取元素||
|getSelection()|获取用户选中的文本||
|hasFocus()|用户是否`focus`到当前页面||
|open()|和`close`对应||
|querySelector()|通过`选择器（css）`获取元素|抄jQuery的|
|querySelectorALL()|通过`选择器（css）`获取元素（返回所有元素）||
|registerElement()|在浏览器注册一个新的 自定义元素 ，返回一个该元素的构造函数。|用的并不多...建议使用：customElements.define（）|
|write()|写文本||
|writeln()|写一行文本||


### i.close()

```
<body>
hello
    <script>
        documetn.write(1)
        document.write(2)
        setTimeout(()=>{
            document.write(3)
        },3000)
    </script>
</body>
```

`document => open => write => close => open`

每次在`script`执行完以后页面会关闭，如果有延时性的`write`，就会把页面冲掉
上面代码块中首先有`hello`和`1` `2`这时候文档close
但是文档`close`了之后写了`3`
所以就会把页面冲掉

所以在写write的时候要谨慎设置延时和异步 

# 5.Element接口
最熟悉的`classList.add()`
而且`Element`也可以`querySelector()`的
可以`div.querySelector()`

### i.innerHTML和innerText

```
<body>
    <input type="text" id="input1"> <button id=x>写入页面</button>
    <div id="output"></div>
</body>

x.onclick = function(){
    output.innerHTML = input1.value
}

/*x.onclick = function(){
    output.innerText = input1.value
}*/
```

innerHTML可以识别写入页面的代码`<b></b>`就会加粗`<i></i>`就会变斜
`<script></script>`怎么搞
那麻烦了，用户真拿这个输入框把`cookie`爬了怎么办。
所以还是很危险的
他会把用户写的标签，真的当做开发者写的。

