### Kudu - overview
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td >Tablets</td>
<td>TabletRunning</td>
<td>-</td>
<td>Total number of tablets currently running on all tablet servers</td>
</tr><tr>
<td >Difference in the number of tablet replicas</td>
<td>ClusterReplicaSkew</td>
<td>-</td>
<td>Difference between the number of replicas on the tablet server hosting the most replicas and the number of replicas on the tablet server hosting the fewest replicas</td>
</tr><tr>
<td >TServer threads</td>
<td>ThreadsRunning</td>
<td>-</td>
<td>	Number of threads currently running on all tablet servers</td>
</tr><tr>
<td >Master threads</td>
<td>ThreadsRunning</td>
<td>-</td>
<td>	Number of threads currently running on all masters</td>
</tr><tr>
<td >TServer logs</td>
<td>ErrorMessages</td>
<td>-</td>
<td>	Number of ERROR-level log messages emitted in all processes</td>
</tr><tr>
<td rowspan=2>Master logs</td>
<td>ErrorMessages</td>
<td>-</td>
<td>Number of ERROR-level log messages emitted in all processes</td>
</tr><tr>
<td>WarningMessages</td>
<td>-</td>
<td>Number of WARNING-level log messages emitted in all processes</td>
</tr><tr>
<td>Oversized write requests</td>
<td>OversizedWriteRequests</td>
<td>-</td>
<td>Number of oversized write requests to the system catalog tablet rejected by the master since start</td>
</tr>
</table>

