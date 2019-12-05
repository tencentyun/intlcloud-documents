
> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

#### Subquery

TDSQL currently only supports derived tables with shardkey.
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
	
