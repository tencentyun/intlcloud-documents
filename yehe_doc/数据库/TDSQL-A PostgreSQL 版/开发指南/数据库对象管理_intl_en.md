## Tablespace
Tablespaces allow admins to define locations in the file system where the files representing database objects can be stored. In TDSQL-A for PostgreSQL, a tablespace is actually a storage directory specified for a table.

By using tablespaces, an admin can control the disk layout of a TDSQL-A for PostgreSQL installation. This is useful in two ways:
- If the partition or volume on which the cluster was initialized runs out of space and cannot be extended, a tablespace can be created on a different partition and used until the system can be reconfigured.
- Tablespaces allow an admin to use the knowledge of the usage pattern of database objects to optimize performance. For example, an index which is very heavily used can be placed on a very fast, highly available disk, such as an expensive solid state device. At the same time, a table storing archived data which is rarely used or not performance critical could be stored on a less expensive, slower disk system.

System tablespaces:
1. The `pg_default` tablespace is the default tablespace used to store system catalog objects, user tables, user table indexes, temporary tables, temporary table indexes, and internal temporary tables. Its corresponding storage directory is `$PADATA/base/`.
2. The `pg_global` tablespace is used to store system dictionaries. Its corresponding storage directory is `$PADATA/global/`.

List existing tablespaces:
```
postgres-# \db
   List of tablespaces
  Name  | Owner | Location 
------------+-------+----------
 pg_default | dbadmin | 
 pg_global | dbadmin | 
(2 rows)
```


## Database
A database is a set of organized, shared, and centrally managed data that is stored on a computer for a long period.

List existing databases:
```
postgres-# \l
               List of databases
  Name  | Owner | Encoding | Collate  |  Ctype  | Access privileges 
-----------+-------+----------+------------+------------+-------------------
 colstore | dbadmin | UTF8   | zh_CN.utf8 | zh_CN.utf8 | 
 postgres | dbadmin | UTF8   | zh_CN.utf8 | zh_CN.utf8 | 
 template0 | dbadmin | UTF8   | zh_CN.utf8 | zh_CN.utf8 | =c/dbadmin     +
      |    |     |      |      | dbadmin=CTc/dbadmin
 template1 | dbadmin | UTF8   | zh_CN.utf8 | zh_CN.utf8 | =c/dbadmin     +
      |    |     |      |      | dbadmin=CTc/dbadmin
(4 rows)
```

## Schema
A schema is essentially a namespace. It is generally called "user" in Oracle, "framework" in SQL Server, and "database" in MySQL. A schema contains tables, data types, functions, and operators whose names can duplicate those of other objects existing in other schemas. You can use `schema name.object name` to access an object in a schema.

## Table
A table in a relational database is two-dimensional: it consists of rows and columns.
- The number and order of columns are fixed, and each column has a name.
- The number of rows is variable. It reflects how much data is stored at a given moment. SQL does not make any guarantees about the order of the rows in a table. When a table is read, the rows will appear in random order, unless sorting is explicitly requested.

Each column has a data type. The data type constrains the set of possible values that can be assigned to a column and assigns semantics to the data stored in the column so that it can be used for computations.
For instance, a column declared to be of a numerical type will not accept arbitrary text strings, and the data stored in such a column can be used for mathematical computations. By contrast, a column declared to be of a character string type will accept almost any kind of data but it does not lend itself to mathematical calculations, although other operations such as string concatenation are available.

TDSQL-A for PostgreSQL includes a sizable set of built-in data types that fit many applications. You can also define your own data types. Most built-in data types have obvious names and semantics. For more information, please see [Data Types](https://intl.cloud.tencent.com/document/product/1099/40796).
Some of the frequently used data types are integer for whole numbers, numeric for possibly fractional numbers, text for character strings, date for dates, time for time-of-day values, and timestamp for values containing both date and time.

## Index
Indexes are a common way to enhance database performance. An index allows the database server to find and retrieve specific rows much faster than it could do without an index. But indexes also add overhead to the database system as a whole, so they should be used sensibly.

TDSQL-A for PostgreSQL provides several index types: regular index, unique index, index on expression, B-tree, Hash, GiST and GIN. Each index type uses a different algorithm that is best suited to different types of queries. By default, the `CREATE INDEX` command creates B-tree indexes, which fit the most common situations.

- Regular indexes are the most basic indexes without any limit.

- Unique indexes can be used to enforce the uniqueness of index attribute values or attribute combination values.
- Indexes on expressions are built based on a function or expression calculated from one or multiple attributes in a table, which take effect only if the same expression as that during index creation is used during query. 
- B-trees can handle equality and range queries on data that can be sorted into some ordering. In particular, the TDSQL-A for PostgreSQL query planner will consider using a B-tree index whenever an indexed column is involved in a comparison using one of these operators: `<, <=, =, >, and >=`. Constructs equivalent to combinations of these operators, such as `BETWEEN` and `IN`, can also be implemented with a B-tree index search.
Also, an `IS NULL` or `IS NOT NULL` condition on an index column can be used with a B-tree index. B-tree indexes can also be used to retrieve data in sorted order. This is not always faster than a simple scan and sort, but it is often helpful.
- Hash indexes can only handle simple equality comparisons. The query planner will consider using a hash index whenever an indexed column is involved in a comparison using the = operator.
- GiST indexes are not a single kind of index, but rather an infrastructure within which many different indexing strategies can be implemented. Accordingly, the particular operators with which a GiST index can be used vary depending on the indexing strategy (the operator class). As an example, the standard distribution of TDSQL-A for PostgreSQL includes GiST operator classes for several two-dimensional geometric data types, which support indexed queries using these operators: `<<, &<, &>, >>, <<|, &<|, |&>, |>>, &>, <&, ~+, and &&`.
- GIN indexes are inverted indexes which can handle values that contain multiple keys (such as arrays). Like GiST, GIN can support many different user-defined indexing strategies and the particular operators with which a GIN index can be used vary depending on the indexing strategy.

## View
A view is a pseudo-table exported from one or multiple tables, whose behaviors are very similar to those of a table. The database stores only the view definition, rather than the view data, which is still stored in the original basic tables. If the data in the basic table changes, the data queried from the corresponding view also changes.

View the view list:
```
postgres-# \dv
       List of relations
 Schema |    Name    | Type | Owner 
--------+--------------------+------+-------
 public | pg_stat_statements | view | dbadmin
(1 row)
```

## Sequence
Sequence objects, also called sequence generators or just sequences, are special single-row tables created with `CREATE SEQUENCE`. Sequence objects are commonly used to generate unique identifiers for rows or tables.

View the sequence list:
```
postgres=# \ds
     List of relations
 Schema | Name |  Type  | Owner 
--------+--------+----------+-------
 public | serial | sequence | dbadmin
(1 row)
```
