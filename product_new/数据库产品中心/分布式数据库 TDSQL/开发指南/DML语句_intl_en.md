
> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).


### DML Statements and Syntax (Partial)

**SELECT**: It is recommended to include the shardkey field in the condition; otherwise, TDSQL cannot determine which nodes the SQL should be routed to. In this case, the system automatically scans all tables and gathers the results at the gateway, which may affect the execution efficiency:
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
**INSERT/REPLACE**: The shardkey field must be included; otherwise, TDSQL cannot determine which nodes the SQL should be routed to. Random routing may cause data exception. Therefore, TDSQL will directly refuse to execute INSERT/REPLACE statements without shardkey:
```
	mysql> insert into test1 (b,c) values(4,"record3");
	ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
		Shard table insert must has field spec

	mysql> insert into test1 (a,c) values(4,"record3");
	Query OK, 1 row affected (0.01 sec)
```
**DELETE/UPDATE:** Similarly, for security reasons, **when an SQL of this type is executed in a non-sharded or broadcast table, it must contain the `where` condition**; otherwise, it will not be executed:
```
	mysql> delete from test1;
	ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
		Shard table delete/update must have a where condition

	mysql> delete from test1 where a=1;
	Query OK, 1 row affected (0.01 sec)
```
