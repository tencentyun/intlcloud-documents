> If you want to view or download the full set of development documents, see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

### Creating a Sharded Table

A **sharded table** is an automatically horizontally split (sharded) table. Sharding is a technical scheme where data is distributed in a way similar to consistency hashing to different physical node sets according to the hash value of the shardkey. This is a core feature of almost all distributed databases. The design goal of TDSQL is to **eliminate developers' needs to care about backend sharding**, so that they can use TDSQL like a general database. Therefore, the detailed schemes of sharding are hidden in the design.

When creating a regular sharded table, you must specify the value of the shardkey at the end, which is a field name in the table and will be used for subsequent SQL routing:
```
	mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
	Query OK, 0 rows affected (0.07 sec)
```
In a TDSQL instance, a shardkey corresponds to the partition field of the backend database, so it must be part of the primary key and all unique indices; otherwise, the table cannot be created:
```
	mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;
```
At this point, there is a unique index u_2 that does not contain the shardkey, so the table cannot be created, and the following error will be displayed:
```
	ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function
```
Because the index of the primary key or unique key has to be globally unique, to implement a globally unique index, you must include the shardkey field.

**In sum, the requirements on the shardkey field are as follows:**
1. The shardkey must be part of the primary key and all unique indices;
2. The type of the shardkey field must be int, bigint, or smallint/char/varchar;
3. The value of the shardkey field cannot contain Asian characters:
4. Do not update the value of the shardkey field (if you need to do so, delete the row and insert the new value);
5. `shardkey=a` must be placed after the `create` statement;
6. Carry the shardkey field as much as possible when accessing data. This is not mandatory, but SQL statements without shardkey will be routed to all nodes and thus compromise the efficiency;

> **Note**: Some sharding schemes allow a "non-primary or non-unique key" to be the shardkey field, which, however, may lead to data inconsistency and is therefore prohibited in TDSQL by default.

### Creating a Broadcast Table

**Broadcast tables** are based on small table broadcasting technology. After a broadcast table is created, its full data is available to every node, and all its operations will be broadcast to all physical shards (sets). It is mainly used as a configuration table to improve the performance of cross-set joins.
```
	mysql> create table global_table ( a int, b int key) shardkey=noshardkey_allset;
	Query OK, 0 rows affected (0.06 sec)
```
>Note: A broadcast table uses a distributed transaction mechanism to ensure the atomicity of data writes, so the data in all nodes naturally is exactly identical.

### Creating a Regular Table (Non-sharded Table)

Creating a **regular table (aka non-sharded table)** using the same syntax as MySQL is supported. All the data in this type of tables is stored in the first set:
```
	mysql> create table noshard_table ( a int, b int key);
	Query OK, 0 rows affected (0.02 sec)
```
### Other DDL Operations

Other DDL operations such as `alter` and `drop` use the same syntax as MySQL and will not be detailed here.
