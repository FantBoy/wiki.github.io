!!! info ""
    top: 显示操作系统中各个进程占用的系统资源

!!! success "查看指定进程的使用情况"
    ```top -i {PID} ```


!!! success "查看包含指定关键字的进程的使用情况"
    ```top -c -p $(pgrep -d',' -f nginx)```
