
## 概述

TDSQL是部署在腾讯云上的一种支持自动水平拆分的 Shared Nothing 架构的分布式数据库。用户只需在创建表的时候指定一个分表字段，由TDSQL系统负责数据的路由以及汇总，应用层可以对数据库进行透明操作。

### 软件版本

本开发手册对应的内核版本为：1.13.21-M-V2R501D002，可通过`/*Proxy*/show status`语句查询。

**注意**：TDSQL 不支持4.0以下版本以及压缩协议，建议在**客户端使用时增加-c选项**，以便使用注释透传功能。

### 功能特性

TDSQL可以提供水平扩容能力，适合海量数据的场景。具有以下功能特性：

- 支持创建分表、单表、广播表

- 提供灵活的读写分离模式

- 支持全局Order by，Group by，Limit操作

- 支持Sum，Count，Avg，Min，Max五种聚合函数

- 支持跨Set的JOIN、子查询功能

- 支持预处理协议

- 支持全局唯一字段，支持Sequence

- 支持分布式事务

- 支持二级分区

- 提供特定的SQL查询整个集群的配置和状态


### 使用限制

TDSQL分布式实例高度兼容 MySQL的协议和语法，由于分布式数据库和单机数据库存在较大的架构差异，对MySQL的部分功能和小语法有使用限制。

**TDSQL大类限制**

- 暂不支持自定义函数、事件、表空间
- 暂不支持视图、存储过程、触发器、游标
- 暂不支持外键、自建分区、临时表
- 暂不支持复合语句，例如：BEGIN END，LOOP，UNION的语句
- 暂不支持主备同步相关的SQL语言

**TDSQL小语法限制**

TDSQL分布式实例暂不支持DDL、DML、管理SQL语言的部分语法，具体限制如下：

- DDL
  * 暂不支持CREATE TABLE ... SELECT 
  * 暂不支持CREATE TEMPORARY TABLE 
  * 暂不支持CREATE/DROP/ALTER SERVER/LOGFILE GROUP/
  * 暂不支持ALTER对分表键(shardkey)进行改名，但可以修改类型
  * 暂不支持RENAME
- DML
  * 暂不支持SELECT INTO OUTFILE/INTO DUMPFILE/INTO var_name
  * 暂不支持query_expression_options，如：HIGH_PRIORITY/STRAIGHT_JOIN/SQL_SMALL_RESULT/ 					SQL_BIG_RESULT/SQL_BUFFER_RESULT/SQL_CACHE/SQL_NO_CACHE/SQL_CALC_FOUND_ROWS
  * 暂不支持非SELECT的子查询
  * 暂不支持不带列名的INSERT/REPLACE
  * 暂不支持全局的DELETE/UPDATE使用ORDER BY/LIMIT
  * 暂不支持不带WHERE条件的UPDATE/DELETE
  * 暂不支持LOAD DATA/XML
  * 暂不支持SQL中使用DELAYED和LOW_PRIORITY
  * 暂不支持SQL中对于变量的引用和操作，比如 SET @c=1, @d=@c+1; SELECT @c, @d
  * 暂不支持index_hint
  * 暂不支持HANDLER/DO
- 管理SQL语句
  * 暂不支持ANALYZE/CHECK/CHECKSUM/OPTIMIZE/REPAIR TABLE，需要用透传语法
  * 暂不支持CACHE INDEX
  * 暂不支持FLUSH
  * 暂不支持KILL（非跨城版本数据库支持）
  * 暂不支持LOAD INDEX INTO CACHE
  * 暂不支持RESET
  * 暂不支持SHUTDOWN
  * 暂不支持SHOW BINARY LOGS/BINLOG EVENTS
  * 暂不支持SHOW WARNINGS/ERRORS和LIMIT/COUNT的组合

### 系统连接方式

TDSQL通过Proxy接口提供和MySQL兼容的连接方式，用户可以通过IP地址、端口号、用户名以及密码连接TDSQL 系统，连接语句如下：

```
mysql -h10.10.10.10 -P3306 -utest12 -ptest123 -c
```

## SQL语句语法的使用

分布式实例高度兼容MySQL的连接协议和语法，支持SSL加密，也支持Navicat、JDBC、ODBC、PHP、Python等相关协议和语法，例如:

```
private final String USERNAME = "test";  
private final String PASSWORD = "123456"; 
private final String DRIVER = "com.mysql.jdbc.Driver";   
private final String URL = "jdbc:mysql://10.10.10.10:3306?userunicode=true&characterEncoding=utf8mb4";  
private Connection connection;  
private PreparedStatement pstmt;  
private ResultSet resultSet;  
```

但由于架构的差异，对于SQL语句有一定的限制，为了更好的发挥分布式数据库的优势，用户尽量使用本文推荐的SQL相关协议和语法。

### DDL语句

本节主要介绍了使用DDL语句创建表和常用DDL语句说明。

#### 创建表

TDSQL分布式实例支持创建分表、单表和广播表。

**注意**：如无特殊要求，建议用户在分布式实例中创建分表进行使用。

**创建分表**

分表即自动水平拆分的表（Shard表），水平拆分是基于分表键（Shardkey）采用类似于一致性 Hash 方式，根据 Hash 后的值分配到不同的节点组中的一种技术方案。如果两张表分表键相等，其对应的行将存储在相同的物理节点组中。这种场景称为组拆分（Groupshard）,可以迅速提高应用层联合查询等语句的处理效率。

在创建普通的分表时，必须最后指定分表键（Shardkey）的值，该值为表的字段名字，用于后续SQL语句的路由选择。语句如下：

```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
Query OK, 0 rows affected (0.07 sec)
```

在分布式实例中，Shardkey对应后端数据库的分区字段，因此必须是主键以及所有唯一索引的一部分，否则无法创建表。详见如下：

```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;

此时有一个唯一索引u_2不包含shardkey，无法创建表，将报如下错误：
ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function
因为主键索引或者unique key索引需要全局唯一，而要实现全局唯一索引则必须包含shardkey字段。
```

**综述：Shardkey字段的主要要求如下：**

- Shardkey 字段必须是主键以及所有唯一索引的一部分；
- Shardkey字段的类型必须为int,bigint,smallint/char/varchar；
- Shardkey字段的值不能为中文，因为Proxy不会转换字符集，所以不同字符集可能会路由到不同的分区；
- 不要Update shardkey字段的值；
- Shardkey=a 需放在SQL语句的最后；
- 访问的数据尽量包含Shardkey字段，否则不带Shardkey字段的SQL语句会路由到所有节点，将消耗较多资源。

**注意**：部分分表方案支持“非主键或唯一索引”成为 Shardkey字段，但此类方案会导致数据不一致，因此 TDSQL 默认禁止“非主键或唯一索引”成为 Shardkey字段。

**创建广播表**

广播表又名小表广播功能，创建广播表后，每个节点都有该表的全量数据，且该表的所有操作都将广播到所有物理分片（set）中。

广播表主要用于提升跨节点组（ Set） 的Join 操作的性能，保证修改操作的原子性，以确保所有Set数据完全一致。常用于配置表等，语句如下：

```
mysql> create table global_table ( a int, b int key) shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.06 sec)
```

**创建普通表**

普通表：又名单表（Noshard表），无需拆分且没有做任何特殊处理的表。其语法和MySQL完全一样，所有该类型表的全量数据默认存放在第一个物理节点组（Set）中，具体语句如下：

```
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)
```

**注意**：由于单表默认放置在物理节点组（Set）中，如果创建过多单表，可能会导致第一个物理节点组（Set）的负载过大。

#### 其他 DDL语句操作

Alter，Drop 等其他 DDL 语句操作，与 MySQL 语法完全一致，此处不再赘述。



### 账号和权限系统语句

TDSQL通过以下两种方式进行账号和权限设置：

- 通过赤兔管理平台系统，授权方式参见《TDSQL赤兔管理平台用户手册》。
- 通过SQL进行授权，本节主要介绍通过SQL进行授权。

SQL授权方式为：Proxy支持命令行的权限控制，SQL解析后发送任务给决策集群（Zookeeper），由调度集群（Scheduler）完成后返回应答，再由Proxy返回客户端。

TDSQL支持创建/修改/删除/重命名用户账号（Create/Alter/Drop/Rename User），设置账号密码（Set password），授权权限（Grant），回收授权（Revoke）等命令，具体语法如下：

**创建用户账号（Create User）语句**

```
CREATE USER [IF NOT EXISTS]
user [auth_option] [, user [auth_option]] ... 

auth_option: {
IDENTIFIED BY 'auth_string'
| IDENTIFIED BY PASSWORD 'hash_string'
}
```

**注意**：暂不支持tls_option、resource_option、password_option和lock_option指令。

**删除用户账号（Drop User）语句**

```
 DROP USER [IF EXISTS] user [, user] ...
```

**修改用户账号（Alter User）语句**

```
ALTER USER [IF EXISTS]
user [auth_option] [, user [auth_option]] ...

auth_option: {
IDENTIFIED BY 'auth_string'
| IDENTIFIED BY PASSWORD 'hash_string'
}
```

**注意**：MariaDB 10.2以下版本不支持修改用户（Alter User）指令。

**重命名用户账号（Rename User）语句**

```
RENAME USER old_user TO new_user [, old_user TO new_user] ...
```

**设置账号密码（Set Password）语句**

```
SET PASSWORD FOR user = password_option

password_option: { 'auth_string'
| PASSWORD('auth_string')
}
```

**注意**：用户必须设置密码，不能为空。

举例如下：

```
set password for test1@'10.10.*' = 'test';

set password for test1@'10.10.*' = password('test');
```

**授权权限（Grant）语句**

```
GRANT
priv_type [(column_list)] [, priv_type [(column_list)]] ...
ON [object_type] priv_level
TO user [auth_option] [, user [auth_option]] ... 
[WITH GRANT OPTION]

object_type: { TABLE
| FUNCTION
| PROCEDURE }

priv_level: { *
| *.*
| db_name.*
| db_name.tbl_name
| tbl_name
| db_name.routine_name
}

auth_option: {
IDENTIFIED BY 'auth_string'
|IDENTIFIED BY PASSWORD 'hash_string'
}

```

