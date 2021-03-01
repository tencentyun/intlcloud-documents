### YARN - overview

| Metric Name | Unit | Description |
| :--------------------------- | :------- | ---------------- |
| NumActiveNMs                 | -       | Number of nodes |
| NumDecommissionedNMs         | -       | Number of nodes |
| NumLostNMs                   | -       | Number of nodes |
| NumUnhealthyNMs              | -       | Number of nodes |
| AllocatedVCores                | -       | Number of CPU cores         |
| ReservedVCores               | -       | Number of CPU cores        |
| AvailableVCores                | -       | Number of CPU cores         |
| PendingVCores                | -       | Number of CPU cores      |
| AppsSubmitted                | -       | Total number of applications         |
| AppsRunning                | -       | Total number of applications         |
| AppsPending                | -       | Total number of applications         |
| AppsCompleted                | -       | Total number of applications         |
| AppsKilled                | -       | Total number of applications         |
| AppsFailed                | -       | Total number of applications         |
| ActiveApplications                | -       | Total number of applications         |
| running_0                | -       | Total number of applications         |
| running_60                | -       | Total number of applications         |
| running_300                | -       | Total number of applications         |
| running_1440                | -       | Total number of applications         |
| AllocatedMB                  | MB       | Memory size         |
| AvailableMB                  | MB       | Memory size         |
| PendingMB                    | MB       | Memory size         |
| ReservedMB                   | MB       | Memory size         |
| AllocatedContainers            | -       | Number of containers         |
| PendingContainers            | -       | Number of containers         |
| ReservedContainers           | -       | Number of containers         |
| AggregateContainersAllocated | -       | Number of allocated containers |
| AggregateContainersReleased | -       | Number of released containers |
| ActiveUsers                  | -       | Number of users           |
| AMLaunchDelayNumOps    | -   | Number of launched AMs           |
| AMLaunchDelayAvgTime   | ms   | Average time for RM to launch AM   |
| AMRegisterDelayNumOps  | -   | Total number of registered AMs         |
| AMRegisterDelayAvgTime | ms   | Average time for AM to register with RM |


### YARN - ResourceManager

| Metric Name | Unit | Description |
| :------------------------- | :------- | ------------------ |
| RpcAuthenticationFailures  | -       | Number of RPC authentications     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentications     |
| RpcAuthorizationFailures   | -       | Number of RPC authentications     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentications     |
| ReceivedBytes              | Bytes/s  | Volume of data received by RPC |
| SentBytes                  | Bytes/s  | Volume of data sent by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
| RpcAuthenticationFailures  | -       | Number of RPC authentications     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentications     |
| RpcAuthorizationFailures   | -       | Number of RPC authentications     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentications     |
| ReceivedBytes              | Bytes/s  | Volume of data received by RPC |
| SentBytes                  | Bytes/s  | Volume of data sent by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
| RpcAuthenticationFailures  | -       | Number of RPC authentications     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentications     |
| RpcAuthorizationFailures   | -       | Number of RPC authentications     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentications     |
| ReceivedBytes              | Bytes/s  | Volume of data received by RPC |
| SentBytes                  | Bytes/s  | Volume of data sent by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
| RpcAuthenticationFailures  | -       | Number of RPC authentications     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentications     |
| RpcAuthorizationFailures   | -       | Number of RPC authentications     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentications     |
| ReceivedBytes              | Bytes/s  | Volume of data received by RPC |
| SentBytes                  | Bytes/s  | Volume of data sent by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
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
| ThreadsNew                     | -       | Number of JVM threads     |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
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
| ProcessCpuLoad                 | %        | CPU utilization       |
| ProcessCpuTime                     | ms       | Cumulative CPU usage time   |
| MaxFileDescriptorCount             | -       | Number of file descriptors      |
| OpenFileDescriptorCount            | -       | Number of file descriptors      |
| Uptime                             | s        | Process run time      |
| DaemonThreadCount                  | -       | Number of worker threads        |
| ThreadCount                        | -       | Number of worker threads        |

