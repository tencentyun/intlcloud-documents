
## Problem Description
In MongoDB's replica set structure, a replica node will save the data logs synced from the primary node. This method is similar to the binlog source-replica replication method of MySQL. MongoDB uses the oplog to sync data from the primary node to the replica node. However, the configured oplog size is not infinite, and if it is exceeded, older oplog entries will be overwritten.

In daily Ops scenarios, when a replica database fails, the primary node still runs normally, and the failure will not affect the running status of the entire replica set. However, if the replica node is restarted, it will need to restore data from the primary node. At this time, if older oplog entries have been overwritten, the restored data will be incomplete since the overwritten data is lost, and the replica node cannot return to normal status. In other cases, database restarts and long primary-replica delays may also cause the problem of insufficient oplog entries.

## Solution
DBbrain can help you observe the risks with oplog storage on all production nodes 24/7 in real time.

### Using the exception diagnosis feature to troubleshoot database exceptions (recommended)
The exception diagnosis feature can proactively locate and perform optimization for failures, with no Ops experience required. It can find abnormal situations with high CPU utilization. Based on TencentDB for MongoDB Ops experts' many years of experience and combined with machine learning, big data, and intelligent analysis algorithms, this feature also quickly duplicates the capabilities of senior database experts to empower your MongoDB databases for smart Ops. It can discover almost all exceptions and failures in MongoDB production databases in real time.

The steps are as shown in the example below:
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/slow-sql) and select **Performance Optimization** on the left sidebar. On the displayed page, select the **Exception Diagnosis** tab.
2. In the overview section, a yellow mark indicates that a risk item is found at this time point.
3. In the **Diagnosis Details** list on the right, the risk item that the oplog storage period is too short is displayed at the same time.
4. Click the risk item to view more detailed exception information. The optimization suggestion will give reasonable measures based on the current situation.

