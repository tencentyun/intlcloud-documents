数据库提供的序列函数，返回多个值，具体见下面表格。

| 函数                         | 参数类型 | 返回类型 | 描述                                | 示例                                                     |
| ------------------------ | -------------- | ------------ | ------------------------------ | -------------------------------------------------- |
| generate_series(start, stop)       | 整数    | 返回一系列值  | 从 start 开始，自增到 stop 的一系列值     | select * from generate_series(2,4);<br>generate_series<br>-----------------<br> 2<br>3<br> 4<br>(3 rows) |
| generate_series(start, stop, step) | 整数     | 返回一系列值  | 从 start 开始，步长为 step 自增到 stop 的一系列值 | select * from generate_series(5,1,-2);<br> generate_series <br>-----------------<br> 5<br>3<br>1<br>(3 rows) |
