It defines a new savepoint within the current transaction.

## Synopsis
```sql
SAVEPOINT savepoint_name
```

## Description
`SAVEPOINT` establishes a new savepoint within the current transaction. A savepoint is a special mark inside a transaction that allows all commands that are executed after it was established to be rolled back, restoring the transaction state to what it was at the time of the savepoint.

## Parameters
savepoint_name: The name to give to the new savepoint.

## Notes
Use **ROLLBACK TO SAVEPOINT** to rollback to a savepoint. 
Use **RELEASE SAVEPOINT** to destroy a savepoint, keeping the effects of commands executed after it was established.

Savepoints can only be established when inside a transaction block. There can be multiple savepoints defined within a transaction.

## Examples
To establish a savepoint and later undo the effects of all commands executed after it was established:
```sql
BEGIN;
    INSERT INTO table1 VALUES (1);
    SAVEPOINT my_savepoint;
    INSERT INTO table1 VALUES (2);
    ROLLBACK TO SAVEPOINT my_savepoint;
    INSERT INTO table1 VALUES (3);
COMMIT;
```
The above transaction will insert the values 1 and 3, but not 2. To establish and later destroy a savepoint:
```sql
BEGIN;
    INSERT INTO table1 VALUES (3);
    SAVEPOINT my_savepoint;
    INSERT INTO table1 VALUES (4);
    RELEASE SAVEPOINT my_savepoint;
COMMIT;
```
The above transaction will insert both 3 and 4.

## Compatibility
SQL requires a savepoint to be destroyed automatically when another savepoint with the same name is established. In the database, the old savepoint is kept, though only the more recent one will be used when rolling back or releasing. (Releasing the newer savepoint will cause the older one to again become accessible to `ROLLBACK TO SAVEPOINT` and `RELEASE SAVEPOINT`.) Otherwise, SAVEPOINT is fully SQL conforming.

## See Also
BEGIN, COMMIT, ROLLBACK, RELEASE SAVEPOINT, ROLLBACK TO SAVEPOINT
