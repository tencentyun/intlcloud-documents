数据库的聚合函数对一些列的值进行计算得到一个返回值，下列表格中是一些内置聚合函数。

| 函数                 | 参数类型                                                     | 返回值类型 | 描述                                            |
| -------------------- | ------------------------------------------------------ | ---------- | ----------------------------------------------- |
| avg(expression)      | 所有数字类型                                                 | 数值类型   | 平均值                                          |
| bit_and(expression)  | smallint, int, bigint, bit                                   | 与参数一致 | 所有非空值的位与                                |
| bit_or(expression)   | smallint, int, bigint,   bit                                 | 与参数一致 | 所有非空值的位或                                |
| bool_and(expression) | bool                                                         | bool       |   所有值为 true，则返回 true，否则返回 false         |
| bool_or(expression)  | bool                                                         | bool       | 存在至少一个值为 true，则返回 true，否则返回 false |
| count(\*)             |      -                                                        | bigint     | 返回行数                                        |
| count(expression)    | any                                                          | bigint     | 返回表达式值为非 null 的所有总和               |
| every(expression)    | bool                                                         | bool       | 与 bool_and 一致                                  |
| max(expression)      | array,numeric,string,   date/time type                       | 与参数一致 | 输入参数中最大的值                              |
| min(expression)      | array,   numeric, string, date/time type                     | 与参数一致 | 输入参数中最小的值                              |
| sum(expression)      | smallint, int, bigint, real, double   precision,numeric, interval |  -          | 所有输入参数中的和                              |
