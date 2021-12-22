## Namespace

Namespace=QCE/TXMR_YARN

## Monitoring Metrics

### YARN - Overview

| Parameter | Metric | Unit | Description | Dimension |
| ----------------------------------------------------- | ----------------------------- | -------- | -------- | --------------------------------------- |
| EmrHdfsOverview<br>YarnRmNumsNumactivenms             | Number of nodes_NumActiveNMs         | -       | Number of nodes | host4yarnoverview, <br>id4yarnoverview  |
| EmrHdfsOverview<br>YarnRmNumsNumde<br>commissionednms | Number of nodes_NumDecommissionedNMs | -       | Number of nodes | host4yarnoverview, <br/>id4yarnoverview |
| EmrHdfsOverviewYarn<br>RmNumsNumlostnms               | Number of nodes_NumLostNMs           | -       | Number of nodes | host4yarnoverview, <br/>id4yarnoverview |
| EmrHdfsOverview<br>YarnRmNumsNumun<br>healthynms      | Number of nodes_NumUnhealthyNMs      | -       | Number of nodes | host4yarnoverview, <br/>id4yarnoverview |

### YARN - OverviewAggregation

| Parameter | Metric | Unit | Description | Dimension |
| ------------------------------------------------------------ | ----------------------------- | -------- | -------- | --------------- |
| EmrHdfsOverviewAggregation<br>YarnRmNumsNumactivenms         | Number of nodes_NumActiveNMs         | -       | Number of nodes | id4yarnoverview |
| EmrHdfsOverviewAggregation<br>YarnRmNumsNumde<br>commissionednms | Number of nodes_NumDecommissionedNMs | -       | Number of nodes | id4yarnoverview |
| EmrHdfsOverviewAggregation<br> RmNumsNumlostnms              | Number of nodes_NumLostNMs           | -       | Number of nodes | id4yarnoverview |
| EmrHdfsOverviewAggregation<br> YarnRmNumsNumun healthynms    | Number of nodes_NumUnhealthyNMs      | -       | Number of nodes | id4yarnoverview |

### YARN - Cluster

| Parameter | Metric | Unit | Description | Dimension |
| ---------------------------------------------- | ------------------------------ | -------- | ---------------- | --------------------------------------- |
| YarnClusterResAppFailed                        | Applications_failed            | -       | Total number of applications         | host4yarnoverview, <br>id4yarnoverview  |
| YarnClusterResAppKilled                        | Applications_killed            | -       | Total number of applications         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResAppPending                       | Applications_pending           | -       | Total number of applications         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResAppRunning                       | Applications_running           | -       | Total number of applications         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterRes<br>AppSubmitted                 | Applications_submitted         | -       | Total number of applications         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResContainer<br>Containersallocated | Containers_containersAllocated | -       | Total number of released containers | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResContainer<br>Containerspending   | Containers_containersPending   | -       | Total number of released containers | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResContainer<br>Containersreserved  | Containers_containersReserved  | -       | Total number of released containers | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResCpu<br>Allocatedvirtualcores     | Cores_allocatedVirtualCores    | -       | Number of CPU cores         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResCpu<br>Availablevirtualcores     | Cores_availableVirtualCores    | -       | Number of CPU cores         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResCpu<br>Reservedvirtualcores      | Cores_reservedVirtualCores     | -       | Number of CPU cores         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResCpu<br>Totalvirtualcores         | Cores_totalVirtualCores        | -       | Number of CPU cores         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResCpu<br>UsageRatioUsageratio      | CPU utilization_usageRatio           | %        | Memory size         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResMem<br>Allocatedmb               | Memory_allocatedMB             | MB       | Memory size         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResMem<br>Availablemb               | Memory_availableMB             | MB       | Memory size         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResMem<br>Reservedmb                | Memory_reservedMB              | MB       | Memory size         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterRes<br>MemTotalmb                   | Memory_totalMB                 | MB       | Memory size         | host4yarnoverview, <br/>id4yarnoverview |
| YarnClusterResMem<br>UsageRatioUsageratio      | Memory utilization_usageRatio          | %        | Memory size         | host4yarnoverview, <br/>id4yarnoverview |



### YARN - ResourceManager

