This document introduces the basic syntax and examples of type aggregate functions.

An aggregate function is a function that performs calculation on a set of values and returns the result. CLS supports the following aggregate functions.

>? 
> - In CLS analysis statements, strings must be included in single quotes (''), and field names and column names are unsigned or included in double quotes (""). For example, 'status' indicates the string `status`, and status or "status" indicates the log field `status`.
> - Currently, CLS functions can be used in most regions. If they are required in Beijing, Shanghai, Guangzhou, and Nanjing, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
>

| Function                             | Description                                                         | Example                                                         |
| -------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| arbitrary(KEY)       | Randomly returns a non-NULL value in the target column.            | `* | SELECT arbitrary(request_method) AS request_method`     |
| avg(KEY)             | Calculates the arithmetic mean of the target column.                           | `* | SELECT AVG(request_time)`                               |
| bitwise_and_agg(KEY) | Returns the result of the bitwise AND operation for all values in the target column.       | `* | SELECT bitwise_and_agg(status)`                          |
| bitwise_or_agg(KEY)  | Returns the result of the bitwise OR operation for all values in the target column.         | `* | SELECT bitwise_or_agg(request_length)`                   |
| checksum(KEY)        | Calculates the checksum of the target column and returns the result in a Base64-encoded string. | `* | SELECT checksum(request_method) AS request_method`       |
| count(\*)             | The number of all rows.                                  | `* | SELECT COUNT(*) WHERE http_status >200`                 |
 | count(1) | COUNT(1) is the same as COUNT({ut}), which is the number of rows.          | `* | SELECT COUNT(1)` |
| count(KEY) | Count the number of rows in a KEY column that are not NULL.                   | `* | SELECT COUNT(request_time) WHERE request_time >5.0` |
| count_if(KEY) | Counts the number of logs that meet the specified requirement.                      | `* | SELECT count_if(remote_addr) AS UV` |
| geometric_mean(KEY) | Calculates the geometric mean of the target column.                          | `* | SELECT geometric_mean(request_time) AS request_time` |
 | max(KEY) | Query the maximum value in `x`. | `* | SELECT MAX(request_time) AS max_request_time`           |    
| max_by(x,y) | Returns the value of `x` when `y` is the maximum value.                        | `* | SELECT MAX(request_method, request_time) AS method` |
| max_by(x,y,n) | Returns a JSON array of the x-values of the maximum n y-values.   | `* | SELECT max_by(request_method, request_time, 3) AS method` |
| min(KEY)             | 查询 x 中最小值。                                   | `* | SELECT MIN(request_time) AS min_request_time`           |
| min_by(x,y)          | 返回 y 为最小值时对应的 x 值。                        | `* | SELECT min_by(request_method, request_time) AS method`   |
| min_by(x,y,n)        | 返回最小的 n 个 y 值对应的 x 值。返回结果为 JSON 数组。   | `* | SELECT min_by(request_method, request_time, 3) AS method` |
| sum(KEY)             | 计算 x 的总值。                                     | `* | SELECT SUM(body_bytes_sent) AS sum_bytes`               |



#### Parameter description

| Parameter         | Description              |
| ---- | ---------------------- |
| KEY    | 表示日志字段名称。           |
| x    | The parameter value can be of any type. |
| y    | The parameter value can be of any type. |
| n    | 大于0的整数。                   |

