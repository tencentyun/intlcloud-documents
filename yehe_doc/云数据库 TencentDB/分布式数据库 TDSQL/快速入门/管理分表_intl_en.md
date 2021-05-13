This document takes a sharded table as an example to describe some simple database operations in TDSQL for MySQL.

## Creating a Table
- For more information about the differences between sharded, non-sharded, and broadcast tables, please see [Overview](https://intl.cloud.tencent.com/document/product/1042/38142).
- For more information about the restrictions on shardkey, please see [Creating Tables](https://intl.cloud.tencent.com/document/product/1042/38506).
- To create a sharded table, the shardkey needs to be specified. The sample code is as follows:
```
mysql> create table test1(id int primary key,name varchar(20),addr varchar(20))shardkey=id;
Query OK,0 rows affected(0.15 sec)
```
		
## Inserting Data
>!The shardkey must be included in an `INSERT` statement or else the operation will be denied.

Insert data into the table just created. The sample code is as follows:
```
mysql> insert into test1(id,name) VALUES(1,'test');
Query OK,1 rows affected(0.08 sec)
mysql> insert into test3(name,addr) values('example','shenzhen');
ERROR 7013 (HY000): Proxy ERROR:get_shardkeys return error
```

## Querying Data
>!When you query data, we recommend that you include the shardkey in the statement so that the request will be automatically routed to the corresponding shard according to the distributed routes, achieving the highest efficiency; otherwise, TDSQL will automatically scan the entire table and then aggregate the results at the gateway, which compromises the efficiency.

The sample code for querying data is as follows:
```
mysql> select id from test1 where id=1;
```

## Deleting Data
>!A `WHERE` clause must be included in a `DELETE` statement, and we recommend including the shardkey in the `WHERE` clause.

The sample code for deleting data is as follows:
```
mysql> delete from test1 where id=1;
Query OK, 1 row affected (0.02 sec)
```
