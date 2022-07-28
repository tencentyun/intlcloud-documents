The sequence functions provided by the database return multiple values as listed below.

| Function | Parameter Type | Return Type | Description | Example |
| ------------------------ | -------------- | ------------ | ------------------------------ | -------------------------------------------------- |
| generate_series(start, stop)       | Integer    | Returns a sequence of values  | A sequence of values starting from `start` and auto-incrementing to `stop`     | select * from generate_series(2,4);<br>generate_series<br>-----------------<br> 2<br>3<br> 4<br>(3 rows) |
| generate_series(start, stop, step) | Integer     | Returns a sequence of values  | A sequence of values starting from `start` and auto-incrementing to `stop` in increments of `step` | select * from generate_series(5,1,-2);<br> generate_series <br>-----------------<br> 5<br>3<br>1<br>(3 rows) |
