
在为nginx新增虚拟域名后，重启nginx收到如下的错误

!!! failure
    ``` shell
    # /etc/init.d/nginx reload
     * Reloading nginx configuration nginx            [fail]
    ```

## nginx.conf检测
``` shell
# nginx -t
nginx: [emerg] could not build the server_names_hash, you should increase either server_names_hash_max_size: 512 or server_names_hash_bucket_size: 64
nginx: configuration file /etc/nginx/nginx.conf test failed

# tail /var/log/nginx/error.log
2015/01/28 10:21:51 [emerg] 22362#0: could not build the server_names_hash, you should increase either server_names_hash_max_size: 512 or server_names_hash_bucket_size: 64
```

**从字面以时可以看出，因为添加了虚拟域名，导致`server_names_hash_bucket`被用光。需要增加其大小。**


## 解决方法

!!! success "在`nginx.conf`中设置其大小"

    ``` shell
    
    http {
            ...
            server_names_hash_max_size 512;
            server_names_hash_bucket_size 128;
            ...
    }
    ```





