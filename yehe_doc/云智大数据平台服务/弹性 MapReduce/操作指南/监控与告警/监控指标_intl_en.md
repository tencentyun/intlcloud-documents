## Server Monitoring Metrics

### Server - CPU

| Metric Name | Unit | Description |
| --------- | ---- | ------------------------------ |
| idle      | %    | Percentage of CPU idle time |
| irq       | %    | Percentage of interrupts |
| nice      | %    | Percentage of CPU utilization under nice priority |
| steal     | %    | Percentage of wait time by virtual CPUs for physical CPUs |
| softirq   | %    | Percentage of CPU soft interrupts |
| guest     | %    | Percentage of time spent running virtual processors |
| system    | %    | CPU utilization in kernel state |
| user      | %    | CPU utilization in user state |
| iowait    | %    | Percentage of CPU idleness due to process I/O waits |
| 1m        | Load/s  | 1-minute load                      |
| 5m        | Load/s  | 5-minute load                      |
| 15m       | Load/s  | 15-minute load                     |
| cpu_count | - | Number of CPU cores |

### CPU - memory

| Metric Name | Unit | Description |
| ----------------- | ---- | ------------------------------ |
| MemTotal          | GB   | Total memory size |
| MemFree           | GB   | Total free memory size |
| MemAvailable      | GB   | Total available memory size |
| Buffers           | GB   | Total memory size used by buffers |
| Cached            | GB   | Total memory size used by file cache |
| SwapCached        | GB   | Total swap memory size by anonymous page writes |
| SwapFree          | GB   | Total available swap size |
| AnonPages         | GB   | Total unmapped memory size |
| SwapTotal         | GB   | Total swap size |
| Dirty             | GB   | Total memory size to write to disk       |
| Writeback         | GB   | Total memory size being written back to disk       |
| HardwareCorrupted | GB   | Total unavailable memory size due to memory hardware failure |
| Shmem             | GB   | Total shared memory size         |
| available_percent | %    | Percentage of available memory size out of total memory |
| used_percent      | %    | Percentage of used memory size out of total memory    |

### Server - network

