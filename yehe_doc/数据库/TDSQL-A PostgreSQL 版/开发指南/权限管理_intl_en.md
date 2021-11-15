
## User
You can use `CREATE USER` and `ALTER USER` to create and manage database users respectively. A database cluster contains one or multiple named databases. Users and roles are shared within the entire cluster, but their data is not shared, that is, a user can connect to any database, but after the connection succeeds, the user can only access the database declared in the connection request. 
```
postgres=# **CREATE USER** tdapg_user1 PASSWORD 'tdapg@123';
CREATE ROLE
```

If you want to create a user who has the permission to create databases, you need to add the `CREATEDB` keyword.
```
postgres=# CREATE USER tdapg_user2 CREATEDB PASSWORD 'tdapg@123';
CREATE ROLE
```

Change the login password of the `tdapg_user2` user from `tdapg@123` to `Abcd@123`:
```
postgres=# **ALTER USER** tdapg_user2 with password 'Abcd@123';
ALTER ROLE
```
- Grant the `CREATEROLE` permission to the `tdapg_user2` user: 
```
ALTER USER tdapg_user2 CREATEROLE; 
```
- Delete a user:
```
DROP USER tdapg_user2;
```


## Role
A role is a set of permissions. After you use `GRANT` to grant a role to a user, the user will have all permissions of the role. We recommend you use roles for efficient permission assignment; for example, you can create different roles for designers, developers, and OPS engineers, grant users the corresponding roles, and grant users under each role the permissions to access data required by their jobs. If you grant/revoke a permission to/from a role, the change will apply to all users under the role.

Create a user that can log in without setting a password for the user:
```
postgres=# CREATE ROLE Tdapg_role1 LOGIN;
CREATE ROLE
```

Create a role that can create databases and manage roles:
```
postgres=# CREATE ROLE Tdapg_role2 WITH CREATEDB CREATEROLE;
CREATE ROLE
```

Grant the permissions of a role to a user:
```
postgres=# GRANT Tdapg_role1 , Tdapg_role2 TO tdapg_user1; 
GRANT ROLE
```

## Schema
By managing schemas, you can enable multiple users to use the same database without interfering with each other, organize database objects into logical groups for easy management, and add third-party applications to corresponding schemas without causing any conflicts. 

Each database contains one or multiple schemas, and each schema contains tables and objects in other types. Initially after a database is created, there will be a default schema named `public`, and all users have the permission of it. You can use schemas to group database objects. A schema is like a directory on an operating system, but it cannot be nested. 

## User Permission Settings
### Database-Level permission management
Use the superuser to create the `user1` user and a test database:
```
postgres=# create user user1 password 'tdapg@123';
CREATE ROLE

postgres=# create database testdb;
CREATE DATABASE
```

Grant the `user1` user CRUD permission for the test database:
```
postgres=# grant create,connect on database testdb to user1;
GRANT
```

Use the `user1` user to perform CRUD operations on the test database:
```
[tdapg@TENCENT64 ~]$ psql -d testdb -p 11347 -U user1
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.


testdb=> create schema schm_user1;
CREATE SCHEMA
testdb=> create table schm_user1.t1(id int);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
testdb=> INSERT INTO schm_user1.t1 VALUES(1);
INSERT 0 1
testdb=> select * from schm_user1.t1;
 id 
----
 1
(1 row) 


testdb=> delete from schm_user1.t1 ;
DELETE 1
```

Use the `user1` user to log in and revoke its permissions:
```
postgres=# revoke all on database testdb from user1;
REVOKE
```

Use the `user1` user to connect to the `testdb` database and create a scheme. The system prompts that `user1` has no permission to create a scheme, indicating that the permissions have been revoked successfully.
```
[tdapg@TENCENT64 ~]$ psql -d testdb -p 11347 -U user1
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.
 
testdb=> create schema schema_user1;
ERROR: permission denied for database testdb
```

### Table-Level permission management
Grant a user the permission to perform CRUD operations on entries in a table.
Use the admin account `dbadmin` to connect to a CN, create the `user1` user, and a test database.

Grant the user the permission to access a schema:
```
postgres=# CREATE SCHEMA mysch;
CREATE SCHEMA
postgres=# CREATE USER user1 PASSWORD 'tdapg@123';
CREATE ROLE
postgres=# CREATE TABLE mysch.t2(id int,name text);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# GRANT usage ON SCHEMA mysch TO user1; 
GRANT
```
>?By default, regular users have no access to unauthorized schemas; therefore, if you want to grant a user access to a table, you need to grant the user the permission to use the schema where the table resides. 
If the user has no access to the schema, `ERROR: permission denied for schema mysch` will be prompted.

Grant a user the permission to perform CRUD operations on entries in a table:
```
postgres=# GRANT SELECT ON mysch.t2 TO user1; 
GRANT
postgres=# GRANT ALL ON mysch.t2 TO user1; 
GRANT 
```
>?CRUD refers to `INSERT`, `DELETE`, `UPDATE`, and `SELECT`. If you want to grant all permissions, write `all`.

Revoke the access permission from a user:
```
postgres=# REVOKE ALL ON mysch.t2 FROM user1;
REVOKE 
postgres=# REVOKE SELECT ON mysch.t2 FROM user1; 
REVOKE 
```

