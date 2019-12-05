[TOC]

## Overview

TDSQL is a distributed database deployed in Tencent Cloud that has a Shared Nothing architecture and supports automatic horizontal splitting (sharding). You only need to specify the field for sharding when creating a table, and TDSQL will perform data routing and aggregation accordingly, where operations imperceptible to the database can be performed at the application layer.

### Software version

The kernel version used in this Development Manual is 1.13.21-M-V2R501D002, which can be queried by running the `/*Proxy*/show status` statement.

**Note**: TDSQL does not support versions below 4.0 and compression protocols. You are recommended to **add the `-c` option** when using the client, so that the comment passthrough feature can be used.

### Features

TDSQL is capable of horizontal scaling, making it suitable for scenarios with massive amounts of data. It has the following features:

- It supports sharded, single, and broadcast tables

- It provides a flexible read-write separation mode

- It supports global `order by`, `group by`, and `limit` operations

- It supports five aggregate functions, i.e., SUM, COUNT, AVG, MIN, and MAX

- It supports cross-set joins and subqueries

- It supports pre-processing protocols

- It supports global unique fields and sequence

- It supports distributed transactions

- It supports two-level partitioning

- It provides specific SQL statements for querying configuration and status of the entire cluster


### Use limits

A distributed instance of TDSQL is highly compatible with MySQL protocols and syntax. However, due to the notable architectural differences between distributed and standalone databases, there are some use limits on MySQL's certain features and small MySQL syntax.

**General limits on TDSQL**

- Custom functions, events, and table spaces are not supported
- Views, stored procedures, triggers, and cursors are not supported
- Foreign keys, self-built partitions, and temporary tables are not supported
- Compound statements such as BEGIN END, LOOP, and UNION are not supported
- SQL syntax related to master-slave sync is not supported

**Limits on small TDSQL syntax**

Currently, a distributed instance of TDSQL does not support some DDL, DML, and SQL management statements. The specific limits are as follows:

- DDL
  * CREATE TABLE ... SELECT is not supported 
  * CREATE TEMPORARY TABLE is not supported 
  * CREATE/DROP/ALTER SERVER/LOGFILE GROUP are not supported
  * ALTER is not supported for renaming shardkey, but it can be used to change the type
  * RENAME is not supported
- DML
  * SELECT INTO OUTFILE/INTO DUMPFILE/INTO var_name are not supported
  * query_expression_options is not supported, such as HIGH_PRIORITY/STRAIGHT_JOIN/SQL_SMALL_RESULT/ 					SQL_BIG_RESULT/SQL_BUFFER_RESULT/SQL_CACHE/SQL_NO_CACHE/SQL_CALC_FOUND_ROWS
  * Non-SELECT subqueries are not supported
  * INSERT/REPLACE without column name are not supported
  * ORDER BY/LIMIT cannot be used for global DELETE/UPDATE operations
  * UPDATE/DELETE without WHERE condition are not supported
  * LOAD DATA/XML are not supported
  * Use of DELAYED and LOW_PRIORITY in SQL is not supported
  * References of and operations on variables in SQL are not supported, such as SET @c=1, @d=@c+1; SELECT @c, @d
  * index_hint is not supported
  * HANDLER/DO are not supported
- SQL management statements
  * ANALYZE/CHECK/CHECKSUM/OPTIMIZE/REPAIR TABLE are not supported, which should be performed with passthrough syntax
  * CACHE INDEX are not supported
  * FLUSH is not supported
  * KILL is not supported (except for non-cross-AZ databases)
  * LOAD INDEX INTO CACHE is not supported
  * RESET is not supported
  * SHUTDOWN is not supported
  * SHOW BINARY LOGS/BINLOG EVENTS are not supported
  * The combination of SHOW WARNINGS/ERRORS and LIMIT/COUNT is not supported

### System connection method

TDSQL provides a connection mode compatible with MySQL through the proxy API. It can be connected using the IP address, port number, username, and password. The connection statement is as follows:

```
mysql -h10.10.10.10 -P3306 -utest12 -ptest123 -c
```

## Use of SQL Syntax

A distributed instance is highly compatible with MySQL's connection protocols and syntax and supports SSL encryption. The relevant protocols and syntax of Navicat, JDBC, ODBC, PHP, and Python are also supported, such as:

```
private final String USERNAME = "test";  
private final String PASSWORD = "123456"; 
private final String DRIVER = "com.mysql.jdbc.Driver";   
private final String URL = "jdbc:mysql://10.10.10.10:3306?userunicode=true&characterEncoding=utf8mb4";  
private Connection connection;  
private PreparedStatement pstmt;  
private ResultSet resultSet;  
```

However, due to architectural differences, there are certain restrictions on SQL statements. To better take advantage of the distributed architecture, you are advised to use the SQL protocols and syntax as recommended in this document.

### DDL statements

This section describes how to use DDL statements to create tables and explains some common DDL statements.

#### Creating a table

A distributed instance of TDSQL supports creating sharded, single, and broadcast tables.

**Note**: You are recommended to create sharded tables for use in a distributed instance if there are no special requirements.

**Create a sharded table**

A sharded table is generated through automatic horizontal splitting (sharding). Sharding is a technical scheme where data is distributed in a way similar to consistency hashing to different physical node sets according to the hash value of the shardkey. If two tables have the same shardkey, their corresponding rows will be stored in the same physical node set. This scenario is called Groupshard, which greatly improves the processing efficiency of statements such as join queries at the application layer.

When creating a regular sharded table, you must specify the value of the shardkey at the end, which is a field name in the table and will be used for subsequent SQL routing. Below is a sample statement:

```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
Query OK, 0 rows affected (0.07 sec)
```

In a distributed instance, a shardkey corresponds to the partition field of the backend database, so it must be part of the primary key and all unique indices; otherwise, the table cannot be created. Below is an example:

```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;

At this point, there is a unique index `u_2` that does not contain the shardkey, so the table cannot be created, and the following error will be displayed:
ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function
Because the index of the primary key or unique key has to be globally unique, to implement a globally unique index, you must include the shardkey field.
```

**In sum, the main requirements on the shardkey field are as follows:**

- The shardkey field must be part of the primary key and all unique indices;
- The type of the shardkey field must be int, bigint, or smallint/char/varchar;
- The value of the shardkey field should not contain Asian characters, as the proxy will not convert the character set, and different character sets may be routed to different partitions;
- Do not update the value of the shardkey field;
- `Shardkey=a` should be placed at the end of the SQL statement;
- The shardkey field should be carried if possible when data is accessed; otherwise, SQL statements without shardkey will be routed to all nodes and thus consume more resources.

**Note**: Some sharding schemes allow a "non-primary or non-unique key" to be the shardkey field, which, however, may lead to data inconsistency and is therefore prohibited in TDSQL by default.

**Create a broadcast table**

Broadcast tables are based on small table broadcasting technology. After a broadcast table is created, its full data is available to every node, and all its operations will be broadcast to all physical shards (sets).

Broadcast tables can improve the performance of cross-set joins while ensuring the atomicity of modification operations, so that the data in all sets is exactly identical. This type of tables is mainly used as configuration tables. The statement is as follows:

```
mysql> create table global_table ( a int, b int key) shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.06 sec)
```

**Create a regular table**

Regular table: This is also known as a regular table (non-sharded table), which does not need to be specifically sharded or processed, as it uses exactly the same syntax as MySQL. Currently, the full data of this type of table is stored in the first physical node set by default. The statement is as follows:

```
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)
```

**Note**: As a non-sharded table is stored in the physical node set by default, if there are too many of them, the first physical node set will be under excessive load.

#### Other DDL statements

Other DDL statements such as ALTER and DROP use exactly the same syntax as MySQL, so they will not be detailed in this document.



### Account and permission statements

TDSQL supports account and permission configuration in the following two ways:

- Chitu management platform. For more information on how to grant permissions in this way, see TDSQL Chitu Management Platform User Guide.
- SQL. The following describes how to grant permissions via SQL.

SQL authorization method: The proxy supports permission control on the command line. SQL sends the parsed task to the decision-making cluster (ZooKeeper) first, then the scheduling cluster (Scheduler) completes the task and returns the response, and finally the proxy returns it to the client.

TDSQL supports commands for creating/altering/dropping/renaming a user account, setting a password, granting permissions, and revoking permissions. The statements are as follows:

**CREATE USER statement**

```
CREATE USER [IF NOT EXISTS]
user [auth_option] [, user [auth_option]] ... 

auth_option: {
IDENTIFIED BY 'auth_string'
| IDENTIFIED BY PASSWORD 'hash_string'
}
```

**Note**: The `tls_option`, `resource_option`, `password_option`, and `lock_option` commands are not supported currently.

**DROP USER statement**

```
 DROP USER [IF EXISTS] user [, user] ...
```

**ALTER USER statement**

```
ALTER USER [IF EXISTS]
user [auth_option] [, user [auth_option]] ...

auth_option: {
IDENTIFIED BY 'auth_string'
| IDENTIFIED BY PASSWORD 'hash_string'
}
```

**Note**: MariaDB versions below 10.2 do not support the `ALTER USER` command.

**RENAME USER statement**

```
RENAME USER old_user TO new_user [, old_user TO new_user] ...
```

**SET PASSWORD statement**

```
SET PASSWORD FOR user = password_option

password_option: { 'auth_string'
| PASSWORD('auth_string')
}
```

**Note**: The password must be set for the user and cannot be left blank.

Below is an example:

```
set password for test1@'10.10.*' = 'test';

set password for test1@'10.10.*' = password('test');
```

**GRANT statement**

```
GRANT
priv_type [(column_list)] [, priv_type [(column_list)]] ...
ON [object_type] priv_level
TO user [auth_option] [, user [auth_option]] ... 
[WITH GRANT OPTION]

object_type: { TABLE
| FUNCTION
| PROCEDURE }

priv_level: { *
| *.*
| db_name.*
| db_name.tbl_name
| tbl_name
| db_name.routine_name
}

auth_option: {
IDENTIFIED BY 'auth_string'
|IDENTIFIED BY PASSWORD 'hash_string'
}

```