### Kudu - server
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>Block cache hit</td>
<td >BlockCacheHit</td>
<td >-</td>
<td >Number of block cache hits. When confirming the cache efficiency, use the value of this metric instead of that of cache_hits</td>
</tr><tr>
<td >BlockCacheMiss</td>
<td >-</td>
<td >Number of block cache misses. When confirming the cache efficiency, use the value of this metric instead of that of cache_misses</td>
</tr><tr>
<td >Block cache utilization</td>
<td >BlockCacheUsage</td>
<td >bytes</td>
<td >Memory used by block cache</td>
</tr><tr>
<td rowspan=2>File cache hit</td>
<td >FileCacheHit</td>
<td >-</td>
<td >Number of file descriptor cache hits. When confirming the cache efficiency, use the value of this metric instead of that of cache_hits</td>
</tr><tr>
<td >FileCacheMiss</td>
<td >-</td>
<td >Number of file descriptor cache misses. When confirming the cache efficiency, use the value of this metric instead of that of cache_misses</td>
</tr><tr>
<td >File cache utilization</td>
<td >FileCacheUsage</td>
<td >-</td>
<td >Number of entries file cache</td>
</tr><tr>
<td rowspan=2>Scanner</td>
<td >ActiveScanners</td>
<td >-</td>
<td >Number of currently active scanners</td>
</tr><tr>
<td >ExpiredScanners</td>
<td >-</td>
<td >Number of scanners that have expired due to inactivity since service start</td>
</tr><tr>
<td rowspan=3>Block manager blocks</td>
<td >BlockUnderManagement</td>
<td >-</td>
<td >Number of currently managed data blocks</td>
</tr><tr>
<td >BlockOpenReading</td>
<td >-</td>
<td >Number of data blocks currently opened for read</td>
</tr><tr>
<td >BlockOpenWriting</td>
<td >-</td>
<td >Number of data blocks currently opened for write</td>
</tr><tr>
<td >Block manager bytes</td>
<td >BytesUnderManagement</td>
<td >bytes</td>
<td >Number of bytes of currently managed data blocks</td>
</tr><tr>
<td rowspan=2>Block manager containers</td>
<td >ContainersUnderManagement</td>
<td >-</td>
<td >Number of log block containers</td>
</tr><tr>
<td >FullContainersUnderManagement</td>
<td >-</td>
<td >Number of full log block containers</td>
</tr><tr>
<td >Tablet leaders</td>
<td >NumRaftLeaders</td>
<td >-</td>
<td >Number of tablet replicas that are Raft leaders</td>
</tr><tr>
<td rowspan=2>Tablet sessions</td>
<td >OpenClientSessions</td>
<td >-</td>
<td >Number of currently opened tablet copy client sessions on this server</td>
</tr><tr>
<td >OpemSourceSessions</td>
<td >-</td>
<td >Number of currently opened tablet copy source sessions on this server</td>
</tr><tr>
<td rowspan=8>Tablets</td>
<td >TabletBootstrapping</td>
<td >-</td>
<td >Number of currently bootstrapping tablets</td>
</tr><tr>
<td >TabletFailed</td>
<td >-</td>
<td >Number of failed tablets</td>
</tr><tr>
<td >TabletInitialized</td>
<td >-</td>
<td >Number of currently initialized tablets</td>
</tr><tr>
<td >TabletNotInitialized</td>
<td >-</td>
<td > Number of currently uninitialized tablets </td>
</tr><tr>
<td >TabletRunning</td>
<td >-</td>
<td >Number of currently running tablets/Number of currently running threads</td>
</tr><tr>
<td >TabletShutdown</td>
<td >-</td>
<td >Number of currently shut down tablets</td>
</tr><tr>
<td >TabletStopped</td>
<td >-</td>
<td >Number of currently stopped tablets</td>
</tr><tr>
<td >TabletStopping</td>
<td >-</td>
<td >Number of currently stopping tablets</td>
</tr><tr>
<td rowspan=2>CPU time</td>
<td >CpuStime</td>
<td >ms</td>
<td >Total system CPU time of process</td>
</tr><tr>
<td >CpuUtime</td>
<td >ms</td>
<td >Total user CPU time of process</td>
</tr><tr>
<td rowspan=2>Data path</td>
<td >DataDirsFailed</td>
<td >-</td>
<td >Number of data directories whose disks are currently in failed status</td>
</tr><tr>
<td >DataDirsFull</td>
<td >-</td>
<td >Number of data directories whose disks are currently full</td>
</tr><tr>
<td >Thread</td>
<td >ThreadsRunning</td>
<td >-</td>
<td >Number of currently running threads</td>
</tr><tr>
<td rowspan=2>Context</td>
<td >InvoluntarySwitches</td>
<td >-</td>
<td >Total involuntary context switches</td>
</tr><tr>
<td >VoluntarySwitches</td>
<td >-</td>
<td >Total voluntary context switches</td>
</tr><tr>
<td >Spinlock</td>
<td >SpinlockContentionTime</td>
<td >μs</td>
<td >Amount of time consumed by contention on internal spinlocks since server start</td>
</tr><tr>
<td rowspan=2>Log information</td>
<td >ErrorMessages</td>
<td >-</td>
<td >Number of ERROR-level log messages emitted by the application</td>
</tr><tr>
<td >WarningMessages</td>
<td >-</td>
<td >Number of WARNING-level log messages emitted by the application</td>
</tr><tr>
<td rowspan=5>Operations in queue</td>
<td >TotalCount</td>
<td >-</td>
<td >Total number</td>
</tr><tr>
<td >Min</td>
<td >-</td>
<td >Minimum number of tasks waiting in the queue</td>
</tr><tr>
<td >Max</td>
<td >-</td>
<td >Maximum number of tasks waiting in the queue</td>
</tr><tr>
<td >Mean</td>
<td >-</td>
<td >Average number of tasks waiting in the queue</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >-</td>
<td >99.9th percentile of the number of tasks waiting in the queue</td>
</tr><tr>
<td rowspan=5>Operation execution duration</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum run time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum run time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average run time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the run time</td>
</tr><tr>
<td rowspan=5>Queuing wait time</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum wait time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum wait time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average wait time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the wait time</td>
</tr><tr>
<td >Allocated bytes</td>
<td >AllocatedBytes</td>
<td >bytes</td>
<td >Number of bytes used by applications. This usually does not match the memory usage reported by the operating system because it does not include TCMalloc overhead or memory fragments</td>
</tr><tr>
<td >Hybrid clock error</td>
<td >HybridClockError</td>
<td >μs</td>
<td >Server clock maximum error; returns 2^64-1 when unable to read the base clock</td>
</tr><tr>
<td >Hybrid clock timestamp</td>
<td >HybridClockTimestamp</td>
<td >μs</td>
<td >Hybrid clock timestamp; returns 2^64-1 when unable to read the base clock</td>
</tr><tr>			
<td rowspan=3>TCMalloc memory</td>
<td >HeapSize</td>
<td >bytes</td>
<td >Bytes of system memory reserved by TCMalloc</td>
</tr><tr>			
<td >CurrentThreadCacheBytes</td>
<td >bytes</td>
<td >	A measure of some of the memory TCMalloc is using (for small objects)</td>
</tr><tr>			
<td >TotalThreadCacheBytes</td>
<td >bytes</td>
<td >	A limit to how much memory TCMalloc dedicates for small objects</td>
</tr><tr>		
<td rowspan=2>TCMalloc PageHeap</td>
<td >FreeBytes</td>
<td >bytes</td>
<td >Number of bytes of free mapped pages in the page heap</td>
</tr><tr>				
<td >UnMappedBytes</td>
<td >bytes</td>
<td >Number of bytes of free unmapped pages in the page heap</td>
</tr><tr>			
<td rowspan=3>RPC request</td>
<td >ConnectionsAccepted</td>
<td >-</td>
<td >Number of incoming TCP connections made to the RPC server</td>
</tr><tr>				
<td >QueueOverflow</td>
<td >-</td>
<td >Number of RPCs dropped because the service queue was full</td>
</tr><tr>			
<td >TimesOutInQueue</td>
<td >-</td>
<td >Number of RPCs that timed out while waiting in the service queue and thus were not processed</td>
</tr><tr>			
<td rowspan=5>RPC FetchData</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC AlterSchema</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC CreateTablet</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC DeleteTablet</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC Quiesce</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC scan</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC ScannerKeepAlive</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC write</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td >Write requests rejected due to queue overloading</td>
<td >QueueOverloadRejections</td>
<td >count</td>
<td >Number of write requests rejected due to queue overloading</td>
</tr><tr>
<td rowspan=2>Scan rate</td>
<td >ScannedFromDiskRate</td>
<td >bytes/s</td>
<td >Amount of data scanned per second</td>
</tr><tr>
<td >ScannerReturnedRate</td>
<td >bytes/s</td>
<td >Amount of data returned per second</td>
</tr><tr>			
<td rowspan=2>Scanner bytes</td>
<td >ScannedFromDisk</td>
<td >bytes</td>
<td >Total amount of data scanned from disk</td>
</tr><tr>
<td >ScannerReturned</td>
<td >bytes</td>
<td >Total amount of returned data</td>
</tr><tr>			
<td rowspan=4>Total row operations</td>
<td >RowsInserted</td>
<td >count</td>
<td >Number of rows inserted into the node</td>
</tr><tr>
<td >RowsDeleted</td>
<td >count</td>
<td >Number of rows deleted from the node</td>
</tr><tr>	
<td >RowsUpserted</td>
<td >count</td>
<td >Number of rows upserted into the node</td>
</tr><tr>
<td >RowsUpdated</td>
<td >count</td>
<td >Number of rows updated on the node</td>
</tr><tr>	
<td rowspan=4>Row operation rate</td>
<td >RowsInsertedRate</td>
<td >count/s</td>
<td >Number of rows inserted into the node per second</td>
</tr><tr>
<td >RowsDeletedRate</td>
<td >count/s</td>
<td >Number of rows deleted from the node per second</td>
</tr><tr>	
<td >RowsUpsertedRate</td>
<td >count/s</td>
<td >Number of rows upserted into the node per second</td>
</tr><tr>
<td >RowsUpdatedRate</td>
<td >count/s</td>
<td >Number of rows updated on the node per second</td>	
</tr>
</table>

