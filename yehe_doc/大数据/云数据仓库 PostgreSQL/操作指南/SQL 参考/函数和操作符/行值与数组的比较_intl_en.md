| Operator | Description | Example | Result |
| -------- | ------------------------------------------------- | ---------------------------------------------- | --------------------- |
| IN       | Equivalent to `IN` for subquery                                  | select * from t1 where a1 in (2,5,6);        | a1 <br>----<br>2<br>(1 row)     |
| NOT IN   | Equivalent to `NOT IN` for subquery                              | select * from t1 where a1 not in (2,5,6);    | a1 <br>----<br>1<br>3<br>(2 rows) |
| ANY/SOME | Returns `TRUE` if at least one comparison result is `TRUE` or returns `FALSE` otherwise | select * from t1 where a1 < any(array[1,3]);   | a1 <br>----<br> 2<br> 1<br>(2 rows) |
| ALL      | Returns `TRUE` if all comparison results are `TRUE` or returns `FALSE` otherwise       | select * from t1 where a1 < ALL(array[3]);   | a1 <br>----<br>2<br>1<br>(2 rows) |
