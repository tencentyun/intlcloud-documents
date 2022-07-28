It defines a new schema.

## Synopsis
```sql
CREATE SCHEMA schema_name [AUTHORIZATION username] 
   [schema_element [ ... ]]
 
CREATE SCHEMA AUTHORIZATION rolename [schema_element [ ... ]]
```

## Description
`CREATE SCHEMA` enters a new schema into the current database. The schema name must be distinct from the name of any existing schema in the current database.

A schema is essentially a namespace: it contains named objects (tables, data types, functions, and operators) whose names may duplicate those of other objects existing in other schemas. Named objects are accessed either by qualifying their names with the schema name as a prefix, or by setting a search path that includes the desired schema(s). A `CREATE` command specifying an unqualified object name creates the object in the current schema (the one at the front of the search path, which can be determined with the function `current_schema`).

Optionally, `CREATE SCHEMA` can include subcommands to create objects within the new schema. The subcommands are treated essentially the same as separate commands issued after creating the schema, except that if the `AUTHORIZATION` clause is used, all the created objects will be owned by that role.

## Parameters
schema_name
The name of a schema to be created. If this is omitted, the user name is used as the schema name. The name cannot begin with `pg\_`, as such names are reserved for system catalog schemas.

rolename
The name of the role who will own the schema. If omitted, defaults to the role executing the command. Only superusers may create schemas owned by roles other than themselves.

schema_element
An SQL statement defining an object to be created within the schema. Currently, only `CREATE TABLE`, `CREATE VIEW`, `CREATE INDEX`, `CREATE SEQUENCE`, `CREATE TRIGGER`, and `GRANT` are accepted as clauses within `CREATE SCHEMA`. Other kinds of objects may be created in separate commands after the schema is created.

>!The database does not support triggers.

## Notes
To create a schema, the invoking user must have the `CREATE` privilege for the current database or be a superuser.

## Examples
Create a schema:
```sql
CREATE SCHEMA myschema;
```
Create a schema for role `joe` (the schema will also be named `joe`):
```sql
CREATE SCHEMA AUTHORIZATION joe;
```

## Compatibility
The SQL standard allows a `DEFAULT CHARACTER SET` clause in `CREATE SCHEMA`, as well as more subcommand types than are presently accepted by the database.

The SQL standard specifies that the subcommands in `CREATE SCHEMA` may appear in any order. The present database implementation does not handle all cases of forward references in subcommands; it may sometimes be necessary to reorder the subcommands in order to avoid forward references.

According to the SQL standard, the owner of a schema always owns all objects within it. The database allows schemas to contain objects owned by users other than the schema owner. This can happen only if the schema owner grants the `CREATE` privilege on the schema to someone else.

## See Also

ALTER SCHEMA, DROP SCHEMA

 
