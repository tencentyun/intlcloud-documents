### Presto - overview

| Metric Name | Unit | Description |
| -------------------------------- | -------- | ------------------ |
| Active                           | -       | Number of active nodes       |
| Total                            | -       | Total number of nodes         |
| Failed                           | -       | Number of failed nodes       |
| RunningQueries                   | -       | Total number of running queries |
| QueuedQueries                    | -       | Total number of waiting queries |
| FailedQueries.OneMinute.Count    | Queries/min   | Total number of failed queries     |
| AbandonedQueries.OneMinute.Count | Queries/min   | Total number of aborted queries     |
| CanceledQueries.OneMinute.Count  | Queries/min   | Total number of cancelled queries     |
| CompletedQueries.OneMinute.Count | Queries/min   | Total number of completed queries     |
| StartedQueries.OneMinute.Count    | Queries/min   | Total number of started queries     |
| SubmittedQueries.OneMinute.Count | Queries/min   | Total number of submitted queries   |
| InputDataSize.OneMinute.Rate     | GB/min   | Data input rate       |
| OutputDataSize.OneMinute.Rate     | GB/min   | Data output rate       |

### Presto - Worker

| Metric Name | Unit | Description |
| ----------------------------- | -------- | --------------------------------------- |
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
| InputDataSize.OneMinute.Rate  | GB/min   | Data input rate                            |
| OutputDataSize.OneMinute.Rate     | GB/min   | Data output rate       |
| PeakThreadCount                               | -       | Peak number of threads        |
| ThreadCount                   | -       | Number of threads                             |
| DaemonThreadCount                             | -       | Number of background threads                                         |
| Uptime                             | s        | Process run time      |
| StartTime                     | s        | Process start time   |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptor      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |

### Presto - Coordinator

| Metric Name | Unit | Description |
| ----------------------- | -------- | --------------------------------------- |
| YGC                                | -       | Young GC count            |
| FGC                                | -       | Full GC count            |
| FGCT                                    | s        | Full GC time                           |
| GCT                                           | s       | Garbage collection time                                     |
| YGCT                    | s        | Young GC time                       |
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
| PeakThreadCount                               | -       | Peak number of threads        |
| ThreadCount                   | -       | Number of threads                             |
| DaemonThreadCount                             | -       | Number of background threads                                         |
| Uptime                             | s        | Process run time      |
| StartTime                     | s        | Process start time   |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptor      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |

 
