
This document describes how to perform simple database operations on a sharded table.

## Creating a table
- For the specific differences among sharded, non-sharded, and broadcast tables, see [Overview](https://intl.cloud.tencent.com/document/product/1042/38142).
- For the restrictions on selecting the shardkey, see [Creating Tables](https://intl.cloud.tencent.com/document/product/1042/38506).
- You need the specify the shardkey when creating a sharded table. Below is the sample code:
```
mysql> create table test1(id int primary key,name varchar(20),addr varchar(20))shardkey=id;
Query OK,0 rows affected(0.15 sec)
```
		
## Inserting data
>!The `insert` field must contain a shardkey; otherwise, the statement will be rejected.

Insert data to the newly created table. Below is the sample code:
```
mysql> insert into test1(id,name) VALUES(1,'test');
Query OK,1 rows affected(0.08 sec)
mysql> insert into test3(name,addr) values('example','shenzhen');
ERROR 7013 (HY000): Proxy ERROR:get_shardkeys return error
```

## Querying data
>!We recommend that you carry a shardkey when querying data, so that the corresponding shard will be automatically redirected to through distributed routing, delivering the highest efficiency; otherwise, the distributed system will automatically perform a full-table scan and aggregate the results on the gateway, which is less efficient.

Below is the sample code for data query:
```
mysql> select id from test1 where id=1;
```

## Deleting data
>!The `delete` field must contain a WHERE condition. We recommend that you include the shardkey in the WHERE condition.

Below is the sample code for data deletion:
```
mysql> delete from test1 where id=1;
Query OK, 1 row affected (0.02 sec)
```
