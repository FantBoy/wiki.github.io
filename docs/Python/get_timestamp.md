!!! info "10位时间戳获取方式"
    ``` python
    >>> import time
    >>> t = time.time()
    >>> t
    1563696759.1498728
    >>> int(t)
    1563696759
    ```

!!! info "13位时间戳获取方法"
    ``` python
    >>> import time
    >>> local_time = time.time()
    >>> local_time
    1563696874.709043
    >>> int(round(local_time * 1000))
    1563696874709
    ```

!!! success "定义宏方法"
    ``` python
    >>> import time
    >>> current_milli_time = lambda: int(round(time.time() * 1000))
    >>>
    >>> current_milli_time()
    1563697127669
    ```

!!! success "13位时间戳转换为时间"
    ``` python
    >>> import time
    >>> now = int(round(time.time() * 1000))
    >>> now_time = time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(now / 1000))
    >>> now_time
    '2019-07-21 16:23:42'
    ```