### Kudu - master
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>Block cache hit</td>
<td >BlockCacheHit</td>
<td >-</td>
<td >Number of block cache hits. When confirming the cache efficiency, use the value of this metric instead of that of cache_hits</td>
</tr><tr>
<td >BlockCacheMiss</td>
<td >-</td>
<td >Number of block cache misses. When confirming the cache efficiency, use the value of this metric instead of that of cache_misses</td>
</tr><tr>
<td >Block cache utilization</td>
<td >BlockCacheUsage</td>
<td >bytes</td>
<td >Memory used by block cache</td>
</tr><tr>
<td rowspan=2>File cache hit</td>
<td >FileCacheHit</td>
<td >-</td>
<td >Number of file descriptor cache hits. When confirming the cache efficiency, use the value of this metric instead of that of cache_hits</td>
</tr><tr>
<td >FileCacheMiss</td>
<td >-</td>
<td >Number of file descriptor cache misses. When confirming the cache efficiency, use the value of this metric instead of that of cache_misses</td>
</tr><tr>
<td >File cache utilization</td>
<td >FileCacheUsage</td>
<td >-</td>
<td >Number of entries file cache</td>
</tr><tr>
<td rowspan=3>Block manager blocks</td>
<td >BlockUnderManagement</td>
<td >-</td>
<td >Number of currently managed data blocks</td>
</tr><tr>
<td >BlockOpenReading</td>
<td >-</td>
<td >Number of data blocks currently opened for read</td>
</tr><tr>
<td >BlockOpenWriting</td>
<td >-</td>
<td >Number of data blocks currently opened for write</td>
</tr><tr>
<td >Block manager bytes</td>
<td >BytesUnderManagement</td>
<td >bytes</td>
<td >Number of bytes of currently managed data blocks</td>
</tr><tr>
<td rowspan=2>Block manager containers</td>
<td >ContainersUnderManagement</td>
<td >-</td>
<td >Number of log block containers</td>
</tr><tr>
<td >FullContainersUnderManagement</td>
<td >-</td>
<td >Number of full log block containers</td>
</tr><tr>
<td rowspan=2>CPU time</td>
<td >CpuStime</td>
<td >ms</td>
<td >Total system CPU time of process</td>
</tr><tr>
<td >CpuUtime</td>
<td >ms</td>
<td >Total user CPU time of process</td>
</tr><tr>
<td >Thread</td>
<td >ThreadsRunning</td>
<td >-</td>
<td >Number of currently running threads</td>
</tr><tr>
<td rowspan=2>Data path</td>
<td >DataDirsFailed</td>
<td >-</td>
<td >Number of data directories whose disks are currently in failed status</td>
</tr><tr>
<td >DataDirsFull</td>
<td >-</td>
<td >Number of data directories whose disks are currently full</td>
</tr><tr>
<td >Allocated bytes</td>
<td >AllocatedBytes</td>
<td >bytes</td>
<td >Number of bytes used by applications. This usually does not match the memory usage reported by the operating system because it does not include TCMalloc overhead or memory fragments</td>
</tr><tr>
<td rowspan=2>Log information</td>
<td >ErrorMessages</td>
<td >-</td>
<td >Number of ERROR-level log messages emitted by the application</td>
</tr><tr>
<td >WarningMessages</td>
<td >-</td>
<td >Number of WARNING-level log messages emitted by the application</td>
</tr><tr>
<td rowspan=2>Context</td>
<td >InvoluntarySwitches</td>
<td >-</td>
<td >Total involuntary context switches</td>
</tr><tr>
<td >VoluntarySwitches</td>
<td >-</td>
<td >Total voluntary context switches</td>
</tr><tr>
<td rowspan=5>Operations in queue</td>
<td >TotalCount</td>
<td >-</td>
<td >Total number</td>
</tr><tr>
<td >Min</td>
<td >-</td>
<td >Minimum number of tasks waiting in the queue</td>
</tr><tr>
<td >Max</td>
<td >-</td>
<td >Maximum number of tasks waiting in the queue</td>
</tr><tr>
<td >Mean</td>
<td >-</td>
<td >Average number of tasks waiting in the queue</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >-</td>
<td >99.9th percentile of the number of tasks waiting in the queue</td>
</tr><tr>
<td rowspan=5>Queuing wait time</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum wait time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum wait time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average wait time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the wait time</td>
</tr><tr>
<td rowspan=5>Operation execution duration</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum run time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum run time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average run time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the run time</td>
</tr><tr>
<td >Spinlock</td>
<td >SpinlockContentionTime</td>
<td >μs</td>
<td >Amount of time consumed by contention on internal spinlocks since server start</td>
</tr><tr>
<td >Oversized write requests</td>
<td >OversizedWriteRequests</td>
<td >-</td>
<td >Number of oversized write requests to the system catalog tablet rejected since start</td>
</tr><tr>
<td >Hybrid clock error</td>
<td >HybridClockError</td>
<td >μs</td>
<td >Server clock maximum error; returns 2^64-1 when unable to read the base clock</td>
</tr><tr>
<td >Hybrid clock timestamp</td>
<td >HybridClockTimestamp</td>
<td >μs</td>
<td >Hybrid clock timestamp; returns 2^64-1 when unable to read the base clock</td>
</tr><tr>
<td >Difference in the number of tablet replicas</td>
<td >ClusterReplicaSkew</td>
<td >-</td>
<td >Difference between the number of replicas on the tablet server hosting the most replicas and the number of replicas on the tablet server hosting the fewest replicas</td>
</tr><tr>
<td >Tablet leaders</td>
<td >NumRaftLeaders</td>
<td >-</td>
<td >Number of tablet replicas that are Raft leaders</td>
</tr><tr>
<td >Tablet sessions</td>
<td >OpemSourceSessions</td>
<td >-</td>
<td >Number of currently opened tablet copy source sessions on this server</td>
</tr><tr>
<td rowspan=3>TCMalloc memory</td>
<td >HeapSize</td>
<td >bytes</td>
<td >Bytes of system memory reserved by TCMalloc</td>
</tr><tr>			
<td >CurrentThreadCacheBytes</td>
<td >bytes</td>
<td >	A measure of some of the memory TCMalloc is using (for small objects)</td>
</tr><tr>			
<td >TotalThreadCacheBytes</td>
<td >bytes</td>
<td >	A limit to how much memory TCMalloc dedicates for small objects</td>
</tr><tr>		
<td rowspan=2>TCMalloc page heap</td>
<td >FreeBytes</td>
<td >bytes</td>
<td >Number of bytes of free mapped pages in the page heap</td>
</tr><tr>				
<td >UnMappedBytes</td>
<td >bytes</td>
<td >Number of bytes of free unmapped pages in the page heap</td>
</tr><tr>			
<td rowspan=3>RPC request</td>
<td >ConnectionsAccepted</td>
<td >-</td>
<td >Number of incoming TCP connections made to the RPC server</td>
</tr><tr>				
<td >QueueOverflow</td>
<td >-</td>
<td >Number of RPCs dropped because the service queue was full</td>
</tr><tr>			
<td >TimesOutInQueue</td>
<td >-</td>
<td >Number of RPCs that timed out while waiting in the service queue and thus were not processed</td>
</tr><tr>			
<td rowspan=5>RPC RunLeaderElection</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC ConnectToMaster</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC Ping</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC TSHeartbeat</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr><tr>
<td rowspan=5>RPC FetchData</td>
<td >TotalCount</td>
<td >μs</td>
<td >Total number of operations</td>
</tr><tr>
<td >Min</td>
<td >μs</td>
<td >Minimum processing time</td>
</tr><tr>
<td >Max</td>
<td >μs</td>
<td >Maximum processing time</td>
</tr><tr>
<td >Mean</td>
<td >μs</td>
<td >Average processing time</td>
</tr><tr>
<td >Percentile_99_9</td>
<td >μs</td>
<td >99.9th percentile of the processing time</td>
</tr>
</table>
