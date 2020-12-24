### Druid - Broker

| Metric Name | Unit | Description |
| ------------------------------ | ---- | ------------------------------------------------------------ |
| YGC                            | -   | Young GC count                                                |
| FGC                            | -   | Full GC count                                                 |
| FGCT                           | s    | Full GC time                                             |
| GCT                            | s    | Garbage collection time                                             |
| YGCT                           | s    | Young GC time                                            |
| S0                             | %    | Percentage of used Survivor 0 memory                                    |
| E                              | %    | Percentage of used Eden memory                                          |
| CCS                            | %    | Percentage of memory used by compressed class space                        |
| S1                             | %    | Percentage of used Survivor 1 memory                                    |
| O                              | %    | Percentage of used Old memory                                           |
| M                              | %    | Percentage of used Metaspace memory                                     |
| MemHeapInitM                   | MB   | Size of initial JVM HeapMem                                      |
| MemNonHeapInitM                | MB   | Size of initial JVM NonHeapMem                                   |
| MemHeapMaxM                    | MB   | Size of HeapMemory configured by JVM                                 |
| MemHeapCommittedM              | MB   | Size of HeapMemory currently committed by JVM                        |
| MemHeapUsedM                   | MB   | Size of HeapMemory currently used by JVM                        |
| MemNonHeapCommittedM           | MB   | Size of NonHeapMemory currently committed by JVM                     |
| MemNonHeapUsedM                | MB   | Size of NonHeapMemory currently used by JVM                     |
| ThreadsNew                     | -   | Number of threads in NEW state                                          |
| ThreadsRunnable                | -   | Number of threads in RUNNABLE state                                     |
| ThreadsBlocked                 | -   | Number of threads in BLOCKED state                                      |
| ThreadsWaiting                 | -   | Number of threads in WAITING state                                      |
| ThreadsTimedWaiting            | -   | Number of threads in TIMED_WAITING state                                |
| ThreadsTerminated              | -   | Number of threads in TERMINATED state                                   |
| LogFatal                       | -   | Number of FATAL logs                                            |
| LogError                       | -   | Number of ERROR logs                                            |
| LogWarn                        | -   | Number of WARN logs                                             |
| LogInfo                        | -   | Number of INFO logs                                             |
| jetty.numOpenConnections       | -   | Number of open Jetty connections                                            |
| segment.scan.pending           | -   | Number of segments in queue waiting to be  scanned           |
| broker.query.count             | -   | number of total queries                                      |
| broker.query.success.count     | -   | number of queries successfully processed                     |
| broker.query.failed.count      | -   | number of failed queries                                     |
| broker.query.interrupted.count | -   | number of queries interrupted due to cancellation  or timeout |
| normal.count                   | -   | Number of queries with delay shorter than 1 second                                            |
| abnormal.count                 | -   | Number of queries with delay longer than or equal to 1 second                                           |


### Druid - Coordinator

