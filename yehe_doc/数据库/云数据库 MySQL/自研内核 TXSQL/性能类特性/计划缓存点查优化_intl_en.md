## Overview
In MySQL, SQL statement execution is divided into four stages: parsing, preparation, optimization, and execution. The execution plan cache feature is only available for prepared statements. After the feature is enabled, the first three stages will be skipped when executing a prepared statement, greatly boosting query performance.

In MySQL 8.0 20210830, the execution plan cache takes effect only for queries using unique keys (UKs) or primary keys (PKs). We will cover more types of queries in later versions.

## Supported Versions
Kernel version: MySQL 8.0 20210830 and later.

## Use Cases
This feature is mainly used to improve the query performance when executing short prepared statements with UKs or PKs on TencentDB instances. However, the extent to which performance may improved depends on your business.

## Performance Impact
- For UK and PK SQL statements, the delay is reduced by 20%-30% and the throughput is improved by 20%-30% after the execution plan cache is enabled (according to the sysbench test using the point_select.lua script).
- Memory usage will increase after the execution plan cache is enabled.

## Instructions
You can use the `cdb_plan_cache` parameter to enable or disable the execution plan cache and the `cdb_plan_cache_stats` parameter to query information about cache hits. Note that only accounts with the tencentroot permission can use the two parameters.

| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| -------------- | ---- | ---- | ----- | ---------- | --------------------------------- |
| cdb_plan_cache | Yes  | bool | false | true/false | Whether to enable the feature. Only accounts with the feature permission can use the parameter. |

>?Currently, you cannot directly modify the values of the above parameter. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

You can run the `show cdb_plan_cache` command to query information about execution plan cache hits. The command will return the following fields:

| Field | Description                                                         |
| ------ | ------------------------------------------------------------ |
| sql    | A SQL statement with the question mark (?) which represents that the execution plan of this statement has been cached. |
| mode   | SQL cache mode. Currently, only the `prepare` mode is supported.                           |
| hit    | Number of hits for this session.                                          |

After `cdb_plan_cache_stats` is enabled, cache hit information will be recorded, affecting database performance.

## SQL Execution Status
You can run `show profile` to show the status at each stage of SQL statement execution. But when the execution plan cache is hit, the status of `optimizing`, `statistics`, and `preparing` will be omitted.

