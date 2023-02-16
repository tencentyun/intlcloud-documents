The monitoring feature provided by TencentDB for MongoDB allows you to view the real-time monitoring metric data of instance resources. It collects the monitoring statistics in various forms such as visual chart, table, and dashboard. In addition, it supports setting alarms and pushing alarm notifications promptly, so that you can stay up to date with database service exceptions and adjust your business in time to guarantee stable business operations.

## Monitoring Granularity
TencentDB for MongoDB currently doesn't allow you to customize the monitoring data collection granularity. The adaptive policy is as follows:

| Time Span | Monitoring Granularity | Retention Period |
| ---------- | -------- | -------- |
| 0–1 day | 5 seconds | 1 day |
| 0–1 day  | 1 minute    | 15 days     |
| 0–1 day  | 5 minutes    | 31 days     |
| 0–1 day | 1 hour | 93 days |
| 0–1 day | 1 day | 186 days |
| 0–7 days | 1 hour | 93 days |
| 0–7 days  | 1 day      | 186 days    |
| 7–30 days | 1 hour    | 93 days     |
| 7–30 days | 1 day | 186 days |



## Types of Instances for Monitoring

- Instance: Primary, read-only, and disaster recovery instances can be monitored, and each instance is provided with a separate monitoring view.
- Node: All mongod and mongos nodes can be monitored, and each node is provided with a separate monitoring view.

## Monitoring Metrics
### Instance

