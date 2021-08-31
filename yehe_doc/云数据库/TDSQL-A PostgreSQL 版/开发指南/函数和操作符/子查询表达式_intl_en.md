## EXISTS
`EXISTS` syntax format:
```
EXISTS (subquery)
```
Its argument is an arbitrary `SELECT` statement or subquery. The subquery is evaluated to determine whether it returns any rows.
- If it returns at least one row, the result of `EXISTS` is "true".
- If the subquery returns no rows, the result of `EXISTS` is "false".

Sample code:
```
postgres=# SELECT EXISTS(SELECT 1<0);
 exists 
--------
 t
(1 row)
 
postgres=# SELECT EXISTS(SELECT 1 where 1<0);
 exists 
--------
 f
(1 row)
```

## IN
`IN` syntax format:
```
expression IN (subquery)
```
The right-hand side is a parenthesized subquery, which must return exactly one column. The left-hand expression is evaluated and compared to each row of the subquery result. 
- The result of `IN` is "true" if any equal subquery row is found.
- The result is "false" if no equal row is found (including the case where the subquery returns no rows).

Sample code:
```
postgres=# SELECT (1>0) IN('true','false');
 ?column? 
----------
 t
(1 row)
 
postgres=# SELECT (2+3) IN(3,4);
 ?column? 
----------
 f
(1 row)
```

## NOT IN
`NOT IN` syntax format:
```
expression NOT IN (subquery)
```
The right-hand side is a parenthesized subquery, which must return exactly one column. The left-hand expression is evaluated and compared to each row of the subquery result. 
- The result of `NOT IN` is "true" if only unequal subquery rows are found (including the case where the subquery returns no rows).
- The result is "false" if any equal row is found.

Sample code:
```
postgres=# SELECT (1>0) NOT IN('true','false');
 ?column? 
----------
 f
(1 row)

postgres=# SELECT (2+3) NOT IN(3,4);
 ?column? 
----------
 t
(1 row)
```

## ANY/SOME
Syntax format:
```
expression operator ANY (subquery)
expression operator SOME (subquery)
```
The right-hand side is a parenthesized subquery, which must return exactly one column. The left-hand expression is evaluated and compared to each row of the subquery result by using the given operator, which must yield a Boolean result.
- The result of `ANY` is "true" if any true result is obtained.
- The result is "false" if no true result is found (including the case where the subquery returns no rows).
`SOME` is a synonym for `ANY`. `IN` is equivalent to `= ANY`.

Sample code:
```
postgres=# CREATE TABLE any_test(a int);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO any_test VALUES(1),(2),(3),(4),(5);
COPY 5
postgres=# SELECT * FROM any_test where a < ANY(SELECT AVG(a) FROM any_test);
 a 
---
 1
 2
(2 rows)
```

## ALL
`ALL` syntax format:
```
expression operator ALL (subquery)
```
The right-hand side of `ALL` is a parenthesized subquery, which must return exactly one column. The left-hand expression is evaluated and compared to each row of the subquery result by using the given operator, which must yield a Boolean result.
- The result of `ALL` is "true" if all rows yield true (including the case where the subquery returns no rows).
- The result is "false" if any false result is found.
- The result is "NULL" if no comparison with a subquery row returns false, and at least one comparison returns NULL.
`NOT IN` is equivalent to `<> ALL`.

Sample code:
```
postgres=# CREATE TABLE all_test(a INT);
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO all_test VALUES(1),(2),(3),(4),(5);
COPY 5
postgres=# SELECT * FROM all_test WHERE a < ALL(SELECT * FROM all_test);
 a 
---
(0 rows)

postgres=# SELECT * FROM all_test WHERE 6 > ALL(SELECT * FROM all_test) order by 1;
 a 
---
 1
 2
 3
 4
 5
(5 rows)
```
