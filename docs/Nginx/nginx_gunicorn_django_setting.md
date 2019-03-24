---
layout: post
filename: nginx_gunicorn_django_setting
title: nginx+gunicorn+django部署
datetime: 2018-04-17 21:04:17
description: 
comments: true
toc: true
tags:
 - gunicorn
 - nginx
 
categories:
 - Nginx
 
---

## gunicorn安装
``` shell
$ sudo apt-get update
$ sudo apt-get install gunicorn
```

## Django配置

### setting配置
添加`gunicorn`到`settings.py`的`INSTALLED_APPS`中
``` python
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.db.backends',
    'gunicorn',
    'LoginMiddleWare',
)
```
### gunicorn配置文件
新建配置文件`gunicorn.py`在Django的根目录。内容如下：

``` python
# -*- coding: utf-8 -*-
from __future__ import unicode_literals

"""
-------------------------------------------------
   File Name：     gunicorn.py
   Description :
   Author :       bearboyxu
   date：          2018/3/31
-------------------------------------------------
   Change Activity:
                   2018/3/31:
-------------------------------------------------
"""
__author__ = 'bearboyxu'

import logging
import logging.handlers
from logging.handlers import WatchedFileHandler
import os
import multiprocessing
bind = '127.0.0.1:8020'      #绑定ip和端口号
backlog = 512                #监听队列
# chdir = '/home/test/server/bin'  #gunicorn要切换到的目的工作目录
timeout = 30      #超时
worker_class = 'gevent' #使用gevent模式，还可以使用sync 模式，默认的是sync模式

workers = multiprocessing.cpu_count() * 2 + 1    #进程数
threads = 4 #指定每个进程开启的线程数
loglevel = 'info' #日志级别，这个日志级别指的是错误日志的级别，而访问日志的级别无法设置
access_log_format = '%(t)s %(p)s %(h)s "%(r)s" %(s)s %(L)s %(b)s %(f)s" "%(a)s"'    #设置gunicorn访问日志格式，错误日志无法设置

"""
其每个选项的含义如下：
h          remote address
l          '-'
u          currently '-', may be user name in future releases
t          date of the request
r          status line (e.g. ``GET / HTTP/1.1``)
s          status
b          response length or '-'
f          referer
a          user agent
T          request time in seconds
D          request time in microseconds
L          request time in decimal seconds
p          process ID
"""
accesslog = "/data/log/gunicorn_access.log"      #访问日志文件
errorlog = "/data/log/gunicorn_error.log"        #错误日志文件

```


##启动gunicorn
通过`gunicorn`启动Django,当Django进程异常kill时，gunicorn会自动拉起进程.
``` shell
gunicorn -c gunicorn.py site.wsgi:application  --reload   # debug模式
gunicorn -c gunicorn.py site.wsgi:application  --daemon # 开启守护进程模式
```

## nginx配置
nginx中通过`proxy_pass`对请求做反向代理。注意保持ip和port跟gunicorn的配置一致。
``` shell
server {
             listen 80;

            server_name servername
            access_log /data/log/access.log;
            error_log /data/log/error.log;

            location / {
            proxy_pass http://127.0.0.1:8020;
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

            root   html;
            index  index.html index.htm;
            }
}
```

### nginx重启
``` shell
[root@TENCENT64 /etc/nginx]#service nginx restart
```





