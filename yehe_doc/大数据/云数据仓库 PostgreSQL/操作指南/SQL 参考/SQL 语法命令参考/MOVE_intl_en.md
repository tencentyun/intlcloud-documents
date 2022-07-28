It positions a cursor.

## Synopsis
```sql
MOVE [ forward_direction {FROM | IN} ] cursorname
```
where `forward_direction` can be empty or one of:
```sql
    NEXT
    FIRST
    LAST
    ABSOLUTE count
    RELATIVE count
    count
    ALL
    FORWARD
    FORWARD count
    FORWARD ALL
```

## Description
`MOVE` repositions a cursor without retrieving any data. `MOVE` works exactly like the `FETCH` command, except it only positions the cursor and does not return rows.
>!It is not possible to move a cursor position backwards in the database, since scrollable cursors are not supported. You can only move a cursor forward in position using `MOVE`.

**Outputs**
On successful completion, a `MOVE` command returns a command tag of the form:
```sql
MOVE count
```
The count is the number of rows that a `FETCH` command with the same parameters would have returned (possibly zero).

## Parameters
forward_direction
See `FETCH` for more information.

cursorname
The name of an open cursor.

## Examples
Start the transaction:
```sql
BEGIN;
```
Set up a cursor:
```sql
DECLARE mycursor CURSOR FOR SELECT * FROM films;
```
Move forward 5 rows in the cursor `mycursor`:
```sql
MOVE FORWARD 5 IN mycursor;
MOVE 5
```
Fetch the next row after that (row 6):
```sql
FETCH 1 FROM mycursor;
 code  | title  | did | date_prod  |  kind  |  len
-------+--------+-----+------------+--------+-------
 P_303 | 48 Hrs | 103 | 1982-10-22 | Action | 01:37
(1 row)
```
Close the cursor and end the transaction:
```sql
CLOSE mycursor;
COMMIT;
```

## Compatibility
There is no `MOVE` statement in the SQL standard.

## See Also
DECLARE, FETCH, CLOSE
