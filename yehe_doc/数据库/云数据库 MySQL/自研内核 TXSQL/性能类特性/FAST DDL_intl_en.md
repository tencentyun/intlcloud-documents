
## Feature Overview
This feature speeds up the creation of secondary index. After the feature is enabled, secondary indexes can be concurrently sorted in a temp table using multiple threads. The feature also optimizes the operation of locking the flush list when loading bulk data, effectively reducing the time consumed by CREATE INDEX and the impact on concurrent DML operations.

## Supported Versions
- Kernel version: MySQL 8.0 20210330 and above.
- Kernel version: MySQL 5.7 20210331 and above.

## Use Cases
You need to perform DDL operations frequently on your database and may encounter the following DDL-related problems:
- Why does database performance fluctuate when I add indexes, which even affects business writes and reads?
- Why does it sometimes take more than 10 minutes to execute a DDL operation on a table less than one GB in size?
- Why does database performance fluctuate when I exit a connection where a temp table is used?

To solve the above common problems, the TXSQL kernel team has optimized the operation of locking the flush list when loading bulk data, based on in-depth analysis and testing in multiple scenarios. The optimization effectively reduces the time consumed by CREATE INDEX, the impact on concurrent DML operations, and the impact caused by DDL operations.

## Performance Data
Use sysbench to test database performance when importing two billion rows of data (about 453 GB) before and after FAST DDL is enabled.
```
mysql> set global innodb_fast_ddl=ON;
Query OK, 0 rows affected (0.00 sec)
```
When the feature is disabled, the operation takes 4,395 seconds; when the feature is enabled, the operation takes 2,455 seconds.

## Use Instructions
Use the `innodb_fast_ddl` parameter to enable or disable this feature.

| Parameter | Effective Immediately | Type | Default Value | Valid Values/Value Range | Description |
| ----------------------------- | ---- | ------- | ---- | ---------- | ---------------------------- |
| innodb_fast_ddl | Yes | bool | OFF | {ON,OFF} | Enable or disable FAST DDL |

>?Currently, you cannot directly modify the values of the above parameters. If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>
