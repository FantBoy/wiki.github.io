---
title: mac下anaconda包管理
date: 2018-01-18 21:40
toc: true
categories: Jetbrains
comments: true
---

{%alert info%}

Anaconda利用conda命令来进行package和environment的管理，其包含了Python和相关的配套工具。 

{%endalert%}

## conda常用命令

```
# 查看已经安装的packages
# 最新版的conda是从site-packages文件夹中搜索已经安装的包，不依赖于pip
conda list
```

```
# 查看当前环境下已安装的包
conda list

# 查看某个指定环境的已安装包
conda list -n python34

# 查找package信息
conda search numpy

# 安装package
conda install -n python34 numpy
# 如果不用-n指定环境名称，则被安装在当前活跃环境
# 也可以通过-c指定通过某个channel安装

# 更新package
conda update -n python34 numpy

# 删除package
conda remove -n python34 numpy

# 更新conda，保持conda最新
conda update conda

# 更新anaconda
conda update anaconda

# 更新python到当前最新版本
conda update python
```



## 添加国内镜像

```
# 添加Anaconda的TUNA镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

# 设置搜索时显示通道地址
conda config --set show_channel_urls yes123456
```



### mac安装MySQLdb

```
conda install pymysql #有可能会失败，更推荐后者
pip install MySQL-python
```