<table width="100">
<thead>
<tr><th width="15%">Dimension</th><th width="25%">Monitoring Metric Name</th><th width="10%">Parameter</th><th width="5%">Unit</th><th width="45%">Description</th></tr>
</thead>
<tbody>
<tr>
<td rowspan="4">CPU</td>
<td>Maximum mongod CPU utilization</td><td>mongod_max_cpu_usage</td><td>%</td><td>Maximum CPU utilization among all mongod nodes in the cluster.</td></tr>
<tr>
<td>Average mongod CPU utilization</td><td>monogd_avg_cpu_usage</td><td>%</td><td>Average CPU utilization of all mongod nodes in the cluster.</td></tr>
<tr>
<td>Maximum mongos CPU utilization</td><td>monogs_max_cpu_usage</td><td>%</td><td>Maximum CPU utilization among all mongos nodes in the sharded cluster.</td></tr>
<tr>
<td>Average mongos CPU utilization</td><td>monogs_avg_cpu_usage</td><td>%</td><td>Average CPU utilization of all mongos nodes in the sharded cluster.</td></tr>   
<tr>
<td rowspan="4">Memory</td>
<td>Maximum mongod memory utilization</td><td>mongod_max_mem_usage</td><td>%</td><td>Maximum memory utilization among all mongod nodes in the cluster.</td></tr>
<tr>
<td>Average mongod memory utilization</td><td>mongod_avg_mem_usage</td><td>%</td><td>Average memory utilization of all mongod nodes in the cluster.</td></tr>
<tr>
<td>Maximum mongos memory utilization</td><td>mongos_max_mem_usage</td><td>%</td><td>Maximum memory utilization among all mongos nodes in the sharded cluster.</td></tr>    
<tr>
<td>Average mongos memory utilization</td><td>mongos_avg_mem_usage</td><td>%</td><td>Average memory utilization of all mongos nodes in the sharded cluster.</td></tr>
<tr>
<td>Disk</td>
<td>Storage space utilization</td><td>disk_usage</td><td>%</td><td>Proportion of the used disk space to the disk space applied for.</td></tr>    
<tr>
<td rowspan="4">Network</td>
<td>Connections</td><td>cluster_conn</td><td>-</td><td>Number of TCP connections to the instance.</td></tr>
<tr>
<td>Connection percentage</td><td>connper</td><td>%</td><td>Proportion of current connections to maximum connections of the cluster.</td></tr>
<tr>
<td>Inbound traffic</td><td>cluster_view</td><td>Bytes</td><td>Number of bytes in the traffic inbound to the cluster.</td></tr>     
<tr>
<td>Outbound traffic</td><td>cluster_netout<//td><td>Bytes</td><td>Number of bytes in the traffic outbound from the cluster.</td></tr>
<tr>
<td rowspan="12">Latency</td>
<td>Average request latency<td>avg_all_request_delay</br></td><td>ms</td><td>Average execution latency of all requests in the cluster.</td></tr>
<tr>
<td>Average update latency</td><td>avg_update_delay</td><td>ms</td><td>Average latency of update requests in the cluster.</td></tr>
<tr>
<td>Average insertion latency</td><td>avg_insert_delay</td><td>ms</td><td>Average latency of insertion requests in the cluster.</td></tr>
<tr>
<td>Average read latency</td><td>avg_read_delay</td><td>ms</td><td>Average latency of read requests in the cluster.</td></tr>
<tr>
<td>Average aggregate latency</td><td>avg_aggregate_delay</td><td>ms</td><td>Average latency of aggregate requests in the cluster.</td></tr>
<tr>
<td>Average count latency</td><td>avg_count_delay</td><td>ms</td><td>Average latency of count requests in the cluster.</td></tr>
<tr>
<td>Average getMore latency</td><td>avg_getmore_delay</td><td>ms</td><td>Average latency of getMore requests in the cluster.</td></tr>
<tr>
<td>Average deletion latency</td><td>avg_delete_delay</td><td>ms</td><td>Average latency of deletion requests in the cluster.</td></tr>
<tr>
<td>Average command latency</td><td>avg_command_delay</td><td>ms</td><td>Average latency of command requests in the cluster other than `insert`, `update`, `delete`, and `query` requests.</td></tr>
<tr>
<td>10–50 ms</td><td>10 ms</td><td>-</td><td>Number of requests with an execution time between 10 and 50 ms.</td></tr>
<tr>
<td>50–100 ms</td><td>50 ms</td><td>-</td><td>Number of requests with an execution time between 50 and 100 ms.</td></tr>
<tr>
<td>100 ms</td><td>100 ms</td><td>-</td><td> Number of requests with an execution time of more than 100 ms.</td></tr>
<tr><td rowspan="9">Request</td>
<td>Total requests</td><td>success_per_second</td><td>Count/sec</td><td>Number of requests successfully executed in the cluster per second.</td></tr>
<tr>
<td>Insertion requests</td><td>insert_per_second</td><td>Count/sec</td><td>Number of insertion requests executed in the cluster per second.</td></tr>
<tr>
<td>Read requests</td><td>read_per_second</td><td>Count/sec</td><td>Number of read requests executed in the cluster per second.</td></tr>
<tr>
<td>Update requests</td><td>update_per_second</td><td>Count/sec</td><td>Number of update requests executed in the cluster per second.</td></tr>
<tr>
<td>Deletion requests</td><td>delete_per_second</td><td>Count/sec</td><td>Number of deletion requests executed in the cluster per second.</td></tr>
<tr>
<td>Count requests</td><td>count_per_second</td><td>Count/sec</td><td>Number of count requests received by the cluster per second.</td></tr>
<tr>
<td>getMore requests</td><td>getmore_per_second</td><td>Count/sec</td><td>Number of getMore requests received by the cluster per second.</td></tr>
<tr>
<td>Aggregate requests</td><td>aggregate_per_second</td><td>Count/sec</td><td>Number of aggregate requests in the cluster per second.</td></tr>
<tr>
<td>Command requests</td><td>command_per_second</td>
<td>Count/sec</td><td>Number of command requests received by the cluster per second other than INSERT, UPDATE, DELETE, and QUERY requests</td></tr>
<tr>
<td rowspan="9">Requests</td>
<td>Total requests</td><td>node_success</td><td>-</td><td>Total number of requests in the cluster.</td></tr>
<tr>
<td>Insertion requests</td><td>node_inserts</td><td>-</td><td>Number of insertion requests received by the cluster.</td></tr>
<tr>
<td>Read requests</td><td>node_reads</td><td>-</td><td>Number of read requests received by the cluster.</td></tr>
<tr>
<td>Update requests</td><td>node_updates</td><td>-</td><td>Number of update requests in the cluster.</td></tr>
<tr>
<td>Deletion requests</td><td>node_deletes</td><td>-</td><td>Number of deletion requests in the cluster.</td></tr>
<tr>
<td>Count requests</td><td>node_counts</td><td>-</td><td>Number of count requests received by the cluster.</td></tr>
<tr>
<td>getMore requests</td><td>node_getmores</td><td>-</td><td>Number of getMore requests received by the cluster.</td></tr>
<tr>
<td>Aggregate requests</td><td>node_aggregates</td><td>-</td><td>Number of aggregate requests in the cluster.</td></tr>
<tr>
<td>Command requests</td><td>node_commands</td><td>-</td><td>Number of command requests received by the cluster other than INSERT, UPDATE, DELETE, and QUERY requests.</td></tr>
</tbody></table>

### Mongod node

