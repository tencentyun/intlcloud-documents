## Background
The instance [monitoring feature](https://intl.cloud.tencent.com/document/product/409/7564) of TencentDB for PostgreSQL was upgraded on May 11, 2021. In the upgrade, certain legacy monitoring policies were optimized, a large number of new metrics were added, and 5-second monitoring was supported for all metrics. After the upgrade, the collected data and upper limits of certain metrics changed greatly compared to those on legacy versions. This document describes the details of such changes.

## Changes in Collected Metric Data
- **CPU Utilization**: the upper limit is fixed at 100%, that is, even if the instance overuses idle resources, the metric value will still not exceed 100%. Please set the alarm threshold on the basis of 100%.

- **Used Storage Capacity**: the collected metric data on legacy versions takes into account only data files while excluding other files such as instance log files. However, the actual disk usage needs to be calculated based on the total size of all files on the instance.
Therefore, in order to avoid the deviation between the actual usage and metric value, this metric has been standardized to the sum of storage space occupied by all files such as data files (datafile), redo log files (xlog/WAL), database running log files (pg_log), and database program files, so there will be a big increase in the used storage space as seen in the monitoring metric.
- **Storage Space Utilization**: similar to the "Used Storage Capacity" metric, this metric is calculated as follows: **used storage capacity/purchased instance storage capacity * 100%**.
- **Queries Per Second (QPS)**: the metric name has been changed to **QPS**, as the original name was ambiguous. The actual collection unit is **counts/sec**.
- **Requests**: the unit of this metric on legacy versions was "counts/min". As the meaning of this metric has changed after monitoring at the second level is supported, which is the total number of requests in a collection period now, the unit has also been changed to "-". In addition, the average value was previously used for the 1-minute and 5-minute granularities, but the total value is used now. The original monitoring metric has been disused in the new release.
- **Read Requests**: the unit of this metric on legacy versions was "counts/min". As the meaning of this metric has changed after monitoring at the second level is supported, which is the total number of requests in a collection period now, the unit has also been changed to "-". In addition, the average value was previously used for the 1-minute and 5-minute granularities, but the total value is used now. The original monitoring metric has been disused in the new release.
- **Write Requests**: the unit of this metric on legacy versions was "counts/min". As the meaning of this metric has changed after monitoring at the second level is supported, which is the total number of requests in a collection period now, the unit has also been changed to "-". In addition, the average value was previously used for the 1-minute and 5-minute granularities, but the total value is used now. The original monitoring metric has been disused in the new release.
- **Other Requests**: the unit of this metric on legacy versions was "counts/min". As the meaning of this metric has changed after monitoring at the second level is supported, which is the total number of requests in a collection period now, the unit has also been changed to "-". In addition, the average value was previously used for the 1-minute and 5-minute granularities, but the total value is used now. The original monitoring metric has been disused in the new release.
- **Primary/Standby XLOG Sync Difference**: the name of this metric has been changed to **Differences Between sent_lsn and replay_lsn**. It indicates the difference between the size of the log sent from the primary node to the standby node and the log replayed on the standby node, which reflects the log application speed of the standby node as well as its performance and network transfer speed. It is available only for primary instances but not for read-only instances.
- **Primary-Standby Lag**: the name of this metric has been changed to **WAL Flush Lag**. It indicates the time difference between the time point when the log is sent from the primary node to the standby node and the time point when the standby node receives the log and flushes it. It is available only for primary instances on v10.x or above.
 
 
 
 
 
 

## New Metrics
- **Rows Scanned in Index Scans /sec**: average number of tupes scanned by the index per second.	
- **Rows Scanned in Sequential Scans /sec**: average number of tupes scanned in the full table per second.	
- **Deadlocks**: total number of deadlocks in a collection period.		
- **Rows Updated /sec**: average number of updated tupes per second.	
- **Rows Inserted /sec**: average number of inserted tupes per second.
- **Rows Deleted /sec**: average number of deleted tupes per second.	
- **Primary-Standby Sync Delay**: for primary instances, this metric indicates the failover duration. For read-only instances, it indicates the time after which the data written to primary instances can be queried on the read-only instances. The metric for read-only instances has the same name.
