It commits the current transaction.

## Synopsis
```sql
COMMIT [WORK | TRANSACTION]
```

## Description
`COMMIT` commits the current transaction. All changes made by the transaction become visible to others and are guaranteed to be durable if a crash occurs.

## Parameters
WORK
TRANSACTION
Optional keywords. They have no effect.

## Notes
Use `ROLLBACK` to abort a transaction.
Issuing `COMMIT` when not inside a transaction does no harm, but it will provoke a warning message.

## Examples
To commit the current transaction and make all changes permanent:
```sql
COMMIT;
```

## Compatibility
The SQL standard only specifies the two forms `COMMIT` and `COMMIT WORK`. Otherwise, this command is fully conforming.

## See Also
BEGIN, END, START TRANSACTION, ROLLBACK
