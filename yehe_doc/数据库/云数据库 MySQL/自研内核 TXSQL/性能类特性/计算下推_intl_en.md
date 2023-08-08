## Overview
This feature pushes LIMIT/OFFSET and SUM operations down to the storage engine InnoDB when querying single tables, effectively reducing query latency.
- When LIMIT/OFFSET is executed using secondary indexes, this feature can avoid using the clustered index values as pointers to find the full table rows, effectively cutting the cost of scanning table data.
- This feature pushes SUM operations down to InnoDB. In other words, instead of sending rows to the MySQL server, InnoDB calculates data itself and returns the final result to the MySQL server.

## Supported Versions
- LIMIT/OFFSET optimization applies to kernel version MySQL 5.7 20180530.
- SUM optimization applies to kernel version MySQL 5.7 20180918.

## Use Cases
- This feature is mainly used to optimize single-table queries with LIMIT/OFFSET or SUM clauses, such as `Select *from tbl Limit 10”, “Select* from tbl Limit 10,2`, and `Select sum(c1) from tbl`.
- This feature cannot optimize the following queries:
  - Queries with DISTINCT, GROUP BY, or HAVING clauses
  - Nested subqueries
  - Queries with FULLTEXT indexes
  - Queries with ORDER BY clauses, where the optimizer fails to use indexes to implement ORDER BY
  - Queries with multi-range read (MRR)
  - Queries with SQL_CALC_FOUND_ROWS.

## Performance Data
Import one million rows of data and test query performance in sysbench:
- The execution time of `select * from sbtest1 limit 1000000,1;` decreases from 6.3 to 2.8 seconds.
- The execution time of `select sum(k) from sbtest1;` decreases from 5.4 to 1.5 seconds.

## Instructions
During the execution of an SQL statement, the optimizer automatically modifies the query execution plan to implement computation pushdown according to the following parameters.
Parameters are as follows:

| Parameter                     | Effective Immediately | Type | Default Value | Valid Values/Value Range | Description                             |
| -------------------------- | ---- | ---- | ---- | ---------- | -------------------------------- |
| cdb_enable_offset_pushdown | Yes  | bool | ON   | {ON,OFF}   | Enable or disable LIMIT/OFFSET pushdown. It is enabled by default. |
| cdb_enable_sumagg_pushdown | Yes  | bool | OFF  | {ON,OFF}   | Enable or disable SUM pushdown. It is disabled by default.          |

>?Currently, you cannot directly modify the values of the above parameters. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
