## Creating Table
To create a table, you need to use the `CREATE TABLE` command and specify at lease one name, column name, and data type for the new table in the command as follows:
```
CREATE TABLE datatypetest (
  col1 integer,
  col2 character varying(20),
  col3 date,
  col4 jsonb,
  col5 smallint
) WITH (orientation='row');
```

### Specifying table storage method
A table supports row/column storage.
`ROW` (row storage) is suitable for OLTP businesses, where row storage-based query is more efficient as tables have many interactive transactions, and one interaction involves multiple columns in a table.
`COLUMN` (column storage) indicates that the table data is stored by column. It is suitable for data warehousing businesses, where high numbers of aggregate computations are performed on tables and few column operations are involved.

#### Creating row storage table
```
CREATE TABLE coltest1 (
  id integer NOT NULL,
   name character(16) NOT NULL,
  start_date date,
  subject character(1)
) WITH (orientation = 'row');
```

#### Creating column storage table
```
CREATE TABLE coltest1 (
  id integer NOT NULL,
  name character(16) NOT NULL,
  start_date date,
  subject character(1)
) WITH (orientation = 'column');
```


### Creating table with its resource group specified
```
CREATE TABLE t3(id integer,nc text) with (orientation ='column') DISTRIBUTE BY shard (id) TO GROUP default_group;
```

#### Creating table with its schema specified
```
CREATE SCHEMA myschema;
CREATE TABLE myschema.t4(
  col1 integer,
  col2 char,
  col3 bigint,
  clo4 varchar(10)
) WITH (orientation ='column');
```

### Creating table with the compression method and level of its column fields specified
Currently, supported compression methods (`compress_method`) include delta, zstd, zlib, RLE, and bitpack. `compress_level` indicates the compression level. The higher the level, the higher the compression ratio, the longer the compression time, and the more the CPU usage.

Lightweight compression algorithms are implemented based on proprietary algorithms, including RLE, delta, and bitpack, which all have only one compression level and can compress only the numeric type.
- RLE mainly compresses a large amount of repeated data such as `11111122222333111111`.
- Delta mainly compresses ascending or descending data such as fixed time type (today, tomorrow, the day after tomorrow) or numeric type such as `12345678`.
- Bitpack compresses small numeric data, such as integers ranging from 1 to 100 in a table.

The compression method is specified during table creation, but it will be automatically and adaptively adjusted in actual storage. In scenarios with writes, the final storage may not use compression at all, because the specified compression method is inappropriate; for example, delta is specified for data of `text` type.

The original table is 15 GB in size:
```
CREATE TABLE coltest2 (
c1 int encoding(compress_method='delta'), 
c2 char(30), 
c3 float4 ENCODING(compress_method='zstd', compress_level=19), 
c4 date encoding(compress_method='zlib', compress_level=9),
c5 int encoding(compress_method='rle'),
c6 int encoding(compress_method='bitpack')
) WITH (orientation = 'column');
```
Description:
- Delta compression: there is no limit on the compression level, and the data after compression will be about 14 GB in size.
- zlib compression: there are compression levels 1–9, and the data after compression will be 4,234 MB in size at level 9.
- zstd compression: there are compression levels 1–19, and the data after compression will be 3,691 MB in size at level 19.
- RLE compression: there is no compression level, and the data after compression will be about 14 GB in size.
- Bitpack compression: there is no compression level, and the data after compression will be about 14 GB in size.

### Table distribution methods
Table replication: each table row is stored on all DNs, that is, each DN has the complete table data. 
```
CREATE TABLE t_rep (id int,mc text) DISTRIBUTE BY REPLICATION TO GROUP default_group;
INSERT INTO t_rep(id,mc) VALUES 
(1,'ReplicationTableTest1'),(2,'ReplicationTableTest2'),(3,'ReplicationTableTest3');
```

Table sharding: the specified column is sharded for data distribution onto specified DNs. If the shardkey is not specified during table creation, the primary key will be used as the shardkey by default. If there is no primary key, the system will use the first field as the table shardkey by default.
```
CREATE TABLE t_shard(
  f1 bigserial not null,
  f2 integer,
  f3 text,
  f4 text, 
f5 date) WITH (orientation = 'column') 
DISTRIBUTE BY SHARD(f1) TO GROUP default_group;
```