**Note**: The GRANT statement is compatible with MySQL syntax. The `tls_option` and `resource_option` commands are not supported currently.	

Below is an example:

```
grant all on *.* to test1@'%' identified by 'test123'

grant all on *.* to test2@'%' identified by 'test',
test3 identified by password '*94E7199DCF1F8F391A73B989F90B147EDAF3908E' 
with grant option

grant select (col1), insert (col1, col2) on mydb.mytbl to 'someuser'@'somehost';

grant execute on procedure mydb.myproc to 'someuser'@'somehost';

```

**REVOKE statement**

```
REVOKE
priv_type [(column_list)] [, priv_type [(column_list)]] ... 
ON [object_type] priv_level
FROM user [, user] ...

REVOKE ALL [PRIVILEGES], GRANT OPTION 
FROM user [, user] ...

```

Below is an example:

```
revoke all,grant option from test1

revoke select,insert on db1.* from test2@'10.*';
```



### DML statements

This section describes commonly used commands in DML statements such as SELECT, INSERT, REPLACE, UPDATE, and DELETE.

**SELECT command**

It is recommended to add the shardkey field in the condition when running the SELECT command.

**Note**: The proxy routes the request made with the SQL command to the corresponding database instance based on the hash value of the field; otherwise, the SQL command will send the request to all database instances in the cluster, and then the proxy will aggregate all the result sets returned by the databases, which affects the efficiency of execution.

```
mysql> select * from test1 where a=2;
+------+------+---------+
| a    | b    | c       |
+------+------+---------+
|    2 |    3 | record2 |
|    2 |    4 | record3 |
+------+------+---------+
2 rows in set (0.00 sec)
```

**INSERT/REPLACE commands**

The shardkey field must be included when running the INSERT/REPLACE commands; otherwise, the system will refuse to execute the SQL commands, as the proxy cannot determine the position of the backend database node in the SQL statement. The statement is as follows:

```
mysql> insert into test1 (b,c) values(4,"record3");
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table insert must has field spec

mysql> insert into test1 (a,c) values(4,"record3");
Query OK, 1 row affected (0.01 sec)
```

**DELETE/UPDATE commands**

For security considerations, **during the execution of the DELETE/UPDATE commands in a sharded or broadcast table, a `where` condition must be present**; otherwise, the SQL commands will be refused. The statement is as follows:

```
mysql> delete from test1;
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table delete/update must have a where condition

mysql> delete from test1 where a=1;
Query OK, 1 row affected (0.01 sec)
```

**Note**: To prevent faulty operations, it is recommended not to use the DELETE/UPDATE commands on the entire table; if they have to be used, a `where 1` condition can be added to the SQL statement.

## Comment Passthrough

Comment passthrough refers to the operation that passes through an SQL statement to one or more corresponding physical shards (sets) and the set corresponding to the shardkey.

For distributed instances, the proxy will parse the SQL syntax, but there are relatively strict restrictions. If you want to execute an SQL statement in a certain physical shard (set), you can use this feature. The statement is as follows:

```
MySQL [test]> delete from s ;
ERROR 664 (HY000): Proxy ERROR:SQL is too complex, only applicable to noshard table: Shard table delete/update must have a where clause
MySQL [test]> /*sets:allsets*/delete from s;
Query OK, 0 rows affected (0.02 sec)
```

The syntax is as follows:

```
/*sets:set_1*/
/*sets:set_1,set_2*/ (The name of the set can be queried by /*proxy*/show status)
/*sets:allsets */   
/*shardkey:10*/ 
```

**Note**: When the SQL statement is passed through to perform write operations, the proxy will not parse the SQL statement, so if it is a passthrough write operation to two or more sets, distributed transactions will not be used by the system, which may cause data inconsistency. Therefore, it is recommended to pass through to only one set during one write operation.

## Joins and Subqueries

For distributed instances, the data is split horizontally across nodes. To improve the performance, you should prioritize the table structure and SQL statement optimization at the application layer to avoid cross-node data storage.

- If join-related tables have the equal condition of shardkey (as shown below), this part of data will be automatically stored to the same physical node based on the sharding consistency principle, making joins work as standalone ones with higher data processing efficiency, which is thus recommended.
- If it involves data across physical nodes, the proxy will pull data from other nodes and cache it first. Due to the network data transmission, the data processing efficiency will be affected.

### Recommended join methods

**Join between sharded tables**

If a join is performed between sharded tables that have the equal condition of shardkey, it will work as a standalone one with no performance loss. The statement is as follows:

```sql
MySQL > select * from test1 join test2 where test1.a=test2.a;     
+---+------+---------+---+------+---------------+
| a | b    | c       | a | d    | e             |
+---+------+---------+---+------+---------------+
| 1 |    2 | record1 | 1 |    3 | test2_record1 |
| 2 |    3 | record2 | 2 |    3 | test2_record2 |
+---+------+---------+---+------+---------------+
2 rows in set (0.00 sec)

MySQL > select * from test1 left join test2 on test1.a<test2.a where test1.a=1;
+---+------+---------+------+------+---------------+
| a | b    | c       | a    | d    | e             |
+---+------+---------+------+------+---------------+
| 1 |    2 | record1 |    2 |    3 | test2_record2 |
+---+------+---------+------+------+---------------+
1 row in set (0.00 sec)
```

**Join between non-sharded tables**

If a join is performed between non-sharded tables, it will work as a standalone one with no performance loss. The statement is as follows:

```sql
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)

mysql> create table noshard_table_2 ( a int, b int key);
Query OK, 0 rows affected (0.00 sec)

mysql> select * from noshard_table,noshard_table_2;
Empty set (0.00 sec)

mysql> insert into noshard_table (a,b) values(1,2),(3,4);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> insert into noshard_table_2 (a,b) values(10,20),(30,40);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from noshard_table,noshard_table_2;
+------+---+------+----+
| a    | b | a    | b  |
+------+---+------+----+
|    1 | 2 |   10 | 20 |
|    3 | 4 |   10 | 20 |
|    1 | 2 |   30 | 40 |
|    3 | 4 |   30 | 40 |
+------+---+------+----+
4 rows in set (0.00 sec)
```

**Join between sharded and broadcast tables**

If a join is performed between sharded and broadcast tables, it will work as a standalone one with no performance loss. The statement is as follows:

```sql
 MySQL> create table global_test(a int key, b int)shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.00 sec)

MySQL> insert into global_test(a, b) values(1,1),(2,2);
Query OK, 2 rows affected (0.00 sec)

MySQL> select * from test1, global_test;
+---+------+---------+---+------+
| a | b    | c       | a | b    |
+---+------+---------+---+------+
| 1 |    2 | record1 | 1 |    1 |
| 2 |    3 | record2 | 1 |    1 |
| 1 |    2 | record1 | 2 |    2 |
| 2 |    3 | record2 | 2 |    2 |
+---+------+---------+---+------+
4 rows in set (0.00 sec)
```

### Subqueries

Currently, TDSQL only supports derived table queries with the shardkey field, which involves no performance loss. The statement is as follows:

```
mysql> select a from (select * from test1 where a=1) as t;
+---+
| a |
+---+
| 1 |
+---+
1 row in set (0.00 sec)


```

### Complex SQL queries

For SQL statements that cannot meet the requirements of the recommended statements, cross-node data interaction is required, which will undermine the performance and may affect the following queries:

- Queries with subqueries.
- Queries with `HAVING` condition.
- Queries where multiple sort/group/deduplication operations are required, such as Count (Distinct ID).
- Join queries for multiple tables where the partition fields (shardkey) of the participating tables are different or the tables are of different types (for example, non-sharded tables and sharded tables).

For such complex queries, the data that participates in the query is extracted from the backend database and stored in the local temporary table through condition pushdown, and then the data in the temporary table is computed.

Therefore, you need to specify the conditions of the tables participating in the query to avoid performance degradation due to the extraction of large amounts of data. The statement is as follows:

```sql
mysql> create table test1 ( a int key, b int, c char(20) ) shardkey=a;
Query OK, 0 rows affected (1.56 sec)

mysql> create table test2 ( a int key, d int, e char(20) ) shardkey=a;
Query OK, 0 rows affected (1.46 sec)

mysql> insert into test1 (a,b,c) values(1,2,"record1"),(2,3,"record2");
Query OK, 2 rows affected (0.02 sec)

mysql> insert into test2 (a,d,e) values(1,3,"test2_record1"),(2,3,"test2_record2");
Query OK, 2 rows affected (0.02 sec)

mysql> select * from test1 join test2 on test1.b=test2.d;
+---+------+---------+---+------+---------------+
| a | b    | c       | a | d    | e             |
+---+------+---------+---+------+---------------+
| 2 |    3 | record2 | 1 |    3 | test2_record1 |
| 2 |    3 | record2 | 2 |    3 | test2_record2 |
+---+------+---------+---+------+---------------+
2 rows in set (0.00 sec)

MySQL> select * from test1 where test1.a in (select a from test2);        
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
| 2 |    3 | record2 |
+---+------+---------+
2 rows in set (0.00 sec)

MySQL> select * from test1 where exists (select * from test2 where test2.a=test1.b);
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
+---+------+---------+
1 row in set (0.00 sec)

MySQL> select a, count(1) from test1 where exists (select * from test2 where test2.a=test1.a) group by a;        
+---+----------+
| a | count(1) |
+---+----------+
| 1 |        1 |
| 2 |        1 |
+---+----------+
2 rows in set (0.00 sec)

MySQL> select distinct count(1) from test1 where exists (select * from test2 where test2.a=test1.a) group by a;   
+----------+
| count(1) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)

MySQL> select count(distinct a) from test1 where exists (select * from test2 where test2.a=test1.a);        
+-------------------+
| count(distinct a) |
+-------------------+
|                 2 |
+-------------------+
1 row in set (0.00 sec)
```