**注意**：Grant语句和MySQL语法兼容，暂时不支持tls_option和resource_option命令。	

举例如下：

```
grant all on *.* to test1@'%' identified by 'test123'

grant all on *.* to test2@'%' identified by 'test',
test3 identified by password '*94E7199DCF1F8F391A73B989F90B147EDAF3908E' 
with grant option

grant select (col1), insert (col1, col2) on mydb.mytbl to 'someuser'@'somehost';

grant execute on procedure mydb.myproc to 'someuser'@'somehost';

```

**回收授权（Revoke）语句**

```
REVOKE
priv_type [(column_list)] [, priv_type [(column_list)]] ... 
ON [object_type] priv_level
FROM user [, user] ...

REVOKE ALL [PRIVILEGES], GRANT OPTION 
FROM user [, user] ...

```

举例如下：

```
revoke all,grant option from test1

revoke select,insert on db1.* from test2@'10.*';
```



### DML语句

本节主要介绍 DML 语句中常用的Select（查询）、Insert（插入）、Replace（替换）、Update（更新）及Delete（删除）指令。

**SELECT指令**

执行Select指令时，建议在条件中增加Shardkey字段，语句如下。

**说明**：Proxy根据该字段的Hash值，将SQL指令请求路由至对应的数据库实例进行处理；否则SQL指令将发送到集群所有的数据库实例，Proxy再进行数据库返回的结果集进行聚合，将影响执行效率。

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

**INSERT/REPLACE指令**

执行Insert/Replace命令时，字段必须包含Shardkey，否则系统会拒绝执行SQL命令，因为Proxy无法判断SQL语句发送的后端数据库节点位置。语句显示如下：

```
mysql> insert into test1 (b,c) values(4,"record3");
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table insert must has field spec

mysql> insert into test1 (a,c) values(4,"record3");
Query OK, 1 row affected (0.01 sec)
```

**DELETE/UPDATE指令**

执行Delete/Update命令时，为了安全考虑，**分表和广播表执行该 SQL指令的时候必须带“ where ”条件**，否则系统拒绝执行该SQL命令。语句如下：

```
mysql> delete from test1;
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table delete/update must have a where clause

mysql> delete from test1 where a=1;
Query OK, 1 row affected (0.01 sec)
```

**注意**：为了防止用户误操作，建议尽量不要使用全表的Update/Delete指令；如必须使用该指令，可在SQL语句中增加‘where 1’ 条件。

## 注释透传功能

注释透传指支持透传 SQL语句到对应的一个或者多个物理分片（Set），并透传到分表键（Shardkey）对应的分片（Set）中的操作方式。

对于分布式实例，Proxy 会对 SQL进行语法解析，但有比较严格的限制，如果用户想在某个物理分片（set）中执行SQL语句，可以使用该功能。语句如下：

```
MySQL [test]> delete from s ;
ERROR 664 (HY000): Proxy ERROR:SQL is too complex, only applicable to noshard table: Shard table delete/update must have a where clause
MySQL [test]> /*sets:allsets*/delete from s;
Query OK, 0 rows affected (0.02 sec)
```

具体语法如下：

```
/*sets:set_1*/
/*sets:set_1,set_2*/ （set名字可以通过/*proxy*/show status查询）
/*sets:allsets */   
/*shardkey:10*/ 
```

**注意**：透传SQL语句进行写操作时，因Proxy不解析SQL语句，所以如果往两个及以上节点组（Set）进行透传写操作，系统将不使用分布式事务，可能导致数据不一致，因此对于写操作建议一次透传一个节点组（set）。

## JOIN和子查询功能

对于分布式实例，数据水平拆分在各个节点上。为了提高性能，应用层应优先优化表结构和SQL语句，使数据尽量采用不跨节点的方式存储。

- 如果Join 相关的表有分表键相等条件（如下示例），由于分表的一致性原则，会让这部分数据自动存储到同一物理节点，此时相当于单机Join，数据处理效率将更高，是我们推荐的使用方式。
- 如果涉及到跨物理节点数据，此时 Proxy 会先从其他节点拉取数据并缓存，由于涉及到网络数据传输，将降低数据处理效率。

### 推荐JOIN方式

**分表之间**

如果分表之间带有分表键相等的条件，则相当于单机Join，性能将无损失。语句如下：

```sql
MySQL > select * from test1 join test2 where test1.a=test2.a;     
+---+------+---------+---+------+---------------+
| a | b    | c       | a | d    | e             |
+---+------+---------+---+------+---------------+
| 1 |    2 | record1 | 1 |    3 | test2_record1 |
| 2 |    3 | record2 | 2 |    3 | test2_record2 |
+---+------+---------+---+------+---------------+
2 rows in set (0.00 sec)

MySQL > select * from test1 left join test2 on test1.a<test2.a where test1.a=1;
+---+------+---------+------+------+---------------+
| a | b    | c       | a    | d    | e             |
+---+------+---------+------+------+---------------+
| 1 |    2 | record1 |    2 |    3 | test2_record2 |
+---+------+---------+------+------+---------------+
1 row in set (0.00 sec)
```

**单表之间**

单表与单表之间，相当于单机 Join，性能将无损失。语句如下：

```sql
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)

mysql> create table noshard_table_2 ( a int, b int key);
Query OK, 0 rows affected (0.00 sec)

mysql> select * from noshard_table,noshard_table_2;
Empty set (0.00 sec)

mysql> insert into noshard_table (a,b) values(1,2),(3,4);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> insert into noshard_table_2 (a,b) values(10,20),(30,40);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from noshard_table,noshard_table_2;
+------+---+------+----+
| a    | b | a    | b  |
+------+---+------+----+
|    1 | 2 |   10 | 20 |
|    3 | 4 |   10 | 20 |
|    1 | 2 |   30 | 40 |
|    3 | 4 |   30 | 40 |
+------+---+------+----+
4 rows in set (0.00 sec)
```

**分表和广播表**

跨分片的分表与广播表，相当于单机 Join，性能将无损失。语句如下：

```sql
 MySQL> create table global_test(a int key, b int)shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.00 sec)

MySQL> insert into global_test(a, b) values(1,1),(2,2);
Query OK, 2 rows affected (0.00 sec)

MySQL> select * from test1, global_test;
+---+------+---------+---+------+
| a | b    | c       | a | b    |
+---+------+---------+---+------+
| 1 |    2 | record1 | 1 |    1 |
| 2 |    3 | record2 | 1 |    1 |
| 1 |    2 | record1 | 2 |    2 |
| 2 |    3 | record2 | 2 |    2 |
+---+------+---------+---+------+
4 rows in set (0.00 sec)
```

### 子查询

TDSQL 目前只支持带 Shardkey字段的派生表(derived table)查询，其性能无损失，语句如下：

```
mysql> select a from (select * from test1 where a=1) as t;
+---+
| a |
+---+
| 1 |
+---+
1 row in set (0.00 sec)


```

### 复杂SQL查询

对于不满足推荐方式的SQL语句，因需要做跨节点的数据交互，将会导致性能变差，可能影响以下查询活动：

- 包含子查询的查询。
- 带有Having条件的查询。
- 需要进行多个排序/分组/去重的查询，例如：Count (Distinct ID)。
- 多表的Join查询，且参与查询的各表的分区字段(Shardkey)不相等，或者同时涉及不同类型的表（例如，单表和分表）。

对于此类复杂查询，可以通过条件下推，将从后端数据库中抽取出参与查询的数据，并存放在本地临时表中，通过临时表中的数据进行计算。

因此用户需要指定参与查询的表的条件，避免因抽取大量数据而导致性能受损。相关语句如下：

```sql
mysql> create table test1 ( a int key, b int, c char(20) ) shardkey=a;
Query OK, 0 rows affected (1.56 sec)

mysql> create table test2 ( a int key, d int, e char(20) ) shardkey=a;
Query OK, 0 rows affected (1.46 sec)

mysql> insert into test1 (a,b,c) values(1,2,"record1"),(2,3,"record2");
Query OK, 2 rows affected (0.02 sec)

mysql> insert into test2 (a,d,e) values(1,3,"test2_record1"),(2,3,"test2_record2");
Query OK, 2 rows affected (0.02 sec)

mysql> select * from test1 join test2 on test1.b=test2.d;
+---+------+---------+---+------+---------------+
| a | b    | c       | a | d    | e             |
+---+------+---------+---+------+---------------+
| 2 |    3 | record2 | 1 |    3 | test2_record1 |
| 2 |    3 | record2 | 2 |    3 | test2_record2 |
+---+------+---------+---+------+---------------+
2 rows in set (0.00 sec)

MySQL> select * from test1 where test1.a in (select a from test2);        
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
| 2 |    3 | record2 |
+---+------+---------+
2 rows in set (0.00 sec)

MySQL> select * from test1 where exists (select * from test2 where test2.a=test1.b);
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
+---+------+---------+
1 row in set (0.00 sec)

MySQL> select a, count(1) from test1 where exists (select * from test2 where test2.a=test1.a) group by a;        
+---+----------+
| a | count(1) |
+---+----------+
| 1 |        1 |
| 2 |        1 |
+---+----------+
2 rows in set (0.00 sec)

MySQL> select distinct count(1) from test1 where exists (select * from test2 where test2.a=test1.a) group by a;   
+----------+
| count(1) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)

MySQL> select count(distinct a) from test1 where exists (select * from test2 where test2.a=test1.a);        
+-------------------+
| count(distinct a) |
+-------------------+
|                 2 |
+-------------------+
1 row in set (0.00 sec)
```

## 分布式事务说明

由于事务操作的数据通常跨多个物理节点，在分布式数据库中，类似方案即称为分布式事务。TDSQL支持普通分布式事务协议和XA分布式事务协议。TDSQL（5.7或以上版本）默认支持分布式事务，且对客户端透明，使用户像使用单机事务一样方便。

