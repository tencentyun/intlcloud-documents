The database supports subquery expressions. The subqueries listed below return `TRUE/FALSE`.

The data in the original table t1 is as follows:
```sql
select * from t1;
 a1 
----
  1
  3
  2
```

## EXISTS/NOT EXISTS
The parameter of `EXISTS` is an arbitrary `SELECT` statement, or subquery. The subquery is evaluated to determine whether it returns any rows. If it returns at least one row, the result of `EXISTS` is `TRUE`; otherwise, the result is `FALSE`.

This subquery will generally only be executed long enough to determine whether at least one row is returned, not all the way to completion. The content of the result returned by the subquery is unimportant, so it is generally better to write `...WHERE EXISTS(SELECT 1 FROM ...) `.

| Example | Result |
| ------------------------------------------------------------ | ---------------------------- |
| select   a1 from t1 where EXISTS(select a1 from t1 where a1>2); | a1    ----     2     1     3 |
| select   a1 from t1 where EXISTS(select a1 from t1 where a1>3); | a1    ----                   |
| select   a1 from t1 where EXISTS(select a1 from t1 where a1>1) and a1>2; | a1    ----     3             |

## IN/NOT IN
The right-hand side of the expression `IN` (subquery) is a parenthesized subquery, which must return exactly one field. The left-hand expression is evaluated and compared to each row of the subquery result. The result of `IN` is `TRUE` if any equal subquery row is found. The result is `FALSE` if no equal row is found (including the case where the subquery returns no rows).

Null values in the expression or rows are combined per the normal rules of SQL Boolean expressions. Two rows are considered equal if all their corresponding members are non-null and equal; they are unequal if any corresponding members are non-null and unequal; otherwise, the result of the row comparison is unknown (null). If all the per-row results are either unequal or null, with at least one null, then the result of `IN` is `NULL`.

Note that `FALSE` is directly returned if the subquery of `NOT IN` has a null value.

| Example | Result |
| ----------------------------------------------------- | ------------------------- |
| select   * from t1 where a1 in (select a1 from t1 where a1 > 2); | a1    ----     3   (1 row) |
| select   * from t1 where a1 in (4,5,6);                      | a1    ----   (0   rows)    |
| select   * from t1 where a1 in (2,5,6);                      | a1    ----     2   (1 row) |

## ANY/SOME
The right-hand side of the expression operator `SOME/ANY` (subquery) is a parenthesized subquery, which must return exactly one field. The left-hand expression is evaluated and compared to each row of the subquery result by using the given operator, which must yield a Boolean result. The result of `ANY` is `TRUE` if any true result is obtained. The result is `FALSE` if no true result is found (including the case where the subquery returns no rows). `SOME` is similar to `ANY`. `IN` is equivalent to `ANY`.

Like `EXISTS`, this subquery will generally only be executed long enough to determine whether the result is `TRUE`, not all the way to completion.

| Example | Result |
| ----------------------------------------------------- | -------------------------------- |
| `select * from t1 where a1 < any(select a1 from t1 where a1 <3);` | a1    ----     1   (1 row)          |
| `select * from t1 where a1 < some(select a1 from t1 where a1 <4);` | a1    ----     1     2   (2   rows) |
| `select * from t1 where a1 < any(select a1 from t1 where a1 <1);` | a1    ----   (0   rows)             |

## ALL
The right-hand side of the expression operator `ALL` (subquery) is a parenthesized subquery, which must return exactly one field. The left-hand expression is evaluated and compared to each row of the subquery result by using the given operator, which must yield a Boolean result. The result of ALL is `TRUE` if all rows yield true (including the case where the subquery returns no rows). The result is `FALSE` if any false result is found.

`NOT IN` is equivalent to `ALL`.

Like `EXISTS`, this subquery will generally only be executed long enough to determine whether the result is `FALSE`, not all the way to completion.

`TRUE` is directly returned if the subquery result is null.

| Example | Result |
| ------------------------------------------------------------ | ----------------------------------------- |
| `select   * from t1 where a1 < all(select a1 from t1 where a1 <1); `| a1    ----     1     3     2   (3   rows) |
| `select   * from t1 where a1 < all(select a1 from t1 where a1 >2);` | a1    ----     2     1   (2   rows)       |
