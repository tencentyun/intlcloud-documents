It changes the definition of a database role (user).

## Synopsis
```sql
ALTER USER name RENAME TO newname
ALTER USER name SET config_parameter {TO | =} {value | DEFAULT}
ALTER USER name RESET config_parameter
ALTER USER name [ [WITH] option [ ... ] ]
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
```

## Description
`ALTER USER` is a deprecated command but is still accepted for historical reasons. It is an alias for `ALTER ROLE`. See `ALTER ROLE` for more information.

## Compatibility
The `ALTER USER` statement is a database extension. The SQL standard leaves the definition of users to the implementation.

## See Also
ALTER ROLE
