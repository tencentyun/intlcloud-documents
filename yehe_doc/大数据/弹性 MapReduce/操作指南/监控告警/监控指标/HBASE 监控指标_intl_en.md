### HBase - overview

| Metric Name | Unit | Description |
| ----------------------- | -------- | -------------------------- |
| ritCount                | -       | Number of cluster regions in RIT state  |
| ritCountOverThreshold   | -       | Number of cluster regions in RIT state  |
| ritOldestAge            | ms       | Cluster RIT time              |
| averageLoad             | -       | Average number of regions per RS |
| numRegionServers        | -       | Number of cluster RSs               |
| numDeadRegionServers    | -       | Number of cluster RSs               |
| receivedBytes           | Bytes/s  | Number of cluster reads/writes               |
| sentBytes               | Bytes/s  | Number of cluster reads/writes               |
| clusterRequests | Requests/s | Total number of requests in cluster |
| Assign_num_ops      | -       | Cluster assignment manager operations |
| BulkAssign_num_ops      | -       | Cluster assignment manager operations |
| BalancerCluster_num_ops | -       | Number of cluster load balancing operations           |
| mergePlanCount          | -       | Cluster plans                  |
| splitPlanCount          | -       | Cluster plans                  |

### HBase - HMaster


| Metric Name | Unit | Description |
| ------------------------------ | -------- | -------------- |
| YGC                                | -       | GC count            |
| FGC                                | -       | GC count            |
| FGCT                               | s        | GC time            |
| GCT                                | s        | GC time            |
| YGCT                               | s        | GC time            |
| S0                                 | %        | Memory area proportion      |
| E                                  | %        | Memory area proportion      |
| CCS                                | %        | Memory area proportion      |
| S1                                 | %        | Memory area proportion      |
| O                                  | %        | Memory area proportion      |
| M                                  | %        | Memory area proportion      |
| LogFatal                       | -       | Number of JVM logs     |
| LogError                       | -       | Number of JVM logs     |
| LogWarn                        | -       | Number of JVM logs     |
| LogInfo                        | -       | Number of JVM logs     |
| MemNonHeapUsedM                | MB       | JVM memory         |
| MemNonHeapCommittedM                          | MB       | JVM memory                                             |
| MemNonHeapMaxM                 | MB       | JVM memory         |
| MemHeapUsedM                   | MB       | JVM memory         |
| MemHeapCommittedM              | MB       | JVM memory         |
| MemHeapMaxM                    | MB       | JVM memory         |
| MemMaxM                            | MB       | JVM memory           |
| ThreadsNew                     | -       | Number of JVM threads     |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
| numOpenConnections                | -       | Number of RPC connections         |
| FailedSanityCheckException        | -       | Number of RPC exceptions       |
| NotServingRegionException         | -       | Number of RPC exceptions       |
| OutOfOrderScannerNextException    | -       | Number of RPC exceptions       |
| RegionMovedException              | -       | Number of RPC exceptions       |
| RegionTooBusyException         | -       | Number of RPC exceptions       |
| UnknownScannerException           | -       | Number of RPC exceptions       |
| numCallsInPriorityQueue        | -       | Number of RPC queue requests     |
| numCallsInReplicationQueue        | -       | Number of RPC queue requests     |
| masterActiveTime               | s        | Process start time   |
| masterStartTime                | s        | Process start time   |

### HBase - RegionServer

