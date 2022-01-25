The monitoring feature provided by TencentDB for MongoDB allows you to view the real-time monitoring metric data of instance resources. It collects the monitoring statistics in various forms such as visual chart, table, and dashboard. In addition, it supports setting alarms and pushing alarm notifications promptly, so that you can stay up to date with database service exceptions and adjust your business in time to guarantee stable business operations.

## Monitoring Granularity
TencentDB for MongoDB currently doesn't support customizing the granularity of monitoring data collection. Its adaptive policy is as follows:

| Time Span | Monitoring Granularity | Retention Period |
| ---------- | -------- | -------- |
| 0–1 day | 5 seconds | 1 day |
| 0–1 day | 1 minute | 15 days |
| 0–1 day | 5 minutes | 31 days |
| 0–7 days | 1 hour | 93 days |
| 7–30 days | 1 day | 186 days |

## Types of Instances for Monitoring
TencentDB for MongoDB primary, read-only, and disaster recovery instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## Monitoring Metrics
Cloud Monitor provides the following monitoring metrics for TencentDB for MongoDB instances:

<table width="100">
<thead>
<tr><th width="15%">Monitoring Dimension</th><th width="25%">Monitoring Metric</th><th width="5%">Unit</th><th width="55%">Description</th></tr>
</thead>
<tbody>
<tr>
<td rowspan="21">Cluster</td>
<td>Write Request</td><td>-</td><td>Number of write requests of the current cluster</td></tr>
<tr>
<td>Read Request</td><td>-</td><td>Number of read requests of the current cluster</td></tr>
<tr>
<td>Update Request</br></td><td>-</td><td>Number of update requests of the current cluster</td></tr>
<tr>
<td>Deletion Request</td><td>-</td><td>Number of deletion requests of the current cluster</td></tr>
<tr>
<td>Count Request</br></td><td>-</td><td>Number of count requests of the current cluster</td></tr>
<tr>
<td>Aggregate Request</td><td>-</td><td>Number of aggregate requests of the current cluster</td></tr>
<tr>
<td>Cluster Connections</td><td>-</td><td>Total number of cluster connections, i.e., number of connections received by the current cluster proxy</td></tr>
<tr>
<td>Cluster Connection Percentage</td><td>%</td><td>Proportion of current connections to total connections of the cluster</td></tr>
<tr>
<td>Max Capacity Utilization</td><td>%</td><td>Proportion of currently used storage capacity to total capacity of the cluster</td></tr>
<tr>
<td>QPS</td><td>Counts/sec</td><td>Operations per second, including CRUD operations</td></tr>
<tr>
<td>Submitted</td><td>-</td><td>Number of successful requests of the cluster</td></tr>
<tr>
<td>10–50 ms</td><td>-</td><td>Number of requests with an execution time between 10 and 50 ms</td></tr>
<tr>
<td>50–100 ms</td><td>-</td><td>Number of requests with an execution time between 50 and 100 ms</td></tr>
<tr>
<td>100 ms</td><td>-</td><td>Number of requests with an execution time of more than 100 ms</td></tr>
 <tr>
<td>Timeout</td><td>-</td><td>Number of timed-out requests</td></tr>
<tr>
<td>Oplog Time Difference</td><td>Hours</td><td>Time difference between the last operation and the first operation in oplog</td></tr>
<tr>
<td>Primary/Secondary Delay</td><td>s</td><td>Primary/Secondary delay time</td></tr>
<tr>
<td>Oplog Retention Period</td><td>Hours</td><td>Oplog retention period</td></tr>
<tr>
<td>Cache Utilization (%)</td><td>%</td><td>Percentage of used cache to total cache space</td></tr>
<tr>
<td>Dirty Data (%) in Cache</td><td>%</td><td>Percentage of the size of dirty data in the cache to total cache space</td></tr>
<tr>
<td>Cache Hit Rate</td><td>%</td><td>Cache hit rate of the current cluster</td></tr>
<tr>
<td rowspan="11">Node</td>
<td>CPU Utilization</td><td>%</td><td>Current node CPU utilization</td></tr>
<tr>
<td>Memory Utilization</td><td>%</td><td>Current node memory utilization</td></tr>
<tr>
<td>Active Write</td><td>-</td><td>Number of data writes of the current node</td></tr>
<tr>
<td>Active Read</td><td>-</td><td>Number of data reads of the current node</td></tr>
<tr>
<td>Pieces of Data Deleted via TTL</td><td>-</td><td>Number of data entries deleted via TTL</td></tr>
<tr>
<td>TTL Run Times</td><td>-</td><td>Number of TTL run times of the current node</td></tr>
<tr>
<td>qr</td><td>-</td><td>Length of the client read request queue</td></tr>
<tr>
<td>qw</td><td>-</td><td>Length of the client write request queue</td></tr>
<tr>
<td>Connections</td><td>-</td><td>Number of connections of the current mongod node</td></tr>
<tr>
<td>netin</td><td>MB/s</td><td>Inbound traffic</td></tr>
<tr>
<td>netout</td><td>MB/s</td><td>Outbound traffic</td></tr>
</tbody></table>

