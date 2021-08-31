## Namespace

Namespace=QCE/TXMR_HBASE

## Monitoring Metrics

### HBase - Overview

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | --------------------------------------------- | -------- | --------------------------- | ----------------------------------------- |
| EmrHbaseOverview<br>HbaseMasterAssignment<br>managerRitRitcount | Number of cluster regions in the RIT state_ritCount              | Count       | Number of cluster regions in the RIT state   | host4hbaseoverview, <br>id4hbaseoverview  |
| EmrHbaseOverview<br/>HbaseMaster<br>Assignmentmanager<br>RitRitcountoverthreshold | Number of cluster regions in the RIT state_ritCountOverThreshold | Count       | Number of cluster regions in the RIT state   | host4hbaseoverview, <br>id4hbaseoverview  |
| EmrHbaseOverview<br/>HbaseMaster<br>Assignmentmanager<br>TimeRitoldestage | Cluster RIT time_ritOldestAge                    | ms       | Cluster RIT time              | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMaster<br>AvgloadAverageload       | Average number of regions per RS_averageLoad            | Count       | Average number of regions per RS     | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMasterRsnums<br>Numregionservers   | Number of cluster RSs_numRegionServers                 | Count       | Number of cluster RSs               | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMasterRsnumsNum<br>deadregionservers | Number of cluster RSs_numDeadRegionServers             | Count       | Number of cluster RSs               | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMaster<br>BytesReceivedbytes       | Number of cluster reads/writes_receivedBytes                    | Bytes/s  | Number of cluster reads/writes                | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMaster<br>BytesSentbytes           | Number of cluster reads/writes_sentBytes                        | Bytes/s  | Number of cluster reads/writes                | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMasterReq<br>Clusterrequests       | Total number of requests in the cluster\_clusterRequests                | Requests/s     | Total number of requests in the cluster              | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMaster<br>Assignmentmanager<br>OpsAssignNumOps | Cluster assignment manager operations\_Assign_num_ops     | Count       | Cluster assignment manager operations | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMaste<br>rAssignmentmanager<br>OpsBulkassignNumOps | Cluster assignment manager operations\_BulkAssign_num_ops | Count       | Cluster assignment manager operations | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMasterBalancerOps<br>BalancerclusterNumOps | Number of cluster load balancing operations\_BalancerclusterNum                    | Count       | Number of cluster load balancing operations            | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMasterServerPlan<br>Mergeplancount | Cluster plans_mergePlanCount                      | Plans       | Cluster plans                  | host4hbaseoverview, <br/>id4hbaseoverview |
| EmrHbaseOverview<br/>HbaseMasterServerPlan<br>Splitplancount | Cluster plans_splitPlanCount                      | Plans       | Cluster plans                  | host4hbaseoverview, <br/>id4hbaseoverview |

### HBase - OverviewAggregation

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | --------------------------------------------- | -------- | --------------------------- | ---------------- |
| EmrHbaseOverviewAggregation<br>HbaseMasterAssignment<br>managerRitRitcount | Number of cluster regions in the RIT state_ritCount              | Count       | Number of cluster regions in the RIT state   | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterAssign<br>mentmanagerRitRitcountover<br>threshold | Number of cluster regions in the RIT state_ritCountOverThreshold | Count       | Number of cluster regions in the RIT state   | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterAssign<br>mentmanager TimeRitoldestage | Cluster RIT time_ritOldestAge                    | ms       | Cluster RIT time              | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMaster AvgloadAverageload | Average number of regions per RS_averageLoad              | Count       | Average number of regions per RS     | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterRsnums<br>Numregionservers | Number of cluster RSs_numRegionServers                 | Count       | Number of cluster RSs               | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterRsnumsNum <br>deadregionservers | Number of cluster RSs_numDeadRegionServers             | Count       | Number of cluster RSs               | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMaster BytesReceivedbytes | Number of cluster reads/writes_receivedBytes                    | Bytes/s  | Number of cluster reads/writes                | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMaster<br>BytesSentbytes | Number of cluster reads/writes_sentBytes                        | Bytes/s  | Number of cluster reads/writes                | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterReq<br>Clusterrequests | Total number of requests in the cluster_clusterRequests                | Requests/s     | Total number of requests in the cluster              | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterAssign<br>mentmanagerOpsAssignNumOps | Cluster assignment manager operations\_Assign_num_ops     | Count       | Cluster assignment manager operations | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterAssign<br/>mentmanagerOpsBulkassignNumOps | Cluster assignment manager operations\_BulkAssign_num_ops | Count       | Cluster assignment manager operations | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterBalancerOps<br>BalancerclusterNumOps | Number of cluster load balancing operations\_BalancerclusterNum                    | Count       | Number of cluster load balancing operations            | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterServerPlan<br>Mergeplancount | Cluster plans_mergePlanCount                      | Plans       | Cluster plans                  | id4hbaseoverview |
| EmrHbaseOverviewAggregation<br/>HbaseMasterServerPlan<br>Splitplancount | Cluster plans_splitPlanCount                      | Plans       | Cluster plans                  | id4hbaseoverview |

