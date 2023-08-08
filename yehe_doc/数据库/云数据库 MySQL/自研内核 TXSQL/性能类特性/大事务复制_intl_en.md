## Overview
If multi-row large transaction is updated by a single statement in row format, an event will be generated for each row. As a result, a large number of binlogs are created, and APPLY operations in the replica database become slower during replication, causing replication delays.
After analyzing and optimizing the large transaction replication scenarios, the Tencent Cloud kernel team developed the large transaction replication optimization feature. With this feature, large transactions are automatically identified and binlogs are converted from row format into statement format, thus reducing the quantity of binlogs and increasing the replication performance.

## Supported Versions
- Kernel version: MySQL 5.6 20210630 and above.
- Kernel version: MySQL 5.7 20200630 and above.
- Kernel version: MySQL 8.0 20200830 and above.

## Use Cases
- This feature accelerates large transaction replay for tables without a primary key in row format. It can be enabled if you are sure that the delay is caused by slow replay due to the lack of primary key.
- This feature aims to solve slow replication when there are large transactions in row format.

## Performance Data
The replication time is reduced by 85% for UPDATE operations and about 30% for INSERT operations.

## Instructions
The large transaction replication optimization feature judges whether a transaction is large based on the historical execution statistics of the SQL statement. If a transaction is identified as large and optimizable, its isolation level will be automatically upgraded to repeatable read (RR), and the binlogs will be stored in statement format to reduce the time of executing the large transaction in the replica database. Here:
- `cdb_optimize_large_trans_binlog` is the switch of this feature.
- `cdb_sql_statistics` is the switch of SQL statement execution statistics collection.
- `cdb_optimize_large_trans_binlog_last_affected_rows_threshold` and `cdb_optimize_large_trans_binlog_aver_affected_rows_threshold` are the thresholds for judging a large transaction.
- `cdb_sql_statistics_info_threshold` is the number of legacy data entries retained in the memory.

To better monitor the transaction execution, the `CDB_SQL_STATISTICS` table is added in the `information_schema` database for you to query the statistics of the current transaction.

#### New parameters

| Parameter                                                         | Status | Type      | Default Value | Description                                      |
| :----------------------------------------------------------- | :------ | :-------- | :------ | :----------------------------------------------- |
| cdb_optimize_large_trans_binlog                              | true    | bool      | false   | Switch of large binlog transaction replication optimization.                           |
| cdb_optimize_large_trans_binlog_last_affected_rows_threshold | true    | ulonglong | 10000   | Large transaction replication optimization condition: threshold of the number of rows affected last time              |
| cdb_optimize_large_trans_binlog_aver_affected_rows_threshold | true    | ulonglong | 10000   | Large transaction replication optimization condition: threshold of the average number of  affected rows              |
| cdb_sql_statistics                                           | true    | bool      | false   | Switch of SQL statement execution statistics collection.            |
| cdb_sql_statistics_info_threshold                            | true    | ulonglong | 10000   | Maximum number of SQL statements saved in `map` of `CDB_SQL_STATISTICS`. |

>?Currently, you cannot directly modify the values of the above parameters. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

#### Newly added `information_schema.CDB_SQL_STATISTICS` table

| Name                           | Type                | Description                                             |
| :----------------------------- | :------------------ | :------------------------------------------------------ |
| DIGEST_MD5                     | MYSQL_TYPE_STRING   | MD5 value calculated from the digest of the SQL statement.                            |
| DIGEST_TEXT                    | MYSQL_TYPE_STRING   | SQL statement digest text format.                                   |
| SQL_COMMAND                    | MYSQL_TYPE_STRING   | SQL command type.                                           |
| FIRST_UPDATE_TIMESTAMP         | MYSQL_TYPE_DATETIME | The time when the statistics information of the SQL statement is generated for the first time.                            |
| LAST_UPDATE_TIMESTAMP          | MYSQL_TYPE_DATETIME | The time when the statistics information of the SQL statement is last updated.                              |
| LAST_ACCESS_TIMESTAMP          | MYSQL_TYPE_DATETIME | The time when the statistics information of the SQL statement is last accessed.                          |
| EXECUTE_COUNT                  | MYSQL_TYPE_LONGLONG | The number of executions of this SQL statement.                                       |
| TOTAL_AFFECTED_ROWS            | MYSQL_TYPE_LONGLONG | Total number of affected rows.                                            |
| AVER_AFFECTED_ROWS             | MYSQL_TYPE_LONGLONG | Average number of affected rows.                                          |
| LAST_AFFECTED_ROWS             | MYSQL_TYPE_LONGLONG | The number of rows affected last time.                                          |
| STMT_BINLOG_FORMAT_IF_POSSIBLE | MYSQL_TYPE_STRING   | Whether binlogs for this SQL statement can be stored in statement format. Valid values: TRUE, FALSE. |

