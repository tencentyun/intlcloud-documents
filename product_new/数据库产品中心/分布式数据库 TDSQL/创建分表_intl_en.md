TDSQL supports sharding, i.e., splitting a large table horizontally for storage in multiple databases through shardkey. The method of sharding is described in detail below.

## Selecting a Shardkey
Once the shardkey is set, it cannot be easily modified, so you need to evaluate the case thoroughly in advance. When selecting a shardkey, you should take into account two major factors:
- Whether the data can be stored and accessed in a balanced manner through the shardkey.
- When multiple correlated tables can use the same shardkey. (If the same shardkey is used, data will be stored in the same physical shard, so that `join` operations that needed by most business logics can be performed directly in the same node without going through the distributed transaction logic, which significantly improves the efficiency).


 **Example:** Assume that your business has two tables, one for recording users' basic information, and one for recording users' order information. If user ID is selected as the shardkey, then theoretically data distribution and access will be relatively balanced. At the same time, the basic information and order information of a single user will be stored in the same backend database, which facilitates subsequent operations such as join.


## Creating a Sharded Table
When creating a sharded table, you must specify the value of the shardkey (which is generally added to the end of the table creating statement). This value is a field name in the table and will be used for subsequent SQL routing:

```
	mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
	Query OK, 0 rows affected (0.07 sec)

```
In a TDSQL instance, a shardkey corresponds to the partition field of the backend database, so it must be part of the primary key and all unique indices; otherwise, the table cannot be created:

```
	mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;

	At this point, there is a unique index u_2 that does not contain the shardkey, so the table cannot be created, and the following error will be displayed:
	ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function

	For example, below is a correct statement:
	 create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;;

```	
Because the index of the primary key or unique key has to be globally unique, to implement a globally unique index, you must include the shardkey field.



In addition to the above restrictions, the shardkey field has the following requirements:

	1. The type of the shardkey field must be int, bigint, or smallint/char/varchar.
	2. The value of the shardkey field should not contain Chinese characters, as the gateway will not convert the character set, and different character sets may be routed to different partitions.
	3. Do not update the value of the shardkey field.
	4. shardkey=a should be placed at the end of the SQL statement.
	5. Carry the shardkey field as much as possible when accessing data. This is not mandatory, but SQL statements without shardkey will be routed to all nodes and thus compromise the performance.

>**Note:**
>`shardkey'` is a keyword for the system to identify the shardkey and should not be occupied.
>`Shardkey=noshardkey_allset` is the keyword to specify a table as a broadcast table. This means that the table will not be sharded but stored in every physical shard.

## Common DML Operations

When using a sharded table, there are certain requirements on DML as shown below ("a" is the shardkey):

### It is best to carry the shardkey for `select`
As distributed routing uses hash mode by default, it is best to carry the shardkey for `select`,
- If `=` or `in` is used, the routing will automatically jump to the corresponding shard, which achieves the highest efficiency.
- For example, the following two SQL statements can be directly sent to the corresponding database according to the value of shardkey, which usually takes less than 5 ms.
```
	mysql> select a,b,c from test.test1 where a=2 order by b;
	mysql> select a,b,c from test.test1 where a in (2) order by b;
```
- If no `=` or `in` is used, the distributed system will automatically scan the entire table and then gather the result set at the gateway, which compromises the efficiency:
- For example, the following two SQL statements will be sent to all backend databases, and additional data collection and sorting will be needed, which usually takes 5-20 ms.
```
	mysql> select a,b,c from test.test1 where a>2 order by b;
	mysql> select a,b,c from test.test1 where c=2 order by b;
```

### Shardkey must be included in the `insert/replace` field

The `insert/replace` field must include the shardkey; otherwise, the routing will not know which physical shard to insert data into and the system will refuse to execute the SQL statement.
> **Note:**
>This is not required for broadcast or non-sharded tables.

```
	mysql> insert into test.test1 (b,c) values(4,"record3");
	ERROR 1105 (07000): Proxy Warning - sql have no shardkey

	mysql> insert into test.test1 (a,c) values(4,"record3");
	Query OK, 1 row affected (0.01 sec)
```

### Shardkey must be included in the `delete/update` field

When `delete/update` operations are performed, for security considerations, during the execution of this type of SQL commands, a `where` condition must be present; otherwise, the SQL commands will be refused. It is best to carry the shardkey for the `where` condition, just like `select`.
>**Note:**
>This is not required for broadcast or non-sharded tables.

```
	mysql> delete from test.test1;
	ERROR 1005 (07000): Proxy Warning - sql is not legal,tokenizer_gram went wrong
	mysql> delete from test.test1 where a=1;
	Query OK, 1 row affected (0.01 sec)
```

### Modify the shardkey value
In addition, `update` cannot modify the value of the shardkey field; if necessary, `insert` and then `delete` instead.
>You cannot change the type of the shardkey field, modify the field name, or delete or replace the shardkey field, unless you create a new table.

```
	mysql> update test.test1 set a=10 where d=1;
	ERROR 7013 (HY000): Proxy ERROR:combine_sql_key return null,something went wrong
	mysql> update test.test1 set d=1 where a=1;
	Query OK, 0 rows affected (0.00 sec)
```

## Common Errors

- The table does not have a primary key:
```
	mysql> create table test.e1 ( a int ,b int) shardkey=a;
	ERROR 1105 (HY000): This table type requires a primary key
```

- A primary key or unique key does not contain the shardkey:
```
	mysql> create table test.e2 ( a int not null,b int not null, c char(20) not null,primary key(a,b) ) shardkey=c;
	ERROR 1105 (HY000): A PRIMARY KEY must include all columns in the table's partitioning function
```

- The shardkey is misspelled or has a wrong column name:
```
	mysql> create table test.e3 ( a int key,b int,c char(20)) shardkey1=d;
	ERROR 1911 (HY000): Unknown option 'shardkey1'
	mysql> create table test.e4 ( a int key,b int,c char(20)) shardkey=d;
	ERROR 7008 (HY000): Proxy ERROR:shardkey must be one of the column
```