| Metric Name | Unit | Description |
| ---------------------- | -------- | ------------------------------------------------------------ |
| ListenDrops            | Connections/s     | Number of incoming connections (SYN packets) dropped for any reason |
| ListenOverflows        | Occurrences/s | Number of occurrences where the upper limit of the Accept queue is exceeded after the last step of three-way handshake is completed |
| SyncookiesFailed       | Packets/s | Number of packets received with invalid SYN Cookie information |
| SyncookiesRecv         | Packets/s | Number of packets received with valid SYN Cookie information |
| SyncookiesSent         | Packets/s     | Number of SYN/ACK packets sent through SYN Cookie                        |
| TCPAbortOnTimeout | Connections/s | Number of connection closed because the attempts of retransmissions of various timers (RTO/PTO/keepalive) exceed the upper limit |
| TCPAbortOnData         | Sockets/s     | Number of sockets closed due to unknown data received                          |
| TCPAbortOnClose        | Sockets/s     | Number of sockets closed when the user-mode program has data in the buffer             |
| TCPAbortOnMemory       | Connections/s     | Number of connections closed due to memory issues                                     |
| TCPAbortOnLinger | Connections/s | Number of connections suspended in lingering state after being closed |
| TCPAbortFailed         | Attempts/s     | Number of failed attempts to close connection                                       |
| ActiveOpens            | Connections/s     | Number of actively established TCP connections                                        |
| CurrEstab              | Connections/s     | Number of TCP connections currently established                                      |
| ActiveOpens            | Connections/s     | Number of passively established TCP connections                                        |
| AttemptFails           | Failures/s     | Number of connection establishment failures                                             |
| EstabResets            | Connections/s     | Number of reset connections                                           |
| InSegs  | Packets/s | Number of received packets, including erroneous ones |
| OutSegs                | Packet/s     | Number of sent data packets                                                 |
| RetransSegs            | Packets/s     | Number of received TCP packets                                             |
| InErrs                 | Packet/s     | Number of retransmitted packets                                                 |
| OutRsts                 | Packet/s     | Number of sent RST packets                                                 |
| RetransSegsRate        | %        | Retransmission rate at TCP layer                                                 |
| ResetRate              | %        | RESET sending frequency                                               |
| InErrRate              | %        | Percentage of erroneous packets                                                   |
| TW | Sockets/s     | Number of sockets ending TIME_WAIT state after normal timeout      |
| TWKilled               | Sockets/s     | Number of sockets ending TIME_WAIT state through tcp_tw_recycle mechanism      |
| TCPTimeWaitOverflow    | Sockets/s     | Number of TIME_WAIT sockets unable to be allocated due to limit exceeding               |
| TWRecycled             | Sockets/s     | Number of sockets ending TIME_WAIT state through tcp_tw_reuse mechanism      |
| TCPTimeouts            | Timeouts/s     | Number of first RTO timer timeouts                                     |
| TCPSpuriousRTOs        | Timeouts/s     | Number of spurious timeouts detected through F-RTO mechanism                            |
| TCPLossProbes          | Packets/s     | Number of Tail Loss Probe (TLP) packets sent due to Probe Timeout (PTO)      |
| TCPLossProbeRecovery   | Packets/s | Number of lost packets just repaired by TLP probes |
| TCPRenoRecoveryFail    | Connections/s | Number of connections that enter the Recovery phase and then undergo RTO (SACK option not supported by the opposite) |
| TCPSackRecoveryFail | Connections/s | Number of connections that enter the Recovery phase and then undergo RTO (SACK option supported by the opposite) |
| TCPRenoFailures        | Failures/s | Number of failures that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option not supported by the opposite) |
| TCPSackFailures        | Failures/s | Number of failures that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option supported by the opposite) |
| TCPLossFailures        | Connections/s | Number of connections that enter the TCP_CA_Loss phase and then undergo RTO timeout |
| RtoAlgorithm           | Algorithms/s | Number of delayed algorithms for forwarding unanswered objects |
| RtoMax                 | Retransmissions/s      | Maximum number of retransmissions due to TCP delay                                         |
| RtoMin                 | Retransmissions/s      | Minimum number of retransmissions due to TCP delay                                         |
| TCPLostRetransmit      | Retransmissions/s     | Number of SKB retransmissions due to loss                                          |
| TCPFastRetrans         | Retransmissions/s     | Number of fast SKB retransmissions                                              |
| TCPForwardRetrans      | Retransmissions/s     | Number of regular SKB transmissions                                              |
| TCPSlowStartRetrans    | Retransmissions/s     | Number of SKB retransmissions with successful slow start                                      |
| TCPRetransFail         | Failures/s     | Number of failed retransmission attempts                                             |
| OutDatagrams           | Datagrams/s     | Number of sent UDP datagrams                                        |
| InDatagrams            | Datagrams/s     | Number of received UDP datagrams                                        |
| eth0-receive_bytes     | MB/s     | Volume of data received by ENI                                               |
| eth0-transmit_bytes    | MB/s     | Volume of data sent by ENI                                               |
| eth0-receive_drop      | Packets/s | Volume of data received and then dropped by ENI                                               |
| eth0-receive_errs      | Packets/s | Volume of data failed to be received by ENI                                             |
| eth0-transmit_drop     | Packets/s | Volume of data sent and then dropped by ENI                                           |
| eth0-transmit_errs     | Packets/s | Volume of data failed to be sent by ENI                                          |
| eth0-transmit_packetsl | Packet/s | Number of packets sent by ENI                                               |
| TCP_inuse | - | Number of TCP sockets in use (listening) |
| TCP_orphan             | -       | Number of TCP connections waiting to be closed                                        |
| TCP_tw | - | Number of TCP sockets to be destroyed |
| TCP_alloc | - | Number of TCP sockets allocated (established, sk_buff obtained) |
| ESTABLISHED                           | -       | Number of TCP connections in Established state                                 |
| SYN-SENT               | -       | Number of TCP connections in SYN-SENT state                                 |
| SYN-RECV              | -       | Number of TCP connections in SYN-RECV state                                |
| FIN-WAIT1              | -       | Number of TCP connections in FIN-WAIT1 state                                |
| FIN-WAIT2              | -       | Number of TCP connections in FIN-WAIT2 state                                |
| TIME-WAIT              | -       | Number of TCP connections in TIME-WAIT state                                |
| CLOSE              | -       | Number of TCP connections in CLOSE state                                |
| CLOSE-WAIT               | -       | Number of TCP connections in CLOSE-WAIT state                                 |
| LAST-ACK                           | -       | Number of TCP connections in LAST-ACK state                                 |
| LISTEN                           | -       | Number of TCP connections in LISTEN state                                 |
| CLOSEING               | -       | Number of TCP connections in CLOSEING state                                 |

