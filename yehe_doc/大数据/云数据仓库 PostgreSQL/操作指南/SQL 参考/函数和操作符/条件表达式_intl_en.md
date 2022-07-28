## CASE
The database supports the `CASE` expression, which is equivalent to `IF/ELSE` in other programming languages.

Example:
```sql
SELECT a,
       CASE WHEN a=1 THEN 'one'
            WHEN a=2 THEN 'two'
            ELSE 'other'
       END
    FROM test;
```

## COALESCE 
`COALESCE` returns the first non-null value in the parameters or returns `NULL` if all parameters are null.
```sql
SELECT COALESCE(null,1,2,null) ;       

 coalesce 

----------

       1
```

## NULLIF
`NULLIF(value1,value2)` returns `NULL` if `value1` and `value2` are equal or returns `value1` otherwise.

## GREATEST and LEAST
These two functions get the maximum or minimum value in a column of values, respectively. They return `NULL` if all parameters are absent (i.e., null).
