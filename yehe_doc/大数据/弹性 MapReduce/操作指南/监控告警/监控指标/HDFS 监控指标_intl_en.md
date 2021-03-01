### HDFS - Overview 

| Metric Name | Unit | Description |
| ---------------------------- | -------- | --------------------------------------------- |
| CapacityTotal | GB | Total capacity of cluster storage |
| CapacityUsed | GB | Used capacity of cluster storage |
| CapacityRemaining | GB | Remaining capacity of cluster storage |
| CapacityUsedNonDFS | GB | Used capacity for non-HDFS purposes |
| TotalLoad | - | Current number of connections |
| FilesTotal | - | Total number of files |
| BlocksTotal | - | Total number of blocks |
| PendingReplicationBlocks | - | Number of blocks pending to be replicated  |
| UnderReplicatedBlocks | - | Number of under-replicated blocks |
| CorruptBlocks  | - |  Number of corrupted blocks |
| ScheduledReplicationBlocks | - |  Number of blocks scheduled for replication |
| PendingDeletionBlocks | - | Number of blocks pending to be deleted  |
| ExcessBlocks | - |Number of excess blocks |
| PostponedMisreplicatedBlocks | - | Number of blocks postponed to be processed |
| BlockCapacity | - | Capacity of blocks |
| NumLiveDataNodes  | - | Number of live data nodes |
| NumDeadDataNodes  | - | Number of dead data nodes |
| NumDecomLiveDataNodes | - | Number of decommissioned live nodes |
| NumDecomDeadDataNodes | - | Number of decommissioned dead nodes |
| NumDecommissioningDataNodes  | - | Number of nodes being decommissioned |
| NumStaleDataNodes | - | Current number of DataNodes marked as expired due to heartbeat delay |
| Snapshots | -  | Number of Snapshots |
| VolumeFailuresTotal | - | Total number of full failures on all DataNodes |

### HDFS - NameNode

