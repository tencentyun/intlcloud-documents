TDSQL-A for PostgreSQL supports multiple modules and opens up its module extension APIs. You can use the `CREATE EXTENSION` syntax to load a new extension into your database. The name of the extension to be loaded must be unique.

Loading an extension essentially amounts to running the extension's script file. The script will typically create new SQL objects such as functions, data types, operators, and index support methods.
`CREATE EXTENSION` additionally records the identities of all the created objects, so that they can be dropped again if `DROP EXTENSION` is issued. Before you can use `CREATE EXTENSION` to load an extension into a database, the extension's supporting files must be installed.

The extensions currently available for loading can be identified from the [pg_available_extension_versions](http://postgres.cn/docs/10/view-pg-available-extension-versions.html) system views.
You can view deployed extensions in the `pg_extension` system table or by running the `\dx` metacommand in psql.
Do not drop system default extensions; otherwise, unpredictable cluster failures may occur.

## Extension Management
The following are some extensions existing in the cluster by default:
- pageinspect: it provides functions that allow you to inspect the contents of database pages at a low level, which is useful for debugging purposes.
- pg_check: it checks the catalog consistency.
- pg_clean: it removes prepared transactions for two-phase commit.
- pg_errcode_stat: it tracks cluster process exceptions.
You can access the `pg_errcode_stat` function to view the current cluster exceptions and use `pg_errcode_stat_reset` to clear them.
- pg_squeeze: it reclaims certain invalid space resources. Compared with `vacuum full`, it doesn't generate prolonged table locks that block reads/writes.
- pg_stat_error: it tracks cluster process exceptions.
- pg_stat_log: it tracks the execution information of all SQL statements.
- pg_stat_statements: it provides a method for tracking execution statistics of all SQL statements executed by a server.
- pg_unlock: it detects and resolves deadlocks.
- plpgsql: it is an extension for the PL/pgSQL programming language.
- Plpythonu: it is an extension for the PL/Python programming language.

### Viewing extension
```
postgres=# SELECT e.extname AS "Name", e.extversion AS "Version", n.nspname AS "Schema", c.description
AS "Description" FROM pg_catalog.pg_extension e LEFT JOIN pg_catalog.pg_namespace n ON n.oid =
e.extnamespace LEFT JOIN pg_catalog.pg_description c ON c.objoid = e.oid AND c.classoid =
'pg_catalog.pg_extension'::pg_catalog.regclass ORDER BY 1;
Name | Version | Schema | Description
--------------------+---------+------------+-----------------------------------------------------------
pageinspect | 1.1 | public | inspect the contents of database pages at a low level
pg_errcode_stat | 1.1 | public | track error code of all processes
pg_stat_statements | 1.1 | public | track execution statistics of all SQL statements executed
plpgsql | 1.0 | pg_catalog | PL/pgSQL procedural language
shard_statistic | 1.0 | public | tools for get shard statistic
(5 rows)
```

### Creating extension
```
postgres=# create extension "uuid-ossp" with schema tdapg;
CREATE EXTENSION
```
The above statement creates `uuid-ossp` under the `tdapg` schema.

### Dropping extension
```
postgres=# drop extension "uuid-ossp" ;
DROP EXTENSION
```

## `pg_trgm` Extension Usage
Prefix, suffix, and prefix-suffix fuzzy matches as well as regex matches are common needs in text search. In addition to full-text search, TDSQL-A for PostgreSQL also provides `pg_trgm` for text search.
For prefix and suffix fuzzy matches, TDSQL-A for PostgreSQL uses B-tree for acceleration just like other databases.
For prefix-suffix fuzzy match and regex match, `pg_trgm` can be used. It is a very powerful extension and can effectively improve the performance in such text search scenarios. The performance for searching about 1 million data entries can be improved by 100 times.
Create the extension:
```
postgres=# create extension pg_trgm;;
CREATE EXTENSION
```
Create a table for full-text search:
```
postgres=# create table t_trgm (id int,trgm text,no_trgm text);
CREATE TABLE
```
Insert the test data:
```
postgres=# insert into t_trgm select t,md5(t::text),md5(t::text) from generate_series(1,1000000) as t;
INSERT 0 1000000
```
Create an index for trgm:
```
postgres=# create index t_trgm_trgm_idx on t_trgm using gist(trgm gist_trgm_ops);
CREATE INDEX
```