### Inheriting table
#### Inheriting single table
```
CREATE TABLE cities(
  name      text,
  population   float,
  altitude    int
) WITH (orientation ='column');
CREATE TABLE capitals(
  state char(2)
) INHERITS (cities) WITH (orientation = 'column');
```

#### Inserting data
```
INSERT INTO cities VALUES('Las Vegas', 1.53, 2174);
INSERT INTO cities VALUES('Mariposa',3.30,1953);
INSERT INTO capitals VALUES('Madison',4.34,845,'WI');
```

#### Querying
```
SELECT name, altitude FROM cities WHERE altitude > 500;
SELECT name, altitude FROM capitals WHERE altitude > 500;
SELECT name,altitude FROM ONLY cities WHERE altitude > 500;
SELECT * FROM capitals;
```

### Inheriting multiple tables
```
CREATE TABLE parent1 (FirstCol integer) WITH (orientation = 'column');
 CREATE TABLE parent2 (FirstCol integer, SecondCol varchar(20)) WITH (orientation = 'column');
 CREATE TABLE parent3 (FirstCol varchar(200)) WITH (orientation = 'column');
 -- The `child1` child table will inherit data from both the `parent1` and `parent2` parent tables, both of which contain the `FirstCol` field of the `integer` type; therefore, `child1` can be successfully created.
 CREATE TABLE child1 (MyCol timestamp) INHERITS (parent1,parent2) WITH (orientation = 'column');
 -- The `child2` child table cannot be created, as although both the parent tables contain the `FirstCol` field, they are of different types.
 CREATE TABLE child2 (MyCol timestamp) INHERITS (parent1,parent3) WITH (orientation = 'column');
 -- The `child3` child table cannot be created either, as although both its parent table and it contain the `FirstCol` field, they are of different types.
 CREATE TABLE child3 (FirstCol varchar(20)) INHERITS(parent1) WITH (orientation = 'column');
```

### Using `IF NOT EXISTS`
If a table with the same name already exists, no error will be thrown; instead, a message will be displayed to indicate the existing table relationship.
```
postgres=# CREATE TABLE t(id int,mc text);       
CREATE TABLE
postgres=# CREATE TABLE t(id int,mc text);
ERROR: relation "t" already exists
postgres=# CREATE TABLE IF NOT EXISTS t(id int,mc text);
NOTICE: relation "t" already exists, skipping
CREATE TABLE
postgres=# 
```

#### Creating table with its schema specified
```
postgres=# CREATE TABLE public.t1(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE 
```

#### Creating table by using query result
```
postgres=# CREATE TABLE t(id int,mc text) DISTRIBUTE BY shard(mc);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t VALUES(1,'tdapg');
INSERT 0 1
postgres=# CREATE TABLE t_as as SELECT * FROM t;
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
INSERT 0 1
postgres=# SELECT * FROM t_as;
 id | mc  
----+-------
 1 | tdapg
(1 row)

postgres=# \d+ t
                   Table "tdapg.t"
 Column | Type  | Collation | Nullable | Default | Storage | Stats target | Description 
--------+---------+-----------+----------+---------+----------+--------------+-------------
 id   | integer |      |     |     | plain  |       | 
 mc   | text  |      |     |     | extended |       | 
DISTRIBUTE BY: SHARD(mc)
Location Nodes: ALL DATANODES

postgres=# \d+ t_as

                   Table "tdapg.t_as"
 Column | Type  | Collation | Nullable | Default | Storage | Stats target | Description 
--------+---------+-----------+----------+---------+----------+--------------+-------------
 id   | integer |      |      |     | plain  |       | 
 mc   | text  |      |     |     | extended |       | 
Distribute By: SHARD(id)
Location Nodes: ALL DATANODES
```

## Altering Table
#### Creating table
```
CREATE TABLE t(
  col1 bigint,
  col2 char,
  col3 text,
  col4 varchar(5)
) WITH(ORIENTATION=column);

```

#### Adding column
```
ALTER TABLE t ADD column_name varchar(20);
```

#### Dropping column
```
ALTER TABLE t DROP column_name;
```

