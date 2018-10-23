---
title: 入门-HTML-II
date: 2018-03-23 22:13:53
tags: HTML
categories: HTML
---
# 1.常见HTML标签

## I. `<iframe>`标签
目前用的很少，但是有些遗留项目可能会碰到它：页面里嵌套页面。
### ①例子：jsbin
举个例子：`<iframe src="http://qq.com" frameborder="0"></iframe>`
frameborder=0?为了把阴影框删了，因为太难看了太难看了太难看了。
默认iframe宽100高50但是可以用CSS给它一个属性

```
<style>
  iframe{
  width: 100%;
  hight: 500PX; //为什么宽度可以100%，高度必须输像素呢？因为CSS规定的
  }
</style>
```

### ②还有些好玩的用法比如：

```
<body>
  <iframe name=xxx src="#" frameborder="0"></iframe>
  <a target=xxx href="http://qq.com">QQ</a>
  <a target=xxx href="http://baidu.com">百度</a>
</body>
```

厉害了呀，这样点击a标签就可以在iframe框里访问相应网页了。
![浏览效果](https://ws1.sinaimg.cn/large/005XzYe2gy1fpn80xrwomj30qo0g4wkr.jpg)

## II.`<a>`标签（HTTP GET 请求）

### ①关于target

i.`<a href="http://qq.com" target="_blank">qq</a>`
ii.`<a href="http://qq.com" target="_self">qq</a>`
iii.`<a href="http://qq.com" target="_parent">qq</a>`
iv.`<a href="http://qq.com" target="_top">qq</a>`

**这个target：规定了在哪里打开**
blank：新页面。
self：在自己身上打开。
parent：在他的父级打开，谁在他上面谁就是他爸咯。
top:顶层窗口，如果他爸爸有爸爸，那就在他爷爷那里打开。

### ②download属性
`<a href="http://qq.com" download>下载</a>`
在`Content-Type: text/html`的时候用↑
或者`Content-Type: application/octet-stream`就不用download了
下安装包的时候他很常见哦。

### ③href属性
`<a href="qq.com">QQ</a>`他会让你跳转到qq.com吗？
并不行，你前面没`http://`呀他会把qq.com看成是一个文件（还有文件叫.com呢？他不管他不管）。
你换成//试试？他会去找文件夹...
**//:你当前协议是什么协议，他就继承该协议。which means：无协议**
那怎么办嘛：**要加协议名称呀**

#### i.问题来了，那我不能写本地路径我怎么调试我的index.html呢？

方法一：上传github，用预览功能调试他。
方法二：下载一个小工具http-server
`npm i -g http-server`
他干吗用的呢？
还记得那年大明湖畔的nodejs服务器吗?没错就是他
运行的时候记得`http-server -c-1`不要缓存

#### ii.问题又来了，我写点别的行不行

可以，你加`#`或者`？`跟内容浏览器会自己识别你想表达的东西
但是`#`:不会发出请求。

### JavaScript伪协议
`<a href="javascript: alert(’我在搞伪协议‘)；">HiaHiaHia</a>`
这时候你点他，他会直接弹alert。这个伪协议不是url但是他会执行（这个可能会给同事留大坑。）
`<a href="javascript:；">HiaHiaHia</a>`
还可以这样做：点击以后让他不会跳转（很神奇是不是，但是它真的可能会有这种需求。他只是想让这个herf被占着。）
`<a href="">HiaHiaHia</a>`什么都不写？那他会刷新。
`<a href="#">HiaHiaHia</a>`写个锚？好了如果它前面有`<p>`那他会跳转一下。
所以只有伪协议让他什么都不做

## III.`<form>`标签（HTTP POST 请求）

```
<form action="users" method="post">
  <input type="text" name=”username“>
<input type="text" name=”password“>
  <input type="submit" value="提交">
</form>
```

一个典型的用户名提交窗口

### ①关于`action`
一个处理这个form信息的程序所在的URL。这个值可以被 `<button>` 或者 `<input>` 元素中的 formaction 属性重载（覆盖）。
你要在提交到哪里

### ②关于`method`
浏览器使用这种 HTTP 方式来提交 form. 可能的值有:
post: 指的是 HTTP POST 方法 ; 表单数据会包含在表单体内然后发送给服务器.
get: 指的是 HTTP GET 方法; 表单数据会附加在 action 属性的URI中，并以 '?' 作为分隔符, 然后这样得到的 URI 再发送给服务器. 当这样做（数据暴露在URI里面）没什么副作用，或者表单仅包含ASCII字符时，再使用这种方法吧。
这个值可以被 `<button>` 或者 `<input>` 元素中的 `formmethod` 属性重载（覆盖）。

**什么都不写，默认是GET，但是估计没人会这么无聊，你有`<a>`为何不用。**
在用**get**的时候，他会把数据传到查询参数里。
**post**会直接放在第四部分，**但是：**
你可以自己加呀`<form action="users?yyy=2" method="post">`他也可以有查询参数

### ③关于`input`

#### i.`<input>`
`type="submit"`类型是提交 `value="提交"`按钮上显示的是提交俩字
**如果表单里面没有提交按钮，那就无法提交form**
不可以有子元素

#### ii.`<button>`标签

如果一个`<form>`里面**只有一个按钮**，他的`type`没写，那么他会自动升级为**提交按钮**
可以有子元素

#### iii.`checkbox`
就是做一个能勾的选项`<input type="checkbox" id="xxx">但是点字没什么卵用`
<input type="checkbox" id="xxx">但是点字没什么卵用
`checkbox`也需要`name`不然无法传上去。
打钩上传，`name`对应上传name后面的内容。
checkbox可以有很多个，是不是感觉在做选择题？怎么判断正误呢？通过上传的`name`，每个选项有对应的`name`。

#### iv.`<label>`
神奇的标签
`<input type="checkbox" id="xxx"><label for="xxx">这样点字就有用了</label>`
可以让`<checkbox>`点字也有用。

---
`<label for="xxx">用户名</label><input type="text" name=”username“ id="xxx">`
`<label for="yyy">密码</label><input type="text" name=”password“ id="yyy">`
对应`<id>`和`<for>`可以点击用户名和密码就进入输入窗。**但是**老司机觉得起名字好麻烦呀。so：
`<label>用户名<input type="text" name=”username“ ></label>`
**一样的效果。只需要把他包起来`<label>`成为了`<input>`的父亲**

#### v.`radio`
**单选框**和checkbox对应。name相同的时候只能点一个。

```
<label><input name="难不难" type="radio" value="yes">Yes</label>
<label><input name="难不难" type="radio" value="yes">No</label>
```

难不难
<label><input name="难不难" type="radio" value="yes">Yes</label>
<label><input name="难不难" type="radio" value="yes">No</label>


### ④关于`name`

提交完了以后`name后面的就会被提交`
写`username`和`password`就会提交上去`username=blablabla&passowrd=blablablabla`
写`xxx`和`yyy`就会提交上去
`xxx=blablabla&yyy=blablabla`

`checkbox`也需要`name`

**为什么说HTTP不安全，因为提交上去是什么直接就显示出来了，如果有人监听那他就直接知道用户名和密码了。所以要用HTTPS，关于这个协议和端口后面再说。**

### ⑤关于`target`

**其实他和`<a>`是兄弟，用法一样一样的。**

### ⑥关于`<select>`

下拉列表

```
<select name="分组">
  <option value="">-</option>
  <option value="1">第一组</option>
  <option value="2">第二组</option>
  <option value="3" disabled>第三组</option>
  <option value="4" selected>第四组</option>
</select>
```

<select name="group">
  <option value="">-</option>
  <option value="1">第一组</option>
  <option value="2">第二组</option>
  <option value="3" disabled>第三组</option>
  <option value="4" selected>第四组</option>
</select>

选谁提交后就是`name的值=相应value`
**还有个属性叫做`multiple`**
加在`<select name="group" mutiple>`
加完了以后选择的时候按住`ctrl`就可以多选了。

### ⑦关于`<textarea>`
需要输入大段文字的时候使用
`<textarea name="text" cols="30" rows="10"></textarea>`
这时候它是可以随意拉动的，但是我们不希望他变大变小所以用CSS：
`<textarea style="resize:none; width: 200px;height: 100px;" name="text" cols="30" rows="10"></textarea>`
`style="resize:none"`让他不要乱动
`width: 200px;height: 100px;`规定他的宽高
在他不能乱动的时候可以用`cols`和`rows`来控制宽高（列、行）然而列不准，所以我们还是用CSS控制吧。

## IV.`<table>`标签
`head`头`body`身体`foot`脚  **他们三个顺序没有区别，他一定会自动按顺序展示**
`tr`行`td`内容
`colgroup`和`col`列宽
其中哪一个不写可不可以？可以，他会自己匀到剩下的部分。
全不写可不可以？那他会按你写的顺序识别。
很大程度上，他还是非常智能的。

**如何把表格的默认border取消？**

```
<style>
  table{
    border-collapse: collapse;
    }
</style>
```

table选择器`border-collapse`属性
改变表格默认border。