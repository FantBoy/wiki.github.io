
## 目录压缩
``` shell
[bearboyxu@~]$ tar -zcvf nginx_trunk.tar.gz nginx_trunk/
```

## 压缩包分割
### 按照固定大小分割
```
[bearboyxu@~]$ split -b 1M nginx_trunk.tar.gz nginx_trunk.tar.gz.
[bearboyxu@~]$ ll
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:22 nginx_trunk.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:24 nginx_trunk.tar.gz.aa
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:24 nginx_trunk.tar.gz.ab
```
### 设置后缀格式为数字
```
[bearboyxu@~]$ split -a 2 -d -b 1M nginx_trunk.tar.gz nginx_trunk.tar.gz.
[bearboyxu@~]$ ll
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:22 nginx_trunk.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:25 nginx_trunk.tar.gz.00
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:25 nginx_trunk.tar.gz.01
```

## 合并压缩包
```
[bearboyxu@~]$ cat nginx_trunk.tar.gz.0* > nginx_trunk_combin.tar.gz
[bearboyxu@~]$ ll
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:28 nginx_trunk_combin.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1971785 9月  12 23:28 nginx_trunk.tar.gz
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:28 nginx_trunk.tar.gz.00
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:28 nginx_trunk.tar.gz.01
```

## 打包压缩分割大文件
```
[bearboyxu@~]$ tar -zcvf - nginx_trunk | split -a 3 -d -b 1M - nginx_trunk.tar.gz
[bearboyxu@~]$ ll
drwxrwxr-x  3 bearboyxu bearboyxu     4096 4月  29 12:20 nginx_trunk
-rw-rw-r--  1 bearboyxu bearboyxu  1048576 9月  12 23:32 nginx_trunk.tar.gz.000
-rw-rw-r--  1 bearboyxu bearboyxu   923209 9月  12 23:32 nginx_trunk.tar.gz.001
```

## 合并压缩包解压
```
[bearboyxu@~]$ cat nginx_trunk.tar.gz.* | tar -zxvf -
```


