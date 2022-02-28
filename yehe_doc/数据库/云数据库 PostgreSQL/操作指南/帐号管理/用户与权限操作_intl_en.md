## TencentDB Default Role
TencentDB for PostgreSQL does not open the `superuser` role attribute and the `pg_execute_server_program`, `pg_read_server_files`, and `pg_write_server_files` roles for you to use. However, as some operations require the `superuser` role, TencentDB for PostgreSQL provides the `pg_tencentdb_superuser` to replace `superuser`.

## pg_tencentdb_superuser Role
This role supports system permissions and database object permissions, as listed in the following tables.

#### System permissions
| Permission        | Description                                                         |
| ----------- | ------------------------------------------------------------ |
| CREATEDB    | Create a database.                                       |
| BYPASSRLS   | Bypass all row-level security policy checks.                                |
| REPLICATION | Have the REPLICATION permission by default, and allow granting the REPLICATION permission to other users.   |
| CREATEROLE | Have the same CREATEROLE permission as the community edition, except that the role cannot create the pg_read_server_files, pg_write_server_files, and pg_execute_server_program roles.   |

#### Object permissions
| Object                 | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| database             | By default, have the permissions of all databases not owned by a  a superuser.               |
| schema               | By default, have the permissions of all schemas not owned by a superuser.               |
| table/sequence    | By default, have the permissions of all tables/sequences not owned by a  a superuser.       |
| function               | By default, have the permissions of all functions not owned by a superuser.             |
| language             | No permissions.                                                     |
| tablespace           | No permissions.                                                     |
| FDW/foreign server | By default, have the permissions of all FDWs/foreign servers not owned by a  a superuser. |
| TYPE                       | By default, have the permissions of all TYPEs not owned by a superuser.                 |

#### Other operations
- Pub/Sub: the tencentdb_superuser role can implement the pub/sub messaging paradigm, create a publication for all tables, and create slots.
- Extensions: the tencentdb_superuser role can create all supported extensions. When creating an extension, the `pg_tencentdb_superuser` is temporarily escalated to superuser and passes all permission checks. 
- The load_file permission only allows loading supported extension libraries.
- The tencentdb_superuser role can use the `pgstat_get_backend_current_activity` function to view deadlock details, so that users can easily troubleshoot deadlocks themselves.
- The use of the `pg_signal_backend` function is restricted, and processes of the `pg_tencentdb_superuser` role can only be killed by itself.

## Permission Operations
For more information, see the official documents in the PostgreSQL community:
- [Create a user](https://www.postgresql.org/docs/13/sql-createuser.html):
```
CREATE USER name [ [ WITH ] option [ ... ] ]

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

- [Create a role](https://www.postgresql.org/docs/13/sql-createrole.html):
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

- [Modify a role attribute](https://www.postgresql.org/docs/13/sql-alterrole.html):
```
ALTER ROLE role_specification [ WITH ] option [ ... ]

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
```

- [Grant an object privilege to a role](https://www.postgresql.org/docs/13/sql-grant.html):
```
# Syntax example
GRANT <privilege> on <object> to <role>;
```

- [Revoke an object privilege from a role](https://www.postgresql.org/docs/current/sql-revoke.html):
```
# Syntax example
REVOKE <privilege> ON <object> FROM <role>;
```

- Grant a role to another role:
```
# Syntax example
GRANT <role name> to <another role>;
```

