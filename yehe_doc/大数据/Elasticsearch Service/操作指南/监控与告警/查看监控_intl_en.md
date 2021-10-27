## Overview
ES provides a number of monitoring metrics for running ES clusters to monitor cluster operations such as storage, I/O, CPU, and memory utilization. Based on these metrics, you can understand the cluster operations in real time and promptly handle possible risks to ensure stable cluster operations. This document describes how to view cluster monitoring information in the ES console.

## Directions
1. Log in to the [ES console](https://console.cloud.tencent.com/es) and click a **cluster ID/name** on the cluster list page to enter the cluster details page.
2. Select the **Cluster Monitoring** tab to view the overall cluster running status. Select **Metric Group** to view the cluster monitoring metrics of data nodes, warm data nodes, and dedicated master nodes separately.
3. Select the **Node Monitoring** tab to view the operations and performance metrics of the nodes in the cluster.

### Cluster monitoring
On the cluster monitoring page, you can set alarm policies and view the cluster monitoring data. You can view the overall cluster status and cluster performance metrics by time range, metric group, and time granularity.
>?You can also view all the ES cluster monitoring metrics in the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/product/es). 
>
![](https://main.qcloudimg.com/raw/d7e31ce62b12dd7126888bbe47125d54.png)

### Node monitoring
- **Node list**
This section shows real-time health metrics of each node in the cluster.
![](https://main.qcloudimg.com/raw/da941a63b3ed26f26ef494f08f53bdf2.png)
- **Single node status**
This section shows detailed historical health status of each metric of each node.
![](https://main.qcloudimg.com/raw/142bc93a2a409fe4984d29e81cefc715.png)

### Descriptions of certain metrics
An ES cluster is generally composed of multiple nodes. To reflect the overall health status of the cluster, certain monitoring metrics provide two types of values: average value and maximum value.
- The average value is the average of the metric's values of all nodes in the cluster.
- The maximum value is the maximum value of the metric of all nodes in the cluster.

The statistical period of each metric is 1 minute; that is, the cluster's metrics are collected once every minute. The metrics are as described below:

<table  border="0" cellspacing="0" cellpadding="0">
   <tr>
      <th width="118px">Monitoring Metric</th>
      <th>Statistical Method</th>
      <th>Details</th>
   </tr>
   <tr>
      <td>Cluster health</td>
      <td>ES cluster health status. <br>0: green (the cluster is normal); <br>1: yellow (alarm; some replica shards are unavailable); <br>2: red (exception; some primary shards are unavailable). </td>
      <td><li>Green indicates that all primary and replica shards are available and the cluster is in the healthiest status. <li>Yellow indicates that all the primary shards are available, but some replica shards are unavailable. In this case, the search results are still complete; however, the high availability of the cluster is affected to some extent, and there are high risks with data loss. When the cluster health status changes to yellow, you should locate and troubleshoot the problem in a timely manner to prevent data loss. <li>Red indicates that at least one primary shard and all its replicas are unavailable. When the cluster health status changes to red, some data has already been lost, the search can only return partial data, and the write requests allocated to a lost shard will return an exception. In this case, you should locate and troubleshoot the exceptional shard as soon as possible.</td>
   </tr>
   <tr>
      <td>Avg disk usage</td>
      <td>The average of disk utilization values of all nodes in the cluster in one statistical period (1 minute).</td>
      <td>If the disk utilization is too high, data cannot be written properly. Solution: <br> Clean up useless indices promptly. <br>Expand the cluster capacity by increasing the disk capacity of individual nodes or increasing the number of nodes.</td>
   </tr>
	  <tr>
      <td>Max disk utilization</td>
      <td>The maximum disk utilization value of all nodes in the cluster in one statistical period (1 minute).</td>
      <td>- </td>
   </tr>
	 <tr>
      <td>Avg JVM memory utilization</td>
      <td>The average of JVM memory utilization values of all nodes in the cluster in one statistical period (1 minute).</td>
      <td>If this value is too high, frequent GC or even OOM will occur on cluster nodes. <br>This happens generally because the tasks to be processed by ES exceed the load capacity of the nodes' JVMs. You need to pay attention to the tasks that are being executed by the cluster or adjust the cluster configuration.</td>
   </tr>
	 <tr>
      <td>Max JVM memory utilization</td>
      <td>The maximum JVM memory utilization value of all nodes in the cluster in one statistical period (1 minute).</td>
      <td>- </td>
   </tr>
	 <tr>
      <td>	Avg CPU utilization</td>
      <td>The average of CPU utilization values of all nodes in the cluster in one statistical period (1 minute).</td>
      <td>When the read/write tasks processed by the nodes in the cluster exceed the load capacity of the nodes' CPUs, the value of this metric will become too high. In this case, the cluster nodes will experience a decrease in processing power or even crash. You can solve this problem in the following ways: <li> Observe whether the value of this metric is persistently or temporarily high. If it is temporarily soaring, determine whether there are temporary complex tasks in progress. <li>If it is persistently high, analyze whether the read/write operations on the cluster by your business can be optimized, lower the read/write frequency, and decrease the amount of data so as to reduce the node load. <li>If the node configuration cannot meet the throughput requirement of your business, you are recommended to perform vertical scaling of the cluster nodes to improve the load capacity of individual nodes.</td>
   </tr>
	 <tr>
      <td>Max CPU utilization	</td>
      <td>The maximum CPU utilization value of all nodes in the cluster in one statistical period (1 minute).</td>
      <td>- </td>
   </tr>
	 <tr>
      <td>Avg cluster load per minute</td>
      <td>The average load per minute (load_1m) of all nodes in the cluster. Source of the metric: ES node status API (_nodes/stats/os/cpu/load_average/1m).</td>
      <td>	If load_1m is too high, you are recommended to lower the cluster load or upgrade the cluster node specification.</td>
   </tr>
	 <tr>
      <td>Max cluster load per minute</td>
      <td>The maximum load per minute (load_1m) of all nodes in the cluster.</td>
      <td>	-   </td>
   </tr>
	 <tr>
      <td>Avg write latency</td>
      <td><li>Write latency (index_latency) refers to the time taken by a single index request (ms/request). The average write latency of the cluster is the average of the time taken by a single index request of all nodes in one statistical period (1 minute).<li>Calculation rule for the single index request time of a node: two metrics are recorded once every statistical period (1 minute), i.e., total number of historical indices on a node (_nodes/stats/indices/indexing/index_total) and total time taken by historical indices (_nodes/stats/indices/indexing/index_time_in_millis), and the difference between two adjacent records (i.e., the absolute value in one statistical period) is taken for calculation (index time / number of indices) to get the average single index time in one statistical period (1 minute).</td>
      <td>Write latency is the average time it takes to write a single document. The average write latency of the cluster refers to the average of write time of all nodes in one statistical period. <br>If the write latency is too high, you are recommended to upgrade the node specification or increase the number of nodes.</td>
   </tr>
	 <tr>
      <td>Max write latency</td>
      <td><li>Write latency (index_latency) refers to the time taken by a single index request (ms/request). The maximum write latency of the cluster is the maximum value of time taken by a single index request of all nodes in one statistical period (1 minute). <li>Calculation rule for single index request time of a node: see the average write latency section.</td>
      <td> - </td>
   </tr>
	 <tr>
      <td>Avg query latency</td>
      <td><li>Query latency (search_latency) refers to the time taken by a single query request (ms/request). The average query latency of the cluster is the average of the time taken by a single query request of all nodes in one statistical period (1 minute). <li>Calculation rule for the single query request time of a node: two metrics are recorded once every statistical period (1 minute), i.e., total number of historical queries on a node (_nodes/stats/indices/search/query_total) and total time taken by historical queries (_nodes/stats/indices/search/query_time_in_millis), and the difference between two adjacent records (i.e., the absolute value in one statistical period) is taken for calculation (query time / number of queries) to get the average single query time in one statistical period (1 minute).</td>
      <td>Query latency is the average time it takes to perform a single query. The average query latency of the cluster refers to the average of query time of all nodes in one statistical period. <br>If the query latency is too high, you are recommended to upgrade the node specification or increase the number of nodes.</td>
   </tr>
	 <tr>
      <td>Max query latency</td>
      <td> <li>Query latency (search_latency) refers to the time taken by a single query request (ms/request). The maximum query latency of the cluster is the maximum value of time taken by a single query request of all nodes in one statistical period (1 minute). <li>Calculation rule for single query request time of a node: see the average query latency section.</td>
      <td> - </td>
   </tr>
	 <tr>
      <td>Avg number of writes per second</td>
      <td>The average of the number of index requests received by all nodes in the cluster per second. Calculation rule for the number of index requests per second of a node: the total number of historical indices on a node (_nodes/stats/indices/indexing/index_total) is recorded once every statistical period (1 minute), and the difference between two adjacent records (i.e., the absolute value in one statistical period) is taken for calculation (number of indices / 60 seconds) to get the average number of index requests per second in one statistical period.</td>
      <td>-  </td>
   </tr>
	 <tr>
      <td>Avg number of queries per second</td>
      <td>The average of the number of query requests received by all nodes in the cluster per second. Calculation rule for the number of query requests per second of a node: the total number of historical queries on a node (_nodes/stats/indices/search/query_total) is recorded once every statistical period (1 minute), and the difference between two adjacent records (i.e., the absolute value in one statistical period) is taken for calculation (number of queries / 60 seconds) to get the average number of query requests per second in one statistical period.</td>
      <td> - </td>
   </tr>
	 <tr>
      <td>Write rejection rate</td>
      <td>This is the ratio calculated by dividing the number of write requests rejected by the cluster by the total number of write requests in one statistical period. Calculation rule: two metrics are collected once every statistical period, i.e., the number of historical write requests rejected (v5.6.4: _nodes/stats/thread_pool/bulk/rejected; v6.4.3 and above: _nodes/stats/thread_pool/write/rejected) and the total number of historical write requests (v5.6.4: _nodes/stats/thread_pool/bulk/completed; v6.4.3 and above: _nodes/stats/thread_pool/write/completed), and the difference between two adjacent records (i.e., the absolute value in one statistical period) is taken for calculation (number of rejected write requests / total number of write requests).</td>
      <td>When the write QPS is too large or the CPU, memory, and disk utilization is too high, the cluster's write rejection rate may increase. Generally, this is because that the current configuration of the cluster cannot meet the requirements of write operations on the business side. For scenarios where the node configuration is too low, you can solve this problem by upgrading the node specification or reducing the number of write operations. For scenarios where the disk utilization is too high, you can solve this problem by expanding the cluster's disk capacity or deleting useless data. </td>
   </tr>
	 <tr>
      <td>Query rejection rate</td>
      <td>This is the ratio calculated by dividing the number of query requests rejected by the cluster by the total number of query requests in one statistical period. Calculation rule: two metrics are collected once every statistical period, i.e., the number of historical query requests rejected (_nodes/stats/thread_pool/search/rejected) and the total number of historical query requests (_nodes/stats/thread_pool/search/completed), and the difference between two adjacent records (i.e., the absolute value in one statistical period) is taken for calculation (number of rejected query requests / total number of query requests).</td>
      <td>When the write QPS is too large or the CPU and memory utilization is too high, the cluster's query rejection rate may increase. Generally, this is because that the current configuration of the cluster cannot meet the requirements of read operations on the business side. If this value is too high, you are recommended to upgrade the cluster node specification so as to improve the processing capabilities of the cluster nodes.</td>
   </tr>
	  <tr>
      <td>Total documents</td>
      <td>Total number of documents written to the cluster. Calculation rule: ES cluster document quantity API (_cluster/stats/indices/docs/count).</td>
      <td>  - </td>
   </tr>
	  <tr>
      <td>Auto snapshot backup status</td>
      <td>The backup result after auto snapshot backup is enabled for the cluster. <br>0: auto backup is not enabled; <br>1: auto backup is normal; <br>-1: auto backup failed. </td>
      <td>Auto snapshot backup will periodically back up the cluster data to COS, so that the data can be recovered when needed, thus more comprehensively ensuring data security. We recommend you enable it. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/845/32587">Automatic Snapshot Backup</a>.</td>
   </tr>
</table>
