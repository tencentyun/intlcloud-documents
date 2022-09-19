## Namespace

Namespace=QCE/TXMR_KUDU

## Monitoring Metrics

### Kudu - master

| Metric | Description | Unit | Dimension |
| ------------------------------------------------------------ | -------------------------------------------- | ----- | -------------------------------------- |
| KuduMasterAllocated<br/>BytesAllocatedbytes                  | Number of allocated bytes_AllocatedBytes                    | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlock<br/>CacheBlockcachehit                       | Number of block cache hits_BlockCacheHit                     | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlock<br/>CacheBlockcachemiss                      | Number of block cache hits_BlockCacheMiss                    | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlockCacheUsage<br/>Blockcacheusage                | Block cache utilization_BlockCacheUsage                 | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlockManager<br/>BlocksBlockopenreading            | Number of block manager blocks_BlockOpenReading             | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlockManager<br/>BlocksBlockopenwriting            | Number of block manager blocks_BlockOpenWriting             | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlockManager<br/>BlocksBlockundermanagement        | Number of block manager blocks_BlockUnderManagement         | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlockManager<br/>BytesBytesundermanagement         | Number of block manager bytes_BytesUnderManagement          | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterBlockManager<br>ContainerContainer<br/>sundermanagement | Number of block manager containers_ContainersUnderManagement     | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterClusterReplica<br/>SkewClusterreplicaskew          | Difference in the number of replicas_ClusterReplicaSkew            | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterContextSwitches<br/>Involuntaryswitches            | Context_InvoluntarySwitches                   | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterContextSwitches<br/>Voluntaryswitches              | Context_InvoluntarySwitches                   | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterCpuTimeCpustime                                    | CPU time_CPUStime                             | ms    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterCpuTimeCpuutime                                    | CPU time_CPUUtime                             | ms    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterDataDirDatadirsfailed                              | Number of data paths_DataDirsFailed                      | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterDataDirDatadirsfull                                | Number of data paths_DataDirsFull                        | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterFileCacheFilecachehit                              | Number of file cache hits_FileCacheHit                    | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterFileCacheFilecachemiss                             | Number of file cache hits_FileCacheMiss                   | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterFileCache<br/>UsageFilecacheusage                  | File cache utilization_FileCacheUsage                | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterHybridClock<br/>ErrorHybridclockerror              | Hybrid clock error_HybridClockError                | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterHybridClock<br/>TimestampHybridclocktimestamp      | Hybrid clock timestamp_HybridClockTimestamp          | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterLogMessages<br/>Errormessages                      | Number of log messages_ErrorMessages                       | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterLogMessages<br/>Warningmessages                    | Number of log messages_WarningMessages                     | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterNumRaft<br/>LeadersNumraftleaders                  | Number of tablet leaders_NumRaftLeaders             | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpenSource<br/>SessionsOpemsourcesessions          | Number of tablet sessions_OpenSourceSessions          | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApply<br/>QueueLengthMax                         | Number of operations in the queue_Max                             | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApply<br/>QueueLengthMean                        | Number of operations in the queue_Mean                            | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApply<br/>QueueLengthMin                         | Number of operations in the queue_Min                             | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApply<br/>QueueLengthPercentile999               | Number of operations in the queue_Percentile_99_9                 | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApply<br/>QueueLengthTotalcount                  | Number of operations in the queue_TotalCount                      | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApply<br/>QueueTimeTotalcount                    | Queuing wait time_TotalCount                      | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOp<br/>ApplyRunTimeMax                             | Operation execution duration_Max                             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOp<br/>ApplyRunTimeMean                            | Operation execution duration_Mean                            | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOp<br/>ApplyRunTimeMin                             | Operation execution duration_Min                             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApplyRun<br/>TimePercentile999                   | Operation execution duration_Percentile_99_9                 | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApplyRun<br/>TimeTotalcount                      | Operation execution duration_TotalCount                      | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOp<br/>ApplyQueueTimeMax                           | Queuing wait time_Max                             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOp<br/>ApplyQueueTimeMean                          | Queuing wait time_Mean                            | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOp<br/>ApplyQueueTimeMin                           | Queuing wait time_Min                             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterOpApplyQueue<br/>TimePercentile999                 | Queuing wait time_Percentile_99_9                 | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConsensus<br/>serviceRunleaderelectionMax       | RPCRunLeader election_Max                         | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConsensus<br/>serviceRunleaderelectionMean      | RPCRunLeader election_Mean                        | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConsensus<br/>serviceRunleaderelectionMin       | RPCRunLeader election_Min                         | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConnections<br/>Connectionsaccepted             | Number of RPC requests_ConnectionsAccepted                  | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConnections<br/>Queueoverflow                   | Number of RPC requests_QueueOverflow                        | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConnections<br/>Timesoutinqueue                 | Number of RPC requests_TimesOutInQueue                      | -    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcConsensus<br/>serviceRunleaderelectionTotalcount | RPCRunLeader election_TotalCount                  | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMasterservice<br/>ConnecttomasterMax            | RPC connection to the master service_Max                        | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMasterservice<br/>ConnecttomasterMean           | RPC connection to the master service_Mean                       | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMasterservice<br/>ConnecttomasterMin            | RPC connection to the master service_Min                        | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMasterservice<br/>ConnecttomasterPercentile999  | RPC connection to the master service_Percentile_99_9            | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMasterservice<br/>ConnecttomasterTotalcount     | RPC connection to the master service_TotalCount                 | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpc<br/>MasterservicePingMax                       | RPCPing connection_Max                              | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>servicePingMean                      | RPCPing connection_Mean                             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>servicePingMin                       | RPCPing connection_Min                              | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>servicePingPercentile999             | RPCPing connection_Percentile_99_9                  | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>servicePingTotalcount                | RPCPing connection_TotalCount                       | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>serviceTsheartbeatMax                | TSHeartbeatRPC request duration_Max             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>serviceTsheartbeatMean               | TSHeartbeatRPC request duration_Mean            | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMaster<br/>serviceTsheartbeatMin                | TSHeartbeatRPC request duration_Min             | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcMasterservice<br/>TsheartbeatPercentile999      | TSHeartbeatRPC request duration_Percentile_99_9 | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcTabletcopy<br/>serviceFetchdataMax              | FetchDataRPC request duration_Max               | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcTabletcopy<br/>serviceFetchdataMean             | FetchDataRPC request duration_Mean              | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcTablet<br/>copyserviceFetchdataMin              | FetchDataRPC request duration_Min               | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcTabletcopy<br/>serviceFetchdataPercentile999    | FetchDataRPC request duration_Percentile_99_9   | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterRpcTabletcopy<br/>serviceFetchdataTotalcount       | FetchDataRPC request duration_TotalCount        | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterSpinlockContention<br/>TimeSpinlockcontentiontime  | Spinlock_SpinlockContentionTime                | us    | host4kudukudumaster, id4kudukudumaster |
| KuduMasterTcmallocMemory<br/>Currentthreadcachebytes         | TCMalloc memory_CurrentThreadCacheBytes         | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterTcmalloc<br/>MemoryHeapsize                        | TCMalloc memory_HeapSize                        | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterTcmallocMemory<br/>Totalthreadcachebytes           | TCMalloc memory_TotalThreadCacheBytes           | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterTcmalloc<br/>PageheapFreebytes                     | TCMallocPageHeap memory_FreeBytes               | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterTcmallocPage<br/>heapUnmappedbytes                 | TCMallocPageHeap memory_UnMappedBytes           | Bytes | host4kudukudumaster, id4kudukudumaster |
| KuduMasterThreadThreadsrunning                               | Number of running threads_ThreadsRunning                    | -    | host4kudukudumaster, id4kudukudumaster |