| Metric Name | Unit | Description |
| --------------------------------------------- | -------- | ---------------------------------------------------- |
| ReceivedBytes | Bytes/s  | Data receiving rate |
| SentBytes | Bytes/s | Data sending rate |
| RpcQueueTimeNumOps  | Calls/s | RPC call rate |
| RpcQueueTimeAvgTime | ms | Average RPC delay |
| RpcAuthenticationFailures | - | Number of RPC authentication failures |
| RpcAuthenticationSuccesses | - | Number of RPC authentication successes |
| RpcAuthorizationFailures | - | Number of RPC authorization failures |
| RpcAuthorizationSuccesses | - | Number of RPC authorization successes |
| NumOpenConnections | - | Current number of connections |
| CallQueueLength | - | Current length of the RPC processing queue |
| MemNonHeapUsedM | MB | Size of used JVM NonHeapMemory |
| MemNonHeapCommittedM | MB | JVM memory |
| MemHeapUsedM | MB | Size of used JVM HeapMemory |
| MemHeapCommittedM | MB | Size of submitted JVM HeapMemory |
| MemHeapMaxM | MB | Size of configured JVM HeapMemory |
| MemMaxM | MB | Maximum size of available JVM memory during runtime |
| BlockReportAvgTime | s | Average delay for processing DataNode blocks per second |
| FGC | - | Number of full GCs |
| YGC | - | Number of young GCs |
| YGCT | ms | Time taken by young GCs |
| FGCT | ms | Time taken by full GCs |
| GCT | ms | Time taken by GCs |
| ThreadsNew | - | Number of new threads |
| ThreadsRunnable | - | Number of runnable threads |
| ThreadsBlocked | - | Number of blocked threads |
| ThreadsWaiting  | - | Number of waiting threads |
| ThreadsTimedWaiting | - | Number of timed waiting threads |
| ThreadsTerminated | - | Number of terminated threads |
| LogFatal | - | Number of fatal logs |
| LogError | - | Number of error logs |
| LogWarn | - | Number of warn logs |
| LogInfo | - | Number of info logs |
| S0 | % | Memory utilization of survivor space 0 |
| S1 | % | Memory utilization of survivor space 1 |
| E | % | Memory utilization of eden space |
| O | % | Memory utilization of old space |
| M | % | Memory utilization of metaspace space |
| CCS | % | Memory utilization of compressed class space |
| NumStaleStorages | - | Number of DataNodes marked as expired due to heartbeat delay |
| PendingDataNodeMessageCount | - | Number of DataNode requests queued on standby NameNode |
| NumberOfMissingBlocks | - | Number of missing blocks |
| NumberOfMissingBlocksWithReplicationFactorOne | - | Number of missing blocks (rf = 1) |
| AllowSnapshotOps | - | Number of AllowSnapshot operations executed per second |
| DisallowSnapshotOps | - | Number of DisallowSnapshot operations executed per second |
| CreateSnapshotOps | - | Number of CreateSnapshot operations executed per second |
| DeleteSnapshotOps | - | Number of DeleteSnapshot operations executed per second |
| ListSnapshottableDirOps | - | Number of ListSnapshottableDir operations executed per second |
| SnapshotDiffReportOps | - | Number of SnapshotDiffReport operations executed per second |
| RenameSnapshotOps | - | Number of RenameSnapshot operations executed per second |
| CreateFileOps | - | Number of CreateFile operations executed per second |
| GetListingOps | - | Number of GetListing operations executed per second |
| TotalFileOps | -  | Number of TotalFile operations executed per second |
| DeleteFileOps | - | Number of DeleteFile operations executed per second |
| FileInfoOps | - | Number of FileInfo operations executed per second |
| GetAdditionalDatanodeOps | - | Number of GetAdditionalDatanode operations executed per second |
| CreateSymlinkOps | - | Number of CreateSymlink operations executed per second |
| GetLinkTargetOps | - | Number of GetLinkTarget operations executed per second |
| FilesInGetListingOps  | - | Number of FilesInGetListing operations executed per second |
| TransactionsNumOps | - | Number of Journal transaction operations processed per second |
| TransactionsBatchedInSync  | - | Number of Journal transaction operations processed in batches per second |
| GetEditNumOps | - | Number of GetEditNum operations executed per second |
| GetImageNumOps | - | Number of GetImageNum operations executed per second |
| PutImageNumOps | - | Number of PutImageNum operations executed per second |
| SyncsNumOps | - | Number of Journal syncs operations processed per second |
| BlockReceivedAndDeletedOps | - | Number of BlockReceivedAndDeleted operations executed per second |
| BlockOpsQueued | s | Delay in processing DataNode block reporting |
| CacheReportNumOps | - | Number of CacheReport operations processed per second |
| BlockReportNumQps  | - | Number of DataNode block reporting operations processed per second |
| SyncsAvgTime  | ms | Average delay in processing Journal syncs operations |
| CacheReportAvgTime  | ms | Average delay in cache reporting |
| GetEditAvgTime | ms | Average delay in reading Edit files |
| GetImageAvgTime | ms | Average delay reading image files |
| PutImageAvgTime | ms | Average delay in writing image files |
| TransactionsAvgTime | ms | Average delay in processing Journal transaction operations |
| StartTime | ms | Start time of the process |
| State | - | NN state |
| PeakThreadCount | - | Peak number of threads |
| ThreadCount  | - | Number of threads |
| DaemonThreadCount  | - | Number of daemon threads |
| RpcQueueTimeAvgTime | ms   | Average RPC delay  |
| RpcProcessingTimeAvgTime | ms | Average time of processing RPC requests |

### HDFS - DataNode

