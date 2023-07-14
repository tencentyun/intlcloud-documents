### HDFS - Overview
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=4>Cluster storage capacity</td>
<td >CapacityTotal </td>
<td >GB </td>
<td >Total cluster storage capacity</td>
</tr><tr>
<td >CapacityUsed </td>
<td >GB </td>
<td >Used cluster storage capacity</td>
</tr><tr>
<td >CapacityRemaining </td>
<td >GB </td>
<td >Remaining cluster storage capacity</td>
</tr><tr>
<td >CapacityUsedNonDFS </td>
<td >GB </td>
<td >Non-HDFS used cluster capacity</td>
</tr><tr>
<td >Cluster load</td>
<td >TotalLoad </td>
<td >1 </td>
<td >Current connections</td>
</tr><tr>
<td >Total files in cluster</td>
<td >FilesTotal </td>
<td > - </td>
<td >Total number of files</td>
</tr><tr>
<td rowspan=8>Blocks</td>
<td >BlocksTotal </td>
<td > - </td>
<td >Total number of blocks</td>
</tr><tr>
<td >PendingReplicationBlocks </td>
<td > - </td>
<td >Number of blocks waiting to be backed up</td>
</tr><tr>
<td >UnderReplicatedBlocks </td>
<td > - </td>
<td >Number of blocks with insufficient replicas</td>
</tr><tr>
<td >CorruptBlocks </td>
<td > - </td>
<td >Number of corrupted blocks</td>
</tr><tr>
<td >ScheduledReplicationBlocks </td>
<td > - </td>
<td >Number of blocks arranged for backup</td>
</tr><tr>
<td >PendingDeletionBlocks </td>
<td > - </td>
<td >Number of blocks waiting to be deleted</td>
</tr><tr>
<td >ExcessBlocks </td>
<td > - </td>
<td >Number of excess blocks</td>
</tr><tr>
<td >PostponedMisreplicatedBlocks</td>
<td > - </td>
<td >Number of abnormal blocks postponed to be processed</td>
</tr><tr>
<td >Block capacity</td>
<td >BlockCapacity </td>
<td > - </td>
<td >Block capacity</td>
</tr><tr>
<td rowspan=6>Cluster data node</td>
<td >NumLiveDataNodes </td>
<td > - </td>
<td >Number of live data nodes</td>
</tr><tr>
<td >NumDeadDataNodes </td>
<td > - </td>
<td >Number of data nodes marked as dead</td>
</tr><tr>
<td >NumDecomLiveDataNodes </td>
<td > - </td>
<td >Number of decommissioned live nodes</td>
</tr><tr>
<td >NumDecomDeadDataNodes </td>
<td > - </td>
<td >Number of decommissioned dead nodes</td>
</tr><tr>
<td >NumDecommissioningDataNodes </td>
<td > - </td>
<td >Number of decommissioning nodes</td>
</tr><tr>
<td >NumStaleDataNodes </td>
<td > - </td>
<td >Number of DataNodes marked as stale</td>
</tr><tr>
<td >HDFS storage space utilization</td>
<td >CapacityUsedRate </td>
<td > - </td>
<td >HDFS cluster storage space utilization</td>
</tr><tr>
<td >Snapshots</td>
<td >Snapshots </td>
<td >-</td>
<td >Number of snapshots</td>
</tr><tr>
<td >Disk failure</td>
<td >VolumeFailuresTotal </td>
<td >-</td>
<td >Total number of volume failures across all DataNodes</td>
</tr>
</table>

### HDFS - NameNode
<table>
<tr>
<th width=22%>Title</th>
<th width=20%>Metric</th>
<th width=13%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>Data traffic</td>
<td >ReceivedBytes</td>
<td >Bytes/s</td>
<td >Data receiving rate</td>
</tr><tr>
<td >SentBytes </td>
<td >Bytes/s </td>
<td >Data sending rate</td>
</tr><tr>
<td >QPS </td>
<td >RpcQueueTimeNumOps </td>
<td >1/s </td>
<td >RPC call rate</td>
</tr><tr>
<td rowspan=2>Request processing latency</td>
<td >RpcQueueTimeAvgTime </td>
<td >ms </td>
<td >Average RPC latency</td>
</tr><tr>
<td >RpcProcessingTimeAvgTime </td>
<td >ms </td>
<td >Average RPC request processing time</td>
</tr><tr>
 <td rowspan=4>Authentication and authorization</td>
 <td >RpcAuthenticationFailures </td>