### Kudu - server

| Metric | Description | Unit | Dimension |
| ------------------------------------------------------------ | ------------------------------------------------- | ----------------- | -------------------------------------- |
| KuduServerAllocated<br/>BytesAllocatedbytes                  | Number of allocated bytes_AllocatedBytes                         | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlock<br/>CacheHitBlockcachehit                    | Number of block cache hits_BlockCacheHit                          | -             | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockCache<br/>HitBlockcachemiss                   | Number of block cache hits_BlockCacheMiss                         | -            | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockCache<br/>UsageBlockcacheusage                | Block cache utilization_BlockCacheUsage                      | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockManager<br/>BlockBlockopenreading             | Number of block manager blocks_BlockOpenReading                  | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockManager<br/>BlockBlockopenwriting             | Number of block manager blocks_BlockOpenWriting                  | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockManager<br/>BlockBlockundermanagement         | Number of block manager blocks_BlockUnderManagement              | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockManager<br/>ByteBytesundermanagement          | Number of block manager bytes_BytesUnderManagement               | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerBlockManager<br/>ContainerContainer<br/>sundermanagement | Number of block manager containers_ContainersUnderManagement          | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerContextSwitch<br/>Involuntaryswitches              | Context_InvoluntarySwitches                        | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerContextSwitch<br/>Voluntaryswitches                | Context_VoluntarySwitches                          | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerCpuTimeCpustime                                    | CPU time_CPUStime                                  | ms                | host4kudukuduserver, id4kudukuduserver |
| KuduServerCpuTimeCpuutime                                    | CPU time_CPUUtime                                  | ms                | host4kudukuduserver, id4kudukuduserver |
| KuduServerDataDirDatadirsfailed                              | Number of data paths_DataDirsFailed                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerDataDirDatadirsfull                                | Number of data paths_DataDirsFull                             | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerFileCacheHitFilecachehit                           | Number of file cache hits_FileCacheHit                         | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerFileCacheHit<br/>Filecachemiss                     | Number of file cache hits_FileCacheMiss                        | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerGlogMessages<br/>Errormessages                     | Number of log messages_ErrorMessages                            | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerGlogMessages<br/>Warningmessages                   | Number of log messages_WarningMessages                          | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerHybridClock<br/>ErrorHybridclockerror              | Hybrid clock error_HybridClockError                     | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerHybridClock<br/>TimestampHybridclocktimestamp      | Hybrid clock timestamp_HybridClockTimestamp               | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerNumRaft<br/>LeadersNumraftleaders                  | Number of tablet leaders_NumRaftLeaders                   | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueLengthMax                         | Number of operations in the queue_Max                                  | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueLengthMean                        | Number of operations in the queue_Mean                                 | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueLengthMin                         | Number of operations in the queue_Min                                  | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyQueue<br/>LengthPercentile999               | Number of operations in the queue_Percentile_99_9                      | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyQueue<br/>LengthTotalcount                  | Number of operations in the queue_TotalCount                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueTimeMean                          | Queuing wait time_Mean                                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueTimeMin                           | Queuing wait time_Min                                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueTimePercentile999                 | Queuing wait time_Percentile_99_9                      | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueTimeTotalcount                    | Queuing wait time_TotalCount                           | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyRunTimeMax                                  | Operation execution duration_Max                                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyRunTimeMean                                 | Operation execution duration_Mean                                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyRunTimeMin                                  | Operation execution duration_Min                                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyRun<br/>TimePercentile999                   | Operation execution duration_Percentile_99_9                      | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApplyRun<br/>TimeTotalcount                      | Operation execution duration_TotalCount                           | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcRequest<br/>Connectionsaccepted                 | Number of RPC requests_ConnectionsAccepted                       | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcRequest<br/>Queueoverflow                       | Number of RPC requests_QueueOverflow                             | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcRequest<br/>Timesoutinqueue                     | Number of RPC requests_TimesOutInQueue                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceAlterschemaMax           | AlterSchemaRPC request duration_Max                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceAlterschemaMean          | AlterSchemaRPC request duration_Mean                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceAlterschemaMin           | AlterSchemaRPC request duration_Min                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceAlterschemaPercentile999 | AlterSchemaRPC request duration_Percentile_99_9      | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceAlterschemaTotalcount    | AlterSchemaRPC request duration_TotalCount           | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceCreatetabletMax          | CreateTabletRPC request duration_Max                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceCreatetabletMean         | CreateTabletRPC request duration_Mean                | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceCreatetabletMin          | CreateTabletRPC request duration_Min                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceCreatetabletPercentile999 | CreateTabletRPC request duration_Percentile_99_9     | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceCreatetabletTotalcount   | CreateTabletRPC request duration_TotalCount          | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceDeletetabletMax          | DeleteTabletRPC request duration_Max                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceDeletetabletMin          | DeleteTabletRPC request duration_Min                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceDeletetabletMean         | DeleteTabletRPC request duration_Mean                | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceDeletetabletPercentile999 | DeleteTabletRPC request duration_Percentile_99_9     | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceDeletetabletTotalcount   | DeleteTabletRPC request duration_TotalCount          | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceQuiesceMax               | QuiesceRPC request duration_Max                      | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceQuiesceMean              | QuiesceRPC request duration_Mean                     | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceQuiesceMin               | QuiesceRPC request duration_Min                      | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceQuiescePercentile999     | QuiesceRPC request duration_Percentile_99_9          | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletadmin<br/>serviceQuiesceTotalcount        | QuiesceRPC request duration_TotalCount               | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>copyFetchdataMax                     | FetchDataRPC request duration_Max                    | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>copyFetchdataMean                    | FetchDataRPC request duration_Mean                   | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>copyFetchdataMin                     | FetchDataRPC request duration_Min                    | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletcopy<br/>FetchdataPercentile999           | FetchDataRPC request duration_Percentile_99_9        | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletcopy<br/>FetchdataTotalcount              | FetchDataRPC request duration_TotalCount             | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScannerkeepaliveMax            | ScannerKeepAliveRPC request duration_Max             | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScannerkeepaliveMean           | ScannerKeepAliveRPC request duration_Mean            | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScannerkeepaliveMin            | ScannerKeepAliveRPC request duration_Min             | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScannerkeepalivePercentile999  | ScannerKeepAliveRPC request duration_Percentile_99_9 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScannerkeepaliveTotalcount     | ScannerKeepAliveRPC request duration_TotalCount      | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>serverScanMax                        | ScanRPC request duration_Max                         | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>serverScanMean                       | ScanRPC request duration_Mean                        | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>serverScanMin                        | ScanRPC request duration_Min                         | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScanPercentile999              | ScanRPC request duration_Percentile_99_9             | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>ScanTotalcount                 | ScanRPC request duration_TotalCount                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>serverWriteMax                       | WriteRPC request duration_Max                        | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>serverWriteMean                      | WriteRPC request duration_Mean                       | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTablet<br/>serverWriteMin                       | WriteRPC request duration_Min                        | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>WritePercentile999             | WriteRPC request duration_Percentile_99_9            | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerRpcTabletserver<br/>WriteTotalcount                | WriteRPC request duration_TotalCount                 | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerScannerActivescanners                              | Number of scanners_ActiveScanners                        | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerScannerExpiredscanners                             | Number of scanners_ExpiredScanners                       | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerSpinlockContention<br/>TimeSpinlockcontentiontime  | Spinlock_SpinlockContentionTime                     | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerTabletSession<br/>Opemsourcesessions               | Number of tablet sessions_OpenSourceSessions                | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerTabletSession<br/>Openclientsessions               | Number of tablet sessions_OpenClientSessions                | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerTablet<br/>Tabletbootstrapping                     | Number of tablets_TabletBootstrapping                      | -                | host4kudukuduserver and id4kudukuduserver |
| KuduServer<br/>TabletTabletfailed                            | Number of tablets_TabletFailed                             | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServer<br/>TabletTabletinitialized                       | Number of tablets_TabletInitialized                        | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServer<br/>TabletTabletnotinitialized                    | Number of tablets_TabletNotInitialized                     | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServer<br/>TabletTabletrunning                           | Number of tablets_TabletRunning                            | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServer<br/>TabletTabletshutdown                          | Number of tablets_TabletShutdown                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServer<br/>TabletTabletstopped                           | Number of tablets_ TabletStopped                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServer<br/>TabletTabletstopping                          | Number of tablets_TabletStopping                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerTcmallocMemory<br/>Currentthreadcachebytes         | TCMalloc memory_CurrentThreadCacheBytes              | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerTcmalloc<br/>MemoryHeapsize                        | TCMalloc memory_HeapSize                             | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerTcmallocMemory<br/>Totalthreadcachebytes           | TCMalloc memory_TotalThreadCacheBytes                | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerTcmalloc<br/>PageheapFreebytes                     | TCMallocPageHeap memory_FreeBytes                    | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerTcmalloc<br/>PageheapUnmappedbytes                 | TCMallocPageHeap memory_UnMappedBytes                | Bytes             | host4kudukuduserver, id4kudukuduserver |
| KuduServerThread<br/>Threadsrunning                          | Number of running threads_ThreadsRunning                           | -                | host4kudukuduserver, id4kudukuduserver |
| KuduMasterRpcMasterservice<br/>TsheartbeatTotalcount         | TSHeartbeatRPC request duration_TotalCount           | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>QueueTimeMax                           | Queuing wait time_Max                                  | us                | host4kudukuduserver, id4kudukuduserver |
| KuduServerFileCache<br/>UsageFilecacheusage                  | Number of entries in the file cache                                | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerOpApply<br/>Queueoverloadrejections                | Number of write requests rejected due to queue overloading                                    | -                | host4kudukuduserver, id4kudukuduserver |
| KuduServerScannerBytes<br/>RateScannedfromdiskrate           | Scanner rate_ScannedFromDiskRate                   | Bytes/s           | host4kudukuduserver, id4kudukuduserver |
| KuduServerScannerBytesRate<br/>Scannerreturnedrate           | Scanner rate_ScannerReturnedRate                   | Bytes/s           | host4kudukuduserver, id4kudukuduserver |
| KuduServerScannerBytes<br/>TotalScannedfromdisk              | Total number of scanned bytes_ScannedFromDisk                       | Bytes     | host4kudukuduserver, id4kudukuduserver |
| KuduServerScannerBytes<br/>TotalScannerreturned              | Total number of scanned bytes_ScannerReturned                       | Bytes     | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>CountRowsinserted                    | Total number of row operations_RowsInserted                           | -   | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>CountRowsdeleted                     | Total number of row operations_RowsDeleted                            | -   | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>CountRowsupserted                    | Total number of row operations_RowsUpserted                           | -   | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>CountRowsupdated                     | Total number of row operations_RowsUpdated                            | -   | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>RateRowsinsertedrate                 | Row operation rate_RowsInsertedRate                       | Count/s | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>RateRowsdeletedrate                  | Row operation rate_RowsDeletedRate                        | Count/s | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>RateRowsupsertedrate                 | Row operation rate_RowsUpsertedRate                       | Count/s | host4kudukuduserver, id4kudukuduserver |
| KuduServerRowsTotal<br/>RateRowsupdatedrate                  | Row operation rate_RowsUpdatedRate                        | Count/s | host4kudukuduserver, id4kudukuduserver |

