
### ZooKeeper

| Metric Name | Unit | Description |
| ----------------------------- | --------------------- | --------------------------------------- |
| YGC                                | -       | Young GC count            |
| FGC                                | -       | Full GC count            |
| FGCT                                    | s        | Full GC time                           |
| GCT                                           | s       | Garbage collection time                                     |
| YGCT | s | Young GC time |
| S0                                             | %        | Percentage of used Survivor 0 memory                                   |
| E                                             | %        | Percentage of used Eden memory                                   |
| CCS                                           | %        | Percentage of memory used by compressed class space             |
| S1                                             | %        | Percentage of used Survivor 1 memory                                   |
| O                                             | %        | Percentage of used Old memory                                   |
| M                                             | %        | Percentage of used Metaspace memory                                   |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently used by JVM |
| MemNonHeapCommittedM          | MB | Size of NonHeapMemory currently committed by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently used by JVM |
| MemHeapCommittedM       | MB | Size of HeapMemory currently committed by JVM |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemHeapInitM                  | MB                    | Size of initial JVM HeapMem                 |
| MemNonHeapInitM               | MB                    | Size of initial JVM NonHeapMem |
| ProcessCpuLoad                 | %        | CPU utilization       |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptor      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |
| zk_max_file_descriptor_count | -       | Maximum number of file descriptor      |
| zk_open_file_descriptor_count | -                    | Number of opened file descriptors                      |
| ProcessCpuTime                     | ms       | Cumulative CPU usage time   |
| Uptime                             | s        | Process run time      |
| DaemonThreadCount                  | -       | Number of Daemon threads        |
| ThreadCount                        | -       | Total number of threads        |
| zk_num_alive_connections      | -                    | Number of current connections |
| zk_avg_latency                | ms                    | Average delay in ZooKeeper processing                         |
| zk_max_latency                | ms                    | Maximum delay in ZooKeeper processing                        |
| zk_min_latency                | ms                    | Minimum delay in ZooKeeper processing                         |
| zk_watch_count                | -                   | Number of ZooKeeper watches                        |
| zk_znode_count                | -                    | Number of ZooKeeper znodes                        |
| zk_ephemerals_count           | -                    | Number of temporary ZooKeeper nodes                       |
| zk_approximate_data_size      | Byte                  | Volume of data stored in ZooKeeper                           |
| zk_server_state               | 1: master, 0: slave, 2: single server | ZooKeeper node type                             |
| zk_packets_received           | Packets/s                  | ZooKeeper package receiving rate                     |
| zk_packets_sent               | Packets/s                  | ZooKeeper package sending rate                     |
| zk_outstanding_requests       | -                    | Number of waiting requests                              |