| Metric Name | Unit | Description |
| --------------------------------------- | -------- | ------------------------------------------ |
| XceiverCount | - | Number of Xceivers |
| BytesWrittenMB | Bytes/s  | Rate of writing into DN |
| BytesReadMB | Bytes/s  | Rate of reading from DN |
| RemoteBytesReadMB | Bytes/s  | Rate of reading of remote clients |
| RemoteBytesWrittenMB  | Bytes/s  | Rate of writing of remote clients |
| WritesFromRemoteClient | - | QPS of writes from remote clients |
| WritesFromLocalClient | - | QPS of writes from local clients |
| ReadsFromRemoteClient | - | QPS of reads from remote clients |
| ReadsFromLocalClient | - | QPS of reads from local clients |
| BlockVerificationFailures | - | Number of block verification failures |
| VolumeFailures | - | Number of disk failures |
| DatanodeNetworkErrors | - | Number of network errors |
| HeartbeatsAvgTime | ms | Average heartbeat API time |
| HeartbeatsNumOps | - | Heartbeat API QPS |
| SendDataPacketTransferNanosAvgTime | ms | Average time of sending data packets |
| ReadBlockOpNumOps | - | OPS of block reads from DataNode |
| WriteBlockOpNumOps | - | OPS of block writes to DataNode |
| BlockChecksumOpNumOps | - | OPS of Checksum operations by DataNode |
| CopyBlockOpNumOps | - | OPS of block copying operations |
| ReplaceBlockOpNumOps | - | OPS of Replace Block operations |
| BlockReportsNumOps | - | OPS of block reporting operations |
| IncrementalBlockReportsNumOps | - | OPS of incremental block reporting |
| CacheReportsNumOps | - | OPS of cache reporting |
| PacketAckRoundTripTimeNanosNumOps | - | Number of ACK round trip operations processed per second |
| FlushNanosNumOps | - | Number of Flush operations processed per second |
| ReadBlockOpAvgTime | ms | Average time of reading blocks |
| WriteBlockOpAvgTime | ms | Average time of writing blocks |
| BlockChecksumOpAvgTime | ms | Average time of checking blocks |
| CopyBlockOpAvgTime | ms | Average time of copying blocks |
| ReplaceBlockOpAvgTime | ms | Average time of replacing blocks |
| BlockReportsAvgTime | ms | Average time of reporting blocks |
| IncrementalBlockReportsAvgTime | ms | Average time of reporting incremental blocks |
| CacheReportsAvgTime | ms | Average time of reporting cache  |
| PacketAckRoundTripTimeNanosAvgTime | ms | Average time of processing ACK round trip operations  |
| FlushNanosAvgTime | ms | Average flush time  |
| FsyncNanosAvgTime | ms | Average fsync time |
| RamDiskBlocksWrite | - | Total number of blocks written to memory |
| RamDiskBlocksWriteFallback | - | Total number of blocks that fail to be written to memory (failover to disk) |
| RamDiskBlocksDeletedBeforeLazyPersisted | - | Total number of blocks deleted before application is saved to disk |
| RamDiskBlocksReadHits | - | Number of reads from blocks in memory |
| RamDiskBlocksEvicted | - | Total number of blocks deleted from memory |
| RamDiskBlocksEvictedWithoutRead | - | Total number of blocks retrieved from memory |
| RamDiskBlocksLazyPersisted | - | Total number of disk writes by lazy writer |
| RamDiskBytesLazyPersisted | Bytes  | Total number of bytes written into disks by lazy writers |
| RamDiskBytesWrite | Bytes  | Total number of bytes written into disks |
| MemNonHeapUsedM | MB | Size of used JVM NonHeapMemory |
| MemNonHeapCommittedM | MB | Size of configured JVM NonHeapCommittedM |
| MemHeapUsedM | MB | Size of used JVM HeapMemory |
| MemHeapCommittedM | MB | Size of submitted JVM HeapMemory |
| MemHeapMaxM | MB | Size of configured JVM HeapMemory |
| MemMaxM | MB | Maximum size of available JVM memory during runtime |
| ThreadsNew | - | Number of new threads |
| ThreadsRunnable | - | Number of runnable threads |
| ThreadsBlocked | - | Number of blocked threads |
| ThreadsWaiting | - | Number of waiting threads |
| ThreadsTimedWaiting | - | Number of timed waiting threads |
| ThreadsTerminated | - | Number of terminated threads |
| LogFatal | - | Number of fatal logs |
| LogError | - | Number of error logs |
| LogWarn | - | Number of warn logs |
| LogInfo | - | Number of info logs |
| S0 | % | Memory utilization of survivor space 0 |
| S1 | % | Memory utilization of survivor space 1 |
| E | % | Memory utilization of eden space |
| O | % | Memory utilization of old space |
| M | % | Memory utilization of metaspace space |
| CCS | % | Memory utilization of compressed class space |
| FGC | - | Number of full GCs |
| YGC | - | Number of young GCs |
| YGCT | s | Time taken by young GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |
| ReceivedBytes | Bytes/s  | Data receiving rate |
| SentBytes | Bytes/s  | Data sending rate |
| RpcQueueTimeNumOps | Calls/s | RPC call rate |
| RpcQueueTimeAvgTime | ms | Average RPC delay |
| RpcAuthenticationFailures | - | Number of RPC authentication failures |
| RpcAuthenticationSuccesses | - | Number of RPC authentication successes |
| RpcAuthorizationFailures | - | Number of RPC authorization failures |
| RpcAuthorizationSuccesses | - | Number of RPC authorization successes |
| NumOpenConnections | - | Current number of connections |
| CallQueueLength | - | Current length of the RPC processing queue |
| CurrentThreadSystemTime | ms | System time |
| CurrentThreadUserTime | ms | User time |
| StartTime | s | Start time of the process |
| PeckThreadCount | - | Peak number of threads |
| DaemonThreadCount | - | Number of daemon threads |
| write | MB/s | Disk write rate |
| read | - | Read QPS |
| FsyncNanosOps | Operations/s | Average number of Fsync operations|
| DataPacketOps   | - | Package transmission QPS |
| RpcQueueTimeAvgTime | ms | Average RPC delay |
| RpcProcessingTimeAvgTime | ms | Average time of processing RPC requests |

