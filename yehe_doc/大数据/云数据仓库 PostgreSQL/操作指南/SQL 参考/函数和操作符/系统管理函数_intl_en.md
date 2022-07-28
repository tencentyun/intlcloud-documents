## Configuration Settings Functions
The functions used to query and modify runtime configuration parameters are as listed below:
 
| Function | Return Type | Description | Example | Result |
| -------------------- | ------ | --------------------- | ---------------------- | ------------------------------- |
| current_setting(setting_name)   | text   | Gets current parameter value   | SELECT current_setting('datestyle');  | current_setting      -----------------    ISO, MDY |
| set_config(setting_name, new_value, is_local) | text   | Sets parameter and returns new value | SELECT set_config('log_statement_stats', 'off', false); | set_config      ------------    off                |

## Server Signaling Functions

| Function | Return Type | Description |
| -------------------------- | ------- | ------------------------------------------------------ |
| pg_cancel_backend(pid int) | boolean | Cancels current query on backend                                       |
| pg_reload_conf()           | boolean | Triggers reloading configuration file                                         |
| pg_rotate_logfile()        | boolean | Rotates server's log file (this function works only for servers with a built-in log collector, as there is no subprocess for log management on other servers) |

**Database Object Size Functions**

| Function | Return Type | Description | Example | Result |
| ------------------- | ------ | ---------------------- | -------------------------- | ---------------------------------------- |
| pg_column_size(any)          | int    | Get data storage space size in bytes    | select   pg_column_size('ddewewe');            | 8            |
| pg_database_size(oid)        | bigint | Gets the size of the specified database       | select oid,* from pg_database;   select   pg_database_size(16384); | pg_database_size      ------------------           127632410 |
| pg_database_size(name)       | bigint | Gets the size of the specified database    | select pg_database_size('gpperfmon');      | 127632410               |
| pg_relation_size(oid)        | bigint | Gets the size of the specified table or index  | select pg_relation_size(17787);   | pg_relation_size      ------------------     65536 |
| pg_relation_size(text)   | bigint | Gets the size of the specified table or index | select pg_relation_size('t1');  | pg_relation_size      ------------------               65536 |
| pg_size_pretty(bigint)       | text   | Converts size in bytes to the specified format     | select pg_size_pretty(122212121);  | pg_size_pretty      ----------------    117 MB   |
| pg_tablespace_size(oid)      | bigint | Gets the size of the specified tablespace     | select oid,* from pg_tablespace ;   select   pg_tablespace_size(1663); | pg_tablespace_size      --------------------             262275170 |
| pg_tablespace_size(name)     | bigint | Gets the size of the specified tablespace    | select pg_tablespace_size('pg_default');   | pg_tablespace_size      --------------------             262275170 |
| pg_total_relation_size(oid)  | bigint | Gets the disk space used by the specified table, including indexes and data | select oid,relname from pg_class where relname='t1';   select   pg_total_relation_size(17787); | pg_total_relation_size      ------------------------                     65536   (1 row) |
| pg_total_relation_size(text) | bigint | Gets the disk space used by the specified table, including indexes and data | select pg_total_relation_size('t1');                         | pg_total_relation_size      ------------------------                     65536 |