### HBase - HMaster

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ------------------------------------------- | -------- | --------------- | --------------------------------------- |
| HbaseHmGcUtilGcCountYgc                                      | GC count_YGC                                 | Count       | GC count        | host4hbasehmaster, <br>id4hbasehmaster  |
| HbaseHmGcUtilGcCountFgc                                      | GC count_FGC                                 | Count       | GC count        | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilGcTimeFgct                                      | GC time_FGCT                                | s        | GC time        | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilGcTimeGct                                       | GC time_GCT                                 | s        | GC time        | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilGcTimeYgct                                      | GC time_YGCT                                | s        | GC time        | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilMemoryS0                                        | Memory space percentage_S0                             | %        | Memory space percentage    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilMemoryE                                         | Memory space percentage_E                              | %        | Memory space percentage    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilMemoryCcs                                       | Memory space percentage_CCS                            | %        | Memory space percentage    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilMemoryS1                                        | Memory space percentage_S1                             | %        | Memory space percentage    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilMemoryO                                         | Memory space percentage_O                              | %        | Memory space percentage    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseHmGcUtilMemoryM                                         | Memory space percentage_M                              | %        | Memory space percentage    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvm<br>LogTotalLogfatal                           | Number of JVM logs_LogFatal                       | Count       | Number of JVM logs   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvm<br>LogTotalLogerror                           | Number of JVM logs_LogError                       | Count       | Number of JVM logs   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvm<br>LogTotalLogwarn                            | Number of JVM logs_LogWarn                        | Count       | Number of JVM logs   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvm<br>LogTotalLoginfo                            | Number of JVM logs_LogInfo                        | Count       | Number of JVM logs   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMem<br>Memnonheapusedm                         | JVM memory_MemNonHeapUsedM                    | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMem<br>Memnonheapcommittedm                    | JVM memory_MemNonHeapCommittedM               | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMemMem<br>heapcommittedm                       | JVM memory_MemHeapUsedM                       | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMem<br>Memheapusedm                            | JVM memory_MemHeapUsedM                       | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMem<br>Memheapcommittedm                       | JVM memory_MemHeapCommittedM                  | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMem<br>Memheapmaxm                             | JVM memory_MemHeapMaxM                        | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmMem<br>Memmaxm                                 | JVM memory_MemMaxM                            | MB       | JVM memory       | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmThreads<br>Threadsnew                          | Number of JVM threads_ThreadsNew                     | Count       | Number of JVM threads   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmThreads<br>Threadsrunnable                     | Number of JVM threads_ThreadsRunnable                | Count       | Number of JVM threads   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmThreads<br>Threadsblocked                      | Number of JVM threads_ThreadsBlocked                 | Count       | Number of JVM threads   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmThreads<br>Threadswaiting                      | Number of JVM threads_ThreadsWaiting                 | Count       | Number of JVM threads   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmThreads<br>Threadstimedwaiting                 | Number of JVM threads_ThreadsTimedWaiting            | Count       | Number of JVM threads   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterJvmThreads<br>Threadsterminated                   | Number of JVM threads_ThreadsTerminated              | Count       | Number of JVM threads   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcConnections<br>Numopenconnections              | Number of RPC connections_numOpenConnections               | Count       | Number of RPC connections     | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcException<br>Failedsanitycheckexception        | Number of RPC exceptions_FailedSanityCheckException     | Count       | Number of RPC exceptions   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcException<br>Notservingregionexception         | Number of RPC exceptions_NotServingRegionException      | Count       | Number of RPC exceptions   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcException<br>Outoforderscanner<br>nextexception | Number of RPC exceptions_OutOfOrderScannerNextException | Count       | Number of RPC exceptions   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcException<br>Regionmovedexception              | Number of RPC exceptions_RegionMovedException           | Count       | Number of RPC exceptions   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcException<br>Regiontoobusyexception            | Number of RPC exceptions_RegionTooBusyException         | Count       | Number of RPC exceptions   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpcException<br>Unknownscannerexception           | Number of RPC exceptions_UnknownScannerException        | Count       | Number of RPC exceptions   | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpc<br>QueueNumcalls<br>inpriorityqueue           | Number of RPC queue requests_numCallsInPriorityQueue      | Count       | Number of RPC queue requests | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterIpc<br>QueueNumcalls<br>inreplicationqueue        | Number of RPC queue requests_numCallsInReplicationQueue   | Count       | Number of RPC queue requests | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterServerTime<br>Masteractivetime                    | Process start time_masterActiveTime               | s        | Process start time    | host4hbasehmaster, <br/>id4hbasehmaster |
| HbaseMasterServerTime<br>Masterstarttime                     | Process start time_masterStartTime                | s        | Process start time    | host4hbasehmaster, <br/>id4hbasehmaster |

