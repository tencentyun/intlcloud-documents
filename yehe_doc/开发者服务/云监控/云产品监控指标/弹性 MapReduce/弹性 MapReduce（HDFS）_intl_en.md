## Namespace

Namespace=QCE/TXMR_HDFS

## Monitoring Metrics

EMR (HDFS) provides the following metrics: [HDFS - Overview](#hdfs-overview), [HDFS - OverviewAggregation](#hdfs-overviewaggregation), [HDFS - NameNode](#hdfs-namenode), [HDFS - DataNode](#hdfs-datanode), [HDFS - Journal Node](#hdfs-journal-node), and [HDFS - ZKFC](#hdfs-zkfc).

>For more information on the parameters in each dimension, please see [Overview of the Parameters in Each Dimension](#.E5.90.84.E7.BB.B4.E5.BA.A6.E5.AF.B9.E5.BA.94.E5.8F.82.E6.95.B0.E6.80.BB.E8.A7.88).

### HDFS - Overview

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ---------------------------------------- | ---- | --------------------------------------------- | --------------------------------------- |
| EmrHdfsOverview<br>HdfsNnBlockCapacityTotal                  | Cluster storage capacity_CapacityTotal               | GB   | Total cluster storage capacity                                | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockCapacityUsed                  | Cluster storage capacity_CapacityUsed                | GB   | Used cluster storage capacity                            | host4hdfsoverview, <br/>id4hdfsoverview |
| EmrHdfsOverview<br/>HdfsNnBlockCapacityRemaining             | Cluster storage capacity_CapacityRemaining           | GB   | Remaining cluster storage capacity                              | host4hdfsoverview, <br/>id4hdfsoverview |
| EmrHdfsOverview<br/>HdfsNnBlockCapacity<br>UsedNonDFS        | Cluster storage capacity_CapacityUsedNonDFS          | GB   | Non-HDFS used cluster capacity                          | host4hdfsoverview, <br/>id4hdfsoverview |
| EmrHdfsOverview<br/>HdfsNnBlockTotalLoad                     | Cluster load_TotalLoad                       | Count   | Number of current connections                                    | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockFilesTotal                    | Total number of cluster files_FilesTotal                  | Count   | Total number of files                                    | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockBlockstotal                   | Number of blocks_BlocksTotal                  | Count   | Total number of blocks                                 | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockPending<br>ReplicationBlocks  | Number of blocks_PendingReplicationBlocks     | Count   | Number of blocks waiting to be backed up                            | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockUnder<br>ReplicatedBlocks     | Number of blocks_UnderReplicatedBlocks        | Count   | Number of blocks with insufficient replicas                            | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockBlocksCorruptblocks           | Number of blocks_CorruptBlocks                | Count   | Number of corrupted blocks                                      | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockScheduled<br>ReplicationBlocks | Number of blocks_ScheduledReplicationBlocks   | Count   | Number of blocks arranged for backup                            | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockPending<br>DeletionBlocks     | Number of blocks_PendingDeletionBlocks        | Count   | Number of blocks waiting to be deleted                            | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockCorruptblocks                 | Number of blocks_CorruptBlocks                | Count   | Number of excessive blocks                                  | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockPostponed<br>MisreplicatedBlocks | Number of blocks_PostponedMisreplicatedBlocks | Count   | Number of blocks with exceptions that were postponed to be processed                         | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockBlockCapacity                 | Capacity of blocks_BlockCapacity                  | Count   | Capacity of blocks                                    | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockNumLiveDataNodes              | Cluster DataNodes_NumLiveDataNodes            | Count   | Number of live DataNodes                            | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockNumDeadDataNodes              | Cluster DataNodes_NumDeadDataNodes            | Count   | Number of DataNodes marked as dead            | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockNum<br>DecomLiveDataNodes     | Cluster DataNodes_NumDecomLiveDataNodes       | Count   | Number of decommissioned live nodes                        | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockNum<br>DecomDeadDataNodes     | Cluster DataNodes_NumDecomDeadDataNodes       | Count   | Number of decommissioned dead nodes                        | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockNum<br>DecommissioningDataNodes | Cluster DataNodes_NumDecommissioningDataNodes | Count   | Number of decommissioning nodes                             | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockNum<br>StaleDataNodes         | Cluster DataNodes_NumStaleDataNodes           | Count   | Number of current DataNodes marked as expired due to heartbeat delay | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockSnapshots                     | Snapshots_Snapshots                  | Count   | Number of snapshots                                | host4hdfsoverview, <br>id4hdfsoverview  |
| EmrHdfsOverview<br/>HdfsNnBlockVolumeFailuresTotal           | Disk failures_VolumeFailuresTotal             | Count   | Total number of failures on all DataNodes                   | host4hdfsoverview, <br>id4hdfsoverview  |

### HDFS - OverviewAggregation 

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ---------------------------------------- | ---- | --------------------------------------------- | --------------- |
| EmrHdfsOverview<br>Aggregation<br>HdfsNnBlockCapacityTotal   | Cluster storage capacity_CapacityTotal               | GB   | Total cluster storage capacity                                | id4hdfsoverview |
| EmrHdfsOverview<br>Aggregation<br/>HdfsNnBlockCapacityUsed   | Cluster storage capacity_CapacityUsed                | GB   | Used cluster storage capacity                            | id4hdfsoverview |
| EmrHdfsOverview<br>AggregationHdfsNn<br>BlockCapacityRemaining | Cluster storage capacity_CapacityRemaining           | GB   | Remaining cluster storage capacity                             | id4hdfsoverview |
| EmrHdfsOverview<br>AggregationHdfsNn<br>BlockCapacity UsedNonDFS | Cluster storage capacity_CapacityUsedNonDFS          | GB   | Non-HDFS used cluster capacity                          | id4hdfsoverview |
| EmrHdfsOverview<br>AggregationHdfsNn<br>BlockTotalLoad       | Cluster load_TotalLoad                       | Count   | Number of current connections                                    | id4hdfsoverview |
| EmrHdfsOverview<br>AggregationHdfsNn<br>BlockFilesTotal      | Total number of cluster files_FilesTotal                  | Count   | Total number of files                                    | id4hdfsoverview |
| EmrHdfsOverview<br>AggregationHdfsNn<br>BlockBlockstotal     | Number of blocks_BlocksTotal                  | Count   | Total number of blocks                                 | id4hdfsoverview |
| EmrHdfsOverview<br>AggregationHdfsNn<br>BlockPending ReplicationBlocks | Number of blocks_PendingReplicationBlocks     | Count   | Number of blocks waiting to be backed up                            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br>BlockUnder ReplicatedBlocks | Number of blocks_UnderReplicatedBlocks        | Count   | Number of blocks with insufficient replicas                            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br>BlockBlocksCorruptblocks | Number of blocks_CorruptBlocks                | Count   | Number of corrupted blocks                                      | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockScheduled ReplicationBlocks | Number of blocks_ScheduledReplicationBlocks   | Count   | Number of blocks arranged for backup                            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockPending DeletionBlocks | Number of blocks_PendingDeletionBlocks        | Count   | Number of blocks waiting to be deleted                            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockCorruptblocks | Number of blocks_CorruptBlocks                | Count   | Number of excessive blocks                                  | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockPostponed MisreplicatedBlocks | Number of blocks_PostponedMisreplicatedBlocks | Count   | Number of blocks with exceptions that were postponed to be processed                        | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockBlockCapacity | Capacity of blocks_BlockCapacity                  | Count   | Capacity of blocks                                    | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockNumLiveDataNodes | Cluster DataNodes_NumLiveDataNodes            | Count   | Number of live DataNodes                            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockNumDeadDataNodes | Cluster DataNodes_NumDeadDataNodes            | Count   | Number of DataNodes marked as dead            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockNum DecomLiveDataNodes | Cluster DataNodes_NumDecomLiveDataNodes       | Count   | Number of decommissioned live nodes                        | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockNum DecomDeadDataNodes | Cluster DataNodes_NumDecomDeadDataNodes       | Count   | Number of decommissioned dead nodes                        | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockNum DecommissioningDataNodes | Cluster DataNodes_NumDecommissioningDataNodes | Count   | Number of decommissioning nodes                            | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockNum StaleDataNodes | Cluster DataNodes_NumStaleDataNodes           | Count   | Number of current DataNodes marked as expired due to heartbeat delay | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockSnapshots     | Snapshots_Snapshots                  | Count   | Number of snapshots                                | id4hdfsoverview |
| EmrHdfsOverview<br/>AggregationHdfsNn<br/>BlockVolumeFailuresTotal | Disk failures_VolumeFailuresTotal             | Count   | Total number of failures on all DataNodes                   | id4hdfsoverview |

### HDFS - NameNode

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ---------------------------------------------------- | --------------------------------------- |
| HdfsNnPort4007RxtxReceivedbytes                              | Data traffic_ReceivedBytes                                       | Bytes/s  | Data receiving rate                                         | host4hdfsnamenode, <br>id4hdfsnamenode  |
| HdfsNnPort4007RxtxSentbytes                                  | Data traffic_SentBytes                                           | Bytes/s  | Data sending rate                                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007Qps<br>Rpcqueuetimenumops                      | QPS_RpcQueueTimeNumOps                                       | Calls/s     | RPC call rate                                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007RtRpc<br>queuetimeavgtime                      | Request processing delay<br>_RpcQueueTimeAvgTime                         | ms       | Average RPC delay                                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007AuthRpc<br>authenticationfailures              | Authentication and authorization<br>_RpcAuthenticationFailure                      | Count       | Number of RPC authentication failures                                      | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007AuthRpc<br>authenticationsuccesses             | Authentication and authorization<br>_RpcAuthenticationSuccesses                    | Count       | Number of RPC authentication successes                                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007AuthRpc<br>authorizationfailures               | Authentication and authorization<br>_RpcAuthorizationFailures                      | Count       | Number of RPC authorization failures                                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007AuthRpc<br>authorizationsuccesses              | Authentication and authorization<br>_RpcAuthorizationSuccesses                     | Count       | Number of RPC authorization successes                                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007Connections<br>Numopenconnections              | Number of current connections<br>_NumOpenConnections                            | Count       | Number of current connections                                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPort4007Queue<br>LenCallqueuelength                    | RPC processing queue length<br>_CallQueueLength                         | Count       | Length of current RPC processing queue                                | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmMemMemnonheapusedm                                  | JVM memory<br>_MemNonHeapUsedM                                 | MB       | Size of the NonHeapMemory currently used by JVM              | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmMemMemnon<br>heapcommittedm                         | JVM memory<br>_MemNonHeapCommittedM                            | MB       | JVM memory                                             | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmMemMemheapusedm                                     | JVM memory<br>_MemHeapUsedM                                    | MB       | Size of the HeapMemory currently used by JVM                 | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmMem<br>Memheapcommittedm                            | JVM memory<br>_MemHeapCommittedM                               | MB       | Size of the HeapMemory committed by JVM                              | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmMemMemheapmaxm                                      | JVM memory_MemHeapMaxM                                         | MB       | Size of the HeapMemory configured by JVM                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmMemMemmaxm                                          | JVM memory_MemMaxM                                             | MB       | Maximum memory size that can be used by JVM during runtime               | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnBlockReportRt<br>Blockreportavgtime                    | Block reporting delay<br>_BlockReportAvgTime                        | Blocks/s     | Average delay in processing DataNode blocks per second                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilGcCountFgc                                       | GC count_FGC                                                  | Operations/s     | Full GC count                                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilGcCountYgc                                       | GC count_YGC                                                   | 2 operations/s    | Young GC count                                        | host4hdfsnamenode, <br>id4hdfsnamenode  |
| HdfsNnGcUtilGcTimeYgct                                       | GC time_YGCT                                                 | ms       | Time consumed by Young GC                                    | host4hdfsnamenode, <br>id4hdfsnamenode  |
| HdfsNnGcUtilGcTimeFgct                                       | GC time_FGCT                                                 | ms       | Time consumed by Full GC                                     | host4hdfsnamenode, <br>id4hdfsnamenode  |
| HdfsNnGcUtilGcTimeGct                                        | GC time_GCT                                                  | ms       | Time used to collect garbage                                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmJavaThreadsThreadsnew                               | Number of JVM threads<br>_ThreadsNew                                  | Count       | Number of threads in the new state                               | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmJavaThreads<br>Threadsrunnable                      | Number of JVM threads<br>_ThreadsRunnable                             | Count       | Number of threads in the runnable state                             | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmJavaThreads<br>Threadsblocked                       | Number of JVM threads<br>_ThreadsBlocked                              | Count       | Number of threads in the blocked state                               | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmJavaThreads<br>Threadswaiting                       | Number of JVM threads<br>_ThreadsWaiting                              | Count       | Number of threads in the WAITING state                          | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmJavaThreads<br>Threadstimedwaiting                  | Number of JVM threads<br>_ThreadsTimedWaiting                         | Count       | Number of threads in the TIMED WAITING state                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmJavaThreads<br>Threadsterminated                    | Number of JVM threads<br>_ThreadsTerminated                           | Count       | Number of threads in the Terminated state                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmLogTotalLogfatal                                    | Number of JVM logs_LogFatal                                        | Count       | Number of Fatal logs                                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmLogTotalLogerror                                    | Number of JVM logs_LogError                                        | Count       | Number of Error logs                                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmLogTotalLogwarn                                     | Number of JVM logs_LogWarn                                         | Count       | Number of Warn logs                                        | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnJvmLogTotalLoginfo                                     | Number of JVM logs_LogInfo                                         | Count       | Number of Info logs                                        | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilMemoryS0                                         | Memory space percentage_S0                                              | %        | Percentage of used Survivor 0 memory                             | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilMemoryS1                                         | Memory space percentage_S1                                              | %        | Percentage of used Survivor 1 memory                             | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilMemoryE                                          | Memory space percentage_E                                               | %        | Percentage of used Eden memory                                  | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilMemoryO                                          | Memory space percentage_O                                               | %        | Percentage of used Old memory                                   | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilMemoryM                                          | Memory space percentage_M                                               | %        | Percentage of used Metaspace memory                             | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnGcUtilMemoryCcs                                        | Memory space percentage_CCS                                             | %        | Percentage of memory used by compressed class space                | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnStaleStorages<br>CountNumstalestorages                 | Number of storages marked as expired<br>_NumStaleStorages                | Count       | Number of current DataNodes marked as expired due to heartbeat delay        | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnPendingDatanodeMessage<br>CountPendingdatanode<br/>messagecount | Number of pending block operation messages on the standby NameNode<br>_PendingDataNode<br/>MessageCount | Requests/s     | Number of DataNode requests queued on the standby NameNode | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnBlocksMissingNum<br>berofmissingblocks                 | Total number of missing blocks<br>_NumberOfMissingBlocks                         | Count       | Number of missing data blocks                                     | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnBlocksMissingNumberof<br>missingblockswithreplication<br/>factorOne | Total number of missing blocks_NumberOf<br>MissingBlocksWithReplication<br/>FactorOne | Count       | Number of missing blocks (rf = 1)                           | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOpsAllowsnapshotops                            | Snapshot operations<br>_AllowSnapshotOps                           | Operations/s     | Number of AllowSnapshot operations executed per second                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOps<br>Disallowsnapshotops                     | Snapshot operations<br>_DisallowSnapshotOps                        | Operations/s     | Number of DisallowSnapshot operations executed per second                 | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOps<br>Createsnapshotops                       | Snapshot operations<br>_CreateSnapshotOps                          | Operations/s     | Number of CreateSnapshot operations executed per second                   | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOps<br>Deletesnapshotops                       | Snapshot operations<br>_DeleteSnapshotOps                          | Operations/s     | Number of DeleteSnapshot operations executed per second                   | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOps<br>Listsnapshottabledirops                 | Snapshot operations_ListSnapshottableDirOps                        | Operations/s     | Number of ListSnapshottableDir operations executed per second               | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOps<br>Snapshotdiffreportops                   | Snapshot operations_SnapshotDiffReportOps                          | Operations/s     | Number of SnapshotDiffReportOps operations executed per second                | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSnapshotOps<br>Renamesnapshotops                       | Snapshot operations_RenameSnapshotOps                              | Operations/s     | Number of RenameSnapshotOps operations executed per second                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsCreatefileops                                  | File operations_CreateFileOps                                       | Operations/s     | Number of CreateFile operations executed per second                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsGetlistingops                                  | File operations_GetListingOps                                       | Operations/s     | Number of GetListing operations executed per second                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsTotalfileops                                   | File operations_TotalFileOps                                        | Operations/s     | Number of TotalFileOps operations executed per second                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsDeletefileops                                  | File operations_DeleteFileOps                                       | Operations/s     | Number of DeleteFile operations executed per second                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsFileinfoops                                    | File operations_FileInfoOps                                         | Operations/s     | Number of FileInfo operations executed per second                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsGetadditional<br>datanodeops                   | File operations<br>_GetAdditionalDatanodeOps                        | Operations/s     | Number of GetAdditionalDatanode operations executed per second            | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsCreatesymlinkops                               | File operations_CreateSymlinkOps                                    | Operations/s     | Number of CreateSymlink operations executed per second                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsGetlinktargetops                               | File operations_GetLinkTargetOps                                    | Operations/s     | Number of GetLinkTarget operations executed per second                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnFilesOpsFilesingetlistingops                           | File operations<br>_FilesInGetListingOps                            | Operations/s     | Number of FilesInGetListing operations executed per second                | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnTransactionOps<br>Transactionsnumops                   | Transaction operations<br>_TransactionsNumOps                              | Operations/s     | Number of Journal transaction operations processed per second              | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnTransactionOps<br>Transactionsbatchedinsync            | Transaction operations<br>_TransactionsBatchedInSync                       | Operations/s     | Number of Journal transaction operations processed in batches per second            | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnImageOpsGeteditnumops                                  | Image operations_GetEditNumOps                                       | Operations/s     | Number of GetEditNumOps operations executed per second                        | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnImageOpsGetimagenumops                                 | Image operations_GetImageNumOps                                      | Operations/s     | Number of GetImageNumOps operations executed per second                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnImageOpsPutimagenumops                                 | Image operations_PutImageNumOps                                      | Operations/s     | Number of PutImageNumOps operations executed per second                       | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSyncsOpsSyncsnumops                                    | Sync operations_SyncsNumOps                                        | Operations/s     | Number of Journal syncs operations processed per second                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnBlocksOpsBlock<br>receivedanddeletedops                | Data block operations<br/>_BlockOpsQueued                               | Operations/s     | Number of BlockReceivedAndDeletedOps operations executed per second           | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnBlocksOpsBlockopsqueued                                | Data block operations<br/>_BlockOpsQueued                               | Operations/s     | Delay in processing DataNode block reporting operations                   | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnCacheReportOps<br>Cachereportnumops                    | Cache reporting<br/>_CacheReportNumOps                              | Operations/s     | Number of CacheReport operations processed per second                      | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnBlockReportOps<br>Blockreportnumops                    | Block reporting<br/>_BlockReportNumOps                            | Operations/s     | Number of DataNode block reporting operations processed per second               | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnSyncsRtSyncsavgtime                                    | Sync operation delay_SyncsAvgTime                                  | ms       | Average delay in processing Journal syncs operations                    | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnCacheReportRt<br>Cachereportavgtime                    | Cache reporting delay_CacheReportAvgTime                            | ms       | Average delay in cache reporting operations                                 | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnImageRtGeteditavgtime                                  | Image operation delay<br/>_GetEditAvgTime                             | ms       | Average delay in reading the Edit file                           | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnImageRtGetimageavgtime                                 | Image operation delay<br/>_GetImageAvgTime                            | ms       | Average delay in reading the image file                                 | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnImageRtPutimageavgtime                                 | Image operation delay<br/>_PutImageAvgTime                            | ms       | Average delay in writing the image file                                 | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnTransactionRt<br>Transactionsavgtime                   | Transaction operation delay<br/>_TransactionsAvgTime                        | ms       | Average delay in processing Journal transaction operations              | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnStartTimeStarttime                                     | Start time_StartTime                                           | ms       | Process start time                                         | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnStateState                                             | Primary/secondary status_State                                               | -        | NN status                                              | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnThreadCountPeakthreadcount                             | Number of threads_PeakThreadCount                                     | Count       | Peak number of threads                                           | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnThreadCountThreadcount                                 | Number of threads_ThreadCount                                         | Count       | Number of threads                                             | host4hdfsnamenode, <br>id4hdfsnamenode |
| HdfsNnThreadCount<br>Daemonthreadcount                       | Number of threads_DaemonThreadCount                                   | Count       | Number of background threads                                         | host4hdfsnamenode, <br>id4hdfsnamenode |

### HDFS - DataNode

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------------------------------------ | -------------------------------------- |
| HdfsDnXceiverXceivercount                                    | Number of Xceivers_XceiverCount                                    | Xceivers       | Number of Xceivers                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBytesByteswrittenmb                                    | Data read/write rate_BytesReadMB                                     | Bytes/s  | DN byte write rate                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBytesBytesreadmb                                       | Data read/write rate_BytesReadMB                                     | Bytes/s  | DN byte read rate                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBytesRemotebytesreadmb                                 | Data read/write rate<br/>_RemoteBytesReadMB                          | Bytes/s  | Rate of bytes read by the remote client                     | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBytesRemoteby<br>teswrittenmb                          | Data read/write rate<br/>_RemoteBytesWrittenMB                       | Bytes/s  | Rate of bytes written by the remote client                     | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnClientWritesfrom<br>remoteclient                       | Number of client connections<br/>_WritesFromRemoteClient                     | Count       | QPS of write operations from the remote client                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnClientWritesfromlocalclient                            | Number of client connections<br/>_WritesFromLocalClient                      | Count       | OPS of write operations from the local client                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnClientReadsfrom<br>remoteclient                        | Number of client connections<br/>_ReadsFromRemoteClient                      | Count       | QPS of read operations from the remote client                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnClientReadsfromlocalclient                             | Number of client connections<br/>_ReadsFromLocalClient                       | Count       | QPS of read operations from the local client                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksVerifiedFailures<br>Blockverificationfailures    | Block check failure<br/>_BlockVerificationFailures                | Failures/s     | Number of block check failures                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnVolumeFailures<br>Volumefailures                       | Disk failures_VolumeFailures                                      | Failures/s     | Number of disk failures                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnNetworkErrors<br>Datanodenetworkerrors                 | Network errors<br/>_DatanodeNetworkErrors                          | Errors/s     | Total number of network errors                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnHbRtHeartbeatsavgtime                                  | Heartbeat delay_HeartbeatsAvgTime                                   | ms       | Average heartbeat API time                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnHbOpsHeartbeatsnumops                                  | Heartbeat QPS_HeartbeatsNumOps                                    | Heartbeats/s     | Heartbeat API QPS                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnDatapacketAvgtimeSend<br>datapackettransfer<br/>nanosavgtime | Packet transfer operations<br/>QPS_SendDataPacketTransfer<br/>NanosAvgTime  | ms       | Average data packet sending time                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsRead<br>blockopnumops                         | Data block operations<br/>_ReadBlockOpNumOps                            | Operations/s     | OPS of block reads from the DataNode                 | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsWrite<br>blockopnumops                        | Data block operations<br/>_WriteBlockOpNumOps                           | Operations/s     | OPS of block writes to the DataNode                 | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsBlock<br>checksumopnumops                     | Data block operations<br/>_BlockChecksumOpNumOps                        | Operations/s     | OPS of Checksum operations by the DataNode          | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsCopy<br>blockopnumops                         | Data block operations<br/>_CopyBlockOpNumOps                            | Operations/s     | OPS of block copying operations                      | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsReplace<br>blockopnumops                      | Data block operations<br/>_ReplaceBlockOpNumOps                         | Operations/s     | OPS of Replace Block operations                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsBlock<br>reportsnumops                        | Data block operations<br/>_BlockReportsNumOps                           | Operations/s     | OPS of block reporting operations                       | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsIncremental<br>blockreports<br/>numops        | Data block operations<br/>_IncrementalBlockReports<br/>NumOps           | Operations/s     | OPS of incremental block reporting                       | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsCache<br>reportsnumops                        | Data block operations<br/>_CacheReportsNumOps                           | Operations/s     | OPS of cache reporting                             | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksOpsPacketack<br>roundtriptimenanos<br/>numops    | Data block operations<br/>_PacketAckRoundTripTimeNanos<br/>NumOps       | Operations/s     | Number of ACK ROUND TRIP operations processed per second               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnFsyncOpsFsync<br>nanosnumops                           | Fsync operations<br/>_FsyncNanosNumOps                             | Operations/s     | Number of Fsync operations                                 | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnFlushOpsFlush<br>nanosnumops                           | Flush operations<br/>_FlushNanosNumOps                             | Operations/s     | Number of Flush operations processed per second                    | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtRead<br>blockopavgtime                         | Data block operation delay<br/>_ReadBlockOpAvgTime                   | ms       | Average block read time                    | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtWrite<br>blockopavgtime                        | Data block operation delay<br/>_ReplaceBlockOpAvgTime                | ms       | Average block write time                      | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtBlock<br>checksumopavgtime                     | Data block operation delay_BlockChecksumOpAvgTime                    | ms       | Average block check time                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtCopy<br>blockopavgtime                         | Data block operation delay<br/>_CopyBlockOpAvgTime                   | ms       | Average block copy time                          | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRt<br>Replaceblockopavgtime                      | Data block operation delay<br/>_Replaceblockopavgtime                | ms       | Average Replace Block operation time                 | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtBlock<br>reportsavgtime                        | Data block operation delay<br/>_BlockReportsAvgTime                  | ms       | Average block reporting time                             | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtIncremental<br>blockreportsavgtime             | Data block operation delay<br/>_IncrementalBlockReportsAvgTime       | ms       | Average time of incremental block reporting                          | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtCache<br>reportsavgtime                        | Data block operation delay<br/>_CacheReportsAvgTime                  | ms       | Average time of cache reporting                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnBlocksRtPacketack<br>roundtriptimenanos<br/>avgtime    | Data block operation delay<br/>_PacketAckRoundTripTimeNanos<br/>AvgTime | ms       | Average time of processing ACK ROUND TRIP               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnFlushRtFlushnanosavgtime                               | Flush delay_FlushNanosAvgTime                                  | ms       | Average Flush operation time                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnFsyncRtFsyncnanosavgtime                               | Fsync delay_FsyncNanosAvgTime                                  | ms       | Average Fsync operation time                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblockswrite                      | RAMDISKBlocks_Ram<br/>DiskBlocksWrite                        | Blocks/s     | Total number of blocks written to the memory                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblockswritefallback              | RAMDISKBlocks_Ram<br/>DiskBlocksWriteFallback                | Blocks/s     | Total number of blocks failed to be written to the memory (failover to the disk)  | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOpRamdisk<br>blocksdeletedbeforelazypersisted | RAMDISKBlocks_RamDiskBlocks<br>DeletedBeforeLazyPersisted    | Blocks/s     | Total number of blocks deleted before the application is saved to the disk | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblocksreadhits                   | RAMDISKBlocks_Ram<br/>DiskBlocksReadHits                     | Blocks/s     | Total number of reads from the blocks in the memory                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblocksevicted                    | RAMDISKBlocks_Ram<br/>DiskBlocksEvicted                      | Blocks/s     | Total number of blocks cleared in the memory                       | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOpRamdisk<br>blocksevictedwithoutread         | RAMDISKBlocks_RamDiskBlocks<br>EvictedWithoutRead            | Blocks/s     | Total number of blocks retrieved from the memory                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblockslazypersisted              | RAMDISKBlocks_RamDisk<br>BlocksLazyPersisted                 | Blocks/s     | Number of disk writes by the lazy writer                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskbyteslazypersisted               | RAMDISKBlocks_Ram<br/>DiskBytesLazyPersisted                 | Bytes/s  | Total number of bytes written to the disk by the lazy writer             | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRamBlocksBytes<br>Ramdiskbyteswrite                    | RAM Disk write speed_RamDiskBytesWrite                           | Bytes/s  | Total number of bytes written to the memory                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmMem<br>Memnonheapusedm                              | JVM memory<br/>_MemNonHeapUsedM                                | MB       | Size of the NonHeapMemory currently used by JVM    | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmMem<br>Memnonheapcommittedm                         | JVM memory<br/>_MemNonHeapCommittedM                           | MB       | Size of the NonHeapCommittedM configured by JVM        | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmMemMemheapusedm                                     | JVM memory<br/>_MemHeapUsedM                                   | MB       | Size of the HeapMemory currently used by JVM       | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmMem<br>Memheapcommittedm                            | JVM memory<br/>_MemHeapCommittedM                              | MB       | Size of the HeapMemory committed by JVM                    | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmMemMemheapmaxm                                      | JVM memory<br/>_MemHeapMaxM                                    | MB       | Size of the HeapMemory configured by JVM               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmMemMemmaxm                                          | JVM memory<br/>_MemMaxM                                        | MB       | Maximum memory size that can be used by JVM during runtime     | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreadsThreadsnew                               | Number of JVM threads<br/>_ThreadsNew                                 | Count       | Number of threads in the new state                     | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadsrunnable                      | Number of JVM threads<br/>_ThreadsRunnable                            | Count       | Number of threads in the runnable state                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadsblocked                       | Number of JVM threads<br/>_ThreadsBlocked                              | Count       | Number of threads in the blocked state                     | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadswaiting                       | Number of JVM threads<br/>_ThreadsWaiting                             | Count       | Number of threads in the WAITING state                | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadstimedwaiting                  | Number of JVM threads<br/>_ThreadsTimedWaiting                        | Count       | Number of threads in the TIMED WAITING state          | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadsterminated                    | Number of JVM threads<br/>_ThreadsTerminated                          | Count       | Number of threads in the Terminated state             | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLogfatal                                    | Number of JVM logs_LogFatal                                        | Count       | Number of Fatal logs                             | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLogerror                                    | Number of JVM logs_LogError                                        | Count       | Number of Error logs                             | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLogwarn                                     | Number of JVM logs_LogWarn                                         | Count       | Number of Warn logs                              | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLoginfo                                     | Number of JVM logs_LogInfo                                         | Count       | Number of Info logs                              | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryS0                                         | Memory space percentage_S0                                              | %        | Percentage of used Survivor 0 memory                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryS1                                         | Memory space percentage_S1                                              | %        | Percentage of used Survivor 1 memory                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryE                                          | Memory space percentage_E                                               | %        | Percentage of used Eden memory                        | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryO                                          | Memory space percentage_O                                               | %        | Percentage of used Old memory                         | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryM                                          | Memory space percentage_M                                               | %        | Percentage of used Metaspace memory                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryCcs                                        | Memory space percentage_CCS                                             | %        | Percentage of memory used by compressed class space      | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilGcCountFgc                                       | GC count_FGC                                                  | Count       | Full GC count                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilGcCountYgc                                       | GC count_YGC                                                  | Count       | Young GC count                              | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilGcTimeYgct                                       | GC time_YGCT                                                 | s        | Time consumed by Young GC                          | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilGcTimeFgct                                       | GC time_FGCT                                                 | s        | Time consumed by Full GC                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnGcUtilGcTimeGct                                        | GC time_GCT                                                  | s        | Time used to collect garbage                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004RxtxReceivedbytes                              | Data traffic_ReceivedBytes                                       | Bytes/s  | Data receiving rate                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004RxtxSentbytes                                  | Data traffic_SentBytes                                           | Bytes/s  | Data sending rate                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004QpsRpc<br>queuetimenumops                      | QPS_RpcQueueTimeNumOps                                       | Queries/s     | RPC call rate                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004RtRpc<br>queuetimeavgtime                      | Request processing delay<br/>_RpcQueueTimeAvgTime                        | ms       | Average RPC delay                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authenticationfailures              | Authentication and authorization<br/>_RpcAuthenticationFailures                    | Failures/s     | Number of RPC authentication failures                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authenticationsuccesses             | Authentication and authorization<br/>_RpcAuthenticationSuccesses                   | Successes/s     | Number of RPC authentication successes                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authorizationfailures               | Authentication and authorization<br/>_RpcAuthorizationFailures                     | Failures/s     | Number of RPC authorization failures                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authorizationsuccesses              | Authentication and authorization<br/>_RpcAuthorizationSuccesses                    | Successes/s     | Number RPC authorization successes                           | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004Connections<br>Numopenconnections              | Number of current connections<br/>_NumOpenConnections                           | Count       | Number of current connections                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnPort4004QueueLen<br>Callqueuelength                    | RPC processing queue length<br/>_CallQueueLength                        | Count       | Length of the current RPC processing queue                      | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnThreadTimeCurrent<br>threadcputime                     | CPU time<br/>_CurrentThreadCpuTime                           | ms       | CPU time                                    | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnThreadTimeCurrent<br>threadusertime                    | CPU time<br/>_CurrentThreadUserTime                          | ms       | User time                                   | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnStartTimeStarttime                                     | Start time_StartTime                              | s        | Process start time                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnThreadCount<br>Peakthreadcount                         | Number of threads_PeakThreadCount                                       | Count       | Peak number of threads                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnThreadCount<br>Daemonthreadcount                       | Number of threads_DaemonThreadCount                                   | Count       | Number of background threads                               | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRtWrit                                                 | Read/write delay_Write                                               | MB/s     | Disk write rate                                 | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnRtRead                                                 | Read/write delay_Read                                                | Queries/s     | Read QPS                                 | id4hdfsdatanode, <br>host4hdfsdatanode |
| HdfsDnDatapacketOps<br>Datapacketops                         | Packet transfer QPS_DataPacketOps                                 | Queries/s     | Packet transfer QPS                             | id4hdfsdatanode, <br>host4hdfsdatanode |

### HDFS - Journal Node 

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------ | ------------------------------------- | -------- | --------------------------------------- | --------------------------------------------- |
| HdfsJnJvmMemMemnon<br>heapusedm                  | JVM memory_MemNonHeapUsedM              | MB       | Size of the NonHeapMemory currently used by JVM | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmMemMemnon<br>heapcommittedm             | JVM memory_MemNonHeapCommittedM         | MB       | JVM memory                                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmMemMem<br>heapusedm                     | JVM memory_MemHeapUsedM                 | MB       | Size of the HeapMemory currently used by JVM    | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmMemMem<br>heapcommittedm                | JVM memory_MemHeapCommittedM            | MB       | Size of the HeapMemory committed by JVM                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmMemMem<br>heapmaxm                      | JVM memory_MemHeapMaxM                  | MB       | Size of the HeapMemory configured by JVM            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmMemMemmaxm                              | JVM memory_MemMaxM                      | MB       | Maximum memory size that can be used by JVM during runtime  | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmJavaThreads<br>Threadsnew               | Number of JVM threads_ThreadsNew               | Count       | Number of threads in the new state                  | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmJavaThreads<br>Threadsrunnable          | Number of JVM threads_ThreadsRunnable          | Count       | Number of threads in the runnable state               | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmJavaThreads<br>Threadsblocked           | Number of JVM threads_ThreadsBlocked           | Count       | Number of threads in the blocked state                  | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmJavaThreads<br>Threadswaiting             | Number of JVM threads_ThreadsWaiting           | Count       | Number of threads in the WAITING state             | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmJavaThreads<br>Threadstimedwaiting      | Number of JVM threads_ThreadsTimedWaiting      | Count       | Number of threads in the TIMED WAITING state        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmJavaThreads<br>Threadsterminated        | Number of JVM threads_ThreadsTerminated        | Count       | Number of threads in the Terminated state          | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmLogTotalLogfatal                        | Number of JVM logs_LogFatal                 | Count       | Number of Fatal logs                          | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmLogTotalLogerror                        | Number of JVM logs_LogError                 | Count       | Number of Error logs                          | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmLogTotalLogwarn                         | Number of JVM logs_LogWarn                  | Count       | Number of Warn logs                           | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnJvmLogTotalLoginfo                         | Number of JVM logs_LogInfo                  | Count       | Number of Info logs                           | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilMemoryS0                             | Memory space percentage_S0                       | %        | Percentage of used Survivor 0 memory                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilMemoryS1                             | Memory space percentage_S1                       | %        | Percentage of used Survivor 1 memory                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilMemoryE                              | Memory space percentage_E                        | %        | Percentage of used Eden memory                     | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilMemoryO                              | Memory space percentage_O                        | %        | Percentage of used Old memory                      | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilMemoryM                              | Memory space percentage_M                        | %        | Percentage of used Metaspace memory                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilMemoryCcs                            | Memory space percentage_CCS                      | %        | Percentage of memory used by compressed class space   | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilGcCountFgc                           | GC count_FGC                           | Count       | Full GC count                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilGcCountYgc                           | GC count_YGC                           | Count       | Young GC count                           | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilGcTimeYgct                           | GC time_YGCT                          | s        | Time consumed by Young GC                       | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilGcTimeFgct                           | GC time_FGCT                          | s        | Time consumed by Full GC                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnGcUtilGcTimeGct                            | GC time_GC                            | s        | Time used to collect garbage                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005Rxtx<br>Receivedbytes              | Data traffic_ReceivedBytes                | Bytes/s  | Data receiving rate                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005Rxtx<br>Receivedbytes              | Data traffic_ReceivedBytes                | Bytes/s  | Data sending rate                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005QpsRpc<br>queuetimenumops          | QPS_RpcQueueTimeNumOps                | Queries/s     | RPC call rate                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005RtRpc<br>queuetimeavgtime          | Request processing delay_RpcQueueTimeAvgTime      | ms       | Average RPC delay                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005AuthRpc<br>authenticationfailures  | Authentication and authorization_RpcAuthenticationFailures  | Failures/s     | Number of RPC authentication failures                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005AuthRpc<br>authorizationsuccesses  | Authentication and authorization_RpcAuthorizationSuccesses  | Successes/s     | Number of RPC authorization successes                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005AuthRpc<br>authenticationsuccesses | Authentication and authorization_RpcAuthenticationSuccesses | Successes/s     | Number of RPC authentication successes                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005AuthRpc<br>authorizationfailures   | Authentication and authorization_RpcAuthorizationFailures   | Failures/s     | Number of RPC authorization failures                        | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005Connections<br>Numopenconnections  | Number of current connections_NumOpenConnections         | Count       | Number of current connections                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnPort4005QueueLen<br>Callqueuelength        | RPC processing queue length_CallQueueLength      | Count       | Length of the current RPC processing queue                   | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnThreadTimeCurrent<br>threadcputime         | CPU time_CurrentThreadCpuTime         | ms       | CPU time                                 | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnThreadTimeCurrent<br>threadusertime        | CPU time_CurrentThreadUserTime        | ms       | User time                                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnStartTimeStarttime                         | Start time_StartTime                    | s        | Process start time                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnThreadCount<br>Threadcount                 | Number of threads_ThreadCount                  | Count       | Number of threads                                | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnThreadCount<br>Peakthreadcount             | Number of threads_PeakThreadCount              | Count       | Peak number of threads                            | host4hdfsjournalnode, <br>id4hdfsjournalnode  |
| HdfsJnThreadCountDaemon<br>threadcount           | Number of threads_DaemonThreadCount            | Count       | Number of background threads                            | host4hdfsjournalnode, <br/>id4hdfsjournalnode |

### HDFS - ZKFC

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------ | ---------------- | -------- | ------------------------------------- | ------------------------------------------------------------ |
| HdfsDfzkGcUtilMemoryS0   | Memory space percentage_S0  | %        | Percentage of used Survivor 0 memory              | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilMemoryS1   | Memory space percentage_S1  | %        | Percentage of used Survivor 1 memory              | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilMemoryE    | Memory space percentage_E   | %        | Percentage of used Eden memory                   | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilMemoryO    | Memory space percentage_O   | %        | Percentage of used Old memory                    | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilMemoryM    | Memory space percentage_M   | %        | Percentage of used Metaspace memory              | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilMemoryCcs  | Memory space percentage_CCS | %        | Percentage of memory used by compressed class space | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilGcCountFgc | GC count_FGC       | Count       | Full GC count                          | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilGcCountYgc | GC count_YGC       | Count       | Young GC count                         | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilGcTimeYgct | GC time_YGCT      | s        | Time consumed by Young GC                     | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilGcTimeFgct | GC time_FGCT      | s        | Time consumed by Full GC                      | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |
| HdfsDfzkGcUtilGcTimeGct  | GC time_GCT       | s        | Time used to collect garbage                      | host4hdfszkfailovercontroller, <br>id4hdfszkfailovercontroller |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------------------------- | ----------------------------- | ------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4hdfsoverview               | Dimension name of the EMR instance ID        | String-type dimension name, such as id4hdfsoverview              |
| Instances.N.Dimensions.0.Value | id4hdfsoverview               | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222              |
| Instances.N.Dimensions.1.Name  | host4hdfsoverview             | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hdfsoverview             |
| Instances.N.Dimensions.1.Value | host4hdfsoverview             | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                        |
| Instances.N.Dimensions.0.Name  | id4hdfsnamenode               | Dimension name of the EMR instance ID        | String-type dimension name, such as id4hdfsnamenode              |
| Instances.N.Dimensions.0.Value | id4hdfsnamenode               | Specific EMR instance ID               | Specific EMR instance ID, such as emr-mm8bs222              |
| Instances.N.Dimensions.1.Name  | host4hdfsnamenode             | Dimension name of the node IP in the EMR instance  | String-type dimension name, such as host4hdfsnamenode             |
| Instances.N.Dimensions.1.Value | host4hdfsnamenode             | Specific node IP in the EMR instance         | Specific node IP, such as 1.1.1.1                         |
| Instances.N.Dimensions.0.Name  | id4hdfsdatanode               | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hdfsdatanode              |
| Instances.N.Dimensions.0.Value | id4hdfsdatanode               | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222              |
| Instances.N.Dimensions.1.Name  | host4hdfsdatanode             | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hdfsdatanode             |
| Instances.N.Dimensions.1.Value | host4hdfsdatanode             | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                         |
| Instances.N.Dimensions.0.Name  | id4hdfsjournalnode            | Dimension name of the EMR instance ID        | String-type dimension name, such as id4hdfsjournalnode           |
| Instances.N.Dimensions.0.Value | id4hdfsjournalnode            | Specific EMR instance ID               | Specific EMR instance ID, such as emr-mm8bs222              |
| Instances.N.Dimensions.1.Name  | host4hdfsjournalnode          | Dimension name of the node IP in the EMR instance  | String-type dimension name, such as host4hdfsjournalnode          |
| Instances.N.Dimensions.1.Value | host4hdfsjournalnode          | Specific node IP in the EMR instance         | Specific node IP, such as 1.1.1.1                         |
| Instances.N.Dimensions.0.Name  | id4hdfszkfailovercontroller   | Dimension name of the EMR instance ID       | String-type dimension name, such as id4hdfszkfailovercontroller  |
| Instances.N.Dimensions.0.Value | id4hdfszkfailovercontroller   | Specific EMR instance ID              | Specific EMR instance ID, such as emr-mm8bs222              |
| Instances.N.Dimensions.1.Name  | host4hdfszkfailovercontroller | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4hdfszkfailovercontroller |
| Instances.N.Dimensions.1.Value | host4hdfszkfailovercontroller | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1                        |

## Input Parameters

EMR (HDFS) supports querying monitoring data based on the following six combinations of dimensions. The values for the input parameters are as follows: 

**1. To query the metric monitoring data of HDFS - OverviewAggregation, use the following input parameters:**
&Namespace=QCE/TXMR_HDFS
&Instances.N.Dimensions.0.Name=id4hdfsoverview 
&Instances.N.Dimensions.0.Value=EMR instance ID 

**2. To query the metric monitoring data of HDFS - Overview, use the following input parameters:**
&Namespace=QCE/TXMR_HDFS
&Instances.N.Dimensions.0.Name=id4hdfsoverview
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4hdfsoverview
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**3. To query the metric monitoring data of HDFS - NameNode, use the following input parameters:**
&Namespace=QCE/TXMR_HDFS
&Instances.N.Dimensions.0.Name=id4hdfsnamenode
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4hdfsnamenode
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**4. To query the metric monitoring data of HDFS - DataNode, use the following input parameters:**
&Namespace=QCE/TXMR_HDFS
&Instances.N.Dimensions.0.Name=id4hdfsdatanode
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4hdfsdatanode 
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**5. To query the metric monitoring data of HDFS - Journal Node, use the following input parameters:**
&Namespace=QCE/TXMR_HDFS 
&Instances.N.Dimensions.0.Name=id4hdfsjournalnode
&Instances.N.Dimensions.0.Value=Specific EMR instance ID
&Instances.N.Dimensions.1.Name=host4hdfsjournalnode
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**6. To query the metric monitoring data of HDFS - ZKFC, use the following input parameters:**
&Namespace=QCE/TXMR_HDFS 
&Instances.N.Dimensions.0.Name=id4hdfszkfailovercontroller
&Instances.N.Dimensions.0.Value=Specific EMR instance ID
&Instances.N.Dimensions.1.Name=host4hdfszkfailovercontroller
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 