## Notes on Distributed Transactions

As the data manipulated by a transaction usually spans across multiple physical nodes, in a distributed database, a similar scheme is called a distributed transaction. TDSQL supports regular and XA distributed transactions. TDSQL (v5.7 and above) supports distributed transactions by default and makes them imperceptible to the client, so that they can be used conveniently just like standalone transactions.

Distributed transactions in TDSQL adopt a two-phase commitment algorithm (2PC) to ensure the atomicity and consistency of transactions, with an isolation level configured as `Read committed`, `Repeatable read`, or `Serializable`.

**Regular distributed transactions**

```
begin; 	# Start a transaction
... 	# Non-DDL operations such as cross-set CRUD
commit; # Commit the transaction
```

**XA distributed transactions**

Based on MySQL's support for XA transactions, TDSQL provides strong consistency support for XA distributed transactions, delivering an experience comparable to standalone transactions. The statement is as follows:

```
xa begin ''; 		# Start an XA transaction, where the transaction identifier is generated internally by the system; therefore, you can pass in an empty string
...			 		# Non-DDL operations such as cross-set CRUD
select gtid();		# Get the ID of the current XA transaction, which is assumed as 'xid' below
xa prepare 'xid';	# Prepare the transaction
xa commit/rollback 'xid'; # Commit or roll back the transaction
```

**New transaction API status description**

| API | Description |
| ----------------------------- | ------------------------------------------------------------ |
| select gtid() | Gets the globally unique ID (gtid) of the current distributed transaction. If the transaction is not a distributed transaction, a null value will be returned.<br />The ID of a regular distributed transaction is in the format of `'gateway id'-'proxy random value'-'serial number'-'timestamp'-'partition number'`, <br />such as c46535fe-b6-dd-595db6b8-25<br />The ID of an XA distributed transaction is in the format of `'ex'-'gateway id'-'proxy random value'-'serial number'-'timestamp'-'partition number'`, <br />such as ex-c46535fe-b6-dd-595db6b8-25 |
| select gtid_state("transaction ID") | Used to get the transaction status after an exception occurs in transaction committing (3 seconds by default). Possible results include: <br />**COMMIT**, indicating that the transaction has been or will eventually be committed. <br />**ABORT**, indicating that the transaction will eventually be rolled back. <br />**Empty**. As the status of the transaction will be cleared after an hour, there are two possibilities: (1) when you query after one hour, the transaction status has been cleared; (2) when you query within one hour, the identified transaction will eventually be rolled back. |
| xa boost (transaction ID) | After an exception occurs in regular transaction commit, the transaction will be automatically committed or rolled back by the backend component in a certain period of time (30 seconds by default). If you are unwilling to wait, you can repeatedly call this API to make the system commit or roll back the transaction timely. |
| xa lockwait | Displays the wait relationship of the current distributed transaction (you can use the `dot` command to convert the output to a wait-for graph). |
| xa show | Shows the distributed transactions that are currently running on the gateway |

## Use of Globally Unique Numerical Sequence

TDSQL supports the globally unique digital sequence (auto_increment). Currently, it can ensure the global uniqueness and increment of auto-incrementing fields, but not the monotonic increment (i.e., absolute increment in chronological order).

The `auto_increment` here is 8 bytes in length with 18446744073709551616 being the maximum value, so you don't need to worry about value overflow. It can be used in the following way:

**Create a table with auto-incrementing fields**

	mysql> create table auto_inc (a int,b int,c int auto_increment,d int,key auto(c),primary key p(a,d)) shardkey=d;
	Query OK, 0 rows affected (0.12 sec)

**Creating a sharded table with auto-incrementing fields**

	mysql>  insert into shard.auto_inc ( a,b,d,c) values(1,2,3,0),(1,2,4,0);
	Query OK, 2 rows affected (0.05 sec)
	Records: 2  Duplicates: 0  Warnings: 0
	
	mysql> select * from shard.auto_inc;
	+---+------+---+---+
	| a | b    | c | d |
	+---+------+---+---+
	| 1 |    2 | 2 | 4 |
	| 1 |    2 | 1 | 3 |
	+---+------+---+---+
	2 rows in set (0.03 sec)

**Fill in auto-increment holes**

As `auto_increment` ensures only the global uniqueness and increment of auto-incrementing fields, if a process such as node switching or restarting occurs, there will be holes in the middle of the auto-incrementing fields, for example:

    mysql> insert into shard.auto_inc ( a,b,d,c) values(11,12,13,0),(21,22,23,0);
    Query OK, 2 rows affected (0.03 sec)
    mysql> select * from shard.auto_inc;
    +‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
    | a | b | c | d |
    +‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
    | 21 | 22 | 2002 | 23 |
    | 1 | 2 | 2 | 4 |
    | 1 | 2 | 1 | 3 |
    | 11 | 12 | 2001 | 13 |
    +‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
    4 rows in set (0.01 sec)

The current value can be modified using the following command:

	alter table auto_inc auto_increment=100

**Note**: The insertion of data through the `insert into auto_inc set c=100` syntax is currently not supported. If you want to specify an auto-incrementing value, you need to use the

`insert into auto_inc (c) values(100)` syntax.

**Get auto-incrementing values via the `select last_insert_id()` command**

If you do not specify the auto-incrementing value, it can be obtained via the `select last_insert_id()` command. Obtaining it directly from the return packet of the insert is currently not supported. Specifically:

```
mysql> insert into auto_inc ( a,b,d,c) values(1,2,3,0),(1,2,4,0);
Query OK, 2 rows affected (0.73 sec)
	
mysql> select * from auto_inc;
+---+------+------+---+
| a | b    | c    | d |
+---+------+------+---+
| 1 |    2 | 4001 | 3 |
| 1 |    2 | 4002 | 4 |
+---+------+------+---+
2 rows in set (0.00 sec)

mysql> select last_insert_id();
+------------------+
| last_insert_id() |
+------------------+
| 4001             |
+------------------+
1 row in set (0.00 sec)
```

**Note**: Currently, the `select last_insert_id()` command can only be used for the auto-incrementing fields in sharded and broadcast tables but not non-sharded tables.

## SEQUENCE

 This section describes how to create, drop, query, and use a sequence and get its value. The sequence syntax is compatible with MariaDB, but the sequence should be globally incremental and unique.

**Note**:

- To prevent users from using the `sequence` keyword, the proxy must prefix the keyword with `tdsql_` starting from this version. If you are using an unprefixed keyword, you need to modify it on your own or submit a ticket.
- The current sequence is used to guarantee the global uniqueness of the distributed transaction, which has a relatively low performance and is therefore only suitable for scenarios with low concurrency.

**Creating a sequence**

```
create tdsql_sequence test.s1 start with 12 tdsql_minvalue 10 maxvalue 50000  tdsql_increment by 5  tdsql_nocycle 
create tdsql_sequence test.s2 start with 12 tdsql_minvalue 10 maxvalue 50000  tdsql_increment by 1  tdsql_cycle 

The above SQL statements include five parameters: start value, minimum value, maximum value, increment, and whether to cycle, all of which should be positive integers.
```

 **Drop a sequence**

```
drop tdsql_sequence test.s1
```

**Query a sequence**

```
show create tdsql_sequence test.s2
```

**Use a sequence**

The statement for using a sequence to get the next value is as follows:

```
select tdsql_nextval(test.s2)
select next value for test.s2
```

------

  Below is an example:

```
mysql> select tdsql_nextval(test.s1);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.18 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.13 sec)

mysql> select tdsql_nextval(test.s1);
+----+
| 17 |
+----+
| 17 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 13 |
+----+
| 13 |
+----+
1 row in set (0.00 sec)

mysql> select next value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.01 sec)

```

The `nextval` command can be used in INSERT statements, as shown below:

```
mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
+----+------+
1 row in set (0.00 sec)

mysql> insert into test.t1(a,b) values(tdsql_nextval(test.s2),3);
Query OK, 1 row affected (0.01 sec)

mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
| 14 |    3 |
+----+------+
2 rows in set (0.00 sec)
```

The last value is needed to connect to the related data; if it has never been obtained with the `nextval` command, 0 will be returned.

```
select tdsql_lastval(test.s1)
select tdsql_previous value for test.s1;
```

------

```
mysql> select tdsql_lastval(test.s1);
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)

mysql> select tdsql_previous value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)
```

Set the next value for the sequence, which must be greater than the current value; otherwise, 0 will be returned.

```
select tdsql_setval(test.s2,1000,bool use)  //  `use` is 1 by default, indicating that the value of 1,000 has been used and will not be included next time. If this is 0, the next return will start from 1,000.
```

If the next value of the sequence is smaller than the current value, the system will make no response.

```
mysql> select tdsql_nextval(test.s2);
+----+
| 15 |
+----+
| 15 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_setval(test.s2,10);
+---+
| 0 |
+---+
| 0 |
+---+
1 row in set (0.03 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 16 |
+----+
| 16 |
+----+

```

If the next value set is larger than the current value, the current value will be successfully returned.

```
mysql> select tdsql_setval(test.s2,20);
+----+
| 20 |
+----+
| 20 |
+----+
1 row in set (0.02 sec)
mysql> select tdsql_nextval(test.s2);
+----+
| 21 |
+----+
| 21 |
+----+
1 row in set (0.01 sec)
```

## Data Import and Export

- **Data export**

​       Data can be exported by running the `mysqldump` command and setting the `net_write_timeout` parameter in the TDSQL Console: set global net_write_timeout=28800.


```
mysqldump --compact --single-transaction --no-create-info -c
               db_name table_name  -utest -h10.10.10.10 -P3336  -ptest123
               
Note: Please select the database name and table name parameters as needed.
```

**Note**: If the exported data is to be imported into other TDSQL environments, the `-c` option must be added.

