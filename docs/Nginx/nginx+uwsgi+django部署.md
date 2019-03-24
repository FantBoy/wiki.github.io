---
title: nginx+uwsgi+django部署
date: 2017-04-02 20:57:00 +09:00
toc: true
categories: Nginx
comments: true
---

{%alert success%}
<p></p>
这里省略掉nginx、uwsgi和django的安装部分，直接讲三者的部署

{%endalert%}

## django的部署
在django项目的根目录编写用于uwsgi启动的配置文件uwsgi.ini

``` xml
[uwsgi]

socket           = :8080                           # Django-related settings
chdir            = /usr/local/server/WechatServer  # the base directory (full path)
module           = WechatServer.wsgi               # Django s wsgi file
master           = true                            # master
processes        = 4                               # maximum number of worker processes
# chmod-socket   = 664
vacuum           = true                            # clear environment on exit
daemonize        = true                            # true or filepath. eg:/tmp/cms/wsgi.log

```
## uwsgi启动

### uwsgi配置参数列表

|    参数     | 含义                                       |
| :-------: | :--------------------------------------- |
|   http    | 协议类型和端口号                                 |
| processes | 开启的进程数量                                  |
|  workers  | 开启的进程数量，等同于processes                     |
|   chdir   | 指定运行目录，django项目的根目录                      |
| wsgi-file | 载入wsgi-file                              |
|  module   | django项目的wsgi文件                          |
|   stats   | 在指定的地址上，开启状态服务                           |
|  threads  | 运行线程。由于GIL的存在，我觉得这个真心没啥用。                |
|  master   | 允许主进程存在                                  |
| daemonize | 使进程在后台运行，并将日志打到指定的日志文件或者udp服务器。实际上最常用的，还是把运行记录输出到一个本地文件上。 |
|  pidfile  | 指定pid文件的位置，记录主进程的pid号。                   |
|  vacuum   | 当服务器退出的时候自动清理环境，删除unix socket文件和pid文件    |



### 启动uwsgi

到django项目的根目录下，启动wsgi有多个参数

- -x  表示以xml为配置文件启动uwsgi
- -d /var/log/uwsgi.log  后台运行uwsgi并把日志写到/var/log/uwsgi.log里面

```
[root@VM_196_194_centos WechatServer]# /usr/local/server/uwsgi/uwsgi --ini uwsgi.ini
```

## nginx配置

### 配置实例

``` xml
server {
    listen         8000;  # 这里的端口是nginx暴露在外网的端口，用户实际访问的端口
    server_name    bearboyxu.cn
    charset UTF-8;
    access_log      /var/log/nginx/myweb_access.log;
    error_log       /var/log/nginx/myweb_error.log;

    client_max_body_size 75M;

    location / {
        include uwsgi_params;
        uwsgi_pass 0.0.0.0:8080;  # 这里的端口一定uwsgi.ini中绑定的端口一直
        uwsgi_read_timeout 2;
    }   
    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /registration/500.html;
    location = /registration/500.html {
        root   html;
    }
    location /static {
        expires 30d;
        autoindex on;
        add_header Cache-Control private;
        alias /usr/local/server/WechatServer/static/;  # 静态文件路径
        index index.html index.htm;
     }
     location /media/ {
         alias  /root/cms/cms/media/;
     }
 }
```
