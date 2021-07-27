### Hive - HiveMetaStore

| Metric Name | Unit | Description |
| -------------------------------------------------- | -------- | --------------------------------------- |
| GC count_YGC                                         | -       | Number of young GCs                         |
| GC count_FGC                                         | -       | Number of full GCs                           |
| GC time_FGCT                                        | s        | Time taken by full GCs                    |
| GC time_GCT                                         | s        | Time taken by GCs                        |
| GC time_YGCT                                        | s        | Time taken by young GCs                       |
| Memory utilization_S0                                    | %        | Memory utilization of survivor 0 space                |
| Memory utilization_E                                     | %        | Memory utilization of eden space   |
| Memory utilization_CCS                                   | %        | Memory utilization of compressed class space  |
| Memory utilization_S1                                    | %        | Memory utilization of survivor 1 space    |
| Memory utilization_O                                     | %        | Memory utilization of old space                      |
| Memory utilization_M                                     | %        | Memory utilization of metaspace space   |
| HiveMetaStore_JVM memory_MemHeapUsedM                 | MB       | Size of HeapMemory used by the JVM    |
| HiveMetaStore_JVM memory_MemHeapCommittedM            | MB       | Size of HeapMemory committed by the JVM    |
| HiveMetaStore_JVM memory_MemHeapMaxM                  | MB       | Size of HeapMemory configured for the JVM              |
| HiveMetaStore_JVM memory_MemHeapInitM                 | MB       | Initial size of HeapMem for the JVM               |
| HiveMetaStore_JVM memory_MemNonHeapUsedM              | MB       | Size of NonHeapMemory used by the JVM |
| HiveMetaStore_JVM memory_MemNonHeapCommittedM         | MB       | Size of NonHeapMemory committed by the JVM     |
| HiveMetaStore_JVM memory_MemNonHeapInitM              | MB       | Initial size of NonHeapMemory for the JVM           |
| HiveMetaStore_file descriptor count_MaxFileDescriptorCount  | -     | Number of open file descriptors                   |
| HiveMetaStore_file descriptor count_OpenFileDescriptorCount | -       | Maximum number of file descriptors                     |
| HiveMetaStore_CPU utilization_ProcessCpuLoad             | %        | Process CPU utilization                          |
| HiveMetaStore_CPU utilization_SystemCpuLoad              | %        | System CPU utilization                          |
| HiveMetaStore_worker thread count_DaemonThreadCount         | -       | Number of daemon threads                           |
| HiveMetaStore_worker thread_ThreadCount               | -       | Total number of threads                                |
| HiveMetaStore_cumulative CPU usage time_ProcessCpuTime       | ms       | Cumulative CPU usage time                         |
| HiveMetaStore_process run time_Uptime                  | s        | Process run time                            |
| HiveMetaStore_GC extra sleep time per second_ExtraSleepTime    | ms/s       | GC extra pause time per second                      |
| HiveMetaStore_CPU usage time_CPURate              | %        | Percentage of CPU usage time                         |

### Hive - HiveServer2

| Metric Name | Unit | Description |
| ------------------------------------ | -------- | ------------------------------------------------------------ |
| GC count_YGC                           | -       | Number of young GCs                                                |
| GC count_FGC                           | -       | Number of full GCs                                                 |
| GC time_FGCT                          | s        | Time taken by full GCs                                             |
| GC time_GCT                           | s        | Time taken by GCs                                            |
| GC time_YGCT                          | s        | Time taken by young GCs                                            |
| Memory utilization_S0                      | %        | Memory utilization of survivor 0 space                                     |
| Memory utilization_E                       | %        | Memory utilization of eden space                                          |
| Memory utilization_CCS                     | %        | Memory utilization of compressed class space                        |
| Memory utilization_S1                      | %        | Memory utilization of survivor 1 space                                     |
| Memory utilization_O                       | %        | Memory utilization of old space                                           |
| Memory utilization_M                       | %        | Memory utilization of  metaspace space                                     |
| JVM memory_MemNonHeapUsedM              | MB       | Amount of NonHeapMemory used by the JVM                        |
| JVM memory_MemNonHeapCommittedM         | MB       | Amount of NonHeapMemory committed by the JVM                        |
| JVM memory_MemHeapUsedM                 | MB       | Amount of HeapMemory used by the JVM                           |
| JVM memory_MemHeapCommittedM            | MB       | Amount of HeapMemory committed by the JVM                           |
| JVM memory_MemHeapMaxM                  | MB       | Amount of HeapMemory configured for the JVM                                 |
| JVM memory_MemHeapInitM                 | MB       | Initial amount of HeapMem for the JVM                                      |
| JVM memory_MemNonHeapInitM              | MB       | Initial amount of NonHeapMem for the JVM                                    |
| CPU utilization_ProcessCpuLoad             | %        | CPU utilization                                                   |
| File descriptor count_MaxFileDescriptorCount  | -       | Maximum number of file descriptors                                             |
| File descriptor count_OpenFileDescriptorCount | -       | Number of open file descriptors                                           |
| Cumulative CPU usage time_ProcessCpuTime       | ms       | Cumulative CPU usage time                                             |
| Process run time_Uptime                  | s        | Process run time                                                 |
| Worker thread count_DaemonThreadCount         | -       | Number of daemon threads                                                |
| Worker thread count_ThreadCount               | -       | Total number of threads                                                     |
| H2_driver execution latency_99th_percentile    | ms       | 99th percentile latency of driver execution                                          |
| H2_driver execution latency_Avg                | ms       | Average latency of driver execution                                       |
| H2_process open connections_NumOpenConnections | -       | Number of open connections                                                 |
| H2_async thread pool count_PoolSize           | -       | Number of HS2 async thread pools                                        |
| H2_async operation queue count_QueueSize        | -       | Number of HS2 async operation queues                                      |
| H2_GC extra sleep time per second_ExtraSleepTime | ms/s     | GC extra pause time per second                                           |
| MaxFileDescriptorCount               | -       | Maximum number of file descriptors                                             |
| File descriptor count_OpenFileDescriptorCount | -       | Number of open file descriptors                                           |
| H2_closed operation count_Closed         | Operations/s     | Number of closed operations per second                                               |
| H2_finished operation count_Finished           | Operations/s     | Number of finished operations per second                                              |
| H2_canceled operation count_Canceled           | Operations/s     | Number of canceled operations per second                                              |
| H2_erroneous operation count_Error              | Operations/s     | Number of erroneous operations per second                                               |
| H2_JVM heap memory utilization_MemHeapUsedRate   | %        | Percentage of the amount of HeapMemory used by the JVM in the amount of HeapMemory configured for the JVM |
| H2_CPU usage time per second_CPURate           | s        | Percentage of CPU usage time                                              |

### Hive - HiveWebHcat

| Metric Name | Unit | Description |
| ---------------- | -------- | ------------------------------------- |
| GC count_YGC       | -       | Number of young GCs                         |
| GC count_FGC       | -       | Number of full GCs                          |
| GC time_FGCT      | s        | Time taken by full GCs                      |
| GC time_GCT       | s        | Time taken by GCs                      |
| GC time_YGCT      | s        | Time taken by young GCs                     |
| Memory utilization_S0  | %        | Memory utilization of survivor 0 space             |
| Memory utilization_E   | %        | Memory utilization of eden space                   |
| Memory utilization_CCS | %        | Memory utilization of compressed class space |
| Memory utilization_S1  | %        | Memory utilization of survivor 1 space             |
| Memory utilization_O   | %        | Memory utilization of old space                    |
| Memory utilization_M   | %        | Memory utilization of metaspace space              |

 
