---
title: 关于webpack
date: 2018-06-19 22:17:38
tags: webpack
categories: 框架
---
# 0.文件结构

```
.____
    |-- src      source            //未经翻译的代码
    |
    |-- dist     distribution      //待发布的代码
    |
    |-- vendors      //第三方代码jQuery什么的
    |
    |-- node_modules    //第三方包
```

# 1.关于webpack
## I.什么是webpack
- webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)
- 当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)
- 其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle
### i.四个核心概念
- 入口(entry)：你要从什么转过去(src)
- 输出(output)：你要输出到哪 bundle (dist)
- loader：最痛苦的部分，webpack 能理解一等公民JS，但是理解不了其他文件，所以我们需要插件把他们转换成 webpack 能处理的有效模块
- 插件(plugins)：loader拿来转模块，插件可以执行更多任务（各种各样）
## II.gulp/grunt 与 webpack
### gulp
- gulp强调的是前端开发的工作流程
- 我们可以通过配置一系列的task，定义task处理的事务（例如文件压缩合并、雪碧图、启动server、版本控制等）
- 然后定义执行顺序，来让gulp执行这些task，从而构建项目的整个前端开发流程。
### webpack
- webpack是一个前端模块化方案，更侧重模块打包
- 我们可以把开发中的所有资源（图片、js文件、css文件等）都看成模块，通过loader（加载器）和plugins（插件）对资源进行处理
- 打包成符合生产环境部署的前端资源。
### 区别
- 虽然都是前端自动化构建工具，但看他们的定位就知道不是对等的。
- gulp严格上讲，模块化不是他强调的东西，他旨在规范前端开发流程。
- webpack更是明显强调模块化开发，而那些文件压缩合并、预处理等功能，不过是他附带的功能。
## III.webpack 如何配置多入口文件页面
前面所介绍的四个核心概念，在这里显得尤为重要
标准的配置文件应该长这样：

```
module.exports={
    //入口文件的配置项
    entry:{},
    //出口文件的配置项
    output:{},
    //模块：例如解读CSS,图片如何转换，压缩
    module:{},
    //插件，用于生产模版和各项功能
    plugins:[],
    //配置webpack开发服务功能
    devServer:{}
}
```

- entry：配置入口文件的地址，可以是单一入口，也可以是多入口。
- output：配置出口文件的地址，在webpack2.X版本后，支持多出口配置。
- module：配置模块，主要是解析CSS和图片转换压缩等功能。
- plugins：配置插件，根据你的需要配置不同功能的插件。
- devServer：配置开发服务功能

### entry
单页面中：`entry: resolve("src/home/index.js")
`
多页面中：

```
//多页应用程序，则需要多个入口文件，例如：
entry: {
  home: resolve("src/home/index.js"),
  about: resolve("src/about/index.js")
}
```

这样，整个项目就有了两个入口 `home` 和 `about`

### 入口变多以后

```
const path = require('path');
module.exports={
    //入口文件的配置项
    entry:{
        home:'./src/home.js',
        //这里我们又引入了一个入口文件
        about:'./src/about.js'
    },
    //出口文件的配置项
    output:{
        //输出的路径，用了Node语法
        path:path.resolve(__dirname,'dist'),
        //输出的文件名称
        filename:'[name].js'
    },
    //模块：例如解读CSS,图片如何转换，压缩
    module:{},
    //插件，用于生产模版和各项功能
    plugins:[],
    //配置webpack开发服务功能
    devServer:{}
}
```

可以看到代码，在入口文件配置中，增加了一个entry2.js的入口文件（这个文件你需要自己手动建立），这时候要打包的就有了两个入口文件。`output` 中的`filename` 我们改成了`[name].js`

`[name]`的意思是根据入口文件的名称，打包成相同的名称，有几个入口文件，就可以打包出几个文件。

- 进去 `home.js` 和 `about.js`
- 出来 `home.js` 和 `about.js`

## IV.webpack解决了什么问题
**前端资源依赖管理**
- 我们在浏览器中的 js 中，不能直接引用其它 js, css 等文件（或说，模块）- 而 webpack 就是用来解决这个问题的，让你的项目可以很好地分文件、分模块

- 支持依赖各种拓展名的文件
- 能够在不依赖 gulp 或 grunt 的情况下直接产出打包文件
- 支持实时编译，浏览器同步刷新

### i.前端用的语言太多了
- html、css和js的配合才能保证webapp的运行，增量安装是按需加载的需要
- 开发完成后输出三种以上不同格式的静态资源，静态资源之间有可能存在互相依赖关系，最终构成一个复杂的资源依赖树（甚至网）

问题：
1. 为什么老项目构建臃肿不堪？
    基于requirejs进行打包，会把项目所有的一来都打包到一个文件里，如果项目中同时依赖一个模块，

2. 老项目为什么模块化不足？
    老项目的模块化，仅仅体现在js层面，解决了模块引用的问题，但在开发方式上，依然可以看做是过程式的， 这样的结果就导致了项目的难扩展和难维护，让开发人员在与产品汪的对峙中，并不从容。

3. 如何避免手动管理DOM？
    如果你在做数据展示这一块的开发工作，相信你一定体会颇深，发送http请求到服务端，拿到返回的数据后手动渲染DOM至页面，这是最原始的开发方式，无非再加一个模板引擎之类的，但最终还是避免不了手动渲染，如果页面逻辑复杂，比如给你来一个翻页的功能，再来一个筛选项，估计你会觉得世界并不那么美好。

### ii.webpack 的优势
1. 代码分割：
  - webpack支持二种依赖加载：同步和异步。同步的依赖会在编译时直接打包输出到目的文件
  - 异步加载会单独生成代码块，只有在浏览器中需要时才会异步加载这些代码块。
2. Loaders：
  - 默认加载js，通过loaders来把其他类型的资源转换成js输出。
3. 各种插件
  - webpack提供强大插件来提高工作效率。

# 2.Couldn't find preset "env" 
找不到他娘的env！
`npm install babel-preset-env`
- webpack这玩意，他说找不到啥你就装啥。
- 所以修好你的npm
- `npm i fucking-webpack`


# 3.Can I use？
[这个网站可以查询兼容性问题](http://caniuse.com)
[这个网站可以自动转换CSS](http://autoprefixer.github.io)
## I.如何让 webpack 解决 flex 布局的兼容性问题
[postcss-loader](https://github.com/postcss/postcss-loader)

他来帮你加前缀`-webkit-``-ms-flexbox`等等

### i.碰到的诡异问题(postcss)

#### 迷之花括号
```
body{
  //↑说我body的花括号是不必要的
}
```

- 告诉我们有时候文档也不能全信
- 遇事不决还是查`stack overflow`

postcss.config.js

```
module.exports = {
  //parser: 'sugarss',
  //这一行 parser 删了就没问题了
  plugins: {
    'postcss-import': {},
    'postcss-cssnext': {},
    'cssnano': {}
  }
}
```

- 这个 `sugarss` 在默认情况是不必要的

#### 重复的插件

- postcss-cssnext found a duplicate plugin ('autoprefixer') in your postcss plugins. 
- This might be inefficient. 
- You should remove 'autoprefixer' from your postcss plugin list since it's already included by postcss-cssnext.

- 他说我使用了重复的插件('autoprefixer')
- 很低效
- 应该把它删了，因为 `postcss-cssnext` 已经包含这个插件了

```
module.exports = {
  //parser: 'sugarss',
  plugins: {
    'postcss-import': {},
    'postcss-cssnext': {},
    //'cssnano': {}
    //把这行删了，他就不会提示这个 warning 了 
  }
}
```