| Metric Name | Unit | Description |
| ----------------------------- | ----- | ------------------------------------------------------------ |
| segment.assigned.count        | -    | Number of segments loaded into Druid cluster                             |
| segment.moved.count           | -    | Number of segments moved in Druid cluster                           |
| segment.dropped.count         | -    | Number of segments deleted in Druid cluster due to expiration                 |
| segment.deleted.count         | -    | Number of segments deleted in Druid cluster due to rule settings              |
| segment.unneeded.count        | -    | Number of segments deleted in Druid cluster for being marked as "unused"      |
| segment.cost.raw              | ms    | Used in cost balancing. The raw cost of hosting segments.   |
| segment.cost.normalization    | ms    | Used in cost balancing. The normalization of hosting segments. |
| segment.cost.normalized       | ms    | Used in cost balancing. The normalized cost of hosting segments. |
| segment.loadQueue.size        | Bytes | Size in bytes of segments to load.                           |
| segment.loadQueue.failed      | -    | Number of segments that failed to load.                      |
| segment.loadQueue.count       | -    | Number of segments to load.                                  |
| segment.dropQueue.count       | -    | Number of segments to drop.                                  |
| segment.overshadowed.count    | -    | Number of overshadowed segments.                             |
| tier.historical.count         | -    | Number of available historical nodes in each tier.          |
| tier.replication.factor       | -    | Configured maximum replication factor in each tier.         |
| tier.required.capacity        | Bytes | Total capacity in bytes required in each tier.              |
| tier.total.capacity           | Bytes | Total capacity in bytes available in each tier.             |
| compact.task.count            | -    | Number of compaction tasks                                               |
| YGC                           | -    | Young GC count                                                |
| FGC                           | -    | Full GC count                                                 |
| FGCT                          | s     | Full GC time                                             |
| GCT                           | s     | Garbage collection time                                             |
| YGCT                          | s     | Young GC time                                            |
| S0                            | %     | Percentage of used Survivor 0 memory                                    |
| E                             | %     | Percentage of used Eden memory                                          |
| CCS                           | %     | Percentage of memory used by compressed class space                        |
| S1                            | %     | Percentage of used Survivor 1 memory                                    |
| O                             | %     | Percentage of used Old memory                                           |
| M                             | %     | Percentage of used Metaspace memory                                     |
| MemHeapInitM                  | MB    | Size of initial JVM HeapMem                                      |
| MemNonHeapInitM               | MB    | Size of initial JVM NonHeapMem                                   |
| MemHeapMaxM                   | MB    | Size of HeapMemory configured by JVM                                 |
| MemHeapCommittedM             | MB    | Size of HeapMemory currently committed by JVM                        |
| MemHeapUsedM                  | MB    | Size of HeapMemory currently used by JVM                        |
| MemNonHeapCommittedM          | MB    | Size of NonHeapMemory currently committed by JVM                     |
| MemNonHeapUsedM               | MB    | Size of NonHeapMemory currently used by JVM                     |
| ThreadsNew                    | -    | Number of threads in NEW state                                          |
| ThreadsRunnable               | -    | Number of threads in RUNNABLE state                                     |
| ThreadsBlocked                | -    | Number of threads in BLOCKED state                                      |
| ThreadsWaiting                | -    | Number of threads in WAITING state                                      |
| ThreadsTimedWaiting           | -    | Number of threads in TIMED_WAITING state                                |
| ThreadsTerminated             | -    | Number of threads in TERMINATED state                                   |
| LogFatal                      | -    | Number of FATAL logs                                            |
| LogError                      | -    | Number of ERROR logs                                            |
| LogWarn                       | -    | Number of WARN logs                                             |
| LogInfo                       | -    | Number of INFO logs                                             |
| segment.size                  | Bytes | Total size of used segments in a data source. Emitted only for data sources to which at least one used segment  belongs. |
| segment.count                 | -    | Number of used segments belonging to a data source. Emitted only for data sources to which at least one used segment  belongs. |
| segment.unavailable.count     | -    | Number of segments (not including  replicas) left to load until segments that should be loaded in the cluster are available for queries. |
| segment.underReplicated.count | -    | Number of segments (including replicas)  left to load until segments that should be loaded in the cluster are  available for queries. |
| jetty.numOpenConnections      | -    | Number of open Jetty connections                                            |

 

### Druid - Historical

