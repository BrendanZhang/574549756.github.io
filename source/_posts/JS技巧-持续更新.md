---
title: JS技巧-持续更新
date: 2018-10-04 01:53:38
tags: JS
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
