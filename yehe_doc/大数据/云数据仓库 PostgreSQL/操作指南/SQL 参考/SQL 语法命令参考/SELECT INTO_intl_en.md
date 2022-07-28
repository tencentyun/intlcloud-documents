It defines a new table from the results of a query.

## Synopsis
```sql
[ WITH with_query [, ...] ]
SELECT [ALL | DISTINCT [ON ( expression [, ...] )]]
    * | expression [AS output_name] [, ...]
    INTO [TEMPORARY | TEMP] [TABLE] new_table
    [FROM from_item [, ...]]
    [WHERE condition]
    [GROUP BY expression [, ...]]
    [HAVING condition [, ...]]
    [{UNION | INTERSECT | EXCEPT} [ALL] select]
    [ORDER BY expression [ASC | DESC | USING operator] [NULLS {FIRST | LAST}] [, ...]]
    [LIMIT {count | ALL}]
    [OFFSET start]
    [FOR {UPDATE | SHARE} [OF table_name [, ...]] [NOWAIT] 
    [...]]
```

## Description
`SELECT INTO` creates a new table and fills it with data computed by a query. The data is not returned to the client, as it is with a normal `SELECT`. The new table's columns have the names and data types associated with the output columns of the `SELECT`.

## Parameters
The main parameters of `SELECT INTO` are the same as those of **SELECT**.

TEMPORARY
TEMP
If specified, the table is created as a temporary table.

new_table
The name (optionally schema-qualified) of the table to be created.

## Examples
Create a new table `films_recent` consisting of only recent entries from the table `films`:
```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= 
'2016-01-01';
```

## Compatibility
The SQL standard uses `SELECT INTO` to represent selecting values into scalar variables of a host program, rather than creating a new table. The PostgreSQL usage of SELECT INTO to represent table creation is historical. It is best to use `CREATE TABLE AS` for this purpose in new code.

## See Also
SELECT, CREATE TABLE AS