TDSQL 分布式事务采用两阶段提交算法（2PC）保证事务的原子性（Atomicity）和一致性（Consistency），隔离级别配置为 Read committed, Repeatable read，或 Serializable。

**普通分布式事务协议**

```
begin; 	# 开启事务
... 	# 跨set的增、删、改、查等非DDL操作
commit; # 提交事务
```

**XA分布式事务协议**

XA 分布式事务利用 MySQL XA 分布式事务协议，提供了强一致的事务支持，能获得最接近单机事务的使用体验。语句如下：

```
xa begin ''; 		# 开启xa事务，事务标识由系统内部生成，因此传入空字符串
...			 		# 跨set的增、删、改、查等非DDL操作
select gtid();		# 获取当前xa事务的标识，下面假定为'xid'
xa prepare 'xid';	# 准备事务
xa commit/rollback 'xid'; # 提交或回滚事务
```

**新增事务接口状态描述**

| 接口                          | 描述                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| select gtid()                 | 获取当前分布式事务的gtid（事务的全局唯一性标识），如果该事务不是分布式事务，则返回空。<br />普通分布式事务标识的格式为：'‘网关id’-‘proxy随机值’-‘序列号’-‘时间戳’-‘分区号’<br />例如：c46535fe-b6-dd-595db6b8-25<br />XA分布式事务标识的格式为：‘ex’-‘网关id’-‘proxy随机值’-‘序列号’-‘时间戳’-‘分区号’<br />例如：ex-c46535fe-b6-dd-595db6b8-25 |
| select gtid_state(“事务标识”) | 在事务提交异常之后（默认3s），用来获取事务的状态。可能出现以下结果：<br />**COMMIT**：代表标识该事务已经或者最终会被提交<br />**ABORT**：代表标识该事务最终会被回滚<br />**空**：代表事务的状态会在一个小时之后清除。可能出现两种情况：（1）一个小时之后查询，标识事务状态已经清除；（2）一个小时以内查询，标识事务最终被回滚。 |
| xa boost（事务标识）          | 普通事务提交（Commit）发送异常之后，事务在一段时间内（默认30s）由后台组件自动提交或者回滚，如果用户不愿意等待，可以反复调用该接口，促使系统及时地提交或回滚事务。 |
| xa lockwait                   | 显示当前分布式事务的等待关系（可以使用dot命令将输出转化为等待关系图）。 |
| xa show                       | 当前网关上正在运行的分布式事务。                             |

## 全局唯一数字序列的使用

TDSQL支持全局唯一数字序列（auto_increment）的使用；暂时仅保证自增字段全局唯一和递增性，但是不保证单调递增（即按时间顺序的绝对递增性）。

全局唯一数字序列（auto_increment） 长 8 字节，最大为 18446744073709551616，因此，您无需担心该值溢出。具体使用方法如下：

**创建自增字段的表**

	mysql> create table auto_inc (a int,b int,c int auto_increment,d int,key auto(c),primary key p(a,d)) shardkey=d;
	Query OK, 0 rows affected (0.12 sec)

**插入自增字段的分表**

	mysql>  insert into shard.auto_inc ( a,b,d,c) values(1,2,3,0),(1,2,4,0);
	Query OK, 2 rows affected (0.05 sec)
	Records: 2  Duplicates: 0  Warnings: 0
	
	mysql> select * from shard.auto_inc;
	+---+------+---+---+
	| a | b    | c | d |
	+---+------+---+---+
	| 1 |    2 | 2 | 4 |
	| 1 |    2 | 1 | 3 |
	+---+------+---+---+
	2 rows in set (0.03 sec)

**自增长字段的空洞处理**

由于 auto_increment 仅保证自增字段全局唯一和递增性，如果在节点调度切换、重启等过程中，自增长字段中间会出现空洞，例如：

    mysql> insert into shard.auto_inc ( a,b,d,c) values(11,12,13,0),(21,22,23,0);
    Query OK, 2 rows affected (0.03 sec)
    mysql> select * from shard.auto_inc;
    +‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
    | a | b | c | d |
    +‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
    | 21 | 22 | 2002 | 23 |
    | 1 | 2 | 2 | 4 |
    | 1 | 2 | 1 | 3 |
    | 11 | 12 | 2001 | 13 |
    +‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
    4 rows in set (0.01 sec)

可更改当前值，命令如下：

	alter table auto_inc auto_increment=100

**注意**：目前不支持通过insert into auto_inc set c=100  语法插入数据，如果用户要指定自增的值，需要使用

insert into auto_inc (c) values(100) 语法进行插入。

**通过select last_insert_id()命令获取自增值**

如果用户不指定自增值，可以通过select last_insert_id()命令获取，暂不支持直接从Insert返回包获取，详见如下：

```
mysql> insert into auto_inc ( a,b,d,c) values(1,2,3,0),(1,2,4,0);
Query OK, 2 rows affected (0.73 sec)
	
mysql> select * from auto_inc;
+---+------+------+---+
| a | b    | c    | d |
+---+------+------+---+
| 1 |    2 | 4001 | 3 |
| 1 |    2 | 4002 | 4 |
+---+------+------+---+
2 rows in set (0.00 sec)

mysql> select last_insert_id();
+------------------+
| last_insert_id() |
+------------------+
| 4001             |
+------------------+
1 row in set (0.00 sec)
```

**注意**：Select last_insert_id()命令只能与Shard表和广播表的自增字段一起使用，不支持与Noshard表的使用。

## SEQUENCE

 本节主要介绍创建、删除、查询和使用Sequence，以及获取显示Sequence的值。Sequence语法和MariaDB兼容，但是需保证分布式全局递增且数值唯一。

**注意**：

- 为了避免用户使用Sequence关键字，从该版本开始，Proxy须在该关键字前面加`tdsql_`前缀。如果已使用Sequence不带前缀的关键字，用户需要修改，或者先提工单规避。
- 目前Sequence为保证分布式全局数值唯一，导致性能较差，主要适用于并发不高的场景。

**创建 Sequence**

```
create tdsql_sequence test.s1 start with 12 tdsql_minvalue 10 maxvalue 50000  tdsql_increment by 5  tdsql_nocycle 
create tdsql_sequence test.s2 start with 12 tdsql_minvalue 10 maxvalue 50000  tdsql_increment by 1  tdsql_cycle 

以上SQL语句包含开始值、最小值、最大值、步长及是否回绕5个参数，参数都应为正整数。
```

 **删除Sequence**

```
drop tdsql_sequence test.s1
```

**查询Sequence**

```
show create tdsql_sequence test.s2
```

**使用Sequence**

使用Sequence获取下一个数值，语句如下：

```
select tdsql_nextval(test.s2)
select next value for test.s2
```

------

  举例如下：

```
mysql> select tdsql_nextval(test.s1);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.18 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.13 sec)

mysql> select tdsql_nextval(test.s1);
+----+
| 17 |
+----+
| 17 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 13 |
+----+
| 13 |
+----+
1 row in set (0.00 sec)

mysql> select next value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.01 sec)

```

nextval命令可以用在Insert语句中。使用如下：

```
mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
+----+------+
1 row in set (0.00 sec)

mysql> insert into test.t1(a,b) values(tdsql_nextval(test.s2),3);
Query OK, 1 row affected (0.01 sec)

mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
| 14 |    3 |
+----+------+
2 rows in set (0.00 sec)
```

如需获取上一次的值，以连接相关数据：如果之前没有用nextval命令获取过数据，数值将返回为0。

```
select tdsql_lastval(test.s1)
select tdsql_previous value for test.s1;
```

------

```
mysql> select tdsql_lastval(test.s1);
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)

mysql> select tdsql_previous value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)
```

设置下一个序列数值，只能比当前数值大，否则将返回数值为0。

```
select tdsql_setval(test.s2,1000,bool use)  //  use 默认为1，表示1000这个值用过了，下一次不包含1000，如果为0，则下一个从1000开始。
```

设置下一个序列数值时，如果比当前数值小，则系统将没有反应。

```
mysql> select tdsql_nextval(test.s2);
+----+
| 15 |
+----+
| 15 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_setval(test.s2,10);
+---+
| 0 |
+---+
| 0 |
+---+
1 row in set (0.03 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 16 |
+----+
| 16 |
+----+

```

如果比当前数值大，成功返回当前设置的值。

```
mysql> select tdsql_setval(test.s2,20);
+----+
| 20 |
+----+
| 20 |
+----+
1 row in set (0.02 sec)
mysql> select tdsql_nextval(test.s2);
+----+
| 21 |
+----+
| 21 |
+----+
1 row in set (0.01 sec)
```

## 数据导入导出

- **数据导出**

​       系统支持mysqldump命令导出数据，在 TDSQL 控制台的参数设置中可以设置 net_write_timeout 参数：set global net_write_timeout=28800。


```
mysqldump --compact --single-transaction --no-create-info -c
               db_name table_name  -utest -h10.10.10.10 -P3336  -ptest123
               
说明：db名和table名的参数根据实际情况选择。
```

**注意**：如果导出的数据要导入到其他的TDSQL环境，必须加上-c选项。

- **数据导入**

​        需提供专门的导入工具进行数据导入，完成加载数据输出文件（Load data outfile）对应数据的导入，语句如下：

```
[tdengine@TENCENT64 ~/]$./load_data

format:./load_data mode0/mode1 proxy_host proxy_port user password db_table shardkey_index file field_terminate filed_enclosed

    example:./load_data mode1 10.10.10.10 3336 test test123 shard.table  1 '/tmp/datafile'  ' ' ''

该工具的原理是将源文件按照shardkey的路由规则，切分成多个文件，然后将每个文件单独透传到对应的后端数据库中。

  注:1、源文件必须以'\n'作为换行符。
	 2、mode0只切分源文件，不做数据导入，一般用于调试，正式导入数据使用mode1指令。
	 3、shardkey_index从0开始，如果shardkey在第2个字段，则shardkey_index为1。
```