### Server - disk

| Metric Name | Unit | Description |
| ----------- | ---- | ------------------------------- |
| Read        | MB/s | Data read per second                    |
| Write       | MB/s | Data written per second                    |
| vd-         | -   | Number of I/O operations in progress on current device      |
| Read        | ms   | Average wait time per device I/O read operation |
| Write       | ms   | Average wait time per device I/O write operation |
| IO          | ms   | Average processing time per I/O request |
| Read        | Queries/s | Read QPS                      |
| Write       | Queries/s | Write QPS                      |
| Merge-Read  | Queries/s | Merged read QPS                  |
| Merge-Write | Queries/s | Merged write QPS                  |
| vd-         | %    | Disk busyness                 |
| Free        | GB   | Free disk capacity                    |
| Used        | GB   | Used disk capacity                  |
| Total       | GB   | Total disk capacity                      |
| Used        | %    | Disk utilization                      |
| Free        | -   | Number of remaining disk inodes            |
| Total       | -   | Total number of disk inodes              |
| Used        | %    | Disk inode utilization              |

### Server - file handle

| Metric Name | Unit | Description |
| --------- | ---- | ------------------ |
| allocated | - | Number of allocated file handles |
| maximum   | - | Maximum number of file handles |

### Server - process

| Metric Name | Unit | Description |
| ---------------------- | ------- | ------------------ |
| intr_total             | Interrupts/s    | Number of system interrupts       |
| context_switches_total | Switches/s    | Number of system context switches |
| forks_total | Processes/s | Number of new system processes |
| procs_running          | Processes/s    | Number of running system processes   |
| procs_blocked          | Processes/s    | Number of blocked system processes   |
| procs_total            | Processes/s    | Total number of system processes     |
| AgentVersionl          | version | Agent version       |

## HDFS Monitoring Metrics

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
| UnderReplicatedBlocks        | -       | Number of blocks with insufficient replicates                            |
| CorruptBlocks | - | Number of corrupted blocks |
| ScheduledReplicationBlocks   | -       | Number of blocks arranged for backup                            |
| PendingDeletionBlocks        | -       | Number of blocks waiting to be deleted                            |
| ExcessBlocks                 | -       | Number of excessive blocks                                  |
| PostponedMisreplicatedBlocks | -       | Number of exceptional blocks postponed to be processed                        |
| BlockCapacity | - | Capacity of blocks |
| NumLiveDataNodes             | -       | Number of live data nodes                              |
| NumDeadDataNodes             | -       | Number of data nodes marked as dead            |
| NumDecomLiveDataNodes        | -       | Number of deactivate live nodes                        |
| NumDecomDeadDataNodes        | -       | Number of deactivated dead nodes                        |
| NumDecommissioningDataNodes  | -       | Number of deactivating nodes |
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
| RpcAuthenticationFailures                     | -     | Number of RPC authentication failures                                     |
| RpcAuthenticationSuccesses                    | - | Number of RPC authentication successes                                     |
| RpcAuthorizationFailures                      | -     | Number of RPC authorization failures                                     |
| RpcAuthorizationSuccesses                     | - | Number of RPC authorization successes                                     |
| NumOpenConnections                            | -     | Number of current connections                                         |
| CallQueueLength                               | -     | Length of current RPC processing queue                                |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently used by JVM |
| MemNonHeapCommittedM                          | MB       | JVM memory                                             |
| MemHeapUsedM | MB | Size of HeapMemory currently used by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to JVM runtime |
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
| | RemoteBytesReadMB | Bytes/s | Rate of bytes read by remote client |
| | RemoteBytesWrittenMB                    | Bytes/s | Rate of bytes written by remote client |
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
| FsyncNanosOps                           | Operations/s     | Number of Fsync operations                                 |
| FlushNanosNumOps                        | Operations/s     | Number of Flush operations processed per second                      |
| ReadBlockOpAvgTime                      | ms       | Average block read time                    |
| WriteBlockOpAvgTime                     | ms       | Average block write operation time                         |
| BlockChecksumOpAvgTime                  | ms       | Average block check time |                         |
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
| RamDiskBytesLazyPersisted               | Bytes/s  | Total number of bytes written to disk by lazy writer           |
| RamDiskBytesWrite                       | Bytes/s  | Total number of bytes written to memory                        |
| MemNonHeapUsedM | MB | Size of NonHeapMemory currently used by JVM |
| MemNonHeapCommittedM                    | MB | Size of NonHeapCommittedM configured by JVM |
| MemHeapUsedM | MB | Size of HeapMemory currently used by JVM |
| MemHeapCommittedM | MB | Submitted size of JVM HeapMemory |
| MemHeapMaxM | MB | Size of HeapMemory configured by JVM |
| MemMaxM | MB | Maximum size of memory available to JVM runtime |
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
| MemMaxM | MB | Maximum size of memory available to JVM runtime |
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

