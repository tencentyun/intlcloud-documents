## Problem Description
All nodes in the cluster have high CPU utilization, but there are not a lot of reads and writes. The specific problem can be seen on the **Stack Monitoring** page in Kibana:
![](https://main.qcloudimg.com/raw/3ebd8230d3d8d9dbb92f115f7515c48f.png)
In addition, you can also see the CPU utilization of each node on the node monitoring page in the [ES console](https://console.cloud.tencent.com/es):
![](https://main.qcloudimg.com/raw/e76f24e93deb429f5b241f113af162bc.png)
In this case, because the cluster read rate and write rate are not high, it is difficult to quickly find the root cause from the monitoring perspective. Therefore, you need to observe carefully and find the cause from the details. Below are several possible scenarios and corresponding troubleshooting ideas.

>? The situation where the CPU utilization of an individual node is much higher than that of other nodes is quite common. In most cases, this is caused by uneven load due to improper use of the cluster. For more information, please see [Uneven Cluster Load](https://intl.cloud.tencent.com/document/product/845/40978).

## Troubleshooting
### Large query requests cause the CPU utilization to soar
This situation is relatively common, and clues can be found from monitoring. Monitoring data shows that the fluctuation of the query request volume is basically in line with the maximum CPU utilization of the cluster.
![](https://main.qcloudimg.com/raw/648230a0eabc6100cdca48d356c71519.png)
To further identify the problem, you need to enable slow log collection for the cluster. For more information, please see [Querying Cluster Logs](https://intl.cloud.tencent.com/document/product/845/30950). You can get more information from the slow logs, such as the indexes that cause slow queries, query parameters, and query content.

### Solutions
- Try to avoid large text searches and optimize queries.
- Use the slow logs to identify indexes where queries are slow. For some indexes with a small amount of data, set a small number of shards and multiple replicas, such as one-shard-multi-replica, to improve the query performance.

### Write requests causes the CPU utilization to soar
If monitoring data shows that the CPU utilization surge is related to writes, then enable slow log collection for the cluster, identify slow write requests, and optimize them. You can also get the `hot_threads` information to identify which thread is consuming the CPU:
```
curl http://9.15.49.78:9200/_nodes/hot_threads
```
![](https://main.qcloudimg.com/raw/b44d79ae65813f73f26b9ae1c2bc0d81.png)
For example, it is found here that there are a lot of `ingest pipeline` operations, and such operations are very resource intensive.
![](https://main.qcloudimg.com/raw/98aa569f971fabb4ad525720a0c16b57.png)

### Solutions
If you encounter the above problems, you need to optimize as appropriate on the business side. The key point of troubleshooting such problems is to make good use of the cluster's monitoring metrics to quickly locate the problems and then use the cluster logs together to identify the root causes, so that the problems can be solved quickly.
