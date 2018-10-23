---
title: vue的小细节
date: 2018-06-22 12:08:17
tags: vue
categories: 框架
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

# 添加事件
`v-on:click="你要干嘛"`

## 移除
```
<i class="el-icon-remove" v-on:click="removeJobExperience(index)"></i>

////////////////////////////////////////////////////////

remoteJobExperience(index) {
    this.jobExperience.splice(index, 1)
}
```

用`splice`从数组里删除一个

# 从外部传变量
比如需要用一个`profile`

```
// 下面是组件里（被分出来封装的），假设文件名为 whoAmI.vue
export default {
  props: ['profile']
}

////////////////封装的时候/////////////////

// 下面是主文件里

<whoAmI v-bind:profile="profile"/>
import whoAmI from './whoAmI'
export default{
    components: { whoAmI }
}

// 绑定这个叫做 profile 的 data
```

注意： 
- 组件的模板必须包含**一个**根元素
- 翻译一下： 最外面包着的，必须只有一个(除了template)

# 想要在 git 上预览 vue 项目
我们需要在 `gitignore` 目录里把 `dist` 取消忽略

1. 进入 `config/index.js`
2. 在 `build` 下的 `assetsPublicPath`
3. 把它的值改成 `'/vue-demo(项目名是什么就改成什么)/dist/'`
4. 这个字符串会被加在编译后的`index`里每一个脚本的前面
5. `npm run build`
6. 去 `.gitignore` 里面把 `dist` 目录删掉
7. `add commit push` 三连

## 解决 404 问题的终极方法
- 加一个目录
- 如果不行
- 再加一个目录
- 如果不行
- 再加一个目录
- 如果还不行
- 减一个目录
- 如果还不行
- 减两个目录

总结一下： **加目录和减目录**

## vue 如何增减目录
在 `config/index.js` 的 `module.exports.build.assetsPublicPath`