<td > 1 per time</td>
<td >Number of RPC authentication failures</td>
</tr><tr>
<td >RpcAuthenticationSuccesses </td>
<td > 2 per time</td>
<td >Number of RPC authentication successes</td>
</tr><tr>
<td >RpcAuthorizationFailures </td>
<td > 3 per time</td>
<td >Number of RPC authorization failures</td>
</tr><tr>
<td >RpcAuthorizationSuccesses </td>
<td > 4 per time</td>
<td >Number of RPC authorization successes</td>
</tr><tr>
<td >Current connections</td>
<td >NumOpenConnections </td>
<td >-</td>
<td >Number of current connections</td>
</tr><tr>
<td >Length of RPC processing queue</td>
<td >CallQueueLength </td>
<td >-</td>
<td >Length of current RPC processing queue</td>
</tr><tr>
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapCommittedM configured by JVM</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Committed size of JVM HeapMemory</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB</td>
<td >Maximum size of memory available to JVM runtime</td>
</tr><tr>
<td >Block reporting latency</td>
<td >BlockReportAvgTime </td>
<td >count/s</td>
<td >Average latency of processing DataNode blocks per second</td>
</tr><tr>
<td rowspan=6>JVM threads</td>
<td >ThreadsNew </td>
<td > - </td>
<td >Number of threads in NEW status</td>
</tr><tr>
<td >ThreadsRunnable </td>
<td > - </td>
<td >Number of threads in RUNNABLE status</td>
</tr><tr>
<td >ThreadsBlocked </td>
<td > - </td>
<td >Number of threads in BLOCKED status</td>
</tr><tr>
<td >ThreadsWaiting </td>
<td > - </td>
<td >Number of threads in WAITING status</td>
</tr><tr>
<td >ThreadsTimedWaiting </td>
<td > - </td>
<td >Number of threads in TIMED WAITING status</td>
</tr><tr>
<td >ThreadsTerminated </td>
<td > - </td>
<td >Number of threads in Terminated status</td>
</tr><tr>
<td rowspan=4>JVM logs</td>
<td >LogFatal </td>
<td > - </td >
<td >Number of FATAL-level logs</td>
</tr><tr>
<td >LogError </td>
<td > - </td>
<td >Number of ERROR-level logs</td>
</tr>			<tr>
<td >LogWarn </td>
<td > - </td>
<td >Number of WARN-level logs</td>
</tr><tr>
<td >LogInfo </td>
<td > - </td>
<td >	Number of INFO-level logs</td>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >Storages marked as content stale</td>
<td >NumStaleStorages </td>
<td > - </td>
<td >Number of DataNode storages marked as content stale</td>
</tr><tr>
<td >Pending block-related messages for later processing on the standby NameNode</td>
<td >PendingDataNodeMessageCount </td>
<td >count/s</td>
<td >Number of DataNode requests queued on the standby NameNode</td>
</tr><tr>
<td rowspan=2>Missing blocks</td>
<td >NumberOfMissingBlocks </td>
<td > - </td>
<td >Number of missing blocks</td>
</tr><tr>
<td >NumberOfMissingBlocksWithReplicationFactorOne</td>
<td > - </td>
<td >Number of missing blocks (rf = 1)</td>
</tr><tr>
<td rowspan=7>Snapshot operation</td>
<td >AllowSnapshotOps </td>
<td >count/s</td>
<td >Number of AllowSnapshot operations executed per second</td>
</tr><tr>
<td >DisallowSnapshotOps </td>
<td >count/s</td>
<td >Number of DisallowSnapshot operations executed per second</td>
</tr><tr>
<td >CreateSnapshotOps </td>
<td >count/s</td>
<td >Number of CreateSnapshot operations executed per second</td>
</tr><tr>
<td >DeleteSnapshotOps </td>
<td >count/s</td>
<td >Number of DeleteSnapshot operations executed per second</td>
</tr><tr>
<td >ListSnapshottableDirOps </td>
<td >count/s</td>
<td >Number of ListSnapshottableDir operations executed per second</td>
</tr><tr>
<td >SnapshotDiffReportOps </td>
<td >count/s</td>
<td >Number of SnapshotDiffReportOps operations executed per second</td>
</tr><tr>
<td >RenameSnapshotOps </td>
<td >count/s</td>
<td >Number of RenameSnapshotOps operations executed per second</td>
</tr><tr>
<td rowspan=9>File operation</td>
<td >CreateFileOps </td>
<td >count/s</td>
<td >Number of CreateFile operations executed per second</td>
</tr><tr>
<td >GetListingOps </td>
<td >count/s</td>
<td >Number of GetListing operations executed per second</td>
</tr><tr>
<td >TotalFileOps </td>
<td >count/s</td>
<td >Number of TotalFileOps operations executed per second</td>
</tr><tr>
<td >DeleteFileOps </td>
<td >count/s</td>
<td >Number of DeleteFile operations executed per second</td>
</tr><tr>
<td >FileInfoOps </td>
<td >count/s</td>
<td >Number of FileInfo operations executed per second</td>
</tr><tr>
<td >GetAdditionalDatanodeOps </td>
<td >count/s</td>
<td >Number of GetAdditionalDatanode operations executed per second</td>
</tr><tr>
<td >CreateSymlinkOps </td>
<td >count/s</td>
<td >Number of CreateSymlink operations executed per second</td>
</tr><tr>
<td >GetLinkTargetOps </td>
<td >count/s</td>
<td >Number of GetLinkTarget operations executed per second</td>
</tr><tr>
<td >FilesInGetListingOps </td>
<td >count/s</td>
<td >Number of FilesInGetListing operations executed per second</td>
</tr>
<tr>
<td rowspan=3>File statistics</td>
<td >FilesDeleted </td>
<td >count</td>
<td >Number of deleted or renamed files and folders</td>
</tr><tr>
<td >FilesCreated </td>
<td >count </td>
<td >Number of created files and folders</td>
</tr>
<tr>
<td >FilesAppended </td>
<td >count </td>
<td >	Number of appended files</td>
</tr> 		
<tr>
<td rowspan=2>Transaction operation</td>
<td >TransactionsNumOps </td>
<td >count/s</td>
<td >Number of journal transaction operations processed per second</td>
</tr><tr>
<td >TransactionsBatchedInSync </td>
<td >count/s</td>
<td >Number of journal transaction operations batch processed per second</td>
</tr><tr>
<td rowspan=3>Image operation</td>
<td >GetEditNumOps </td>
<td >count/s</td>
<td >Number of GetEditNumOps operations executed per second</td>
</tr><tr>
<td >GetImageNumOps </td>
<td >count/s</td>
<td >Number of GetImageNumOps operations executed per second</td>
</tr><tr>
<td >PutImageNumOps </td>
<td >count/s</td>
<td >Number of PutImageNumOps operations executed per second</td>
</tr><tr>
<td >Sync operation</td>
<td >SyncsNumOps </td>
<td >count/s</td>
<td >Number of journal sync operations processed per second</td>
</tr><tr>
<td rowspan=2>Block operation</td>
<td >BlockReceivedAndDeletedOps </td>
<td >count/s</td>
<td >Number of BlockReceivedAndDeletedOps operations executed per second</td>
</tr><tr>
<td >BlockOpsQueued </td>
<td >count/s</td>
<td >Number of processed DataNode block reporting operations</td>
</tr><tr>
<td >Cache reporting</td>
<td >CacheReportNumOps </td>
<td >count/s</td>
<td >Number of CacheReport operations processed per second</td>
</tr><tr>
<td >Block reporting</td>
<td >BlockReportNumQps </td>
<td >count/s</td>
<td >Number of DataNode block reporting operations processed per second</td>
</tr><tr>
<td >Sync operation latency</td>
<td >SyncsAvgTime </td>
<td >ms </td>
<td >Average latency of processing journal sync operations</td>
</tr><tr>
<td >Cache reporting latency</td>
<td >CacheReportAvgTime </td>
<td >ms </td>
<td >Average latency of cache reporting</td>
</tr><tr>
<td rowspan=3>Image operation latency</td>
<td >GetEditAvgTime </td>
<td >ms </td>
<td >Average latency of reading Edit files</td>
</tr><tr>
<td >GetImageAvgTime </td>
<td >ms </td>
<td >Average latency of reading image files</td>
</tr><tr>
<td >PutImageAvgTime </td>
<td >ms </td>
<td >Average latency of writing image files</td>
</tr><tr>
<td >Transaction operation latency</td>
<td >TransactionsAvgTime </td>
<td >ms </td>
<td >Average latency of processing journal transaction operations</td>
</tr><tr>
<td >Start time</td>
<td >StartTime </td>
<td >ms </td>
<td >Process start time</td>
</tr><tr>
<td >Active/Standby status</td>
<td >State </td>
<td >1 </td>
<td >NameNode HA status</td>
</tr><tr>
<td >Active/Standby status</td>
<td >State </td>
<td >1: Active. 0: Standby</td>
<td >NameNode active/standby status</td>
</tr><tr>
<td rowspan=3>Threads</td>
<td >PeakThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >ThreadCount </td>
<td > - </td>
<td >Number of threads</td>
</tr><tr>
<td >DaemonThreadCount </td>
<td > - </td>
<td >Number of backend threads</td>
</tr>
<tr>
<td >Transactions since the last checkpoint</td>
<td >SinceLastCheckpoint </td>
<td >count </td>
<td >Total number of transactions since the last checkpoint</td>
</tr>
<tr>
<td >Checkpoint time</td>
<td >LastCheckpoint </td>
<td >time </td>
<td >Time since the last checkpoint</td>
</tr>
<tr>
<td >Length of the queue waiting for file locks</td>
<td >LockQueueLength </td>
<td >count </td>
<td >	LockQueueLength	 - length of the queue waiting for file locks</td>
</tr>
<tr>
<td rowspan=7>Average RPC time (1)</td>
<td >CompleteAvgTime </td>
<td >ms </td>
<td >	Average latency of Complete requests</td>
</tr>			
<tr>
<td >CreateAvgTime </td>
<td >ms </td>
<td >	Average latency of Create requests</td>
</tr>		
<tr>
<td >RenameAvgTime </td>
<td >ms </td>
<td >	Average latency of Rename requests</td>
</tr>	
<tr>
<td >AddBlockAvgTime </td>
<td >ms </td>
<td >	Average latency of AddBlock requests</td>
</tr>	
<tr>
<td >GetListingAvgTime </td>
<td >ms </td>
<td >	Average latency of GetListing requests</td>
</tr>	
<tr>
<td >GetFileInfoAvgTime </td>
<td >ms </td>
<td >	Average latency of GetFileInfo requests</td>
</tr>	
<tr>
<td >SendHeartbeatAvgTime </td>
<td >ms </td>
<td >	Average latency of SendHeartbeat requests</td>
</tr>	
<tr>
<td rowspan=7>Average RPC time (2)</td>
<td >RegisterDatanodeAvgTime </td>
<td >ms </td>
<td >	Average latency of RegisterDatanode requests</td>
</tr>			
<tr>
<td >BlockReportAvgTime </td>
<td >ms </td>
<td >	Average latency of BlockReport requests</td>
</tr>		
<tr>
<td >DeleteAvgTime </td>
<td >ms </td>
<td >	Average latency of Delete requests</td>
</tr>	
<tr>
<td >RenewLeaseAvgTime </td>
<td >ms </td>
<td >	Average latency of RenewLease requests</td>
</tr>	
<tr>
<td >BlockReceivedAndDeletedAvgTime </td>
<td >ms </td>
<td >	Average latency of BlockReceivedAndDeleted requests</td>
</tr>	
<tr>
<td >FsyncAvgTime </td>
<td >ms </td>
<td >	Average latency of fsync requests</td>
</tr>	
<tr>
<td >VersionRequestAvgTime </td>
<td >ms </td>
<td >	Average latency of VersionRequest requests</td>
</tr>
<tr>
<td rowspan=7>Average RPC time (3)</td>
<td >ListEncryptionZonesAvgTime </td>
<td >ms </td>
<td >	Average latency of ListEncryptionZones requests</td>
</tr>			
<tr>
<td >SetPermissionAvgTime </td>
<td >ms </td>
<td >	Average latency of SetPermission requests</td>
</tr>		
<tr>
<td >SetTimesAvgTime </td>
<td >ms </td>
<td >	Average latency of SetTimes requests</td>
</tr>	
<tr>
<td >SetSafeModeAvgTime </td>
<td >ms </td>
<td >	Average latency of SetSafeMode requests</td>
</tr>	
<tr>
<td >MkdirsAvgTime </td>
<td >ms </td>
<td >	Average latency of Mkdirs requests</td>
</tr>	
<tr>
<td >GetServerDefaultsAvgTime </td>
<td >ms </td>
<td >	Average latency of GetServerDefaults requests</td>
</tr>	
<tr>
<td >GetBlockLocationsAvgTime </td>
<td >ms </td>
<td >	Average latency of GetBlockLocations requests</td>
</tr>	
<tr>
<td rowspan=7>RPC statistics (1)</td>
<td >CompleteNumOps </td>
<td >count/s</td>
<td >	Number of Complete calls per second</td>
</tr>			
<tr>
<td >CreateNumOps </td>
<td >count/s</td>
<td >	Number of Create calls per second</td>
</tr>		
<tr>
<td >RenameNumOps </td>
<td >count/s</td>
<td >	Number of Rename calls per second</td>
</tr>	
<tr>
<td >AddBlockNumOps </td>
<td >count/s</td>
<td >	Number of AddBlock calls per second</td>
</tr>	
<tr>
<td >GetListingNumOps </td>
<td >count/s</td>
<td >	Number of GetListing calls per second</td>
</tr>	
<tr>
<td >GetFileInfoNumOps </td>
<td >count/s</td>
<td >Number of GetFileInfo calls per second</td>
</tr>	
<tr>
<td >SendHeartbeatNumOps </td>
<td >count/s</td>
<td >	Number of SendHeartbeat calls per second</td>
</tr>	
<tr>
<td rowspan=7>RPC statistics (2)</td>
<td >RegisterDatanodeNumOps </td>
<td >count/s</td>
<td >	Number of RegisterDatanode calls per second</td>
</tr>			
<tr>
<td >BlockReportNumOps </td>
<td >count/s</td>
<td >	Number of BlockReport calls per second</td>
</tr>		
<tr>
<td >DeleteNumOps </td>
<td >count/s</td>
<td >	Number of Delete calls per second</td>
</tr>	
<tr>
<td >RenewLeaseNumOps </td>
<td >count/s</td>
<td >	Number of RenewLease calls per second</td>
</tr>	
<tr>
<td >BlockReceivedAndDeletedNumOps </td>
<td >count/s</td>
<td >	Number of BlockReceivedAndDeleted calls per second</td>
</tr>	
<tr>
<td >FsyncNumOps </td>
<td >count/s</td>
<td >	Number of fsync calls per second</td>
</tr>	
<tr>
<td >VersionRequestNumOps </td>
<td >count/s</td>
<td >Number of VersionRequest calls per second</td>
</tr>	
<tr>
<td rowspan=7>RPC statistics (3)</td>
<td >ListEncryptionZonesNumOps </td>
<td >count/s</td>
<td >	Number of ListEncryptionZones calls per second</td>
</tr>			
<tr>
<td >SetPermissionNumOps </td>
<td >count/s</td>
<td >	Number of SetPermission calls per second</td>
</tr>		
<tr>
<td >SetTimesNumOps </td>
<td >count/s</td>
<td >	Number of SetTimes calls per second</td>
</tr>	
<tr>
<td >SetSafeModeNumOps </td>
<td >count/s</td>
<td >	Number of SetSafeMode calls per second</td>
</tr>	
<tr>
<td >MkdirsNumOps </td>
<td >count/s</td>
<td >	Number of Mkdirs calls per second</td>
</tr>	
<tr>
<td >GetServerDefaultsNumOps </td>
<td >count/s</td>
<td >	Number of GetServerDefaults calls per second</td>
</tr>	
<tr>
<td >GetBlockLocationsNumOps </td>
<td >count/s</td>
<td >Number of GetBlockLocations calls per second</td>
</tr>	
</table>

