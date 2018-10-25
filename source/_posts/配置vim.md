---
title: 配置vim
date: 2018-10-25 17:40:42
tags: cli
catogray: cli
---
# 0. 首先需要检查 vim 是否支持 clipboard
终端输入
`vim --version | grep "clipboard"`
检查 vim 版本是否支持 clipboard
如果显示 `-clipboard` 则说明不支持

## I. 安装图形化界面的 vim 

`sudo apt get install vim-gnome`
安装完成后再次运行
`vim --version | grep "clipboard"`
发现之前的减号变成了加号`+`

这时 vim 已经支持 clipboard 了

# 1. 导入 vimrc 配置 vim
已上传 github 
快捷键`space + y`即可复制到系统剪贴板

## I.安装 vim-plug
这是个管理 vim 其他插件的工具

install:

```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## II. 如何使用

vi ~/.vimrc

```
call plug#begin('/.vim/plugged')
Plug '插件名'
Plug 'mattn/emmet-vim'
...这里都是插件
call plug#end()
```

保存-退出-重进
执行`:PlugInstall`

