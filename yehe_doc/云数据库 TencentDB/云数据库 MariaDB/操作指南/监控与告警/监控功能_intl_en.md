## Performance Monitoring
To make it easier for you to view and stay up to date with how instances work, TencentDB for MariaDB provides a wide variety of performance monitoring metrics. You can log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql) and view them on the **System Monitoring** tab on the instance management page.

## Slave Monitoring
TencentDB for MariaDB supports monitoring slave performance. On the **System Monitoring** tab, you can switch to slave data as prompted.

## Available Monitoring Metrics

| Metric Name | Unit | Remarks |
|-------|-------|-------|
| CPU Utilization | % | TencentDB for MariaDB adopts flexible CPU limiting, allowing your instance to use extra device CPU resources when they are idle. In this case, CPU utilization may exceed 100%. |
| Buffer Cache Hit Ratio | % | The percentage of data a SELECT or preprocessing query directly gets from the memory. You are recommended to keep it above 90%; otherwise, you need to increase the memory specification. |
| Freeable Memory (this metric will be deleted) | GB | Actual memory capacity available in Innodb_buffer. As the database uses the LRU scheduling scheme, normally this value tends to be zero. However, when large transactions are processed, it may be negative, i.e., the used database memory exceeds the assigned capacity. |
| Storage Space Utilization | % | Percentage of current storage capacity used by instanced data, logs, temporary data, and system files out of the purchased disk capacity. Generally, this value should be smaller than 80% of the purchased disk capacity; otherwise, the disk capacity should be expanded. |
| Free Storage Space | GB | Absolute value of remaining available disk capacity of current instance. Generally, this value should be greater than 20% of the purchased disk capacity; otherwise, the disk capacity should be expanded. |
| Binary Log Disk Usage | GB | Storage capacity temporarily stored in database on data disk. Generally, this value varies by percentage of written data. Please note that this value is not the log storage capacity in the backup system. |
| DB Connections | - | Total number of connections from client to database server. |
| Active Connections | - | Total number of active connections from client to database server. |
| IO Utilization | % | TencentDB for MariaDB adopts a flexible I/O limiting policy, allowing instances to use extra device I/O resources when they are idle. In this case, I/O utilization may exceed 100%. |
| SQL Throughput | Statements/second | Total number of DDL, DML, and DCL statements. |
| SQL Error Throughput | Statements/second | Total number of execution errors of DDL, DML, and DCL statements. If this value is high, please check the service logs as soon as possible. |
| SQL Success Throughput | Statements/second | Total number of successful executions of DDL, DML, and DCL statements. |
| Slow Query | Statements/second | Number of SQL statements whose execution time exceeds the set value of `long_query_time`. For more information, please see the performance optimization page. |
| DML Latency 1ms - 5ms | Statements/second | Overall statistics of SQL statement execution time. |
| DML Latency 5ms - 20ms | Statements/second | Overall statistics of SQL statement execution time. |
| DML Latency 20ms - 30ms | Statements/second | Overall statistics of SQL statement execution time. |
| DML Latency more than 30ms | Statements/second | Overall statistics of SQL statement execution time. |
| DML Throughput | Statements/second | Total number of DML statements. |
| SELECT | Statements/second | Total number of SELECT statements. If this value is high, you can enable read/write separation. |
| UPDATE | Statements/second | Total number of UPDATE statements. |
| INSERT | Statements/second | Total number of INSERT statements. |
| REPLACE | Statements/second | Total number of REPLACE statements. |
| REPLACE_SELECT | Statements/second | Total number of REPLACE_SELECT statements. |
| DELETE | Statements/second | Total number of DELETE statements. |
| Master Switch | - | Number of occurrences of switching from the master to the slave. |
| Replica Lag | Seconds | Data delay between the slave and master. With strong sync, the master will return a transaction response only when data is written to the binlog of the slave. In this case, the data has not been fully written to the disk, so delay will still occur. |
| Innodb Buffer Pool Read | Requests/second | This metric is used to analyze current performance of the InnoDB storage engine. |
| Innodb Buffer Pool Read Requests | Requests/second | This metric is used to analyze current performance of the InnoDB storage engine. |
| Innodb Buffer Pool Read Ahead | Requests/second | This metric is used to analyze current performance of the InnoDB storage engine. |
| Innodb Rows Deleted | Rows/second | This metric is used to analyze current performance of the InnoDB storage engine. |
| Innodb Rows Insert | Rows/second | This metric is used to analyze current performance of the InnoDB storage engine. |
| Innodb Rows Read | Rows/second | This metric is used to analyze current performance of the InnoDB storage engine. |
| Innodb Rows Updated | Rows/second | This metric is used to analyze current performance of the InnoDB storage engine. |
