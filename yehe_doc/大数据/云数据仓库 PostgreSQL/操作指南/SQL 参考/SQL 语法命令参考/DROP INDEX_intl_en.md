It removes an index.

## Synopsis
```sql
DROP INDEX [IF EXISTS] name [, ...] [CASCADE | RESTRICT]
```

## Description
`DROP INDEX` drops an existing index from the database system. To execute this command you must be the owner of the index.

## Parameters
IF EXISTS
Do not throw an error if the index does not exist. A notice is issued in this case.

name
The name (optionally schema-qualified) of an existing index.

CASCADE
Automatically drop objects that depend on the index.

RESTRICT
Refuse to drop the index if any objects depend on it. This is the default.

## Examples
Remove the index `title_idx`:
```sql
DROP INDEX title_idx;
```

## Compatibility
`DROP INDEX` is a database language extension. There are no provisions for indexes in the SQL standard.

## See Also
ALTER INDEX, CREATE INDEX, REINDEX
