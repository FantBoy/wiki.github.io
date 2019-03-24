---
title: Curl分析Http请求耗时 
date: 2018-01-23 22:10
toc: true
categories: Linux指令
comments: true
---

{%alert info%}

实际开发中，经常遇到网络请求时延比较高的情况，在分析请求耗时分布的时候，Curl有一个特别有用的功能：测试请求的耗时分布。
可以测试本地请求，也可以测试网络请求。

{%endalert%}

## curl参数说明
```
[root@VM_196_194_centos _posts]# curl --help
 -w, --write-out FORMAT  What to output after completion
     --xattr        Store metadata in extended file attributes
```
`-w`参数能够按照我们指定的格式，打印curl请求的相关信息。包括status_code 、 local_port 、 size_download 等重要信息。

## 打印网络请求耗时相关的变量
创建文件 curl-format.txt
```
time_namelookup: %{time_namelookup}\n 
time_connect: %{time_connect}\n  
time_appconnect: %{time_appconnect}\n  
time_redirect: %{time_redirect}\n  
time_pretransfer: %{time_pretransfer}\n  
time_starttransfer: %{time_starttransfer}\n  
----------\n 
time_total: %{time_total}\n 
```

### 参数解释
 - time_namelookup ：DNS 域名解析的时候，
 - time_connect ：TCP 连接建立的时间，就是三次握手的时间
 - time_appconnect ：SSL/SSH 等上层协议建立连接的时间，比如 connect/handshake 的时间
 - time_redirect ：从开始到最后一个请求事务的时间
 - time_pretransfer ：从请求开始到响应开始传输的时间
 - time_starttransfer ：从请求开始到第一个字节将要传输的时间
 - time_total ：这次请求花费的全部时间

## 实例
```
[root@VM_196_194_centos ~]# curl -w "@curl-format.txt" -o /dev/null -s -L "http://www.qq.com"
time_namelookup: 0.012
time_connect: 0.044
time_appconnect: 0.000
time_redirect: 0.000
time_pretransfer: 0.044
time_starttransfer: 0.076
----------
time_total: 0.206
```

其中：
 - `-o /dev/null`: 重定向响应输出
 - `-s`：不打印进度条


