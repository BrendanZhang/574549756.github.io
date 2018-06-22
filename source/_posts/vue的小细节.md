---
title: vue的小细节
date: 2018-06-22 12:08:17
tags: vue
---
`npm run dev`
# vue 引入第三方 CSS
- reset css 和 normalize css 哪个好？
    - normalize css 让页面默认样式在每一个浏览器上是一样的（统一默认样式）
    - reset css 篡改默认样式（特别不喜欢的样式给它改了）
    - 他们是不冲突的
    - 我们可以先统一样式，然后再改些特别不喜欢的。

# element
饿了么做的 vue 2.0 组件库
[element](http://element-cn.eleme.io/#/zh-CN)

main.js 里加入这点东西

```
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';

Vue.use(ElementUI);
// 注册很多全局组件，不用声明就可以使用
```