## 预处理协议

TDSQL 支持预处理协议，使用方式与单机 MySQL 相同，例如：

- PREPARE Syntax
- EXECUTE Syntax

二进制协议的支持：

- COM_STMT_PREPARE
- COM_STMT_EXECUTE

举例如下：

	mysql> select * from test1;
	+---+------+
	| a | b    |
	+---+------+
	| 5 |    6 |
	| 3 |    4 |
	| 1 |    2 |
	+---+------+
	3 rows in set (0.03 sec)
	
	mysql> prepare ff from "select * from test1 where a=?";
	Query OK, 0 rows affected (0.00 sec)
	Statement prepared
	
	mysql> set @aa=3;
	Query OK, 0 rows affected (0.00 sec)
	
	mysql> execute ff using @aa;
	+---+------+
	| a | b    |
	+---+------+
	| 3 |    4 |
	+---+------+
	1 row in set (0.06 sec)

**注意**：目前TDSQL只对Prepare/Execute命令做语法兼容，从性能角度的话，在分布式下建议用户尽量不要使用该种方式，直接使用文本协议。

## 二级分区

二级分区是将特定条件的数据进行分区处理，TDSQL支持Range和List两种格式的二级分区，具体建表语法和MySQL分区语法类似。

TDSQL只用Hash方式进行数据拆分，不利于删除特定条件的数据（例如，流水类型），为便于删除旧数据，可以使用二级分区语法。

**注意**：分区使用小于符号“<”，如果要存储当年数据（例如，2017），需要创建小于往后一年（<2018）的分区，用户只需创建到当前的时间分区。TDSQL会自动增加后续分区，默认往后创建3个分区，以Year为例，TDSQL会自动往后创建3年（2018年、2019年、2020年）的分区，后续也会自动增减。

- **Range支持类型**

	- DATE，DATETIME，TIMESTAMP
	  	 —支持year，month，day函数，函数为空和day函数一样
	
	- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT
	  	—支持year，month，day函数，此时传入的值转换为年月日，然后和分表信息进行对比
	
	函数为空则使用该Int值和分表信息进行对比。

举例如下：

如果Hired是Date类型，则查询插入对应的值格式为 '20160101 10:20:20' ,20160101 ，语句如下：

	CREATE TABLE employees_int (
	    id INT key NOT NULL,
	    fname VARCHAR(30),
	    lname VARCHAR(30),
	    hired date,
	    separated DATE NOT NULL DEFAULT '9999-12-31',
	    job_code INT,
	    store_id INT
	)
	shardkey=id 
	PARTITION BY RANGE ( month(hired) ) (
	    PARTITION p0 VALUES LESS THAN (199102),
	    PARTITION p1 VALUES LESS THAN (199603),
	    PARTITION p2 VALUES LESS THAN (200101)
	);

如果Hired是Int类型，则查询插入对应的值格式为1474961034，Proxy首先会转换成对应的Date格式，20160927，然后和分表信息进行对比。语句如下：

	CREATE TABLE employees_int (
	    id INT key NOT NULL,
	    fname VARCHAR(30),
	    lname VARCHAR(30),
	    hired int,
	    separated DATE NOT NULL DEFAULT '9999-12-31',
	    job_code INT,
	    store_id INT
	)
	shardkey=id 
	PARTITION BY RANGE ( month(hired) ) (
	    PARTITION p0 VALUES LESS THAN (199102),
	    PARTITION p1 VALUES LESS THAN (199603),
	    PARTITION p2 VALUES LESS THAN (200101)
	);

- **List支持类型**

	- DATE，DATETIME，TIMESTAMP     —支持年月日函数
	
	- TINYINT, SMALLINT, MEDIUMINT, INT (INTEGER), and BIGINT
	
	- CHAR, VARCHAR, BINARY, and VARBINARY
	
	举例如下：
	
	```
	 CREATE TABLE customers_1 (
	    first_name VARCHAR(25) key,
	    last_name VARCHAR(25),
	    street_1 VARCHAR(30),
	    street_2 VARCHAR(30),
	    city VARCHAR(15),
	    renewal DATE
	) shardkey=first_name
	PARTITION BY LIST (city) (
	    PARTITION pRegion_1 VALUES IN('1', '2', '3'),
	    PARTITION pRegion_2 VALUES IN('4', '5', '6'),
	    PARTITION pRegion_3 VALUES IN('7', '8', '9'),
	    PARTITION pRegion_4 VALUES IN('10', '11', '12')
	);
	```

**删除和新增二级分区**

删除和新增二级分区的格式和单机MySQL一致，语句如下：

```
alter table customers_1 drop partition pRegion_1;

alter table customers_1 add partition (partition pRegion_5 VALUES IN('13', '14', '15'));
```

**注意**：TDSQL不支持除Range和List二级分区以外的其他分区操作，例如，Reorganize。

## 读写分离模式

读写分离的基本原理是让主节点 (Master) 处理事务性操作，例如：增加（INSERT）、更新（UPDATE）、删除（DELETE）操作，让从节点 (Slave) 处理查询（SELECT）操作，将读写功能分开处理，以降低主节点处理数据的压力。

TDSQL 默认支持读写分离功能，架构中的每个从机都支持只读能力，如果配置有多个从机，将由网关集群（TProxy）自动分配到低负载从机上，以支撑大型应用程序的读取流量。

支持以下三种模式的读写分离操作。

- Proxy开启语法解析的配置，通过语法解析过滤出用户选择的读请求，默认把读请求直接发给备机。

- 通过增加Slave注释标记，将指定的SQL指令发往备机。即在SQL中添加`/*slave*/`标记，该SQL会发送给备机。

  ​      **说明**：系统还支持` /*slave:slaveonly*/`,` /*slave:20*/`,` /*slave:slaveonly,20*/`三种形式。数值表示备机（Slave）应该满足的延迟；Slaveonly表示在没有符合条件的备机（Slave）时，不会将查询发送给主节点。

- 创建只读账号，由只读账号发送请求，系统会根据配置的属性发给备机。

## 连接保护

连接保护是当网关与后端DB连接断开时（例如，后端DB发生主备切换），保持客户端和网关之间的连接不断开的使用方式。网关与DB断开连接后的保护流程如下：

- 当Proxy正在执行SQL语句时与DB的连接断开，则Proxy断开与该SQL相关的所有连接（除Proxy与客户端之间的连接），并告知用户如下错误：

```c++
ER_PROXY_TRANSACTION_ERROR // 正在处理事务状态
ER_PROXY_CONN_BROKEN_ERROR // 非事务状态
```

- 如果Proxy与DB的连接断开时，用户Session处于`普通事务`状态，系统将执行如下流程动作：（图中错误码都为ER_PROXY_TRANSACTION_ERROR）：

```sequence
非事务状态-->事务中(ACTIVE): BEGIN
事务中(ACTIVE)-->ROLLBACK ONLY状态: PROXY与DB连接断开
ROLLBACK ONLY状态-->ROLLBACK ONLY状态: SQL(返回错误，要求用户ROLLBACK事务)

ROLLBACK ONLY状态-->事务回滚: ROLLBACK / BEGIN
ROLLBACK ONLY状态-->事务回滚: COMMIT(proxy返回错误信息，提示用户事务已经回滚)

ROLLBACK ONLY状态-->断开用户连接: 超时
```

- 如果Proxy与后端连接断开时，用户正处于`XA 事务`状态，系统将执行如下流程动作：（图中错误码都为ER_PROXY_TRANSACTION_ERROR）：

```sequence
非事务状态->事务中(ACTIVE、IDLE): XA BEGIN ''
事务中(ACTIVE、IDLE)-->ROLLBACK ONLY状态: PROXY与DB连接断开
ROLLBACK ONLY状态-->ROLLBACK ONLY状态:   普通SQL / XA COMMIT 'xid'(报错)
ROLLBACK ONLY状态->ROLLBACK状态: XA ROLLBACK 'xid'

事务中(ACTIVE、IDLE)-->PREPARED状态: XA PREPARE 'xid'
PREPARED状态-->PREPARED状态: PROXY与DB(或Client)连接断开
PREPARED状态->ROLLBACK状态: XA ROLLBACK 'xid'
PREPARED状态->COMMIT状态: XA COMMIT 'xid'
ROLLBACK ONLY状态-->断开用户连接: 超时
```

- 如果用户在事务中Proxy与后端DB发生连接断开事件，如果用户在`超时`之前还没有回滚事务，则Proxy断开与用户的连接。超时参数在Proxy的配置文件中，显示如下：

```json
<server_close timeout="60"/>

```

## 数据库管理语句

通过SQL语句可以查看Proxy的配置以及状态信息，支持命令如下：

```
mysql> /*proxy*/help;
+-----------------------+-------------------------------------------------------+
| command               | description                                           |
+-----------------------+-------------------------------------------------------+
| show config           | show config from conf                                 |
| show status           | show proxy status,like route,shardkey and so on       |
| set sys_log_level=N   | change the sys debug level N should be 0,1,2,3        |
| set inter_log_level=N | change the interface debug level N should be 0,1      |
| set inter_time_open=N | change the interface time debug level N should be 0,1 |
| set sql_log_level=N   | change the sql debug level N should be 0,1            |
| set slow_log_level=N  | change the slow debug level N should be 0,1           |
| set slow_log_ms=N     | change the slow ms                                    |
| set log_clean_time=N  | change the log clean days                             |
| set log_clean_size=N  | change the log clean size in GB                       |
+-----------------------+-------------------------------------------------------+
10 rows in set (0.00 sec)

mysql> /*proxy*/show config;
+-----------------+--------------------+
| config_name     | value              |
+-----------------+--------------------+
| version         | V2R120D001         |
| mode            | group shard        |
| rootdir         | /shard_922         |
| sys_log_level   | 0                  |
| inter_log_level | 0                  |
| inter_time_open | 0                  |
| sql_log_level   | 0                  |
| slow_log_level  | 0                  |
| slow_log_ms     | 1000               |
| log_clean_time  | 1                  |
| log_clean_size  | 1                  |
| rw_split        | 1                  |
| ip_pass_through | 0                  |
+-----------------+--------------------+
14 rows in set (0.00 sec)

mysql> /*proxy*/show status;
+-----------------------------+------------------------------------------------------------------------------+
| status_name                 | value                                                                        |
+-----------------------------+------------------------------------------------------------------------------+
| cluster                     | group_1499858910_79548                                                       |
| set_1499859173_1:ip         | 10.*.*.*:5025;10.*.*.*:5025@1@IDC_4@0,10.*.*.*:5025@1@IDC_2@0 |
| set_1499859173_1:hash_range | 0---31                                                                       |
| set_1499911640_3:ip         | 10.*.*.*:5026;10.*.*.*:5026@1@IDC_4@0,10.*.*.*:5026@1@IDC_2@0 |
| set_1499911640_3:hash_range | 32---63                                                                      |
| set                         | set_1499859173_1,set_1499911640_3                                            |
```

