It defines a new database role with the `LOGIN` privilege by default.

## Synopsis
```sql
CREATE USER name [ [WITH] option [ ... ] ]
```
where `option` can be:
```sql
      SUPERUSER | NOSUPERUSER
    | CREATEDB | NOCREATEDB
    | CREATEROLE | NOCREATEROLE
    | CREATEUSER | NOCREATEUSER
    | INHERIT | NOINHERIT
    | LOGIN | NOLOGIN
    | [ ENCRYPTED | UNENCRYPTED ] PASSWORD 'password'
    | VALID UNTIL 'timestamp' 
    | IN ROLE rolename [, ...]
    | IN GROUP rolename [, ...]
    | ROLE rolename [, ...]
    | ADMIN rolename [, ...]
    | USER rolename [, ...]
    | SYSID uid    | RESOURCE QUEUE queue_name
```

## Description
As of the database's 2.2 release, `CREATE USER` has been replaced by **`CREATE ROLE`**, although it is still accepted as practical for backward compatibility.

The only difference between `CREATE ROLE` and `CREATE USER` is that `LOGIN` is assumed by default with `CREATE USER`, whereas `NOLOGIN` is assumed by default with `CREATE ROLE`.

## Compatibility
There is no `CREATE USER` statement in the SQL standard.

## See Also
CREATE ROLE
