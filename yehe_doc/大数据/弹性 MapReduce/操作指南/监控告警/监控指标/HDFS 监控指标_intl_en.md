### HDFS - overview

| Metric Name | Unit | Description |
| ---------------------------- | -------- | --------------------------------------------- |
| CapacityTotal                | GB       | Total cluster storage capacity                                |
| CapacityUsed                 | GB       | Used cluster storage capacity                            |
| CapacityRemaining            | GB       | Remaining cluster storage capacity |
| CapacityUsedNonDFS           | GB       | Non-HDFS used cluster capacity                          |
| TotalLoad | - | Number of current connections |
| FilesTotal | - | Total number of files |
| BlocksTotal                  | -       | Total number of blocks                               |
| PendingReplicationBlocks     | -       | Number of blocks waiting to be backed up                            |
| UnderReplicatedBlocks        | -       | Number of blocks with insufficient replicas                            |
| CorruptBlocks | - | Number of corrupted blocks |
| ScheduledReplicationBlocks   | -       | Number of blocks arranged for backup                            |
| PendingDeletionBlocks        | -       | Number of blocks waiting to be deleted                            |
| ExcessBlocks                 | -       | Number of excessive blocks                                  |
| PostponedMisreplicatedBlocks | -       | Number of exceptional blocks postponed to be processed                        |
| BlockCapacity | - | Capacity of blocks |
| NumLiveDataNodes             | -       | Number of live data nodes                              |
| NumDeadDataNodes             | -       | Number of data nodes marked as dead            |
| NumDecomLiveDataNodes        | -       | Number of decommissioned live nodes                        |
| NumDecomDeadDataNodes        | -       | Number of decommissioned dead nodes                        |
| NumDecommissioningDataNodes  | -       | Number of decommissioning nodes |
| NumStaleDataNodes            | - | Number of current DataNodes marked as expired due to heartbeat delay |
| Snapshots                    | -       | Number of snapshots                                |
| VolumeFailuresTotal | - | Total number of failures on all DataNodes |

### HDFS - NameNode

