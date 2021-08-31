
## Naming Conventions
- Names of database objects such as database, schema, table, column, view, index, sequence, function, and trigger:
 - We recommend you use combinations of lowercase letters, digits, and underscores (_).
 - We recommend you not enclose a name with double quotation marks ("), unless the name must contain uppercase letters or special symbols such as space.
 - The name cannot contain more than 63 characters.
 - We recommend you not start a name with `pg_` or `pgxc_` (so as to avoid confusion with database system objects) or a digit.
 - Do not use SQL keywords such as `type` and `order`.
- A table can contain 250–1,600 columns subject to the field type.
- We recommend you add a date to the name of a temporary or backup database object such as table and view; for example, `dbaa_ops.b2c_product_summay_2014_07_12` (`dba_ops` is the dedicated schema of the DBA).
- Index naming conventions: the name of a regular index should be `table name_column name_idx`, and that of a unique index should be `table name_column name_uidx`, for example, `student_name_idx,student_id_uidx`.

## Column Design
- We recommend you use numeric types instead of character types.
- We recommend you use `varchar(N)` instead of `char(N)` to save the storage space.
- We recommend you use `varchar(N)` instead of `text` or `varchar`.
- We recommend you use `default NULL` instead of `default ''` to save the storage space.
- We recommend you use `timestamp with time zone(timestamptz)` instead of `timestamp without time zone` for global businesses so as to avoid different returned values of time points in different timezones and facilitate business globalization.
- We recommend you use `NUMERIC(precision, scale)` instead of `real` or `double precision` to store currency amounts and other values requiring precise calculation.

## Constraint Design
- We recommend you use the shardkey as the primary key or unique index for each table. The primary key or unique index must carry the shardkey.
- We recommend you set the primary key or unique index when creating a table.
- Currently, columnar tables don't support foreign keys.

## Index Design
- TDSQL-A for PostgreSQL provides the following index types: B-tree, Hash, Generalized Search Tree (GiST), space-partitioned GiST (SP-GiST), Generalized Inverted Index (GIN), and Block Range Index (BRIN). Currently, Hash is not recommended, and B-tree should be used generally. Columnar tables currently support only B-tree and Hash indexes.
- We recommend you add the `CONCURRENTLY` parameter when using `create` or `drop index` so as to achieve concurrency with data write.
- For tables where columns contained in the index definition are frequently updated or deleted, we recommend you use `create index CONCURRENTLY` and `drop index CONCURRENTLY` to maintain the corresponding index.
- We recommend you use the unique index to replace the unique constraints so as to facilitate subsequent maintenance.
- We recommend you create a composite index containing multiple fields based on data distribution for frequent queries with a WHERE clause containing multiple fields concatenated with AND.
- We recommend you use partial indexes with a WHERE clause for queries with fixed conditions (which are business-specific generally) and a small portion of data.
```
   select * from test where status=1 and col=?; -- `status=1` is a fixed condition
   create index on test (col) where status=1;
```
- We recommend you use indexes on expressions or functions to accelerate queries that frequently use expressions as query conditions.
```
   select * from test where exp(xxx);
   create index on test ( exp(xxx) );     
```
- We recommend you not create too many indexes. Generally, do not create more than six indexes. For core tables (such as product and order tables), you can add more indexes accordingly.

## Notes on NULL
- NULL judgment: `IS NULL` and `IS NOT NULL`. 
- Note that the valid values of the `boolean` data type are `true`, `false`, and `NULL`.
- Pay special attention to queries where the `NOT IN` collection contains `NULL` elements:

```
postgres=# select * from tdapg;
 id |   nickname    
----+-------------------------------
  1 | hello TDSQL-A for PostgreSQL
  2 | TDSQL-A for PostgreSQL good
  3 | TDSQL-A for PostgreSQL good
  4 | TDSQL-A for PostgreSQL default
(4 rows)

postgres=# select * from tdapg where id not in (null);
 id | nickname 
----+----------
(0 rows)
```
- We recommend you perform the "||" operation after processing the `NULL` value of the string data type.

```
postgres=# select id,nickname from tdapg limit 1;
 id |  nickname   
----+-----------------------------
  1 | hello TDSQL-A for PostgreSQL
(1 row) 

postgres=# select id,nickname||null from tdapg limit 1;
 id | ?column? 
----+----------
  1 | 
(1 row) 

postgres=# select id,nickname||coalesce(null,'') from tdapg limit 1;
 id |  ?column?   
----+-----------------------------
  1 | hello TDSQL-A for PostgreSQL
(1 row)
```
- We recommend you use `count(1)` or `count(\*)` to count the number of rows. `count(col)` is not recommended, as `NULL` values will not be included.
>!When you use `count(multiple column names)`, you must enclose the multiple column names with parentheses; for example, `count( (col1,col2,col3) )`. Note that even all columns are `NULL` in multi-column `count` operations, they are still counted, so the effect is the same as that of `count(\*)`.

```
postgres=# select * from tdapg ;
 id |   nickname    
----+-------------------------------
  1 | hello TDSQL-A for PostgreSQL
  2 | TDSQL-A for PostgreSQL good
  5 | 
  3 | TDSQL-A for PostgreSQL good
  4 | TDSQL-A for PostgreSQL default
(5 rows)

postgres=# select count(1) from tdapg;
 count 
\-------
     5
(1 row) 

postgres=# select count(*) from tdapg; 
 count 
\-------
     5
(1 row)     

postgres=# select count(nickname) from tdapg;        
 count 
\-------
     4
(1 row)

postgres=# select count((id,nickname)) from tdapg;   
 count 
\-------
     5
(1 row)
```
- If you use `count(distinct col)` to count non-NULL unique values in a column, `NULL` values will not be counted.
>!If you use `count(distinct (col1,col2,...) )` to count unique values in multiple columns, `NULL` values will be counted, and multiple `NULL` values will be considered as the same value.

```
postgres=# select count(distinct nickname) from tdapg;             
 count 
\-------
     3
(1 row)

postgres=# select count(distinct (id,nickname)) from tdapg; 
 count 
\-------
     5
(1 row)
```
- Comparison between two `NULL` values:

```
postgres=# select null is not  distinct from null as Tdapgnull;      
 Tdapgnull 
\-----------
 t
(1 row)
```


## Development Specifications
1) We recommend you comment database objects, especially columns, to make it easier for other engineers to understand and maintain the business.
Comparison of table readability before and after commenting:

```
postgres=# \d+ TDAPG_main
                      Table "public.tdapg_main"
 Column |  Type   | Modifiers | Storage  | Stats target | Description 
--------+---------+-----------+----------+--------------+-------------
 id     | integer |           | plain    |              | 
 mc     | text    |           | extended |              | 
Indexes:
    "TDAPG_main_id_uidx" UNIQUE, btree (id)
Has OIDs: no
Distribute By SHARD(id)
        Location Nodes: ALL DATANODES

postgres=# comment on column TDAPG_main.id is 'ID';
COMMENT
postgres=# comment on column TDAPG_main.mc is 'product name';
COMMENT
postgres=# \d+ TDAPG_main
                      Table "public.tdapg_main"
 Column |  Type   | Modifiers | Storage  | Stats target | Description 
--------+---------+-----------+----------+--------------+-------------
 id     | integer |           | plain    |              | ID
 mc     | text    |           | extended |              | Product name
Indexes:
    "TDAPG_main_id_uidx" UNIQUE, btree (id)
Has OIDs: no
Distribute By SHARD(id)
        Location Nodes: ALL DATANODES
```

2) We recommend you avoid `select \*` unless necessary and take only the required fields so as to reduce the consumption of network bandwidth and other resources.

```
postgres=#  explain (verbose) select * from tdapg_main where id=1;
                                         QUERY PLAN                                          
\---------------------------------------------------------------------------------------------
 Index Scan using Tdapg_main_id_uidx on public.tdapg_main  (cost=0.15..8.17 rows=1 width=36)
   Output: id, mc
   Index Cond: (Tdapg_main.id = 1)
(3 rows) 

postgres=#  explain (verbose) select tableoid from tdapg_main where id=1;   
                                         QUERY PLAN                                         
\--------------------------------------------------------------------------------------------
 Index Scan using Tdapg_main_id_uidx on public.tdapg_main  (cost=0.15..8.17 rows=1 width=4)
   Output: tableoid
   Index Cond: (Tdapg_main.id = 1)
(3 rows)
```

\* returns 36 bytes per record, while the other query returns 4 bytes per record.

3) We recommend you perform `<>` operations in updates; for example, `update table_a set column_b = c where column_b <> c`.

```
postgres=# update tdapg_main set mc='TDSQL-A for PostgreSQL' ;         
UPDATE 1
postgres=# select xmin,* from tdapg_main;
 xmin | id |  mc   
------+----+-----------------------
 2562 |  1 | TDSQL-A for PostgreSQL
(1 row) 

postgres=# update tdapg_main set mc='TDSQL-A for PostgreSQL' ;
UPDATE 1
postgres=# select xmin,* from tdapg_main;    
 xmin | id |  mc   
------+----+-----------------------
 2564 |  1 | TDSQL-A for PostgreSQL
(1 row)

postgres=# update tdapg_main set mc='TDSQL-A for PostgreSQL' where mc!='TDSQL-A for PostgreSQL';
UPDATE 0
postgres=# select xmin,* from tdapg_main;                     
 xmin | id |  mc   
------+----+-----------------------
 2564 |  1 | TDSQL-A for PostgreSQL
(1 row)
```
The effects of the above queries are the same, but the conditional update will not generate a new version record and does not require the system to vacuum the trash can.

4) We recommend you split multiple SQL operations in a single transaction or put them in different transactions so as to make the granularity of each transaction as fine as possible and lock as few resources as possible to avoid locks and dead locks.

\#session1 updates all data records without committing them, so 20 million records are locked at a time.
```
postgres=# begin;
BEGIN
postgres=# update tdapg_main set mc='TDAPG_1.3';
UPDATE 20000000
```
\#session2 waits.
```
postgres=# update tdapg_main set mc='TDAPG_1.4'  where id=1;
```
\#session3 waits.
```
postgres=# update tdapg_main set mc='TDAPG_1.5'  where id=2;
```
If #session1 is updated in batches as follows:
```
postgres=# begin;
BEGIN
postgres=# update tdapg_main set mc='TDAPG_1.3' where id>0 and id <=100000;
UPDATE 100000
postgres=#COMMIT; 

postgres=# begin;
BEGIN
postgres=# update tdapg_main set mc='TDAPG_1.3' where id>100000 and id <=200000;
UPDATE 100000
postgres=#COMMIT;
```
Then, part of the work in #session2 and #session3 can be completed in advance to avoid the large number of lock waits and system resource usage by many generated sessions. Therefore, please use this method for full-table update.

5) If you need to write a large amount of data to the database, we recommend you use `copy` instead of `insert` so as to improve the write speed as follows (the performance of `copy` is 5 times higher than that of `insert`):

```
postgres=# insert into tdapg_main select t,'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' from generate_series(1,100000) as t;
INSERT 0 100000
Time: 9511.755 ms

postgres=# copy  TDAPG_main to '/data/pgxz/TDAPG_main.txt';      
COPY 100002
Time: 179.428 ms

postgres=# copy  TDAPG_main from  '/data/pgxz/TDAPG_main.txt';
COPY 100002
Time: 1625.803 ms
postgres=# 
```


6) For reports or queries generating basic data, we recommend you use materialized views to fix data snapshots periodically so as to avoid repeated queries on multiple tables (especially tables with frequent reads/writes). In addition, materialized views support `REFRESH MATERIALIZED VIEW CONCURRENTLY` and concurrent update.
If a program needs to constantly query the total number of records in `TDAPG_main`, you can use the following code:
```
postgres=# select count(1) from tdapg_main;
 count  
\--------
 200004
(1 row)

Time: 27.948 ms

postgres=# create MATERIALIZED VIEW TDAPG_main_count as select count(1) as num from tdapg_main;
SELECT 1
Time: 322.372 ms
postgres=# select num from  TDAPG_main_count ;
  num   
\--------
 200004
(1 row)

Time: 0.421 ms
```
The performance is improved by 100 times.


Recommended update method in case of data changes:
```
postgres=#  copy  tdapg_main from  '/data/pgxz/TDAPG_main.txt';
COPY 100002
Time: 1201.774 ms
postgres=# select count(1) from tdapg_main;
 count  
\--------
 300006
(1 row)

Time: 23.164 ms
postgres=# REFRESH MATERIALIZED VIEW TDAPG_main_count;         
REFRESH MATERIALIZED VIEW
Time: 49.486 ms
postgres=# select num from tdapg_main_count ;
  num   
\--------
 300006
(1 row)

Time: 0.301 ms
```

7) We recommend you use window functions for complex statistical queries. 

8) Use the shardkey as much as possible when joining two tables.
When creating the primary and details table of a business, you need to use their foreign keys as the shardkeys as follows:
```
[pgxz@VM_0_29_centos pgxz]$ psql -p 15001              
psql (PostgreSQL 10 (TDAPG 2.01))
Type "help" for help.

postgres=# create table tdapg_main(id integer,mc text) distribute by shard(id);
CREATE TABLE
postgres=# create table tdapg_detail(id integer,tdapg_main_id integer,mc text) distribute by shard(TDAPG_main_id);   
CREATE TABLE
postgres=# explain select TDAPG_detail.* from tdapg_main,TDAPG_detail where TDAPG_main.id=TDAPG_detail.TDAPG_main_id;       
                                 QUERY PLAN                                 
\----------------------------------------------------------------------------
 Data Node Scan on "__REMOTE_FQS_QUERY__"  (cost=0.00..0.00 rows=0 width=0)
   Node/s: dn001, dn002
(2 rows) 

postgres=# explain (verbose) select TDAPG_detail.* from tdapg_main,TDAPG_detail where TDAPG_main.id=TDAPG_detail.TDAPG_main_id; 
                                                                                     QUERY PLAN                                                                                     
\------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
 Data Node Scan on "__REMOTE_FQS_QUERY__"  (cost=0.00..0.00 rows=0 width=0)
   Output: TDAPG_detail.id, TDAPG_detail.TDAPG_main_id, TDAPG_detail.mc
   Node/s: dn001, dn002
   Remote query: SELECT TDAPG_detail.id, TDAPG_detail.TDAPG_main_id, TDAPG_detail.mc FROM public.TDAPG_main, public.TDAPG_detail WHERE (TDAPG_main.id = TDAPG_detail.TDAPG_main_id)
(4 rows)

postgres=# 
```

9) Use the unique index to replace the primary key for the shardkey.
```
postgres=# create unique index TDAPG_main_id_uidx on TDAPG_main using btree(id);
CREATE INDEX
```
This is because that the subsequent maintenance cost of the unique index is much lower than that of the primary key.

10) If a unique index cannot be created for the shardkey, then you should create a regular index to improve the query efficiency:
```
postgres=# create index TDAPG_detail_TDAPG_main_id_idx on TDAPG_detail using btree(TDAPG_main_id);                   
CREATE INDEX
```
Only in this way can the efficiency be improved when two tables are queried with JOIN and a small amount of data is returned.

11) Do not create foreign keys for fields.
The current version doesn't support multi-DN foreign key constraints, unless you can make sure that all foreign key data is on the same DN.
