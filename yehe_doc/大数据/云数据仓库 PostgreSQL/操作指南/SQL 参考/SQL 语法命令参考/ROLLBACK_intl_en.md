It aborts the current transaction.

## Synopsis
```sql
ROLLBACK [WORK | TRANSACTION]
```

## Description
`ROLLBACK` rolls back the current transaction and causes all the updates made by the transaction to be discarded.

## Parameters
WORK
TRANSACTION
Optional keywords. They have no effect.

## Notes
Use `COMMIT` to successfully end the current transaction. Issuing `ROLLBACK` when not inside a transaction does no harm, but it will provoke a warning message.

## Examples
To discard all changes made in the current transaction:
```sql
ROLLBACK;
```

## Compatibility
The SQL standard only specifies the two forms `ROLLBACK` and `ROLLBACK WORK`. Otherwise, this command is fully conforming.

## See Also
BEGIN, COMMIT, SAVEPOINT, ROLLBACK TO SAVEPOINT