| Metric Name | Unit | Description |
| --------------------------------------------- | -------- | ---------------------------------------------------- |
| ReceivedBytes                                 | Bytes/s  | Data receiving rate                                         |
| SentBytes                                     | Bytes/s  | Data sending rate                                         |
| RpcQueueTimeNumOps                            | Calls/s      | RPC call rate                                         |
| RpcQueueTimeAvgTime                           | ms       | Average RPC delay                                     |
| RpcAuthenticationFailures               | -     | Number of RPC authentication failures                                     |
| RpcAuthenticationSuccesses                    | -     | Number of RPC authentication successes                                     |
| RpcAuthorizationFailures                      | -     | Number of RPC authorization failures                                     |
| RpcAuthorizationSuccesses                     | -     | Number of RPC authorization successes                                     |
| NumOpenConnections                            | -     | Number of current connections                                         |
| CallQueueLength                               | -     | Length of current RPC processing queue                                |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently used by JVM |
| MemNonHeapCommittedM                          | MB       | JVM memory                                             |
| MemHeapUsedM | MB | Size of HeapMemory currently used by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum memory size that can be used by JVM during runtime| 
| BlockReportAvgTime                            | Blocks/s     | Average delay for processing DataNode blocks per second                     |
| FGC                                | Operations/s       | Full GC count            |
| YGC                                | 2/s      | Young GC count            |
| YGCT | ms | Young GC time |
| FGCT                                          | ms       | Full GC time                                     |
| GCT                                           | ms       | Garbage collection time                                     |
| ThreadsNew                                    | -       | Number of threads in new state                               |
| ThreadsRunnable                               | -       | Number of threads in runnable state                             |
| ThreadsBlocked                                | - | Number of threads in blocked state |
| ThreadsWaiting                     | -       | Number of threads in WAITING state     |
| ThreadsTimedWaiting                     | -       | Number of threads in TIMED WAITING state     |
| ThreadsTerminated                             | -       | Number of threads in Terminated state                       |
| LogFatal                                      | -       | Number of Fatal logs                                       |
| LogError                                      | -       | Number of Error logs                                       |
| LogWarn                                       | -       | Number of Warn logs                                       |
| LogInfo                                       | -       | Number of Info logs                                       |
| S0                                             | %        | Percentage of used Survivor 0 memory                                   |
| S1                                             | %        | Percentage of used Survivor 1 memory                                   |
| E                                             | %        | Percentage of used Eden memory                                   |
| O                                             | %        | Percentage of used Old memory                                   |
| M                                             | %        | Percentage of used Metaspace memory                                   |
| CCS                                           | %        | Percentage of memory used by compressed class space             |
| NumStaleStorages                              | - | Number of current DataNodes marked as expired due to heartbeat delay |
| PendingDataNodeMessageCount                   | Requests/s     | Number of DataNode requests queued on standby NameNode |
| NumberOfMissingBlocks                         | -       | Number of missing blocks                                     |
| NumberOfMissingBlocksWithReplicationFactorOne | -       | Number of missing blocks (rf = 1)                           |
| AllowSnapshotOps                      | Operations/s     | Number of AllowSnapshot operations executed per second            |
| DisallowSnapshotOps                           | Operations/s     | Number of DisallowSnapshot operations executed per second            |
| CreateSnapshotOps                             | Operations/s     | Number of CreateSnapshot operations executed per second            |
| DeleteSnapshotOps                             | Operations/s     | Number of DeleteSnapshot operations executed per second            |
| ListSnapshottableDirOps                       | Operations/s     | Number of ListSnapshottableDir operations executed per second            |
| SnapshotDiffReportOps                         | Operations/s     | Number of SnapshotDiffReportOps operations executed per second            |
| RenameSnapshotOps                             | Operations/s     | Number of RenameSnapshotOps operations executed per second            |
| CreateFileOps                      | Operations/s     | Number of CreateFile operations executed per second            |
| GetListingOps                                 | Operations/s     | Number of GetListing operations executed per second            |
| TotalFileOps                                  | Operations/s     | Number of TotalFileOps operations executed per second            |
| DeleteFileOps                                 | Operations/s     | Number of DeleteFile operations executed per second            |
| FileInfoOps                                   | Operations/s     | Number of FileInfo operations executed per second            |
| GetAdditionalDatanodeOps                      | Operations/s     | Number of GetAdditionalDatanode operations executed per second            |
| CreateSymlinkOps                              | Operations/s     | Number of CreateSymlink operations executed per second            |
| GetLinkTargetOps                              | Operations/s     | Number of GetLinkTarget operations executed per second            |
| FilesInGetListingOps                          | Operations/s     | Number of FilesInGetListing operations executed per second            |
| TransactionsNumOps                            | Operations/s     | Number of Journal transaction operations processed per second                      |
| TransactionsBatchedInSync                     | Operations/s     | Number of Journal transaction operations processed in batches per second                      |
| GetEditNumOps                      | Operations/s     | Number of GetEditNumOps operations executed per second            |
| GetImageNumOps                                | Operations/s     | Number of GetImageNumOps operations executed per second            |
| PutImageNumOps                                | Operations/s     | Number of PutImageNumOps operations executed per second            |
| SyncsNumOps                                   | Operations/s     | Number of Journal syncs operations processed per second                      |
| BlockReceivedAndDeletedOps                      | Operations/s     | Number of BlockReceivedAndDeletedOps operations executed per second            |
| BlockOpsQueued                                | Operations/s     | Delay in processing DataNode block reporting operations                   |
| CacheReportNumOps                             | Operations/s     | Number of CacheReport operations processed per second                      |
| BlockReportNumQps                             | Operations/s     | Number of DataNode block reporting operations processed per second               |
| SyncsAvgTime                                  | ms       | Average delay in processing Journal syncs operations                    |
| CacheReportAvgTime                            | ms       | Average time of cache reporting operation                                 |
| GetEditAvgTime                                | ms       | Average delay in reading Edit file |
| GetImageAvgTime                               | ms       | Average delay reading image file |
| PutImageAvgTime                               | ms       | Average delay in writing image file                                 |
| TransactionsAvgTime                           | ms       | Average delay in processing Journal transaction operations              |
| StartTime                     | ms        | Process start time   |
| State                                         | -        | NN state                                              |
| PeakThreadCount                               | -       | Peak number of threads        |
| ThreadCount                   | -       | Number of threads                             |
| DaemonThreadCount                             | -       | Number of background threads                                         |

