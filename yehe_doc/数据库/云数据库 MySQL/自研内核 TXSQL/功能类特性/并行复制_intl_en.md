## Overview
Prior to MySQL 5.6, the source node syncs binlogs and the replica node replays binlogs, both in the single-thread mode. MySQL 5.6 and later versions support the DATABASE/LOGICAL_CLOCK parallel replication scheme, but the granularity is too large to achieve expected parallel replication in many cases.

Tencent Cloud's TXSQL kernel team has optimized the parallel replication scheme. Table parallel replication is now supported, improving parallelism and reducing source-replica delay.

## Supported Versions
- Kernel version: MySQL 8.0 20201230 and later.
- Kernel version: MySQL 5.7 20180530 and later.
- Kernel version: MySQL 5.6 20170830 and later.

## Use Cases
This feature is suitable for use cases where optimizing the parallelism of some loads can speed up the binlog replay at the replica node, thus reducing the source-replica delay.

## Instructions
For MySQL 5.6 and 5.7, you can enable this feature by setting the `slave_parallel_type` parameter to the newly added value `TABLE`. MySQL 8.0 does not support the TABLE mode.
Additionally, the `cdb_slave_thread_status` table is added to the `information_schema` database to display the thread status of the replica node.

<dx-tabs>
::: MySQL 5.6 parameter description
| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ------------------- | ---- | ----- | -------- | ---------------------------- | ------------------------------------------------------------ |
| slave_parallel_type | Yes  | char\* | SCHEMA | SCHEMA/TABLE | The level of parallel replication on the replica node. <li>SCHEMA: Replication events of different schemas can be executed in parallel. <li>TABLE: Replication events of different tables can be executed in parallel. |
:::
::: MySQL 5.7 parameter description
| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ------------------- | ---- | ----- | -------- | ---------------------------- | ------------------------------------------------------------ |
| slave_parallel_type | Yes  | char\* | LOGICAL_CLOCK | DATABASE/TABLE/LOGICAL_CLOCK | The level of parallel replication on the replica node. <li>DATABASE: Replication events of different databases can be executed in parallel. <li>TABLE: Replication events of different tables can be executed in parallel. <li>LOGICAL_CLOCK: Replication events of the same logical clock on the host can be executed in parallel. |
:::
::: MySQL 8.0 parameter description
| Parameter                                  | Effective Immediately | Type    | Default Value | Valid Values/Value Range      | Description                                                         |
| ------------------- | ---- | ----- | -------- | ---------------------------- | ------------------------------------------------------------ |
| slave_parallel_type | Yes  | char\* | LOGICAL_CLOCK | DATABASE/LOGICAL_CLOCK | The level of parallel replication on the replica node. <li>DATABASE: Replication events of different databases can be executed in parallel. <li>LOGICAL_CLOCK: Replication events of the same logical clock on the host can be executed in parallel. |

:::
</dx-tabs>
