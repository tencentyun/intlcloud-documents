This documents takes a sharded table as an example to describe some simple database operations in TDSQL.

## Creating a Table
- For more information on the differences between sharded, non-sharded, and broadcast tables, see [Table Overview](https://intl.cloud.tencent.com/document/product/1042/33358#.E5.88.86.E8.A1.A8.EF.BC.9A.E5.8F.82.E8.80.83.26lt.3B.E5.88.86.E8.A1.A8.26gt.3B).
- For selection restrictions on the shardkey, see [Shardkey Overview](https://intl.cloud.tencent.com/document/product/1042/33379#shardkey.E9.80.89.E6.8B.A9.E7.9A.84.E9.99.90.E5.88.B6).
- When creating a sharded table, the shardkey needs to be specified. Below is the sample code:
```
mysql> create table test1(id int primary key,name varchar(20),addr varchar(20))shardkey=id;
Query OK,0 rows affected(0.15 sec)
```
		
## Inserting Data
>The `insert` field must include the shardkey; otherwise, the operation will be refused.

Insert data into the table just created. Below is the sample code:
```
mysql> insert into test1(id,name);
Query OK,1 rows affected(0.08 sec)
mysql> insert into test3(name,addr) values('example','shenzhen');
ERROR 7013 (HY000): Proxy ERROR:get_shardkeys return error
```

## Querying Data
>When you query data, you are recommended to include the shardkey, so that the distributed route will be automatically redirected to the corresponding shard, achieving the highest efficiency; otherwise, the distributed system will automatically scan the entire table and then aggregate the results at the gateway, which compromises the efficiency.

Below is the sample code for data query:
```
mysql> select id from test1 where id=1;
```

## Deleting Data
>A "where" condition must be included in a "DELETE" operation, and you are recommended to include the shardkey in the "where" condition.

Below is the sample code for data deletion:
```
mysql> delete from test1 where id=1;
Query OK, 1 row affected (0.02 sec)
```
