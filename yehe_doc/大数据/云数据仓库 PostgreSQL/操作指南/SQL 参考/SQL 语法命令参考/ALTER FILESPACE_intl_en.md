It changes the definition of a filespace.

## Synopsis
```sql
ALTER FILESPACE name RENAME TO newname
ALTER FILESPACE name OWNER TO newowner
```

## Description
`ALTER FILESPACE` changes the definition of a filespace. You must own the filespace to use `ALTER FILESPACE`. To alter the owner, you must also be a direct or indirect member of the new owning role (**note that superusers have these privileges automatically**).

## Parameters

| Parameter | Description | 
|---------|---------|
| name | The name of an existing filespace. | 
| newname | The new name of the filespace. The new name cannot begin with `pg\_` or `gp\_` (reserved for system filespaces). | 
| newowner | The new owner of the filespace. | 

## Examples
Rename filespace `myfs` to `fast_ssd`:
```sql
ALTER FILESPACE myfs RENAME TO fast_ssd;
```
Change the owner of tablespace `myfs`:
```sql
ALTER FILESPACE myfs OWNER TO dba;
```

## Compatibility
There is no `ALTER FILESPACE` statement in the SQL standard or in PostgreSQL.

## See Also
DROP FILESPACE
