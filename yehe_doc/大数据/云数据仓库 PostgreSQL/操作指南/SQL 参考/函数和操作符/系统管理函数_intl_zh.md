## 配置设置函数
下面是查询和修改运行时配置参数的函数，见下面表格。
 
| 函数             | 返回值 | 描述                       | 示例                  | 结果                            |
| -------------------- | ------ | --------------------- | ---------------------- | ------------------------------- |
| current_setting(setting_name)   | text   | 现在的参数值   | SELECT current_setting('datestyle');  | current_setting      -----------------    ISO, MDY |
| set_config(setting_name, new_value, is_local) | text   | 设置参数值，并返回最新的值 | SELECT set_config('log_statement_stats', 'off', false); | set_config      ------------    off                |

## 服务信号函数

| 函数                   | 返回值  | 描述                                                         |
| -------------------------- | ------- | ------------------------------------------------------ |
| pg_cancel_backend(pid int) | boolean | 取消一个后端的当前查询                                       |
| pg_reload_conf()           | boolean | 触发重新加载配置文件                                         |
| pg_rotate_logfile()        | boolean | 滚动服务器的日志文件，只有内置日志收集器的有用，其他的则没用，因为没有管理日志的子进程 |

**数据库对象大小函数**

| 函数                     | 返回值 | 描述                         | 示例                          | 结果                                 |
| ------------------- | ------ | ---------------------- | -------------------------- | ---------------------------------------- |
| pg_column_size(any)          | int    | 获取数据的存储空间字节大小    | select   pg_column_size('ddewewe');            | 8            |
| pg_database_size(oid)        | bigint | 指定数据库的大小       | select oid,* from pg_database;   select   pg_database_size(16384); | pg_database_size      ------------------           127632410 |
| pg_database_size(name)       | bigint | 指定数据库的大小    | select pg_database_size('gpperfmon');      | 127632410               |
| pg_relation_size(oid)        | bigint | 获取指定表或者索引的大小  | select pg_relation_size(17787);   | pg_relation_size      ------------------     65536 |
| pg_relation_size(text)   | bigint | 获取表或者索引的大小 | select pg_relation_size('t1');  | pg_relation_size      ------------------               65536 |
| pg_size_pretty(bigint)       | text   | 字节数转为格式化的大小     | select pg_size_pretty(122212121);  | pg_size_pretty      ----------------    117 MB   |
| pg_tablespace_size(oid)      | bigint | 获取指定表空间的大小     | select oid,* from pg_tablespace ;   select   pg_tablespace_size(1663); | pg_tablespace_size      --------------------             262275170 |
| pg_tablespace_size(name)     | bigint | 获取指定表空间的大小    | select pg_tablespace_size('pg_default');   | pg_tablespace_size      --------------------             262275170 |
| pg_total_relation_size(oid)  | bigint | 指定表所占的包括索引和数据的磁盘空间 | select oid,relname from pg_class where relname='t1';   select   pg_total_relation_size(17787); | pg_total_relation_size      ------------------------                     65536   (1 row) |
| pg_total_relation_size(text) | bigint | 指定表所占的包括索引和数据的磁盘空间 | select pg_total_relation_size('t1');                         | pg_total_relation_size      ------------------------                     65536 |