- **Data import**

​        A dedicated import tool is provided to complete the import of data corresponding to the load data outfile. The statement is as follows:

```
[tdengine@TENCENT64 ~/]$./load_data

format:./load_data mode0/mode1 proxy_host proxy_port user password db_table shardkey_index file field_terminate filed_enclosed

    example:./load_data mode1 10.10.10.10 3336 test test123 shard.table  1 '/tmp/datafile'  ' ' ''

This tool works by sharding the source file into multiple files according to the routing rule of the shardkey, and then passing through each file to the corresponding backend database.

  Notes: 1. The source file must use '\n' as a line break.
	 2. `mode0` only shards the source file with no data import, which is generally used for debugging. For data import, use the `mode1` command.
	 3. `shardkey_index` starts from 0. If shardkey is in the second field, `shardkey_index` will be 1.
```

## Pre-processing Protocols

TDSQL supports pre-processing protocols, which are used in the same way as in standalone MySQL, for example:

- PREPARE Syntax
- EXECUTE Syntax

Supported binary protocols:

- COM_STMT_PREPARE
- COM_STMT_EXECUTE

Below is an example:

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

**Note**: Currently, TDSQL is only compatible with PREPARE/EXECUTE statement syntax, which is not recommended for distributed databases. For higher performance, text protocols can be used.

## Two-level Partitioning

Two-level partitioning means to partition data of specific conditions. TDSQL supports two-level partitioning in range and list formats where the specific table creating syntax is similar to the partitioning syntax in MySQL.

TDSQL only uses the HASH method to shard data, which is not convenient for deleting old data of specific conditions (e.g., transactional data). To solve this problem, the two-level partitioning syntax can be used.

**Note**: Partitioning uses the less than symbol "<"; therefore, if you want to store the data of the current year (e.g., 2017), you need to create a partition less than the next year (e.g., <2018). You only need to create partitions up to the current time, and TDSQL will automatically add subsequent partitions (3 by default). Take YEAR as an example. TDSQL will automatically create 3 partitions (2018, 2019, and 2020) and increase or decrease them afterwards.

- **Supported range types**

	- DATE, DATETIME, and TIMESTAMP
	  	 - `year`, `month`, and `day` functions are supported. If the function is empty, it will be defaulted to the `day` function
	
	- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT
	  	- `year`, `month`, and `day` functions are supported. The value entered is converted to year, month, and day and then compared against the sharded table information
	
	If the function is empty, this `int` value will be compared against the sharded table information.

Below is an example:

If `hired` is of `date` type, the query for the corresponding value inserted is in the format of `'20160101 10:20:20' ,20160101`. The statement is as follows:

	CREATE TABLE employees_int (
	    id INT key NOT NULL,
	    fname VARCHAR(30),
	    lname VARCHAR(30),
	    hired date,
	    separated DATE NOT NULL DEFAULT '9999-12-31',
	    job_code INT,
	    store_id INT
	)
	shardkey=id 
	PARTITION BY RANGE ( month(hired) ) (
	    PARTITION p0 VALUES LESS THAN (199102),
	    PARTITION p1 VALUES LESS THAN (199603),
	    PARTITION p2 VALUES LESS THAN (200101)
	);

If `hired` is of `int` type, the query for the corresponding value inserted will be in the format of `1474961034`. The proxy will first convert it into the corresponding date format (20160927) and then compare it against the sharded table information. The statement is as follows:

	CREATE TABLE employees_int (
	    id INT key NOT NULL,
	    fname VARCHAR(30),
	    lname VARCHAR(30),
	    hired int,
	    separated DATE NOT NULL DEFAULT '9999-12-31',
	    job_code INT,
	    store_id INT
	)
	shardkey=id 
	PARTITION BY RANGE ( month(hired) ) (
	    PARTITION p0 VALUES LESS THAN (199102),
	    PARTITION p1 VALUES LESS THAN (199603),
	    PARTITION p2 VALUES LESS THAN (200101)
	);

- **Supported list types**

	- DATE，DATETIME，TIMESTAMP     - year, month, and day functions are supported
	
	- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT
	
	- CHAR, VARCHAR, BINARY, and VARBINARY
	
	Below is an example:
	
	```
	 CREATE TABLE customers_1 (
	    first_name VARCHAR(25) key,
	    last_name VARCHAR(25),
	    street_1 VARCHAR(30),
	    street_2 VARCHAR(30),
	    city VARCHAR(15),
	    renewal DATE
	) shardkey=first_name
	PARTITION BY LIST (city) (
	    PARTITION pRegion_1 VALUES IN('1', '2', '3'),
	    PARTITION pRegion_2 VALUES IN('4', '5', '6'),
	    PARTITION pRegion_3 VALUES IN('7', '8', '9'),
	    PARTITION pRegion_4 VALUES IN('10', '11', '12')
	);
	```

**Drop/add a secondary partition**

Dropping or adding a secondary partition is in the same format as in standalone MySQL. The statement is as follows:

```
alter table customers_1 drop partition pRegion_1;

alter table customers_1 add partition (partition pRegion_5 VALUES IN('13', '14', '15'));
```

**Note**: TDSQL does not support other partitioning operations than RANGE and LIST, such as REORGANIZE.

## Read-write Separation

Read-write separation is to separate read and write capabilities by letting the master node handle transactional operations, such as INSERT, UPDATE, and DELETE, and the slave nodes perform SELECT operations, thereby reducing the master node's data processing pressure.

TDSQL supports read-write separation by default. Each slave in the master-slave architecture can be read-only. If multiple slaves are configured, read requests will be automatically assigned to low-load slaves by TProxy to support the read traffic of large applications.

Three read-write separation schemes are supported.

- The proxy enables the syntax parsing configuration, filters out user-selected read requests through syntax parsing, and sends them directly to the slave by default.

- A slave comment flag can be added to send the specified SQL command to the slave, i.e., adding the `/*slave*/` flag in the query, so that the query will be sent to the slave.

  ​      **Note**: `/*slave:slaveonly*/`,` /*slave:20*/`, and ` /*slave:slaveonly,20*/` are also supported, where the value indicates the delay that the slave should satisfy, and `slaveonly` indicates that the query will not be sent to the master if there is no eligible slave.

- Read-only accounts can be created, from which requests are sent to the slave according to the configured attributes.

## Connection Protection

Connection protection keeps the connection intact between the client and the gateway when the gateway is disconnected from the backend database (for example, a master-slave switch occurs in the backend database). The protection process is as follows:

- If the proxy is disconnected from the database while executing SQL statements, the proxy will close all connections related to the SQL (except the one between the proxy and the client) and display the following error:

```c++
ER_PROXY_TRANSACTION_ERROR // Transaction in process
ER_PROXY_CONN_BROKEN_ERROR // Non-transactional status
```

- If the proxy is disconnected from the database and your session is in a `regular transaction` status, the following process actions will be executed (all the error codes below are `ER_PROXY_TRANSACTION_ERROR`):

```sequence
Non-transactional status --> transaction in progress (ACTIVE): BEGIN
Transaction in progress (ACTIVE) --> ROLLBACK ONLY status: Connection between the proxy and the database closed
ROLLBACK ONLY status --> ROLLBACK ONLY status: SQL (an error is returned requiring you to roll back the transaction)

ROLLBACK ONLY status --> transaction rolled back: ROLLBACK / BEGIN
ROLLBACK ONLY status --> transaction rolled back: COMMIT (the proxy returns an error message prompting that the transaction has been rolled back)

ROLLBACK ONLY status --> user connection closed: timeout
```

- If you are in an `XA transaction` status when the proxy is disconnected from the backend, the following process actions will be executed (all the error codes below are `ER_PROXY_TRANSACTION_ERROR`):

```sequence
Non-transactional status -> transaction in progress (ACTIVE, IDLE): XA BEGIN ''
Transaction in progress (ACTIVE、IDLE) --> ROLLBACK ONLY status: Connection between the proxy and the database closed
ROLLBACK ONLY status --> ROLLBACK ONLY status: ordinary SQL / XA COMMIT 'xid' (error)
ROLLBACK ONLY status -> ROLLBACK status: XA ROLLBACK 'xid'

Transaction in progress (ACTIVE, IDLE) --> PREPARED status: XA PREPARE 'xid'
PREPARED status --> PREPARED status: Connection between the proxy and the database (or client) closed
PREPARED status -> ROLLBACK status: XA ROLLBACK 'xid'
PREPARED status -> COMMIT status: XA COMMIT 'xid'
ROLLBACK ONLY status --> user connection closed: timeout
```

- When you are in a transaction in progress but the proxy is disconnected from the database, if you haven't rolled back the transaction before the `timeout` time, the proxy will disconnect from you. The timeout parameter in the proxy configuration file is as follows:

```json
<server_close timeout="60"/>

```

## Database Management Statements

You can view the configuration and status of the proxy through SQL statements. The following commands are supported:

```
mysql> /*proxy*/help;
+-----------------------+-------------------------------------------------------+
| command               | description                                           |
+-----------------------+-------------------------------------------------------+
| show config           | show config from conf                                 |
| show status           | show proxy status,like route,shardkey and so on       |
| set sys_log_level=N   | change the sys debug level N should be 0,1,2,3        |
| set inter_log_level=N | change the interface debug level N should be 0,1      |
| set inter_time_open=N | change the interface time debug level N should be 0,1 |
| set sql_log_level=N   | change the sql debug level N should be 0,1            |
| set slow_log_level=N  | change the slow debug level N should be 0,1           |
| set slow_log_ms=N     | change the slow ms                                    |
| set log_clean_time=N  | change the log clean days                             |
| set log_clean_size=N  | change the log clean size in GB                       |
+-----------------------+-------------------------------------------------------+
10 rows in set (0.00 sec)

mysql> /*proxy*/show config;
+-----------------+--------------------+
| config_name     | value              |
+-----------------+--------------------+
| version         | V2R120D001         |
| mode            | group shard        |
| rootdir         | /shard_922         |
| sys_log_level   | 0                  |
| inter_log_level | 0                  |
| inter_time_open | 0                  |
| sql_log_level   | 0                  |
| slow_log_level  | 0                  |
| slow_log_ms     | 1000               |
| log_clean_time  | 1                  |
| log_clean_size  | 1                  |
| rw_split        | 1                  |
| ip_pass_through | 0                  |
+-----------------+--------------------+
14 rows in set (0.00 sec)

mysql> /*proxy*/show status;
+-----------------------------+------------------------------------------------------------------------------+
| status_name                 | value                                                                        |
+-----------------------------+------------------------------------------------------------------------------+
| cluster                     | group_1499858910_79548                                                       |
| set_1499859173_1:ip         | 10.*.*.*:5025;10.*.*.*:5025@1@IDC_4@0,10.*.*.*:5025@1@IDC_2@0 |
| set_1499859173_1:hash_range | 0---31                                                                       |
| set_1499911640_3:ip         | 10.*.*.*:5026;10.*.*.*:5026@1@IDC_4@0,10.*.*.*:5026@1@IDC_2@0 |
| set_1499911640_3:hash_range | 32---63                                                                      |
| set                         | set_1499859173_1,set_1499911640_3                                            |
```

Meanwhile, the proxy enhances the return result of `explain`, and the SQL statement modified by the proxy is displayed. The statement is as follows:

```
mysql> explain select * from test1;
+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
| id   | select_type | table | type | possible_keys | key  | key_len | ref  | rows | Extra | info                                    |
+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
|    1 | SIMPLE      | test1 | ALL  | NULL          | NULL | NULL    | NULL |   16 |       | set_2,explain select * from shard.test1 |
|    1 | SIMPLE      | test1 | ALL  | NULL          | NULL | NULL    | NULL |   16 |       | set_1,explain select * from shard.test1 |
+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
2 rows in set (0.03 sec)
```

## Supported Language Structures

A distributed instance supports all text formats used by MySQL, including:

- String Literals
- Numeric Literals
- Date and Time Literals
- Hexadecimal Literals
- Bit-Value Literals
- Boolean Literals
- NULL Values

**String Literals**

A string literal is a sequence of bytes or characters enclosed in single quotation marks `'` or double quotation marks `"`. Currently, TDSQL does not support `ANSI_QUOTES SQL MODE`. Strings enclosed in double quotation marks `"` are always treated as string literals rather than identifiers.

The `character set introducer` format is not supported, i.e., `[_charset_name]'string' [COLLATE collation_name]`.

Supported escape characters include:

```
\0: ASCII NUL (X’00’) character
\': single quotation mark
\": double quotation mark
\b: Backspace character
\n: Link break
\r: Carriage return
\t: Tab
\z: ASCII 26 (Ctrl + Z)
\\: backslash\
\%: \%
\_: _
```

**Numeric Literals**

Numeric literals include integers, decimal-point numbers, and floating-point numbers.

An integer can contain a decimal separator "." and begin with a plus sign "+" or a minus sign "-" indicating whether it is a positive or negative number.

Exact numeric literals can be expressed in various formats, such as 1, .2, 3.4, -5, -6.78, and +9.10.

Scientific notation in the format of 1.2E3, 1.2E-3, -1.2E3, and -1.2E-3.

**Date and Time Literals**

Date supports the following formats:

```
'YYYY-MM-DD' or 'YY-MM-DD'
'YYYYMMDD' or 'YYMMDD'
YYYYMMDD or YYMMDD

Examples: '2012-12-31', '2012/12/31', '2012^12^31', '2012@12@31', '20070523', '070523' 
```

Datetime and Timestamp support the following formats:

```
'YYYY-MM-DD HH:MM:SS' or 'YY-MM-DD HH:MM:SS'
'YYYYMMDDHHMMSS' or 'YYMMDDHHMMSS'
YYYYMMDDHHMMSS or YYMMDDHHMMSS 

Examples: '2012-12-31 11:30:45', '2012^12^31 11+30+45', '2012/12/31 11*30*45', '2012@12@31 11^30^45', 19830905132800 
```

**Hexadecimal Literals**

Hexadecimal Literals support the following formats:

```
X'01AF'
X'01af'
x'01AF'
x'01af'
0x01AF
0x01af
```

**Bit-Value Literals**

Bit-Value Literals support the following formats:

```
b'01'
B'01'
0b01
```

**Boolean Literals**

Constants `TRUE` and `FALSE` are equal to 1 and 0 respectively, which are case-insensitive.

```
mysql>  SELECT TRUE, true, FALSE, false;
+------+------+-------+-------+
| TRUE | TRUE | FALSE | FALSE |
+------+------+-------+-------+
|    1 |    1 |     0 |     0 |
+------+------+-------+-------+
1 row in set (0.03 sec)
```

**NULL Values**

NULL implies the absence of any value. It is case-insensitive and has the same meaning as the `\N` command (case-insensitive).

Note that NULL does not mean the same as 0 or the empty string ('').

## Supported Character Sets and Time Zones

TDSQL supports all character sets and character sequences of MySQL on the backend storage, as shown below:

```
mysql> show character set;
+----------+---------------------------------+---------------------+--------+
| Charset  | Description                     | Default collation   | Maxlen |
+----------+---------------------------------+---------------------+--------+
| big5     | Big5 Traditional Chinese        | big5_chinese_ci     |      2 |
| dec8     | DEC West European               | dec8_swedish_ci     |      1 |
| cp850    | DOS West European               | cp850_general_ci    |      1 |
| hp8      | HP West European                | hp8_english_ci      |      1 |
| koi8r    | KOI8-R Relcom Russian           | koi8r_general_ci    |      1 |
| latin1   | cp1252 West European            | latin1_swedish_ci   |      1 |
| latin2   | ISO 8859-2 Central European     | latin2_general_ci   |      1 |
| swe7     | 7bit Swedish                    | swe7_swedish_ci     |      1 |
| ascii    | US ASCII                        | ascii_general_ci    |      1 |
| ujis     | EUC-JP Japanese                 | ujis_japanese_ci    |      3 |
| sjis     | Shift-JIS Japanese              | sjis_japanese_ci    |      2 |
| hebrew   | ISO 8859-8 Hebrew               | hebrew_general_ci   |      1 |
| tis620   | TIS620 Thai                     | tis620_thai_ci      |      1 |
| euckr    | EUC-KR Korean                   | euckr_korean_ci     |      2 |
| koi8u    | KOI8-U Ukrainian                | koi8u_general_ci    |      1 |
| gb2312   | GB2312 Simplified Chinese       | gb2312_chinese_ci   |      2 |
| greek    | ISO 8859-7 Greek                | greek_general_ci    |      1 |
| cp1250   | Windows Central European        | cp1250_general_ci   |      1 |
| gbk      | GBK Simplified Chinese          | gbk_chinese_ci      |      2 |
| latin5   | ISO 8859-9 Turkish              | latin5_turkish_ci   |      1 |
| armscii8 | ARMSCII-8 Armenian              | armscii8_general_ci |      1 |
| utf8     | UTF-8 Unicode                   | utf8_general_ci     |      3 |
| ucs2     | UCS-2 Unicode                   | ucs2_general_ci     |      2 |
| cp866    | DOS Russian                     | cp866_general_ci    |      1 |
| keybcs2  | DOS Kamenicky Czech-Slovak      | keybcs2_general_ci  |      1 |
| macce    | Mac Central European            | macce_general_ci    |      1 |
| macroman | Mac West European               | macroman_general_ci |      1 |
| cp852    | DOS Central European            | cp852_general_ci    |      1 |
| latin7   | ISO 8859-13 Baltic              | latin7_general_ci   |      1 |
| utf8mb4  | UTF-8 Unicode                   | utf8mb4_general_ci  |      4 |
| cp1251   | Windows Cyrillic                | cp1251_general_ci   |      1 |
| utf16    | UTF-16 Unicode                  | utf16_general_ci    |      4 |
| utf16le  | UTF-16LE Unicode                | utf16le_general_ci  |      4 |
| cp1256   | Windows Arabic                  | cp1256_general_ci   |      1 |
| cp1257   | Windows Baltic                  | cp1257_general_ci   |      1 |
| utf32    | UTF-32 Unicode                  | utf32_general_ci    |      4 |
| binary   | Binary pseudo charset           | binary              |      1 |
| geostd8  | GEOSTD8 Georgian                | geostd8_general_ci  |      1 |
| cp932    | SJIS for Windows Japanese       | cp932_japanese_ci   |      2 |
| eucjpms  | UJIS for Windows Japanese       | eucjpms_japanese_ci |      3 |
| gb18030  | China National Standard GB18030 | gb18030_chinese_ci  |      4 |
+----------+---------------------------------+---------------------+--------+
41 rows in set (0.02 sec)
```

**View character sets of the current connection**

```
mysql> show variables like "%char%";
+--------------------------+-----------------------------------------------------+
| Variable_name            | Value                                               |
+--------------------------+-----------------------------------------------------+
| character_set_client     | latin1                                              |
| character_set_connection | latin1                                              |
| character_set_database   | utf8                                                |
| character_set_filesystem | binary                                              |
| character_set_results    | latin1                                              |
| character_set_server     | utf8                                                |
| character_set_system     | utf8                                                |
| character_sets_dir       | /data/tdsql_run/8812/percona-5.7.17/share/charsets/ |
+--------------------------+-----------------------------------------------------+
```

**Set the current connection-related character sets**

```
mysql> set names utf8;
Query OK, 0 rows affected (0.03 sec)

mysql> show variables like "%char%";
+--------------------------+-----------------------------------------------------+
| Variable_name            | Value                                               |
+--------------------------+-----------------------------------------------------+
| character_set_client     | utf8                                                |
| character_set_connection | utf8                                                |
| character_set_database   | utf8                                                |
| character_set_filesystem | binary                                              |
| character_set_results    | utf8                                                |
| character_set_server     | utf8                                                |
| character_set_system     | utf8                                                |
| character_sets_dir       | /data/tdsql_run/8811/percona-5.7.17/share/charsets/ |
+--------------------------+-----------------------------------------------------+
```