### HDFS - DataNode

| Metric Name | Unit | Description |
| --------------------------------------- | -------- | ------------------------------------------ |
| XceiverCount | - | Number of Xceivers |
| BytesWrittenMB                          | Bytes/s  | DN byte write rate                         |
| BytesReadMB                             | Bytes/s  | DN byte read rate                         |
| RemoteBytesReadMB | Bytes/s | Rate of bytes read by remote client |
| RemoteBytesWrittenMB                    | Bytes/s | Rate of bytes written by remote client |
| WritesFromRemoteClient                  | -       | QPS of write operations from remote client                  |
| WritesFromLocalClient                   | -       | OPS of write operations from local client                  |
| ReadsFromRemoteClient                   | -       | QPS of read operations from remote client                  |
| ReadsFromLocalClient                    | -       | QPS of read operations from local client                  |
| BlockVerificationFailures               | Failures/s     | Number of block check failures                         |
| VolumeFailures                          | Failures/s     | Number of disk failures                                 |
| DatanodeNetworkErrors | Errors/s | Total number of network errors |
| HeartbeatsAvgTime                       | ms       | Average heartbeat API time                        |
| HeartbeatsNumOps                        | Queries/s     | Heartbeat API QPS                               |
| SendDataPacketTransferNanosAvgTime      | ms       | Average data packet sending time                         |
| ReadBlockOpNumOps                       | Operations/s     | OPS of block reads from DataNode                 |
| WriteBlockOpNumOps                      | Operations/s     | OPS of block writes to DataNode                 |
| BlockChecksumOpNumOps                   | Operations/s     | OPS of Checksum operations by DataNode          |
| CopyBlockOpNumOps                       | Operations/s     | OPS of block copying operations                      |
| ReplaceBlockOpNumOps                    | Operations/s     | OPS of Replace Block operations                      |
| BlockReportsNumOps                      | Operations/s     | OPS of block reporting operations                       |
| IncrementalBlockReportsNumOps                      | Reports/s     | OPS of incremental block reporting                             |
| CacheReportsNumOps                      | Reports/s     | OPS of cache reporting                             |
| PacketAckRoundTripTimeNanosNumOps       | Operations/s     | Number of ACK ROUND TRIP operations processed per second                      |
| FlushNanosNumOps                        | Operations/s     | Number of Flush operations processed per second                      |
| ReadBlockOpAvgTime                      | ms       | Average block read time                    |
| WriteBlockOpAvgTime                     | ms       | Average block write operation time                         |
| BlockChecksumOpAvgTime                  | ms       | Average block check time |
| CopyBlockOpAvgTime                      | ms       | Average block copy time                         |
| ReplaceBlockOpAvgTime                   | ms       | Average Replace Block operation time                         |
| BlockReportsAvgTime                     | ms       | Average block reporting time                             |
| IncrementalBlockReportsAvgTime          | ms       | Average time of incremental block reporting                         |
| CacheReportsAvgTime                     | ms       | Average time of cache reporting                           |
| PacketAckRoundTripTimeNanosAvgTime      | ms       | Average time of processing ACK ROUND TRIP               |
| FlushNanosAvgTime                       | ms       | Average Flush operation time                         |
| FsyncNanosAvgTime                       | ms       | Average Fsync operation time                         |
| RamDiskBlocksWrite                      | Blocks/s     | Total number of blocks written to memory                         |
| RamDiskBlocksWriteFallback              | Blocks/s     | Total number of blocks failed to be written to memory (failover to disk) |
| RamDiskBlocksDeletedBeforeLazyPersisted | Blocks/s     | Total number of blocks deleted before application is saved to disk |
| RamDiskBlocksReadHits                   | Blocks/s     | Number of reads from blocks in memory                   |
| RamDiskBlocksEvicted                    | Blocks/s     | Total number of blocks cleared in memory                       |
| RamDiskBlocksEvictedWithoutRead         | Blocks/s     | Total number of blocks retrieved from memory          |
| RamDiskBlocksLazyPersisted              | Blocks/s     | Number of disk writes by lazy writer                   |
| RamDiskBytesLazyPersisted  | Bytes/s  | Total number of blocks written by the lazy writer to a disk |
| RamDiskBytesWrite                       | Bytes/s  | Total number of bytes written to memory                        |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently used by JVM |
| MemNonHeapCommittedM                    | MB | Size of NonHeapCommittedM configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently used by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum memory size that can be used by JVM during runtime| 
| ThreadsNew                                    | -       | Number of threads in new state                               |
| ThreadsRunnable                               | -       | Number of threads in runnable state                             |
| ThreadsBlocked                                | - | Number of threads in blocked state |
| ThreadsWaiting                     | -       | Number of threads in WAITING state     |
| ThreadsTimedWaiting                     | -       | Number of threads in TIMED WAITING state     |
| ThreadsTerminated                             | -       | Number of threads in Terminated state                       |
| LogFatal                                      | -       | Number of Fatal logs                                       |
| LogError                                      | -       | Number of Error logs                                       |
| LogWarn                                       | -       | Number of Warn logs                                       |
| LogInfo                                       | -       | Number of Info logs                                       |
| S0                                             | %        | Percentage of used Survivor 0 memory                                   |
| S1                                             | %        | Percentage of used Survivor 1 memory                                   |
| E                                             | %        | Percentage of used Eden memory                                   |
| O                                             | %        | Percentage of used Old memory                                   |
| M                                             | %        | Percentage of used Metaspace memory                                   |
| CCS                                           | %        | Percentage of memory used by compressed class space             |
| FGC                                | -       | Full GC count            |
| YGC                                | ms      | Young GC count            |
| YGCT | s | Young GC time |
| FGCT                                    | s        | Full GC time                           |
| GCT                                           | s       | Garbage collection time                                     |
| ReceivedBytes                                 | Bytes/s  | Data receiving rate                                         |
| SentBytes                                     | Bytes/s  | Data sending rate                                         |
| RpcQueueTimeNumOps                      | Calls/s     | RPC call rate                               |
| RpcQueueTimeAvgTime                           | ms       | Average RPC delay                                     |
| RpcAuthenticationFailures               | Failures/s     | Number of RPC authentication failures                                     |
| RpcAuthenticationSuccesses                    | Successes/s     | Number of RPC authentication successes                                     |
| RpcAuthorizationFailures                      | Failures/s     | Number of RPC authorization failures                                     |
| RpcAuthorizationSuccesses                     | Successes/s     | Number of RPC authorization successes                                     |
| NumOpenConnections                            | -     | Number of current connections                                         |
| CallQueueLength                         | -        | Length of current RPC processing queue                      |
| CurrentThreadSystemTime                 | ms       | System time                                   |
| CurrentThreadUserTime                   | ms       | User time                                   |
| StartTime                     | s        | Process start time   |
| PeckThreadCount                         | -       | Peak number of threads        |
| DaemonThreadCount                             | -       | Number of background threads                                         |
| write                                   | MB/s     | Disk write rate                                 |
| read                                    | Queries/s     | QPS of read operations                                 |
| FsyncNanosOps                           | Operation/s     | Average number of Fsync operations                         |
| DataPacketOps                           | Operations/s     | QPS of packet transmission operations                              |