### HDFS - DataNode
<table>
<tr>
<th width=18%>Title</th>
<th width=20%>Metric</th>
<th width=12%>Unit</th>
<th width=50%>Description</th>
</tr><tr>
<td >Xceivers</td>
<td >XceiverCount </td>
<td > - </td>
<td >Number of Xceivers</td>
</tr><tr>
<td rowspan=4>Data read/write rate</td>
<td >BytesWrittenMB</td>
<td >Bytes/s </td>
<td >DataNode byte write rate</td>
</tr><tr>
<td >BytesReadMB</td>
<td >Bytes/s </td>
<td >DataNode byte read rate</td>
</tr><tr>
<td >RemoteBytesReadMB </td>
<td >Bytes/s </td>
<td >Remote client byte read rate</td>
</tr><tr>
<td >RemoteBytesWrittenMB </td>
<td >Bytes/s </td>
<td >Remote client byte write rate</td>
</tr><tr>
 <td  rowspan=4>Client connections</td>
<td >WritesFromRemoteClient </td>
<td > - </td>
<td >Remote client write QPS</td>
</tr><tr>
<td >WritesFromLocalClient </td>
<td > - </td>
<td >Local client write QPS</td>
</tr><tr>
<td >ReadsFromRemoteClient </td>
<td > - </td>
<td >Remote client read QPS</td>
</tr><tr>
<td >ReadsFromLocalClient </td>
<td > - </td>
<td >Local client read QPS</td>
</tr><tr>
<td >Block verification failure</td>
<td >BlockVerificationFailures </td>
<td >count/s</td>
<td >Number of block verification failures</td>
</tr><tr>
<td >Disk failure</td>
<td >VolumeFailures </td>
<td >count/s</td>
<td >Number of disk failures</td>
</tr><tr>
<td >Network error</td>
<td >DatanodeNetworkErrors </td>
<td >count/s</td>
<td >Network error statistics</td>
</tr><tr>
<td >Heartbeat latency</td>
<td >HeartbeatsAvgTime </td>
<td >ms </td>
<td >Average heartbeat time</td>
</tr><tr>
<td >Heartbeat QPS</td>
<td >HeartbeatsNumOps </td>
<td >count/s</td>
<td >Heartbeat QPS</td>
</tr><tr>
<td >Packet transfer RT</td>
<td >SendDataPacketTransferNanosAvgTime </td>
<td >ms </td>
<td >Average time of sending packets</td>
</tr><tr>
<td rowspan=9>Block operation</td>
<td >ReadBlockOpNumOps </td>
<td >count/s</td>
<td >Block read OPS from DataNode</td>
</tr><tr>
<td >WriteBlockOpNumOps </td>
<td >count/s</td>
<td >Block write OPS to DataNode</td>
</tr><tr>
<td >BlockChecksumOpNumOps </td>
<td >count/s</td>
<td >Checksum OPS by DataNode</td>
</tr><tr>
<td >CopyBlockOpNumOps </td>
<td >count/s</td>
<td >Block copying OPS</td>
</tr><tr>
<td >ReplaceBlockOpNumOps </td>
<td >count/s</td>
<td >Block replacement OPS</td>
</tr><tr>
<td >BlockReportsNumOps </td>
<td >count/s</td>
<td >Block reporting OPS</td>
</tr><tr>
<td >IncrementalBlockReportsNumOps </td>
<td >count/s</td>
<td >Incremental block reporting OPS</td>
</tr><tr>
<td >CacheReportsNumOps </td>
<td >count/s</td>
<td >Cache reporting OPS</td>
</tr><tr>
<td >PacketAckRoundTripTimeNanosNumOps </td>
<td >count/s</td>
<td >Number of ACK round trips processed per second</td>
</tr><tr>	
<td >Fsync operation</td>
<td >FsyncNanosNumOps </td>
<td >count/s</td>
<td >Number of fsync operations processed per second</td>
</tr><tr>
<td >Flush operation</td>
<td >FlushNanosNumOps </td>
<td >count/s</td>
<td >Number of flush operations processed per second</td>
</tr><tr>
<td rowspan=9>Block operation latency statistics</td>
<td >ReadBlockOpAvgTime </td>
<td >ms </td>
<td >Average block read time</td>
</tr><tr>
<td >WriteBlockOpAvgTime </td>
<td >ms </td>
<td >Average block write time</td>
</tr><tr>
<td >BlockChecksumOpAvgTime </td>
<td >ms </td>
<td >Average block check time</td>
</tr><tr>
<td >CopyBlockOpAvgTime </td>
<td >ms </td>
<td >Average block copy time</td>
</tr><tr>
<td >ReplaceBlockOpAvgTime </td>
<td >ms </td>
<td >Average block replacement time</td>
</tr><tr>
<td >BlockReportsAvgTime </td>
<td >ms </td>
<td >Average block reporting time</td>
</tr><tr>
<td >IncrementalBlockReportsAvgTime </td>
<td >ms </td>
<td >Average time of incremental block reporting</td>
</tr><tr>
<td >CacheReportsAvgTime </td>
<td >ms </td>
<td >Average time of cache reporting</td>
</tr><tr>
<td >PacketAckRoundTripTimeNanosAvgTime </td>
<td >ms </td>
<td >Average time of ACK round trip processing</td>
</tr><tr>
<td >Flush latency</td>
<td >FlushNanosAvgTime </td>
<td >ms </td>
<td >Average flush time</td>
</tr><tr>
<td >Fsync latency</td>
<td >FsyncNanosAvgTime </td>
<td >ms </td>
<td >Average fsync time</td>
</tr><tr>
<td rowspan=8>RamDisk Blocks </td>
<td >RamDiskBlocksWrite </td>
<td >blocks/s </td>
<td >Total number of blocks written to memory</td>
</tr><tr>
<td >RamDiskBlocksWriteFallback </td>
<td >blocks/s </td>
<td >Total number of blocks failed to be written to memory (failover to disk)</td>
</tr><tr>
<td >RamDiskBlocksDeletedBeforeLazyPersisted</td>
<td >blocks/s </td>
<td >Total number of blocks deleted before the application is saved to the disk</td>
</tr><tr>
<td >RamDiskBlocksReadHits </td>
<td >blocks/s </td>
<td >Number of blocks read from memory</td>
</tr><tr>
<td >RamDiskBlocksEvicted </td>
<td >blocks/s </td>
<td >Total number of blocks cleared in memory</td>
</tr><tr>
<td >RamDiskBlocksEvictedWithoutRead </td>
<td >blocks/s </td>
<td >Total number of blocks retrieved from memory</td>
</tr><tr>
<td >RamDiskBlocksLazyPersisted </td>
<td >blocks/s </td>
<td >Number of disk writes by lazy writer</td>
</tr><tr>
<td >RamDiskBytesLazyPersisted </td>
<td >Bytes/s </td>
<td >Total number of bytes written to disk by lazy writer</td>
</tr><tr>
<td >RamDisk write speed</td>
<td >RamDiskBytesWrite </td>
<td >Bytes/s </td>
<td >Total number of bytes written to memory</td>
</tr><tr>
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapCommittedM configured by JVM</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Committed size of JVM HeapMemory</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB</td>
<td >Maximum size of memory available to JVM runtime</td>
</tr><tr>
<td rowspan=6>JVM threads</td>
<td >ThreadsNew </td>
<td > - </td>
<td >Number of threads in NEW status</td>
</tr><tr>
<td >ThreadsRunnable </td>
<td > - </td>
<td >Number of threads in RUNNABLE status</td>
</tr><tr>
<td >ThreadsBlocked </td>
<td > - </td>
<td >Number of threads in BLOCKED status</td>
</tr><tr>
<td >ThreadsWaiting </td>
<td > - </td>
<td >Number of threads in WAITING status</td>
</tr><tr>
<td >ThreadsTimedWaiting </td>
<td > - </td>
<td >Number of threads in TIMED WAITING status</td>
</tr><tr>
<td >ThreadsTerminated </td>
<td > - </td>
<td >Number of threads in Terminated status</td>
</tr><tr>
<td  rowspan=4>JVM logs</td>
<td >LogFatal </td>
<td > - </td>
<td >Number of Fatal logs</td>
</tr><tr>
<td >LogError </td>
<td > - </td>
<td >Number of Error logs</td>
</tr><tr>
<td >LogWarn </td>
<td > - </td>
<td >Number of Warn logs</td>
</tr><tr>
<td >LogInfo </td>
<td > - </td>
<td >Number of Info logs</td>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td rowspan=2>Data traffic</td>
<td >ReceivedBytes </td>
<td >Bytes/s </td>
<td >Data receiving rate</td>
</tr><tr>
<td >SentBytes </td>
<td >Bytes/s </td>
<td >Data sending rate</td>
</tr><tr>
<td >QPS </td>
<td >RpcQueueTimeNumOps </td>
<td >count/s</td>
<td >RPC call rate</td>
</tr><tr>
<td rowspan=2>Request processing latency</td>
<td >RpcQueueTimeAvgTime </td>
<td >ms </td>
<td >Average RPC latency</td>
</tr><tr>
<td >RpcProcessingTimeAvgTime </td>
<td >count/s</td>
<td >Average RPC request processing time</td>
</tr><tr>
<td rowspan=4>Authentication and authorization</td>
<td >RpcAuthenticationFailures </td>
<td >count/s</td>
<td >Number of RPC authentication failures</td>
</tr><tr>
<td >RpcAuthenticationSuccesses </td>
<td >count/s</td>
<td >Number of RPC authentication successes</td>
</tr><tr>
<td >RpcAuthorizationFailures </td>
<td >count/s</td>
<td >Number of RPC authorization failures</td>
</tr><tr>
<td >RpcAuthorizationSuccesses </td>
<td >count/s</td>
<td >Number of RPC authorization successes</td>
</tr><tr>
<td >Current connections</td>
<td >NumOpenConnections </td>
<td > - </td>
<td >Number of current connections</td>
</tr><tr>
<td >Length of RPC processing queue</td>
<td >CallQueueLength </td>
<td >1 </td>
<td >Length of current RPC processing queue</td>
</tr><tr>
<td rowspan=2>CPU time</td>
<td >CurrentThreadSystemTime </td>
<td >ms </td>
<td >System time</td>
</tr><tr>
<td >CurrentThreadUserTime </td>
<td >ms </td>
<td >User time</td>
</tr><tr>
<td >Start time</td>
<td >StartTime </td>
<td >s</td>
<td >Process start time</td>
</tr><tr>
<td rowspan=2>Threads</td>
<td >PeckThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >DaemonThreadCount </td>
<td > - </td>
<td >Number of backend threads</td>
</tr><tr>
<td rowspan=2>Read/Write latency</td>
<td >write </td>
<td >ms </td>
<td >Write time</td>
</tr><tr>
<td >read </td>
<td >ms </td>
<td >Read time</td>
</tr><tr>
<td >Packet transfer QPS</td>
<td >DataPacketOps </td>
<td >count/s</td>
<td >Packet transfer QPS</td>
</tr>
<tr>
<td >Blocks</td>
<td >Related to disk information, such as `/data/qcloud/data/hdfs`</td>
<td >-</td>
<td >Blocks</td>
</tr><tr>
<td >Used disk capacity</td>
<td >Related to disk information, such as `/data/qcloud/data/hdfs`</td>
<td >GB</td>
<td >Used disk capacity</td>
</tr><tr>
<td >Free disk capacity</td>
<td >Related to disk information, such as `/data/qcloud/data/hdfs`</td>
<td >GB</td>
<td >Free disk capacity</td>
</tr><tr>
<td >Reserved disk capacity</td>
<td >Related to disk information, such as `/data/qcloud/data/hdfs`</td>
<td >GB</td>
<td >Reserved disk capacity</td>
</tr>			
</table>
			
