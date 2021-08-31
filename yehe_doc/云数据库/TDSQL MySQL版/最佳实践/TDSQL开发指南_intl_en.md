TDSQL provides a connection mode compatible with MySQL. It can be connected using the IP address, port number, username, and password:
```
mysql -hxxx.xxx.xxx.xxx -Pxxxx -uxxx -pxxx -c
```	
>TDSQL does not support versions below 4.0 and compression protocols. You are recommended to add the `-c` option when using the client, so that you can use certain advanced features.

## Overview
TDSQL can implement horizontal sharding. You only need to specify the shardkey when creating a table, and TDSQL will perform data routing and aggregation accordingly, where operations are imperceptible to the business.
- It provides a flexible read/write separation mode.
- It supports global order by, group by, and limit operations.
- It supports aggregate functions, including sum, count, avg, min, and max (but not other aggregate functions).
- It supports single-set join and can implement cross-set join to a certain extent based on groups and small tables.
- It supports preprocessing protocols.
- It supports global unique fields.
- It provides specific SQL statements for querying configuration and status of the entire cluster.
- It supports distributed transactions.
- It supports two-level partitioning.


Unsupported MySQL features are as follows:
- Custom functions.
- Views, stored procedures, triggers, and cursors.
- Foreign keys and self-built partitions.
- Compound statements such as BEGIN END, LOOP, and UNION.
- Subqueries and `having` clause (however, derived tables with shardkey are supported).


## Language Structures
TDSQL supports all text formats used by MySQL, including:
```
  String Literals
  Numeric Literals
  Date and Time Literals
  Hexadecimal Literals
  Bit-Value Literals
  Boolean Literals
  NULL Values
```