同时Proxy增强Explain的返回结果，并显示Proxy修改后的SQL语句。具体如下：

```
mysql> explain select * from test1;
+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
| id   | select_type | table | type | possible_keys | key  | key_len | ref  | rows | Extra | info                                    |
+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
|    1 | SIMPLE      | test1 | ALL  | NULL          | NULL | NULL    | NULL |   16 |       | set_2,explain select * from shard.test1 |
|    1 | SIMPLE      | test1 | ALL  | NULL          | NULL | NULL    | NULL |   16 |       | set_1,explain select * from shard.test1 |
+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
2 rows in set (0.03 sec)
```

## 支持的语言结构

分布式实例支持所有MySQL使用的文字格式，包括如下：

- String Literals
- Numeric Literals
- Date and Time Literals
- Hexadecimal Literals
- Bit-Value Literals
- Boolean Literals
- NULL Values

**String Literals格式**

String Literals 是一个 bytes 或者 characters 的序列，两端被单引号 ' 或者双引号 " 包围，目前TDSQL不支持ANSI_QUOTES SQL MODE，双引号 " 包围的始终认为是String Literals，而不是Identifier。

不支持 character set introducer格式，即：[_charset_name]'string' [COLLATE collation_name]格式。

支持如下转义字符：

```
\0: ASCII NUL (X’00’) 字符
\‘: 单引号
\“: 双引号
\b: 退格符号
\n: 换行符
\r: 回车符
\t: tab 符（制表符）
\z: ASCII 26 (Ctrl + Z)
\\: 反斜杠 \
\%: \%
\_: _
```

**Numeric Literals格式**

数值字面值包括Integer类型 、 Decimal 类型、浮点数字面值。

Integer 可以包括“ . ”作为小数点分隔，数字前加字符“ -” 、“ +” 来表示正数或者负数。

精确数值字面值可以表示多种格式，如格式：1, .2, 3.4, -5, -6.78, +9.10。

科学记数法，如格式：1.2E3, 1.2E-3, -1.2E3, -1.2E-3。

**Date and Time Literals格式**

Date支持如下格式：

```
'YYYY-MM-DD' or 'YY-MM-DD'
'YYYYMMDD' or 'YYMMDD'
YYYYMMDD or YYMMDD

例如：'2012-12-31', '2012/12/31', '2012^12^31',  '2012@12@31'  '20070523' , '070523' 
```

Datetime、Timestamp支持如下格式：

```
'YYYY-MM-DD HH:MM:SS' or 'YY-MM-DD HH:MM:SS'
'YYYYMMDDHHMMSS' or 'YYMMDDHHMMSS'
YYYYMMDDHHMMSS or YYMMDDHHMMSS 

例如：'2012-12-31 11:30:45', '2012^12^31 11+30+45', '2012/12/31 11*30*45',  '2012@12@31 11^30^45'，19830905132800 
```

**Hexadecimal Literals格式**

Hexadecimal Literals支持的格式如下：

```
X'01AF'
X'01af'
x'01AF'
x'01af'
0x01AF
0x01af
```

**Bit-Value Literals格式**

Bit-Value Literals支持的格式如下：

```
b'01'
B'01'
0b01
```

**Boolean Literals格式**

常量 True=1 和 False =0，其不区分大小写。

```
mysql>  SELECT TRUE, true, FALSE, false;
+------+------+-------+-------+
| TRUE | TRUE | FALSE | FALSE |
+------+------+-------+-------+
|    1 |    1 |     0 |     0 |
+------+------+-------+-------+
1 row in set (0.03 sec)
```

**NULL Values**

NULL 代表数据为空，不区分大小写，与命令 \N(不区分大小写) 同义。

需要注意的是 NULL 跟 0 的意义不一样，跟空字符串 '' 的意义也不一样。

## 支持的字符集和时区

TDSQL在后端存储支持 MySQL 的所有字符集和字符序。具体显示如下：

```
mysql> show character set;
+----------+---------------------------------+---------------------+--------+
| Charset  | Description                     | Default collation   | Maxlen |
+----------+---------------------------------+---------------------+--------+
| big5     | Big5 Traditional Chinese        | big5_chinese_ci     |      2 |
| dec8     | DEC West European               | dec8_swedish_ci     |      1 |
| cp850    | DOS West European               | cp850_general_ci    |      1 |
| hp8      | HP West European                | hp8_english_ci      |      1 |
| koi8r    | KOI8-R Relcom Russian           | koi8r_general_ci    |      1 |
| latin1   | cp1252 West European            | latin1_swedish_ci   |      1 |
| latin2   | ISO 8859-2 Central European     | latin2_general_ci   |      1 |
| swe7     | 7bit Swedish                    | swe7_swedish_ci     |      1 |
| ascii    | US ASCII                        | ascii_general_ci    |      1 |
| ujis     | EUC-JP Japanese                 | ujis_japanese_ci    |      3 |
| sjis     | Shift-JIS Japanese              | sjis_japanese_ci    |      2 |
| hebrew   | ISO 8859-8 Hebrew               | hebrew_general_ci   |      1 |
| tis620   | TIS620 Thai                     | tis620_thai_ci      |      1 |
| euckr    | EUC-KR Korean                   | euckr_korean_ci     |      2 |
| koi8u    | KOI8-U Ukrainian                | koi8u_general_ci    |      1 |
| gb2312   | GB2312 Simplified Chinese       | gb2312_chinese_ci   |      2 |
| greek    | ISO 8859-7 Greek                | greek_general_ci    |      1 |
| cp1250   | Windows Central European        | cp1250_general_ci   |      1 |
| gbk      | GBK Simplified Chinese          | gbk_chinese_ci      |      2 |
| latin5   | ISO 8859-9 Turkish              | latin5_turkish_ci   |      1 |
| armscii8 | ARMSCII-8 Armenian              | armscii8_general_ci |      1 |
| utf8     | UTF-8 Unicode                   | utf8_general_ci     |      3 |
| ucs2     | UCS-2 Unicode                   | ucs2_general_ci     |      2 |
| cp866    | DOS Russian                     | cp866_general_ci    |      1 |
| keybcs2  | DOS Kamenicky Czech-Slovak      | keybcs2_general_ci  |      1 |
| macce    | Mac Central European            | macce_general_ci    |      1 |
| macroman | Mac West European               | macroman_general_ci |      1 |
| cp852    | DOS Central European            | cp852_general_ci    |      1 |
| latin7   | ISO 8859-13 Baltic              | latin7_general_ci   |      1 |
| utf8mb4  | UTF-8 Unicode                   | utf8mb4_general_ci  |      4 |
| cp1251   | Windows Cyrillic                | cp1251_general_ci   |      1 |
| utf16    | UTF-16 Unicode                  | utf16_general_ci    |      4 |
| utf16le  | UTF-16LE Unicode                | utf16le_general_ci  |      4 |
| cp1256   | Windows Arabic                  | cp1256_general_ci   |      1 |
| cp1257   | Windows Baltic                  | cp1257_general_ci   |      1 |
| utf32    | UTF-32 Unicode                  | utf32_general_ci    |      4 |
| binary   | Binary pseudo charset           | binary              |      1 |
| geostd8  | GEOSTD8 Georgian                | geostd8_general_ci  |      1 |
| cp932    | SJIS for Windows Japanese       | cp932_japanese_ci   |      2 |
| eucjpms  | UJIS for Windows Japanese       | eucjpms_japanese_ci |      3 |
| gb18030  | China National Standard GB18030 | gb18030_chinese_ci  |      4 |
+----------+---------------------------------+---------------------+--------+
41 rows in set (0.02 sec)
```

**查看当前连接的相关字符集**

```
mysql> show variables like "%char%";
+--------------------------+-----------------------------------------------------+
| Variable_name            | Value                                               |
+--------------------------+-----------------------------------------------------+
| character_set_client     | latin1                                              |
| character_set_connection | latin1                                              |
| character_set_database   | utf8                                                |
| character_set_filesystem | binary                                              |
| character_set_results    | latin1                                              |
| character_set_server     | utf8                                                |
| character_set_system     | utf8                                                |
| character_sets_dir       | /data/tdsql_run/8812/percona-5.7.17/share/charsets/ |
+--------------------------+-----------------------------------------------------+
```

**设置当前连接的相关字符集**

```
mysql> set names utf8;
Query OK, 0 rows affected (0.03 sec)

mysql> show variables like "%char%";
+--------------------------+-----------------------------------------------------+
| Variable_name            | Value                                               |
+--------------------------+-----------------------------------------------------+
| character_set_client     | utf8                                                |
| character_set_connection | utf8                                                |
| character_set_database   | utf8                                                |
| character_set_filesystem | binary                                              |
| character_set_results    | utf8                                                |
| character_set_server     | utf8                                                |
| character_set_system     | utf8                                                |
| character_sets_dir       | /data/tdsql_run/8811/percona-5.7.17/share/charsets/ |
+--------------------------+-----------------------------------------------------+
```

