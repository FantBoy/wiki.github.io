## 设置数据库的字符集
!!! info "查看字符集设置"
    ``` mysql
    mysql> show variables like 'collation_%';
    +----------------------+--------------------+
    | Variable_name        | Value              |
    +----------------------+--------------------+
    | collation_connection | utf8mb4_general_ci |
    | collation_database   | latin1_swedish_ci  |
    | collation_server     | latin1_swedish_ci  |
    +----------------------+--------------------+
    3 rows in set (0.05 sec)

    mysql> show variables like 'character_set_%';
    +--------------------------+----------------------------+
    | Variable_name            | Value                      |
    +--------------------------+----------------------------+
    | character_set_client     | utf8mb4                    |
    | character_set_connection | utf8mb4                    |
    | character_set_database   | latin1                     |
    | character_set_filesystem | binary                     |
    | character_set_results    | utf8mb4                    |
    | character_set_server     | latin1                     |
    | character_set_system     | utf8                       |
    | character_sets_dir       | /usr/share/mysql/charsets/ |
    +--------------------------+----------------------------+
    8 rows in set (0.06 sec)
    ```
!!! success "修改字符集"
    ``` mysql
    mysql> set character_set_connection=utf8mb4;
    Query OK, 0 rows affected (0.05 sec)
    ```

## 设置数据库表指定column的字符集

!!! info "查询table column的字符集"
    ``` mysql
    mysql> show full columns from t_device_list;
    +-------------+---------------+-----------------+------+-----+---------+----------------+---------------------------------+---------+
    | Field       | Type          | Collation       | Null | Key | Default | Extra          | Privileges                      | Comment |
    +-------------+---------------+-----------------+------+-----+---------+----------------+---------------------------------+---------+
    | id          | int(11)       | NULL            | NO   | PRI | NULL    | auto_increment | select,insert,update,references |         |
    | device_name | varchar(64)   | utf8_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | device_ip   | varchar(16)   | utf8_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | status      | int(11)       | NULL            | NO   |     | NULL    |                | select,insert,update,references |         |
    | desc        | varchar(1024) | utf8_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | modify_time | datetime(6)   | NULL            | NO   |     | NULL    |                | select,insert,update,references |         |
    | group_id    | int(11)       | NULL            | NO   | MUL | NULL    |                | select,insert,update,references |         |
    | owner_id    | int(11)       | NULL            | NO   | MUL | NULL    |                | select,insert,update,references |         |
    +-------------+---------------+-----------------+------+-----+---------+----------------+---------------------------------+---------+
    8 rows in set (0.05 sec)
    ```
!!! success "设置指定column的字符集"
    ``` mysql
    mysql> show full columns from t_device_list;
    +-------------+---------------+-------------------+------+-----+---------+----------------+---------------------------------+---------+
    | Field       | Type          | Collation         | Null | Key | Default | Extra          | Privileges                      | Comment |
    +-------------+---------------+-------------------+------+-----+---------+----------------+---------------------------------+---------+
    | id          | int(11)       | NULL              | NO   | PRI | NULL    | auto_increment | select,insert,update,references |         |
    | device_name | varchar(64)   | latin1_swedish_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | device_ip   | varchar(16)   | latin1_swedish_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | status      | int(11)       | NULL              | NO   |     | NULL    |                | select,insert,update,references |         |
    | desc        | varchar(1024) | latin1_swedish_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | modify_time | datetime(6)   | NULL              | NO   |     | NULL    |                | select,insert,update,references |         |
    | group_id    | int(11)       | NULL              | NO   | MUL | NULL    |                | select,insert,update,references |         |
    | owner_id    | int(11)       | NULL              | NO   | MUL | NULL    |                | select,insert,update,references |         |
    +-------------+---------------+-------------------+------+-----+---------+----------------+---------------------------------+---------+
    8 rows in set (0.05 sec)

    mysql> alter table t_device_list change `desc` `desc` varchar(1024) character set utf8 collate utf8_unicode_ci not null default 'NULL';
    Query OK, 0 rows affected (0.09 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> alter table t_device_list change device_name device_name varchar(64) character set utf8 collate utf8_unicode_ci not null default 'NULL';
    Query OK, 0 rows affected (0.07 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> alter table t_device_list change device_ip device_ip varchar(16) character set utf8 collate utf8_unicode_ci not null default 'NULL';
    Query OK, 0 rows affected (0.08 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> show full columns from t_device_list;
    +-------------+---------------+-----------------+------+-----+---------+----------------+---------------------------------+---------+
    | Field       | Type          | Collation       | Null | Key | Default | Extra          | Privileges                      | Comment |
    +-------------+---------------+-----------------+------+-----+---------+----------------+---------------------------------+---------+
    | id          | int(11)       | NULL            | NO   | PRI | NULL    | auto_increment | select,insert,update,references |         |
    | device_name | varchar(64)   | utf8_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | device_ip   | varchar(16)   | utf8_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | status      | int(11)       | NULL            | NO   |     | NULL    |                | select,insert,update,references |         |
    | desc        | varchar(1024) | utf8_unicode_ci | NO   |     | NULL    |                | select,insert,update,references |         |
    | modify_time | datetime(6)   | NULL            | NO   |     | NULL    |                | select,insert,update,references |         |
    | group_id    | int(11)       | NULL            | NO   | MUL | NULL    |                | select,insert,update,references |         |
    | owner_id    | int(11)       | NULL            | NO   | MUL | NULL    |                | select,insert,update,references |         |
    +-------------+---------------+-----------------+------+-----+---------+----------------+---------------------------------+---------+
    8 rows in set (0.05 sec)
    ```







