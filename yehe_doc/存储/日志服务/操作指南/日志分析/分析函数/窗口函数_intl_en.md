This document introduces the basic syntax and examples of window functions.

A window function calculates the data of multiple rows and returns the calculation result. Unlike GROUP BY, it only appends the calculation result to each row of data and does not merge the rows.

### Syntax

```
window_function (expression) OVER (
   [ PARTITION BY part_key ]
   [ ORDER BY order_key ]
   [ { ROWS | RANGE } BETWEEN frame_start AND frame_end ] )
```

## Parameters

| Parameter                                               | Description                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| window_function                                    | Specifies the window value calculation method. Aggregate functions, ranking functions and value functions are supported.         |
| PARTITION BY                                       | Specifies how a window is partitioned.                                                 |
| ORDER BY                                           | Specifies how the rows in each window partition are ordered.                                   |
| { ROWS |RANGE } BETWEEN frame_start AND frame_end | Window frame, that is, data range (rows) used to calculate values for each row of data in a window partition. If not specified, it represents all rows in a window partition. <br />Examples:<br />rows between current row and 1 following: the current row and the following row<br />rows between 1 preceding and current row: the current row and the preceding row<br />rows between 1 preceding and 1 following: from the preceding row to the following row (a total of 3 rows)<br />rows between current row and unbounded following: the current row and all following rows<br />rows between unbounded preceding and current row: the current row and all preceding rows |

## General Aggregate Function

All [general aggregate functions](https://intl.cloud.tencent.com/document/product/614/41995) are supported, such as sum() and avg(), can be used to calculate the statistics of each row of data in window frames.

## Ranking Functions

Ranking functions cannot use window frames.

| Function                                            | Description                                                         |
| -------------- | ------------------------------------------------------------ |
| rank()         | Returns the rank of each row in a window partition. Rows that have the same field value are assigned the same rank, and therefore ranks may not be consecutive. For example, if two rows have the same rank of 1, the rank of the next row is 3. |
| dense_rank()   | Similar to rank(). The difference is that the ranks in this function are consecutive. For example, if two rows have the same rank of 1, the rank of the next row is 2. |
| cume_dist()    | Returns the cumulative distribution of each value in a window partition, that is, the proportions of rows whose field values are less than or equal to the current field value to the total number of rows in the window partition. |
| ntile(n)       | Divides the rows for a window partition into `n` groups. If the number of rows in the partition is not divided evenly into `n` groups, the remaining values are distributed one per group, starting with the first group. For example, if there are 4 rows of data, and they need to be divided into 4 groups, the numbers of each row of data are: 1, 1, 2, 2, 3, 4. |
| percent_rank() | Calculates the percentage ranking of each row in a window partition. The calculation formula is: (r - 1) / (n - 1), where `r` is the rank value obtained via rank() and `n` is the total number of rows in the window partition. |
| row_number()   | Calculates the rank of each row (after ranking based on ranking rules) in a window partition. The ranks are unique and start from 1. |


## Value Functions

| Function                                            | Description                                                         |
| ------------------------------------ | ------------------------------------------------------------ |
| first_value(key)                     | Returns the first value of `key` of the window partition.                                     |
| last_value(key)                      | Returns the last value of `key` of the window partition.                                     |
| nth_value(key, offset)               | Returns the value of `key` in the row at the specified offset of the window partition. Offsets start from 1 and cannot be 0 or negative. If `offset` is `null` or exceeds the number of rows in the window partition, `null` is returned. |
| lead(key[, offset[, default_value]]) | Returns the value of `key` in the row that is at the specified offset after the current row of the window partition. Offsets start from 0, indicating the current row. `offset` is 1 by default. If `offset` is `null`, `null` is returned. If the offset row exceeds the window partition, `default_value` is returned. If `default_value` is not specified, `null` is returned.<br />When using this function, you must specify the ranking rule (ORDER BY) within the window partition and cannot use window frames. |
| lag(key[, offset[, default_value]]) | Similar to `lead(key[, offset[, default_value]])`. The only difference is that this function returns the value at `offset` rows before the current row. |

## Examples

#### Example 1. Query the 5 slowest requests and their IDs of each API in the last hour

Set the time range to the last hour and run the following query and analysis statement, where `action` indicates the API name, `timeCost` indicates the API response time, and `seqId` indicates the request ID.
- Query and analysis statement
```
* | select * from (select action,timeCost,seqId,rank() over (partition by action order by timeCost desc) as ranking order by action,ranking,seqId) where ranking<=5 limit 10000
```
- Query and analysis result

| action      | timeCost | seqId                                | ranking |
| ----------- | -------- | ------------------------------------ | ------- |
| ModifyXXX   | 151      | d75427b3-c562-6d7a-354f-469963aab689 | 1       |
| ModifyXXX   | 104      | add0d353-1099-2c73-e9c9-19ad02480474 | 2       |
| CreateXXX   | 1254     | c7d591f0-2da6-292c-8abf-98a0716ff8c6 | 1       |
| CreateXXX   | 970      | d920cf7a-7e7b-524b-68e9-a957c454c328 | 2       |
| CreateXXX   | 812      | 16357f6d-33b3-83ea-0ae3-b1a2233d4858 | 3       |
| CreateXXX   | 795      | 0efdab5e-af5f-4a4a-0618-7961420d17a1 | 4       |
| CreateXXX   | 724      | fb0481f2-dcfc-9500-cb44-a139b774aceb | 5       |
| DescribeXXX | 55242    | 4129dcda-46d7-9213-510e-f58cba29daf5 | 1       |
| DescribeXXX | 17413    | e36cdeb0-cbc5-ce2b-dec7-f485818ab6c7 | 2       |
| DescribeXXX | 10171    | cd6228f7-4644-ba45-f539-0fce7b09455b | 3       |
| DescribeXXX | 9475     | 48b6f6e3-6d08-5a31-cd68-89006a346497 | 4       |
| DescribeXXX | 9337     | 940b5398-e2ae-9141-801b-b7f0ca548875 | 5       |


#### Example 2. Query the 3-day moving average trend of the application throughput

Select the last 7 days as the query and analysis time range and run the following query and analysis statement, where `pv` indicates the daily application throughput and `avg_pv_3` indicates the application throughput after 3-day moving average.

- Query and analysis statement
```
* | select avg(pv) over(order by analytic_time rows between 2 preceding and current row) as avg_pv_3,pv,analytic_time from (select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 day) as analytic_time, count(*) as pv group by analytic_time order by analytic_time)
```
- Query and analysis result
![](https://qcloudimg.tencent-cloud.cn/raw/e4056fba03106eb8705a19f1f77f68b0.png)


