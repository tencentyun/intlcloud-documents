| 操作符   | 功能描述                                          | 示例                                           | 结果                  |
| -------- | ------------------------------------------------- | ---------------------------------------------- | --------------------- |
| IN       | 与子查询的 IN 一致                                  | select * from t1 where a1 in (2,5,6);        | a1 <br>----<br>2<br>(1 row)     |
| NOT IN   | 与子查询的 NOT IN 一致                              | select * from t1 where a1 not in (2,5,6);    | a1 <br>----<br>1<br>3<br>(2 rows) |
| ANY/SOME | 对比结果至少有一个真值，则返回 TRUE，否则返回 FALSE | select * from t1 where a1 < any(array[1,3]);   | a1 <br>----<br> 2<br> 1<br>(2 rows) |
| ALL      | 对比结果都为 TRUE，则返回 TRUE，否则返回 FALSE       | select * from t1 where a1 < ALL(array[3]);   | a1 <br>----<br>2<br>1<br>(2 rows) |
