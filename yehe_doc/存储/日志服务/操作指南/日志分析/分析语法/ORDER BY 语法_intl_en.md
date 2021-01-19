

The `ORDER BY` statement is used to sort results according to the specified `KEY`.
The `ORDER BY` statement sorts records in ascending order by default.
If you want to sort records in descending order, you can use the `DESC` keyword.

## ORDER BY Syntax Format

```sql
ORDER BY column (KEY) [ DESC | ASC ]
```

## ORDER BY Syntax Sample

Count different access status codes and sort them in descending order:

```sql
SELECT status, COUNT(status) AS c GROUP BY status ORDER BY c DESC
```