### HDFS - Journal Node 

| Metric Name | Unit | Description |
| -------------------------- | -------- | --------------------------------------- |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently used by JVM |
| MemNonHeapCommittedM                          | MB       | JVM memory                                             |
| MemHeapUsedM | MB | Size of HeapMemory currently used by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum memory size that can be used by JVM during runtime| 
| ThreadsNew                                    | -       | Number of threads in new state                               |
| ThreadsRunnable                               | -       | Number of threads in runnable state                             |
| ThreadsBlocked                                | - | Number of threads in blocked state |
| ThreadsWaiting                     | -       | Number of threads in WAITING state     |
| ThreadsTimedWaiting                     | -       | Number of threads in TIMED WAITING state     |
| ThreadsTerminated                             | -       | Number of threads in Terminated state                       |
| LogFatal                                      | -       | Number of Fatal logs                                       |
| LogError                                      | -       | Number of Error logs                                       |
| LogWarn                                       | -       | Number of Warn logs                                       |
| LogInfo                                       | -       | Number of Info logs                                       |
| S0                                             | %        | Percentage of used Survivor 0 memory                                   |
| S1                                             | %        | Percentage of used Survivor 1 memory                                   |
| E                                             | %        | Percentage of used Eden memory                                   |
| O                                             | %        | Percentage of used Old memory                                   |
| M                                             | %        | Percentage of used Metaspace memory                                   |
| CCS                                           | %        | Percentage of memory used by compressed class space             |
| FGC                                | -       | Full GC count            |
| YGC                                | -       | Young GC count            |
| YGCT                       | s        | Young GC time                       |
| FGCT                                    | s        | Full GC time                           |
| GCT                                           | s       | Garbage collection time                                     |
| ReceivedBytes                                 | Bytes/s  | Data receiving rate                                         |
| SentBytes                                     | Bytes/s  | Data sending rate                                         |
| RpcQueueTimeNumOps                      | Calls/s     | RPC call rate                               |
| RpcQueueTimeAvgTime                           | ms       | Average RPC delay                                     |
| RpcAuthenticationFailures               | Failures/s     | Number of RPC authentication failures                                     |
| RpcAuthenticationSuccesses                    | Successes/s     | Number of RPC authentication successes                                     |
| RpcAuthorizationFailures                      | Failures/s     | Number of RPC authorization failures                                     |
| NumOpenConnections                            | -     | Number of current connections                                         |
| CallQueueLength                         | -        | Length of current RPC processing queue                      |
| CurrentThreadSystemTime    | ms       | System time                                   |
| CurrentThreadUserTime                   | ms       | User time                                   |
| StartTime                     | s        | Process start time   |
| ThreadCount                   | -       | Number of threads                             |
| PeckThreadCount                         | -       | Peak number of threads        |
| DaemonThreadCount                             | -       | Number of background threads                                         |

### HDFS - ZKFC

| Metric Name | Unit | Description |
| -------- | -------- | ------------------------------------- |
| S0                                             | %        | Percentage of used Survivor 0 memory                                   |
| S1                                             | %        | Percentage of used Survivor 1 memory                                   |
| E                                             | %        | Percentage of used Eden memory                                   |
| O                                             | %        | Percentage of used Old memory                                   |
| M                                             | %        | Percentage of used Metaspace memory                                   |
| CCS                                           | %        | Percentage of memory used by compressed class space             |
| FGC                                | -       | Full GC count            |
| YGC                                | -       | Young GC count            |
| YGCT | s | Young GC time |
| FGCT                                    | s        | Full GC time                           |
| GCT                                           | s       | Garbage collection time                                     |
