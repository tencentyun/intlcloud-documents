
## Account Privilege System
PostgreSQL adopts a role-based access control (RBAC) model to manage users, roles, and privileges.

In PostgreSQL, the concepts of users and roles are almost the same. The only difference is that a user has the login privilege, while a role has the nologin privilege.

PostgreSQL supports system privileges and database object privileges, and manages them using the concept of roles. Both categories of the privileges can be granted to a role, and this role can grant its own privileges to other roles or users.
You can grant system or object privileges to roles/users to manage databases.

## System Privileges
System privileges are used to perform database operations. PostgreSQL manages system privileges using role attributes and default roles.

### Role attributes
You can specify attributes when creating a role with CREATE ROLE, or modify them after creation with ALTER ROLE. Role attributes are stored in the pg_authid system table.
CREATE ROLE syntax:
```
CREATE ROLE name [ [ WITH ] option [ ... ] ]
where option can be:
      SUPERUSER | NOSUPERUSER
    | CREATEDB | NOCREATEDB
    | CREATEROLE | NOCREATEROLE
    | INHERIT | NOINHERIT
    | LOGIN | NOLOGIN
    | REPLICATION | NOREPLICATION
    | BYPASSRLS | NOBYPASSRLS
    | CONNECTION LIMIT connlimit
    | [ ENCRYPTED ] PASSWORD 'password' | PASSWORD NULL
    | VALID UNTIL 'timestamp'
    | IN ROLE role_name [, ...]
    | IN GROUP role_name [, ...]
    | ROLE role_name [, ...]
    | ADMIN role_name [, ...]
    | USER role_name [, ...]
    | SYSID uid
```
A role with the superuser attribute can bypass all privilege checks and perform all database operations, because a superuser has the highest privilege in the database, which is similar to the root privilege in Linux.

>! TencentDB for PostgreSQL has disabled the superuser privilege due to security requirements. However, some operations must be performed by a superuser, so TencentDB for PostgreSQL provides the tencentdb_superuser role. For details, see [Users, Privileges, and Operations](https://intl.cloud.tencent.com/document/product/409/43242).

### Default roles
PostgreSQL provides a set of default roles which provide access to certain, commonly needed, privileged capabilities and information. Administrators can grant these roles to users and/or other roles in their environment, providing those users with access to the specified capabilities and information. The following table lists the [default roles](https://www.postgresql.org/docs/11/default-roles.html) supported in PostgreSQL 11.

| Role                      | Allowed Access                                                   |
| ------------------------- | ------------------------------------------------------------ |
| pg_execute_server_program | Allow executing programs on the database server as the user the database runs as with COPY and other functions which allow executing a server-side program. |
| pg_monitor                |   Read/Execute various monitoring views and functions. This role is a member of pg_read_all_settings, pg_read_all_stats, and pg_stat_scan_tables. |
| pg_read_all_settings      | Read all configuration variables, even those normally visible only to superusers.          |
| pg_read_all_stats         | Read all pg_stat\_\* views and use various statistics related extensions, even those normally visible only to superusers. |
| pg_read_server_files      | Allow reading files from any location the database can access on the server with COPY and other file-access functions. |
| pg_signal_backend         | Signal another backend to cancel a query or terminate its session.              |
| pg_stat_scan_tables       | Execute monitoring functions that may take ACCESS SHARE locks on tables, potentially for a long time.     |
| pg_write_server_files     | Allow writing to files in any location the database can access on the server with COPY and other file-access functions. |
| public                    | An implicitly defined group that always includes all roles. Any particular role will have the sum of privileges granted directly to public. PostgreSQL grants default privileges on some types of objects to public. |

## Database Object Privileges
PostgreSQL uses an access control list (ACL) to manage database object privileges. The following table lists all database object privileges in PostgreSQL and their abbreviations.

| Privilege       | Abbreviation         | Supported Object                                                   |
| ---------- | ------------ | ------------------------------------------------------------ |
| SELECT     | r ("read")   | LARGE OBJECT, SEQUENCE, TABLE (and table-like objects), table column |
| INSERT     | a ("append") | TABLE, table column                                          |
| UPDATE     | w ("write")  | LARGE OBJECT, SEQUENCE, TABLE, table column                  |
| DELETE     | d            | TABLE                                                        |
| TRUNCATE   | D            | TABLE                                                        |
| REFERENCES | x            | TABLE, table column                                          |
| TRIGGER    | t            | TABLE                                                        |
| CREATE     | C            | DATABASE, SCHEMA, TABLESPACE                                 |
| CONNECT    | c            | DATABASE                                                     |
| TEMPORARY  | T            | DATABASE                                                     |
| EXECUTE    | X            | FUNCTION, PROCEDURE                                          |
| USAGE      | U            | DOMAIN, FOREIGN DATA WRAPPER, FOREIGN SERVER, LANGUAGE, SCHEMA, SEQUENCE, TYPE |

The following table lists the privileges owned by a type of objects and the psql command to query the privileges:

| Object Type                       | Privileges | Privileges of the Default Role public | psql Command to Query Privileges |
| :----------------------------- | :------- | :------------------- | :----------------- |
| DATABASE                       | CTc      | Tc                   | \l                 |
| DOMAIN                         | U        | U                    | \dD+               |
| FUNCTION or PROCEDURE          | X        | X                    | \df+               |
| FOREIGN DATA WRAPPER           | U        | none                 | \dew+              |
| FOREIGN SERVER                 | U        | none                 | \des+              |
| LANGUAGE                       | U        | U                    | \dL+               |
| LARGE OBJECT                   | rw       | none                 |      -              |
| SCHEMA                         | UC       | none                 | \dn+               |
| SEQUENCE                       | rwU      | none                 | \dp                |
| TABLE (and table-like objects) | arwdDxt  | none                 | \dp                |
| Table column                   | arwx     | none                 | \dp                |
| TABLESPACE                     | C        | none                 | \db+               |
| TYPE                           | U        | U                    | \dT+               |

In PostgreSQL, the privileges granted for a particular object are displayed as a list of aclitem entries. The aclitem list of database and schema privileges is stored in pg_database.datacl and pg_namespace.nspacl, that of privileges for tables, views, and other objects stored in pg_class.relacl, and that of column privileges stored in pg_attribute.attacl.

For example, "normal_user=a\*r/test1" specifies that the user normal_user has the privilege INSERT with grant option (which gives the user the right to grant the privilege to others) and the privilege SELECT, both granted by test1.

```
postgres=# \dp
                            Access privileges
 Schema | Name | Type  | Access privileges | Column privileges | Policies
--------+------+-------+-------------------+-------------------+----------
 public | t1   | table | test1=arwdDxt/test1 |                   |
(1 rows)
postgres=# grant select on t1 to normal_user;
GRANT
postgres=# grant insert on t1 to normal_user with grant option;
GRANT
postgres=# grant update on t1 to public;
GRANT
postgres=# grant select (a) on t1 to test2;
GRANT
postgres=# \dp
                              Access privileges
 Schema | Name | Type  |  Access privileges    | Column privileges | Policies
--------+------+-------+-----------------------+-------------------+----------
 public | t1   | table | test1=arwdDxt/test1  +| a:               +|
        |      |       | normal_user=a*r/test1+|   test2=r/test1   |
        |      |       | =w/test1              |                   |
(1 rows)
-- Where, "=w/test1" specifies that test1 grants public the UPDATE privilege.
```


