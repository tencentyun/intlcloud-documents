## Monitoring Granularity
TencentDB for MongoDB does not support customizing monitoring granularity. The adaptive monitoring policy is as follows:

| Time Span | Monitoring Granularity | Retention Period |
| -------- | -------- | -------- |
| 0-2 days | 1 minute | 2 days |
| 2-7 days | 5 minutes | 7 days |
| 7-30 days | 1 minute | 30 days |

## Types of Instances for Monitoring

TencentDB for MongoDB can monitor master instances, read-only instances and disaster recovery instances, and provide an independent monitoring view for each instance for query.

## Monitoring Metrics

Tencent Cloud's Cloud Monitor provides the following monitoring metrics for TencentDB for MongoDB instances:

| Metric Name | Metric | Unit | Dimension | Metric Description |
| ---------------- | ----------------- | ----- | ---- | ------------------------------------------ |
| Write request | inserts | N/A | Cluster | Number of write requests for current cluster |
| Read request | reads | N/A | Cluster | Number of read requests for current cluster |
| Update request | updates | N/A | Cluster | Number of update requests for current cluster |
| Delete request | deletes | N/A | Cluster | Number of delete requests for current cluster |
| count request | counts | N/A | Cluster | Total number of requests for current cluster |
| Aggregates request | aggregates | N/A | Cluster | Number of aggregation requests for current cluster |
| Number of cluster connections | conn | N/A | Cluster | Total number of connections, i.e. the total number of connections received by current cluster proxy |
| Proportion of cluster connections | connper | % | Cluster | Proportion of current connections to the configured total connections of the cluster |
| Capacity usage | diskusage | % | Cluster | Proportion of storage space occupied of the cluster to the total capacity |
| QPS | qps | N/A | Cluster | Operations per second, including CRUD operations |
| 10-50 ms | 10 ms | N/A | Cluster | Number of requests with an execution time between 10 ms and 50 ms |
| 50-100 ms | 50 ms | N/A | Cluster | Number of requests with an execution time between 50 ms and 100 ms |
| 100 ms | 100 ms | N/A | Cluster | Number of requests with an execution time of more than 100 ms |
| Timeout | timeouts | N/A | Cluster | Number of timeout requests |
| Master-slave delay | slavedelay | Seconds | Cluster | Master-slave delay time |
| Time difference in oplog | oplogreservedtime | Hours | Cluster | Time difference between the last operation and the first operation in oplog |
| CPU utilization | cpuusage | % | Node | CPU utilization of current node |
| MEM usage | memusage | % | Node | MEM usage of current node |
| qr | qr | N/A | Node | Length of client read request queue |
| qw | qw | N/A | Node | Length of client write request queue |
| Number of connections | conn | N/A | Node | Number of connections of current mongod node |
| netin | netin | MB/s | Node | Inbound traffic |
| netout | netout | MB/s | Node | Outbound traffic |

