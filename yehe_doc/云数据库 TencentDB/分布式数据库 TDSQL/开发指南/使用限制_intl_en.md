
TDSQL is a distributed database deployed in Tencent Cloud that has a Shared Nothing architecture and supports automatic horizontal splitting (sharding). You only need to specify the field for sharding when creating a table, and TDSQL will perform data routing and aggregation accordingly, where operations imperceptible to the database can be performed at the application layer.

## Software Version
The kernel version used in this development guide is 1.13.21-M-V2R501D002, which can be queried by running the `/*Proxy*/show status` statement.

>TDSQL does not support versions below 4.0 and compression protocols. You are recommended to add the `-c` option when using the client, so that the comment passthrough feature can be used.

## Features
TDSQL is capable of horizontal scaling, making it suitable for scenarios with massive amounts of data. It has the following features:
- It supports sharded, single, and broadcast tables
- It provides a flexible read/write separation mode
- It supports global `Order by`, `Group by`, and `Limit` operations
- It supports five aggregate functions, i.e., SUM, COUNT, AVG, MIN, and MAX
- It supports cross-set joins and subqueries
- It supports pre-processing protocols
- It supports global unique fields and sequence
- It supports distributed transactions
- It supports two-level partitioning
- It provides specific SQL statements for querying configuration and status of the entire cluster


## Use Limits
A distributed instance of TDSQL is highly compatible with MySQL protocols and syntax. However, due to the notable architectural differences between distributed and standalone databases, there are some use limits on MySQL's certain features and small MySQL syntax.

### General limits on TDSQL
- Custom functions, events, and tablespaces are not supported
- Views, stored procedures, triggers, and cursors are not supported
- Foreign keys, self-built partitions, and temporary tables are not supported
- Compound statements such as BEGIN END, LOOP, and UNION are not supported
- SQL syntax related to master/slave sync is not supported

### Limits on small TDSQL syntax
Currently, a TDSQL instance does not support some DDL, DML, and SQL management statements. The specific limits are as follows:

#### DDL
- CREATE TABLE ... SELECT is not supported 
- CREATE TEMPORARY TABLE is not supported 
- CREATE/DROP/ALTER SERVER/LOGFILE GROUP are not supported
- ALTER is not supported for renaming shardkey, but it can be used to change the type
- RENAME is not supported

#### DML
- SELECT INTO OUTFILE/INTO DUMPFILE/INTO var_name are not supported
- query_expression_options is not supported, such as HIGH_PRIORITY/STRAIGHT_JOIN/SQL_SMALL_RESULT/ 					SQL_BIG_RESULT/SQL_BUFFER_RESULT/SQL_CACHE/SQL_NO_CACHE/SQL_CALC_FOUND_ROWS
- Non-SELECT subqueries are not supported
- INSERT/REPLACE without column name are not supported
- ORDER BY/LIMIT cannot be used for global DELETE/UPDATE
- UPDATE/DELETE without WHERE condition are not supported
- LOAD DATA/XML are not supported
- Use of DELAYED and LOW_PRIORITY in SQL is not supported
- References and operations on variables in SQL are not supported, such as SET @c=1, @d=@c+1; SELECT @c, @d
- index_hint is not supported
- HANDLER/DO are not supported

#### SQL management statements
- ANALYZE/CHECK/CHECKSUM/OPTIMIZE/REPAIR TABLE are not supported, which should be performed with passthrough syntax
- CACHE INDEX are not supported
- FLUSH is not supported
- KILL is not supported (except for non-cross-AZ databases)
- LOAD INDEX INTO CACHE is not supported
- RESET is not supported
- SHUTDOWN is not supported
- SHOW BINARY LOGS/BINLOG EVENTS is not supported
- The combination of SHOW WARNINGS/ERRORS and LIMIT/COUNT is not supported


## System Connection Method
TDSQL provides a connection mode compatible with MySQL through the proxy API. It can be connected using the IP address, port number, username, and password. The connection statement is as follows:
```
mysql -h10.10.10.10 -P3306 -utest12 -ptest123 -c
```
