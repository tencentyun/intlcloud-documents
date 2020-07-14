## Namespace

Namespace=QCE/TXMR_HDFS

## Monitoring Metrics

The elastic MapReduce (HDFS) service provides the following metrics: [HDFS-Overview, HDFS-OverviewAggregation](#hdfs-overview.E3.80.81hdfs-overviewaggregation), [HDFS-NameNode](#hdfs-namenode), [HDFS-DataNode](#hdfs-datanode), [HDFS-Journal Node](#hdfs-journal-node), and [HDFS-ZKFC](#hdfs-zkfc).

> For parameters corresponding to different dimensions, see the [Overview of the Parameters at Each Dimension](#.E5.90.84.E7.BB.B4.E5.BA.A6.E5.AF.B9.E5.BA.94.E5.8F.82.E6.95.B0.E6.80.BB.E8.A7.88).

### HDFS-Overview and HDFS-OverviewAggregation 

>
>
> 1. To query the metrics of HDFS-Overview, add the "EmrHdfsOverview" prefix.
> 2. To query the metrics of HDFS-OverviewAggregation, add the "EmrHdfsOverviewAggregation" prefix.

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------- | ---------------------------------------- | ---- | --------------------------------------------- | -------------------------------------- |
| HdfsNnBlockCapacityTotal | Cluster storage capacity_CapacityTotal | GB | Total storage capacity of the cluster | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockCapacityUsed | Cluster storage capacity_CapacityUsed | GB | Capacity used by the cluster | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockCapacityRemaining | Cluster storage capacity_CapacityRemaining | GB | Free storage capacity of the cluster | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockCapacity<br>UsedNonDFS | Cluster storage capacity_CapacityUsedNonDFS | GB | Capacity of the cluster used by others (not HDFS) | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockTotalLoad | Cluster load_TotalLoad | Count | Number of current connections | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockFilesTotal | Total files of the cluster_FilesTotal | Count | Total number of cluster files | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockBlockstotal | Number of blocks_BlocksTotal | Count | Total number of blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockPending<br>ReplicationBlocks | Number of blocks_PendingReplicationBlocks | Count | Number of blocks to be backed up | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockUnder<br>ReplicatedBlocks | Number of blocks_UnderReplicatedBlocks | Count | Number of blocks with insufficient copies | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockBlocksCorruptblocks | Number of blocks_CorruptBlocks | Count | Number of bad blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockScheduled<br>ReplicationBlocks | Number of blocks_ScheduledReplicationBlocks | Count | Number of blocks to be backed up as scheduled | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockPending<br>DeletionBlocks | Number of blocks_PendingDeletionBlocks | Count | Number of blocks to be deleted | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockCorruptblocks | Number of blocks_CorruptBlocks | Count | Number of redundant blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockPostponed<br>MisreplicatedBlocks | Number of blocks_PostponedMisreplicatedBlocks | Count | Number of exceptional blocks whose processing is delayed | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockBlockCapacity | Block capacity_BlockCapacity | Count | Block capacity | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockNumLiveDataNodes | Cluster data node_NumLiveDataNodes | Count | Number of living data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockNumDeadDataNodes | Cluster data node_NumDeadDataNodes | Count | Number of data nodes that are marked as dead | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockNum<br>DecomLiveDataNodes | Cluster data node_NumDecomLiveDataNodes | Count | Number of offline living nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockNum<br>DecomDeadDataNodes | Cluster data node_NumDecomDeadDataNodes | Count | Number of offline dead nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockNum<br>DecommissioningDataNodes | Cluster data node_NumDecommissioningDataNodes | Count | Number of nodes going offline | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockNum<br>StaleDataNodes | Cluster data node_NumStaleDataNodes | Count | Number of current data nodes that are marked as expired due to heartbeat latency | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockSnapshots | Snapshot related_Snapshots | Count | Number of snapshots | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockVolumeFailuresTotal | Disk failure_VolumeFailuresTotal | Count | Total number of failures of all data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |

### HDFS-NameNode

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ---------------------------------------------------- | -------------------------------------- |
| HdfsNnPort4007RxtxReceivedbytes | Data traffic_ReceivedBytes | Bytes/sec | Data receiving rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007RxtxSentbytes | Data traffic_SentBytes | Bytes/sec | Data transmission rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007Qps<br>Rpcqueuetimenumops | QPS_RpcQueueTimeNumOps | Times/sec | RPC call rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007RtRpc<br>queuetimeavgtime | Request processing latency<br>_RpcQueueTimeAvgTime | ms | Average RPC latency | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007AuthRpc<br>authenticationfailures | Authentication and authorization<br>_RpcAuthenticationFailure | Times | Number of RPC authentication failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007AuthRpc<br>authenticationsuccesses | Authentication and authorization<br>_RpcAuthenticationSuccesses | Times | Number of successful RPC authentication operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007AuthRpc<br>authorizationfailures | Authentication and authorization<br>_RpcAuthorizationFailures | Times | Number of RPC authorization failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007AuthRpc<br>authorizationsuccesses | Authentication and authorization<br>_RpcAuthorizationSuccesses | Times | Number of successful RPC authorization operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007Connections<br>Numopenconnections | Number of current connections<br>_NumOpenConnections | Count | Number of current connections | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPort4007Queue<br>LenCallqueuelength | Length of the RPC processing queue<br>_CallQueueLength | Count | Length of the current RPC processing queue | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmMemMemnonheapusedm | JVM memory<br>_MemNonHeapUsedM | MB | Size of the NonHeapMemory currently used by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmMemMemnon<br>heapcommittedm | JVM memory<br>_MemNonHeapCommittedM | MB | Size of the JVM memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmMemMemheapusedm | Memory of JVM<br>_MemHeapUsedM | MB | Size of the HeapMemory currently used by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmMem<br>Memheapcommittedm | Memory of JVM<br>_MemHeapCommittedM | MB | Size of the HeapMemory committed by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmMemMemheapmaxm | Memory of JVM_MemHeapMaxM | MB | Size of the HeapMemory configured for JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmMemMemmaxm | Memory of JVM_MemMaxM | MB | Maximum memory size that can be used by JVM during runtime | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockReportRt<br>Blockreportavgtime | Data block reporting latency <br>_BlockReportAvgTime | Times/sec | Average latency of DataNode Block processing per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilGcCountFgc | Number of GC times_FGC | Times/sec | Number of full GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilGcCountYgc | Number of C times_YGC | Twice/sec | Number of Young GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilGcTimeYgct | GC time_YGCT | ms | Time consumed by Young GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilGcTimeFgct | GC time_FGCT | ms | Time consumed by full GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilGcTimeGct | GC time_GCT | ms | Time used to collect garbage | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmJavaThreadsThreadsnew | Number of JVM threads<br>_ThreadsNew | Count | Number of new threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmJavaThreads<br>Threadsrunnable | Number of JVM threads<br>_ThreadsRunnable | Count | Number of runnable threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmJavaThreads<br>Threadsblocked | Number of JVM threads<br>_ThreadsBlocked | Count | Number of blocked threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmJavaThreads<br>Threadswaiting | Number of JVM threads<br>_ThreadsWaiting | Count | Number of waiting threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmJavaThreads<br>Threadstimedwaiting | Number of JVM threads<br>_ThreadsTimedWaiting | Count | Number of threads in the TIMED WAITING state | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmJavaThreads<br>Threadsterminated | Number of JVM threads<br>_ThreadsTerminated | Count | Number of terminated threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmLogTotalLogfatal | Number of JVM logs_LogFatal | Count | Number of Fatal logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmLogTotalLogerror | Number of JVM logs_LogError | Count | Number of Error logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmLogTotalLogwarn | Number of JVM logs_LogWarn | Count | Number of Warn logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnJvmLogTotalLoginfo | Number of JVM logs_LogInfo | Count | Number of Info logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilMemoryS0 | Memory area ratio_S0 | % | Memory usage ratio of the Survivor 0 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilMemoryS1 | Memory area ratio_S1 | % | Memory usage ratio of the Survivor 1 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilMemoryE | Memory usage ratio_E | % | Memory usage ratio of the Eden area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilMemoryO | Memory usage ratio_O | % | Memory usage ratio of the Old area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilMemoryM | Memory usage ratio_M | % | Memory usage ratio of the Metaspace area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnGcUtilMemoryCcs | Memory usage ratio_CCS | % | Memory usage ratio of the Compressed class space area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnStaleStorages<br>CountNumstalestorages | Number of storages that are marked as expired<br>_NumStaleStorages | Count | Number of current data nodes that are marked as expired due to heartbeat latency | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnPendingDatanodeMessage<br>CountPendingdatanode<br/>messagecount | Number of messages related to the block operation suspended on the standby NN<br>_PendingDataNode<br/>MessageCount | Requests/sec | Number of data node requests queued in the standby namenode | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlocksMissingNum<br>berofmissingblocks | Number of missing blocks<br>_NumberOfMissingBlocks | Count | Number of missing data blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlocksMissingNumberof<br>missingblockswithreplication<br/>factorOne | Number of missing blocks_NumberOf<br>MissingBlocksWithReplication<br/>FactorOne | Count | Number of missing databases (rf = 1) | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOpsAllowsnapshotops | Snapshot operations<br>_AllowSnapshotOps | Times/sec | Number of AllowSnapshot operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOps<br>Disallowsnapshotops | Snapshot operations<br>_DisallowSnapshotOps | Times/sec | Number of DisallowSnapshot operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOps<br>Createsnapshotops | Snapshot operations<br>_CreateSnapshotOps | Times/sec | Number of CreateSnapshot operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOps<br>Deletesnapshotops | Snapshot operations<br>_DeleteSnapshotOps | Times/sec | Number of DeleteSnapshot operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOps<br>Listsnapshottabledirops | Snapshot operations_ListSnapshottableDirOps | Times/sec | Number of ListSnapshottableDir operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOps<br>Snapshotdiffreportops | Snapshot operations_SnapshotDiffReportOps | Times/sec | Number of SnapshotDiffReportOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSnapshotOps<br>Renamesnapshotops | Snapshot operations<br>_RenameSnapshotOps | Times/sec | Number of RenameSnapshotOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsCreatefileops | File operations_CreateFileOps | Times/sec | Number of CreateFile operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsGetlistingops | File operations_GetListingOps | Times/sec | Number of GetListing operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsTotalfileops | File operations_TotalFileOps | Times/sec | Number of TotalFileOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsDeletefileops | File operations_DeleteFileOps | Times/sec | Number of DeleteFile operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsFileinfoops | File operations_FileInfoOps | Times/sec | Number of FileInfo operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsGetadditional<br>datanodeops | File operations<br>_GetAdditionalDatanodeOps | Times/sec | Number of GetAdditionalDatanode operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsCreatesymlinkops | File operations_CreateSymlinkOps | Times/sec | Number of CreateSymlink operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsGetlinktargetops | File operations_GetLinkTargetOps | Times/sec | Number of GetLinkTarget operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnFilesOpsFilesingetlistingops | File operations<br>_FilesInGetListingOps | Times/sec | Number of FilesInGetListing operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnTransactionOps<br>Transactionsnumops | Transaction operations<br>_TransactionsNumOps | Times/sec | Number of Journal transaction operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnTransactionOps<br>Transactionsbatchedinsync | Transaction operations<br>_TransactionsBatchedInSync | Times/sec | Number of batch Journal transaction operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnImageOpsGeteditnumops | Image operations_GetEditNumOps | Times/sec | Number of GetEditNumOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnImageOpsGetimagenumops | Image operations_GetImageNumOps | Times/sec | Number of GetImageNumOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnImageOpsPutimagenumops | Image operations_PutImageNumOps | Times/sec | Number of PutImageNumOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSyncsOpsSyncsnumops | SYNC operations_SyncsNumOps | Times/sec | Number of Journal syncs operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlocksOpsBlock<br>receivedanddeletedops | Data block operations<br/>_BlockOpsQueued | Times/sec | Number of BlockReceivedAndDeletedOps operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlocksOpsBlockopsqueued | Data block operations<br/>_BlockOpsQueued | Times/sec | Latency of the DataNode Block reporting operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnCacheReportOps<br>Cachereportnumops | Cache reporting<br/>_CacheReportNumOps | Times/sec | Number of CacheReport operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnBlockReportOps<br>Blockreportnumops | Data block reporting<br/>_BlockReportNumOps | Times/sec | Number of DataNode Block reporting operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnSyncsRtSyncsavgtime | SYNCS operation latency_SyncsAvgTime | ms | Average latency of Journal syncs operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnCacheReportRt<br>Cachereportavgtime | Cache reporting latency_CacheReportAvgTime | ms | Average latency of cache reporting operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnImageRtGeteditavgtime | Latency of image operations<br/>_GetEditAvgTime | ms | Average latency of Edit file reads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnImageRtGetimageavgtime | Latency of image operations<br/>_GetImageAvgTime | ms | Average latency of reading image files | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnImageRtPutimageavgtime | Latency of image operations<br/>_PutImageAvgTime | ms | Average latency of writing image files | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnTransactionRt<br>Transactionsavgtime | Latency of transaction operations<br/>_TransactionsAvgTime | ms | Average latency of Journal transaction operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnStartTimeStarttime | Start time_StartTime | ms | Process launch time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnStateState | Master/slave state_State | - | NN state | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnThreadCountPeakthreadcount | Number of threads_PeakThreadCount | Count | Number of peak threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnThreadCountThreadcount | Number of threads_ThreadCount | Count | Number of threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsNnThreadCount<br>Daemonthreadcount | Number of threads_DaemonThreadCount | Count | Number of daemon threads | id4hdfsdatanode and <br>host4hdfsdatanode |

### HDFS-DataNode

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ------------------------------------------ | -------------------------------------- |
| HdfsDnXceiverXceivercount | Number of Xceivers_XceiverCount | Count | Number of Xceivers | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBytesByteswrittenmb | Data read/write rate_BytesReadMB | Bytes/sec | Rate of writing bytes to data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBytesBytesreadmb | Data read/write rate_BytesReadMB | Bytes/sec | Rate of reading bytes from data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBytesRemotebytesreadmb | Data read/write rate<br/>_RemoteBytesReadMB | Bytes/sec | Rate of reading bytes via the remote client | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBytesRemoteby<br>teswrittenmb | Data read/write rate<br/>_RemoteBytesWrittenMB | Bytes/sec | Rate of writing bytes via the remote client | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnClientWritesfrom<br>remoteclient | Number of client connections<br/>_WritesFromRemoteClient | Count | QPS of the writes from the remote client | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnClientWritesfromlocalclient | Number of client connections<br/>_WritesFromLocalClient | Count | QPS of the writes from the local client | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnClientReadsfrom<br>remoteclient | Number of client connections<br/>_ReadsFromRemoteClient | Count | QPS of the reads from the remote client | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnClientReadsfromlocalclient | Number of client connections<br/>_ReadsFromLocalClient | Count | QPS of the reads from the local client | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksVerifiedFailures<br>Blockverificationfailures | Block check failures<br/>_BlockVerificationFailures | Times/sec | Number of block check failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnVolumeFailures<br>Volumefailures | Disk failures_VolumeFailures | Times/sec | Number of disk failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnNetworkErrors<br>Datanodenetworkerrors | Network errors<br/>_DatanodeNetworkErrors | Times/sec | Number of network errors | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnHbRtHeartbeatsavgtime | Heartbeat latency_HeartbeatsAvgTime | ms | Average processing time of the heartbeat interface | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnHbOpsHeartbeatsnumops | Heartbeat QPS_HeartbeatsNumOps | Times/sec | QPS of the heartbeat interface | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnDatapacketAvgtimeSend<br>datapackettransfer<br/>nanosavgtime | Packet transmission operation<br/> QPS_SendDataPacketTransfer<br/>NanosAvgTime | ms | Average time of packet transmissions | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsRead<br>blockopnumops | Data block operations<br/>_ReadBlockOpNumOps | Times/sec | OPS of reading blocks from data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsWrite<br>blockopnumops | Data block operations<br/>_WriteBlockOpNumOps | Times/sec | OPS of writing blocks to data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsBlock<br>checksumopnumops | Data block operations<br/>_BlockChecksumOpNumOps | Times/sec | OPS of checksum operations performed by data nodes | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsCopy<br>blockopnumops | Data block operations<br/>_CopyBlockOpNumOps | Times/sec | OPS of copying blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsReplace<br>blockopnumops | Data block operations<br/>_ReplaceBlockOpNumOps | Times/sec | OPS of replacing blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsBlock<br>reportsnumops | Data block operations<br/>_BlockReportsNumOps | Times/sec | OPS of reporting blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsIncremental<br>blockreports<br/>numops | Data block operations<br/>_IncrementalBlockReports<br/>NumOps | Times/sec | OPS of reporting incremental blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksOpsCache<br>reportsnumops | Data block operations<br/>_CacheReportsNumOps | Times/sec | OPS of processing blocks reported by the cache | id4hdfsdatanode and <br>host4hdfsdatanode |
| HfsDnBlocksOpsPacketack<br>roundtriptimenanos<br/>numops | Data block operations<br/>_PacketAckRoundTripTimeNanos<br/>NumOps | Times/sec | Number of ACK ROUND TRIP operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnFsyncOpsFsync<br>nanosnumops | FSYNC operations<br/>_FsyncNanosNumOps | Times/sec | Number of FSYNC operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnFlushOpsFlush<br>nanosnumops | Flush operations<br/>_FlushNanosNumOps | Times/sec | Number of flush operations per second | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtRead<br>blockopavgtime | Latency of the data block operation<br/>_ReadBlockOpAvgTime | ms | Average time of reading blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtWrite<br>blockopavgtime | Latency of the data block operation<br/>_ReplaceBlockOpAvgTime | ms | Average time of writing blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtBlock<br>checksumopavgtime | Latency of the data block operation<br/>_BlockChecksumOpAvgTime | ms | Average time of checking blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtCopy<br>blockopavgtime | Latency of the data block operation<br/>_CopyBlockOpAvgTime | ms | Average time of copying blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRt<br>Replaceblockopavgtime | Latency of the data block operation<br/>_Replaceblockopavgtime | ms | Average time of replacing blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtBlock<br>reportsavgtime | Latency of the data block operation<br/>_BlockReportsAvgTime | ms | Average time of reporting blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtIncremental<br>blockreportsavgtime | Latency of the data block operation<br/>_IncrementalBlockReportsAvgTime | ms | Average time of reporting incremental blocks | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtCache<br>reportsavgtime | Latency of the data block operation<br/>_CacheReportsAvgTime | ms | Average time of processing blocks reported by the cache | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnBlocksRtPacketack<br>roundtriptimenanos<br/>avgtime | Latency of the data block operation<br/>_PacketAckRoundTripTimeNanos<br/>AvgTime | ms | Average time of performing ACK ROUND TRIP operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnFlushRtFlushnanosavgtime | Flush latency_FlushNanosAvgTime | ms | Average time of flush operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnFsyncRtFsyncnanosavgtime | FSYNC latency_FsyncNanosAvgTime | ms | Average time of Fsync operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblockswrite | RAMDISKBlocks_Ram<br/>DiskBlocksWrite | Blocks/sec | Total number of blocks written to the memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblockswritefallback | RAMDISKBlocks_Ram<br/>DiskBlocksWriteFallback | Blocks/sec | Total number of blocks failed to be written to the memory (that is, failed over to the disk) | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOpRamdisk<br>blocksdeletedbeforelazypersisted | RAMDISKBlocks_RamDiskBlocks<br>DeletedBeforeLazyPersisted | Blocks/sec | Total number of blocks deleted before the application was saved to a disk | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblocksreadhits | RAMDISKBlocks_Ram<br/>DiskBlocksReadHits | Blocks/sec | Total number of read blocks in the memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblocksevicted | RAMDISKBlocks_Ram<br/>DiskBlocksEvicted | Blocks/sec | Total number of blocks cleared from the memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOpRamdisk<br>blocksevictedwithoutread | RAMDISKBlocks_RamDiskBlocks<br>EvictedWithoutRead | Blocks/sec | Total number of blocks read from the memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskblockslazypersisted | RAMDISKBlocks_RamDisk<br>BlocksLazyPersisted | Blocks/sec | Total number of blocks written by the lazy writer to a disk | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksOp<br>Ramdiskbyteslazypersisted | RAMDISKBlocks_Ram<br/>DiskBytesLazyPersisted | Bytes/sec | Total number of bytes written by the lazy writer to a disk | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRamBlocksBytes<br>Ramdiskbyteswrite | RAMDISK write speed_RamDiskBytesWrite | Bytes/sec | Total number of bytes written to the memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmMem<br>Memnonheapusedm | Memory of JVM<br/>_MemNonHeapUsedM | MB | Size of the NonHeapMemory already used by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmMem<br>Memnonheapcommittedm | Memory of JVM<br/>_MemNonHeapCommittedM | MB | Size of the NonHeapCommittedM configured by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmMemMemheapusedm | Memory of JVM<br/>_MemHeapUsedM | MB | Size of the HeapMemory already used by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmMem<br>Memheapcommittedm | Memory of JVM<br/>_MemHeapCommittedM | MB | Size of the HeapMemory committed by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmMemMemheapmaxm | Memory of JVM<br/>_MemHeapMaxM | MB | Size of the HeapMemory configured by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmMemMemmaxm | Memory of JVM<br/>_MemMaxM | MB | Maximum memory size that can be used by JVM during runtime | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreadsThreadsnew | Number of JVM threads<br/>_ThreadsNew | Count | Number of new threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadsrunnable | Number of JVM threads<br/>_ThreadsRunnable | Count | Number of runnable threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadsblocked | Number of JVM threads<br/>_ThreadsBlocked | Count | Number of blocked threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadswaiting | Number of JVM threads<br/>_ThreadsWaiting | Count | Number of waiting threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadstimedwaiting | Number of JVM threads<br/>_ThreadsTimedWaiting | Count | Number of threads that are in the TIMES WAITING state | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmJavaThreads<br>Threadsterminated | Number of JVM threads<br/>_ThreadsTerminated | Count | Number of terminated threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLogfatal | Number of JVM logs_LogFatal | Count | Number of Fatal logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLogerror | Number of JVM logs_LogError | Count | Number of Error logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLogwarn | Number of JVM logs_LogWarn | Count | Number of Warn logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnJvmLogTotalLoginfo | Number of JVM logs_LogInfo | Count | Number of Info logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryS0 | Ratio of the memory area_S0 | % | Ratio of the memory usage of the Survivor 0 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryS1 | Ratio of the memory area_S1 | % | Ratio of the memory usage of the Survivor 1 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryE | Ratio of the memory area_E | % | Ratio of the memory usage of the Eden area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryO | Ratio of the memory area_O | % | Ratio of the memory usage of the Old area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryM | Ratio of the memory area_M | % | Ratio of the memory usage of the Metaspace area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilMemoryCcs | Ratio of the memory area_CCS | % | Ratio of the memory usage of the Compressed class space area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilGcCountFgc | Number of GC times_FGC | Times | Number of full GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilGcCountYgc | Number of GC times_YGC | Times | Number of Young GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilGcTimeYgct | GC time_YGCT | Seconds | Time consumed by Young GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilGcTimeFgct | GC time_FGCT | Seconds | Time consumed by Full GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnGcUtilGcTimeGct | GC time_GCT | Seconds | Time used to collect garbage | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004RxtxReceivedbytes | Data traffic_ReceivedBytes | Bytes/sec | Data receiving rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004RxtxSentbytes | Data traffic_SentBytes | Bytes/sec | Data transmission rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004QpsRpc<br>queuetimenumops | QPS_RpcQueueTimeNumOps | Times/sec | RPC call rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004RtRpc<br>queuetimeavgtime | Request processing latency<br/>_RpcQueueTimeAvgTime | ms | Average RPC latency | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authenticationfailures | Authentication and authorization<br/>_RpcAuthenticationFailures | Times/sec | Number of RPC authentication failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authenticationsuccesses | Authentication and authorization<br/>_RpcAuthenticationSuccesses | Times/sec | Number of successful RPC authentication operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authorizationfailures | Authentication and authorization<br/>_RpcAuthorizationFailures | Times/sec | Number of RPC authorization failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004AuthRpc<br>authorizationsuccesses | Authentication and authorization<br/>_RpcAuthorizationSuccesses | Times/sec | Number of successful RPC authorization operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004Connections<br>Numopenconnections | Number of current connections<br/>_NumOpenConnections | Count | Number of current connections | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnPort4004QueueLen<br>Callqueuelength | Length of the RPC processing queue<br/>_CallQueueLength | Count | Length of the current RPC processing queue | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnThreadTimeCurrent<br>threadcputime | CPU time<br/>_CurrentThreadCpuTime | ms | CPU time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnThreadTimeCurrent<br>threadusertime | CPU time<br/>_CurrentThreadUserTime | ms | User time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnStartTimeStarttime | Number of threads<br/>_DaemonThreadCount | Seconds | Thread launch time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnThreadCount<br>Peakthreadcount | Number of threads_PeakThreadCount | Count | Number of peak threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnThreadCount<br>Daemonthreadcount | Number of threads_DaemonThreadCount | Count | Number of daemon threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRtWrit | Read/Write latency_Write | MB/s | Disk write rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnRtRead | Read/Write latency_Read | Times/sec | QPS of reads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDnDatapacketOps<br>Datapacketops | QPS of the packet transmission operations_DataPacketOps | Times/sec | QPS of the packet transmission operations | id4hdfsdatanode and <br>host4hdfsdatanode |

### HDFS-Journal Node 

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------------------ | ------------------------------------- | -------- | --------------------------------------- | -------------------------------------- |
| HdfsJnJvmMemMemnon<br>heapusedm | Memory of JVM_MemNonHeapUsedM | MB | Size of the NonHeapMemory already used by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmMemMemnon<br>heapcommittedm | Memory of JVM_MemNonHeapCommittedM | MB | Size of the JVM memory | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmMemMem<br>heapusedm | Memory of JVM_MemHeapUsedM | MB | Size of the HeapMemory already used by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmMemMem<br>heapcommittedm | Memory of JVM_MemHeapCommittedM | MB | Size of the HeapMemory committed by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmMemMem<br>heapmaxm | Memory of JVM_MemHeapMaxM | MB | Size of the HeapMemory configured by JVM | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmMemMemmaxm | Memory of JVM_MemMaxM | MB | Maximum memory size that can be used by JVM during runtime | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmJavaThreads<br>Threadsnew | Number of JVM threads_ThreadsNew | Count | Number of new threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmJavaThreads<br>Threadsrunnable | Number of JVM threads_ThreadsRunnable | Count | Number of runnable threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmJavaThreads<br>Threadsblocked | Number of JVM threads_ThreadsBlocked | Count | Number of blocked threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmJavaThreads<br>Threadswaiting | Number of JVM threads_ThreadsWaiting | Count | Number of waiting threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmJavaThreads<br>Threadstimedwaiting | Number of JVM threads_ThreadsTimedWaiting | Count | Number of threads that are in the TIMES WAITING state | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmJavaThreads<br>Threadsterminated | Number of JVM threads_ThreadsTerminated | Count | Number of terminated threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmLogTotalLogfatal | Number of JVM logs_LogFatal | Count | Number of Fatal logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmLogTotalLogerror | Number of JVM logs_LogError | Count | Number of Error logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmLogTotalLogwarn | Number of JVM logs_LogWarn | Count | Number of Warn logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnJvmLogTotalLoginfo | Number of JVM logs_LogInfo | Count | Number of Info logs | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilMemoryS0 | Ratio of the memory area_S0 | % | Ratio of the memory usage of the Survivor 0 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilMemoryS1 | Ratio of the memory area_S1 | % | Ratio of the memory usage of the Survivor 1 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilMemoryE | Ratio of the memory area_E | % | Ratio of the memory usage of the Eden area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilMemoryO | Ratio of the memory area_O | % | Ratio of the memory usage of the Old area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilMemoryM | Ratio of the memory area_M | % | Ratio of the memory usage of the Metaspace area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilMemoryCcs | Ratio of the memory area_CCS | % | Ratio of the memory usage of the Compressed class space area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilGcCountFgc | Number of GC times_FGC | Times | Number of full GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilGcCountYgc | Number of GC times_YGC | Times | Number of Young GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilGcTimeYgct | GC time_YGCT | Seconds | Time consumed by Young GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilGcTimeFgct | GC time_FGCT | Seconds | Time consumed by Full GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnGcUtilGcTimeGct | GC time_GC | Seconds | Time used to collect garbage | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005Rxtx<br>Receivedbytes | Data traffic_ReceivedBytes | Bytes/sec | Data receiving rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005Rxtx<br>Sentbytes | Data traffic_SentBytes | Bytes/sec | Data transmission rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005QpsRpc<br>queuetimenumops | QPS_RpcQueueTimeNumOps | Times/sec | RPC call rate | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005RtRpc<br>queuetimeavgtime | Request processing latency_RpcQueueTimeAvgTime | ms | Average RPC latency | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005AuthRpc<br>authenticationfailures | Authentication and authorization_RpcAuthenticationFailures | Times/sec | Number of RPC authentication failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005AuthRpc<br>authorizationsuccesses | Authentication and authorization_RpcAuthorizationSuccesses | Times/sec | Number of successful RPC authorization operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005AuthRpc<br>authenticationsuccesses | Authentication and authorization_RpcAuthenticationSuccesses | Times/sec | Number of successful RPC authentication operations | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005AuthRpc<br>authorizationfailures | Authentication and authorization_RpcAuthorizationFailures | Times/sec | Number of RPC authorization failures | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005Connections<br>Numopenconnections | Number of current connections_NumOpenConnections | Count | Number of current connections | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnPort4005QueueLen<br>Callqueuelength | Length of the RPC processing queue_CallQueueLength | Count | Length of the current RPC processing queue | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnThreadTimeCurrent<br>threadcputime | CPU time_CurrentThreadCpuTime | ms | CPU time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnThreadTimeCurrent<br>threadusertime | CPU time_CurrentThreadUserTime | ms | User time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnStartTimeStarttime | Start time_StartTime | Seconds | Process launch time | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnThreadCount<br>Threadcount | Number of threads_ThreadCount | Count | Number of threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnThreadCount<br>Peakthreadcount | Number of threads_PeakThreadCount | Count | Number of peak threads | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsJnThreadCountDaemon<br>threadcount | Number of threads_DaemonThreadCount | Count | Number of daemon threads | id4hdfsdatanode and <br>host4hdfsdatanode |

### HDFS-ZKFC

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------ | ---------------- | -------- | ------------------------------------- | -------------------------------------- |
| HdfsDfzkGcUtilMemoryS0 | Ratio of the memory area_S0 | % | Ratio of the memory usage of the Survivor 0 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilMemoryS1 | Ratio of the memory area_S1 | % | Ratio of the memory usage of the Survivor 1 area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilMemoryE | Ratio of the memory area_E | % | Ratio of the memory usage of the Eden area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilMemoryO | Ratio of the memory area_O | % | Ratio of the memory usage of the Old area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilMemoryM | Ratio of the memory area_M | % | Ratio of the memory usage of the Metaspace area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilMemoryCcs | Ratio of the memory area_CCS | % | Ratio of the memory usage of the Compressed class space area | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilGcCountFgc | Number of GC times_FGC | Times | Number of full GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilGcCountYgc | Number of GC times_YGC | Times | Number of Young GC times | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilGcTimeYgct | GC time_YGCT | Seconds | Time consumed by Young GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilGcTimeFgct | GC time_FGCT | Seconds | Time consumed by Full GC | id4hdfsdatanode and <br>host4hdfsdatanode |
| HdfsDfzkGcUtilGcTimeGct | GC time_GCT | Seconds | Time used to collect garbage | id4hdfsdatanode and <br>host4hdfsdatanode |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ----------------- | ---------------------------- | ------------------------------------------ |
| Instances.N.Dimensions.0.Name | id4hdfsdatanode | Dimension name of the EMR instance ID | Enter a string-type dimension name, such as id4hdfsdatanode |
| Instances.N.Dimensions.0.Value | id4hdfsdatanode | A specific EMR instance ID | Enter a specific EMR instance ID, such as emr-mm8bs222 |
| Instances.N.Dimensions.0.Name | host4hdfsdatanode | Dimension name of the node IP address in an EMR instance | Enter a string-type dimension name, such as host4hdfsdatanode |
| Instances.N.Dimensions.0.Value | host4hdfsdatanode | A specific IP address of a node in an EMR instance | Enter a specific node IP address, such as 1.1.1.1 |



## Input Parameters

To query the monitoring data of the elastic MapReduce (HDFS) service, use the following input parameters:
&Namespace=QCE/TXMR_HDFS 
&Instances.N.Dimensions.0.Name=id4hdfsdatanode
&Instances.N.Dimensions.0.Value=<ID of the EMR instance>
&Instances.N.Dimensions.1.Name=host4hdfsdatanode
&Instances.N.Dimensions.1.Value=<IP address of a specific node in an EMR instance> 
