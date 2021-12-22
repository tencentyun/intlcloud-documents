## Namespace

Namespace=QCE/TXMR_ZOOKEEPER

## Monitoring Metrics

| Parameter | Metric | Unit | Description | Dimension |
| ---------------------------------------------- | ------------------------------------------- | --------------------- | --------------------------------------- | ------------------------------------------------ |
| ZkQmGcUtilGcCountYgc                           | GC count_YGC                                 | -                    | Young GC count                           | id4zookeeperzookeeper,  <br>host4zookeeperzookeeper |
| ZkQmGcUtilGcCountFgc                           | GC count_FGC                                 | -                    | Full GC count                            | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilGcTimeFgct                           | GC time_FGCT                                | s                     | Time consumed by Full GC                        | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilGcTimeGct                            | GC time_FGCT                                | s                     | Time used to collect garbage                        | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilGcTimeYgct                           | GC time_YGCT                                | s                     | Time consumed by Young GC                       | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilMemoryS0                             | Memory space percentage_S0                             | %                     | Percentage of used Survivor 0 memory                | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilMemoryE                              | Memory space percentage_E                              | %                     | Percentage of used Eden memory                     | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilMemoryCcs                            | Memory space percentage_CCS                            | %                     | Percentage of memory used by compressed class space   | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilMemoryS1                             | Memory space percentage_S1                             | %                     | Percentage of used Survivor 1 memory                | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilMemoryO                              | Memory space percentage_O                              | %                     | Percentage of used Old memory                      | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmGcUtilMemoryM                              | Memory space percentage_M                              | %                     | Percentage of used Metaspace memory                | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMemMem<br>nonheapusedm                  | JVM memory\_MemNonHeapUsedM                   | MB                    |  Size of the NonHeapMemory currently used by JVM | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMemMem<br>nonheapcommittedm             | JVM memory\_MemNonHeapCommittedM              | MB                    | Size of the NonHeapMemory currently committed by JVM | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMemMem<br>heapusedm                     | JVM memory\_MemHeapUsedM                      | MB                    | Size of the HeapMemory currently used by JVM    | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMemMem<br>heapcommittedm                | JVM memory\_MemHeapCommittedM                 | MB                    | Size of the HeapMemory currently committed by JVM    | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMem<br>Memheapmaxm                      | JVM memory\_MemHeapMaxM                       | MB                    | Size of the HeapMemory configured by JVM            | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMem<br>Memheapinitm                     | JVM memory_MemHeapInitM                       | MB                    | Size of the initial JVM HeapMem                 | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmJvmMemMem<br>nonheapinitm                  | JVM memory_MemNonHeapInitM                    | MB                    | Size of the initial JVM NonHeapMem              | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmOsCpuLoad<br>Processcpuload                | CPU utilization_ProcessCpuLoad                   | %                     | CPU utilization                              | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmOsFdCountZk<br>MaxFileDescriptorCount      | Number of file descriptors\_zk_max_file_descriptor_count  | -                    | Maximum number of file descriptors                        | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmOsFdCountZk<br>OpenFileDescriptorCount     | Number of file descriptors\_zk_open_file_descriptor_count | -                    | Number of opened file descriptors                      | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmOsCpuTime<br>Processcputime                | Cumulative CPU usage time\_ProcessCpuTime            | ms                    | Cumulative CPU usage time                        | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmRtUptimeUptime                             | Process run time_Uptime                         | s                     | Process run time                            | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmThreadCount<br>Daemonthreadcount           | Number of worker threads_DaemonThreadCount                | -                    | Number of daemon threads                           | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkQmThreadCount<br>Threadcount                 | Number of worker threads_ThreadCount                      | -                    | Total number of threads                                | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkConnectionsNumZk<br>NumAliveConnections      | Number of connections\_zk_num_alive_connections            | -                    | Number of current connections                              | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkLatencyZkAvgLatency                          | Latency\_zk_avg_latency                        | ms                    | Average latency in ZooKeeper processing                         | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkLatencyZkMaxLatency                          | Latency\_zk_max_latency                        | ms                    | Maximum latency in ZooKeeper processing                         | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkLatencyZkMinLatency                          | Latency\_zk_min_latency                        | ms                    | Minimum latency in ZooKeeper processing                         | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkDataCount<br>ZkWatchCount                    | Number of znodes\_zk_watch_count                  | -                    | Number of ZooKeeper watches                        | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkDataCount<br>ZkZnodeCount                    | Number of znodes\_zk_znode_count                  | -                    | Number of ZooKeeper znodes                        | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkDataCountZk<br>EphemeralsCount               | Number of znodes\_zk_ephemerals_count              | -                    | Number of ephemeral ZooKeeper nodes                       | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkDataSizeZk<br>ApproximateDataSize            | Data volume\_zk_approximate_data_size          | Byte                  | Volume of data stored in ZooKeeper                           | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkStateZkServerState                           | Node status\_zk_server_state                   | 1: primary, 0: secondary, 2: standalone | ZooKeeper node type                             | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkPacketsZk<br>PacketsReceived                 | Number of received/sent packets\_zk_packets_received           | Packets/s                  | ZooKeeper package receiving rate                     | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkPacketsZkPacketsSent                         | Number of received/sent packets\_zk_packets_sent               | Packets/s                  | ZooKeeper package sending rate                     | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |
| ZkRequestsOutstanding<br>ZkOutstandingRequests | Number of waiting requests\_zk_outstanding_requests         | -                    | Number of waiting requests                              | id4zookeeperzookeeper, <br>host4zookeeperzookeeper |

## Dimension and Parameters

| Parameter | Dimension | Dimension Description | Format |
| :----------------------------- | :---------------------- | :--------------------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4zookeeperzookeeper           | Dimension name of the EMR instance ID       | String-type dimension name, such as id4zookeeperzookeeper              |
| Instances.N.Dimensions.0.Value | id4zookeeperzookeeper           | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4zookeeperzookeeper        | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4zookeeperzookeeper            |
| Instances.N.Dimensions.1.Value | host4zookeeperzookeeper      | Specific node IP in the EMR instance         | Specific node IP, which can be obtained by clicking **Instance** > **Cluster Resources** > **Resource Management** > **Node Private IP** in the [EMR console](https://console.cloud.tencent.com/emr) or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |

## Input Parameter Description

To query the monitoring data of EMR (ZooKeeper), use the following input parameters:

Namespace=QCE/TXMR_ZOOKEEPER
&Instances.N.Dimensions.0.Name=id4zookeeperzookeepe
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4zookeeperzookeeper
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