### String Literals
A string literal is a sequence of bytes or characters surrounded by single quotation mark (') or double quotation mark ("). Currently, TDSQL does not support ANSI_QUOTES SQL MODE. Things surrounded by double quotation marks (") are always considered string literals instead of identifiers.

The `character set introducer` format is not supported, i.e., `[_charset_name]'string' [COLLATE collation_name]`.

Supported escape characters are as follows:
```	
	\0: ASCII NUL (X’00’) character
	\': single quotation mark
	\": double quotation mark
	\b: backspace character
	\n: line break
	\r: carriage return
	\t: tab
	\z: ASCII 26 (Ctrl + Z)
	\\: backslash\
	\%: \%
	\_: _
```

### Numeric Literals
Numeric literals include integers, decimal-point numbers, and floating-point numbers.
An integer may include a decimal separator `.` and begin with a plus sign `+` or a minus sign `-` to indicate whether it is a positive or negative number.
An exact numeric literal can be expressed as follows: 1, .2, 3.4, -5, -6.78, +9.10.
Scientific notation in the format of 1.2E3, 1.2E-3, -1.2E3, and -1.2E-3.

### Date and Time Literals
Supported DATE formats are as follows:
```
	'YYYY-MM-DD' or 'YY-MM-DD'
	'YYYYMMDD' or 'YYMMDD'
	YYYYMMDD or YYMMDD

	Examples: '2012-12-31', '2012/12/31', '2012^12^31',  '2012@12@31'  '20070523', '070523' 
```
Supported DATETIME and TIMESTAMP formats are as follows:
```
	'YYYY-MM-DD HH:MM:SS' or 'YY-MM-DD HH:MM:SS'
	'YYYYMMDDHHMMSS' or 'YYMMDDHHMMSS'
	YYYYMMDDHHMMSS or YYMMDDHHMMSS 

	Examples: '2012-12-31 11:30:45', '2012^12^31 11+30+45', '2012/12/31 11*30*45',  '2012@12@31 11^30^45', 19830905132800 
```

### Hexadecimal Literals
Supported formats are as follows:
```
	X'01AF'
	X'01af'
	x'01AF'
	x'01af'
	0x01AF
	0x01af
```

### Bit-Value Literals
Supported formats are as follows:
```
	b'01'
	B'01'
	0b01
```

### Boolean Literals
Constants TRUE and FALSE are equal to 1 and 0, which are case-insensitive.
```	
	mysql>  SELECT TRUE, true, FALSE, false;
	+------+------+-------+-------+
	| TRUE | TRUE | FALSE | FALSE |
	+------+------+-------+-------+
	|    1 |    1 |     0 |     0 |
	+------+------+-------+-------+
	1 row in set (0.03 sec)
```

### NULL Values
Null indicates an absence of a value. It is case-insensitive and has the same meaning as `\N` (case-sensitive).
Note that NULL is not the same as 0 or empty string (`''`).

## Character Sets and Time Zones
TDSQL supports all character sets and character sequences of MySQL on the backend storage.
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

View character sets of the current connection:
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

Set the character sets related to the current connection:
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

>TDSQL does not support setting global parameters, which can only be set by calling the OSS API.


Modifying time zone attributes by setting the `time_zone` variable is supported:
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

## Data Types
TDSQL supports all data types of MySQL, including numbers, characters, dates, spatial types, and JSON.

### Numbers
For integer types, INTEGER, INT, SMALLINT, TINYINT, MEDIUMINT, and BIGINT are supported.
```
| Type | Number of Bytes | Minimum (Signed/Unsigned) | Maximum (Signed/Unsigned) |
| --------- | ---- | ---------------------- | ---------------------------------------- |
| TINYINT   | 1    | -128/0                 | 127/255                                  |
| SMALLINT  | 2    | -32768/0               | 32767/65535                              |
| MEDIUMINT | 3    | -8388608/0             | 8388607/16777215                         |
| INT       | 4    | -2147483648/0          | 2147483647/4294967295                    |
| BIGINT    | 8    | -9223372036854775808/0 | 9223372036854775807/18446744073709551615 |

```
For floating point types, FLOAT and DOUBLE are supported in the format of `FLOAT(M,D)`, `REAL(M,D)`, or ` DOUBLE PRECISION(M,D)`.
For fixed point types, DECIMAL and NUMERIC are supported in the format of ``DECIMAL(M,D)`.


### Characters
The following character types are supported:
```
	CHAR and VARCHAR Types
	BINARY and VARBINARY Types
	BLOB and TEXT Types
		TINYBLOB, TINYTEXT, MEDIUMBLOB, MEDIUMTEXT, LONGBLOB, LONGTEXT
	ENUM Type
	SET Type
```

### Dates
The following date and time types are supported:
```
	DATE, DATETIME, TIMESTAMP Types
	TIME Type
	YEAR Type
```

### Space
The following spatial types are supported:
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

### JSON
Storing data in JSON format is supported, making JSON processing more efficient while ensuring that errors can be detected in advance
```
	mysql>  CREATE TABLE t1 (jdoc JSON,a int) shardkey=a;
	Query OK, 0 rows affected (0.30 sec)
	
	mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": "value2"}',1);
	Query OK, 1 row affected (0.07 sec)
	
	mysql> INSERT INTO t1 (jdoc,a)VALUES('[1, 2,',5);
	ERROR 3140 (22032): Invalid JSON text: "Invalid value." at position 6 in value for column 't1.jdoc'.
	mysql> select * from t1;
	+--------------------------------------+------+
	| jdoc                                 | a    |
	+--------------------------------------+------+
	| {"key1": "value1", "key2": "value2"} |    1 |
	+--------------------------------------+------+
	1 row in set (0.03 sec)

```
Mixed-type sorting is not supported for `orderby` of JSON type, for example, you cannot compare string type with int type. Same-type sorting is supported only for value and string types and sorting for other types will not be processed.


## SQL Syntax
### Creating table
When creating a regular sharded table, you must specify the value of the shardkey at the end, which is a field name in the table and will be used for subsequent SQL routing:
```
	mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
	Query OK, 0 rows affected (0.07 sec)
```

In a TDSQL instance, a shardkey corresponds to the partition field of the backend database, so it must be part of the primary key and all unique indexes; otherwise, the table cannot be created:
```
	mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;
```
At this point, there is a unique index `u_2` that does not contain the shardkey, so the table cannot be created, and the following error will be displayed:
`ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function`
Because the index of the primary key or unique key has to be globally unique, to implement a globally unique index, you must include the shardkey field.


In addition to the above restrictions, the shardkey field also has the following requirements:
- The type of the shardkey field must be int, bigint, or smallint/char/varchar.
- The value of the shardkey field should not contain Asian characters, as the proxy will not convert the character set, and different character sets may be routed to different partitions.
- Do not update the value of the shardkey field.
- `shardkey=a` should be placed at the end of the SQL statement.
- Carry the shardkey field as much as possible when accessing data. This is not mandatory, but SQL statements without shardkey will be routed to all nodes and thus consume more resources.


The creation of small tables (broadcast tables) is supported. In this case, all sets have all of the data, which makes it easier to perform cross-set joins, while ensuring the atomicity of the modification operations through distributed transactions, so that the data in all sets is exactly identical.
```
	mysql> create table global_table ( a int, b int key) shardkey=noshardkey_allset;
	Query OK, 0 rows affected (0.06 sec)
```

The creation of regular tables using the same syntax with MySQL is supported. All the data in this type of tables is stored in the first set.
```
	mysql> create table noshard_table ( a int, b int key);
	Query OK, 0 rows affected (0.02 sec)
```

### General SQL
SELECT: it is best to include the shardkey field; otherwise, a full-table scan needs to be performed, and the result set will be aggregated at the gateway, which may affect the execution efficiency:
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

insert/replace: the shardkey field must be contained; otherwise, the SQL statement will be rejected because the proxy does not know to which backend database it should send the query:
```
	mysql> insert into test1 (b,c) values(4,"record3");
	ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
		Shard table insert must has field spec

	mysql> insert into test1 (a,c) values(4,"record3");
	Query OK, 1 row affected (0.01 sec)
```	

delete/update: for security considerations, when an SQL statement of this type is executed in a non-sharded or broadcast table, it must contain the `where` condition; otherwise, it will not be executed:
```
	mysql> delete from test1;
	ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
		Shard table delete/update must have a where clause

	mysql> delete from test1 where a=1;
	Query OK, 1 row affected (0.01 sec)
```

### Aggregation
TDSQL supports the following global aggregate functions and global sort groups: sum, min, max, count, avg, order by, and group by.

They can be used in the same way as standalone MySQL. For `order by` and `group by`, the corresponding fields need to be explicitly specified in the `select` list.
```
        mysql> select count(*),b from test group by b;
        
        mysql> select a,b from test order by b;
```

### Passthrough SQL
In TDSQL, the proxy will parse the SQL syntax, but there are relatively strict restrictions. If you want to execute an SQL statement in a certain set, you can use the SQL passthrough feature.
```
	mysql> select * from test1 where a in (select a from test1);
	ERROR 808 (HY000): Proxy ERROR:sql should has one shardkey
	mysql> /*set_1*/select * from test1 where a in (select a from test1);
	Empty set (0.00 sec)
```

Syntax:
```	
	Sets:set_1,set_2 (the set name can be queried by `/*proxy*/show status`)   
	sets:allsets   
	shardkey:10. The SQL statement can be passed through to one or more corresponding sets or the set corresponding to the shardkey.
```
> When the query is passed through, the proxy will not parse the query, so if it is a passthrough write operation to two sets, distributed transactions will not be used, which may cause inconsistency in extreme cases. Therefore, you are recommended to pass through only to one set during one write operation.

### JOIN
Only join operations in a single set are supported, which means that all SQL commands in a transaction must be executed in the same set; therefore, the `shardkey` field must be specified.
```
	mysql> create table test1 ( a int key, b int, c char(20) ) shardkey=a;
	Query OK, 0 rows affected (1.56 sec)
	
	mysql> create table test2 ( a int key, d int, e char(20) ) shardkey=a;
	Query OK, 0 rows affected (1.46 sec)
	
	mysql> insert into test1 (a,b,c) values(1,2,"record1"),(2,3,"record2");
	Query OK, 2 rows affected (0.02 sec)
	
	mysql> insert into test2 (a,d,e) values(1,3,"test2_record1"),(2,3,"test2_record2");
	Query OK, 2 rows affected (0.02 sec)
	
	mysql>  select * from test1 left join test2 on test1.a=test2.a;
	ERROR 7015 (HY000): Proxy ERROR:sql should send to only one backend
	mysql>  select * from test1 left join test2 on test1.a=test2.a where test1.a=1;
	+---+------+---------+---+------+---------------+
	| a | b    | c       | a | d    | e             |
	+---+------+---------+---+------+---------------+
	| 1 |    2 | record1 | 1 |    3 | test2_record1 |
	+---+------+---------+---+------+---------------+
	1 row in set (0.00 sec)

```

Conditional cross-set inner joins are supported:
```
	mysql>  select * from test1 join test2 on test1.a=test2.a;
	+---+------+---------+---+------+---------------+
	| a | b    | c       | a | d    | e             |
	+---+------+---------+---+------+---------------+
	| 1 |    2 | record1 | 1 |    3 | test2_record1 |
	| 2 |    3 | record2 | 2 |    3 | test2_record2 |
	+---+------+---------+---+------+---------------+
	2 rows in set (0.03 sec)
```

However, there are the following prerequisites:
- They must be inner joins.
- The condition of inner joins must be that the shardkey fields of all tables are equal. The `on`, `using`, and `where` formats are supported.


For joins related to small tables and non-sharded tables, there are no restrictions on shardkey:
```
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
Currently, join operations between non-sharded table and sharded table are not supported.


### Distributed transactions
Distributed transactions are supported and imperceptible to the client, so that they can be used by the business just like standalone transactions.
```
	begin; // Start a transaction
	delete
	update  // Manipulate data (cross-set operations are supported)
	select
	insert
	commit; // Commit a transaction
```

SQL statements are added to query the information of a specific transaction:
1. `select gtid()` is used to get the `gtid` (global transaction identifier) of the current distributed transaction. Null will be returned if the transaction is not a distributed one.
Format of `gtid`:
'Gateway ID'-'random value of gateway'-'serial number'-'timestamp'-'partition number', such as c46535fe-b6-dd-595db6b8-25.

2. `select gtid_state("gtid")` is used to get the status of `gtid`. Below are possible results:
 - "COMMIT", indicating that the transaction has been or will be eventually committed.
 - "ABORT", indicating that the transaction will be eventually rolled back.
 - Null. The transaction status will be cleared after one hour, so there are two possibilities:
1). For query after one hour, it indicates that the transaction status has been cleared.
2). For query within an hour, it indicates that the transaction will be eventually rolled back.				
Note: when a commit operation times out or fails, you should wait a few seconds before calling the API to query the transaction status.
		
