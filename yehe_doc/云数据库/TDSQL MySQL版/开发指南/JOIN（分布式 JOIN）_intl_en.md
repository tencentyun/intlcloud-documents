If you want to view or download the full set of development documents, please see [TDSQL Development Guide](https://intl.cloud.tencent.com/document/product/1042/33352).

Because there are multiple physical nodes in a TDSQL instance, some join operations may involve data of multiple physical nodes. This type of data join is generally called distributed join.

- Data of tables with the same shardkey is automatically stored on the same physical node. Therefore, if related tables are joined on a shardkey equality condition (as shown in the example below), it is equivalent to joining tables on the same physical node, which has the best performance. For more information on how to select the most appropriate shardkey, please see [FAQs](https://intl.cloud.tencent.com/document/product/1042/33328).
- If a join operation involves data across physical nodes, the proxy will pull data from other nodes and cache it first. Due to data transmission over a network, the performance will be affected.

### Joining Tables on a Shardkey Equality Condition (No Performance Loss)
```
	mysql> create table test1 ( a int key, b int, c char(20) ) shardkey=a;
	Query OK, 0 rows affected (1.56 sec)

	mysql> create table test2 ( a int key, d int, e char(20) ) shardkey=a;
	Query OK, 0 rows affected (1.46 sec)

	mysql> insert into test1 (a,b,c) values(1,2,"record1"),(2,3,"record2");
	Query OK, 2 rows affected (0.02 sec)

	mysql> insert into test2 (a,d,e) values(1,3,"test2_record1"),(2,3,"test2_record2");
	Query OK, 2 rows affected (0.02 sec)

	mysql>  select * from test1 left join test2 on test1.a=test2.a where test1.a=1;
	+---+------+---------+---+------+---------------+
	| a | b    | c       | a | d    | e             |
	+---+------+---------+---+------+---------------+
	| 1 |    2 | record1 | 1 |    3 | test2_record1 |
	+---+------+---------+---+------+---------------+
	1 row in set (0.00 sec)

	mysql>  select * from test1 join test2 on test1.a=test2.a;
	+---+------+---------+---+------+---------------+
	| a | b    | c       | a | d    | e             |
	+---+------+---------+---+------+---------------+
	| 1 |    2 | record1 | 1 |    3 | test2_record1 |
	| 2 |    3 | record2 | 2 |    3 | test2_record2 |
	+---+------+---------+---+------+---------------+
	2 rows in set (0.03 sec)
```

### Joining Tables not on a Shardkey Equality Condition (Performance Loss)
```
  mysql>  select * from test1  join test2;
  +---+------+---------+---+------+---------------+
  | a | b    | c       | a | d    | e             |
  +---+------+---------+---+------+---------------+
  | 1 |    2 | record1 | 1 |    3 | test2_record1 |
  | 2 |    3 | record2 | 1 |    3 | test2_record1 |
  | 1 |    2 | record1 | 2 |    3 | test2_record2 |
  | 2 |    3 | record2 | 2 |    3 | test2_record2 |
  +---+------+---------+---+------+---------------+
  4 rows in set (0.06 sec)
```

### Joins Related to Broadcast Tables and Non-sharded Tables (Regular Tables)
- A join operation can be performed between non-sharded tables (regular tables). It is equivalent to joining tables on the same physical node with no performance loss.
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
- A join operation can be performed between broadcast tables and sharded tables. It is equivalent to joining tables on the same physical node with no performance loss.
- A join operation can be performed between broadcast tables. It is equivalent to joining tables on the same physical node with no performance loss.
- A join operation can be performed between non-sharded tables (regular tables) and sharded tables.
```
  mysql> CREATE TABLE `a1` (
    `a` int(11) NOT NULL,
    `b` int(11) DEFAULT NULL,
    `c` char(20) COLLATE utf8_bin DEFAULT NULL,
    PRIMARY KEY (`a`)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin shardkey=a

  mysql> DROP TABLE IF EXISTS TABLE_10;
  CREATE TABLE TABLE_10 (
      INTEGER_ID INTEGER,
      CHARACTER_COL VARCHAR(20),
      CHARACTER_1 CHAR(1),
      PRIMARY KEY(INTEGER_ID)
  )ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin;

  mysql> select * from TABLE_10 left join a1 on TABLE_10.INTEGER_ID=a1.a;
```