| Parameter | Metric | Unit | Description | Dimension |
| -------------------------------------------------- | ---------------------------------------- | -------- | ------------------ | ----------------------------------------------------- |
| YarnRmRpcAuth5000<br> Rpcauthenticationfailures    | Number of RPC authentication authorizations_RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br>id4yarnresourcemanager  |
| YarnRmRpcAuth5000<br> Rpcauthenticationsuccesses   | Number of RPC authentication authorizations_RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthorizationfailures     | Number of RPC authentication authorizations_RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthorizationsuccesses    | Number of RPC authentication authorizations_RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcBytes5000<br>  Receivedbytes              | Volume of data received/sent by RPC_ReceivedBytes          | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcBytes5000<br> Sentbytes                   | Volume of data received/sent by RPC_SentBytes              | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpc<br>Connections5000<br>Numopenconnections | Number of RPC connections_NumOpenConnections             | -       | Number of RPC connections         | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcOps5000<br>Rpcprocessingtimenumops        | Number of RPC requests_RpcProcessingTimeNumOps      | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcOps5000<br>Rpcqueuetimenumops             | Number of RPC requests_RpcQueueTimeNumOps           | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcQueueLen5000<br>Callqueuelength           | RPC queue length_CallQueueLength              | -       | RPC queue length       | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcTime5000<br>Rpcprocessingtimeavgtime      | Average RPC processing time_RpcProcessingTimeAvgTime | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcTime5000<br>Rpcqueuetimeavgtime           | Average RPC processing time_RpcQueueTimeAvgTime      | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthenticationfailures    | Number of RPC authentication authorizations_RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthenticationsuccesses   | Number of RPC authentication authorizations_RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthorizationfailures     | Number of RPC authentication authorizations_RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthorizationsuccesses    | Number of RPC authentication authorizations_RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcBytes5000<br>  Receivedbytes              | Volume of data received/sent by RPC_ReceivedBytes          | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcBytes5000<br> Sentbytes                   | Volume of data received/sent by RPC_SentBytes              | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcConnections5000<br>Numopenconnections     | Number of RPC connections_NumOpenConnections             | -       | Number of RPC connections         | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcOps5000<br>Rpcprocessingtimenumops        | Number of RPC requests_RpcProcessingTimeNumOps      | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcOps5000<br>Rpcqueuetimenumops             | Number of RPC requests_RpcQueueTimeNumOps           | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcQueueLen5000<br>Callqueuelength           | RPC queue length_CallQueueLength              | -       | RPC queue length       | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcTime5000<br>Rpcprocessingtimeavgtime      | Average RPC processing time_RpcProcessingTimeAvgTime | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcTime5000<br>Rpcqueuetimeavgtime           | Average RPC processing time_RpcQueueTimeAvgTime      | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthenticationfailures   | Number of RPC authentication authorizations_RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthenticationsuccesses   | Number of RPC authentication authorizations_RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthorizationfailures     | Number of RPC authentication authorizations_RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcAuth5000<br> Rpcauthorizationsuccesses    | Number of RPC authentication authorizations_RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager |
| YarnRmRpcBytes5000<br>  Receivedbytes              | Volume of data received/sent by RPC_ReceivedBytes          | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcBytes5000<br> Sentbytes                   | Volume of data received/sent by RPC_SentBytes              | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcConnections5000<br>Numopenconnections     | Number of RPC connections_NumOpenConnections             | -       | Number of RPC connections         | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcOps5000<br>Rpcprocessingtimenumops        | Number of RPC requests_RpcProcessingTimeNumOps      | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcOps5000<br>Rpcqueuetimenumops             | Number of RPC requests_RpcQueueTimeNumOps           | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcQueueLen5000<br>Callqueuelength           | RPC queue length_CallQueueLength              | -       | RPC queue length       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcTime5000<br>Rpcprocessingtimeavgtime      | Average RPC processing time_RpcProcessingTimeAvgTime | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcTime5000<br>Rpcqueuetimeavgtime           | Average RPC processing time_RpcQueueTimeAvgTime      | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcAuth5000<br> Rpcauthenticationfailures    | Number of RPC authentication authorizations_RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcAuth5000<br> Rpcauthenticationsuccesses   | Number of RPC authentication authorizations_RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcAuth5000<br> Rpcauthorizationfailures     | Number of RPC authentication authorizations_RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcAuth5000<br> Rpcauthorizationsuccesses    | Number of RPC authentication authorizations_RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcBytes5000<br>  Receivedbytes              | Volume of data received/sent by RPC_ReceivedBytes          | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcBytes5000<br> Sentbytes                   | Volume of data received/sent by RPC_SentBytes              | bytes/s  | Volume of data received/sent by RPC | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpc<br>Connections5000<br>Numopenconnections | Number of RPC connections_NumOpenConnections             | -       | Number of RPC connections         | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcOps5000<br>Rpcprocessingtimenumops        | Number of RPC requests_RpcProcessingTimeNumOps      | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcOps5000<br>Rpcqueuetimenumops             | Number of RPC requests_RpcQueueTimeNumOps           | -       | Number of RPC requests       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpc<br>QueueLen5000<br>Callqueuelength       | RPC queue length_CallQueueLength              | -       | RPC queue length       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcTime5000<br>Rpcprocessingtimeavgtime      | Average RPC processing time_RpcProcessingTimeAvgTime | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRpcTime5000<br>Rpcqueuetimeavgtime           | GC count_YGC                               | s        | Average RPC processing time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilGcCountYgc                             | GC count_FGC                               | -       | GC count            | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilGcCountFgc                             | GC time_FGCT                              | -       | GC count            | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilGcTimeFgct                             | GC time_FGCT                              | s        | GC time            | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilGcTimeGct                              | GC time_YGCT                              | s        | GC time            | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilGcTimeYgct                             | Memory space percentage_S0                          | s        | GC time            | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilMemoryS0                               | Memory space percentage_E                           | %        | Memory space percentage       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilMemoryE                                | Memory space percentage_CCS                         | %        | Memory space percentage       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilMemoryCcs                              | Memory space percentage_S1                          | %        | Memory space percentage       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilMemoryS1                               | Memory space percentage_O                           | %        | Memory space percentage       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilMemoryO                                | Memory space percentage_M                           | %        | Memory space percentage       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmGcUtilMemoryM                                | Number of JVM threads_ThreadsNew                   | %        | Memory space percentage       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmJava<br>ThreadsThreadsnew                 | Number of JVM threads_ThreadsRunnable              | -       | Number of JVM threads       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmJavaThreads<br>Threadsrunnable            | Number of JVM threads_ThreadsBlocked               | -       | Number of JVM threads       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmJavaThreads<br>Threadsblocked             | Number of JVM threads_ThreadsWaiting               | -       | Number of JVM threads       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmJavaThreads<br>Threadswaiting             | Number of JVM threads_ThreadsTimedWaiting          | -       | Number of JVM threads       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmJavaThreads<br>Threadstimedwaiting        | Number of JVM threads_ThreadsTerminated            | -       | Number of JVM threads       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmJavaThreads<br>Threadsterminated          | Number of JVM logs_LogFatal                     | -       | Number of JVM threads       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmLogTotalLogfatal                          | Number of JVM logs_LogError                     | -       | Number of JVM logs       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmLogTotalLogerror                          | Number of JVM logs_LogWarn                      | -       | Number of JVM logs       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmLogTotalLogwarn                           | Number of JVM logs_LogInfo                      | -       | Number of JVM logs       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmLogTotalLoginfo                           | JVM memory_MemNonHeapUsedM                  | -       | Number of JVM logs       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmMem<br>Memnonheapusedm                    | JVM memory_MemNonHeapCommittedM             | MB       | JVM memory           | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmMemMem<br>nonheapcommittedm               | JVM memory_MemHeapUsedM                     | MB       | JVM memory           | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmMemMem<br>heapusedm                       | JVM memory_MemHeapCommittedM                | MB       | JVM memory           | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmMemMem<br>heapcommittedm                  | JVM memory_MemHeapMaxM                      | MB       | JVM memory           | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmMem<br>Memheapmaxm                        | JVM memory_MemMaxM                          | MB       | JVM memory           | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmJvmMemMemmaxm                                | CPU utilization_ProcessCpuLoad                 | MB       | JVM memory           | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmOsCpuLoad<br>Processcpuload                  | Cumulative CPU usage time_ProcessCpuTime           | %        | CPU utilization         | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmOsCpuTime<br>Processcputime                  | Number of file descriptors_MaxFileDescriptorCount      | ms       | Cumulative CPU usage time   | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmOsFdCount<br>Maxfiledescriptorcount          | Number of file descriptors_OpenFileDescriptorCount     | -       | Number of file descriptors       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmOsFdCount<br>Openfiledescriptorcount         | Process run time_Uptime                      | -       | Number of file descriptors       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmRtUptimeUptime                               | Process run time_Uptime                      | s        | Process run time       | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmThreadCount<br>Daemonthreadcount             | Number of worker threads_DaemonThreadCount             | -       | Number of worker threads         | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |
| YarnRmThreadCount<br>Threadcount                   | Number of worker threads_ThreadCount                   | -       | Number of worker threads         | host4yarnresourcemanager, <br/>id4yarnresourcemanager   |