3. OPS commands:
 -	xa recover: sends the `xa recover` command to the backend set and summarizes the results.
 -	xa lockwait: displays the wait relationship of the current distributed transaction (you can use the `dot` command to convert the output to a wait-for graph).
 -	xa show: shows the distributed transactions that are currently running on the gateway.
		

### Global unique field
Fields that auto-increment in a certain sense are supported to ensure that they are globally unique; however, monotonic increasing is not guaranteed. The specific usage is as follows:

Create:
```
	mysql> create table auto_inc (a int,b int,c int auto_increment,d int,key auto(c),primary key p(a,d)) shardkey=d;
	Query OK, 0 rows affected (0.12 sec)
```

Insert:
```
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
```

Note: if a process such as proxy switching or restarting occurs, there will be holes in the middle of the auto-increment fields, for example:
```
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
```   

Change the current value:
```
	alter table auto_inc auto_increment=100
```

If the auto-increment value is not specified, it can be obtained through `select last_insert_id()`:
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
>Currently, `select last_insert_id()` can only be used for auto-increment fields in sharded tables but not non-sharded tables or small broadcast tables.

### Database management statements
Status query
You can view the configuration and status of the proxy through SQL. The following commands are currently supported:
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
	| set_1499859173_1:ip         | xxx.xxx.xxx.xxx:xxxx;xxx.xxx.xxx.xxx:xxxx@1@IDC_4@0,xxx.xxx.xxx.xxx:xxxx@1@IDC_2@0 |
	| set_1499859173_1:hash_range | 0---31                                                                       |
	| set_1499911640_3:ip         | xxx.xxx.xxx.xxx:xxxx;xxx.xxx.xxx.xxx:xxxx@1@IDC_4@0,xxx.xxx.xxx.xxx:xxxx@1@IDC_2@0 |
	| set_1499911640_3:hash_range | 32---63                                                                      |
	| set                         | set_1499859173_1,set_1499911640_3                                            |