**注意**：TDSQL 不支持通过命令行设置参数，需要通过云控制台进行设置。

**通过设置time_zone变量修改时区相关的属性**

```
mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | SYSTEM |
+------------------+--------+
2 rows in set (0.00 sec)

mysql> create table test.tt (ts timestamp, dt datetime,c int) shardkey=c;
Query OK, 0 rows affected (0.49 sec)

mysql>  insert into test.tt (ts,dt,c)values ('2017-10-01 12:12:12', '2017-10-01 12:12:12',1);
Query OK, 1 row affected (0.09 sec)

mysql> select * from test.tt;
+---------------------+---------------------+------+
| ts                  | dt                  | c    |
+---------------------+---------------------+------+
| 2017-10-01 12:12:12 | 2017-10-01 12:12:12 |    1 |
+---------------------+---------------------+------+
1 row in set (0.04 sec)

mysql> set time_zone = '+12:00';
Query OK, 0 rows affected (0.00 sec)

mysql> show variables like '%time_zone%';
+------------------+--------+
| Variable_name    | Value  |
+------------------+--------+
| system_time_zone | CST    |
| time_zone        | +12:00 |
+------------------+--------+
2 rows in set (0.00 sec)

mysql> select * from test.tt;
+---------------------+---------------------+------+
| ts                  | dt                  | c    |
+---------------------+---------------------+------+
| 2017-10-01 16:12:12 | 2017-10-01 12:12:12 |    1 |
+---------------------+---------------------+------+
1 row in set (0.06 sec)
```

## 支持的数据类型

分布式数据库支持MySQL所有数据类型，包括数字类型、字符类型、日期时间类型、空间数据类型和Json数据类型。

**数字类型**

分布式实例兼容整型、浮点型和定点型三种数字类型，具体兼容类型如下：

- 整型支持INTEGER、 INT、SMALLINT、TINYINT、 MEDIUMINT、BIGINT七种类型，相关信息详见如下表。

| 类型      | 字节数 | 最小值(有符号/无符号)  | 最大值(有符号/无符号)                    |
| --------- | ------ | ---------------------- | ---------------------------------------- |
| TINYINT   | 1      | -128/0                 | 127/255                                  |
| SMALLINT  | 2      | -32768/0               | 32767/65535                              |
| MEDIUMINT | 3      | -8388608/0             | 8388607/16777215                         |
| INT       | 4      | -2147483648/0          | 2147483647/4294967295                    |
| BIGINT    | 8      | -9223372036854775808/0 | 9223372036854775807/18446744073709551615 |

- 浮点型支持FLOAT和DOUBLE，格式支持FLOAT(M,D) 、REAL(M,D) 、 DOUBLE PRECISION(M,D)。

- 定点型支持DECIMAL和NUMERIC，格式DECIMAL(M,D)。

**字符类型**

TDSQL支持如下字符类型：

```
CHAR 和 VARCHAR Types
BINARY 和 VARBINARY Types
BLOB 和 TEXT Types
	TINYBLOB，TINYTEXT，MEDIUMBLOB,MEDIUMTEXT，LONGBLOB，LONGTEXT
ENUM Type
SET Type
```

**日期类型**

TDSQL支持如下时间类型：

```
DATE, DATETIME,  TIMESTAMP Types
TIME Type
YEAR Type
```

**空间数据类型**

TDSQL支持如下空间数据类型：

```
GEOMETRY
POINT
LINESTRING
POLYGON

MULTIPOINT
MULTILINESTRING
MULTIPOLYGON
GEOMETRYCOLLECTION
```

**Json数据类型**

支持存储Json格式的数据类型，以便更加有效的对Json进行处理，同时又能提早检查错误。语句如下：

**注意**：对Json类型的字段进行排序时，不支持混合类型排序。例如，不能将String类型和Int类型做比较，同类型排序只支持数值类型和String类型，其它类型排序暂不处理。

```sql
mysql>  CREATE TABLE t1 (jdoc JSON,a int) shardkey=a;
Query OK, 0 rows affected (0.30 sec)

mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": "value2"}',1);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO t1 (jdoc,a)VALUES('{"key1": "value1", "key2": 2}',2);

mysql> INSERT INTO t1 (jdoc,a)VALUES('[1, 2,',5);
ERROR 3140 (22032): Invalid JSON text: "Invalid value." at position 6 in value for column 't1.jdoc'.

mysql> select * from t1;
+--------------------------------------+---+
| jdoc                                 | a |
+--------------------------------------+---+
| {"key1": "value1", "key2": "value2"} | 1 |
| {"key1": "value1", "key2": 2}        | 2 |
+--------------------------------------+---+
2 rows in set (0.00 sec)

```

## 支持的函数

分布式实例支持以下7种类型的函数：

- 流程控制函数（Control Flow Functions）
- 字符串函数（String Functions）
- 数字函数（Numeric Functions and Operators）
- 日期时间函数（Date and Time Functions）
- 聚合函数（Aggregate (GROUP BY) Functions）
- 位函数（Bit Functions and Operators）
- 转换函数（Cast Functions and Operators）

以上类型的各函数具体描述如下：

**流程控制函数（Control Flow Functions）**

| 函数名   | 描述                         |
| -------- | ---------------------------- |
| CASE     | Case operator                |
| IF()     | If/else construct            |
| IFNULL() | Null if/else construct       |
| NULLIF() | Return NULL if expr1 = expr2 |


 **字符串函数（String Functions）**

| 函数名             | 描述                                                         |
| ------------------ | ------------------------------------------------------------ |
| ASCII()            | Return numeric value of left-most character                  |
| BIN()              | Return a string containing binary representation of a number |
| BIT_LENGTH()       | Return length of argument in bits                            |
| CHAR()             | Return the character for each integer passed                 |
| CHAR_LENGTH()      | Return number of characters in argument                      |
| CHARACTER_LENGTH() | Synonym for CHAR_LENGTH()                                    |
| CONCAT()           | Return concatenated string                                   |
| CONCAT_WS()        | Return concatenate with separator                            |
| ELT()              | Return string at index number                                |
| EXPORT_SET()       | Return a string such that for every bit set in the value bits, you get an on string and for every unset bit, you get an off string |
| FIELD()            | Return the index (position) of the first argument in the subsequent arguments |
| FIND_IN_SET()      | Return the index position of the first argument within the second argument |
| FORMAT()           | Return a number formatted to specified number of decimal places |
| FROM_BASE64()      | Decode to a base-64 string and return result                 |
| HEX()              | Return a hexadecimal representation of a decimal or string value |
| INSERT()           | Insert a substring at the specified position up to the specified number of characters |
| INSTR()            | Return the index of the first occurrence of substring        |
| LCASE()            | Synonym for LOWER()                                          |
| LEFT()             | Return the leftmost number of characters as specified        |
| LENGTH()           | Return the length of a string in bytes                       |
| LIKE               | Simple pattern matching                                      |
| LOAD_FILE()        | Load the named file                                          |
| LOCATE()           | Return the position of the first occurrence of substring     |
| LOWER()            | Return the argument in lowercase                             |
| LPAD()             | Return the string argument, left-padded with the specified string |
| LTRIM()            | Remove leading spaces                                        |
| MAKE_SET()         | Return a set of comma-separated strings that have the corresponding bit in bits set |
| MATCH              | Perform full-text search                                     |
| MID()              | Return a substring starting from the specified position      |
| NOT LIKE           | Negation of simple pattern matching                          |
| NOT REGEXP         | Negation of REGEXP                                           |
| OCT()              | Return a string containing octal representation of a number  |
| OCTET_LENGTH()     | Synonym for LENGTH()                                         |
| ORD()              | Return character code for leftmost character of the argument |
| POSITION()         | Synonym for LOCATE()                                         |
| QUOTE()            | Escape the argument for use in an SQL statement              |
| REGEXP             | Pattern matching using regular expressions                   |
| REPEAT()           | Repeat a string the specified number of times                |
| REPLACE()          | Replace occurrences of a specified string                    |
| REVERSE()          | Reverse the characters in a string                           |
| RIGHT()            | Return the specified rightmost number of characters          |
| RLIKE              | Synonym for REGEXP                                           |
| RPAD()             | Append string the specified number of times                  |
| RTRIM()            | Remove trailing spaces                                       |
| SOUNDEX()          | Return a soundex string                                      |
| SOUNDS LIKE        | Compare sounds                                               |
| SPACE()            | Return a string of the specified number of spaces            |
| STRCMP()           | Compare two strings                                          |
| SUBSTR()           | Return the substring as specified                            |
| SUBSTRING()        | Return the substring as specified                            |
| SUBSTRING_INDEX()  | Return a substring from a string before the specified number of occurrences of the delimiter |
| TO_BASE64()        | Return the argument converted to a base-64 string            |
| TRIM()             | Remove leading and trailing spaces                           |
| UCASE()            | Synonym for UPPER()                                          |
| UNHEX()            | Return a string containing hex representation of a number    |
| UPPER()            | Convert to uppercase                                         |
| WEIGHT_STRING()    | Return the weight string for a string                        |


 **数字函数（Numeric Functions and Operators）**

