It aborts the current transaction.

## Synopsis
```sql
ABORT [WORK | TRANSACTION]
```

## Description
`ABORT` rolls back the current transaction and causes all the updates made by the transaction to be discarded. This command is identical in behavior to the standard SQL command `ROLLBACK`, and is present only for historical reasons.

## Parameters
WORK
TRANSACTION
Optional keywords. They have no effect.

## Notes
Use `COMMIT` to successfully terminate a transaction.

Issuing `ABORT` when not inside a transaction does no harm, but it will provoke a warning message.

## Examples

```sql
-- Create the table `table1`.
 
CREATE TABLE table1
(
    a1                      INTEGER               NOT NULL,
    b1                             CHAR(10)                      ,
    c1                           INTEGER                       
)
WITH (
        APPENDONLY = TRUE,
    ORIENTATION = COLUMN,
    COMPRESSTYPE = ZLIB
)
DISTRIBUTED BY (a1);
 
-- Inset a record.
INSERT INTO table1 VALUES(20190117,'test', 11);
 
-- Query the data.
select * from table1;
    a1    |     b1     | c1 
----------+------------+----
 20190117 | test       | 11
(1 row)
 
Time: 16.718 ms
 
-- Start a transaction (equivalent to `START TRANSACTION`).
BEGIN;
 
-- Update a field value.
 
UPDATE table1 SET b1= 'yes';
UPDATE 1
Time: 13.510 ms
 
-- Query the data. You can see that the data has been updated in this transaction.
select * from table1;
    a1    |     b1     | c1 
----------+------------+----
 20190117 | yes        | 11
(1 row)
 
Time: 6.378 ms
 
-- Terminate the transaction, so the update performed above will be undone (equivalent to `ROLLBACK`).
ABORT; 
ROLLBACK
Time: 0.651 ms
 
-- Query the data, which is rolled back.
select * from table1;
    a1    |     b1     | c1 
----------+------------+----
 20190117 | test       | 11
(1 row)
 
Time: 6.124 ms
```

## Compatibility
This command is a database extension present for historical reasons. `ROLLBACK` is the equivalent standard SQL command.

## See Also
BEGIN, COMMIT, ROLLBACK
