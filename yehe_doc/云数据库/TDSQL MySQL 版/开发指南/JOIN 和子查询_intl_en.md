In TDSQL for MySQL, data is split horizontally across nodes. To improve database performance, we recommend that you prioritize the optimization of table structures and SQL statements, and try not to manipulate data across nodes.

## Recommended SQL Statements
### For multiple sharded tables with a WHERE condition of the same shardkey
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

MySQL> select * from test1 where test1.a in (select a from test2);        
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
| 2 |    3 | record2 |
+---+------+---------+
2 rows in set (0.00 sec)

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

### For non-sharded tables
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

### For broadcast tables
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

### For derived tables where the subquery has a shardkey
```
mysql> select a from (select * from test1 where a=1) as t;
+---+
| a |
+---+
| 1 |
+---+
1 row in set (0.00 sec)
```

## Complex SQL Statements
For SQL statements that cannot be optimized into the recommended statements, cross-node data interaction is required, resulting in a relatively low performance.
Including:
- Queries with subqueries
- Join queries for multiple tables which have different shardkeys or are of different types (for example, non-sharded tables and sharded tables)

In such complex queries, the query conditions will be sent to shards to extract data that actually participates in the query from backend databases. The extracted data will be stored in a local temporary table and then be computed.

Therefore, you need to explicitly specify the query conditions of the tables to avoid performance degradation due to the extraction of large amounts of data.
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

MySQL> select * from test1 where exists (select * from test2 where test2.a=test1.b);
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
+---+------+---------+
1 row in set (0.00 sec)
```

TDSQL also supports many complex UPDATE, DELETE, and INSERT operations.

Note that these operations are based on SELECT operations. As data needs to be extracted into a temporary table on the gateway, we recommend that you explicitly specify the query conditions to avoid performance degradation due to the extraction of large amounts of data.
In addition, the gateway will not lock the extracted data by default, which is slightly different from the official MySQL. If you need to lock the data, you can modify the proxy configuration.

```sql
MySQL [th]> update test1 set test1.c="record" where exists(select 1 from test2 where test1.b=test2.d);
Query OK, 1 row affected (0.00 sec)

MySQL [th]> update test1, test2 set test1.b=2 where test1.b=test2.d;
Query OK, 1 row affected (0.00 sec)

MySQL [th]> insert into test1 select cast(rand()*1024 as unsigned), d, e from test2;
Query OK, 2 rows affected (0.00 sec)

MySQL [th]> delete from test1 where b in (select b from test2);
Query OK, 6 rows affected (0.00 sec)

MySQL [th]> delete from test2.* using test1 right join test2 on test1.a=test2.a where test1.a is null;
Query OK, 2 rows affected (0.00 sec)
```