| 函数名          | 描述                                                         |
| --------------- | ------------------------------------------------------------ |
| ABS()           | Return the absolute value                                    |
| ACOS()          | Return the arc cosine                                        |
| ASIN()          | Return the arc sine                                          |
| ATAN()          | Return the arc tangent                                       |
| ATAN2(), ATAN() | Return the arc tangent of the two arguments                  |
| CEIL()          | Return the smallest integer value not less than the argument |
| CEILING()       | Return the smallest integer value not less than the argument |
| CONV()          | Convert numbers between different number bases               |
| COS()           | Return the cosine                                            |
| COT()           | Return the cotangent                                         |
| CRC32()         | Compute a cyclic redundancy check value                      |
| DEGREES()       | Convert radians to degrees                                   |
| DIV             | Integer division                                             |
| /               | Division operator                                            |
| EXP()           | Raise to the power of                                        |
| FLOOR()         | Return the largest integer value not greater than the argument |
| LN()            | Return the natural logarithm of the argument                 |
| LOG()           | Return the natural logarithm of the first argument           |
| LOG10()         | Return the base-10 logarithm of the argument                 |
| LOG2()          | Return the base-2 logarithm of the argument                  |
| -               | Minus operator                                               |
| MOD()           | Return the remainder                                         |
| %, MOD          | Modulo operator                                              |
| PI()            | Return the value of pi                                       |
| +               | Addition operator                                            |
| POW()           | Return the argument raised to the specified power            |
| POWER()         | Return the argument raised to the specified power            |
| RADIANS()       | Return argument converted to radians                         |
| RAND()          | Return a random floating-point value                         |
| ROUND()         | Round the argument                                           |
| SIGN()          | Return the sign of the argument                              |
| SIN()           | Return the sine of the argument                              |
| SQRT()          | Return the square root of the argument                       |
| TAN()           | Return the tangent of the argument                           |
| *               | Multiplication operator                                      |
| TRUNCATE()      | Truncate to specified number of decimal places               |
| -               | Change the sign of the argument                              |

**日期时间函数（Date and Time Functions）**

| 函数名                                 | 描述                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| ADDDATE()                              | Add time values (intervals) to a date value                  |
| ADDTIME()                              | Add time                                                     |
| CONVERT_TZ()                           | Convert from one time zone to another                        |
| CURDATE()                              | Return the current date                                      |
| CURRENT_DATE(), CURRENT_DATE           | Synonyms for CURDATE()                                       |
| CURRENT_TIME(), CURRENT_TIME           | Synonyms for CURTIME()                                       |
| CURRENT_TIMESTAMP(), CURRENT_TIMESTAMP | Synonyms for NOW()                                           |
| CURTIME()                              | Return the current time                                      |
| DATE()                                 | Extract the date part of a date or datetime expression       |
| DATE_ADD()                             | Add time values (intervals) to a date value                  |
| DATE_FORMAT()                          | Format date as specified                                     |
| DATE_SUB()                             | Subtract a time value (interval) from a date                 |
| DATEDIFF()                             | Subtract two dates                                           |
| DAY()                                  | Synonym for DAYOFMONTH()                                     |
| DAYNAME()                              | Return the name of the weekday                               |
| DAYOFMONTH()                           | Return the day of the month (0-31)                           |
| DAYOFWEEK()                            | Return the weekday index of the argument                     |
| DAYOFYEAR()                            | Return the day of the year (1-366)                           |
| EXTRACT()                              | Extract part of a date                                       |
| FROM_DAYS()                            | Convert a day number to a date                               |
| FROM_UNIXTIME()                        | Format Unix timestamp as a date                              |
| GET_FORMAT()                           | Return a date format string                                  |
| HOUR()                                 | Extract the hour                                             |
| LAST_DAY                               | Return the last day of the month for the argument            |
| LOCALTIME(), LOCALTIME                 | Synonym for NOW()                                            |
| LOCALTIMESTAMP, LOCALTIMESTAMP()       | Synonym for NOW()                                            |
| MAKEDATE()                             | Create a date from the year and day of year                  |
| MAKETIME()                             | Create time from hour, minute, second                        |
| MICROSECOND()                          | Return the microseconds from argument                        |
| MINUTE()                               | Return the minute from the argument                          |
| MONTH()                                | Return the month from the date passed                        |
| MONTHNAME()                            | Return the name of the month                                 |
| NOW()                                  | Return the current date and time                             |
| PERIOD_ADD()                           | Add a period to a year-month                                 |
| PERIOD_DIFF()                          | Return the number of months between periods                  |
| QUARTER()                              | Return the quarter from a date argument                      |
| SEC_TO_TIME()                          | Converts seconds to 'HH:MM:SS' format                        |
| SECOND()                               | Return the second (0-59)                                     |
| STR_TO_DATE()                          | Convert a string to a date                                   |
| SUBDATE()                              | Synonym for DATE_SUB() when invoked with three arguments     |
| SUBTIME()                              | Subtract times                                               |
| SYSDATE()                              | Return the time at which the function executes               |
| TIME()                                 | Extract the time portion of the expression passed            |
| TIME_FORMAT()                          | Format as time                                               |
| TIME_TO_SEC()                          | Return the argument converted to seconds                     |
| TIMEDIFF()                             | Subtract time                                                |
| TIMESTAMP()                            | With a single argument, this function returns the date or datetime expression; with two arguments, the sum of the arguments |
| TIMESTAMPADD()                         | Add an interval to a datetime expression                     |
| TIMESTAMPDIFF()                        | Subtract an interval from a datetime expression              |
| TO_DAYS()                              | Return the date argument converted to days                   |
| TO_SECONDS()                           | Return the date or datetime argument converted to seconds since Year 0 |
| UNIX_TIMESTAMP()                       | Return a Unix timestamp                                      |
| UTC_DATE()                             | Return the current UTC date                                  |
| UTC_TIME()                             | Return the current UTC time                                  |
| UTC_TIMESTAMP()                        | Return the current UTC date and time                         |
| WEEK()                                 | Return the week number                                       |
| WEEKDAY()                              | Return the weekday index                                     |
| WEEKOFYEAR()                           | Return the calendar week of the date (1-53)                  |
| YEAR()                                 | Return the year                                              |
| YEARWEEK()                             | Return the year and week                                     |

**聚合函数（Aggregate (GROUP BY) Functions）**     

| 函数名  | 描述                                          |
| ------- | --------------------------------------------- |
| AVG()   | Return the average value of the argument      |
| COUNT() | Return a count of the number of rows returned |
| MAX()   | Return the maximum value                      |
| MIN()   | Return the minimum value                      |
| SUM()   | Return the sum                                |

**位函数（Bit Functions and Operators）**

| 函数名      | 描述                                   |
| ----------- | -------------------------------------- |
| BIT_COUNT() | Return the number of bits that are set |
| &           | Bitwise AND                            |
| ~           | Bitwise inversion                      |
| &#124;      | Bitwise OR                             |
| ^           | Bitwise XOR                            |
| <<          | Left shift                             |
| >>          | Right shift                            |

**转换函数（Cast Functions and Operators）**

| 函数名    | 描述                             |
| --------- | -------------------------------- |
| BINARY    | Cast a string to a binary string |
| CAST()    | Cast a value as a certain type   |
| CONVERT() | Cast a value as a certain type   |



## Proxy错误码及错误信息汇总

