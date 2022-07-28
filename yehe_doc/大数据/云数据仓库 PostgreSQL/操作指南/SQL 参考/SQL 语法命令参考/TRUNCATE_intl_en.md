It empties a table.

## Synopsis
```sql
TRUNCATE [TABLE] name [, ...] [CASCADE | RESTRICT]
```

## Description
`TRUNCATE` quickly removes all rows from a table or set of tables. It has the same effect as an unqualified `DELETE` on each table, but since it does not actually scan the tables it is faster. This is most useful on large tables.

You must have the `TRUNCATE` privilege on the table to truncate table rows.

## Parameters
name
The name (optionally schema-qualified) of a table to truncate.

CASCADE
Because this keyword applies to foreign key references (which are not supported in the database) it has no effect.

RESTRICT
Because this keyword applies to foreign key references (which are not supported in the database) it has no effect.

## Notes
`TRUNCATE` will not run any user-defined `ON DELETE` triggers that might exist for the tables. `TRUNCATE` will not truncate any tables that inherit from the named table. Only the named table is truncated, not its child tables. `TRUNCATE` will not truncate any subtables of a partitioned table. If you specify a subtable of a partitioned table, `TRUNCATE` will not remove rows from the subtable and its child tables.

## Examples
Empty the tables `films`:
```sql
TRUNCATE films;
```

## Compatibility
There is no `TRUNCATE` statement in the SQL standard.

## See Also
DELETE, DROP TABLE
