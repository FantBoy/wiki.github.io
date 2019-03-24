
> `information_schema ` 库主要存储的就是一些数据库表的信息。其中`COLUMNS `记录了数据库中所有表的字段信息。

获取表的字段名:
``` mysql
select COLUMN_NAME from information_schema.COLUMNS where table_name = 'your_table_name';
```

也可以指定库名:
``` mysql
select COLUMN_NAME from information_schema.COLUMNS where table_name = 'your_table_name' and table_schema = 'your_db_name';
```







