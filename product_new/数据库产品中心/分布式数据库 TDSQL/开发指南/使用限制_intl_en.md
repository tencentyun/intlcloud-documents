### Limits on User Permissions
For the current version, you cannot configure user permissions on the command line. You need to log in to Tencent Cloud Console to do so.
```
	mysql> grant all on *.* to 'test'@'%' identified by 'test123';
	ERROR 7009 (HY000): Proxy ERROR:proxy do not support such use yet
```	

### Currently Unsupported Features
1. Custom data types and functions.
2. Views, stored procedures, triggers, and cursors.
3. Foreign keys and self-built partitions.
4. Compound statements such as BEGIN END and LOOP.
5. Subqueries are supported only for derived tables with shardkey.

### Limits on Database Status Information
1. As the SQL for querying database status information is randomly sent to a physical shard, the statistics may be inaccurate.
2. The SQL for querying a system table is also randomly sent to a physical shard.

### Limits on Aggregate Functions
1. If you aggregate after `distinct`, the `where` condition must contain the `shardkey`.
```
select count(distinct a)，sum(distinct a)，avg(distinct a) from table where sk=\*\*
```
2. If `distinct`, `order by`, and `group by` are followed by a function, the function must appear in the `select` field and be defined by an alias which is used after the corresponding `distinct`, `order by`, and `group by`.
```
select concat(...) as substr from table where ... order by substr
```

3. The `group by` field must be contained in the `select` field. For example, the `select` field below must contain the `b` field.
```
select count(a),b from test group by b
```

### Limits on Joins
For now, TDSQL only supports join operations in a single shard, which means that all SQLs in a transaction must be executed in the same shard; therefore, the `shardkey` field must be specified.
```
mysql> create table test1 ( a int , b int, c char(20) ) shardkey=a;
Query OK, 0 rows affected (1.56 sec)
mysql> create table test2 ( a int , d int, e char(20) ) shardkey=a;
Query OK, 0 rows affected (1.46 sec)
mysql> insert into test1 (a,b,c) values(1,2,"record1"),(2,3,"record2");
Query OK, 2 rows affected (0.02 sec)
mysql> insert into test2 (a,d,e) values(1,3,"test2_record1"),(2,3,"test2_record2");
Query OK, 2 rows affected (0.02 sec)
mysql> select * from test1 join test2 on test1.a=test2.a;
ERROR 1105 (07000): Proxy Warning - join shardkey error
mysql> select * from test1 join test2 on test1.a=test2.a where test1.a=1;
+------+------+---------+------+------+---------------+
| a     | b     | c        | a     | d     | e                |
+------+------+---------+------+------+---------------+
| 1     | 2     | record1 | 1    | 3      | test2_record1 |
+------+------+---------+------+------+---------------+
1 row in set (0.00 sec)
```
>`mysql> select * from test1 join test2 on test1.a=test2.a;` will be supported in subsequent versions, but it should be inner join and the `where` condition of inner join must be that the `shardkey` fields of two tables are identical.

### Limits on Preprocessing
Supported SQL types:
```
PREPARE Syntax
EXECUTE Syntax
```
Supported binary protocols:
```
COM_STMT_PREPARE
COM_STMT_EXECUTE
```
Below is a code sample:
```
	mysql> select * from test1;
	+---+------+
	| a | b    |
	+---+------+
	| 5 |    6 |
	| 3 |    4 |
	| 1 |    2 |
	+---+------+
	3 rows in set (0.03 sec)
	
	mysql> prepare ff from "select * from test1 where a=?";
	Query OK, 0 rows affected (0.00 sec)
	Statement prepared
	
	mysql> set @aa=3;
	Query OK, 0 rows affected (0.00 sec)
	
	mysql> execute ff using @aa;
	+---+------+
	| a | b    |
	+---+------+
	| 3 |    4 |
	+---+------+
	1 row in set (0.06 sec)
```

### Limits on SQL
The following syntax is not supported for table creation:
```
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
SELECT * from old_tbl_name;
```
The following syntax is not supported for INSERT:
```
	INSERT [LOW_PRIORITY | HIGH_PRIORITY] [IGNORE]
	    [INTO] tbl_name [(col_name,...)]
	    SELECT ...
	    [ ON DUPLICATE KEY UPDATE
	      col_name=expr
	        [, col_name=expr] ... ]
```
The following syntax is not supported for SELECT:
```
	SELECT
	    [INTO OUTFILE 'file_name'
	        [CHARACTER SET charset_name]
	        export_options
	      | INTO DUMPFILE 'file_name'
	      | INTO var_name [, var_name]]
```
KILL is not supported.

### Supported SQL Types
DDL syntax is supported. For more information, see [DDL Statements](https://intl.cloud.tencent.com/document/product/1042/33358).
```
	CREATE TABLE Syntax
	CREATE INDEX Syntax
	DROP TABLE Syntax
	DROP INDEX Syntax
	ALTER TABLE Syntax
	TRUNCATE TABLE Syntax
```
DML syntax is supported. For more information, see [Creating a Sharded Table](https://intl.cloud.tencent.com/document/product/1042/33379)。
```
	INSERT Syntax
	REPLACE Syntax
	UPDATE Syntax
	DELETE Syntax
	SELECT Syntax
```
Prepare syntax is supported:
```
	PREPARE Syntax
	EXECUTE Syntax
	DEALLOCATE PREPARE Syntax
```
Prepare syntax samples:
```
	mysql> prepare ff from 'select * from test.test1 where a=?';
	mysql> set @a=1;
	mysql> execute ff using @a;
	mysql> deallocate prepare ff;
```
Database tool commands:
```
	DESCRIBE Syntax
	EXPLAIN Syntax
	USE Syntax
```	
Database management syntax is supported:
```
	SET Syntax (modification of global variables is not supported)
	SHOW Syntax
	SHOW COLUMNS Syntax
	SHOW CREATE TABLE Syntax
	SHOW INDEX
	SHOW TABLES Syntax
	SHOW TABLE STATUS Syntax
	SHOW TABLES Syntax
	SHOW VARIABLES Syntax
```
Database management syntax samples:
```
	mysql> show columns from test.test1;
	mysql> show index from test.test1;
	mysql> show table status;	
	mysql> show tables from test;	
	mysql> show variables like "%char%";	
```
"proxy" randomly sends other SHOW commands to a physical shard (set).