```


Meanwhile, the proxy enhances the returned result of explain, showing the SQL statement modified by the proxy:
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

### Data import and export
Data can be exported by mysqldump: 
Set the `net_write_timeout` parameter before export: `set global net_write_timeout=28800`
```
	mysqldump --compact --single-transaction --no-create-info -c
                     shard sbtest1  -uxxx -hxxx.xxx.xxx.xxx -Pxxxx -pxxx
```
The parameters should be selected based on the actual situation. If the exported data is to be imported into another set of TDSQL environment, the `-c` option must be added.

If you want to import data, a dedicated import tool is provided to complete the import of data corresponding to `load data outfile`:
```
	[tdengine@TENCENT64 ~/]$./load_data
	
	format:./load_data mode0/mode1 proxy_host proxy_port user password db_table shardkey_index file field_terminate filed_enclosed
	
	    example:./load_data mode1 1x.231.136.34 3336 test test123 shard.table  1 '/tmp/datafile'  ' ' ''
	
	
	
	format:./load_data mode2 routers_file shardkey_index file field_terminate filed_enclosed
	
	    example:./load_data mode2 '/data/3336.xml' 1 '/tmp/datafile'  ' ' ''
	
	note:lines should terminated by \n
	note:field_terminate may have more than one char,filed_enclosed must have only one char,all can not have ',do not support escape char
	
