It changes the definition of a view.

## Synopsis
```sql
ALTER VIEW name RENAME TO newname
```

## Description
`ALTER VIEW` changes the definition of a view. The only currently available functionality is to rename the view. To execute this command you must be the owner of the view.

## Parameters
name
The (optionally schema-qualified) name of an existing filespace.

newname
The new name of the view.

## Notes
Some variants of `ALTER TABLE` can be used with views as well; for example, to rename a view, it is also possible to use `ALTER TABLE RENAME`. To change the schema or owner of a view, you currently must use `ALTER TABLE`.

## Examples
Rename the view `myview` to `newview`:
```sql
ALTER VIEW myview RENAME TO newview;
```
Change the owner of tablespace `myfs`:
```sql
ALTER FILESPACE myfs OWNER TO dba;
```

## Compatibility
ALTER VIEW is a database extension of the SQL standard.

## See Also
CREATE VIEW, DROP VIEW
