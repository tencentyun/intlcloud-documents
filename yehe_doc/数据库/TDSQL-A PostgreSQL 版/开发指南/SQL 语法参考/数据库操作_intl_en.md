## Creating Database
To create a database, you must be a superuser or have the special `CREATEDB` permission. By default, the new database will be created by cloning the standard system database `template1`. A different template can be specified by writing `TEMPLATE name`. In particular, by writing `TEMPLATE template0`, you can create a pristine database (one where no user-defined objects exist and where the system objects have not been altered) containing only the standard objects predefined by your version of TDSQL-A for PostgreSQL.

### Creating database by using default parameters
```
postgres=# CREATE DATABASE tdapg_db;
CREATE DATABASE
```

### Specifying database to be cloned
```
postgres=# CREATE DATABASE tdapg_db_template TEMPLATE template0;
CREATE DATABASE
```

### Specifying owner
```
postgres=# CREATE ROLE pgxz WITH LOGIN;
CREATE ROLE
postgres=# CREATE DATABASE tdapg_db_owner OWNER pgxz;
CREATE DATABASE
postgres=# \l+ tdapg_db_owner
                         List of databases
   Name   | Owner | Encoding | Collate  |  Ctype  | Access privileges | Size | Tablespace | Description 
----------------+-------+----------+------------+------------+-------------------+-------+------------+-------------
 tdapg_db_owner | pgxz | UTF8   | en_US.utf8 | en_US.utf8 |          | 18 MB | pg_default | 
(1 row)
```

### Specifying encoding
```
postgres=# CREATE DATABASE tdapg_db_encoding ENCODING UTF8;  
CREATE DATABASE
postgres=# \l+ tdapg_db_encoding
                          List of databases
    Name    | Owner | Encoding | Collate  |  Ctype  | Access privileges | Size | Tablespace | Description 
-------------------+-------+----------+------------+------------+-------------------+-------+------------+-------------
 tdapg_db_encoding | dbadmin | UTF8   | en_US.utf8 | en_US.utf8 |          | 18 MB | pg_default | 
(1 row)
```

### Specifying sorting rule
```
postgres=# CREATE DATABASE tdapg_db_lc_collate LC_COLLATE 'zh_CN.utf8';
CREATE DATABASE
postgres=# \l+ tdapg_db_lc_collate
                          List of databases
    Name     | Owner | Encoding | Collate  |  Ctype  | Access privileges | Size | Tablespace | Description 
---------------------+-------+----------+------------+------------+-------------------+-------+------------+-------------
 tdapg_db_lc_collate | dbadmin | UTF8   | zh_CN.utf8 | zh_CN.utf8 |          | 18 MB | pg_default |
```

### Specifying grouping rule
```
postgres=# CREATE DATABASE tdapg_db_lc_ctype LC_CTYPE 'zh_CN.utf8';
CREATE DATABASE
postgres=# \l+ tdapg_db_lc_ctype
                          List of databases
    Name    | Owner | Encoding | Collate  |  Ctype  | Access privileges | Size | Tablespace | Description 
-------------------+-------+----------+------------+------------+-------------------+-------+------------+-------------
 tdapg_db_lc_ctype | dbadmin | UTF8   | zh_CN.utf8 | zh_CN.utf8 |          | 18 MB | pg_default | 
(1 row)
```

### Configuring data connectivity
```
postgres=# CREATE DATABASE tdapg_db_allow_connections ALLOW_CONNECTIONS true;

CREATE DATABASE
postgres=# SELECT datallowconn FROM pg_database WHERE datname='tdapg_db_allow_connections'; 
 datallowconn 
--------------
 t
(1 row)
```

### Configuring the number of connections
```
postgres=# CREATE DATABASE tdapg_db_connlimit CONNECTION LIMIT 100;
CREATE DATABASE
postgres=# SELECT datconnlimit FROM pg_database WHERE datname='tdapg_db_connlimit';            
 datconnlimit 
--------------
     100
(1 row)
```

### Configuring database replicability
```
postgres=# CREATE DATABASE tdapg_db_istemplate IS_TEMPLATE true;
CREATE DATABASE
postgres=# SELECT datistemplate FROM pg_database WHERE datname='tdapg_db_istemplate';      
 datistemplate 
---------------
 t
(1 row)
```

### Configuring multiple parameters together
```
postgres=# CREATE DATABASE tdapg_db_mul OWNER pgxz CONNECTION LIMIT 50 TEMPLATE template0 ENCODING 'utf8' LC_COLLATE 'C';
CREATE DATABASE
```

## Altering Database
### Renaming database
```
postgres=# ALTER DATABASE tdapg_db RENAME TO tdapg_db_new;
ALTER DATABASE
```

If you alter a database when a session is connected to it, the following error will be reported:
```
ERROR: database "tdapg_db" is being accessed by other users
DETAIL: There are 6 other sessions using the database.
```

You can use the following method to disconnect the session and then alter the database:
```
postgres=# SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname='tdapg_db_template';  
 pg_terminate_backend 
----------------------
 t
(1 row)
```

### Modifying the number of connections
```
postgres=# ALTER DATABASE tdapg_db_new CONNECTION LIMIT 50;
ALTER DATABASE
```

### Changing database owner
```
postgres=# ALTER DATABASE tdapg_db_new OWNER TO dbadmin;
ALTER DATABASE
```

### Configuring default database running parameters
```
postgres=# ALTER DATABASE tdapg_db_new SET search_path TO public,pg_catalog,pg_oracle;   
ALTER DATABASE
```

`ALTER DATABASE` doesn't support the following items:

| **Item**   | **Remarks** |
| ---------- | -------- |
| encoding   | Encoding |
| lc_collate | Sorting rule |
| lc_ctype   | Grouping rule |

## Dropping Database
```
postgres=# DROP DATABASE tdapg_db_new;
DROP DATABASE
```

If you drop a database when a session is connected to it, the following error will be reported:
```
postgres=# DROP DATABASE tdapg_db_template;
ERROR: database "tdapg_db_template" is being accessed by other users
DETAIL: There is 1 other session using the database.
```
You can use the following method to disconnect the session and then drop the database:
```
postgres=# SELECT pg_terminate_backend(pid) FROM pg_stat_activity WHERE datname='tdapg_db_template';  
 pg_terminate_backend 
----------------------
 t
(1 row)
postgres=# DROP DATABASE tdapg_db_template;
DROP DATABASE
```