```

### Preprocessing
Supported SQL types:
- PREPARE Syntax
- EXECUTE Syntax

Supported binary protocols:
- `COM_STMT_PREPARE`
- `COM_STMT_EXECUTE`

Sample:
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

### Subquery
TDSQL currently supports subqueries only for derived tables with shardkey:
```
	mysql> select a from (select * from test1) as t;
	ERROR 7012 (HY000): Proxy ERROR:sql should has one shardkey
	mysql> select a from (select * from test1 where a=1) as t;
	+---+
	| a |
	+---+
	| 1 |
	+---+
	1 row in set (0.00 sec)
```

### Two-Level partitioning
TDSQL only uses the HASH method to shard data, which is not convenient for deleting old data of specific conditions, such as transactional data. In order to solve this problem, two-level partitioning can be used.

TDSQL supports two-level partitioning in range and list formats where the specific table creating syntax is similar to the partitioning syntax in MySQL.

Supported range types:
```
	DATE, DATETIME, TIMESTAMP
		`year`, `month`, and `day` functions are supported. If the function is empty, it will be defaulted to the `day` function

	TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT
		`year`, `month`, and `day` functions are supported. The value entered is converted to year, month, and day and then compared against the sharded table information.

		If the function is empty, this int value will be compared against the sharded table information directly