### HDFS - JournalNode
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=50%>Description</th>
</tr><tr>
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapCommittedM configured by JVM</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Committed size of JVM HeapMemory</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB</td>
<td >Maximum size of memory available to JVM runtime</td>
</tr><tr>
<td rowspan=6>JVM threads</td>
<td >ThreadsNew </td>
<td > - </td>
<td >Number of threads in NEW status</td>
</tr><tr>
<td >ThreadsRunnable </td>
<td > - </td>
<td >Number of threads in RUNNABLE status</td>
</tr><tr>
<td >ThreadsBlocked </td>
<td > - </td>
<td >Number of threads in BLOCKED status</td>
</tr><tr>
<td >ThreadsWaiting </td>
<td > - </td>
<td >Number of threads in WAITING status</td>
</tr><tr>
<td >ThreadsTimedWaiting </td>
<td > - </td>
<td >Number of threads in TIMED WAITING status</td>
</tr><tr>
<td >ThreadsTerminated </td>
<td > - </td>
<td >Number of threads in Terminated status</td>
</tr><tr>
<td rowspan=4>JVM logs</td>
<td >LogFatal </td>
<td > - </td>
<td >Number of FATAL-level logs</td>
</tr><tr>
<td >LogError </td>
<td > - </td>
<td >Number of ERROR-level logs</td>
</tr><tr>
<td >LogWarn </td>
<td > - </td>
<td >Number of WARN-level logs</td>
</tr><tr>
<td >LogInfo </td>
<td > - </td>
<td >Number of INFO-level logs</td>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td rowspan=2>Data traffic</td>
<td >ReceivedBytes </td>
<td >Bytes/s </td>
<td >Data receiving rate</td>
</tr><tr>
<td >SentBytes </td>
<td >Bytes/s </td>
<td >Data sending rate</td>
</tr><tr>
<td >Request processing latency</td>
<td >RpcQueueTimeAvgTime </td>
<td >ms </td>
<td >Average RPC latency</td>
</tr><tr>
<td rowspan=4>Authentication and authorization</td>
<td >RpcAuthenticationFailures </td>
<td >count/s</td>
<td >Number of RPC authentication failures</td>
</tr><tr>
<td >RpcAuthenticationSuccesses </td>
<td >count/s</td>
<td >Number of RPC authentication successes</td>
</tr><tr>
<td >RpcAuthorizationFailures </td>
<td >count/s</td>
<td >Number of RPC authorization failures</td>
</tr><tr>
<td >RpcAuthorizationSuccesses </td>
<td >count/s</td>
<td >Number of RPC authorization successes</td>
</tr><tr>
<td >Current connections</td>
<td >NumOpenConnections </td>
<td > - </td>
<td >Number of current connections</td>
</tr><tr>
<td >Length of RPC processing queue</td>
<td >CallQueueLength </td>
<td >1 </td>
<td >Length of current RPC processing queue</td>
</tr><tr>
<td rowspan=2>CPU time</td>
<td >CurrentThreadSystemTime </td>
<td >ms </td>
<td >System time</td>
</tr><tr>
<td >CurrentThreadUserTime </td>
<td >ms </td>
<td >User time</td>
</tr><tr>
<td >Start time</td>
<td >StartTime </td>
<td >s</td>
<td >Process start time</td>
</tr><tr>
<td rowspan=2>Threads</td>
<td >PeckThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >DaemonThreadCount </td>
<td > - </td>
<td >Number of backend threads</td>
</tr>
</table>

