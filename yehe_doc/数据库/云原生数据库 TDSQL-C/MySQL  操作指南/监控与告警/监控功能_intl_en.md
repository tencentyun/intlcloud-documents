
To make it easier for you to view and stay up to date with how instances work, TDSQL-C provides a wide variety of performance monitoring metrics and convenient monitoring features (custom view, time comparison, merged monitoring metrics, etc). You can log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb), click a cluster ID in the cluster list to enter the instance list, click an instance ID, and select **Instance Monitoring** to view them.

>?If the number of tables in a single instance exceeds one million, database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.

## Types of Instances for Monitoring
TDSQL-C offers instance-level monitoring information, supports monitoring read-write and read-only instances, and provides each instance with a separate monitoring view for easy query.

## Monitoring Granularity
TDSQL-C has adopted an adaptive policy for monitoring granularity, which means that you cannot select a monitoring granularity as desired for the time being. The adaptive policy is as follows:

| Time Span | Monitoring Granularity | Adaptation Description | Retention Period |
|:-------|:--------|:----|:-----|
| (0h, 4h] | 5 seconds | The time span is below 4 hours, and the monitoring granularity is 5 seconds | 1 day |
| (4h, 2d] | 1 minute | The time span is above 4 hours but below 2 days, and the monitoring granularity is 1 minute | 15 days |
| (2d, 10d] | 5 minutes | The time span is above 2 days but below 10 days, and the monitoring granularity is 5 minutes | 31 days |
| (10d, 30d] | 1 hour | The time span is above 10 days but below 30 days, and the monitoring granularity is 1 hour | 62 days |

>?Currently, you can view the monitoring data of TDSQL-C in the last 30 days.
 
## Monitoring Metrics
CM provides the following monitoring metrics for TDSQL-C instances in the instance dimension:
>?For more information on how to use TencentDB monitoring metrics, see [TDSQL-C for MySQL Monitoring Metrics](https://intl.cloud.tencent.com/document/product/248/37383).

| Metric Name                                                   | Unit                |
| ------------------------------------------------------------ | ------------------- |
| Traffic Received from Client     | MB/s            |
| Traffic Sent to Client     | MB/s            |
| DELETE Statements    | Counts/sec            |
| TPS       | Counts/Sec            |
| UPDATE Statements    | Counts/sec            |
| INSERT Statements    | Counts/sec            |
| Used Memory  | MB            |
| Max Connections  | -              |
| Cache Hit Ratio  | %              |
| Cache Hits  | -              |
| SELECT Statements        | Counts/sec            |
| QPS           | Counts/sec            |
| CPU Utilization          | %              |
| Used Storage Space           | GB             |
| Database Connections        | -              |
| Cache Hit Ratio (New)      | %              |
| Temp Tables Created  | -              |
| InnoDB Cache Utilization | %               |
| Slow Queries       | -             |
| Running Threads | -             |
| Rollbacks Performed in Storage Engine    | -             |
| Internal COMMIT Statements    | -             |
| Rows Deleted from InnoDB Tables | -              |
| Rows Inserted to InnoDB Tables | -              |
| Rows Updated in InnoDB Tables | -              |
| Rows Read from InnoDB Tables | -              |
| Redo Log Based Replication Lag of Secondary Instance                   | ms             |
| Primary-Secondary LSN Difference During Redo Log Based Replication    | Bytes          |
| Replication Status of Secondary Instance     | 0-Yes, 1-No |
| InnoDB Logical Writes        | -             |
| InnoDB Logical Reads        | -              |

 
