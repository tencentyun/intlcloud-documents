## Feature Limits
- Custom functions, events, and tablespaces are not supported
- Views, stored procedures, triggers, and cursors are not supported
- Foreign keys and self-built partitions are not supported
- Compound statements such as BEGIN END, LOOP, and UNION are not supported
- SQL syntax related to master/slave sync is not supported

## Limits on small syntax


### DDL

- CREATE TABLE ... SELECT is not supported 
- CREATE TEMPORARY TABLE is not supported 
- CREATE/DROP/ALTER SERVER/LOGFILE GROUP are not supported
- ALTER is not supported for renaming shardkey, but it can be used to change the type
- RENAME is not supported

### DML
- SELECT INTO OUTFILE/INTO DUMPFILE/INTO var_name are not supported
- query_expression_options is not supported, such as HIGH_PRIORITY/STRAIGHT_JOIN/SQL_SMALL_RESULT/SQL_BIG_RESULT/SQL_BUFFER_RESULT/SQL_CACHE/SQL_NO_CACHE/SQL_CALC_FOUND_ROWS
- INSERT/REPLACE without column name are not supported
- ORDER BY/LIMIT cannot be used for global DELETE/UPDATE
- UPDATE/DELETE without WHERE condition are not supported
- LOAD DATA/XML are not supported
- DELAYED/LOW_PRIORITY cannot be used in SQL statements
- INSERT ... SELECT is not supported
- References and operations on variables in SQL are not supported, such as SET @c=1, @d=@c+1; SELECT @c, @d
- index_hint is not supported
- HANDLER/DO are not supported

### SQL management
- ANALYZE/CHECK/CHECKSUM/OPTIMIZE/REPAIR TABLE are not supported, which should be performed with passthrough syntax
- CACHE INDEX are not supported
- FLUSH is not supported
- KILL is not supported
- LOAD INDEX INTO CACHE is not supported
- RESET is not supported
- SHUTDOWN is not supported
- SHOW BINARY LOGS/BINLOG EVENTS is not supported
- The combination of SHOW WARNINGS/ERRORS and LIMIT/COUNT is not supported

### Other limits
Up to 1,000 tables can be created by default. If you need to create more tables, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