### HBase - RegionServer

| Parameter | Metric Name | Unit | Description | Dimension |
| :----------------------------------------------------------- | ------------------------------------------------------- | -------- | ------------------ | -------------------------------------------------- |
| HbaseHsGcUtilGcCountYgc                                      | GC count_YGC                                             | Count       | GC count            | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseHsGcUtilGcCountFgc                                      | GC count_FGC                                             | Count       | GC count            | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseHsGcUtilGcTimeFgct                                      | GC time_FGCT                                            | s        | GC time           | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseHsGcUtilGcTimeGct                                       | GC time_GCT                                             | s        | GC time            | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseHsGcUtilGcTimeYgct                                      | GC time_YGCT                                            | s        | GC time            | host4hbaseregionserver<br>id4hbaseregionserver     |
| HbaseHsGcUtilMemoryS0                                        | Memory space percentage_S0                                         | %        | Memory space percentage       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseHsGcUtilMemoryE                                         | Memory space percentage_E                                          | %        | Memory space percentage       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseHsGcUtilMemoryCcs                                       | Memory space percentage_CCS                                        | %        | Memory space percentage       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseHsGcUtilMemoryS1                                        | Memory space percentage_S1                                         | %        | Memory space percentage       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseHsGcUtilMemoryO                                         | Memory space percentage_O                                          | %        | Memory space percentage       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseHsGcUtilMemoryM                                         | Memory space percentage_M                                          | %        | Memory space percentage       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmLog<br>TotalLogfatal                           | Number of JVM logs_LogFatal                                   | Count       | Number of JVM logs       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmLog<br>TotalLogerror                           | Number of JVM logs_LogError                                   | Count       | Number of JVM logs       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmLog<br>TotalLogwarn                            | Number of JVM logs_LogWarn                                    | Count       | Number of JVM logs       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmLog<br>TotalLoginfo                            | Number of JVM logs_LogInfo                                    | Count       | Number of JVM logs       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMem<br>Memnonheapusedm                         | JVM memory<br/>_MemNonHeapUsedM                           | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMem<br>Memnonheapcommittedm                    | JVM memory<br/>_MemNonHeapCommittedM                      | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMem<br>Memheapmaxm                             | JVM memory<br/>_MemHeapMaxM                               | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMem<br>Memheapusedm                            | JVM memory<br/>_MemHeapUsedM                              | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMemMem<br>heapcommittedm                       | JVM memory<br/>_MemHeapCommittedM                         | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMemMem<br>heapmaxm                             | JVM memory_MemHeapMaxM                                    | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmMem<br>Memmaxm                                 | JVM memory_MemMaxM                                        | MB       | JVM memory           | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvm<br>ThreadsThreadsnew                          | Number of JVM threads_ThreadsNew                                 | Count       | Number of JVM threads       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmThreads<br>Threadsrunnable                     | Number of JVM threads<br/>_ThreadsRunnable                       | Count       | Number of JVM threads       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmThreads<br>Threadsblocked                      | Number of JVM threads<br/>_ThreadsBlocked                        | Count       | Number of JVM threads       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmThreads<br>Threadswaiting                      | Number of JVM threads<br/>_ThreadsWaiting                        | Count       | Number of JVM threads       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmThreads<br>Threadstimedwaiting                 | Number of JVM threads_ThreadsTimedWaiting                        | Count       | Number of JVM threads       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterJvmThreads<br>Threadsterminated                   | Number of JVM threads_ThreadsTerminated                          | Count       | Number of JVM threads       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseRegionserver<br>AvgsizeAverageregionsize                | Average region size_averageRegionSize                       | Bytes     | Average region size    | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseRegionserver<br>RegionCountRegioncount                  | Number of regions_regionCount                                 | Count       | Number of regions        | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerHfilesPercentPercent<br>fileslocalsecond | Region replica localization_percentFilesLocal<br>SecondaryRegions | %        | Region replica localization  | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseRegionserver<br>IpcAuthentication<br>Authenticationfailures | Number of RPC authentications_authenticationFailures                     | Count       | Number of RPC authentications       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseRegionserver<br>IpcAuthentication<br>Authenticationsuccesses | Number of RPC authentications_authenticationSuccesses                    | Count       | Number of RPC authentications       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterIpcConnections<br>Numopenconnections              | Number of RPC connections<br/>_numOpenConnections                      | Count       | Number of RPC connections         | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterIpcException<br>Failedsanitycheckexception        | Number of RPC exceptions<br/>_FailedSanityCheckException            | Count       | Number of RPC exceptions       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterIpcException<br>Notservingregionexception         | Number of RPC exceptions<br/>_NotServingRegionException             | Count       | Number of RPC exceptions       | host4hbaseregionserver, <br>id4hbaseregionserver  |
| HbaseMasterIpcException<br>Outoforderscannernextexception    | Number of RPC exceptions<br/>_OutOfOrderScannerNext<br/>Exception   | Count       | Number of RPC exceptions       | host4hbaseregionserver, <br/>id4hbaseregionserver |
| HbaseMasterIpcException<br>Regionmovedexception              | Number of RPC exceptions_RegionMovedException                       | Count       | Number of RPC exceptions       | host4hbaseregionserver, <br/>id4hbaseregionserver |
| HbaseMasterIpcException<br>Regiontoobusyexception            | Number of RPC exceptions<br/>_RegionTooBusyException                | Count       | Number of RPC exceptions       | host4hbaseregionserver, <br/>id4hbaseregionserver |
| HbaseMasterIpcException<br>Unknownscannerexception           | Number of RPC exceptions<br/>_UnknownScannerException               | Count       | Number of RPC exceptions       | host4hbaseregionserver, <br/>id4hbaseregionserver |
 HbaseRegionserver<br>IpcHandlerNumactivehandler              | Number of RPC handles<br/>_numActiveHandler                        | Count       | Number of RPC handles         | host4hbaseregionserver, <br/>id4hbaseregionserver |