**Note**: TDSQL does not support setting parameters via the command line. Instead, you need to set parameters in the console.

**Modify time zone-related attributes by setting the `time_zone` variable**

```
mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | SYSTEM |
+------------------+--------+
2 rows in set (0.00 sec)

mysql> create table test.tt (ts timestamp, dt datetime,c int) shardkey=c;
Query OK, 0 rows affected (0.49 sec)

mysql>  insert into test.tt (ts,dt,c)values ('2017-10-01 12:12:12', '2017-10-01 12:12:12',1);
Query OK, 1 row affected (0.09 sec)

mysql> select * from test.tt;
+---------------------+---------------------+------+
| ts                  | dt                  | c    |
+---------------------+---------------------+------+
| 2017-10-01 12:12:12 | 2017-10-01 12:12:12 |    1 |
+---------------------+---------------------+------+
1 row in set (0.04 sec)

mysql> set time_zone = '+12:00';
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | +12:00 |
+------------------+--------+
2 rows in set (0.00 sec)

mysql> select * from test.tt;
+---------------------+---------------------+------+
| ts                  | dt                  | c    |
+---------------------+---------------------+------+
| 2017-10-01 16:12:12 | 2017-10-01 12:12:12 |    1 |
+---------------------+---------------------+------+
1 row in set (0.06 sec)
```

## Supported Data Types

TDSQL supports all MySQL data types, including numeric types, character types, date and time types, spatial types, and JSON data types.

**Numeric types**

TDSQL supports three numeric data types: integer, floating-point, and fixed-point. The specific supported types are as follows:

- For integer types, INT, SMALLINT, TINYINT, MEDIUMINT, and BIGINT are supported. See the following table for details.

| Type | Number of Bytes | Minimum (Signed/Unsigned) | Maximum (Signed/Unsigned) |
| --------- | ------ | ---------------------- | ---------------------------------------- |
| TINYINT   | 1      | -128/0                 | 127/255                                  |
| SMALLINT  | 2      | -32768/0               | 32767/65535                              |
| MEDIUMINT | 3      | -8388608/0             | 8388607/16777215                         |
| INT       | 4      | -2147483648/0          | 2147483647/4294967295                    |
| BIGINT    | 8      | -9223372036854775808/0 | 9223372036854775807/18446744073709551615 |

- For floating-point types, FLOAT and DOUBLE are supported in the format FLOAT(M,D), REAL(M,D), or DOUBLE PRECISION(M,D).

- For fixed point types, DECIMAL and NUMERIC are supported in the format of DECIMAL(M,D).

**Character types**

TDSQL supports the following character types:

```
CHAR and VARCHAR Types
BINARY and VARBINARY Types
BLOB and TEXT Types
	TINYBLOB, TINYTEXT, MEDIUMBLOB, MEDIUMTEXT, LONGBLOB, LONGTEXT
ENUM Type
SET Type
```

**Date and time types**

TDSQL supports the following date and time types:

```
DATE, DATETIME,  TIMESTAMP Types
TIME Type
YEAR Type
```

**Spatial data types**

TDSQL supports the following spatial data types:

```
GEOMETRY
POINT
LINESTRING
POLYGON

MULTIPOINT
MULTILINESTRING
MULTIPOLYGON
GEOMETRYCOLLECTION
```

**JSON data types**

Storing JSON-formatted data is supported, making JSON processing more efficient and enabling the early detection of errors. The statement is as follows:

**Note**: Mixed-type sorting is not supported for sorting fields of JSON type. For example, you cannot compare string type with int type. Same-type sorting is supported only for value and string types, while sorting for other types will not be processed.

```sql
mysql>  CREATE TABLE t1 (jdoc JSON,a int) shardkey=a;
Query OK, 0 rows affected (0.30 sec)

mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": "value2"}',1);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": 2}',2);

mysql> INSERT INTO t1 (jdoc,a)VALUES('[1, 2,',5);
ERROR 3140 (22032): Invalid JSON text: "Invalid value." at position 6 in value for column 't1.jdoc'.

mysql> select * from t1;
+--------------------------------------+---+
| jdoc                                 | a |
+--------------------------------------+---+
| {"key1": "value1", "key2": "value2"} | 1 |
| {"key1": "value1", "key2": 2}        | 2 |
+--------------------------------------+---+
2 rows in set (0.00 sec)

```

## Supported Functions

A distributed instance supports the following seven types of functions:

- Control flow functions
- String functions
- Numeric functions and operators
- Date and time functions
- Aggregate (GROUP BY) functions
- Bit functions and operators
- Cast functions and operators

The specific descriptions of each function type are as follows:

**Control flow functions**

| Function Name | Description |
| -------- | ---------------------------- |
| CASE     | Case operator                |
| IF()     | If/else construct            |
| IFNULL() | Null if/else construct       |
| NULLIF() | Return NULL if expr1 = expr2 |


 **String functions**

| Function Name | Description |
| ------------------ | ------------------------------------------------------------ |
| ASCII()            | Return numeric value of left-most character                  |
| BIN()              | Return a string containing binary representation of a number |
| BIT_LENGTH()       | Return length of argument in bits                            |
| CHAR()             | Return the character for each integer passed                 |
| CHAR_LENGTH()      | Return number of characters in argument                      |
| CHARACTER_LENGTH() | Synonym for CHAR_LENGTH()                                    |
| CONCAT()           | Return concatenated string                                   |
| CONCAT_WS()        | Return concatenate with separator                            |
| ELT()              | Return string at index number                                |
| EXPORT_SET()       | Return a string such that for every bit set in the value bits, you get an on string and for every unset bit, you get an off string |
| FIELD()            | Return the index (position) of the first argument in the subsequent arguments |
| FIND_IN_SET()      | Return the index position of the first argument within the second argument |
| FORMAT()           | Return a number formatted to specified number of decimal places |
| FROM_BASE64()      | Decode to a base-64 string and return result                 |
| HEX()              | Return a hexadecimal representation of a decimal or string value |
| INSERT()           | Insert a substring at the specified position up to the specified number of characters |
| INSTR()            | Return the index of the first occurrence of substring        |
| LCASE()            | Synonym for LOWER()                                          |
| LEFT()             | Return the leftmost number of characters as specified        |
| LENGTH()           | Return the length of a string in bytes                       |
| LIKE               | Simple pattern matching                                      |
| LOAD_FILE()        | Load the named file                                          |
| LOCATE()           | Return the position of the first occurrence of substring     |
| LOWER()            | Return the argument in lowercase                             |
| LPAD()             | Return the string argument, left-padded with the specified string |
| LTRIM()            | Remove leading spaces                                        |
| MAKE_SET()         | Return a set of comma-separated strings that have the corresponding bit in bits set |
| MATCH              | Perform full-text search                                     |
| MID()              | Return a substring starting from the specified position      |
| NOT LIKE           | Negation of simple pattern matching                          |
| NOT REGEXP         | Negation of REGEXP                                           |
| OCT()              | Return a string containing octal representation of a number  |
| OCTET_LENGTH()     | Synonym for LENGTH()                                         |
| ORD()              | Return character code for leftmost character of the argument |
| POSITION()         | Synonym for LOCATE()                                         |
| QUOTE()            | Escape the argument for use in an SQL statement              |
| REGEXP             | Pattern matching using regular expressions                   |
| REPEAT()           | Repeat a string the specified number of times                |
| REPLACE()          | Replace occurrences of a specified string                    |
| REVERSE()          | Reverse the characters in a string                           |
| RIGHT()            | Return the specified rightmost number of characters          |
| RLIKE              | Synonym for REGEXP                                           |
| RPAD()             | Append string the specified number of times                  |
| RTRIM()            | Remove trailing spaces                                       |
| SOUNDEX()          | Return a soundex string                                      |
| SOUNDS LIKE        | Compare sounds                                               |
| SPACE()            | Return a string of the specified number of spaces            |
| STRCMP()           | Compare two strings                                          |
| SUBSTR()           | Return the substring as specified                            |
| SUBSTRING()        | Return the substring as specified                            |
| SUBSTRING_INDEX()  | Return a substring from a string before the specified number of occurrences of the delimiter |
| TO_BASE64()        | Return the argument converted to a base-64 string            |
| TRIM()             | Remove leading and trailing spaces                           |
| UCASE()            | Synonym for UPPER()                                          |
| UNHEX()            | Return a string containing hex representation of a number    |
| UPPER()            | Convert to uppercase                                         |
| WEIGHT_STRING()    | Return the weight string for a string                        |


 **Numeric functions and operators**

| Function Name | Description |
| --------------- | ------------------------------------------------------------ |
| ABS()           | Return the absolute value                                    |
| ACOS()          | Return the arc cosine                                        |
| ASIN()          | Return the arc sine                                          |
| ATAN()          | Return the arc tangent                                       |
| ATAN2(), ATAN() | Return the arc tangent of the two arguments                  |
| CEIL()          | Return the smallest integer value not less than the argument |
| CEILING()       | Return the smallest integer value not less than the argument |
| CONV()          | Convert numbers between different number bases               |
| COS()           | Return the cosine                                            |
| COT()           | Return the cotangent                                         |
| CRC32()         | Compute a cyclic redundancy check value                      |
| DEGREES()       | Convert radians to degrees                                   |
| DIV             | Integer division                                             |
| /               | Division operator                                            |
| EXP()           | Raise to the power of                                        |
| FLOOR()         | Return the largest integer value not greater than the argument |
| LN()            | Return the natural logarithm of the argument                 |
| LOG()           | Return the natural logarithm of the first argument           |
| LOG10()         | Return the base-10 logarithm of the argument                 |
| LOG2()          | Return the base-2 logarithm of the argument                  |
| -               | Minus operator                                               |
| MOD()           | Return the remainder                                         |
| %, MOD          | Modulo operator                                              |
| PI()            | Return the value of pi                                       |
| +               | Addition operator                                            |
| POW()           | Return the argument raised to the specified power            |
| POWER()         | Return the argument raised to the specified power            |
| RADIANS()       | Return argument converted to radians                         |
| RAND()          | Return a random floating-point value                         |
| ROUND()         | Round the argument                                           |
| SIGN()          | Return the sign of the argument                              |
| SIN()           | Return the sine of the argument                              |
| SQRT()          | Return the square root of the argument                       |
| TAN()           | Return the tangent of the argument                           |
| *               | Multiplication operator                                      |
| TRUNCATE()      | Truncate to specified number of decimal places               |
| -               | Change the sign of the argument                              |

