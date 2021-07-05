## CASE
The `CASE` expression is a generic conditional expression, similar to `if…else` statements in other programming languages:
```
CASE WHEN condition THEN result
   [WHEN ...]
   [ELSE result]
END
```
Or:
```
CASE expression
  WHEN value THEN result
  [WHEN ...]
  [ELSE result]
END
```

Sample code:
```
postgres=# CREATE TABLE test(a INT); 
NOTICE: Replica identity is needed for shard table, please add to this table through "alter table" command.
CREATE TABLE
postgres=# INSERT INTO test VALUES(1),(2),(3);
COPY 3
postgres=# SELECT * FROM test;
a 
---
 1
 3
 2
(3 rows)
 
postgres=# SELECT a,
postgres-#    CASE WHEN a=1 THEN 'one'
postgres-#       WHEN a=2 THEN 'two'
postgres-#       ELSE 'other'
postgres-#    END
postgres-#   FROM test;
 a | case 
---+-------
 1 | one
 3 | other
 2 | two
(3 rows) 

postgres=# SELECT a,
postgres-#    CASE a WHEN 1 THEN 'one'
postgres-#        WHEN 2 THEN 'two'
postgres-#        ELSE 'other'
postgres-#    END
postgres-#   FROM test;
 a | case 
---+-------
 1 | one
 3 | other
 2 | two
(3 rows)
```

## COALESCE
The `COALESCE` function returns the first of its arguments that is not null. Null is returned only if all arguments are null. It is often used to substitute a default value for null values when data is retrieved for display.
The syntax is as follows:
```
COALESCE(value [, ...])
```

Sample code:
```
postgres=# SELECT COALESCE(null,'a',null,'hello');
 coalesce 
----------
 a
(1 row)
```

## NULLIF
The syntax of `NULLIF` is as follows:
```
NULLIF(value1, value2)
```
The `NULLIF` function returns a null value if `value1` equals `value2`; otherwise, it returns `value1`.
Sample code:
```
postgres=# SELECT NULLIF('hello','hello');
 nullif 
--------
(1 row)
 
postgres=# SELECT NULLIF(null,'hello');
 nullif 
--------
(1 row)

postgres=# SELECT NULLIF('hello',null);
 nullif 
--------
 hello
(1 row)
```

## `GREATEST` and `LEAST`
The `GREATEST` and `LEAST` functions select the largest or smallest value from a list of any number of expressions. The syntax is as follows:
```
GREATEST(value [, ...])
LEAST(value [, ...])
```
Sample code:
```
postgres=# SELECT GREATEST(1,2,3,4,5);
 greatest 
----------
    5
(1 row)
 
postgres=# SELECT LEAST(1,2,3,4,5);
 least 
-------
   1
(1 row)
```
