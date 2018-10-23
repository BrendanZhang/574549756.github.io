---
title: JavaScript-数据
date: 2018-04-10 12:17:16
tags: JS
categories: JavaScript
---
# 1.数据类型
### 种类&备注
七种数据类型：

```
number;
string;
boolean;
symbol;
undefined;
null;
object
```

没有array类也没有function类，因为他们都算object。
**永远不要说JS里一切都是对象**

## I.number
### i.整数和小数
`1`是一个整数
如何得到`1.1`这个数呢?
可以用`0.1`也可以用`.1`
### ii.科学计数法
`1.23e2`是合理的可识别的`123`
### iii.二进制
开头是`0b`的
### iv.八进制
开头是`0`的，后来ES5添加了0o11语法
### v.十六进制
开头是`0x`的
## II.string
### i.空字符串
`''`或者`""`空字符串，里面什么都没有
### ii.转义符
表达这个字符串里面只有一个`'`怎么办
`"'"`这么来
那么问题来了，我要表达这个字符串是`"'`怎么办，一个单引号一个双引号区分不开呀
这时候需要一个`\`反杠，`\`来告诉浏览器，这个引号不是拿来结束字符串的。
这就叫做，**转义符**
他不仅仅有这个作用还有：

|转义符|作用|Unicode|
|:---:|:---:|:---:|
|`\0`|null|（\u0000）|
|`\b`|后退键|（\u0008）|
|`\f`|换页符|（\u000C）|
|`\n`|换行符|（\u000A）|
|`\r`|回车键|（\u000D）|
|`\t`|制表符|（\u0009）|
|`\v`|垂直制表符|（\u000B）|
|`\'`|单引号|（\u0027）|
|`\"`|双引号|（\u0022）|
|`\\`|反斜杠|（\u005C）|

### iii.多行字符串
不是字符串里面有回车
而是我希望字符串有换行

```
var s = '12345 \
        67890'
```

就像命令行一样

```
var s2 = '12345' + '67890'
```

这样也可以
**但是方法一有个很鬼的问题**

```
var s = '12345 \     //反杠后面如果有一堆空格
67890'
```

反杠后面有一堆空格那么就热闹了，反杠会把第一个空格变成...字符串里的空格...
遭重了，很坑很坑。
所以最好用第二个方法了。

**既然这个这么坑，那JS要解决它呀**
所以在ES6里就有了这个符号`就是这个点

```
var s4 = `12345
67890`
```

他会记录里面的一切，包括回车
所以这就是11个字符`s4.length`是`11`
## III.boolean
### i.George Boole
数学家、哲学家，发明逻辑学。
为了纪念他，我们把`ture`和`false`两个值叫做布尔
`&&`与
`||`或
## IV.symbol
### i.是什么
ES6引入了新的数据类型Symbol，用于生成一个全局唯一的值。
### ii.怎么用
借用方方老师的例子
```
var race = {
  protoss: 'protoss', // 神族
  terran: 'terran', // 人族
  zerg: 'zerg' // 虫族
}

function createRole(type){
  if(type === race.protoss){选择神族兵种}
  else if(type === race.terran){选择人族兵种}
  else if(type === race.zerg){选择虫族兵种}
}
```

打星际选择兵种。race的键-值组合中，值显得并不重要。
那么值甚至可以乱敲只要他们三个种族的值不重复就可以。
那么Symbol可以替代对应的值

```
var race = {
  protoss: Symbol(),
  terran: Symbol(),
  zerg: Symbol()
}

race.protoss !== race.terran // true
race.protoss !== race.zerg // true
```

还可以给`Symbol()`加个注释`Symbol('protoss')`仅仅就是个提示，起什么和值没有任何关系。

总结：占位置的。起名字福音。
## V.undefined和null
### i.null
是一个类型。只有一个值`null`
### ii.undefined
是一个类型。只有一个值`undefined`
### iii.这两个兄弟干嘛的
这是个BUG，语言问题。
都表达了一个：`什么也没有`原创BUG哟
### iv.那他们有什么区别呢？？？
① 变量没有值 - undefined
② 如果你想有一个对象（`obj`），但是目前不想赋值，那就给他一个`null`（推荐）.`var obj = null`
如果你有一个非对象，目前不想赋值，那就给他一个`undefined`（推荐）。`var n`那它就是一个`undefine`
③ **②为惯例 ①为语法**
总结一下，null是空对象，undefined是非对象。
## VI.object
之前说的，都是基本（简单）类型，到了对象，就是复杂类型了。
复杂类型由简单类型组成。
举个例子：

```
var name = 'Oracle'
var age = '24'
var gender = 'male'
```

他们三个都是一对一，冥冥之中似乎可以放在一起。

```
var person = 
{
'name':'Oracle',
'age':'24',
'gender':'male'
}
```

变成这种`键-值`组合
### i.语法
`{`开头
`}`结尾
左边的键，可以不用引号，左边永远都是字符串。
右边该怎么写怎么写
需要变量去容纳它`var person = `，他就是一个类型是对象的变量
读取它`person['name']`这个`name`必须加引号
为了避免之前有变量也叫name
如果他符合标识符规则那可以`person.name`
### ii.对象里还可以套对象
**那么对象里套的对象，里面的对象是否可以是自己？**
这个麻烦了
**解决这个问题之前请参见([JavaScript-类型](https://574549756.github.io/2018/04/11/JavaScript-%E7%B1%BB%E5%9E%8B/))**

```
var a = {}
a.self = a
a.self.self.self是什么
```

首先对象存了一个ADDR然后不断引用这个地址

### iii.空字符串是否能当做key？

```
person = {'':'oracle'}
person['']   //oracle
```

可以
### iv.key的第一个字是否可以是数字
不可以。
`9name: 'oracle',` 这种是不可以
如果不加引号，key必须依照标识符（变量名）原则
不加引号，写起来舒服。加上引号，功能多。
同理，如果是**数组**那么读取数组成员的时候就**不能用点结构**
单独的数值不能作为标识符。数组成员只能用方括号`arr[0]`来表示
### v.key能不能有空格
一样的规则，有引号就可以，没有就GG
### vi.key可不可以加中文
可以，因为中文可以当做变量名。
### vii.for in

```
for(var key in person){
        console.log(key)
}
```

遍历数组的`key`但是
出现`key`的顺序是看天的。
那我想打出值呢？

```
for(var key in person){
        console.log(person[key])
}
```

那一起打呢？

```
for(var key in person){
        console.log(key,person[key])
}
```

和上面说的一样，随机的
## VII.typeof
### i.干吗用的？
看类型的

```
var t = 1
typeof t //"number"

var t = true
typeof t //"boolean"
```
### ii.但是有一个特殊
**这是JS的BUG**
他叫做`null`
如果测`typeof null`会返回`‘object’`
如果声明一个`函数`
用`typeof fn`本应该是`‘object’`但是他会返回`‘function’`
什么时候函数也是独立的类型了？