```

Sample:
If `hired` is of `date` type, the query for the corresponding value inserted is in the format of `'20160101 10:20:20' ,20160101` 
```
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
```
	
If `hired` is of `int` type, the query for the corresponding value inserted will be in the format of `1474961034`. The proxy will first convert it into the corresponding date format (20160927) and then compare it against the sharded table information:
```
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
```


Supported list types:
```
	DATE, DATETIME, TIMESTAMP. `year`, `month`, and `day` functions are supported

	TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT

	CHAR, VARCHAR, BINARY, and VARBINARY.

	CREATE TABLE customers_1 (
	    first_name VARCHAR(25),
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
Note: partitioning uses the less than symbol; therefore, if you want to store the data of the current year (e.g., 2017), you need to create a `<2018` partition. You only need to create partitions up to the current time, and TDSQL will automatically add subsequent partitions (3 by default). Taking YEAR as an example, TDSQL will automatically create partitions of 2018, 2019, and 2020 and increase or decrease them afterwards.


### Supported functions
```
Control Flow Functions

| Name     | Description                  |
| -------- | ---------------------------- |
| CASE     | Case operator                |
| IF()     | If/else construct            |
| IFNULL() | Null if/else construct       |
| NULLIF() | Return NULL if expr1 = expr2 |


 String Functions

| Name               | Description                              |
| ------------------ | ---------------------------------------- |
| ASCII()            | Return numeric value of left-most character |
| BIN()              | Return a string containing binary representation of a number |
| BIT_LENGTH()       | Return length of argument in bits        |
| CHAR()             | Return the character for each integer passed |
| CHAR_LENGTH()      | Return number of characters in argument  |
| CHARACTER_LENGTH() | Synonym for CHAR_LENGTH()                |
| CONCAT()           | Return concatenated string               |
| CONCAT_WS()        | Return concatenate with separator        |
| ELT()              | Return string at index number            |
| EXPORT_SET()       | Return a string such that for every bit set in the value bits, you get an on string and for every unset bit, you get an off string |
| FIELD()            | Return the index (position) of the first argument in the subsequent arguments |
| FIND_IN_SET()      | Return the index position of the first argument within the second argument |
| FORMAT()           | Return a number formatted to specified number of decimal places |
| FROM_BASE64()      | Decode to a base-64 string and return result |
| HEX()              | Return a hexadecimal representation of a decimal or string value |
| INSERT()           | Insert a substring at the specified position up to the specified number of characters |
| INSTR()            | Return the index of the first occurrence of substring |
| LCASE()            | Synonym for LOWER()                      |
| LEFT()             | Return the leftmost number of characters as specified |
| LENGTH()           | Return the length of a string in bytes   |
| LIKE               | Simple pattern matching                  |
| LOAD_FILE()        | Load the named file                      |
| LOCATE()           | Return the position of the first occurrence of substring |
| LOWER()            | Return the argument in lowercase         |
| LPAD()             | Return the string argument, left-padded with the specified string |
| LTRIM()            | Remove leading spaces                    |
| MAKE_SET()         | Return a set of comma-separated strings that have the corresponding bit in bits set |
| MATCH              | Perform full-text search                 |
| MID()              | Return a substring starting from the specified position |
| NOT LIKE           | Negation of simple pattern matching      |
| NOT REGEXP         | Negation of REGEXP                       |
| OCT()              | Return a string containing octal representation of a number |
| OCTET_LENGTH()     | Synonym for LENGTH()                     |
| ORD()              | Return character code for leftmost character of the argument |
| POSITION()         | Synonym for LOCATE()                     |
| QUOTE()            | Escape the argument for use in an SQL statement |
| REGEXP             | Pattern matching using regular expressions |
| REPEAT()           | Repeat a string the specified number of times |
| REPLACE()          | Replace occurrences of a specified string |
| REVERSE()          | Reverse the characters in a string       |
| RIGHT()            | Return the specified rightmost number of characters |
| RLIKE              | Synonym for REGEXP                       |
| RPAD()             | Append string the specified number of times |
| RTRIM()            | Remove trailing spaces                   |
| SOUNDEX()          | Return a soundex string                  |
| SOUNDS LIKE        | Compare sounds                           |
| SPACE()            | Return a string of the specified number of spaces |
| STRCMP()           | Compare two strings                      |
| SUBSTR()           | Return the substring as specified        |
| SUBSTRING()        | Return the substring as specified        |
| SUBSTRING_INDEX()  | Return a substring from a string before the specified number of occurrences of the delimiter |
| TO_BASE64()        | Return the argument converted to a base-64 string |
| TRIM()             | Remove leading and trailing spaces       |
| UCASE()            | Synonym for UPPER()                      |
| UNHEX()            | Return a string containing hex representation of a number |
| UPPER()            | Convert to uppercase                     |
| WEIGHT_STRING()    | Return the weight string for a string    |


 Numeric Functions and Operators

| Name            | Description                              |
| --------------- | ---------------------------------------- |
| ABS()           | Return the absolute value                |
| ACOS()          | Return the arc cosine                    |
| ASIN()          | Return the arc sine                      |
| ATAN()          | Return the arc tangent                   |
| ATAN2(), ATAN() | Return the arc tangent of the two arguments |
| CEIL()          | Return the smallest integer value not less than the argument |
| CEILING()       | Return the smallest integer value not less than the argument |
| CONV()          | Convert numbers between different number bases |
| COS()           | Return the cosine                        |
| COT()           | Return the cotangent                     |
| CRC32()         | Compute a cyclic redundancy check value  |
| DEGREES()       | Convert radians to degrees               |
| DIV             | Integer division                         |
| /               | Division operator                        |
| EXP()           | Raise to the power of                    |
| FLOOR()         | Return the largest integer value not greater than the argument |
| LN()            | Return the natural logarithm of the argument |
| LOG()           | Return the natural logarithm of the first argument |
| LOG10()         | Return the base-10 logarithm of the argument |
| LOG2()          | Return the base-2 logarithm of the argument |
| -               | Minus operator                           |
| MOD()           | Return the remainder                     |
| %, MOD          | Modulo operator                          |
| PI()            | Return the value of pi                   |
| +               | Addition operator                        |
| POW()           | Return the argument raised to the specified power |
| POWER()         | Return the argument raised to the specified power |
| RADIANS()       | Return argument converted to radians     |
| RAND()          | Return a random floating-point value     |
| ROUND()         | Round the argument                       |
| SIGN()          | Return the sign of the argument          |
| SIN()           | Return the sine of the argument          |
| SQRT()          | Return the square root of the argument   |
| TAN()           | Return the tangent of the argument       |
| *               | Multiplication operator                  |
| TRUNCATE()      | Truncate to specified number of decimal places |
| -               | Change the sign of the argument          |


Date and Time Functions

| Name                                   | Description                              |
| -------------------------------------- | ---------------------------------------- |
| ADDDATE()                              | Add time values (intervals) to a date value |
| ADDTIME()                              | Add time                                 |
| CONVERT_TZ()                           | Convert from one time zone to another    |
| CURDATE()                              | Return the current date                  |
| CURRENT_DATE(), CURRENT_DATE           | Synonyms for CURDATE()                   |
| CURRENT_TIME(), CURRENT_TIME           | Synonyms for CURTIME()                   |
| CURRENT_TIMESTAMP(), CURRENT_TIMESTAMP | Synonyms for NOW()                       |
| CURTIME()                              | Return the current time                  |
| DATE()                                 | Extract the date part of a date or datetime expression |
| DATE_ADD()                             | Add time values (intervals) to a date value |
| DATE_FORMAT()                          | Format date as specified                 |
| DATE_SUB()                             | Subtract a time value (interval) from a date |
| DATEDIFF()                             | Subtract two dates                       |
| DAY()                                  | Synonym for DAYOFMONTH()                 |
| DAYNAME()                              | Return the name of the weekday           |
| DAYOFMONTH()                           | Return the day of the month (0-31)       |
| DAYOFWEEK()                            | Return the weekday index of the argument |
| DAYOFYEAR()                            | Return the day of the year (1-366)       |
| EXTRACT()                              | Extract part of a date                   |
| FROM_DAYS()                            | Convert a day number to a date           |
| FROM_UNIXTIME()                        | Format Unix timestamp as a date          |
| GET_FORMAT()                           | Return a date format string              |
| HOUR()                                 | Extract the hour                         |
| LAST_DAY                               | Return the last day of the month for the argument |
| LOCALTIME(), LOCALTIME                 | Synonym for NOW()                        |
| LOCALTIMESTAMP, LOCALTIMESTAMP()       | Synonym for NOW()                        |
| MAKEDATE()                             | Create a date from the year and day of year |
| MAKETIME()                             | Create time from hour, minute, second    |
| MICROSECOND()                          | Return the microseconds from argument    |
| MINUTE()                               | Return the minute from the argument      |
| MONTH()                                | Return the month from the date passed    |
| MONTHNAME()                            | Return the name of the month             |
| NOW()                                  | Return the current date and time         |
| PERIOD_ADD()                           | Add a period to a year-month             |
| PERIOD_DIFF()                          | Return the number of months between periods |
| QUARTER()                              | Return the quarter from a date argument  |
| SEC_TO_TIME()                          | Converts seconds to 'HH:MM:SS' format    |
| SECOND()                               | Return the second (0-59)                 |
| STR_TO_DATE()                          | Convert a string to a date               |
| SUBDATE()                              | Synonym for DATE_SUB() when invoked with three arguments |
| SUBTIME()                              | Subtract times                           |
| SYSDATE()                              | Return the time at which the function executes |
| TIME()                                 | Extract the time portion of the expression passed |
| TIME_FORMAT()                          | Format as time                           |
| TIME_TO_SEC()                          | Return the argument converted to seconds |
| TIMEDIFF()                             | Subtract time                            |
| TIMESTAMP()                            | With a single argument, this function returns the date or datetime expression; with two arguments, the sum of the arguments |
| TIMESTAMPADD()                         | Add an interval to a datetime expression |
| TIMESTAMPDIFF()                        | Subtract an interval from a datetime expression |
| TO_DAYS()                              | Return the date argument converted to days |
| TO_SECONDS()                           | Return the date or datetime argument converted to seconds since Year 0 |
| UNIX_TIMESTAMP()                       | Return a Unix timestamp                  |
| UTC_DATE()                             | Return the current UTC date              |
| UTC_TIME()                             | Return the current UTC time              |
| UTC_TIMESTAMP()                        | Return the current UTC date and time     |
| WEEK()                                 | Return the week number                   |
| WEEKDAY()                              | Return the weekday index                 |
| WEEKOFYEAR()                           | Return the calendar week of the date (1-53) |
| YEAR()                                 | Return the year                          |
| YEARWEEK()                             | Return the year and week                 |

Aggregate (GROUP BY) Functions     

| Name                                   | Description                              |
| -------------------------------------- | ---------------------------------------- |
| AVG()                                   | Return the average value of the argument |
| COUNT()                                 | Return a count of the number of rows returned                                |
| MAX()	                                 | Return the maximum value                 |
| MIN()	                                 | Return the minimum value                 |
| SUM()                                   | Return the sum                           |


Bit Functions and Operators

| Name                                   | Description                              |
| -------------------------------------- | ---------------------------------------- |
|BIT_COUNT()	|Return the number of bits that are set|
|&	|Bitwise AND|
|~	|Bitwise inversion|
|&#124; |Bitwise OR|
|^	|Bitwise XOR|
|<<	|Left shift|
|>>	|Right shift|


Cast Functions and Operators

| Name                                   | Description                              |
| -------------------------------------- | ---------------------------------------- |
|BINARY|	Cast a string to a binary string|
|CAST()|	Cast a value as a certain type|
|CONVERT()|	Cast a value as a certain type|

```

## Read/write Separation
TDSQL supports read/write separation in three modes.
- TDSQL enables the syntax parsing configuration, filters out `select` read requests through syntax parsing, and sends them directly to the slave by default. This mode is highly risky and can be enabled only by [submitting a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- A slave comment flag can be added to send the specified SQL statement to the slave, i.e., adding a flag such as `/*slave*/` in the query, so that the query will be sent to the slave.
- Requests sent by read-only accounts are sent to the slave according to the configured attributes.

## Error Codes and Error Messages
The following error codes have been added for the proxy:
```
	enum proxy_error
	{
	    ER_PROXY_GRAM_ERROR_BEGIN=800,
	
	    ER_PROXY_SANITY_ERROR, /*Incorrect SQL type*/
	    ER_PROXY_BAD_COMMAND,/*Unsupported SQL command*/
	    ER_PROXY_SQL_NOT_SUPPORT,/*Type not supported by TDSQL*/
	    ER_PROXY_SQLUSE_NOT_SUPPORT,/*Operation not supported by TDSQL*/
	    ER_PROXY_ERROR_SHARDKEY, /*The primary and secondary shardkeys was misselected; for example, they should be different and should be certain columns in the table*/
	
	    ER_PROXY_ERROR_SUB_SHARDKEY, /*Not used for now*/
	    ER_PROXY_PRE_DEAL_ERROR, /*Non-compliant join*/
	    ER_PROXY_SHADKEY_ERROR, /*Complex SQL. The shardkey should be included for a derived table.*/
	    ER_PROXY_COMBINE_SQL_ERROR, /*SQL recombination error; for example, there is no corresponding secondary sharded table*/
	    ER_PROXY_SQL_ERROR,/*General SQL error*/
	    ER_PROXY_ONE_SET, /*`count (distinct)` must be sent to only one set*/
	    ER_PROXY_STRICT_ERROR, /*Not used for now*/
	    ER_PROXY_TRANSACTION_ERROR, /*Transaction error*/
	
	
	    ER_PROXY_GRAM_ERROR_END,
	    ER_PROXY_SYSTEM_ERROR_BEGIN=900,
	
	    ER_PROXY_SLICING,
	    ER_PROXY_NO_DEFAULT_SET,/*Set is empty*/
	    ER_PROXY_SOCK_ADDRESS_ERROR,/*Set address is empty*/
	    ER_PROXY_SOCK_ERROR,/*Failed to connect to the backend database*/
	    ER_PROXY_STATUS_ERROR,/*Group status error*/
	    ER_PROXY_UNKNOWN_ERROR, /*Unknown error*/
	
	    ER_PROXY_ERROR_END
	
	
	};
```
Error codes above 900 are system errors and will be alarmed on through the monitoring platform.