| Metric Name | Unit | Description |
| ---------------------------------- | ----- | ------------------------------------------------------------ |
| YGC                                | -    | Young GC count                                                |
| FGC                                | -    | Full GC count                                                 |
| FGCT                               | s     | Full GC time                                             |
| GCT                                | s     | Garbage collection time                                             |
| YGCT                               | s     | Young GC time                                            |
| S0                                 | %     | Percentage of used Survivor 0 memory                                    |
| E                                  | %     | Percentage of used Eden memory                                          |
| CCS                                | %     | Percentage of memory used by compressed class space                        |
| S1                                 | %     | Percentage of used Survivor 1 memory                                    |
| O                                  | %     | Percentage of used Old memory                                           |
| M                                  | %     | Percentage of used Metaspace memory                                     |
| MemHeapInitM                       | MB    | Size of initial JVM HeapMem                                      |
| MemNonHeapInitM                    | MB    | Size of initial JVM NonHeapMem                                   |
| MemHeapMaxM                        | MB    | Size of HeapMemory configured by JVM                                 |
| MemHeapCommittedM                  | MB    | Size of HeapMemory currently committed by JVM                        |
| MemHeapUsedM                       | MB    | Size of HeapMemory currently used by JVM                        |
| MemNonHeapCommittedM               | MB    | Size of NonHeapMemory currently committed by JVM                     |
| MemNonHeapUsedM                    | MB    | Size of NonHeapMemory currently used by JVM                     |
| ThreadsNew                         | -    | Number of threads in NEW state                                          |
| ThreadsRunnable                    | -    | Number of threads in RUNNABLE state                                     |
| ThreadsBlocked                     | -    | Number of threads in BLOCKED state                                      |
| ThreadsWaiting                     | -    | Number of threads in WAITING state                                      |
| ThreadsTimedWaiting                | -    | Number of threads in TIMED_WAITING state                                |
| ThreadsTerminated                  | -    | Number of threads in TERMINATED state                                   |
| LogFatal                           | -    | Number of FATAL logs                                            |
| LogError                           | -    | Number of ERROR logs                                            |
| LogWarn                            | -    | Number of WARN logs                                             |
| LogInfo                            | -    | Number of INFO logs                                             |
| jetty.numOpenConnections           | -    | Number of open Jetty connections                                            |
| segment.scan.pending               | -    | Number of segments in queue waiting to be  scanned           |
| segment.max                        | Bytes | Maximum byte limit available for segments                    |
| segment.pendingdelete              | Bytes | On-disk size in bytes of segments that  are waiting to be cleared out |
| historical.query.count             | -    | Total number of historical queries                                         |
| historical.query.success.count     | -    | Total number of historical query successes                                       |
| historical.query.failed.count      | -    | Total number of historical query failures                                       |
| historical.query.interrupted.count | -    | Total number of historical query interruptions                                     |
| normal.count                       | -    | Number of queries with delay shorter than 1 second                                            |
| abnormal.count                     | -    | Number of queries with delay longer than or equal to 1 second                                           |


### Druid - MiddleManager

| Metric Name | Unit | Description |
| ------------------------ | ---- | ---------------------------------------- |
| YGC                      | -   | Young GC count                            |
| FGC                      | -   | Full GC count                             |
| FGCT                     | s    | Full GC time                         |
| GCT                      | s    | Garbage collection time                         |
| YGCT                     | s    | Young GC time                        |
| S0                       | %    | Percentage of used Survivor 0 memory                |
| E                        | %    | Percentage of used Eden memory                      |
| CCS                      | %    | Percentage of memory used by compressed class space    |
| S1                       | %    | Percentage of used Survivor 1 memory                |
| O                        | %    | Percentage of used Old memory                       |
| M                        | %    | Percentage of used Metaspace memory                 |
| MemHeapInitM             | MB   | Size of initial JVM HeapMem                  |
| MemNonHeapInitM          | MB   | Size of initial JVM NonHeapMem               |
| MemHeapMaxM              | MB   | Size of HeapMemory configured by JVM             |
| MemHeapCommittedM        | MB   | Size of HeapMemory currently committed by JVM    |
| MemHeapUsedM             | MB   | Size of HeapMemory currently used by JVM    |
| MemNonHeapCommittedM     | MB   | Size of NonHeapMemory currently committed by JVM |
| MemNonHeapUsedM          | MB   | Size of NonHeapMemory currently used by JVM |
| ThreadsNew               | -   | Number of threads in NEW state                      |
| ThreadsRunnable          | -   | Number of threads in RUNNABLE state                 |
| ThreadsBlocked           | -   | Number of threads in BLOCKED state                  |
| ThreadsWaiting           | -   | Number of threads in WAITING state                  |
| ThreadsTimedWaiting      | -   | Number of threads in TIMED_WAITING state            |
| ThreadsTerminated        | -   | Number of threads in TERMINATED state               |
| LogFatal                 | -   | Number of FATAL logs                        |
| LogError                 | -   | Number of ERROR logs                        |
| LogWarn                  | -   | Number of WARN logs                         |
| LogInfo                  | -   | Number of INFO logs                         |
| jetty.numOpenConnections | -   | Number of open Jetty connections                        |

 

### Druid - Overlord

 

