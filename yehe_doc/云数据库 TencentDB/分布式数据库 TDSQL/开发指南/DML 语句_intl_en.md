## select
We recommend including the shardkey field whose hash value allows the direct routing of SQL request through the proxy to the database instance. Otherwise, the proxy needs to send requests to all database instances in the cluster and aggregates the results, which degrades performance:

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

## insert/replace
Include the shardkey field to avoid errors, because the proxy is unable to determine the target backend database for SQL.

```
mysql> insert into test1 (b,c) values(4,"record3");
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table insert must has field spec

mysql> insert into test1 (a,c) values(4,"record3");
Query OK, 1 row affected (0.01 sec)
```
## delete/update
For security reasons, include the `where` condition to avoid errors.

```
mysql> delete from test1;
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table delete/update must have a where clause

mysql> delete from test1 where a=1;
Query OK, 1 row affected (0.01 sec)
```
