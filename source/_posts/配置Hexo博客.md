---
title: 配置Hexo博客
date: 2018-03-17 02:08:19
tags: Hexo博客相关
---
## 1.配置环境
I. Deepin 15.5系统（Arch Linux内核）
II. 需要nood.js、NPM、Git。
III. 需要Github SSH公钥（linux环境下存在权限问题，务必在root用户下添加SSH公钥）——
`sudo ssh-keygen -t rsa -C "your_email@example.com"`
`sudo cat ~/.ssh/id_rsa.pub`
`sudo cat ~/.ssh/id_rsa.pub`
拷贝id_rsa.pub文件内所有内容去Github的SSH页面New SSH key
去掉`sudo`重做以上四部以添加普通用户SSH Key
以上操作用于`sudo`命令中由于SSH Key缺失而产生的：
`Permission denied (publickey).`
`fatal: The remote end hung up unexpectedly`
~~权限问题~~

---

## 2.创建博客
I. 终端进入安全目录（`cd ~Desktop`or`cd ~/Documents`）
II. 在GitHub上创建一个空repo（即空仓库，后文统称repo）名称`用户名.githubio`
III. 运行`npm install -g hexo-cli`安装Hexo
IV. `hexo init myBlog`创建博客本地路径`cd myBlog`进入博客路径
V. `npm i` 安装Hexo模块（Hexo规格）
VI. `hexo new 博客名` 创建博客
这里注意`hexo new`命令创建一篇博客才是有效的，仅在/source/_posts添加MarkDown文件并不能创建博客。（不然给你hexo命令干吗用？）
VII. `open _config.yml`打开配置文件更改网站配置（可用vim也可用其他软件）：
     <font size=2 color=gray>把title改成标题名
     把author改成你自己的名字（作者）
     最后一行type改成`type: git`(git前有个空格，不做盲人。)
     与type平齐加一行`repo: 仓库地址` 地址为`git@github.com:用户名.github.io`(地址前面有个空格，其余同上括号。)</font>
VIII. `npm install hexo-developer-git --save`这步很重要，安装git部署插件。
IX. `Hexo deploy`发布发布发布
X. 这时候也许会遇到各种各样奇奇怪怪的问题~~比如~~:
`Permission denied`这时候在命令前加`sudo`
Git部署问题：
`fatal: 'username.github.io' does not appear to be a git repository`
请确认已配置Git，或者将地址改为HTTPS地址。
或许还有别的特别麻烦的问题，这个原因很多列出来超长...[所以我决定丢一个链接](https://hexo.io/zh-cn/docs/troubleshooting.html)
XI. 进入`用户名.github.io`即可看到效果
XII. 对博客的任意改动执行`hexo g` 和 `hexo d`即可发布。

---
## 3.博客创建Git仓库代码
I. 为什么需要备份呢？
因为`hexo g hexo d`发布的仅仅是本地博客仓库的public路径下的内容，但是我们需要博客仓库的整个代码以防意外~~手抖~~。
II. 两种方法:分支＆新仓库
III. 分支：
    1.创建仓库用户名.github.io
    2.创建两个分支：master和hexo
    3.设置Hexo默认分支（反正git push用的是Hexo分支，hexo命令只影响master）
    4.`git clone git@github.com:用户名/用户名.github.io.git`拷贝仓库
    5.`cd 用户名.github.io.git`进入文件夹`npm install hexo`、`hexo init`、`npm i`、`npm install hexo-deployer-git --save`
    6.修改_config.uml中deploy为master
    7.`git add .` `git commit` `git push`三连击提交网站文件
    8.`hexo g` `hexo d`二连击生成部署网站（有问题？请`hexo clean`）

IV. 新仓库：
    1.创建新仓库新仓库blog-Generator
    2.在myBlog里打开终端执行（注意点SSH地址）
![SSH](https://video.jirengu.com/Fpl8Cw-Pb4FCBdE_OE_N0ftCrtry)
    3.每次`hexo d之后`请`git add .` `git commit` `git push`三连击提交网站文件