### HDFS - Journal Node 

| Metric Name  | Unit | Description |
| -------------------------- | -------- | --------------------------------------- |
| MemNonHeapUsedM | MB | Size of used JVM NonHeapMemory |
| MemNonHeapCommittedM | MB | JVM Memory |
| MemHeapUsedM | MB | Size of used JVM HeapMemory |
| MemHeapCommittedM | MB | Size of submitted JVM HeapMemory |
| MemHeapMaxM | MB | Size of configured JVM HeapMemory |
| MemMaxM | MB | Maximum size of available JVM memory during runtime |
| ThreadsNew  | - | Number of new threads |
| ThreadsRunnable | - | Number of runnable threads |
| ThreadsBlocked | - | Number of blocked threads |
| ThreadsWaiting | - | Number of waiting threads |
| ThreadsTimedWaiting | - | Number of timed waiting threads |
| ThreadsTerminated | - | Number of terminated threads |
| LogFatal | - | Number of fatal logs |
| LogError | - | Number of error logs |
| LogWarn | - | Number of warn logs |
| LogInfo | - | Number of info logs |
| S0 | % | Memory utilization of survivor space 0 |
| S1 | % | Memory utilization of survivor space 1 |
| E | % | Memory utilization of eden space |
| O | %  | Memory utilization of old space |
| M | % | Memory utilization of metaspace space |
| CCS  | % | Memory utilization of compressed class space |
| FGC | - | Number of full GCs |
| YGC | - | Number of young GCs |
| YGCT | s | Time taken by young GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |
| ReceivedBytes | Bytes/s  | Data receiving rate  |
| SentBytes | Bytes/s |  Data sending rate |
| RpcQueueTimeNumOps | Calls/s | RPC call rate |
| RpcQueueTimeAvgTime | ms | Average RPC delay |
| RpcAuthenticationFailures  | - | Number of RPC authentication failures |
| RpcAuthenticationSuccesses | - | Number of RPC authentication successes |
| RpcAuthorizationFailures | - | Number of RPC authorization failures |
| NumOpenConnections | - | Current number of connections |
| CallQueueLength | - | Current length of the RPC processing queue |
| CurrentThreadSystemTime    | ms       | system time |
| CurrentThreadUserTime      | ms       | User time |
| StartTime | s | Start time of the process |
| ThreadCount | - | Number of threads |
| PeckThreadCount | - | Peak number of threads |
| DaemonThreadCount | - | Number of daemon threads |

### HDFS - ZKFC

| Metric Name | Unit | Description |
| -------- | -------- | ------------------------------------- |
| S0 | % | Memory utilization of survivor space 0 |
| S1 | % | Memory utilization of survivor space 1 |
| E | % | Memory utilization of eden space |
| O | % | Memory utilization of old space |
| M | % | Memory utilization of metaspace space |
| CCS | % | Memory utilization of compressed class space |
| FGC | - | Number of full GCs |
| YGC | - | Number of young GCs |
| YGCT | s | Time taken by young GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |





