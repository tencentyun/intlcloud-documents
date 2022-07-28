It commits the current transaction.

## Synopsis
```sql
END [WORK | TRANSACTION]
```

## Description
`END` commits the current transaction. All changes made by the transaction become visible to others and are guaranteed to be durable if a crash occurs. This command is a database extension that is equivalent to `COMMIT`.

## Parameters
WORK
TRANSACTION
Optional keywords. They have no effect.

## Examples
Commit the current transaction:
```sql
END;
```

## Compatibility
`END` is a database extension that provides functionality equivalent to `COMMIT`, which is specified in the SQL standard.

## See Also
BEGIN, ROLLBACK, COMMIT