| HbaseMasterIpcQueue<br>Numcallsinpriorityqueue               | Number of RPC queue requests<br/>_numCallsInPriorityQueue             | Count       | Number of RPC queue requests     | host4hbaseregionserver, <br/>id4hbaseregionserver |
| HbaseMasterIpcQueue<br>Numcallsinreplicationqueue            | Number of RPC queue requests<br/>_numCallsInReplicationQueue          | Count       | Number of RPC queue requests     | host4hbaseregionserver, <br/>id4hbaseregionserver |
| HbaseRegionserver<br>IpcQueueNumcalls<br>ingeneralqueue      | Number of RPC queue requests<br/>_numCallsInGeneralQueue              | Count       | Number of RPC queue requests     | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>HlogcountHlogfilecount                  | Number of WAL files_hlogFileCount                              | Count       | Number of WAL files       | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>HlogsizeHlogfilesize                    | WAL file size_hlogFileSize                               | Bytes     | WAL file size       | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>MemstroreMemstoresize                   | MemStore size_memStoreSize                              | MB       | MemStore size      | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>StoreCountStorecount                    | Number of stores_storeCount                                   | Count       | Number of stores         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>StorefilecountStorefilecount            | Number of StoreFiles\_storeFileCount                           | Count       | Number of StoreFiles     | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>StorefilesizeStorefilesize              | StoreFile size\_storeFileSize                            | MB       | StoreFile size     | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerCellsFlushedcellssize             | Disk write rate\_flushedCellsSize                             | Bytes/s  | Disk write rate         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerDelayAppendMean                   | Average delay\_Append_mean                                    | ms       | Average delay           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerDelayReplayMean                   | Average delay\_Replay_mean                                    | ms       | Average delay           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerDelayGetMean                      | Average delay\_Get_mean                                       | ms       | Average delay           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerDelayUpdatesblockedtime           | Average delay<br/>\_updatesBlockedTime                        | ms       | Average delay           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerFlushFlushtimeNumOps              | Number of RS disk writes<br/>\_FlushTime_num_ops                   | Writes       | Number of RS disk writes      | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerQueueSplitqueuelength             | Number of operation queue requests<br/>\_splitQueueLength                    | Count       | Number of operation queue requests     | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerQueueCompaction<br>queuelength    | Number of operation queue requests\_compactionQueueLength                    | Count       | Number of operation queue requests     | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerQueueFlushqueuelength             | Number of operation queue requests<br/>\_flushQueueLength                    | Count       | Number of operation queue requests     | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerReplayReplayNumOps                | Number of Replay operations<br/>\_Replay_num_ops                     | Count       | Number of Replay operations    | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSlowSlowappendcount               | Number of slow operations<br/>\_slowAppendCount                         | Count       | Number of slow operations         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSlowSlowdeletecount               | Number of slow operations\_slowDeleteCount                              | Count       | Number of slow operations         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSlowSlowgetcount                  | Number of slow operations<br/>\_slowGetCount                            | Count       | Number of slow operations         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSlowSlowincrementcount            | Number of slow operations<br/>\_slowIncrementCount                      | Count       | Number of slow operations         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSlowSlowputcount                  | Number of slow operations\_slowPutCount                                 | Count       | Number of slow operations         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSplitSplitrequestcount            | Split requests\_splitRequestCount                            | Count       | Split requests         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerSplitSplitsuccesscount            | Split requests\_splitSuccessCount                            | Count       | Split requests         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerBlockcacheCountBlock<br>cachecount | Number of cache blocks<br/>\_blockCacheCount                         | Count       | Number of cache blocks         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerBlockcacheCountBlock<br>cachehitcount | Number of cache blocks<br/>\_blockCacheHitCount                      | Count       | Number of cache blocks         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerBlockcacheCountBlock<br>cachemisscount | Number of cache blocks<br/>\_blockCacheMissCount                     | Count       | Number of cache blocks         | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerBlockcachePercent<br>Blockcacheexpresshi | Cache read hit rate<br/>\_blockCacheExpress<br/>HitPercent      | %        | Cache read hit rate       | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerBlockcacheSize<br>Blockcachesize  | Size of the memory used by the cache block\_blockCacheSize                       | Bytes     | Size of the memory used by the cache block | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerIndexStaticbloomsize              | Index size\_staticBloomSize                                | Bytes     | Index size           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerIndexStaticindexsize              | Index size\_staticIndexSize                                | Bytes     | Index size           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>ServerIndexStorefileindexsize           | Index size\_storeFileIndexSize                             | Bytes     | Index size           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>IpcBytesReceivedbytes                   | Read/write traffic\_receivedBytes                                  | Bytes/s  | Read/write traffic           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseRegionserver<br>IpcBytesSentbytes                       | Read/write traffic\_sentBytes                                      | Bytes/s  | Read/write traffic           | host4hbaseregionserver, <br/>id4hbaseregionserver  |
| HbaseMasterJvm<br>LogTotalLogerror                           | Number of read/write requests\_Total                                        | Requests/s     | Number of read/write requests         | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseRegionserver<br>ReqcountRead                      | Number of read/write requests<br/>\_Read                        | Requests/s     | Number of read/write requests         | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseRegionserver<br>ReqcountWrite                           | Number of read/write requests\_Write                                       | Requests/s     | Number of read/write requests         | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseRegionserver<br>ReqcountAppendNumOps                    | Number of read/write requests\_Append_num_ops                               | Requests/s     | Number of read/write requests         | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseRegionserver<br>ServerMutationCount<br>Mutationswithoutwalcoun | Number of mutations\_mutationsWithout<br/>WALCount              | Count       | Number of mutations      | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseRegionserver<br>ServerMutationSizeMutation<br>swithoutwalsize | Size of the mutation\_mutationsWithoutWALSize               | Bytes     | Size of the mutation      | host4hbaseregionserver, <br>id4hbaseregionserver   |
| HbaseRegionserver<br>StarttimeRegionserverstarttime          | Process start time_regionServerStartTime                      | s        | Process start time       | host4hbaseregionserver, <br>id4hbaseregionserver   |

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| :----------------------------- | :--------------------- | :--------------------------- | :----------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4hbaseoverview       | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hbaseoverview       |
| Instances.N.Dimensions.0.Value | id4hbaseoverview       | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222        |
| Instances.N.Dimensions.1.Name  | host4hbaseoverview     | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hbaseoverview     |
| Instances.N.Dimensions.1.Value | host4hbaseoverview     | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                  |
| Instances.N.Dimensions.0.Name  | id4hbasehmaster        | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hbasehmaster        |
| Instances.N.Dimensions.0.Value | id4hbasehmaster        | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222        |
| Instances.N.Dimensions.1.Name  | host4hbasehmaster      | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hbasehmaster      |
| Instances.N.Dimensions.1.Value | host4hbasehmaster      | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                  |
| Instances.N.Dimensions.0.Name  | id4hbaseregionserver   | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hbaseregionserver   |
| Instances.N.Dimensions.0.Value | id4hbaseregionserver   | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222        |
| Instances.N.Dimensions.1.Name  | host4hbaseregionserver | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hbaseregionserver |
| Instances.N.Dimensions.1.Value | host4hbaseregionserver | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                  |

## Input Parameters

EMR (HBase) supports querying monitoring data based on the following four combinations of dimensions. The values for the input parameters are as follows: 

**1. To query the metric monitoring data of HBase - OverviewAggregation, use the following input parameters:**
&Namespace=QCE/TXMR_HBASE
&Instances.N.Dimensions.0.Name=id4hbaseoverview
&Instances.N.Dimensions.0.Value=EMR instance ID

**2. To query the metric monitoring data of HBase - Overview, use the following input parameters:**
&Namespace=QCE/TXMR_HBASE
&Instances.N.Dimensions.0.Name=id4hbaseoverview
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4hbaseoverview
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**3. To query the metric monitoring data of HBase - HMaster, use the following input parameters:**
&Namespace=QCE/TXMR_HBASE
&Instances.N.Dimensions.0.Name=id4hbasehmaster
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name= host4hbasehmaster
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**4. To query the metric monitoring data of HBase - RegionServer, use the following input parameters:**
&Namespace=QCE/TXMR_HBASE
&Instances.N.Dimensions.0.Name=id4hbaseregionserver 
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4hbaseregionserver
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance
