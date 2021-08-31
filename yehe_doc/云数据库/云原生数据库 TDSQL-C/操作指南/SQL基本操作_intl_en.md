
## Basic Operations in TDSQL-C (MySQL Edition)
### Querying version
Method 1:
```
MySQL [(none)]> SELECT CYNOS_VERSION();
+------------------------+
| CYNOS_VERSION() |
+------------------------+
| 5.7.mysql_cynos.1.3.10 |
+------------------------+
1 row in set (0.00 sec)
```
Method 2:
```
MySQL [(none)]> SELECT @@CYNOS_VERSION;
+------------------------+
| @@CYNOS_VERSION |
+------------------------+
| 5.7.mysql_cynos.1.3.10 |
+------------------------+
1 row in set (0.00 sec)
```
Method 3:
```
MySQL [(none)]> SHOW VARIABLES LIKE 'CYNOS_VERSION'; 
+---------------+------------------------+
| Variable_name | Value |
+---------------+------------------------+
| cynos_version | 5.7.mysql_cynos.1.3.10 |
+---------------+------------------------+
1 row in set (0.01 sec)
```

## Basic Operations in TDSQL-C (PostgreSQL Edition)

### Querying version
```
postgres=# select cynosdb_version(); cynosdb_version
————————
 CynosDB 1.0
(1 row)
```


### Creating table
```
postgres=# create table x(x1 int, x2 int);
CREATE TABLE

postgres=# insert into x values(1, 2);
INSERT 0 1

postgres=# update x set x1 = 1;
UPDATE 1
```

### Creating view
```
postgres=# create view v_x as select * from x;
CREATE VIEW

postgres=# select * from v_x;

 x1 | x2
——+——
  1 |  2
(1 row)
```

### Querying table
```
postgres=# select * from x;


 x1 | x2
——+——
  1 |  2
(1 row)
```

### System table
TDSQL-C supports PostgreSQL 10 system tables, such as pg_class and pg_proc.

### GUC parameters
TDSQL-C is compatible with the GUC parameters of PostgreSQL 10. You can use the `SHOW` or `SET` command to display or set GUC parameters.

### Index
TDSQL-C supports multiple indexes, such as B-tree, Hash, GiST, SP-GiST, GIN, and BRIN. The default index created by `CREATE INDEX` is B-tree index.

### Multi-Column and single-column indexes
```
postgres=# CREATE TABLE test2 (
postgres(#   major int,
postgres(#   minor int,
postgres(#   name varchar
postgres(# );
CREATE TABLE
```

### Supporting multi-column index
```
postgres=# CREATE INDEX test2_mm_idx ON test2 (major, minor);
CREATE INDEX
```
### Supporting single-column index
```
postgres=# CREATE INDEX test2_mm ON test2 (name);
CREATE INDEX
```

### Expression index
TDSQL-C is compatible with PostgreSQL 10 and supports expression indexes.
```
postgres=# CREATE INDEX test2_expr ON test2 ((major + minor));
CREATE INDEX
```