#### Renaming column
```
ALTER TABLE t RENAME col2 TO col5;
```

#### Modifying default column value
```
ALTER TABLE t ALTER col3 SET DEFAULT 'test';
```

#### Renaming table
```
ALTER TABLE t RENAME TO t1;
```

#### Changing the data type of column field
```
ALTER TABLE t1 ALTER COLUMN col5 type TEXT;
```
In column storage mode, the column field data type cannot be changed currently.

#### Adding primary key
```
ALTER TABLE t1 ADD CONSTRAINT t_id_pkey PRIMARY KEY (col1) ;
```

#### Adding unique constraint
```
ALTER TABLE t1 ADD CONSTRAINT unique_t1_clo1 UNIQUE(col1);
```

#### Adding check constraint
```
ALTER TABLE t1 ADD CONSTRAINT t1_CONSTR_clo3 CHECK (col3 IS NOT NULL);
```


#### Creating foreign key
```
postgres=# CREATE TABLE t_p(f1 int not null,f2 int ,primary key(f1));
CREATE TABLE t_f(f1 int not null,f2 int );NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# CREATE TABLE t_f(f1 int not null,f2 int );
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# ALTER TABLE t_f ADD CONSTRAINT t_f_f1_fkey FOREIGN KEY (f1) REFERENCES t_p (f1);
ALTER TABLE
```
Currently, you cannot create foreign keys for columnar tables.

#### Dropping foreign key
```
ALTER TABLE t_f DROP CONSTRAINT t_f_f1_fkey; 
```
A foreign key takes effect only within the same node. Therefore, the foreign key field and the corresponding primary key field must both be the table shardkey; otherwise, update will fail as data is distributed on different nodes.

## Dropping Table
#### Dropping table in current schema
```
CREATE TABLE t(
  col1 bigint
);

postgres=# DROP TABLE t;
DROP TABLE
```

#### Dropping table in specified schema
```
postgres=# DROP TABLE public.t;
DROP TABLE
```

#### Dropping table (if the table does not exist, this command will not be executed, and no errors will be reported)
```
postgres=# DROP TABLE IF EXISTS t;  
NOTICE: table "t" does not exist, skipping
DROP TABLE
```

#### Using `CASCADE` to drop table unconditionally
```
postgres=# CREATE SCHEMA if not exists tdapg_schema;
CREATE SCHEMA
postgres=# CREATE TABLE tdapg_schema.t1( col1 bigint);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# CREATE VIEW tdapg_schema.t1_view AS SELECT * FROM tdapg_schema.t1 ;
CREATE VIEW
postgres=# DROP TABLE tdapg_schema.t1 ;
ERROR: cannot DROP TABLE tdapg_schema.t1 because other objects depend on it
DETAIL: view tdapg_schema.t1_view depends on table tdapg_schema.t1
HINT: Use DROP ... CASCADE to drop the dependent objects too.

postgres=# DROP TABLE tdapg_schema.t1 CASCADE;
NOTICE: drop cascades to view tdapg_schema.t1_view
DROP TABLE
```

## Inserting Data
#### Inserting single data record
```
postgres=# DROP TABLE IF EXISTS t6;
DROP TABLE
postgres=# CREATE TABLE t6(id int,mc text) WITH (ORIENTATION='column');
CREATE TABLE
postgres=# INSERT INTO t6 VALUES(1,'tdapg01');
INSERT 0 1
```

#### Batch inserting data
```
postgres=# INSERT INTO t6 VALUES(1,'tdapg01'),(1,'tdapg02');
COPY 2
```

#### Returned value for insertion
```
postgres=# INSERT INTO t6 VALUES(1,'tdapg03') RETURNING id ;
 id 
----
 1
(1 row)

INSERT 0 1
```

## Updating Data
#### Updating
```
postgres=# DROP TABLE IF EXISTS t1;
DROP TABLE
postgres=# CREATE TABLE t1(name text, price integer, id serial) WITH (ORIENTATION ='column');
CREATE TABLE
postgres=# INSERT INTO t1(name, price) VALUES ('potato',4),('tomato',5),('chicken',20),('beef',50);
COPY 4
postgres=# UPDATE t1 SET price = price * 1.10 WHERE price <= 99.99;
UPDATE 4
```

#### Returned value for update
```
postgres=# DROP TABLE IF EXISTS t1;
DROP TABLE
postgres=# CREATE TABLE t1(name text, price integer, id serial) WITH (ORIENTATION ='column');
CREATE TABLE
postgres=# insert into t1(name, price) values ('potato',4),('tomato',5),('chicken',20),('beef',50);
COPY 4
postgres=# UPDATE t1 SET price = price * 1.10 WHERE price <= 99.99 RETURNING name, price AS new_price;
 name  | new_price 
---------+-----------
 potato |     4
 tomato |     6
 beef  |    55
 chicken |    22
(4 rows)

UPDATE 4
```

## Deleting Data
Delete data:
```
postgres=# DROP TABLE IF EXISTS t1;
DROP TABLE
CREATE TABLE t1(
  id integer,
  nickname text
) WITH (ORIENTATION ='column');
INSERT INTO t1(id,nickname) 
VALUES(1,'tdapgCTest1'),(2,'tdapgCTest2'),(3,'tdapgCTest3'),(33,'tdapgCTest3');
postgres=# DELETE FROM t1 WHERE id=1;
DELETE 1
```

## Truncating Data
The `TRUNCATE` operation is used to quickly delete table data. `TRUNCATE` is at the DDL level and will add the highest-level (`ACCESS EXCLUSIVE`) lock to the table to be truncated.

### Truncating regular table
```
postgres=# TRUNCATE TABLE t1;
TRUNCATE TABLE
\# Multiple tables can be truncated at a time
postgres=# TRUNCATE TABLE t1,t6;
TRUNCATE TABLE
postgres=# 
```

### Truncating partitioned table
Truncate a table partitioned by time:
```
CREATE TABLE t_time_range(
 f1 bigint, 
f2 timestamp,f3 varchar(20))
PARTITION BY range (f2) begin (timestamp without time zone '2017-09-01 0:0:0') 
step (interval '1 month') 
PARTITIONS (12)
 WITH (orientation = 'column') ;
postgres=# INSERT INTO t_time_range VALUES(1,'2017-09-01','tdapg');
INSERT 0 1
postgres=# INSERT INTO t_time_range VALUES(2,'2017-10-01','pgxz');
INSERT 0 1
postgres=# \d+ t_time_range
                           Column oriented table "public.t_time_range"
 Column |      Type       | TC method | TC level | LWC method | Collation | Nullable | Default | Storage | Stats target | Description 
--------+-----------------------------+-------------+----------+-------------+-----------+----------+---------+----------+--------------+-------------
 f1   | bigint           | no compress |     | no compress |      |     |     | plain  |       | 
 f2   | timestamp without time zone | no compress |     | no compress |      |     |     | plain  |       | 
 f3   | character varying(20)    | no compress |     | no compress |      |     |     | extended |       | 
Distribute By: SHARD(f1)
Location Nodes: ALL DATANODES
PARTITION BY: RANGE(f2)
     \# Of Partitions: 12
     Start With: 2017-09-01
     Interval Of Partition: 1 MONTH
Options: orientation=column

postgres=# SELECT * FROM t_time_range;
 f1 |     f2     | f3  
----+---------------------+-------
 1 | 2017-09-01 00:00:00 | tdapg
 2 | 2017-10-01 00:00:00 | pgxz
(2 rows)

postgres=# TRUNCATE t_time_range partition for ('2017-09-01' ::timestamp without time zone);
TRUNCATE TABLE
postgres=# SELECT * FROM t_time_range;
 f1 |     f2     | f3 
----+---------------------+------
 2 | 2017-10-01 00:00:00 | pgxz
(1 row)
```

Truncate a table partitioned by numeric range:
```
CREATE TABLE t_range(
   f1 bigint,
   f2 timestamp default now(),
   f3 integer
 ) PARTITION BY range (f3) begin (1) step (50) partitions (3) WITH (orientation = 'column') DISTRIBUTE BY shard(f1) TO GROUP default_group;
INSERT INTO t_range(f1,f3) VALUES (1,1);
 INSERT INTO t_range(f1,f3) VALUES(2,50);
 INSERT INTO t_range(f1,f3) VALUES(2,110);
 INSERT INTO t_range(f1,f3) VALUES(3,100);

postgres=# \d+ t_range
                            Column oriented table "public.t_range"
 Column |      Type       | TC method | TC level | LWC method | Collation | Nullable | Default | Storage | Stats target | Description 
--------+-----------------------------+-------------+----------+-------------+-----------+----------+---------+---------+--------------+-------------
 f1   | bigint           | no compress |     | no compress |      |     |     | plain  |       | 
 f2   | timestamp without time zone | no compress |     | no compress |      |     | now()  | plain  |       | 
 f3   | integer           | no compress |     | no compress |      |     |     | plain  |       | 
Distribute By: SHARD(f1)
Location Nodes: ALL DATANODES
PARTITION BY: RANGE(f3)
     \# Of Partitions: 3
     Start With: 1
     Interval Of Partition: 50
Options: orientation=column

postgres=# SELECT * FROM t_range ;
 f1 |       f2       | f3 
----+----------------------------+-----
 3 | 2021-01-19 19:47:31.060817 | 100
 1 | 2021-01-19 19:47:30.258023 |  1
 2 | 2021-01-19 19:47:30.37273 | 50
 2 | 2021-01-19 19:47:30.387583 | 110
(4 rows)

postgres=# TRUNCATE t_range partition for (1);  
TRUNCATE TABLE
postgres=# SELECT * FROM t_range ;
 f1 |       f2       | f3 
----+----------------------------+-----
 3 | 2021-01-19 19:47:31.060817 | 100
 2 | 2021-01-19 19:47:30.387583 | 110
(2 rows)
postgres=#
```

## Reclaiming Space
In database operations, the deleted rows are not physically deleted and still exist before they are vacuumed. If you update or delete a large number of rows in a table, many disk page fragments will be generated, which compromises the query efficiency. In this case, you should run the `VACUUM FULL` command to vacuum the garbage data and reclaim the space.

Sample code:
After creating a table and importing data into it, delete all data in it. At this point, the table size does not change, and the garbage data is only logically deleted:
```
postgres=# CREATE TABLE vacuum_test(a INT,b VARCHAR) WITH(ORIENTATION=column);
CREATE TABLE
postgres=# INSERT INTO vacuum_test VALUES(generate_series(1,10000),'hello world');
INSERT 0 10000
postgres=# DELETE FROM vacuum_test;
DELETE 10000
postgres=# \dt+ vacuum_test
               List of relations
 Schema |  Name   | Type | Owner | Size | Allocated Size | Description 
--------+-------------+-------+-------+--------+----------------+-------------
 public | vacuum_test | table | dbadmin | 144 MB | 144 MB     | 
(1 row)
```

You need to connect to all related DNs to vacuum the columnar table:
```
postgres=# EXECUTE DIRECT ON(dn001) 'VACUUM FULL vacuum_test;';
EXECUTE DIRECT
postgres=# EXECUTE DIRECT ON(dn002) 'VACUUM FULL vacuum_test;';
EXECUTE DIRECT
postgres=# EXECUTE DIRECT ON(dn003) 'VACUUM FULL vacuum_test;';
EXECUTE DIRECT
postgres=# EXECUTE DIRECT ON(dn004) 'VACUUM FULL vacuum_test;';
EXECUTE DIRECT
postgres=# EXECUTE DIRECT ON(dn005) 'VACUUM FULL vacuum_test;';
EXECUTE DIRECT
postgres=# EXECUTE DIRECT ON(dn006) 'VACUUM FULL vacuum_test;';
EXECUTE DIRECT
postgres=# \dt+ vacuum_test
                List of relations
 Schema |  Name   | Type | Owner | Size  | Allocated Size | Description 
--------+-------------+-------+-------+---------+----------------+-------------
 public | vacuum_test | table | dbadmin | 0 bytes | 0 bytes    | 
(1 row)
```
After the `VACUUM FULL` operation, all garbage data in the table is vacuumed, and the space is reclaimed.
In addition to manual execution of `VACUUM`, the `autovacuum` process of the system can automatically run the `VACUUM` command to reclaim record space marked as deleted.
