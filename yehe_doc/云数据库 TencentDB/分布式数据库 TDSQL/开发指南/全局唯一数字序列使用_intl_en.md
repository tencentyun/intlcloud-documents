The `auto_increment` keyword can be used to create a global unique auto-incremental field which is definitely global unique but may not be monotonically increasing. You can use `auto_increment` as instructed below.

## Create
```
mysql> create table auto_inc (a int,b int,c int auto_increment,d int,key auto(c),primary key p(a,d)) shardkey=d;
Query OK, 0 rows affected (0.12 sec)
```

## Insert
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

If a process such as switching or restarting occurs, there will be holes in the auto-increment fields, for example:
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
Use `select last_insert_id()` to query the last inserted value of the auto-incremental field:
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
Currently, you can use `select last_insert_id()` to query the auto-incremental field in a sharded table or broadcast table. Such an operation is unsupported in a non-sharded table.
