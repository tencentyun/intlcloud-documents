## TencentDB Default Role
TencentDB for PostgreSQL has disabled the superuser attribute and some special default roles due to security requirements. However, some operations must be performed by a superuser, so TencentDB for PostgreSQL provides the tencentdb_superuser role.
The administrator role you specify when creating an instance is a tencentdb_superuser.

## tencentdb_superuser
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
| database             | By default, have the permissions of all databases whose owner is not a superuser.               |
| schema               | By default, have the permissions of all schemas whose owner is not a superuser.               |
| table/sequence    | By default, have the permissions of all tables/sequences whose owner is not a superuser.       |
| function               | By default, have the permissions of all functions whose owner is not a superuser.             |
| language             | No permissions.                                                     |
| tablespace           | No permissions.                                                     |
| FDW/foreign server | By default, have the permissions of all FDWs/foreign servers whose owner is not a superuser. |
| TYPE                       | By default, have the permissions of all TYPEs whose owner is not a superuser.                 |

#### Other operations
- Pub/Sub: the tencentdb_superuser role can implement the pub/sub messaging paradigm, create a publication for all tables, and create slots.
- Extensions: the tencentdb_superuser role can create all supported extensions. When creating an extension, the tencentdb_superuser is temporarily escalated to superuser and passes all permission checks. 
- The load_file permission only allows loading supported extension libraries.
- The tencentdb_superuser role can use the `pgstat_get_backend_current_activity` function to view deadlock details, so that users can easily troubleshoot deadlocks themselves.
- The use of the `pg_signal_backend` function is restricted, and processes of the tencentdb_superuser role can only be killed by itself.

## Permission Operations
For more information, please see the official documents in the PostgreSQL community:
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

