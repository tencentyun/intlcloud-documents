## Creating a Sharded Table
When creating a sharded table, you must specify the value of shardkey at the end of the SQL statement. The value of shardkey is a field name in the table and will be used for subsequent SQL routing.
```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
Query OK, 0 rows affected (0.07 sec)
```

In a TDSQL instance, the shardkey corresponds to the partition field of the backend database, so it must be part of all primary keys and unique indexes; otherwise, the table cannot be created.

Use case : an error occurs when there are multiple unique indexes.
```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;
```
According to the above SQL statement, there is a unique index `u_2` that does not include the shardkey field, so the table cannot be created and the following error message will be displayed:
```
ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function
```
The index on the primary key or unique key has to be globally unique. To do so, the index must include the shardkey field.

In addition to the above restrictions, the shardkey field has the following requirements:
- The type of the shardkey field must be int, bigint, smallint, char, or varchar.
- The value of the shardkey field should not contain Asian characters, as the proxy will not convert the character set, and different character sets may be routed to different partitions.
- Do not update the value of the shardkey field.
- `shardkey=a` should be placed at the end of the SQL statement.
- We recommend that you specify the value of shardkey in SQL statements when accessing data. This is not mandatory, but SQL statements without shardkey will be routed to all nodes and thus consume more resources.


## Creating a Broadcast Table
You can create small tables (broadcast tables). Each set has all the data of a small table, which makes it easier to perform cross-set joins. In addition, distributed transactions ensure the atomicity of the modification operations, so that the data in all sets is exactly identical.
```
mysql> create table global_table ( a int, b int key) shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.06 sec)
```

## Creating a Non-sharded Table
You can create non-sharded tables using the same syntax as MySQL. All the data in this type of tables is stored in the first set.
```
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)
```
