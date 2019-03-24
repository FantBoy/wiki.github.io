---
layout: post
filename: cp命令覆盖拷贝
title: cp命令覆盖拷贝
date: 2018-04-15 01:33:36
description: cp命令覆盖拷贝
comments: true
toc: true
categories:
 - Linux指令
---


>cp覆盖时，无论加什么参数-f之类的还是提示是否覆盖，究其根本原因是操作系统默认对`cp`做了别名操作, 在 `~/.bashrc`

## 系统默认配置
``` shell
# .bashrc

# User specific aliases and functions

#alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi
```
所以我们在`cp`的时候，无论无何都会出现是否覆盖的提示

## 解决方法
### 临时使用
执行`cp`命令前，先执行 `alise cp='cp'`.可以屏蔽到覆盖提醒，而不改变用户设置。用户重新登录后失效

### 永久修改
注释掉`~/.bashrc`里对`cp`的别名