Proxy错误码及错误信息显示如下：

	#define ER_PROXY_GRAM_ERROR_BEGIN 600
	
	#define ER_PROXY_SANITY_ERROR 601 // "Sanity error: %s"
	#define ER_PROXY_SQL_TYPE_NOT_SUPPORT 602 // sql 类型不支持
	#define ER_PROXY_SQL_NOT_SUPPORT_ORDERBY_1 603 // order by index is negative
	#define ER_PROXY_SQL_NOT_SUPPORT_ORDERBY_2 604 // order by index is too big
	#define ER_PROXY_SQL_NOT_SUPPORT_ORDERBY_3 605 // 不支持到 order by 用法
	#define ER_PROXY_SQL_NOT_SUPPORT_GROUPBY_1 606 // group by index is negative
	#define ER_PROXY_SQL_NOT_SUPPORT_GROUPBY_2 607 // group by index is too big
	#define ER_PROXY_SQL_NOT_SUPPORT_GROUPBY_3 608 // 不支持的 group by 用法
	#define ER_PROXY_GET_AUTO_ID_FAILED 609 // get auto id back with error
	#define ER_PROXY_TEANS_ROLLED_BACK 610 // 事务已经被回滚
	#define ER_PROXY_ONE_SET 611 // 当前 sql 应该被发往一个后端，但是不是
	#define ER_PROXY_CLIENT_HS_ERROR 612 // 解析客户端握手包出错
	#define ER_PROXY_ACCESS_DENIED_ERROR 613 // the length of readu_auth_switch_result is not 20，不应该出现
	#define ER_PROXY_TRANS_NOT_ALLOWED 614 // 事务中不允许执行的命令
	#define ER_PROXY_TRANS_READ_ONLY 615 // 只读事务中不允许执行的命令
	#define ER_PROXY_TRANS_ERROR_DIFFENT_SET 616 // 非 xa 事务中，只读 sql 使用了多个后端
	#define ER_PROXY_STRICT_ERROR 617 // strict 模式下，一次仅允许修改一个 set	
	#define ER_PROXY_SC_TOO_LONG 618 // 后端断开时间过长，断开链接
	#define ER_PROXY_START_TRANS_FAILED 619 // 开启新的 xa 事务失败
	#define ER_PROXY_SC_RETRY 620 // server 已经 close，请重试上一条 sql
	#define ER_PROXY_SC_TRANS_IN_ROLLBACK_ONLY 621 // server 已经 close，当前事务处于 rollback 
	#define ER_PROXY_SC_COMMIT_LATER 622 // server 已经 close，事务会在稍后提交
	#define ER_PROXY_SC_ROLLBACL_LATER 623 // server 已经 close，事务会在稍后回滚
	#define ER_PROXY_SC_IN_COMMIT_OR_ROLLBACK 624 // server 在事务提交/回滚阶段 close
	#define ER_PROXY_SC_NEED_ROLLBACK 625 // server 已经 close，需要首先会滚当前事务
	#define ER_PROXY_SC_STATE_WILL_ROLLBACK 626 // server 已经 close，将会会滚
	#define ER_PROXY_XA_UNSUPPORT 627 // xa 目前不支持的命令
	#define ER_PROXY_XA_INVALID_COMMAND 628 // xa 命令不合法
	#defien ER_PROXY_XA_GTID_INIT_ERROR 629 // gtid log 初始化失败
	#define ER_PROXY_XA_GET_SET_IP_PORT_FAILED 630 // 获取 set 地址失败
	#define ER_PROXY_XA_UPDATE_GTID_LOG_FAILED 631 // 更新 gtid log 失败
	#define ER_PROXY_MYSQL_PARSER_ERROR 632 // mysql 解析失败，返回详细错误信息
	#define ER_PROXY_MYSQL_PARSER_UNEXPECTED_ERROR 633 // mysql 解析失败，unexpected error
	#define ER_PROXY_MYSQL_PARSER_NOT_SUPPORTED 634 // mysql 不支持的命令
	#define ER_PROXY_ILLEGAL_ID 635 // kill id 不合法
	#define ER_PROXY_NOT_SUPPORT_CURSOR 636 // CURSOR_TYPE_READ_ONLY 暂不支持
	#define ER_PROXY_UNKNOWN_PREPARE_HANDLER 637 // 执行的 prepare 不明确
	#define ER_PROXY_SET_PARA_FAIL 638 // Set parameters failed
	#define ER_PROXY_SUBPARTITION_TABLE_TOO_MANY_DEAL 639 // 只能够处理一个二级分区表
	#define ER_PROXY_NS_AND_SHARD_TABLE_DENY 640 // can not deal with noshard and shard table
	#define ER_PROXY_NS_AND_GLOBAL_TABLE_DENY 641 // Can not deal with noshard and global table
	#define ER_PROXY_NO_SUBPARTITION_ROUTE 642 // 没有获取到二级分区表的路由信息
	#define ER_PROXY_LOCK_MORE_TABLE 643 // 一次只可以锁定一张二级分区表
	#define ER_PROXY_GET_ROUTER_LOCK_FAIL 644 // 获取路由锁失败
	#define ER_PROXY_PART_NAME_EMPTY 645 // part name 为空
	#define ER_PROXY_SUB_PART_TABLE_IS_NONE 646 // 没有耳机分区表
	#define ER_PROXY_ALTER_PART_TYPE_TO_RANGE 647 // "Table has list type, alter use range type"
	#define ER_PROXY_ALTER_PART_TYPE_TO_LIST 648 // "Table has range type, alter use list type"
	#define ER_PROXY_PART_NAME_ILLEGAL 649 // 分区名不合法
	#define ER_PROXY_DROP_ALL_PARTITION_FAIL 650 // 删除所有分区失败，尝试直接删除表
	#define ER_PROXY_GET_OLD_PART_NUM_FAIL 651 // 获取表的分片数失败
	#define ER_PROXY_EMPTY_SQL 652 // empty sql，不会返回给客户端
	#define ER_PROXY_ERROR_SHARDKEY 653 // sk 必须为某一列	
	#define ER_PROXY_ERROR_SUB_SHARDKEY 654 // 二级分表键失败	
	#define ER_PROXY_SQLUSE_NOT_SUPPORT 655 // proxy 不支持这种用法
	#define ER_PROXY_DBFW_WHITE_LIST_DENY 656 // 不在白名单，被防火墙拒绝
	#define ER_PROXY_DBFW_DENY 657 // 防火墙拒绝
	#define ER_PROXY_INCORRECT_ARGS 658 // stmt 参数不正确	
	#define ER_PROXY_SYSTABLE_UNSUPPORT_NON_READ_SQL 659 // 不支持非只读sql访问系统表
	#define ER_PROXY_TABLE_NOT_EXIST 660 // 表不存在	
	#define ER_PROXY_SHARD_JOIN_UNSUPPORT_TYPE 661 // shard join 暂不支持的用法
	#define ER_PROXY_RECURSIVE_JOIN_DENY 662 // 递归 join 不支持
	#define ER_PROXY_JOIN_INTERNAL_ERROR 663 // join 异常
	#define ER_PROXY_SQL_TOO_COMPLEX 664 // sql 太复杂，groupshard 暂不支持
	#define ER_PROXY_INVALID_ARG_FOR_GTID_STATE 665 // gtid_state() 参数不合法
	#define ER_PROXY_CANT_SET_GLOBAL_AUTOCOMMIT_GS 666 // Global autocommit cannot be set in groupshard
	#define ER_PROXY_INVALID_VALUE_FOR_AUTOCOMMIT 667 // autocommit 值设置不合法
	#define ER_PROXY_XID_ERROR 668 // xid 不合法
	#define ER_PROXY_XID_GENERAT_FAILED 669 // xid 不能由用户指定	
	#define ER_PROXY_CANT_EXEC_IN_INTER_TRANS 670 // "The command cannot be executed in internal transction"
	#define ER_PROXY_XID_TIME_ERROR 671 // "Unexpected time part of xid"
	#define ER_PROXY_XID_TIMEDIFF_TOO_LONG 672 // "timediff > 1800s, it's not safe to execute boost"
	#define ER_PROXY_SAVEPOINT_NOT_EXIST 673 // SAVEPOINT 不存在
	#define ER_PROXY_SC_TRANS_IN_ROLLED 674 // 事务已经会滚，由于 serevr 已经 close
	#define ER_PROXY_CANT_BOOST_IN_TRANS 675 // 事务中不允许执行 SQLCOM_BOOST
	#define ER_PROXY_TRANS_EXPECTED 676 // "A transaction is expected, this maybe a bug"
	#define ER_PROXY_EXTERNAL_TRANS 677 // 外部 xa 中不允许执行
	#define ER_PROXY_AUTO_INC_FAIL 678 // "Deal auto inc failed"
	#define ER_PROXY_CHECK_JOIN_FAIL 679 // "Check join failed"
	#define ER_PROXY_TABLE_TYPE_NOT_MATCH 680 // "Do not support shard-table operations in noshard instance"
	#define ER_PROXY_UNSUPPORT_NS_IN_INSERT 681 // "Do not support noshard and noshard_allset in insert sql"
	#define ER_PROXY_ALTER_SEQ_ID_FAIL 682 // Alter seq id failed
	#define ER_PROXY_ALTER_ID_ILLEGAL 683 // Alter seq id is illegal	
	#define ER_PROXY_CANT_CHANGE_STEP 684 // "Current table use zk to get auto inc, do not support to change step: \'%s\'"
	#define ER_PROXY_ALTER_STEP_FAIL 685 // Alter step failed	
	#define ER_PROXY_TOO_MUCH_TABLES 686 // "Too much tables, exceed the maximum value"
	#define ER_PROXY_TABLE_EXISTED 687 // 表已经存在
	#define ER_PROXY_CREATE_STABLE_FAILED 688 // "Complex sql can not used to create shard tables"
	#define ER_PROXY_DDL_DENY 689 // "DDL can not handle noshard and global table"
	#define ER_PROXY_SHADKEY_ERROR 690 // "SQL should not relate to subpartition tables"
	#define ER_PROXY_NO_SK 691 // reject nosk
	#define ER_PROXY_COMBINE_SQL_KEY 692 // "Something went wrong:%s"
	#define ER_PROXY_GET_SK_ERROR 693 // sk 获取失败
	#define ER_PROXY_SHOW_FAILED 684 // "%s, see /*proxy*/ help"
	#define ER_PROXY_SET_FAILED 695 // "%s, see /*proxy*/ help"
	#define ER_PROXY_UNLOCK_FORMAT_ERROR 696 // sql 格式不正确
	#define ER_PROXY_UNLOCK_ROUTER_FAIL 697 // "Unlock failed"
	#define ER_PROXY_LOCK_ROUTER_FAIL 698 // "Lock failed"
	#define ER_PROXY_PROXY_CMD_FAIL 699 // 不支持的/*proxy*/ 命令
	#define ER_PROXY_PROCESS_RULE_FILE_FAILED 700 // dump_error
	#define ER_PROXY_GET_AUTO_NUM_ERROR 701 // "Get auto num failed"
	#define ER_PROXY_SEQUENCE_NOT_EXIST 702 // sequence 不存在
	#define ER_PROXY_SEQUENCE_ERROR 703 // sequence 不合法
	#define ER_PROXY_SEQUENCE_ALREADY_EXIST 704 // Sequence 已经存在
	
	#define ER_PROXY_GRAM_ERROR_END 705
	#define ER_PROXY_SYSTEM_ERROR_BEGIN 900 
	
	#define ER_PROXY_SLICING 901 // slice 被修改，可能在扩容阶段，拒掉当前 sql
	#define ER_PROXY_NO_DEFAULT_SET 902 // set 为空
	#define ER_PROXY_GET_ADDRESS_FAILED 903 // 还未初始化完成，获取后端地址失败，稍后重试
	#define ER_PROXY_SQL_SIZE_ERROR_IN_GET_CANDIDATE_ADDRESS 904 // 获取后端地址出错（发往后端个数不正确）
	#define ER_PROXY_GET_ADDRESS_ERROR 905 // 获取后端地址出错
	#define ER_PROXY_CANDIDATE_ADDRESS_EMPTY 906 // 未获取到后端地址
	#define ER_PROXY_SOCK_ERROR 907 // 当前 sql 不允许发送到后端	
	#define ER_PROXY_CANT_GET_SOCK 908 // socket 获取失败	
	#define ER_PROXY_GET_SET_SOCK_FAIL 909 // socket 获取失败
	#define ER_PROXY_CONNECT_ERROR 910 // 后端连接失败
	#define ER_PROXY_NO_SQL_ASSIGN_TO_SET 911 // an unbelievable error
	#define ER_PROXY_STATUS_ERROR 912 // group 状态异常，断开链接
	#define ER_PROXY_CONN_BROKEN_ERROR 913 // server close，sql 状态不正常
	#define ER_PROXY_UNKNOWN_ERROR 914 // proxy 未知错误（可能为异常引起）
	#define ER_PROXY_SQL_RETRY 915 // sql 还未提交或回顾	
	#define ER_PROXY_XA2PC_ABORT 916 // 2pc 失败，事务将会会滚:
	#define ER_PROXY_XA2PC_COMMIT 917 // 2pc 失败，后续提交
	#define ER_PROXY_XA2PC_UNCERTAIN 918 // 2pc 失败，结果未知
	#define ER_PROXY_ERROR_END 919

**注意**：其中错误码为900以上的为系统错误，将会通过监控平台进行告警。

