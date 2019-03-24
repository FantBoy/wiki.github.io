
!!! summary "撤销已经add的文件，但是保留变更"
    ``` shell
    git reset --mixed
    ```

!!! summary "撤销所有已经add的文件"
    ``` shell
    git reset HEAD .
    ```

!!! summary "撤销某个文件或者文件夹"
    ``` shell
    git reset HEAD -filename
    ```

!!! summary "版本回退，不保留变更"
    ``` shell
    git reset --hard commit_id
    ```

!!! summary "红字变无，撤销没有add的变更"
    ``` shell
    git checkout -- filename
    ```