### YARN - JobHistoryServer

| Parameter | Metric | Unit | Description | Dimension |
| -------------------------------------------- | ------------------------------------ | -------- | ---------------- | ------------------------------------------------------- |
| YarnJhJvmJava<br> <br> ThreadsThreadsnew     | Number of JVM threads_ThreadsNew               | -       | Number of JVM threads     | host4yarnjobhistoryserver, <br>id4yarnjobhistoryserver  |
| YarnJhJvmJava<br> ThreadsThreadsrunnable     | Number of JVM threads_ThreadsRunnable          | -       | Number of JVM threads     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmJava<br> ThreadsThreadsblocked      | Number of JVM threads_ThreadsBlocked           | -       | Number of JVM threads     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmJava<br> ThreadsThreadswaiting      | Number of JVM threads_ThreadsWaiting           | -       | Number of JVM threads     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmJava<br> ThreadsThreadstimedwaiting | Number of JVM threads_ThreadsTimedWaiting      | -       | Number of JVM threads     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmJava<br> ThreadsThreadsterminated   | Number of JVM threads_ThreadsTerminated        | -       | Number of JVM threads     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmLogTotalLogfatal                    | Number of JVM logs_LogFatal                 | -       | Number of JVM logs     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmLogTotalLogerror                    | Number of JVM logs_LogError                 | -       | Number of JVM logs     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmLogTotalLogwarn                     | Number of JVM logs_LogWarn                  | -       | Number of JVM logs     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmLogTotalLoginfo                     | Number of JVM logs_LogInfo                  | -       | Number of JVM logs     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmMemMem<br> nonheapusedm             | JVM memory_MemNonHeapUsedM              | MB       | JVM memory         | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmMemMem<br> nonheapcommittedm        | JVM memory_MemNonHeapCommittedM         | MB       | JVM memory         | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmMemMem<br> heapusedm                | JVM memory_MemHeapUsedM                 | MB       | JVM memory         | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmMemMem<br> heapcommittedm           | JVM memory_MemHeapCommittedM            | MB       | JVM memory         | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmMemMem<br> heapmaxm                 | JVM memory_MemHeapMaxM                  | MB       | JVM memory         | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhJvmMemMem<br> maxm                     | JVM memory_MemMaxM                      | MB       | JVM memory         | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilGcCountYgc                      | GC count_YGC                           | -       | GC count          | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilGcCountFgc                      | GC count_FGC                           | -       | GC count          | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilGcTimeFgct                      | GC time_FGCT                          | s        | GC time          | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilGcTimeGct                       | GC time_FGCT                          | s        | GC time          | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilGcTimeYgct                      | GC time_YGCT                          | s        | GC time          | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilMemoryS0                        | Memory space percentage_S0                      | %        | Memory space percentage     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilMemoryE                         | Memory space percentage_E                       | %        | Memory space percentage     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilMemoryCcs                       | Memory space percentage_CCS                     | %        | Memory space percentage     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilMemoryS1                        | Memory space percentage_S1                      | %        | Memory space percentage     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilMemoryO                         | Memory space percentage_O                       | %        | Memory space percentage     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhsGcUtilMemoryM                         | Memory space percentage_M                       | %        | Memory space percentage     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhOsCpuLoad<br>Processcpuload            | CPU utilization_ProcessCpuLoad             | %        | CPU utilization       | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhOsCpuTime<br>Processcputime            | Cumulative CPU usage time_ProcessCpuTime       | ms       | Cumulative CPU usage time | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhOsFdCountMax<br>filedescriptorcount    | Number of file descriptors_MaxFileDescriptorCount  | -       | Number of file descriptors     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhOsFdCountOpen<br>filedescriptorcount   | Number of file descriptors_OpenFileDescriptorCount | -       | Number of file descriptors     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhRtUptimeUptime                         | Process run time_Uptime                  | s        | Process run time     | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhThreadCount<br>Daemonthreadcount       | Number of worker threads_DaemonThreadCount         | -       | Number of worker threads       | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |
| YarnJhThreadCount<br>Threadcount             | Number of worker threads_ThreadCount               | -       | Number of worker threads       | host4yarnjobhistoryserver, <br/>id4yarnjobhistoryserver |

