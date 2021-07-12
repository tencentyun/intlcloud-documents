
## Creating Sequence
### Creating sequence
```
postgres=# CREATE SEQUENCE tdapg_seq;
CREATE SEQUENCE
```

Create a sequence only if it does not exist:
```
postgres=# CREATE SEQUENCE IF NOT EXISTS tdapg_seq; 
NOTICE: relation "tdapg_seq" already exists, skipping
CREATE SEQUENCE
```

### Viewing current sequence usage
```
postgres=# \x 
Expanded display is on.
postgres=# SELECT * FROM tdapg_seq ;
-[ RECORD 1 ]-
last_value | 1
log_cnt  | 0
is_called | f
```

### Getting next value in sequence
```
postgres=# SELECT nextval('tdapg_seq');
-[ RECORD 1 ]
nextval | 1
```

### Getting current sequence value
You can use the following command only after accessing `nextval()`:
```
postgres=# SELECT currval('tdapg_seq');
-[ RECORD 1 ]
currval | 1
```

You can also use the following method to get the currently used value in the sequence:
```
postgres=# SELECT last_value FROM tdapg_seq ;
-[ RECORD 1 ]-
last_value | 1
```

### Setting current sequence value
```
postgres=# SELECT setval('tdapg_seq',1);
-[ RECORD 1 ]
setval | 1
postgres=# \x
Expanded display is off.
```

## Using Sequence
```
postgres=# CREATE TABLE t (id int, nickname text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO t (id,nickname) VALUES(nextval('tdapg_seq'),'tdapg good');  
INSERT 0 1
postgres=# SELECT * FROM t;
 id | nickname 
----+----------
 2 | tdapg good
(1 row)
```

#### Using sequence as default field value
```
postgres=# ALTER TABLE t alter column id set default nextval('tdapg_seq');
postgres=# INSERT INTO t (nickname) VALUES('hello tdapg');                     
INSERT 0 1
postgres=# SELECT * FROM t;
 id | nickname  
----+-------------
 3 | hello tdapg
 2 | tdapg good
(2 rows)
```

#### Using sequence as field type
```
postgres=# DROP TABLE t;
DROP TABLE
postgres=# CREATE TABLE t (id serial not null,nickname text);
CREATE TABLE
postgres=# INSERT INTO t (nickname) VALUES('hello tdapg');  
INSERT 0 1
postgres=# SELECT * FROM t;
 id | nickname  
----+-------------
 1 | hello tdapg
(1 row)
```

## Deleting sequence
```
postgres=# DROP SEQUENCE tdapg_seq;
DROP SEQUENCE
```

Delete a sequence (skip it if it does not exist):
```
postgres=# DROP SEQUENCE IF EXISTS tdapg_seq;  
NOTICE: sequence "tdapg_seq" does not exist, skipping
DROP SEQUENCE
```