Grant a user access to all tables in a schema:
```
postgres=# CREATE TABLE mysch.t4(f1 serial,f2 int); 
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# CREATE TABLE mysch.t5(f1 serial,f2 int); 
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# GRANT ALL ON ALL TABLES IN SCHEMA mysch TO user1; 
GRANT 
postgres=# \c - user1
You are now connected to database "postgres" as user "user1".
postgres=> SELECT * FROM mysch.t4;
 f1 | f2 
----+----
(0 rows)
 

postgres=> SELECT * FROM mysch.t5;
 f1 | f2 
----+----
(0 rows)
postgres=> \q
```

Use the admin account `dbadmin` to connect to a CN, create the `user1` user, and a test database.
Revoke access to all tables in a schema:
```
postgres=# REVOKE ALL ON ALL TABLES IN SCHEMA mysch FROM user1; 
REVOKE
```

### Field-Level permission management
Use the superuser to create the `user1` user, a test database, and the table `t0(id int,name varchar(10),num varchar(20));`:
```
postgres=# create user user1 password 'tdapg@123';
CREATE ROLE 
postgres=# create database testdb;
CREATE DATABASE
postgres=# \c testdb
You are now connected to database "testdb" as user "dbadmin".
testdb=# create table t0(id int,name varchar(10),num varchar(20)) distribute by replication; CREATE TABLE
```

Grant the `user1` user CRUD permission for the `ID` field in the `t0` table:
```
testdb=# grant select(id),insert(id),update(id) on t0 to user1;
GRANT
```

Use the `user1` user to perform CRUD operations on the `t0` table and perform CRUD operations on the `ID` column:
```
[tdapg@TENCENT64 ~]$ psql -d testdb -p 11347 -U user1
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.
 
testdb=> insert into t0 values(1,1,1);
ERROR: permission denied for relation t0
testdb=> update t0 set name=2;
ERROR: permission denied for relation t0
testdb=> select * from t0;
ERROR: permission denied for relation t0
testdb=> insert into t0(id) values(1);
INSERT 0 1
testdb=> update t0 set id=2;
UPDATE 1
testdb=> select id from t0;
id
----
  2
(1 row)
```
 
Use the superuser to connect to the `testdb` database, revoke all permissions of `user1`, and view the permission information:
```
[tdapg@VM-16-32-tlinux ~]$ psql -d testdb -U dbadmin -p 11347
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.


testdb=# revoke all(id) on t0 from user1;
REVOKE
```

Use the `user1` user to perform CRUD operations on the `t0` table, and the system prompts that the user has no permission, indicating that the permissions have been revoked successfully:
```
[tdapg@TENCENT64 ~]$ psql -d testdb -p 11347 -U user1
psql (PostgreSQL 10.0 TDSQL-A for PostgreSQL)
Type "help" for help.
 
testdb=> insert into t0 values(1,1,1);
ERROR: permission denied for relation t0
testdb=> update t0 set id=2;
ERROR: permission denied for relation t0
testdb=> select * from t0;
ERROR: permission denied for relation t0
testdb=> insert into t0(id) values(1);
ERROR: permission denied for relation t0
testdb=> select id from t0;
ERROR: permission denied for relation t0
```

## Account Security
### Account security policies
In TDSQL-A for PostgreSQL, the database admin (DBA) role in a traditional database system is divided into three independent roles: security admin, audit admin, and data admin, and the three roles are mutually restricted to eliminate super privileges in the system, solving data security problems from the aspect of system role design.

Responsibilities of security admin:
- This role defines security policies such as forced access, data masking, and encryption policies.
- This role defines security policies independently of the data admin.
- All admins must comply with the security policies.

Responsibilities of audit admin:
- This role can audit all operations.
- This role defines audit policies independently of the data admin.
- This role's operations are forcibly logged and cannot be changed.

Responsibilities of data admin:
- This role still has independent access control and OPS permissions.
- This role cannot interfere with the operations of security and audit admins.

### Account validity period
```
postgres=# create role user1 with login password 'user1@123' VALID UNTIL '2023-09-30 23:59:59'; 
CREATE ROLE
```
`VALID UNTIL '2023-09-30 23:59:59'` indicates the expiration timestamp of the user password, and `VALID UNTIL 'infinity'` makes the password permanently valid.

### Password security management
In TDSQL-A for PostgreSQL, passwords are always encrypted and stored in the system catalog. You can configure the encryption method through the `password_encryption` parameter.
```
postgres=# show password_encryption;
 password_encryption 
---------------------
 md5
(1 row)

postgres=# select passwd from pg_shadow where usename='user1';
        passwd         
-------------------------------------
 md57a215dcdf258f57c76edeec46243f85b
(1 row)
```

Set the expiration timestamp of a user password:
```
postgres=# alter role user1 with VALID UNTIL '2023-09-30 23:59:59';
ALTER ROLE 
postgres=# alter role user1 with VALID UNTIL 'infinity'; 
ALTER ROLE 
```
`VALID UNTIL '2023-09-30 23:59:59'` indicates the expiration timestamp of the user password, and `VALID UNTIL 'infinity'` makes the password permanently valid.
