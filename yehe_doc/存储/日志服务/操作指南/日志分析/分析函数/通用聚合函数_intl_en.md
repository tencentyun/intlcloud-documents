This document introduces the basic syntax and examples of aggregate functions.

An aggregate function calculates a set of values and returns the calculation result. CLS supports the following aggregate functions.

>? In CLS analysis statements, strings must be included in single quotes (''), and field names and column names are unsigned or included in double quotes (""). For example, 'status' indicates the string **'status'**, and **status** or **"status"** indicates the log field `status`.
>

| Function             | Description                                              | Example                                                         |
| -------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| arbitrary(KEY)       | Returns an arbitrary non-null value of `KEY`.                  | `* | SELECT arbitrary(request_method) AS request_method`     |
| avg(KEY)             | Returns the average (arithmetic mean) of the `KEY` column.                          | `* | SELECT AVG(request_time)`                               |
| bitwise_and_agg(KEY) | Returns the bitwise AND result of all input values of the `KEY` column.       | `* | SELECT bitwise_and_agg(status)`                          |
| bitwise_or_agg(KEY)  | Returns the bitwise OR result of all input values of the `KEY` column.        | `* | SELECT bitwise_or_agg(request_length)`                   |
| checksum(KEY)        | Returns the checksum of the `KEY` column. The return result is of Base64 encoding type. | `* | SELECT checksum(request_method) AS request_method`       |
| count(\*)             | Returns the number of input rows.                                  | `* | SELECT COUNT(*) WHERE http_status >200`                 |
| count(1)             | Returns the number of input rows. This function is equivalent to count(\*).          | `* | SELECT COUNT(1)`                                       |
| count(KEY)           | Returns the number of non-null input values of the `KEY` column.                   | `* | SELECT COUNT(request_time) WHERE request_time >5.0`    |
| count_if(boolean)        | Returns the number of logs that meet specified conditions.                      | `* | select count_if(returnCode>=400) as errorCounts`                    |
| geometric_mean(KEY)  | Returns the geometric mean of the `KEY` column.                          | `* | SELECT geometric_mean(request_time) AS request_time`     |
| max(KEY)             | Returns the maximum value of `KEY`.                                 | `* | SELECT MAX(request_time) AS max_request_time`           |
| max_by(x,y)          | Returns the value of `x` associated with the maximum value of `y `over all input values.                        | `* | SELECT MAX(request_method, request_time) AS method`     |
| max_by(x,y,n)        | Returns `n` values of `x` associated with the `n` largest of all input values of `y` in descending order of `y`.   | `* | SELECT max_by(request_method, request_time, 3) AS method` |
| min(KEY)             | Returns the minimum value of `KEY`.                                   | `* | SELECT MIN(request_time) AS min_request_time`           |
| min_by(x,y)          | Returns the value of `x` associated with the minimum value of `y `over all input values.                        | `* | SELECT min_by(request_method, request_time) AS method`   |
| min_by(x,y,n)        | Returns `n` values of `x` associated with the `n` smallest of all input values of `y` in descending order of `y`.   | `* | SELECT min_by(request_method, request_time, 3) AS method` |
| sum(KEY)             | Returns the sum of the `KEY` column.                                     | `* | SELECT SUM(body_bytes_sent) AS sum_bytes`               |



#### Parameter description

| Parameter         | Description              |
| ---- | ---------------------- |
| KEY    | Name of the log field.           |
| x    | The parameter value can be of any data type.           |
| y    | The parameter value can be of any data type.           |
| n    | An integer greater than 0.                   |

