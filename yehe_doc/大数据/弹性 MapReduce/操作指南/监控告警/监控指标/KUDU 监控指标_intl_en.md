| Metric Name | Unit | Description |
| ----------------------------- | ----- | ------------------------------------------------------------ |
| BlockCacheHit | - | Number of block cache hits. When the cache efficiency is confirmed, use the value of this metric instead of that of cache_hits. |
| BlockCacheMiss  | - | Number of block cache misses. When the cache efficiency is confirmed, use the value of this metric instead of that of cache_misses. |
| ActiveScanners | - | Number of active scanners |
| ExpiredScanners | - | Number of expired scanners |
| OpenClientSessions | - | Number of opened sessions of tablet copying client on the server  |
| OpemSourceSessions | - | Number of opened sessions of tablet copying source on the server |
| TabletBootstrapping | - | Number of bootstrapping tablets |
| TabletFailed | - | Number of failed tablets |
| TabletInitialized | - | Number of initialized tablets |
| TabletNotInitialized | - | Number of uninitialized tablets |
| TabletRunning | - | Number of running tablets or threads |
| TabletShutdown  | - | Number of tablets shut down |
| TabletStopped | - | Number of stopped tablets |
| TabletStopping | - | Number of stopping tablets |
| TotalCount | - | Total number of operations |
| Min | s | Minimum number of waiting tasks, minimum running time, minimum waiting time, or minimum processing time in the queue  |
| Max | s | Maximum number of waiting tasks, maximum running time, maximum waiting time, or maximum processing time in the queue |
| Mean | s | Average number of waiting tasks, average running time, average waiting time, or average processing time in the queue  |
| Percentile_99_9 | s | 99.9th percentile value of waiting tasks, 99.9th percentile value of running time, 99.9th percentile value of waiting time, or 99.9th percentile value of processing time in the queue |
| BlockCacheUsage | Bytes | Memory occupied by block cache |
| FileCacheHit | - | Number of file descriptor cache hits. When the cache efficiency is confirmed, use the value of this metric instead of that of cache_hits. |
| FileCacheMiss | - | Number of file descriptor cache misses. When the cache efficiency is confirmed, use the value of this metric instead of that of cache_misses. |
| FileCacheUsage  | - | Number of file cache entries |
| BlockUnderManagement | - | Number of data blocks under management |
| BlockOpenReading | - | Number of data blocks open for reading |
| BlockOpenWriting | - | Number of data blocks open for writing |
| BytesUnderManagement | Bytes | Number of bytes of data blocks under management |
| ContainersUnderManagement | - | Number of log block containers |
| FullContainersUnderManagement | - | Number of full log block containers |
| CpuStime | ms  | Total system CPU time used by processes |
| CpuUtime | ms  | Total user CPU time used by processes |
| DataDirsFailed | - | Number of data directories in a failed disk |
| DataDirsFull | - | Number of data directories in a full disk |
| AllocatedBytes | - | Number of bytes used by applications. This usually does not match the memory usage reported by the operating system because it does not include TCMalloc overhead or memory fragments. |
| ErrorMessages | - | Number of ERROR log messages sent by applications |
| WarningMessages | - | Number of WARNING log messages send by applications |
| InvoluntarySwitches | - | Number of involuntary context switches |
| VoluntarySwitches | - | Number of voluntary context switches |
| SpinlockContentionTime | ms | Time consumed by internal spinlock contention since the server starts |
| OversizedWriteRequests | - | Number of oversize write requests for system catalog tablet rejected after startup |
| HybridClockError | ms | Biggest server clock error. `2^64-1` is returned when the basic clock cannot be read. |
| HybridClockTimestamp | ms | Hybrid clock timestamp. `2^64-1` is returned when the basic clock cannot be read. |
| ClusterReplicaSkew | - | Difference between the number of replicas on the tablet server hosting the most replicas and the number of replicas on the tablet server hosting the fewest replicas |
| NumRaftLeaders | - | Number of raft leader replicas on the tablet  |
| HeapSize | Bytes | System memory reserved by TCMalloc |
| CurrentThreadCacheBytes  | Bytes | Memory measure used by TCMalloc for small objects |
| TotalThreadCacheBytes | Bytes | Memory limit used by TCMalloc for small objects |
| FreeBytes | Bytes | Number of bytes of the available mapped pages in the page heap |
| UnMappedBytes | Bytes | Number of bytes of the available unmapped pages in the page heap  |
| ConnectionsAccepted | - | Number TCP connections to RPC servers |
| QueueOverflow | - | Number of RPCs dropped because the service queue is full |
| TimesOutInQueue | - | Number of unprocessed RPCs because they times out while waiting in the service queue |
| ThreadsRunning | - | Number of threads currently running in all tablet servers or number of threads currently running in all master servers |