**Date and time functions**

| Function Name | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| ADDDATE()                              | Add time values (intervals) to a date value                  |
| ADDTIME()                              | Add time                                                     |
| CONVERT_TZ()                           | Convert from one time zone to another                        |
| CURDATE()                              | Return the current date                                      |
| CURRENT_DATE(), CURRENT_DATE           | Synonyms for CURDATE()                                       |
| CURRENT_TIME(), CURRENT_TIME           | Synonyms for CURTIME()                                       |
| CURRENT_TIMESTAMP(), CURRENT_TIMESTAMP | Synonyms for NOW()                                           |
| CURTIME()                              | Return the current time                                      |
| DATE()                                 | Extract the date part of a date or datetime expression       |
| DATE_ADD()                             | Add time values (intervals) to a date value                  |
| DATE_FORMAT()                          | Format date as specified                                     |
| DATE_SUB()                             | Subtract a time value (interval) from a date                 |
| DATEDIFF()                             | Subtract two dates                                           |
| DAY()                                  | Synonym for DAYOFMONTH()                                     |
| DAYNAME()                              | Return the name of the weekday                               |
| DAYOFMONTH()                           | Return the day of the month (0-31)                           |
| DAYOFWEEK()                            | Return the weekday index of the argument                     |
| DAYOFYEAR()                            | Return the day of the year (1-366)                           |
| EXTRACT()                              | Extract part of a date                                       |
| FROM_DAYS()                            | Convert a day number to a date                               |
| FROM_UNIXTIME()                        | Format Unix timestamp as a date                              |
| GET_FORMAT()                           | Return a date format string                                  |
| HOUR()                                 | Extract the hour                                             |
| LAST_DAY                               | Return the last day of the month for the argument            |
| LOCALTIME(), LOCALTIME                 | Synonym for NOW()                                            |
| LOCALTIMESTAMP, LOCALTIMESTAMP()       | Synonym for NOW()                                            |
| MAKEDATE()                             | Create a date from the year and day of year                  |
| MAKETIME()                             | Create time from hour, minute, second                        |
| MICROSECOND()                          | Return the microseconds from argument                        |
| MINUTE()                               | Return the minute from the argument                          |
| MONTH()                                | Return the month from the date passed                        |
| MONTHNAME()                            | Return the name of the month                                 |
| NOW()                                  | Return the current date and time                             |
| PERIOD_ADD()                           | Add a period to a year-month                                 |
| PERIOD_DIFF()                          | Return the number of months between periods                  |
| QUARTER()                              | Return the quarter from a date argument                      |
| SEC_TO_TIME()                          | Converts seconds to 'HH:MM:SS' format                        |
| SECOND()                               | Return the second (0-59)                                     |
| STR_TO_DATE()                          | Convert a string to a date                                   |
| SUBDATE()                              | Synonym for DATE_SUB() when invoked with three arguments     |
| SUBTIME()                              | Subtract times                                               |
| SYSDATE()                              | Return the time at which the function executes               |
| TIME()                                 | Extract the time portion of the expression passed            |
| TIME_FORMAT()                          | Format as time                                               |
| TIME_TO_SEC()                          | Return the argument converted to seconds                     |
| TIMEDIFF()                             | Subtract time                                                |
| TIMESTAMP()                            | With a single argument, this function returns the date or datetime expression; with two arguments, the sum of the arguments |
| TIMESTAMPADD()                         | Add an interval to a datetime expression                     |
| TIMESTAMPDIFF()                        | Subtract an interval from a datetime expression              |
| TO_DAYS()                              | Return the date argument converted to days                   |
| TO_SECONDS()                           | Return the date or datetime argument converted to seconds since Year 0 |
| UNIX_TIMESTAMP()                       | Return a Unix timestamp                                      |
| UTC_DATE()                             | Return the current UTC date                                  |
| UTC_TIME()                             | Return the current UTC time                                  |
| UTC_TIMESTAMP()                        | Return the current UTC date and time                         |
| WEEK()                                 | Return the week number                                       |
| WEEKDAY()                              | Return the weekday index                                     |
| WEEKOFYEAR()                           | Return the calendar week of the date (1-53)                  |
| YEAR()                                 | Return the year                                              |
| YEARWEEK()                             | Return the year and week                                     |

**Aggregate (GROUP BY) functions**     

| Function Name | Description |
| ------- | --------------------------------------------- |
| AVG()   | Return the average value of the argument      |
| COUNT() | Return a count of the number of rows returned |
| MAX()   | Return the maximum value                      |
| MIN()   | Return the minimum value                      |
| SUM()   | Return the sum                                |

**Bit functions and operators**

| Function Name | Description |
| ----------- | -------------------------------------- |
| BIT_COUNT() | Return the number of bits that are set |
| &           | Bitwise AND                            |
| ~           | Bitwise inversion                      |
| &#124;      | Bitwise OR                             |
| ^           | Bitwise XOR                            |
| <<          | Left shift                             |
| >>          | Right shift                            |

**Cast functions and operators**

| Function Name | Description |
| --------- | -------------------------------- |
| BINARY    | Cast a string to a binary string |
| CAST()    | Cast a value as a certain type   |
| CONVERT() | Cast a value as a certain type   |



## Proxy Error Codes and Error Messages