| Metric Name | Unit | Description |
| ------------------------ | ---- | ---------------------------------------- |
| YGC                      | -   | Young GC count                            |
| FGC                      | -   | Full GC count                             |
| FGCT                     | s    | Full GC time                         |
| GCT                      | s    | Garbage collection time                         |
| YGCT                     | s    | Young GC time                        |
| S0                       | %    | Percentage of used Survivor 0 memory                |
| E                        | %    | Percentage of used Eden memory                      |
| CCS                      | %    | Percentage of memory used by compressed class space    |
| S1                       | %    | Percentage of used Survivor 1 memory                |
| O                        | %    | Percentage of used Old memory                       |
| M                        | %    | Percentage of used Metaspace memory                 |
| MemHeapInitM             | MB   | Size of initial JVM HeapMem                  |
| MemNonHeapInitM          | MB   | Size of initial JVM NonHeapMem               |
| MemHeapMaxM              | MB   | Size of HeapMemory configured by JVM             |
| MemHeapCommittedM        | MB   | Size of HeapMemory currently committed by JVM    |
| MemHeapUsedM             | MB   | Size of HeapMemory currently used by JVM    |
| MemNonHeapCommittedM     | MB   | Size of NonHeapMemory currently committed by JVM |
| MemNonHeapUsedM          | MB   | Size of NonHeapMemory currently used by JVM |
| ThreadsNew               | -   | Number of threads in NEW state                      |
| ThreadsRunnable          | -   | Number of threads in RUNNABLE state                 |
| ThreadsBlocked           | -   | Number of threads in BLOCKED state                  |
| ThreadsWaiting           | -   | Number of threads in WAITING state                  |
| ThreadsTimedWaiting      | -   | Number of threads in TIMED_WAITING state            |
| ThreadsTerminated        | -   | Number of threads in TERMINATED state               |
| LogFatal                 | -   | Number of FATAL logs                        |
| LogError                 | -   | Number of ERROR logs                        |
| LogWarn                  | -   | Number of WARN logs                         |
| LogInfo                  | -   | Number of INFO logs                         |
| jetty.numOpenConnections | -   | Number of open Jetty connections                        |

### Druid - Router

| Metric Name | Unit | Description |
| ------------------------ | ---- | ---------------------------------------- |
| YGC                      | -   | Young GC count                            |
| FGC                      | -   | Full GC count                             |
| FGCT                     | s    | Full GC time                         |
| GCT                      | s    | Garbage collection time                         |
| YGCT                     | s    | Young GC time                        |
| S0                       | %    | Percentage of used Survivor 0 memory                |
| E                        | %    | Percentage of used Eden memory                      |
| CCS                      | %    | Percentage of memory used by compressed class space    |
| S1                       | %    | Percentage of used Survivor 1 memory                |
| O                        | %    | Percentage of used Old memory                       |
| M                        | %    | Percentage of used Metaspace memory                 |
| MemHeapInitM             | MB   | Size of initial JVM HeapMem                  |
| MemNonHeapInitM          | MB   | Size of initial JVM NonHeapMem               |
| MemHeapMaxM              | MB   | Size of HeapMemory configured by JVM             |
| MemHeapCommittedM        | MB   | Size of HeapMemory currently committed by JVM    |
| MemHeapUsedM             | MB   | Size of HeapMemory currently used by JVM    |
| MemNonHeapCommittedM     | MB   | Size of NonHeapMemory currently committed by JVM |
| MemNonHeapUsedM          | MB   | Size of NonHeapMemory currently used by JVM |
| ThreadsNew               | -   | Number of threads in NEW state                      |
| ThreadsRunnable          | -   | Number of threads in RUNNABLE state                 |
| ThreadsBlocked           | -   | Number of threads in BLOCKED state                  |
| ThreadsWaiting           | -   | Number of threads in WAITING state                  |
| ThreadsTimedWaiting      | -   | Number of threads in TIMED_WAITING state            |
| ThreadsTerminated        | -   | Number of threads in TERMINATED state               |
| LogFatal                 | -   | Number of FATAL logs                        |
| LogError                 | -   | Number of ERROR logs                        |
| LogWarn                  | -   | Number of WARN logs                         |
| LogInfo                  | -   | Number of INFO logs                         |
| jetty.numOpenConnections | -   | Number of open Jetty connections                        |

 
