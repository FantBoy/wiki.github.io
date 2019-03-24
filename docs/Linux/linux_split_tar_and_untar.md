---
layout: post
filename: linux_split_tar_and_untar
title: Linux下压缩包分割、合并和解压
datetime: 2018-09-12 23:35:29
description: Linux下压缩包分割、合并和解压
comments: true
toc: true
tags:
categories:
 - Linux指令
 
---

## 目录压缩
```
[bearboyxu@VM_196_194_centos ~]$ tar -zcvf nginx_trunk.tar.gz nginx_trunk/
```
## 压缩包分割
### 按照固定大小分割
```
[bearboyxu@VM_196_194_centos ~]$ split -b 1M nginx_trunk.tar.gz nginx_trunk.tar.gz.
[bearboyxu@VM_196_194_centos ~]$ ll
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:22 nginx_trunk.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:24 nginx_trunk.tar.gz.aa
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:24 nginx_trunk.tar.gz.ab
```
### 设置后缀格式为数字
```
[bearboyxu@VM_196_194_centos ~]$ split -a 2 -d -b 1M nginx_trunk.tar.gz nginx_trunk.tar.gz.
[bearboyxu@VM_196_194_centos ~]$ ll
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:22 nginx_trunk.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:25 nginx_trunk.tar.gz.00
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:25 nginx_trunk.tar.gz.01
```

## 合并压缩包
```
[bearboyxu@VM_196_194_centos ~]$ cat nginx_trunk.tar.gz.0* > nginx_trunk_combin.tar.gz
[bearboyxu@VM_196_194_centos ~]$ ll
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:28 nginx_trunk_combin.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:28 nginx_trunk.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:28 nginx_trunk.tar.gz.00
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:28 nginx_trunk.tar.gz.01
```

## 打包压缩分割大文件
```
[bearboyxu@VM_196_194_centos ~]$ tar -zcvf - nginx_trunk | split -a 3 -d -b 1M - nginx_trunk.tar.gz
[bearboyxu@VM_196_194_centos ~]$ ll
drwxrwxr-x  3 bearboyxu bearboyxu     4096 4月  29 12:20 nginx_trunk
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:32 nginx_trunk.tar.gz.000
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:32 nginx_trunk.tar.gz.001
```

## 合并压缩包解压
```
[bearboyxu@VM_196_194_centos ~]$ cat nginx_trunk.tar.gz.* | tar -zxvf -
```