### YARN - NodeManager

| Parameter | Metric | Unit | Description | Dimension |
| ------------------------------------------------ | ------------------------------------ | -------- | ---------------- | ---------------------------------------------- |
| YarnNmGcUtilGcCountYgc                           | GC count_YGC                           | -       | GC count          | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmGcUtilGcCountFgc                           | GC count_FGC                           | -       | GC count          | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilGcTimeFgct                           | GC time_FGCT                          | s        | GC time          | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilGcTimeGct                            | GC time_FGCT                          | s        | GC time          | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilGcTimeYgct                           | GC time_YGCT                          | s        | GC time          | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilMemoryS0                             | Memory space percentage_S0                      | %        | Memory space percentage     | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilMemoryE                              | Memory space percentage_E                       | %        | Memory space percentage     | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilMemoryCcs                            | Memory space percentage_CCS                     | %        | Memory space percentage     | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilMemoryS1                             | Memory space percentage_S1                      | %        | Memory space percentage     | id4yarnnodemanager, <br/>host4yarnnodemanager  |
| YarnNmGcUtilMemoryO                              | Memory space percentage_O                       | %        | Memory space percentage     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmGcUtilMemoryM                              | Memory space percentage_M                       | %        | Memory space percentage     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmJavaThreads<br> <br> Threadsnew         | Number of JVM threads_ThreadsNew               | -       | Number of JVM threads     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmJavaThreads<br> Threadsrunnable         | Number of JVM threads_ThreadsRunnable          | -       | Number of JVM threads     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmJavaThreads<br> Threadsblocked          | Number of JVM threads_ThreadsBlocked           | -       | Number of JVM threads     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmJavaThreads<br> Threadswaiting          | Number of JVM threads_ThreadsWaiting           | -       | Number of JVM threads     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmJavaThreads<br> <br>Threadstimedwaiting | Number of JVM threads_ThreadsTimedWaiting      | -       | Number of JVM threads     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmJavaThreads<br> <br>Threadsterminated   | Number of JVM threads_ThreadsTerminated        | -       | Number of JVM threads     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmLog<br>TotalLogfatal                    | Number of JVM logs_LogFatal                 | -       | Number of JVM logs     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmLog<br>TotalLogerror                    | Number of JVM logs_LogError                 | -       | Number of JVM logs     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmLog<br>TotalLogwarn                     | Number of JVM logs_LogWarn                  | -       | Number of JVM logs     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmLog<br>TotalLoginfo                     | Number of JVM logs_LogInfo                  | -       | Number of JVM logs     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmMem<br>Memnonheapusedm                  | JVM memory_MemNonHeapUsedM              | MB       | JVM memory         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmMem<br>Memnonheapcommittedm             | JVM memory_MemNonHeapCommittedM         | MB       | JVM memory         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmMemMem<br>heapusedm                     | JVM memory_MemHeapUsedM                 | MB       | JVM memory         | id4yarnnodemanager, <br>host118yarnnodemanager |
| YarnNmJvmMemMem<br>heapcommittedm                | JVM memory_MemHeapCommittedM            | MB       | JVM memory         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmMem<br>Memheapmaxm                      | JVM memory_MemHeapMaxM                  | MB       | JVM memory         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmJvmMem<br>Memmaxm                          | JVM memory_MemMaxM                      | MB       | JVM memory         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmVcores<br>Availablevcores                  | Number of CPU cores_AvailableVCores              | -       | Number of CPU cores         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmVcores<br>Allocatedvcores                  | Number of CPU cores_AllocatedVCores              | -       | Number of CPU cores         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmMemAllocatedgb                             | Memory size_AllocatedGB                 | GB       | Memory size         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmMemAvailablegb                             | Memory size_AvailableGB                 | GB       | Memory size         | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmOsCpuLoad<br>Processcpuload                | CPU utilization_ProcessCpuLoad             | %        | CPU utilization       | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmOsCpuTime<br>Processcputime                | Cumulative CPU usage time_ProcessCpuTime       | ms       | Cumulative CPU usage time | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmOsFdCount<br>Maxfiledescriptorcount        | Number of file descriptors_MaxFileDescriptorCount  | -       | Number of file descriptors     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmOsFdCount<br>Openfiledescriptorcount       | Number of file descriptors_OpenFileDescriptorCount | -       | Number of file descriptors     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmRtUptimeUptime                             | Process run time_Uptime                  | s        | Process run time     | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmThreadCount<br>Daemonthreadcount           | Number of worker threads_DaemonThreadCount         | -       | Number of worker threads       | id4yarnnodemanager, <br>host4yarnnodemanager   |
| YarnNmThread<br>CountThreadcount                 | Number of worker threads_ThreadCount               | -       | Number of worker threads       | id4yarnnodemanager, <br>host4yarnnodemanager   |