<table width="100">
<thead>
<tr><th width="15%">Dimension</th><th width="25%">Monitoring Metric Name</th><th width="10%">Parameter</th><th width="5%">Unit</th><th width="45%">Description</th></tr>
</thead>
<tbody>
<tr>
<td>CPU</td>
<td>CPU utilization</td><td>cpuusage</td><td>%</td><td>CPU utilization of the mongod node.</td></tr> 
<tr>
<td>Memory</td>
<td>Memory utilization</td><td>memusage</td><td>%</td><td>Memory utilization of the mongod node.</td></tr>
<tr>
<td rowspan="3">Disk</td>
<td>Disk space usage</td><td>diskusage</td><td>MB</td><td>Disk capacity usage of the mongod node.</td></tr>
<tr>
<td>Disk reads</td><td>ioread</td><td>Count/sec</td><td>Number of reads on the mongod node per second.</td></tr>
<tr>
<td>Disk writes</td><td>iowrite</td><td>Count/sec</td><td>Number of writes on the mongod node per second.</td></tr>     
<tr>
<td rowspan="2">Network</td>
<td>Inbound traffic</td><td>netout</td><td>Bytes</td><td>Number of bytes in the traffic inbound to the mongod node.</td>   
<tr>
<td>Outbound traffic</td><td>netin</td><td>Bytes</td><td>Number of bytes in the traffic outbound from the mongod node.</td></tr>
<tr>
<td rowspan="12">Average request latency</td>
<td>Average request latency</td><td>node_avg_all_requests_delay</td><td>ms</td><td>Average latency of all requests received by the mongod node.</td></tr>
<tr>
<td>Average update latency</td><td>node_avg_update_delay</td><td>ms</td><td>Average latency of update requests on the mongod node.</td></tr>
<tr>
<td>Average insertion latency</td><td>node_avg_insert_delay</td><td>ms</td><td>Average latency of insertion requests on the mongod node.</td></tr>
<tr>
<td>Average read delay</td><td>node_avg_read_delay</td><td>ms</td><td>Average latency of read requests on the mongod node.</td></tr>
<tr>
<td>Average aggregate delay</td><td>node_avg_aggregate_delay</td><td>ms</td><td>Average latency of aggregate requests on the mongod node.</td></tr>
<tr>
<td>Average count delay</td><td>node_avg_count_delay</td><td>ms</td><td>Average latency of count requests on the mongod node.</td></tr>
<tr>
<td>Average getMore delay</td><td>node_avg_getmore_delay</td><td>ms</td><td>Average latency of getMore requests on the mongod node.</td></tr>
<tr>
<td>Average deletion latency</td><td>node_avg_delete_delay</td><td>ms</td><td>Average latency of deletion requests on the mongod node.</td></tr>
<tr>
<td>Average command latency</td><td>node_avg_command_delay</td><td>ms</td><td>Average latency of command requests on the mongod node.</td></tr>
<tr>
<td>10–50 ms</td><td>10 ms</td><td>-</td><td>Number of requests with an execution time between 10 and 50 ms.</td></tr>
<tr>
<td>50–100 ms</td><td>50 ms</td><td>-</td><td>Number of requests with an execution time between 50 and 100 ms.</td></tr>
<tr>
<td>100 ms</td><td>100 ms</td><td>-</td><td> Number of requests with an execution time of more than 100 ms.</td></tr>
<tr>
<td rowspan="9">Request</td>
<td>Total requests</td><td>node_success_per_second</td><td>Count/sec</td><td>Total number of requests on the mongod node per second.</td></tr>
<tr>
<td>Insertion requests</td><td>node_insert_per_second<td>Count/sec</td><td>Number of insertion requests on the mongod node per second.</td></tr>
<tr>
<td>Read requests</td><td>node_read_per_second</td><td>Count/sec</td><td>Number of read requests on the mongod node per second.</td></tr>
<tr>
<td>Update requests</td><td>node_update_per_second</td><td>Count/sec</td><td>Number of update requests on the mongod node per second.</td></tr>
<tr>
<td>Deletion requests</td><td>node_delete_per_second</td><td>Count/sec</td><td>Number of deletion requests on the mongod node per second.</td></tr>
<tr>
<td>Count requests</td><td>node_count_per_second</td><td>Count/sec</td><td>Number of count requests received by the mongod node per second.</td></tr>
<tr>
<td>getMore requests</td><td>node_getmore_per_second</td><td>Count/sec</td><td>Number of getMore requests received by the mongod node per second.</td></tr>
<tr>
<td>Aggregate requests</td><td>node_aggregate_per_second</td><td>Count/sec</td><td>Number of aggregate requests in the mongod node per second.</td></tr>
<tr>
<td>Command requests</td><td>node_command_per_second</td><td>Count/sec</td><td>Number of command requests received by the mongod node per second other than INSERT, UPDATE, DELETE, and QUERY requests.</td></tr>
<tr>
<td rowspan="12">Kernel</td>
<td>Active write requests</td><td>ar</td><td>-</td><td>Number of active write requests on the mongod node.</td></tr>
<tr>
<td>Active read requests</td><td>aw</td><td>-</td><td>Number of active read requests on the mongod node.</td></tr>
<tr>
<td>Read requests in queue</td><td>qr</td><td>-</td><td>Length of the client read request queue on the mongod node.</td></tr>
<tr>
<td>Write requests in queue</td><td>qw</td><td>-</td><td>Length of the client write request queue on the mongod node.</td></tr>
<tr>
<td>Pieces of data deleted via </td><td>ttl_deleted</td><td>-</td><td>Number of documents deleted through TTL on the mongod node.</td></tr>
<tr>
<td>TTL run times</td><td>ttl_pass</td><td>-</td><td>Number of file deletions from the TTL collection performed by the backend process.</td></tr>
<tr>
<td>Active sessions</td><td>active_session</td><td>-</td><td>Number of active sessions on the node.</td></tr>
<tr>
<td>Oplog retention period</td><td>node_oplog_reserved_time</td><td>Hour</td><td>Oplog retention period.</td></tr>
<td>Primary/Replica delay</td><td>node_slavedelay</td><td>s</td><td>Delay time between the primary and replica nodes.</td></tr>   
<tr>
<td>Cache hit rate</td><td>replicaset_node</td><td>%</td><td>Cache hit rate of the current cluster.</td></tr><tr>
<td>Cache utilization</td><td>node_cache_used</td><td>%</td><td>Percentage of the used cache to the total cache space.</td></tr>
<tr>
<td>Dirty cache percentage</td><td>node_cache_dirty</td><td>%</td><td>Percentage of the size of dirty data in the cache to the total cache space.</td></tr>
<tr>
<td rowspan="9">Requests</td>
<td>Total requests</td><td>node_success</td><td>-</td><td>Total number of requests in the cluster.</td></tr>
<tr>
<td>Insertion requests</td><td>node_inserts</td><td>-</td><td>Number of insertion requests in the cluster.</td></tr>
<tr>
<td>Read requests</td><td>node_reads</td><td>-</td><td>Number of read requests in the cluster.</td></tr>
<tr>
<td>Update requests</td><td>replicaset_node</td><td>-</td><td>Number of update requests in the cluster.</td></tr>
<tr>
<td>Deletion requests</td><td>node_deletes</td><td>-</td><td>Number of deletion requests in the cluster.</td></tr>
<tr>
<td>Count requests</td><td>node_counts</td><td>-</td><td>Number of count requests received by the cluster.</td></tr>
<tr><td>getMore requests</td><td>node_getmores</td><td>-</td><td>Number of getMore requests received by the cluster.</td></tr>
<tr>
<td>Aggregate requests</td><td>node_aggregates</td><td>-</td><td>Number of aggregate requests in the cluster.</td></tr>
<tr>
<td>Command requests</td><td>node_commands</td><td>-</td><td>Number of command requests received by the cluster other than INSERT, UPDATE, DELETE, and QUERY requests.</td></tr>
</tbody></table>