### HDFS - ZKFC
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=50%>Description</th>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr>
</table>

### HDFS-Router
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=50%>Description</th>
</tr><tr>
<td>ALTER TABLE request duration</td>
<td>HIVE.HMS.API_ALTER_TABLE</td>
<td>ms</td>
<td>Average duration of ALTER TABLE requests</td>
</tr>
<tr>
<td>ALTER TABLE WITH ENV CONTEXT request duration</td>
<td>HIVE.HMS.API_ALTER_TABLE_WITH_ENV_CONTEXT</td>
<td>ms</td>
<td>Average duration of ALTER TABLE WITH ENV CONTEXT requests</td>
</tr>
<tr>
<td>CREATE TABLE request duration</td>
<td>HIVE.HMS.API_CREATE_TABLE</td>
<td>ms</td>
<td>Average duration of CREATE TABLE requests</td>
</tr>
<tr>
<td>CREATE TABLE WITH ENV CONTEXT request duration</td>
<td>HIVE.HMS.API_CREATE_TABLE_WITH_ENV_CONTEXT</td>
<td>ms</td>
<td>Average duration of CREATE TABLE WITH ENV CONTEXT requests</td>
</tr>
<tr>
<td>DROP TABLE request duration</td>
<td>HIVE.HMS.API_DROP_TABLE</td>
<td>ms</td>
<td>Average duration of DROP TABLE requests</td>
</tr>
<tr>
<td>DROP TABLE WITH ENV CONTEXT request duration</td>
<td>HIVE.HMS.API_DROP_TABLE_WITH_ENV_CONTEXT</td>
<td>ms</td>
<td>Average duration of DROP TABLE WITH ENV CONTEXT requests</td>
</tr>
<tr>
<td>GET TABLE request duration</td>
<td>HIVE.HMS.API_GET_TABLE</td>
<td>ms</td>
<td>Average duration of GET TABLE requests</td>
</tr>
<tr>
<td>GET TABLES request duration</td>
<td>HIVE.HMS.API_GET_TABLES</td>
<td>ms</td>
<td>Average duration of GET TABLES requests</td>
</tr>
<tr>
<td>GET MULTI TABLE request duration</td>
<td>HIVE.HMS.API_GET_MULTI_TABLE</td>
<td>ms</td>
<td>Average duration of GET MULTI TABLE requests</td>
</tr>
<tr>
<td>GET TABLE REQ request duration</td>
<td>HIVE.HMS.API_GET_TABLE_REQ</td>
<td>ms</td>
<td>Average duration of GET TABLE REQ requests</td>
</tr>
<tr>
<td>GET DATABASE request duration</td>
<td>HIVE.HMS.API_GET_DATABASE</td>
<td>ms</td>
<td>Average duration of GET DATABASE requests</td>
</tr>
<tr>
<td>GET DATABASES request duration</td>
<td>HIVE.HMS.API_GET_DATABASES</td>
<td>ms</td>
<td>Average duration of GET DATABASES requests</td>
</tr>
<tr>
<td>GET ALL DATABASES request duration</td>
<td>HIVE.HMS.API_GET_ALL_DATABASES</td>
<td>ms</td>
<td>Average duration of GET ALL DATABASES requests</td>
</tr>
<tr>
<td>GET ALL FUNCTIONS request duration</td>
<td>HIVE.HMS.API_GET_ALL_FUNCTIONS</td>
<td>ms</td>
<td>Average duration of GET ALL FUNCTIONS requests</td>
</tr>
<tr>
<td>Current number of active CREATE TABLE requests</td>
<td>HIVE.HMS.ACTIVE_CALLS_API_CREATE_TABLE</td>
<td>-</td>
<td>Current number of active CREATE TABLE requests</td>
</tr>
<tr>
<td>Current number of active DROP TABLE requests</td>
<td>HIVE.HMS.ACTIVE_CALLS_API_DROP_TABLE</td>
<td>-</td>
<td>Current number of active DROP TABLE requests</td>
</tr>
<tr>
<td>Current number of active ALTER TABLE requests</td>
<td>HIVE.HMS.ACTIVE_CALLS_API_ALTER_TABLE</td>
<td>-</td>
<td>Current number of active ALTER TABLE requests</td>
</tr>
</tbody></table>