## Yarn Monitoring Metrics

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
| AllocatedContainers            | -       | Total number of containers         |
| PendingContainers            | -       | Total number of containers         |
| ReservedContainers           | -       | Total number of containers         |
| AggregateContainersAllocated | -       | Number of allocated containers |
| AggregateContainersReleased | -       | Number of released containers |
| ActiveUsers                  | -       | Number of users           |

### YARN - ResourceManager

| Metric Name | Unit | Description |
| :------------------------- | :------- | ------------------ |
| RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     |
| ReceivedBytes              | Bytes/s  | Volume of sent data received by RPC |
| SentBytes                  | Bytes/s  | Volume of sent data received by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
| RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     |
| ReceivedBytes              | Bytes/s  | Volume of sent data received by RPC |
| SentBytes                  | Bytes/s  | Volume of sent data received by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
| RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     |
| ReceivedBytes              | Bytes/s  | Volume of sent data received by RPC |
| SentBytes                  | Bytes/s  | Volume of sent data received by RPC |
| NumOpenConnections         | -       | Number of RPC connections         |
| RpcProcessingTimeNumOps    | -       | Number of RPC requests       |
| RpcQueueTimeNumOps         | -       | Number of RPC requests       |
| CallQueueLength            | -       | RPC queue length       |
| RpcProcessingTimeAvgTime   | s        | Average RPC processing time   |
| RpcQueueTimeAvgTime        | s        | Average RPC processing time   |
| RpcAuthenticationFailures  | -       | Number of RPC authentication authorizations     |
| RpcAuthenticationSuccesses | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationFailures   | -       | Number of RPC authentication authorizations     |
| RpcAuthorizationSuccesses  | -       | Number of RPC authentication authorizations     |
| ReceivedBytes              | Bytes/s  | Volume of sent data received by RPC |
| SentBytes                  | Bytes/s  | Volume of sent data received by RPC |
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
| MaxFileDescriptorCount             | -       | Number of file descriptor      |
| OpenFileDescriptorCount            | -       | Number of file descriptor      |
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
| MaxFileDescriptorCount             | -       | Number of file descriptor      |
| OpenFileDescriptorCount            | -       | Number of file descriptor      |
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



## HBase Monitoring Metrics

### Hbase - overview

