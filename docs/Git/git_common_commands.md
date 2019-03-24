---
layout: post
filename: git_common_commands
title: git常规操作指令
datetime: 2018-04-20 14:28:29
description: 
comments: true
toc: true
tags:
categories:
 - Git
 
 
---


### 撤销git add .
文件退出暂存区，但是修改保留
```
git reset --mixed
```
如果是撤销所有的已经add的文件
```
git reset HEAD .
```
如果是撤销某个文件或文件夹：
```
git reset HEAD -filename
```
版本回退
```
git reset --hard 版本号
```
红字变无 (撤销没add修改)
```
git checkout -- 文件
```