## Dimension and Parameters

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ------------------------- | ----------------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | id4yarnoverview           | Dimension name of the EMR instance ID       | String-type dimension name, such as id4yarnoverview                   |
| Instances.N.Dimensions.0.Value | id4yarnoverview           | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4yarnoverview         | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4yarnoverview                  |
| Instances.N.Dimensions.1.Value | host4yarnoverview      | Specific node IP in the EMR instance         | Specific node IP, which can be obtained by clicking **Instance** > **Cluster Resources** > **Resource Management** > **Node Private IP** in the [EMR console](https://console.cloud.tencent.com/emr) or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.0.Name  | id4yarnresourcemanager           | Dimension name of the EMR instance ID       | String-type dimension name, such as id4yarnresourcemanager            |
| Instances.N.Dimensions.0.Value | id4yarnresourcemanager           | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4yarnresourcemanager         | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4yarnresourcemanager           |
| Instances.N.Dimensions.1.Value | host4yarnresourcemanager      | Specific node IP in the EMR instance         | Specific node IP, which can be obtained by clicking **Instance** > **Cluster Resources** > **Resource Management** > **Node Private IP** in the [EMR console](https://console.cloud.tencent.com/emr) or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.0.Name  | id4yarnjobhistoryserver           | Dimension name of the EMR instance ID       | String-type dimension name, such as id4yarnjobhistoryserver           |
| Instances.N.Dimensions.0.Value | id4yarnjobhistoryserver           | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4yarnjobhistoryserver         | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4yarnjobhistoryserver          |
| Instances.N.Dimensions.1.Value | host4yarnjobhistoryserver      | Specific node IP in the EMR instance         | Specific node IP, which can be obtained by clicking **Instance** > **Cluster Resources** > **Resource Management** > **Node Private IP** in the [EMR console](https://console.cloud.tencent.com/emr) or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.0.Name  | id4yarnnodemanager           | Dimension name of the EMR instance ID       | String-type dimension name, such as id4yarnnodemanager                |
| Instances.N.Dimensions.0.Value | id4yarnnodemanager           | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222                |
| Instances.N.Dimensions.1.Name  | host4yarnnodemanager         | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4yarnnodemanager               |
| Instances.N.Dimensions.1.Value | host4yarnnodemanager      | Specific node IP in the EMR instance         | Specific node IP, which can be obtained by clicking **Instance** > **Cluster Resources** > **Resource Management** > **Node Private IP** in the [EMR console](https://console.cloud.tencent.com/emr) or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |

## Input Parameter Description

EMR (YARN) supports querying monitoring data based on the following five combinations of dimensions. The values for the input parameters are as follows: 

**1. To query the metric monitoring data of Yarn - Overview Aggregation or YARN - Cluster, use the following input parameters:** &Namespace=QCE/TXMR_YARN
&Instances.N.Dimensions.0.Name=id4yarnoverview
&Instances.N.Dimensions.0.Value=EMR instance ID

**2. To query the metric monitoring data of Yarn - Overview, use the following input parameters:**
&Namespace=QCE/TXMR_YARN
&Instances.N.Dimensions.0.Name=id4yarnoverview
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4yarnoverview
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**3. To query the metric monitoring data of YARN - ResourceManager, use the following input parameters:**
&Namespace=QCE/TXMR_YARN
&Instances.N.Dimensions.0.Name=id4yarnresourcemanager
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4yarnresourcemanager
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**4. To query the metric monitoring data of YARN - JobHistoryServer, use the following input parameters:**
&Namespace=QCE/TXMR_YARN
&Instances.N.Dimensions.0.Name=id4yarnjobhistoryserver 
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4yarnjobhistoryserver
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**5. To query the metric monitoring data of YARN - NodeManager, use the following input parameters:**
&Namespace=QCE/TXMR_YARN
&Instances.N.Dimensions.0.Name=id4yarnnodemanager 
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4yarnnodemanager
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 


