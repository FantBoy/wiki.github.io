---
layout: post
filename: Linux_get_external_network_ip
title: Linux下查询外网ip的方法
datetime: 2018-04-17 21:17:55
description: 
comments: true
toc: true
tags:
categories:
 - Linux指令
---

## Curl 纯文本格式输出方法
``` shell
curl icanhazip.com
curl ifconfig.me
curl curlmyip.com
curl ifconfig.io
```

## Json 格式输出方法
``` shell
curl ipinfo.io/json
curl ifconfig.me/all.json
curl ifconfig.io/all.json
```

## Xml 格式输出方法

``` shell
curl ifconfig.me/all.xml
curl ifconfig.io/all.xml
```
## Curl 获取所有IP细节
``` shell
curl ifconfig.io/all
curl ifconfig.me/all
```


## 使用 Wget 代替 Curl
``` shell
wget http://ipecho.net/plain -O - -q ; echo
wget http://observebox.com/ip -O - -q ; echo
```





