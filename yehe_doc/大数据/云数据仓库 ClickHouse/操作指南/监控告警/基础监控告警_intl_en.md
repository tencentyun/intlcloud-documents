## Basic Monitoring
### Features
ClickHouse provides 46 service and performance monitoring metrics for you to stay up to date with cluster status. You can configure metrics to get real-time alarms for fast response to problems.


### Cluster monitoring
Log in to the [Cloud Data Warehouse console](https://console.cloud.tencent.com/cdwch), click a **Cluster ID/Name** in the **Cluster List** to enter the cluster details page, and switch to the **Cluster Monitoring** tab to view performance metrics.
![](https://qcloudimg.tencent-cloud.cn/raw/3e7d23cf9cd4d7b414e21dfcab996626.png)

>?You can configure an alarm threshold and export monitoring data for specific metrics. Metrics are collected once every 10 seconds, the minimum time granularity for data display is 1 minute, and the maximum value of data points collected within 1 minute is displayed.

### Cluster alarm configuration
1. On the cluster monitoring page, select a metric and configure its threshold for alarming as detailed below.
2. On the CM console window that pops up, filter the instance objects (by ClickHouse cluster name) and configure the metric thresholds as instructed in the configuration template. The configuration items for an alarm policy are as displayed below:
<table>
<tr>
<th>Item</th>
<th>Description</th>
</tr>
<tr>
<td>Policy Name</td>
<td>Name of the alarm policy</td>
</tr>
<tr>
<td>Monitor Type</td>
<td>Default: Cloud Product Monitoring</td>
</tr>
<tr>
<td>Policy Type</td>
<td>Default: Cloud Data Warehouse/CK alarm</td>
</tr>
<tr>
<td rowspan="2">Alarm Object</td>
<td>Default: Instance ID</td>
</tr>
<tr>
<td>Select a ClickHouse cluster in the drop-down list</td>
</tr>
<tr>
<td rowspan="2">Trigger Condition</td>
<td>Default: Manual Configuration</td>
</tr>
<tr>
<td>Thresholds and alarm policies configured in <b>Metric alarm</b></td>
</tr>
<tr>
<td>Notification Template</td>
<td>Select an existing notification template or create one</td>
</tr>
</table>
>?Do not modify the default values.
>
3. Click **Complete** to submit the alarm policy. For more CM alarm policies, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

## Monitoring Metrics
### Node metrics

| Metric           | Description                         | Remarks   |
| ---------------- | ---------------------------- | ------ |
| CPU utilization       | CPU utilization       | Average value |
| File opens       | Number of file opens per unit of time       | Average value |
| Memory utilization       | Memory utilization       | Average value |
| 1-min node load | Node load in 1 minute               | Average value |
| 5-min node load   | Node load in 5 minutes               | Average value |
| 15-min node load   | Node load in 15 minutes               | Average value |
| Data disk utilization     | Data disk utilization             | Average value |
| Inbound node traffic     | Amount of data received by the node per unit of time | Average value |
| Outbound node traffic     | Amount of data sent by the node per unit of time | Average value |

### Service metrics

| Metric                     | Description                              | Remarks                                                  |
| -------------------------- | --------------------------------- | ----------------------------------------------------- |
| Survival                        | Detects the survival of the CH process on a node          | Instantaneous value                                                |
| Contextual lock waits             | Number of contextual lock waits                | ClickHouseMetrics_ContextLockWait, instantaneous value             |
| HTTP connections                 | Number of HTTP connections                  | ClickHouseMetrics_HTTPConnection, instantaneous value              |
| TCP connections                  | Number of TCP connections                   | ClickHouseMetrics_TCPConnection, instantaneous value               |
| Insertions per unit of time     | Number of insertions per unit of time            | ClickHouseProfileEvents_InsertQuery, average value             |
| Merge time (rate)    | Time consumed by merges per unit of time         | ClickHouseProfileEvents_MergesTimeMilliseconds, average value  |
| MySQL connections                  | Number of JDBC connections                   | ClickHouseMetrics_MySQLConnection, instantaneous value               |
| CRUD queries    | Number of queries including CRUDs per unit of time | ClickHouseProfileEvents_Query, average value                   |
| Query threads                 | Number of current query threads              | ClickHouseMetrics_QueryThread, instantaneous value                 |
| Replica blocks merged per unit of time | Number of replica blocks merged per unit of time        | ClickHouseProfileEvents_ReplicatedPartMerges, average value    |
| Replica blocks modified per unit of time | Number of replica blocks modified per unit of time        | ClickHouseProfileEvents_ReplicatedPartMutations, average value    |
| Failed insertions                 | Number of failed insertions per unit of time            | ClickHouseProfileEvents_FailedInsertQuery, average value       |
| Failed queries                 | Number of failed queries per unit of time            | ClickHouseProfileEvents_FailedSelectQuery, average value       |
| Merges                     | Number of current merges                | ClickHouseMetrics_Merge, instantaneous value                       |

### CK ZooKeeper metrics

| Metric             | Description                            | Remarks                                       |
| ------------------ | ------------------------------- | ------------------------------------------ |
| ZooKeeper requests           | Number of current ZooKeeper requests      | ClickHouseMetrics_ZooKeeperRequest, instantaneous value |
| Current ZooKeeper sessions | Number of current ZooKeeper sessions | ClickHouseMetrics_ZooKeeperSession, instantaneous value  |
| ZooKeeper watches       | Number of current ZooKeeper watches    | ClickHouseMetrics_ZooKeeperWatch, instantaneous value   |

### ZooKeeper metrics

| Metric             | Description                               | Remarks                               |
| ------------------ | ---------------------------------- | ---------------------------------- |
| Sent packets           | Number of packets sent by ZooKeeper nodes per unit of time     | packets_sent, average value                 |
| Received packets           | Number of packets received by ZooKeeper  nodes per unit of time     | packets_received, average value             |
| ZooKeeper process survival         | ZooKeeper process monitoring. 1: alive; 0: dead | Instantaneous value                             |
| Global sessions    | Number of current global sessions          | global_sessions, instantaneous value            |
| Rejected connections        | Number of connections rejected by ZooKeeper per unit of time         | connection_rejected, average value          |
| Committed queue requests   | Number of current requests committed to the queue           | request_commit_queued, average value        |
| Wait time for queue preprocessing | Wait time for queue preprocessing per unit of time       | prep_processor_queue_time_ms, average value |
| Preprocessing time         | Preprocessing time per unit of time               | prep_process_time, average value            |
| ZooKeeper watches       | Number of current ZooKeeper watches               | watch_count, instantaneous value                |
| JVM memory pool utilization      | JVM memory pool usage details              | jvm_memory_pool_bytes_used, instantaneous value |

For metric descriptions, see [system.metrics](https://clickhouse.tech/docs/en/operations/system-tables/metrics/).

#### Notes
1. ZooKeeper monitoring metrics are available for HA clusters on v21.3.9.84 or later.
2. When advanced [Grafana monitoring](https://intl.cloud.tencent.com/document/product/1129/44427) is enabled, the basic monitoring page will be updated to the advanced monitoring page.