Proxy error codes and error messages are as shown below:

	#define ER_PROXY_GRAM_ERROR_BEGIN 600
	
	#define ER_PROXY_SANITY_ERROR 601 // "Sanity error: %s"
	#define ER_PROXY_SQL_TYPE_NOT_SUPPORT 602 // Unsupported SQL type
	#define ER_PROXY_SQL_NOT_SUPPORT_ORDERBY_1 603 // order by index is negative
	#define ER_PROXY_SQL_NOT_SUPPORT_ORDERBY_2 604 // order by index is too big
	#define ER_PROXY_SQL_NOT_SUPPORT_ORDERBY_3 605 // order by is not supported
	#define ER_PROXY_SQL_NOT_SUPPORT_GROUPBY_1 606 // group by index is negative
	#define ER_PROXY_SQL_NOT_SUPPORT_GROUPBY_2 607 // group by index is too big
	#define ER_PROXY_SQL_NOT_SUPPORT_GROUPBY_3 608 // group by is not supported
	#define ER_PROXY_GET_AUTO_ID_FAILED 609 // get auto id back with error
	#define ER_PROXY_TEANS_ROLLED_BACK 610 // The transaction has been rolled back
	#define ER_PROXY_ONE_SET 611 // The current SQL statement should have been sent to the backend but it was not
	#define ER_PROXY_CLIENT_HS_ERROR 612 // Error parsing the client handshake packet
	#define ER_PROXY_ACCESS_DENIED_ERROR 613 // The length of readu_auth_switch_result is not 20, which should not happen
	#define ER_PROXY_TRANS_NOT_ALLOWED 614 // Command not allowed in the transaction
	#define ER_PROXY_TRANS_READ_ONLY 615 // Command not allowed in the read-only transaction
	#define ER_PROXY_TRANS_ERROR_DIFFENT_SET 616 // In the non-XA transaction, the read-only SQL uses multiple backends
	#define ER_PROXY_STRICT_ERROR 617 // In strict mode, only one set can be modified at a time	
	#define ER_PROXY_SC_TOO_LONG 618 // The backend disconnection time is too long and the link is closed
	#define ER_PROXY_START_TRANS_FAILED 619 // Failed to start a new XA transaction
	#define ER_PROXY_SC_RETRY 620 // The server is closed. Please retry the previous SQL statement
	#define ER_PROXY_SC_TRANS_IN_ROLLBACK_ONLY 621 // The server is closed. The current transaction is being rolled back 
	#define ER_PROXY_SC_COMMIT_LATER 622 // The server is closed. The transaction will be committed later
	#define ER_PROXY_SC_ROLLBACL_LATER 623 // The server is closed. The transaction will be rolled back later
	#define ER_PROXY_SC_IN_COMMIT_OR_ROLLBACK 624 // The server was closed during transaction committing/rollback
	#define ER_PROXY_SC_NEED_ROLLBACK 625 // The server is closed. You need to roll back the current transaction first
	#define ER_PROXY_SC_STATE_WILL_ROLLBACK 626 // The server is closed. Rollback will be performed
	#define ER_PROXY_XA_UNSUPPORT 627 // Command not supported by XA currently
	#define ER_PROXY_XA_INVALID_COMMAND 628 // The XA command is invalid
	#defien ER_PROXY_XA_GTID_INIT_ERROR 629 // gtid log initialization failed
	#define ER_PROXY_XA_GET_SET_IP_PORT_FAILED 630 // Failed to obtain the set address
	#define ER_PROXY_XA_UPDATE_GTID_LOG_FAILED 631 // Failed to update gtid log
	#define ER_PROXY_MYSQL_PARSER_ERROR 632 // MySQL parsing failed. The detailed error message is returned
	#define ER_PROXY_MYSQL_PARSER_UNEXPECTED_ERROR 633 // MySQL parsing failed. Unexpected error
	#define ER_PROXY_MYSQL_PARSER_NOT_SUPPORTED 634 // Command not supported by MySQL
	#define ER_PROXY_ILLEGAL_ID 635 // kill id is invalid
	#define ER_PROXY_NOT_SUPPORT_CURSOR 636 // CURSOR_TYPE_READ_ONLY is not supported for the time being
	#define ER_PROXY_UNKNOWN_PREPARE_HANDLER 637 // The executed prepare is not clear
	#define ER_PROXY_SET_PARA_FAIL 638 // Set parameters failed
	#define ER_PROXY_SUBPARTITION_TABLE_TOO_MANY_DEAL 639 // Only one level-two partition table can be processed
	#define ER_PROXY_NS_AND_SHARD_TABLE_DENY 640 // can not deal with noshard and shard table
	#define ER_PROXY_NS_AND_GLOBAL_TABLE_DENY 641 // Can not deal with noshard and global table
	#define ER_PROXY_NO_SUBPARTITION_ROUTE 642 // No routing information was obtained for the level-two partition table
	#define ER_PROXY_LOCK_MORE_TABLE 643 // Only one level-two partition table can be locked at a time
	#define ER_PROXY_GET_ROUTER_LOCK_FAIL 644 // Failed to obtain the route lock
	#define ER_PROXY_PART_NAME_EMPTY 645 // part name is empty
	#define ER_PROXY_SUB_PART_TABLE_IS_NONE 646 // There is no level-two partition table
	#define ER_PROXY_ALTER_PART_TYPE_TO_RANGE 647 // "Table has list type, alter use range type"
	#define ER_PROXY_ALTER_PART_TYPE_TO_LIST 648 // "Table has range type, alter use list type"
	#define ER_PROXY_PART_NAME_ILLEGAL 649 // The partition name is invalid
	#define ER_PROXY_DROP_ALL_PARTITION_FAIL 650 // Failed to delete all partitions. Please try deleting the table directly
	#define ER_PROXY_GET_OLD_PART_NUM_FAIL 651 // Failed to obtain the number of shards of the table
	#define ER_PROXY_EMPTY_SQL 652 // Empty SQL, which will not be returned to the client
	#define ER_PROXY_ERROR_SHARDKEY 653 // sk must be a specified column	
	#define ER_PROXY_ERROR_SUB_SHARDKEY 654 // Level-two shardkey failed	
	#define ER_PROXY_SQLUSE_NOT_SUPPORT 655 // The proxy does not support this usage
	#define ER_PROXY_DBFW_WHITE_LIST_DENY 656 // Not in the whitelist and rejected by the firewall
	#define ER_PROXY_DBFW_DENY 657 // Rejected by the firewall
	#define ER_PROXY_INCORRECT_ARGS 658 // The stmt parameter is incorrect	
	#define ER_PROXY_SYSTABLE_UNSUPPORT_NON_READ_SQL 659 // Non-read-only SQL statements cannot access system tables
	#define ER_PROXY_TABLE_NOT_EXIST 660 // The table does not exist	
	#define ER_PROXY_SHARD_JOIN_UNSUPPORT_TYPE 661 // shard join is not supported for the time being
	#define ER_PROXY_RECURSIVE_JOIN_DENY 662 // Recursive join is not supported
	#define ER_PROXY_JOIN_INTERNAL_ERROR 663 // join is exceptional
	#define ER_PROXY_SQL_TOO_COMPLEX 664 // The SQL statement is too complex and cannot be supported by groupshard
	#define ER_PROXY_INVALID_ARG_FOR_GTID_STATE 665 // The gtid_state() parameter is invalid
	#define ER_PROXY_CANT_SET_GLOBAL_AUTOCOMMIT_GS 666 // Global autocommit cannot be set in groupshard
	#define ER_PROXY_INVALID_VALUE_FOR_AUTOCOMMIT 667 // The set autocommit value is invalid
	#define ER_PROXY_XID_ERROR 668 // xid is invalid
	#define ER_PROXY_XID_GENERAT_FAILED 669 // xid cannot be specified by the user	
	#define ER_PROXY_CANT_EXEC_IN_INTER_TRANS 670 // "The command cannot be executed in internal transction"
	#define ER_PROXY_XID_TIME_ERROR 671 // "Unexpected time part of xid"
	#define ER_PROXY_XID_TIMEDIFF_TOO_LONG 672 // "timediff > 1800s, it's not safe to execute boost"
	#define ER_PROXY_SAVEPOINT_NOT_EXIST 673 // The SAVEPOINT does not exist
	#define ER_PROXY_SC_TRANS_IN_ROLLED 674 // The transaction has already been rolled back as the server has been closed
	#define ER_PROXY_CANT_BOOST_IN_TRANS 675 // SQLCOM_BOOST is not allowed in the transaction
	#define ER_PROXY_TRANS_EXPECTED 676 // "A transaction is expected, this maybe a bug"
	#define ER_PROXY_EXTERNAL_TRANS 677 // An external XA transaction cannot be executed
	#define ER_PROXY_AUTO_INC_FAIL 678 // "Deal auto inc failed"
	#define ER_PROXY_CHECK_JOIN_FAIL 679 // "Check join failed"
	#define ER_PROXY_TABLE_TYPE_NOT_MATCH 680 // "Do not support shard-table operations in noshard instance"
	#define ER_PROXY_UNSUPPORT_NS_IN_INSERT 681 // "Do not support noshard and noshard_allset in insert sql"
	#define ER_PROXY_ALTER_SEQ_ID_FAIL 682 // Alter seq id failed
	#define ER_PROXY_ALTER_ID_ILLEGAL 683 // Alter seq id is illegal	
	#define ER_PROXY_CANT_CHANGE_STEP 684 // "Current table use zk to get auto inc, do not support to change step: \'%s\'"
	#define ER_PROXY_ALTER_STEP_FAIL 685 // Alter step failed	
	#define ER_PROXY_TOO_MUCH_TABLES 686 // "Too much tables, exceed the maximum value"
	#define ER_PROXY_TABLE_EXISTED 687 // The table already exists
	#define ER_PROXY_CREATE_STABLE_FAILED 688 // "Complex sql can not used to create shard tables"
	#define ER_PROXY_DDL_DENY 689 // "DDL can not handle noshard and global table"
	#define ER_PROXY_SHADKEY_ERROR 690 // "SQL should not relate to subpartition tables"
	#define ER_PROXY_NO_SK 691 // reject nosk
	#define ER_PROXY_COMBINE_SQL_KEY 692 // "Something went wrong:%s"
	#define ER_PROXY_GET_SK_ERROR 693 // Failed to get the sk
	#define ER_PROXY_SHOW_FAILED 684 // "%s, see /*proxy*/ help"
	#define ER_PROXY_SET_FAILED 695 // "%s, see /*proxy*/ help"
	#define ER_PROXY_UNLOCK_FORMAT_ERROR 696 // The SQL statement format is incorrect
	#define ER_PROXY_UNLOCK_ROUTER_FAIL 697 // "Unlock failed"
	#define ER_PROXY_LOCK_ROUTER_FAIL 698 // "Lock failed"
	#define ER_PROXY_PROXY_CMD_FAIL 699 // Unsupported /*proxy*/ command
	#define ER_PROXY_PROCESS_RULE_FILE_FAILED 700 // dump_error
	#define ER_PROXY_GET_AUTO_NUM_ERROR 701 // "Get auto num failed"
	#define ER_PROXY_SEQUENCE_NOT_EXIST 702 // The sequence does not exist
	#define ER_PROXY_SEQUENCE_ERROR 703 // The sequence is invalid
	#define ER_PROXY_SEQUENCE_ALREADY_EXIST 704 // The sequence already exists
	
	#define ER_PROXY_GRAM_ERROR_END 705
	#define ER_PROXY_SYSTEM_ERROR_BEGIN 900 
	
	#define ER_PROXY_SLICING 901 // The slice is modified and possibly being scaled, causing the current SQL statement to be rejected
	#define ER_PROXY_NO_DEFAULT_SET 902 // The set is empty
	#define ER_PROXY_GET_ADDRESS_FAILED 903 // Initialization has not been completed yet. Failed to obtain the backend address. Please try again later
	#define ER_PROXY_SQL_SIZE_ERROR_IN_GET_CANDIDATE_ADDRESS 904 // Error obtaining the backend address (the number of destination backends is incorrect)
	#define ER_PROXY_GET_ADDRESS_ERROR 905 // Error obtaining the backend address
	#define ER_PROXY_CANDIDATE_ADDRESS_EMPTY 906 // No backend address obtained
	#define ER_PROXY_SOCK_ERROR 907 // The current SQL statement is not allowed to be sent to the backend	
	#define ER_PROXY_CANT_GET_SOCK 908 // Failed to obtain the socket	
	#define ER_PROXY_GET_SET_SOCK_FAIL 909 // Failed to obtain the socket
	#define ER_PROXY_CONNECT_ERROR 910 // Backend connection failed
	#define ER_PROXY_NO_SQL_ASSIGN_TO_SET 911 // an unbelievable error
	#define ER_PROXY_STATUS_ERROR 912 // The group is in an exceptional status and disconnected
	#define ER_PROXY_CONN_BROKEN_ERROR 913 // The server is closed and the SQL statement is in an exceptional status
	#define ER_PROXY_UNKNOWN_ERROR 914 // Unknown proxy error (which may be caused by an exception)
	#define ER_PROXY_SQL_RETRY 915 // The SQL statement has not been committed or rolled back	
	#define ER_PROXY_XA2PC_ABORT 916 // 2pc failed and the transaction will be rolled back
	#define ER_PROXY_XA2PC_COMMIT 917 // 2pc failed and will be committed later
	#define ER_PROXY_XA2PC_UNCERTAIN 918 // 2pc failed with unknown result
	#define ER_PROXY_ERROR_END 919

**Note**: Error codes above 900 are system errors and will be alarmed on through the monitoring platform.

