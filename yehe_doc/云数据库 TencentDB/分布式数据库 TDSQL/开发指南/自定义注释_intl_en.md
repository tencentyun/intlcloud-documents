By adding a hint in front of an SQL statement, you can achieve specific features. TDSQL provides the following hints:

### Passthrough to Specified Physical Shard
In TDSQL, the proxy will parse the SQL syntax, but there are relatively strict restrictions. If you want to execute an SQL statement in a certain physical shard (set), you can use the SQL passthrough feature.
SQL passthrough: the SQL statement can be passed through to one or more corresponding physical shards (sets) or the set corresponding to the shardkey. Below is a sample:
```
	mysql> select * from test1 where a in (select a from test1);
	ERROR 7009 (HY000): Proxy ERROR:proxy do not support such use yet
	mysql> /*set_1*/select * from test1 where a in (select a from test1);
	Empty set (0.00 sec)
```
Syntax:
```
	/*sets:set_1*/
	/*sets:set_1,set_2*/  
	/*sets:allsets*/
	/*shardkey:10*/
```

### Forced SQL Read/Write Separation Based on Slave
TDSQL supports a variety of read/write separation schemes. The scheme of `/*slave*/` is often fixed into business logic during code implementation for easier use in development. Below is a sample:
```
	mysql> /*slave*/select * from test.ff limit 0;
```


>For more information on how to execute TDSQL-specific SQL statements, please see [Control Commands](https://intl.cloud.tencent.com/document/product/1042/33371).
