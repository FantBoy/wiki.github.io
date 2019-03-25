!!! info ""
    du : 获取指定文件或指定目录的磁盘使用空间、文件大小

!!! summary "命令参数"
    - -a :显示目录中文件的大小  单位 KB.
    - -b :显示目录中文件的大小，以字节byte为单位.
    - -c :显示目录中文件的大小，同时也显示总和；单位KB.
    - -k/-m :显示目录中文件的大小，-k 单位KB，-m 单位MB.
    - -s :仅显示目录的总值，单位KB.
    - -h :以K  M  G为单位显示，提高可读性. **最常用的一个**
    - --max-depth=n : 显示的目录深度

 
!!! success "实例"
    ``` bash 
    [root@VM_196_194_centos wiki.github.io]# du -h --max-depth=1
    8.0K	./bin
    2.4M	./site
    752K	./.git
    192K	./docs
    3.3M	.
    [root@VM_196_194_centos wiki.github.io]# du -h --max-depth=2
    8.0K	./bin
    32K	./site/MySQL
    60K	./site/Git
    124K	./site/Linux
    80K	./site/search
    108K	./site/Tools
    60K	./site/images
    116K	./site/Python
    100K	./site/Nginx
    1.6M	./site/assets
    2.4M	./site
    32K	./.git/logs
    44K	./.git/hooks
    612K	./.git/objects
    4.0K	./.git/branches
    8.0K	./.git/info
    28K	./.git/refs
    752K	./.git
    8.0K	./docs/MySQL
    12K	./docs/Git
    36K	./docs/Linux
    28K	./docs/Tools
    60K	./docs/images
    24K	./docs/Python
    16K	./docs/Nginx
    192K	./docs
    3.3M	.
    
    ```