## Dimensions and Parameters

| Parameter | Dimension | Description | Format |
| :----------------------------- | :------------------ | :--------------------------- | :----------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | host4kudukudumaster | Dimension name of the EMR instance node IP | Enter a string-type dimension name, such as `host4kudukudumaster`                |
| Instances.N.Dimensions.0.Value | host4kudukudumaster | Specific node IP in the EMR instance        | Enter a specific node IP, which can be obtained by clicking <b>Instance > Cluster Resource > Resource Management > Node Private IP in the [EMR console](https://console.cloud.tencent.com/emr)</b> or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.1.Name  | id4kudukudumaster   | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `id4kudukudumaster`                  |
| Instances.N.Dimensions.1.Value | id4kudukudumaster   | Dimension name of the EMR instance ID  | Enter an EMR instance ID, such as `emr-mm8bs222`                     |
| Instances.N.Dimensions.0.Name  | host4kudukuduserver | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `host4kudukuduserver`                |
| Instances.N.Dimensions.0.Value | host4kudukuduserver | Specific node IP in the EMR instance        | Enter a specific node IP, which can be obtained by clicking <b>Instance > Cluster Resource > Resource Management > Node Private IP in the [EMR console](https://console.cloud.tencent.com/emr)</b> or calling the [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198) API. |
| Instances.N.Dimensions.1.Name  | id4kudukuduserver   | Dimension name of the EMR instance ID        | Enter a string-type dimension name, such as `id4kudukuduserver`                  |
| Instances.N.Dimensions.1.Value | id4kudukuduserver   | Dimension name of the EMR instance ID  | Enter an EMR instance ID, such as `emr-mm8bs222`                     |

## Input Parameters

#### To query the monitoring data of an EMR instance (Kudu - master), use the following input parameters:

Namespace=QCE/TXMR_KUDU
&Instances.N.Dimensions.0.Name=host4kudukudumaster
&Instances.N.Dimensions.0.Value=Specific node IP in the EMR instance
&Instances.N.Dimensions.1.Name=id4kudukudumaster
&Instances.N.Dimensions.1.Value=EMR instance ID 



#### To query the monitoring data of an EMR instance (Kudu - server), use the following input parameters:

Namespace=QCE/TXMR_KUDU
&Instances.N.Dimensions.0.Name=host4kudukuduserver
&Instances.N.Dimensions.0.Value=Specific node IP in the EMR instance
&Instances.N.Dimensions.1.Name=id4kudukuduserver
&Instances.N.Dimensions.1.Value=EMR instance ID 



