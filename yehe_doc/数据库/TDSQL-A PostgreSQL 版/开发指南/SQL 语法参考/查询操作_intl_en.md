**Sorting by column**
```
postgres=# DROP TABLE if exists tdapg;
DROP TABLE
postgres=#  CREATE TABLE tdapg (id int, nickname text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO tdapg (nickname) VALUES('TDSQL-A for PostgreSQL is good');              
INSERT 0 1
postgres=# INSERT INTO tdapg (id,nickname) VALUES(1,'The era of TDSQL-A for PostgreSQL has come');       
INSERT 0 1
postgres=# INSERT INTO tdapg (id,nickname) VALUES(2,'hello tdapg '); 
INSERT 0 1
postgres=# SELECT * FROM tdapg ORDER BY id;
 id |    nickname    
----+-----------------------
 1 | The era of TDSQL-A for PostgreSQL has come
 2 | hello tdapg 
  | TDSQL-A for PostgreSQL is good
(3 rows)
```

**Random sorting**
```
postgres=# SELECT * FROM tdapg ORDER BY random();
 id |    nickname    
----+-----------------------
 1 | The era of TDSQL-A for PostgreSQL has come
  | TDSQL-A for PostgreSQL is good
 2 | hello tdapg 
(3 rows)
```

**Computational sorting**
```
postgres=# SELECT * FROM tdapg ORDER BY md5(nickname);
 id |    nickname    
----+-----------------------
 2 | hello tdapg 
  | TDSQL-A for PostgreSQL is good
 1 | The era of TDSQL-A for PostgreSQL has come
(3 rows)
```

**Subquery sorting**
```
postgres=# SELECT * FROM tdapg ORDER BY (SELECT id FROM tdapg ORDER BY random() limit 1);
 id |    nickname    
----+-----------------------
 1 | The era of TDSQL-A for PostgreSQL has come
 2 | hello tdapg 
  | TDSQL-A for PostgreSQL is good
(3 rows)
```

**Null value sorting**
```
postgres=# INSERT INTO tdapg VALUES(4,null);
INSERT 0 1
```

Place null values at the beginning:
```
postgres=# SELECT * FROM tdapg ORDER BY nickname nulls first;
 id |    nickname    
----+-----------------------
 4 | 
 2 | hello tdapg 
 1 | The era of TDSQL-A for PostgreSQL has come
  | TDSQL-A for PostgreSQL is good
(4 rows)
```

Place null values at the end:
```
postgres=# SELECT * FROM tdapg ORDER BY nickname nulls last; 
 id |    nickname    
----+-----------------------
 2 | hello tdapg 
 1 | The era of TDSQL-A for PostgreSQL has come
  | TDSQL-A for PostgreSQL is good
 4 | 
(4 rows)
```

**Sorting by Pinyin**
```
postgres=# SELECT * FROM (VALUES ('张三'), ('王四'),('陈五')) t(myname) ORDER BY myname;               
 myname 
--------
 张三
 王四
 陈五
(3 rows)
```

If the entries are not processed, they will be sorted by UTF-8 encoding of Chinese characters, which does not conform to usage habits:
```
postgres=# SELECT * FROM (VALUES ('张三'), ('王四'),('陈五')) t(myname) ORDER BY convert(myname::bytea,'UTF-8','GBK');
 myname 
--------
 陈五
 王四
 张三
(3 rows)
```

Use the `convert` function to sort the Chinese character entries by Pinyin:
```
postgres=# SELECT * FROM (VALUES ('张三'), ('王四'),('陈五')) t(myname) ORDER BY convert_to(myname,'GBK');      
 myname 
--------
 陈五
 王四
 张三
(3 rows)
```

Use the `convert_to` function to sort the Chinese character entries by Pinyin:
```
postgres=# SELECT * FROM (VALUES ('张三'), ('王四'),('陈五')) t(myname) ORDER BY myname  collate "zh_CN.utf8";
 myname 
--------
 陈五
 王四
 张三
(3 rows)
```
Use `collact` to specify the sorting rule to sort the Chinese character entries by Pinyin.

## `WHERE` Condition Usage
#### Single-Condition query
```
postgres=# SELECT * FROM tdapg WHERE id=1;
 id |    nickname    
----+-----------------------
 1 | The era of TDSQL-A for PostgreSQL has come
(1 row)
```

#### Multi-Condition `and`
```
postgres=# SELECT * FROM tdapg WHERE id=2 and nickname like '%h%';
 id | nickname  
----+-------------
 1 | hello tdapg
(1 row)
```

#### Multi-Condition `or`
```
postgres=# SELECT * FROM tdapg WHERE id=1 or nickname like '%h%';
 id |    nickname    
----+-----------------------
 1 | The era of TDSQL-A for PostgreSQL has come
 2 | hello tdapg 
(2 rows)
```

#### Case-Insensitive match of `ilike`
```
postgres=# CREATE TABLE t_ilike(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t_ilike VALUES(1,'tdapg'),(2,'tdapg');
COPY 2
postgres=# SELECT * FROM t_ilike WHERE mc ilike '%tb%';
 id | mc  
----+-------
 1 | tdapg
 2 | tdapg
(2 rows)
```

#### `WHERE` condition's support for subquery
```
postgres=# SELECT * FROM tdapg WHERE id=(SELECT (random()*2)::integer FROM tdapg ORDER BY random() limit 1); 
 id |    nickname    
----+-----------------------
 1 | The era of TDSQL-A for PostgreSQL has come
(1 row)

postgres=# SELECT * FROM tdapg WHERE id=(SELECT (random()*2)::integer FROM tdapg ORDER BY random() limit 1); 
 id | nickname 
----+----------
(0 rows)
```

#### Null value query method
```
postgres=# SELECT * FROM tdapg WHERE nickname is null;
 id | nickname 
----+----------
 4 | 
(1 row)

postgres=# SELECT * FROM tdapg WHERE nickname is not null;
 id |    nickname    
----+-----------------------
  | TDSQL-A for PostgreSQL is good
 1 | The era of TDSQL-A for PostgreSQL has come
 2 | hello tdapg 
(3 rows)
```

#### `exists` yields `true` if any record is returned
```
postgres=# CREATE TABLE t_exists1(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE

postgres=# INSERT INTO t_exists1 VALUES(1,'tdapg'),(2,'tdapg'); 
COPY 2

postgres=# CREATE TABLE t_exists2(id int,mc text); 
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE

postgres=# INSERT INTO t_exists2 VALUES(1,'tdapg'),(1,'tdapg');
COPY 2

postgres=# SELECT * FROM t_exists1 WHERE exists(SELECT 1 FROM t_exists2 WHERE t_exists1.id=t_exists2.id) ;
 id | mc  
----+-------
 1 | tdapg
(1 row)
```

#### Equivalent of `exists`
```
postgres=# SELECT t_exists1.* FROM t_exists1,(SELECT distinct id FROM t_exists2) as t WHERE t_exists1.id=t.id;
 id | mc  
----+-------
 1 | tdapg
(1 row)
```

## Paged Query
Return one record starting from the first record by default:
```
postgres=# SELECT * FROM tdapg limit 1;
 id |  nickname  
----+---------------
  | TDSQL-A for PostgreSQL is good
(1 row)
```

Use `offset` to specify from which record to return the records. `0` indicates to return one record from the first record:
```
postgres=# SELECT * FROM tdapg limit 1 offset 0; 
 id | nickname  
----+-------------
 1 | hello tdapg
(1 row)
```

Return two records from the third record:
```
postgres=# SELECT * FROM tdapg limit 1 offset 2;
 id |  nickname  
----+--------------
 2 | hello tdapg 
(1 row)
```

You can use `ORDER BY` to get a sorted result:
```
postgres=# SELECT * FROM tdapg ORDER BY id limit 1 offset 2;
 id | nickname 
----+----------
 4 | 
(1 row)
```

## Combining Multiple Query Results
#### No duplicate record filtering
```
postgres=# create table u1(a int,b varchar)with(orientation=column);
CREATE TABLE
postgres=# create table u2(a int,b varchar)with(orientation=column);
CREATE TABLE
postgres=# insert into u1 values(1,'hi'),(2,'hello');
COPY 2
postgres=# insert into u2 values(1,'hi'),(2,'hello'),(3,'nihao');
COPY 3
postgres=# select * from u1 union all select * from u2 order by 1;
 a |  b  
---+-------
 1 | hi
 1 | hi
 2 | hello
 2 | hello
 3 | nihao
(5 rows)
```

#### Duplicate record filtering
```
postgres=# select * from u1 union select * from u2 order by 1;
 a |  b  
---+-------
 1 | hi
 2 | hello
 3 | nihao
(3 rows)
```

#### Use of subqueries distributed in combined result
```
postgres=# SELECT * FROM ( SELECT * FROM tdapg limit 1) as t union all SELECT * FROM (SELECT * FROM t_appoint_col limit 1) as t ; 
 id |  nickname  
----+---------------
  | TDSQL-A for PostgreSQL is good
 2 | hello tdapg
(2 rows)
```

## Returning the Intersection of Two Results
```
postgres=# CREATE TABLE t_intersect1(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t_intersect1 VALUES(1,'tdapg'),(2,'tdapg');
COPY 2
postgres=# CREATE TABLE t_intersect2(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t_intersect2 VALUES(1,'tdapg'),(3,'tdapg');
COPY 2
postgres=# SELECT * FROM t_intersect1 INTERSECT SELECT * FROM t_intersect2;
 id | mc  
----+-------
 1 | tdapg
(1 row)
```

## Returning the Difference of Two Results
```
postgres=# CREATE TABLE t_except1(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t_except1 VALUES(1,'tdapg'),(2,'tdapg');
COPY 2
postgres=# CREATE TABLE t_except2(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t_except2 VALUES(1,'tdapg'),(3,'tdapg');
COPY 2
postgres=# SELECT * FROM t_except1 except SELECT * FROM t_except2;
 id | mc  
----+-------
 2 | tdapg
(1 row)
```

## Multi-Table Join
#### Inner join
```
postgres=# SELECT * FROM tdapg inner join t_appoint_col on tdapg.id=t_appoint_col.id;
 id |  nickname  | id | nickname 
----+--------------+----+-------------
 2 | hello tdapg | 2 | hello tdapg
(1 row)
```

#### Left outer join
```
postgres=# SELECT * FROM tdapg left join t_appoint_col on tdapg.id=t_appoint_col.id;
 id |    nickname    | id |  nickname 
----+-----------------------+----+-------------
  | TDSQL-A for PostgreSQL is good     |  | 
 1 | The era of TDSQL-A for PostgreSQL has come |  | 
 2 | hello tdapg      | 2 | hello tdapg
 4 |            |  | 
(4 rows)
```

#### Right outer join
```
postgres=# SELECT * FROM tdapg right join t_appoint_col on tdapg.id=t_appoint_col.id; 
 id |  nickname  | id | nickname 
----+--------------+----+-------------
 2 | hello tdapg | 2 | hello tdapg
(1 row)
```

#### Full join
```
postgres=# SELECT * FROM tdapg full join t_appoint_col on tdapg.id=t_appoint_col.id;
 id |    nickname    | id | nickname 
----+-----------------------+----+-------------
  | TDSQL-A for PostgreSQL is good     |  | 
 1 | The era of TDSQL-A for PostgreSQL has come |  | 
 2 | hello tdapg      | 2 | hello tdapg
 4 |            |  | 
(4 rows)
```
