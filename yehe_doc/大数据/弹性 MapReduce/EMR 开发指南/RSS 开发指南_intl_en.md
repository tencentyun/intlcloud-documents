## RSS overview
Apache Uniffle is a unified remote shuffle service (RSS) for compute engines. It provides the ability to aggregate and store shuffle data on a remote server, thus improving the performance and reliability of large jobs.
## Background
Problems with the existing shuffle solution:
- The existing shuffle solution cannot make computing serverless. Therefore, shuffle data will be computed again when server resources are preempted.
- Shuffle partitioning will lead to a large number of shuffle connections and small network packets, tending to cause timeouts in large-scale scenarios.
- The shuffle process is subject to write amplification and random I/O. In the case of a large shuffle data volume, the cluster performance and stability will be severely affected.
- The Spark shuffle service and NodeManager are in the same process, which means the NodeManager tends to restart due to a high I/O load, thereby affecting YARN scheduling.

## Basic RSS characteristics
1. It stores shuffle data on a remote server and supports computing-storage separation, hybrid deployment of computing and storage, and other cluster deployment modes.
2. It supports mechanisms for aggregating and caching shuffle data, maximizes memory utilization, and reduces random access to the disk.
3. It supports multiple methods for storing shuffle data, such as `MEMORY_LOCALFILE`, `MEMORY_HDFS`, and `MEMORY_LOCALFILE_HDFS`.
4. It supports verifying the correctness of shuffle data, ensuring the data correctness in the computing process while filtering out invalid data.
5. It adopts the primary-secondary architecture and active-standby multi-site active-active mode to improve the cluster resource utilization and service stability.

## Basic RSS architecture
![](https://qcloudimg.tencent-cloud.cn/raw/d96ed876585eb8f375108ccce1f07e58.png)
Here, component features are as follows:
- Coordinator: It manages shuffle servers based on the heartbeat mechanism, stores metadata information such as shuffle server resource usage, and assigns tasks. Specifically, it assigns proper shuffle servers to Spark applications to process different partition data based on the shuffle server load.
- Shuffle server: It receives, aggregates, and writes shuffle data into the storage. It also reads shuffle data based on different storage methods (such as `MEMORY_LOCALFILE`).
- Shuffle client: It communicates with the coordinator and shuffle server, sends shuffle data read/write requests, and keeps the heartbeats of the application and coordinator.

## RSS use
An RSS cluster provides the remote shuffle service. It cannot be used alone and needs to be associated with a Spark container cluster as follows:
Click **Spark Cluster** > **Cluster Info** > **Associate RSS cluster** and select a running RSS cluster.

## RSS configuration
You can view the configuration files and common configuration items of different RSS roles on the **Cluster Service** > **Configuration Management** page.
The coordinator role has `coordinator.conf` and `log4j.properties` configuration files, and the shuffle server role has `server.conf` and `log4j.properties` configuration files.
We recommend you not modify common configuration items in `coordinator.conf`.

| Parameter | Default Value | Description |
|---------|---------|---------|
| rss.coordinator.app.expired	| 60000	| Application expiration time (ms) |
| rss.coordinator.dynamicClientConf.enabled	| false	| Whether to enable dynamic client configuration. This parameter can be obtained from the Spark client. |
| rss.coordinator.exclude.nodes.file.path	| file:///usr/local/service/rss/conf/exclude_nodes	| The configuration file path of the excluded node |
| rss.coordinator.server.heartbeat.timeout	| 30000| 	The timeout period if no heartbeat is obtained from the shuffle server |
| rss.coordinator.shuffle.nodes.max	| 1000| 	The maximum number of shuffle servers that can be assigned |
| rss.jetty.http.port	| 19998	| Coordinator HTTP port |
| rss.rpc.server.port	| 19999	| Coordinator RPC port |
| rss.storage.type	| MEMORY_LOCALFILE	| RSS storage type. Valid values: `MEMORY_ONLY`, `MEMORY_LOCALFILE`, `MEMORY_LOCALFILE_HDFS`. As there is no available Hadoop cluster, `MEMORY_LOCALFILE` is used by default. |

We recommend you not modify common configuration items in `server.conf`.

| Parameter | Default Value | Description |
|---------|---------|---------|
| rss.coordinator.quorum	| rss-coordinator-rss-<Cluster ID>-0:19999,rss-coordinator-rss-<Cluster ID>-1:19999	| Coordinator quorum |
| rss.jetty.http.port	| 19998	| The HTTP port for the shuffle server |
| rss.rpc.server.port| 	19999	| The RPC port for the shuffle server |
| rss.server.buffer.capacity	| Memory limit value * 0.75 * 0.6	| The maximum memory of the buffer manager for the shuffle server |
| rss.server.disk.capacity	| The capacity of a data disk * 0.9| 	 The available disk capacity on the shuffle server |
| rss.server.flush.thread.alive	| The number of data disks | 	 The number of threads for flushing data to a file |
| rss.server.flush.threadPool.size	| The number of data disks * 2	| The size of the thread pool for flushing data to a file |
| rss.server.heartbeat.interval	| 10000	| The heartbeat interval to the coordinator |
| rss.server.heartbeat.timeout	| 60000	| Heartbeat timeout period |
| rss.server.read.buffer.capacity	| Memory limit value * 0.75 * 0.2	| The maximum size of buffer for reading data |
| rss.storage.basePath	| /data1/rssdata,/data2/rssdata... The number of paths equals to that of data disks by default. | 	The data disk path into which shuffle data is written |
| rss.storage.type	| MEMORY_LOCALFILE	| RSS storage type, which must be the same as that of the coordinator |

For more information, see [incubator-uniffle](https://github.com/apache/incubator-uniffle).