| Metric Name | Unit | Description |
| ----------------------- | -------- | -------------------------- |
| ritCount                | -       | Number of cluster regions in RIT state  |
| ritCountOverThreshold   | -       | Number of cluster regions in RIT state  |
| ritOldestAge            | ms       | Cluster RIT time              |
| averageLoad             | -       | Average number of regions per RS |
| numRegionServers        | -       | Number of cluster RSs               |
| numDeadRegionServers    | -       | Number of cluster RSs               |
| receivedBytes           | Bytes/s  | Number of cluster reads/writes               |
| sentBytes               | Bytes/s  | Number of cluster reads/writes               |
| clusterRequests | Requests/s | Total number of requests in cluster |
| Assign_num_ops      | -       | Cluster assignment manager operations |
| BulkAssign_num_ops      | -       | Cluster assignment manager operations |
| BalancerCluster_num_ops | -       | Number of cluster load balancing operations           |
| mergePlanCount          | -       | Cluster plans                  |
| splitPlanCount          | -       | Cluster plans                  |

### HBase - HMaster

| Metric Name | Unit | Description |
| ------------------------------ | -------- | -------------- |
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
| ThreadsNew                     | -       | Number of JVM threads     |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
| numOpenConnections                | -       | Number of RPC connections         |
| FailedSanityCheckException        | -       | Number of RPC exceptions       |
| NotServingRegionException         | -       | Number of RPC exceptions       |
| OutOfOrderScannerNextException    | -       | Number of RPC exceptions       |
| RegionMovedException              | -       | Number of RPC exceptions       |
| RegionTooBusyException         | -       | Number of RPC exceptions       |
| UnknownScannerException           | -       | Number of RPC exceptions       |
| numCallsInPriorityQueue        | -       | Number of RPC queue requests     |
| numCallsInReplicationQueue        | -       | Number of RPC queue requests     |
| masterActiveTime               | s        | Process start time   |
| masterStartTime                | s        | Process start time   |

### HBase - RegionServer

| Metric Name | Unit | Description |
| --------------------------------- | -------- | ------------------ |
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
| ThreadsNew                     | -       | Number of JVM threads     |
| ThreadsRunnable                     | -       | Number of JVM threads     |
| ThreadsBlocked                     | -       | Number of JVM threads     |
| ThreadsWaiting                     | -       | Number of JVM threads     |
| ThreadsTimedWaiting            | -       | Number of JVM threads     |
| ThreadsTerminated              | -       | Number of JVM threads     |
| averageRegionSize                 | Byte | Average region size |
| regionCount                       | -       | Number of regions       |
| percentFilesLocalSecondaryRegions | %        | Region replicate localization |
| authenticationFailures            | -       | Number of RPC authentications       |
| authenticationSuccesses            | -       | Number of RPC authentications       |
| numOpenConnections                | -       | Number of RPC connections         |
| FailedSanityCheckException        | -       | Number of RPC exceptions       |
| NotServingRegionException         | -       | Number of RPC exceptions       |
| OutOfOrderScannerNextException    | -       | Number of RPC exceptions       |
| RegionMovedException              | -       | Number of RPC exceptions       |
| RegionTooBusyException            | -       | Number of RPC exceptions       |
| UnknownScannerException           | -       | Number of RPC exceptions       |
| numActiveHandler                  | -       | Number RPC handles         |
| numCallsInPriorityQueue           | -       | Number of RPC queue requests     |
| numCallsInReplicationQueue        | -       | Number of RPC queue requests     |
| numCallsInGeneralQueue            | -       | Number of RPC queue requests     |
| hlogFileCount                     | -       | Number of WAL files       |
| hlogFileSize                      | Bytes     | WAL file size       |
| memStoreSize                      | MB       | Memstore size      |
| storeCount                        | -       | Number of stores |
| storeFileCount                    | -       | Number of Storefiles    |
| storeFileSize                     | MB       | Storefile size     |
| flushedCellsSize                  | Bytes/s  | Disk write rate         |
| Append_mean                       | ms       | Average delay           |
| Replay_mean                       | ms       | Average delay           |
| Get_mean                          | ms       | Average delay           |
| updatesBlockedTime                                       | ms       | Average delay           |
| FlushTime_num_ops                 | -       | Number of RS disk writes      |
| splitQueueLength                  | -       | Number of operation queue requests     |
| compactionQueueLength             | -       | Number of operation queue requests     |
| flushQueueLength                  | -       | Number of operation queue requests     |
| Replay_num_ops                    | -       | Number of Replay operations    |
| slowAppendCount                   | -       | Number of slow operations         |
| slowDeleteCount                   | -       | Number of slow operations         |
| slowGetCount                      | -       | Number of slow operations         |
| slowIncrementCount                | -       | Number of slow operations         |
| slowPutCount                      | -       | Number of slow operations         |
| splitRequestCount                 | -       | Split requests         |
| splitSuccessCount                 | -       | Split requests         |
| blockCacheCount                   | -       | Number of cache blocks         |
| blockCacheHitCount                | -       | Number of cache blocks         |
| blockCacheMissCount                 | -       | Number of cache blocks         |
| blockCacheExpressHitPercent       | %        | Cache read hit rate       |
| blockCacheSize                    | Byte     | Memory size used by cache block |
| staticBloomSize                   | Bytes     | Index size           |
| staticIndexSize                   | Bytes     | Index size           |
| storeFileIndexSize                | Bytes     | Index size           |
| receivedBytes                     | bytes/s  | Read/write traffic           |
| sentBytes                         | bytes/s  | Read/write traffic           |
| Total                             | Requests/s     | Number of read/write requests         |
| Read | Requests/s     | Number of read/write requests         |
| Write                                   | Requests/s     | Number of read/write requests         |
| Append_num_ops                             | Requests/s     | Number of read/write requests         |
| mutationsWithoutWALCount          | -       | Number of mutations       |
| mutationsWithoutWALSize           | Bytes     | Mutation size      |
| regionServerStartTime             | s        | Process start time   |

