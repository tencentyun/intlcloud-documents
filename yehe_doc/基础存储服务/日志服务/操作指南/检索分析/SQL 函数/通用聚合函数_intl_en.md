This document describes the basic syntax and examples of aggregate functions.

An aggregate function calculates a set of values and returns the calculation result. CLS supports the following aggregate functions.

>? In CLS analysis statements, strings must be included in single quotes (''), and field names and column names are unsigned or included in double quotes (""). For example, 'status' indicates the string **'status'**, and **status** or **"status"** indicates the log field `status`.
>

| Function             | Description                                              | Example                                                         |
| -------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| arbitrary(KEY) [](id:arbitrary)      | Returns an arbitrary non-null value of the `KEY` column.                  | `* | SELECT arbitrary(request_method) AS request_method`     |
| avg(KEY) [](id:avg)             | Returns the average (arithmetic mean) of the `KEY` column.                          | `* | SELECT AVG(request_time)`                               |
| bitwise_and_agg(KEY)[](id:bitwise_and_agg) | Returns the bitwise AND result of all input values of the `KEY` column.       | `* | SELECT bitwise_and_agg(status)`                          |
| bitwise_or_agg(KEY)  [](id:bitwise_or_agg) | Returns the bitwise OR result of all input values of the `KEY` column.        | `* | SELECT bitwise_or_agg(request_length)`                   |
| checksum(KEY)[](id:checksum)        | Returns the checksum of the `KEY` column. The return result is of Base64 encoding type. | `* | SELECT checksum(request_method) AS request_method`       |
| count(\*)  [](id:count_1)           | Returns the number of input rows.                                  | `* | SELECT COUNT(*) WHERE http_status >200`                 |
| count(1)   [](id:count_2)          | Returns the number of input rows. This function is equivalent to count(\*).          | `* | SELECT COUNT(1)`                                       |
| count(KEY)  [](id:count_3)        | Returns the number of non-null input values of the `KEY` column.                   | `* | SELECT COUNT(request_time) WHERE request_time >5.0`    |
| count_if(boolean) [](id:count_if)       | Returns the number of logs that meet specified conditions.                      | `* | select count_if(returnCode>=400) as errorCounts`                    |
| geometric_mean(KEY)[](id:geometric_mean) | Returns the geometric mean of `KEY`, which cannot contain negative numbers; otherwise, the result will be `NaN`.    | `* | SELECT geometric_mean(request_time) AS request_time`     |
| max(KEY)  [](id:max)             | Returns the maximum value of `KEY`.                                 | `* | SELECT MAX(request_time) AS max_request_time`           |
| max_by(x,y) [](id:max_by_1)         | Returns the value of `x` associated with the maximum value of `y `over all input values.                        | `* | SELECT MAX_BY(request_method, request_time) AS method`     |
| max_by(x,y,n) [](id:max_by_2)       | Returns `n` values of `x` associated with the `n` largest of all input values of `y` in descending order of `y`.   | `* | SELECT max_by(request_method, request_time, 3) AS method` |
| min(KEY)[](id:min)          | Returns the minimum value of `KEY`.                                   | `* | SELECT MIN(request_time) AS min_request_time`           |
| min_by(x,y)  [](id:min_by_1)      | Returns the value of `x` associated with the minimum value of `y `over all input values.                        | `* | SELECT min_by(request_method, request_time) AS method`   |
| min_by(x,y,n) [](id:min_by_2)       | Returns `n` values of `x` associated with the `n` smallest of all input values of `y` in descending order of `y`.   | `* | SELECT min_by(request_method, request_time, 3) AS method` |
| sum(KEY)  [](id:sum)         | Returns the sum of the `KEY` column.                                     | `* | SELECT SUM(body_bytes_sent) AS sum_bytes`               |
|  bool_and(boolean) [](id:bool_and)      |  Returns `TRUE` if all logs meet the specified condition or `FALSE` otherwise.                                  | `* | select bool_and(returnCode>=400)`               |
| bool_or(boolean) [](id:bool_or)     | Returns `TRUE` if any log meets the specified condition or `FALSE` otherwise.                                   | `* | select bool_or(returnCode>=400)`               |
|  every(boolean) [](id:every)    |   Equivalent to `bool_and(boolean)`.                                 | `* | select every(returnCode>=400)
`               |



#### Field description

| Parameter | Description |
| ---- | ---------------------- |
| KEY    | Name of the log field.           |
| x    | The parameter value can be of any data type.           |
| y    | The parameter value can be of any data type.           |
| n    | An integer greater than 0.                   |
