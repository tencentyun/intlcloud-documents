## Creating Schema
Standard statement:
```
postgres=# CREATE SCHEMA tdapg;
CREATE SCHEMA
```

Use the extended syntax to create a schema only if it does not exist:
```
postgres=# CREATE SCHEMA IF NOT EXISTS tdapg ;  
NOTICE: schema "tdapg" already exists, skipping
CREATE SCHEMA
```

Specify the owner:
```
postgres=# CREATE SCHEMA tdapg_pgxz AUTHORIZATION pgxz;
CREATE SCHEMA

postgres=# \dn tdapg_pgxz
 List of schemas
  Name  | Owner 
------------+-------
 tdapg_pgxz | pgxz
(1 row)
```

## Altering Schema
Rename a schema:
```
postgres=# ALTER SCHEMA tdapg RENAME TO tdapg_new;
ALTER SCHEMA
```

Change the owner:
```
postgres=# ALTER SCHEMA tdapg_pgxz OWNER TO tdapg;
ALTER SCHEMA
```

## Dropping Schema
```
postgres=# DROP SCHEMA tdapg_new;
DROP SCHEMA
```

If there are objects in the schema, dropping will fail, and the following message will be prompted:
```
postgres=# CREATE TABLE tdapg_pgxz.t(id int);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# DROP SCHEMA tdapg_pgxz;
ERROR: cannot drop schema tdapg_pgxz because other objects depend on it
DETAIL: table tdapg_pgxz.t depends on schema tdapg_pgxz
HINT: Use DROP ... CASCADE to drop the dependent objects too.
```

Use `CASCADE` to forcibly drop it:
```
postgres=# DROP SCHEMA tdapg_pgxz CASCADE;
NOTICE: drop cascades to table tdapg_pgxz.t
DROP SCHEMA
```

## Configuring User Access to Schema
If a regular user wants to access an object in a schema, the user needs to be authorized to access both the object and the schema.
```
[tdapg@VM_0_37_centos root]$ psql -U dbadmin
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.

postgres=# CREATE SCHEMA tdapg;
CREATE SCHEMA
postgres=# CREATE TABLE tdapg.t(id int);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
```

Grant the `pgxz` user the permission to query the `tdapg.t` table:
```
postgres=# GRANT SELECT ON tdapg.t TO pgxz;
GRANT
postgres=# \q
[tdapg@VM_0_37_centos root]$ psql -U pgxz
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.
```

Before the user is granted access to the `tdapg` schema, the user still cannot access the table:
```
postgres=> SELECT * FROM tdapg.t;
ERROR: permission denied for schema tdapg
LINE 1: SELECT * FROM tdapg.t;
           ^
postgres=> \q
[tdapg@VM_0_37_centos root]$ psql -U dbadmin
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.

postgres=# GRANT USAGE ON SCHEMA tdapg TO pgxz;
GRANT
postgres=# \q
[tdapg@VM_0_37_centos root]$ psql -U pgxz
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.
```

After the user is granted access to the `tdapg` schema, the user can access the `tdapg.t` table:
```
postgres=> SELECT * FROM tdapg.t;
 id 
----
(0 rows)
```

## Configuring Schema Access Order
TDSQL-A for PostgreSQL provides an execution variable named `search_path` to configure the order of data object access, whose value is a list of schema names as shown below:

View the currently connected user:
```
[tdapg@VM_0_37_centos root]$ psql -U dbadmin
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.
postgres=# SELECT current_user;
 current_user 
--------------
 dbadmin
(1 row)
```

There are two schemas in total:
```
postgres=# \dn
  List of schemas
   Name   | Owner 
--------------+-------
 public    | dbadmin
 tdapg    | dbadmin
(2 rows)
```

Set the search path to `"$user", public` where "$user" is the current username, i.e., `"dbadmin"` (value of `current_user` in the above code):
```
postgres=# SHOW search_path ;
  search_path 
-----------------
 "$user", public
(1 row)
```

Create a table without specifying its schema, and it will be stored in the first searched schema:
```
postgres=# CREATE TABLE t_schema(id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# \dt t_schema
     List of relations
 Schema |  Name  | Type | Owner 
--------+----------+-------+-------
 dbadmin| t_schema | table | dbadmin
(1 row)
```

Specify the schema to store the table. Table names in different schemas can be the same:
```
postgres=# CREATE SCHEMA tdapg_schema;
CREATE SCHEMA
postgres=# CREATE TABLE tdapg_schema.t_schema (id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# \dt tdapg_schema.t_schema
      List of relations
  Schema  |  Name  | Type | Owner 
--------------+----------+-------+-------
 tdapg_schema | t_schema | table | dbadmin
(1 row)
```

If you want to access an object outside the search path, you need to enter its full path:
```
postgres=# CREATE TABLE tdapg_schema.t2 (id int,mc text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE

postgres=# SELECT * FROM t2;
ERROR: relation "t2" does not exist
LINE 1: SELECT * FROM t2;
           ^
postgres=# SELECT * FROM tdapg_schema.t2;
 id | mc 
----+----
(0 rows)
```
The above error occurs because the `tdapg_schema` schema is not configured in the `search_path`.
