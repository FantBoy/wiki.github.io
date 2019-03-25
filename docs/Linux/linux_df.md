!!! info ""
    df: 显示磁盘分区上可以使用的磁盘空间

!!! summary "命令参数"
    - -a : 查看全部文件系统，单位默认KB
    - -h : 使用-h选项以KB、MB、GB的单位来显示，可读性高

!!! success "实例"
    ``` bash
    [root@VM_196_194_centos wiki.github.io]# df -a
    文件系统          1K-块     已用    可用 已用% 挂载点
    rootfs                -        -       -     - /
    sysfs                 0        0       0     - /sys
    proc                  0        0       0     - /proc
    devtmpfs         499348      352  498996    1% /dev
    securityfs            0        0       0     - /sys/kernel/security
    tmpfs            508452       24  508428    1% /dev/shm
    devpts                0        0       0     - /dev/pts
    tmpfs            508452    12844  495608    3% /run
    tmpfs            508452        0  508452    0% /sys/fs/cgroup
    cgroup                0        0       0     - /sys/fs/cgroup/systemd
    pstore                0        0       0     - /sys/fs/pstore
    cgroup                0        0       0     - /sys/fs/cgroup/freezer
    cgroup                0        0       0     - /sys/fs/cgroup/blkio
    cgroup                0        0       0     - /sys/fs/cgroup/net_cls
    cgroup                0        0       0     - /sys/fs/cgroup/memory
    cgroup                0        0       0     - /sys/fs/cgroup/perf_event
    cgroup                0        0       0     - /sys/fs/cgroup/cpu,cpuacct
    cgroup                0        0       0     - /sys/fs/cgroup/cpuset
    cgroup                0        0       0     - /sys/fs/cgroup/devices
    cgroup                0        0       0     - /sys/fs/cgroup/hugetlb
    configfs              0        0       0     - /sys/kernel/config
    /dev/vda1      20510332 14791724 4670092   77% /
    systemd-1             -        -       -     - /proc/sys/fs/binfmt_misc
    mqueue                0        0       0     - /dev/mqueue
    debugfs               0        0       0     - /sys/kernel/debug
    hugetlbfs             0        0       0     - /dev/hugepages
    tmpfs            101692        0  101692    0% /run/user/0
    tmpfs            101692        0  101692    0% /run/user/1000
    binfmt_misc           0        0       0     - /proc/sys/fs/binfmt_misc
    [root@VM_196_194_centos wiki.github.io]# df -h
    文件系统        容量  已用  可用 已用% 挂载点
    /dev/vda1        20G   15G  4.5G   77% /
    devtmpfs        488M  352K  488M    1% /dev
    tmpfs           497M   24K  497M    1% /dev/shm
    tmpfs           497M   13M  484M    3% /run
    tmpfs           497M     0  497M    0% /sys/fs/cgroup
    tmpfs           100M     0  100M    0% /run/user/0
    tmpfs           100M     0  100M    0% /run/user/1000
    ```
