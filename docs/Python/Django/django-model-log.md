---
title: 为model添加自动化log
date: 2017-08-10 11:59
toc: true
categories: Django
comments: true
---

{%alert info%}
在web服务中，除了一些业务log意外，还需要有专门的db相关的log。在Django的服务中，db的执行时靠model来执行的，而model的执行内容对我们分析业务至关重要，
本文主要介绍Django服务中，model如果将每一次的执行都输出到log文件中。
{%endalert%}




## 在业务代码中，独立输出log

有时候需要在业务代码中，需要单独打出某一个model执行的执行语句，可以采用`query`方法
```
print Model.objects.filter(name='test').query
```

## django业务中添加model的日志自动输出
在django服务的settings配置文件中配置 **Quickly setup SQL query logging**

```
LOGGING = {
    'version': 1,
    'disable_existing_loggers': False,
    'handlers': {
        'console': {
            'level': 'DEBUG',
            'class': 'logging.StreamHandler',
        }
    },
    'loggers': {
        'django.db.backends': {
            'handlers': ['console'],
            'level': 'DEBUG',
        },
    }}

```

{%alert success%}
还有一种方式是通过中间件监控每一次model的执行，<a href=" https://djangosnippets.org/snippets/290/"> 中间件监控model </a>
{%endalert%}
