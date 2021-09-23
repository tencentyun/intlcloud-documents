>!Currently, only PrestoSQL v322, PrestoSQL v350 and above supports PrestoSQL metrics.


### PrestoSQL - Overview

| Metric Name | Unit | Description |
| ----------------------- | -------- | ------------------ |
| Active                  | -       | Number of active nodes       |
| Total                   | -       | Total number of nodes         |
| Failed                  | -       | Number of failed nodes       |
| RunningQueries          | -       | Number of running queries |
| QueuedQueries           | -       | Number of queued queries |
| FailedQueries           | Queries/min   | Number of failed queries     |
| AbandonedQueries        | Queries/min   | Number of abandoned queries     |
| CanceledQueries         | Queries/min   | Number of canceled queries     |
| SubmittedQueries        | Queries/min   | Number of submitted queries   |
| CompletedQueries        | Queries/min   | Number of completed queries     |
| StartedQueries          | Queries/min   | Number of started queries   |
| InputDataSizeOneMinute  | GB/min   | Data input rate      |
| OutputDataSizeOneMinute | GB/min   | Data output rate       |

### PrestoSQL - Coordinator

| Metric Name | Unit | Description |
| ----------------------- | -------- | --------------------------------------- |
| YGC                                | -       | Number of young GCs            |
| FGC                                | -       | Number of full GCs            |
| FGCT                                    | s        | Time taken by full GCs                           |
| GCT                                           | s       | Time taken by GCs                                     |
| YGCT                    | s        | Time taken by young GCs                       |
| S0                                             | %        | Percentage of used survivor 0 memory                                   |
| E                                             | %        | Percentage of used eden memory                                   |
| CCS                                           | %        | Percentage of used compressed class space memory             |
| S1                      | %        | Percentage of used survivor 1 memory                |
| O                                             | %        | Percentage of used old memory                                   |
| M                                             | %        | Percentage of used metaspace memory                                   |
| MemNonHeapUsedM | MB | Amount of NonHeapMemory used by the JVM |
| MemNonHeapCommittedM | MB | Amount of NonHeapMemory committed by the JVM |
| MemHeapUsedM | MB | Amount of HeapMemory used by the JVM |
| MemHeapCommittedM | MB | Amount of HeapMemory committed by the JVM |
| MemHeapMaxM | MB | Amount of HeapMemory configured for the JVM |
| MemHeapInitM | MB | Initial amount of HeapMemory for the JVM |
| MemNonHeapInitM | MB | Initial amount of NonHeapMemory for the JVM |
| PeakThreadCount | - | Peak number of threads |
| ThreadCount                        | -       | Total number of threads        |
| DaemonThreadCount                  | -       | Number of daemon threads        |
| Uptime                             | s        | Process run time      |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptors      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |

### PrestoSQL - Worker

| Metric Name | Unit | Description |
| ----------------------------- | -------- | --------------------------------------- |
| YGC | - | Number of young GCs |
| FGC | - | Number of full GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |
| YGCT | s | Time taken by young GCs |
| S0 | % | Percentage of used survivor 0 memory |
| E | % | Percentage of used eden memory |
| CCS | % | Percentage of used compressed class space memory |
| S1 | % | Percentage of used survivor 1 memory |
| O | % | Percentage of used old memory |
| M | % | Percentage of used metaspace memory |
| MemNonHeapUsedM | MB | Amount of NonHeapMemory used by the JVM |
| MemNonHeapCommittedM | MB | Amount of NonHeapMemory committed by the JVM |
| MemHeapUsedM | MB | Amount of HeapMemory used by the JVM |
| MemHeapCommittedM | MB | Amount of HeapMemory committed by the JVM |
| MemHeapMaxM | MB | Amount of HeapMemory configured for the JVM |
| MemHeapInitM | MB | Initial amount of HeapMem for the JVM |
| MemNonHeapInitM | MB | Initial amount of NonHeapMem for the JVM |
| InputDataSize.OneMinute.Rate  | GB/min   | Data input rate                            |
| OutputDataSize.OneMinute.Rate | GB/min   | Data output rate                            |
| PeakThreadCount | - | Peak number of threads |
| ThreadCount                        | -       | Total number of threads        |
| DaemonThreadCount                  | -       | Number of daemon threads        |
| Uptime                             | s        | Process run time      |
| MaxFileDescriptorCount               | -       | Maximum number of file descriptors                                             |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |

 