### Mongos node (sharded cluster)

<table width="100">
<thead>
<tr><th width="15%">Dimension</th><th width="25%">Monitoring Metric Name</th><th width="10%">Parameter</th><th width="5%">Unit</th><th width="45%">Description</th></tr>
</thead>
<tbody>
<tr>
<td>CPU</td>
<td>CPU utilization</td><td>cpuusage</td><td>%</td><td>CPU utilization of the mongos node.</td></tr> 
<tr>
<td>Memory</td>
<td>Memory utilization</td><td>memusage</td><td>%</td><td>Memory utilization of the mongos node.</td></tr>   
<tr>
<td rowspan="2">Network</td>
<td>Private network inbound traffic</td><td>netin</td><td>Bytes</td><td>Number of bytes in the traffic inbound to the mongos node.</td>   
<tr>
<td>Private network outbound traffic</td><td>netout</td><td>Bytes</td><td>Number of bytes in the traffic outbound from the mongos node.</td></tr>
<tr>
<td rowspan="12">Latency</td>
<td>Average request latency</td><td>node_avg_all_request_delay</td><td>ms</td><td>Average latency of all requests received by the mongos node.</td></tr>
<tr>
<td>Average update latency</td><td>node_avg_update_delay</td><td>ms</td><td>Average latency of update requests on the mongos node.</td></tr>
<tr>
<td>Average insertion latency</td><td>replicaset_node</td><td>ms</td><td>Average latency of insertion requests on the mongos node.</td></tr>
<tr>
<td>Average read delay</td><td>node_avg_read_delay</td><td>ms</td><td>Average latency of read requests on the mongos node.</td></tr>
<tr>
<td>Average aggregate delay</td><td>node_avg_aggregate_delay</td><td>ms</td><td>Average latency of aggregate requests on the mongos node.</td></tr>
<tr>
<td>Average count delay</td><td>node_avg_count_delay</td><td>ms</td><td>Average latency of count requests on the mongos node.</td></tr>
<tr>
<td>Average getMore delay</td><td>node_avg_getmore_delay</td><td>ms</td><td>Average latency of getMore requests on the mongos node.</td></tr>
<tr>
<td>Average deletion latency</td><td>node_avg_delete_delay</td><td>ms</td><td>Average latency of deletion requests on the mongos node.</td></tr>
<tr>
<td>Average command latency</td><td>node_avg_command_delay</td><td>ms</td><td>Average latency of command requests on the mongos node other than `insert`, `update`, `delete`, and `query` requests.</td></tr>
<tr>
<td>10–50 ms</td><td>10 ms</td><td>-</td><td>Number of requests per second with an execution time between 10 and 50 ms.</td></tr>
<tr>
<td>50–100 ms</td><td>50 ms</td><td>-</td><td>Number of requests per second with an execution time between 50 and 100 ms.</td></tr>
<tr>
<td>100 ms</td><td>100 ms</td><td>-</td><td> Number of requests per second with an execution time of more than 100 ms.</td></tr>
<tr>
<td rowspan="9">Request</td>
<td>Total requests</td><td>qps</td><td>Count/sec</td><td>Total number of requests on the mongos node per second.</td></tr>
<tr>
<td>Insertion requests</td><td>inserts</td><td>Count/sec</td><td>Number of insertion requests on the mongos node per second.</td></tr>
<tr>
<td>Read requests</td><td>reads</td><td>Count/sec</td><td>Number of read requests on the mongos node per second.</td></tr>
<tr>
<td>Update requests</td><td>updates</td><td>Count/sec</td><td>Number of update requests on the mongos node per second.</td></tr>
<tr>
<td>Deletion requests</td><td>deletes</td><td>Count/sec</td><td>Number of deletion requests on the mongos node per second.</td></tr>
<tr>
<td>Count requests</td><td>counts</td><td>Count/sec</td><td>Number of count requests received by the mongos node per second.</td></tr>
<tr><td>getMore requests</td><td>getmores</td><td>Count/sec</td><td>Number of getMore requests received by the mongos node per second.</td></tr>
<tr>
<td>Aggregate requests</td><td>aggregates</td><td>Count/sec</td><td>Number of aggregate requests in the mongos node per second.</td></tr>
<tr>
<td>Command requests</td><td>commands</td><td>Count/sec</td><td>Number of command requests received by the mongos node per second other than INSERT, UPDATE, DELETE, and QUERY requests.</td></tr>
<tr><td rowspan="9">Requests</td>
<td>Total requests</br></td><td>node_success</td><td>-</td><td>Total number of requests received by the mongos node.</td></tr>
<tr>
<td>Insertion requests</br></td><td>node_inserts</td><td>-</td><td>Number of insertion requests received by the mongos node.</td></tr>
<tr>
<td>Read requests</br></td><td>node_reads</td><td>-</td><td>Number of read requests received by the mongos node.</td></tr>
<tr>
<td>Update requests</br></td><td>node_updates</td><td>-</td><td>Number of update requests received by the mongos node.</td></tr>
<tr>
<td>Deletion requests</td><td>node_deletes</td><td>-</td><td>Number of deletion requests received by the mongos node.</td></tr>
<tr>
<td>Count requests</br></td><td>node_counts</td><td>-</td><td>Number of count requests received by the mongos node.</td></tr>
<tr><td>getMore requests</br></td><td>node_getmores</td><td>-</td><td>Number of getMore requests received by the mongos node.</td></tr>
<tr>
<td>Aggregate requests</td><td>node_aggregates</td><td>-</td><td>Number of aggregate requests received by the mongos node.</td></tr>
<tr>
<td>Command requests</td><td>node_commands</td><td>-</td><td>Number of command requests received by the mongos node other than INSERT, UPDATE, DELETE, and QUERY requests.</td></tr>
</tbody></table>

