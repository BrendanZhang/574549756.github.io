---
title: JS技巧-持续更新
date: 2018-10-04 01:53:38
tags: JS
categories: JavaScript
---

# 0.对象操作

## I.reduce

### i.原始状态

```
this.view.$el.on('submit', 'form', (e)=>{
    e.preventDefault()
    let form = this.view.$from.get(0)
    let data = {
        name: form.name.value.trim(),
        summary: form.name.value.trim()
    }
    this.model.create(data)
})
```

-   在进行 MVC 的表单提交的时候
-   往往需要表单信息更新 model 中的 data 数据
-   在表单信息繁多时
-   通常`let data = {blablablablabla}`会写的很长
-   为解决这个问题，使用 reduce

### ii.改良状态

```
this.view.$el.on('submit', 'form', (e) => {
    e.preventDefault()
    let form = this.view.$form.get(0)
    let keys = ['name', 'summary']
    let data = {}
    keys.reduce((prev, item) => {
        prev[item] = form[item].value.trim()
        return prev
    }, data)
    this.model.create(data)
})
```

-   keys 就是原来 data 中的 key
-   流程如下：
-   可以把它理解为打劫
-   打劫 name ，把 form 里 name 的 value 抢到 data.name 里
-   return 出来已经劫走的赃物
-   继续打劫新的(原来的 name 保留)
-   打劫 summary, 把 form 里的 summary 的 value 抢到 data.summary 里
-   打劫结束

# 1.数组操作
## I.Promise相关
**前言：**
- JavaScript 是以单线程运行于浏览器中
- JS 和 UI 线程处于同一个线程
- 长时间的耗时操作，会阻塞 UI 的相应
- 浏览器大多数任务都应该以异步执行
- Event Loop 的浏览器内部事件循环机制,使得 JS 一直以callback回调的方式进行。
- 喜闻乐见的回调地狱（callback hell）

### i.遍历过程中的异步执行
使用`leancloud`获取对象信息的过程中遇到了这个问题
1. 第二轮`promise`操作依赖第一轮查找操作的结果
2. 第一轮返回一个数组，第二轮需要对数组进行遍历
3. 数组的每一项需要分别进行查询(异步操作)
4. 最终返回一个数组进行第三轮`promise`操作

```
let playlistResult = new AV.Object.createWithoutData(
    'Playlist',
    playlistId
)
var query = new AV.Query('playlistMap')                     // 建立查询
query.equalTo('playlistPointer', playlistResult)                // 设置查询条件
return query                                                // 第一轮查询开始
    .find()
    .then(playlistMap => {
        let songResultsId = []
        playlistMap.forEach(scm => {
            this.data.templateMap.push(scm.id)
            var songs = scm.get('songPointer')
            songResultsId.push(songs.id)
        })
        return songResultsId                                // 返回第一轮查询结果
    })
    .then(async songResultsId => {                              // 传入第一轮查询数组 标记异步
        let songAfter = []                                  // 建立目标数组
        var searchSong = new AV.Query('Song')                   // 建立查询对象
        for (i = 0; i < songResultsId.length; i++) {        // 遍历开始
            await searchSong.get(songResultsId[i]).then(songResult => {     // 查询开始(告诉遍历，等我查完) 
                songAfter.push(songResult)                  // 查询完毕，推送到目标数组
            })
        }
        return songAfter                                    // 返回目标数组
    })
    .then(songAfter => {                                    
        this.data.songs = songAfter.map(song => {           // 遍历目标数组选取需要的信息
            return {
                id: song.id,
                ...song.attributes
            }
        })
    })
```

**async 和 await**
1. 语义简单明确，和普通的函数执行一模一样，`async` 表达函数里有异步操作，`await` 表达紧跟在后面的表达式需要等待。
2. `async`自带执行器
3. 适用性更好，`async`函数的`await`命令后面，可以跟 Promise 对象和原始类型的值（数值、字符串、布尔，等同于同步操作）
4. `async`返回一个 Promise 对象，可以 then 链式调用。函数执行过程遇到`await`就先返回，等待`await`的异步操作完成，再继续执行后面的语句。
5. `await`后的 Promise 对象，运行结果可能是失败，所以最好放在 try...catch 块里抓取错误信息
6. `await`只能用在`async`函数之中，用于普通函数会报错。