## Hive Monitoring Metrics

### Hive - HiveMetaStore

| Metric Name | Unit | Description |
| -------- | -------- | ------------------------------------- |
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

### Hive - HiveServer2

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
| ProcessCpuLoad                 | %        | CPU utilization       |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptor      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |
| ProcessCpuTime                     | ms       | Cumulative CPU usage time   |
| Uptime                             | s        | Process run time      |
| DaemonThreadCount                  | -       | Number of Daemon threads        |
| ThreadCount                        | -       | Total number of threads        |

### Hive - HiveWebHcat

| Metric Name | Unit | Description |
| -------- | -------- | ------------------------------------- |
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

## ZooKeeper Monitoring Metrics

### ZooKeeper

| Metric Name | Unit | Description |
| ----------------------------- | --------------------- | --------------------------------------- |
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
| ProcessCpuLoad                 | %        | CPU utilization       |
| MaxFileDescriptorCount             | -       | Maximum number of file descriptor      |
| OpenFileDescriptorCount | -                    | Number of opened file descriptors                      |
| zk_max_file_descriptor_count | -       | Maximum number of file descriptor      |
| zk_open_file_descriptor_count | -                    | Number of opened file descriptors                      |
| ProcessCpuTime                     | ms       | Cumulative CPU usage time   |
| Uptime                             | s        | Process run time      |
| DaemonThreadCount                  | -       | Number of Daemon threads        |
| ThreadCount                        | -       | Total number of threads        |
| zk_num_alive_connections      | -                    | Number of current connections |
| zk_avg_latency                | ms                    | Average delay in ZooKeeper processing                         |
| zk_max_latency                | ms                    | Maximum delay in ZooKeeper processing                        |
| zk_min_latency                | ms                    | Minimum delay in ZooKeeper processing                         |
| zk_watch_count                | -                   | Number of ZooKeeper watches                        |
| zk_znode_count                | -                    | Number of ZooKeeper znodes                        |
| zk_ephemerals_count           | -                    | Number of temporary ZooKeeper nodes                       |
| zk_approximate_data_size      | Byte                  | Volume of data stored in ZooKeeper                           |
| zk_server_state               | 1: master, 0: slave, 2: single server | ZooKeeper node type                             |
| zk_packets_received           | Packets/s                  | ZooKeeper package receiving rate                     |
| zk_packets_sent               | Packets/s                  | ZooKeeper package sending rate                     |
| zk_outstanding_requests       | -                    | Number of waiting requests                              |

## Spark Monitoring Metrics

### SPARK - SparkJobHistory 

| Metric Name | Unit | Description |
| -------- | -------- | ------------------------------------- |
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

## Presto Monitoring Metrics

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
