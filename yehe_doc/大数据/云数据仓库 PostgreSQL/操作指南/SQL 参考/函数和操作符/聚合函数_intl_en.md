The aggregate functions of the database calculate the values of columns to get a return value as listed below:

| Function | Parameter Type | Return Type | Description |
| -------------------- | ------------------------------------------------------ | ---------- | ----------------------------------------------- |
| avg(expression)      | All numeric types                                                 | Numeric   | Average                                          |
| bit_and(expression)  | smallint, int, bigint, bit                                   | Same as parameter type | Bitwise AND of all non-null values                                |
| bit_or(expression)   | smallint, int, bigint,   bit                                 | Same as parameter type | Bitwise OR of all non-null values                                |
| bool_and(expression) | bool                                                         | bool       |   Returns `true` if all values are `true` or returns `false` otherwise         |
| bool_or(expression)  | bool                                                         | bool       | Returns `true` if at least one value is `true` or returns `false` otherwise |
| count(\*)             |      -                                                        | bigint     | Number of input rows                                        |
| count(expression)    | any                                                          | bigint     | Number of input rows for which the value of expression is not null               |
| every(expression)    | bool                                                         | bool       |  Equivalent to `bool_and`                                  |
| max(expression)      | array,numeric,string,   date/time type                       | Same as parameter type | Maximum value in input parameters                              |
| min(expression)      | array,   numeric, string, date/time type                     | Same as parameter type | Minimum value in input parameters                              |
| sum(expression)      | smallint, int, bigint, real, double   precision,numeric, interval |  -          | Sum of all input parameters                              |