### YARN - JobHistoryServer

| Metric Name | Unit | Description |
| :--------------------------------- | :------- | ----------------- |
ThreadsNew                         | -       | Number of JVM threads       |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
| LogFatal                       | -       | Number of JVM logs     |
| LogError                       | -       | Number of JVM logs     |
| LogWarn                        | -       | Number of JVM logs     |
| LogInfo                        | -       | Number of JVM logs     |
| MemNonHeapUsedM                | MB       | JVM memory         |
| MemNonHeapCommittedM                          | MB       | JVM memory                                             |
| MemNonHeapMaxM                 | MB       | JVM memory         |
| MemHeapUsedM                   | MB       | JVM memory         |
| MemHeapCommittedM                  | MB       | JVM memory           |
| MemHeapMaxM                        | MB       | JVM memory           |
| MemMaxM                            | MB       | JVM memory           |
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
| ProcessCpuLoad                     | %        | CPU utilization         |
| ProcessCpuTime                     | ms       | Cumulative CPU usage time   |
| MaxFileDescriptorCount             | -       | Number of file descriptors      |
| OpenFileDescriptorCount            | -       | Number of file descriptors      |
| Uptime                             | s        | Process run time      |
| DaemonThreadCount                  | -       | Number of worker threads        |
| ThreadCount                        | -       | Number of worker threads        |

### YARN - NodeManager

| Metric Name | Unit | Description |
| :----------------------------- | :------- | ---------------- |
| YGC                                | -       | GC count            |
| FGC                                | -       | GC count            |
| FGCT                               | s        | GC time            |
| GCT                                | s        | GC time            |
| YGCT                                | s        | GC time            |
| S0                                  | %        | Memory area proportion      |
| E                                  | %        | Memory area proportion      |
| CCS                                  | %        | Memory area proportion      |
| S1                                  | %        | Memory area proportion      |
| O                                  | %        | Memory area proportion      |
| M                                  | %        | Memory area proportion      |
| ThreadsNew                     | -       | Number of JVM threads     |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
| LogFatal                       | -       | Number of JVM logs     |
| LogError                       | -       | Number of JVM logs     |
| LogWarn                        | -       | Number of JVM logs     |
| LogInfo                        | -       | Number of JVM logs     |
| MemNonHeapUsedM                | MB       | JVM memory         |
| MemNonHeapCommittedM           | MB       | JVM memory         |
| MemNonHeapMaxM                 | MB       | JVM memory         |
| MemHeapUsedM                   | MB       | JVM memory         |
| MemHeapCommittedM              | MB       | JVM memory         |
| MemHeapMaxM                    | MB       | JVM memory         |
| MemMaxM                        | MB       | JVM memory         |
| ContainersLaunched             | -       | Total number of containers         |
| ContainersCompleted            | -       | Total number of containers         |
| ContainersFailed               | -       | Total number of containers         |
| ContainersKilled               | -       | Total number of containers         |
| ContainersIniting              | -       | Total number of containers         |
| ContainersRunning              | -       | Total number of containers         |
| AllocatedContainers            | -       | Total number of containers         |
| ContainerLaunchDurationAvgTime | ms       | Average container launch time |
| ContainerLaunchDurationNumOps  | -       | Number of container launches   |
| AvailableVCores                | -       | Number of CPU cores         |
| AllocatedVCores                | -       | Number of CPU cores      |
| AllocatedGB                    | GB       | Memory size         |
| AvailableGB                    | GB       | Memory size         |
| ProcessCpuLoad                 | %        | CPU utilization       |
| ProcessCpuTime                 | ms       | Cumulative CPU usage time |
| MaxFileDescriptorCount         | -       | Number of file descriptors     |
| OpenFileDescriptorCount         | -       | Number of file descriptors     |
| Uptime                         | s        | Thread run time     |
| DaemonThreadCount              | -       | Number of worker threads       |
| ThreadCount              | -       | Number of worker threads       |