| Metric Name | Unit | Description |
| --------------------------------- | -------- | ------------------ |
| YGC                                | -       | GC count            |
| FGC                                | -       | GC count            |
| FGCT                               | s        | GC time            |
| GCT                                | s        | GC time            |
| YGCT                               | s        | GC time            |
| S0                                 | %        | Memory area proportion      |
| E                                  | %        | Memory area proportion      |
| CCS                                | %        | Memory area proportion      |
| S1                                 | %        | Memory area proportion      |
| O                                  | %        | Memory area proportion      |
| M                                  | %        | Memory area proportion      |
| LogFatal                       | -       | Number of JVM logs     |
| LogError                       | -       | Number of JVM logs     |
| LogWarn                        | -       | Number of JVM logs     |
| LogInfo                        | -       | Number of JVM logs     |
| MemNonHeapUsedM                | MB       | JVM memory         |
| MemNonHeapCommittedM                          | MB       | JVM memory                                             |
| MemNonHeapMaxM                 | MB       | JVM memory         |
| MemHeapUsedM                   | MB       | JVM memory         |
| MemHeapCommittedM              | MB       | JVM memory         |
| MemHeapMaxM                    | MB       | JVM memory         |
| MemMaxM                            | MB       | JVM memory           |
| ThreadsNew                     | -       | Number of JVM threads     |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
| averageRegionSize                 | Byte | Average region size |
| regionCount                       | -       | Number of regions       |
| percentFilesLocalSecondaryRegions | %        | Region replica localization |
| authenticationFailures            | -       | Number of RPC authentications       |
| authenticationSuccesses            | -       | Number of RPC authentications       |
| numOpenConnections                | -       | Number of RPC connections         |
| FailedSanityCheckException        | -       | Number of RPC exceptions       |
| NotServingRegionException         | -       | Number of RPC exceptions       |
| OutOfOrderScannerNextException    | -       | Number of RPC exceptions       |
| RegionMovedException              | -       | Number of RPC exceptions       |
| RegionTooBusyException            | -       | Number of RPC exceptions       |
| UnknownScannerException           | -       | Number of RPC exceptions       |
| numActiveHandler                  | -       | Number RPC handles         |
| numCallsInPriorityQueue           | -       | Number of RPC queue requests     |
| numCallsInReplicationQueue        | -       | Number of RPC queue requests     |
| numCallsInGeneralQueue            | -       | Number of RPC queue requests     |
| hlogFileCount                     | -       | Number of WAL files       |
| hlogFileSize                      | Bytes     | WAL file size       |
| memStoreSize                      | MB       | Memstore size      |
| storeCount                        | -       | Number of stores |
| storeFileCount                    | -       | Number of Storefiles    |
| storeFileSize                     | MB       | Storefile size     |
| flushedCellsSize                  | Bytes/s  | Disk write rate         |
| Append_mean                       | ms       | Average delay           |
| Replay_mean                       | ms       | Average delay           |
| Get_mean                          | ms       | Average delay           |
| updatesBlockedTime                                       | ms       | Average delay           |
| FlushTime_num_ops                 | -       | Number of RS disk writes      |
| splitQueueLength                  | -       | Number of operation queue requests     |
| compactionQueueLength             | -       | Number of operation queue requests     |
| flushQueueLength                  | -       | Number of operation queue requests     |
| Replay_num_ops                    | -       | Number of Replay operations    |
| slowAppendCount                   | -       | Number of slow operations         |
| slowDeleteCount                   | -       | Number of slow operations         |
| slowGetCount                      | -       | Number of slow operations         |
| slowIncrementCount                | -       | Number of slow operations         |
| slowPutCount                      | -       | Number of slow operations         |
| splitRequestCount                 | -       | Split requests         |
| splitSuccessCount                 | -       | Split requests         |
| blockCacheCount                   | -       | Number of cache blocks         |
| blockCacheHitCount                | -       | Number of cache blocks         |
| blockCacheMissCount                 | -       | Number of cache blocks         |
| blockCacheExpressHitPercent       | %        | Cache read hit rate       |
| blockCacheSize                    | Byte     | Memory size used by cache block |
| staticBloomSize                   | Bytes     | Index size           |
| staticIndexSize                   | Bytes     | Index size           |
| storeFileIndexSize                | Bytes     | Index size           |
| receivedBytes                     | Bytes/s  | Read/write traffic           |
| sentBytes                         | Bytes/s  | Read/write traffic           |
| Total                             | Requests/s     | Number of read/write requests         |
| Read | Requests/s     | Number of read/write requests         |
| Write                                   | Requests/s     | Number of read/write requests         |
| Append_num_ops                             | Requests/s     | Number of read/write requests         |
| mutationsWithoutWALCount          | -       | Number of mutations       |
| mutationsWithoutWALSize           | Bytes     | Mutation size      |
| regionServerStartTime             | s        | Process start time   |
| 99th_percentile   | ms   | 99% request processing latency   |
| 99.9th_percentile | ms   | 99.9% request processing latency |
| 99th_percentile   | ms   | 99% request queueing latency   |
| 99.9th_percentile | ms   | 99.9% request queueing latency |


