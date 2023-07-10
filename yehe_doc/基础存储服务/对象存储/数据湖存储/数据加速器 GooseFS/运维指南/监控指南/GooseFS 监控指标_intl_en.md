## Monitoring Metrics Overview

GooseFS’s monitoring metrics include the running statuses of clients, clusters, masters, workers, and processes.

1. Monitoring metrics are classified into the following four types based on the statistics dimension:
 - **Gauge**: records the instantaneous values of an event. The values can be up and down and are usually used to monitor the system running status.
 - **Meter**: records event frequency (how many times an event occurs in a fixed period of time) such as the number of requests in 1, 5, or 15 minutes.
 - **Counter**: records how many times an event occurs in total. Compared with Gauge, the value will only go up but not down. It is usually used to record data such as the number of access requests.
 - **Timer**: records the frequency and distribution of an event. This metric is a combination of the Histogram and Meter metrics. Histogram is used to record the time consumption distribution, and Meter is used to record the QPS. If you need statistics on both the frequency and time consumption, you can use the Timer metric.

>!For more metric classifications, please see [Metrics Library](https://metrics.dropwizard.io/3.1.0/getting-started). Currently, GooseFS supports only the four metrics above.
>

2. Monitoring metrics are classified into the following two types based on the data source:
 - **Cluster status metric**: records the monitoring data of the cluster, masters, and workers. These metrics show the running status of the entire cluster and each node. The recording format is as follows:
```plaintext
Master.[metricName].[tag1].[tag2]...
[Worker_ip].[metricName].[tag1].[tag2]...
```
 - **Process metric**: records the number of requests, delay, CPU consumption, and RPC calling times for the cluster. These metrics can be pushed to and displayed on a third-party monitoring tool. The recording format is as follows:
```plaintext
[processType].[metricName].[tag1].[tag2]...[hostName]
```

## Cluster Monitoring Metrics

If a GooseFS cluster is deployed, clients and workers will send the monitoring data to the master periodically through the heartbeat. You can use `goosefs.master.worker.heartbeat.interval` and `goosefs.user.metrics.heartbeat.interval` to set the heartbeat interval of workers and clients, respectively.

Cluster-level monitoring metrics:

| **Metric** | **Type** | **Description** |
| ------------------------------------ | ------------ | ------------------------------------------------------------ |
| Cluster.BytesReadDomain              | COUNTER      | Total number of bytes read from GooseFS storage via domain socket reported by all workers |
| Cluster.BytesReadDomainThroughput    | GAUGE        | Bytes read throughput from GooseFS storage via domain socket by all workers |
| Cluster.BytesReadLocal               | COUNTER      | Total number of bytes short-circuit read from local storage by all clients |
| Cluster.BytesReadLocalThroughput     | GAUGE        | Bytes throughput short-circuit read from local storage by all clients |
| Cluster.BytesReadPerUfs              | COUNTER      | Total number of bytes read from a specific UFS by all workers |
| Cluster.BytesReadRemote              | COUNTER      | Total number of bytes read from GooseFS storage or underlying UFS if data does not exist in GooseFS storage reported by all workers. This does not include short-circuit local reads and domain socket reads |
| Cluster.BytesReadRemoteThroughput    | GAUGE        | Bytes read throughput from GooseFS storage or underlying UFS if data does not exist in GooseFS storage reported by all workers. This does not include short-circuit local reads and domain socket reads |
| Cluster.BytesReadUfsAll              | COUNTER      | Total number of bytes read from all GooseFS UFSes by all workers |
| Cluster.BytesReadUfsThroughput       | GAUGE        | Bytes read throughput from all GooseFS UFSes by all workers  |
| Cluster.BytesWrittenDomain           | COUNTER      | Total number of bytes written to GooseFS storage via domain socket by all workers |
| Cluster.BytesWrittenDomainThroughput | GAUGE        | Throughput of bytes written to GooseFS storage via domain socket by all workers |
| Cluster.BytesWrittenLocal            | COUNTER      | Total number of bytes short-circuit written to local storage by all clients |
| Cluster.BytesWrittenLocalThroughput  | GAUGE        | Bytes throughput written to local storage by all clients     |
| Cluster.BytesWrittenPerUfs           | COUNTER      | Total number of bytes written to a specific GooseFS UFS by all workers | 
| Cluster.BytesWrittenRemote           | COUNTER      | Total number of bytes written to GooseFS storage in all workers or the underlying UFS. This does not include short-circuit local writes and domain socket writes. |
| Cluster.BytesWrittenRemoteThroughput | GAUGE        | Bytes write throughput to GooseFS storage in all workers or the underlying UFS. This does not include short-circuit local writes and domain socket writes. |
| Cluster.BytesWrittenUfsAll           | COUNTER      | Total number of bytes written to all GooseFS UFSes by all workers |
| Cluster.BytesWrittenUfsThroughput    | GAUGE        | Bytes write throughput to all GooseFS UFSes by all workers   |
| Cluster.CapacityFree                 | GAUGE        | Total free bytes on all tiers, on all workers of GooseFS     |
| Cluster.CapacityTotal                | GAUGE        | Total capacity (in bytes) on all tiers, on all workers of GooseFS |
| Cluster.CapacityUsed                 | GAUGE        | Total used bytes on all tiers, on all workers of GooseFS     |
| Cluster.RootUfsCapacityFree          | GAUGE        | Free capacity of the GooseFS root UFS in bytes               |
| Cluster.RootUfsCapacityTotal         | GAUGE        | Total capacity of the GooseFS root UFS in bytes              |
| Cluster.RootUfsCapacityUsed          | GAUGE        | Used capacity of the GooseFS root UFS in bytes               |
| Cluster.Workers                      | GAUGE        | Total number of active workers inside the cluster            |


## Master Monitoring Metrics

Master monitoring metrics are classified into default metrics (recorded by default when the master is running) and dynamic metrics. Default metrics are as follows:

| **Metric** | **Type** | **Description** |
| ------------------------------------ | ------------ | ------------------------------------------------------------ |
| Master.CompleteFileOps               | COUNTER      | Total number of the CompleteFile operations                  |
| Master.CreateDirectoryOps            | COUNTER      | Total number of the CreateDirectory operations               |
| Master.CreateFileOps                 | COUNTER      | Total number of the CreateFile operations                    |
| Master.DeletePathOps                 | COUNTER      | Total number of the Delete operations                        |
| Master.DirectoriesCreated            | COUNTER      | Total number of successful CreateDirectory operations       |
| Master.EdgeCacheEvictions            | GAUGE        | Total number of edges (inode metadata) that was evicted from cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheHits                 | GAUGE        | Total number of hits in the edge (inode metadata) cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheLoadTimes            | GAUGE        | Total load times in the edge (inode metadata) cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheMisses               | GAUGE        | Total number of misses in the edge (inode metadata) cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheSize                 | GAUGE        | Total number of edges (inode metadata) cached. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeLockPoolSize              | GAUGE        | The size of master edge lock pool                            |
| Master.FileBlockInfosGot             | COUNTER      | Total number of successful GetFileBlockInfo operations          |
| Master.FileInfosGot                  | COUNTER      | Total number of successful GetFileInfo operations           |
| Master.FilesCompleted                | COUNTER      | Total number of successful CompleteFile operations          |
| Master.FilesCreated                  | COUNTER      | Total number of successful CreateFile operations            |
| Master.FilesFreed                    | COUNTER      | Total number of successful FreeFile operations                  |
| Master.FilesPersisted                | COUNTER      | Total number of successfully persisted files                 |
| Master.FilesPinned                   | GAUGE        | Total number of currently pinned files                       |
| Master.FreeFileOps                   | COUNTER      | Total number of FreeFile operations                          |
| Master.GetFileBlockInfoOps           | COUNTER      | Total number of GetFileBlockInfo operations                  |
| Master.GetFileInfoOps                | COUNTER      | Total number of the GetFileInfo operations                   |
| Master.GetNewBlockOps                | COUNTER      | Total number of the GetNewBlock operations                   |
| Master.InodeCacheEvictions           | GAUGE        | Total number of inodes that were evicted from the cache.      |
| Master.InodeCacheHits                | GAUGE        | Total number of hits in the inodes (inode metadata) cache.   |
| Master.InodeCacheLoadTimes           | GAUGE        | Total load times in the inodes (inode metadata) cache.       |
| Master.InodeCacheMisses              | GAUGE        | Total number of misses in the inodes (inode metadata) cache. |
| Master.InodeCacheSize                | GAUGE        | Total number of inodes (inode metadata) cached.              |
| Master.InodeLockPoolSize             | GAUGE        | The size of master inode lock pool                           |
| Master.JournalFlushFailure           | COUNTER      | Total number of failed journal flush                         |
| Master.JournalFlushTimer             | TIMER        | The timer statistics of journal flush                        |
| Master.JournalGainPrimacyTimer       | TIMER        | The timer statistics of journal gain primacy                 |
| Master.LastBackupEntriesCount        | GAUGE        | The total number of entries written in the last leading master metadata backup |
| Master.LastBackupRestoreCount        | GAUGE        | The total number of entries restored from backup when a leading master initializes its metadata |
| Master.LastBackupRestoreTimeMs       | GAUGE        | The processing time of the last restore from backup             |
| Master.LastBackupTimeMs              | GAUGE        | The processing time of the last backup                          |
| Master.ListingCacheSize              | GAUGE        | Size of the master listing cache                             |
| Master.MountOps                      | COUNTER      | Total number of Mount operations                             |
| Master.NewBlocksGot                  | COUNTER      | Total number of successful GetNewBlock operations           |
| Master.PathsDeleted                  | COUNTER      | Total number of successful Delete operations                |
| Master.PathsMounted                  | COUNTER      | Total number of successful Mount operations                     |
| Master.PathsRenamed                  | COUNTER      | Total number of successful Rename operations                    |
| Master.PathsUnmounted                | COUNTER      | Total number of successful Unmount operations                   |
| Master.RenamePathOps                 | COUNTER      | Total number of Rename operations                            |
| Master.SetAclOps                     | COUNTER      | Total number of SetAcl operations                            |
| Master.SetAttributeOps               | COUNTER      | Total number of SetAttribute operations                      |
| Master.TotalPaths                    | GAUGE        | Total number of files and directory in Goosefs namespace     |
| Master.UfsJournalCatchupTimer        | TIMER        | The timer statistics of journal catchup                      |
| Master.UfsJournalFailureRecoverTimer | TIMER        | The timer statistics of ufs journal failure recover          |
| Master.UfsJournalInitialReplayTimeMs | GAUGE        | The processing time of the ufs journal initial replay           |
| Master.UnmountOps                    | COUNTER      | Total number of Unmount operations                           |

Dynamic metrics:

| **Metric** | **Type** | **Description** |
| ---------------------------- | ------------ | ------------------------------------------------------------ |
| Master.CapacityTotalTier     | GAUGE        | Total capacity in tier of the Goosefs file system in bytes   |
| Master.CapacityUsedTier      | GAUGE        | Used capacity in tier of the Goosefs file system in bytes    |
| Master.CapacityFreeTier      | GAUGE        | Free capacity in tier of the Goosefs file system in bytes    |
| Master.UfsSessionCount-Ufs:  | COUNTER      | The total number of currently opened UFS sessions to connect to the given |
| Master..UFS:.UFS_TYPE:.User: | GAUGE        | The details UFS rpc operation done by the current master     |
| Master.PerUfsOp.UFS:         | TIMER        | The aggregated number of UFS operations ran on UFS by leading master |
| Master.                      | TIMER        | The duration statistics of RPC calls exposed on leading master |


## Worker Monitoring Metrics

Worker monitoring metrics are classified into default metrics (recorded by default when workers are running) and dynamic metrics. Default metrics are as follows:

| **Metric** | **Type** | **Description** |
| --------------------------------------- | ------------ | ------------------------------------------------------------ |
| Worker.AsyncCacheDuplicateRequests      | COUNTER      | Total number of duplicated async cache requests received by this worker |
| Worker.AsyncCacheFailedBlocks           | COUNTER      | Total number of async cache failed blocks in this worker     | 
| Worker.AsyncCacheRemoteBlocks           | COUNTER      | Total number of blocks that need to be async cached from remote source |
| Worker.AsyncCacheRequests               | COUNTER      | Total number of async cache requests received by this worker  |
| Worker.AsyncCacheSucceededBlocks        | COUNTER      | Total number of async cache succeeded blocks in this worker  |
| Worker.AsyncCacheUfsBlocks              | COUNTER      | Total number of blocks that need to be async cached from local source |
| Worker.BlockRemoverBlocksToRemovedCount | COUNTER      | The total number of blocks removed from this worker by asynchronous block remover. |
| Worker.BlockRemoverRemovingBlocksSize   | GAUGE        | The size of blocks is removing from this worker by asynchronous block remover. |
| Worker.BlockRemoverTryRemoveBlocksSize  | GAUGE        | The size of blocks to be removed from this worker by asynchronous block remover. |
| Worker.BlockRemoverTryRemoveCount       | COUNTER      | The total number of blocks tried to be removed from this worker by asynchronous block remover. |
| Worker.BlocksAccessed                   | COUNTER      | Total number of times any one of the blocks in this worker is accessed. |
| Worker.BlocksCached                     | GAUGE        | Total number of blocks used for caching data in a GooseFS worker |
| Worker.BlocksCancelled                  | COUNTER      | Total number of aborted temporary blocks in this worker.     |
| Worker.BlocksDeleted                    | COUNTER      | Total number of deleted blocks in this worker by external requests. |
| Worker.BlocksEvicted                    | COUNTER      | Total number of evicted blocks in this worker.               |
| Worker.BlocksLost                       | COUNTER      | Total number of lost blocks in this worker.                  |
| Worker.BlocksPromoted                   | COUNTER      | Total number of times any one of the blocks in this worker moved to a new tier. |
| Worker.BytesReadDomain                  | COUNTER      | Total number of bytes read from goosefs storage via domain socket by this worker |
| Worker.BytesReadDomainThroughput        | METER        | Bytes read throughput from goosefs storage via domain socket by this worker |
| Worker.BytesReadPerUfs                  | COUNTER      | Total number of bytes read from a specific goosefs UFS by this worker |
| Worker.BytesReadRemote                  | COUNTER      | Total number of bytes read from goosefs storage managed by this worker and underlying UFS if data cannot be found in the goosefs storage. This does not include short-circuit local reads and domain socket reads. |
| Worker.BytesReadRemoteThroughput        | METER        | Total number of bytes read from goosefs storage managed by this worker and underlying UFS if data cannot be found in the goosefs storage. This does not include short-circuit local reads and domain socket reads. |
| Worker.BytesReadUfsThroughput           | METER        | Bytes read throughput from all goosefs UFSes by this worker  |
| Worker.BytesWrittenDomain               | COUNTER      | Total number of bytes written to goosefs storage via domain socket by this worker |
| Worker.BytesWrittenDomainThroughput     | METER        | Throughput of bytes written to goosefs storage via domain socket by this worker |
| Worker.BytesWrittenPerUfs               | COUNTER      | Total number of bytes written to a specific goosefs UFS by this worker |
| Worker.BytesWrittenRemote               | COUNTER      | Total number of bytes written to goosefs storage or the underlying UFS by this worker. This does not include short-circuit local writes and domain socket writes. |
| Worker.BytesWrittenRemoteThroughput     | METER        | Bytes write throughput to goosefs storage or the underlying UFS by this workerThis does not include short-circuit local writes and domain socket writes. |
| Worker.BytesWrittenUfsThroughput        | METER        | Bytes write throughput to all goosefs UFSes by this worker   |
| Worker.CapacityFree                     | GAUGE        | Total free bytes on all tiers of a specific goosefs worker   |
| Worker.CapacityTotal                    | GAUGE        | Total capacity (in bytes) on all tiers of a specific goosefs worker |
| Worker.CapacityUsed                     | GAUGE        | Total used bytes on all tiers of a specific goosefs worker   |

Dynamic metrics:

| **Metric** | **Type** | **Description** |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| Worker.UfsSessionCount-Ufs | GAUGE        | The total number of currently opened UFS sessions to connect to the given |
| Worker.                    | TIMER        | The duration statistics of RPC calls exposed on workers      |


## Client Monitoring Metrics

Client monitoring metrics are aggregated based on the user ID or client IP. If a user ID is already registered in GooseFS, data will be aggregated by ID first. You can use `goosefs.user.app.id` to specify an ID. Client monitoring metrics are as follows:

| **Metric** | **Type** | **Description** |
| --------------------------------------- | ------------ | ------------------------------------------------------------ |
| Client.BytesReadLocal                   | COUNTER      | Total number of bytes short-circuit read from local storage by this client |
| Client.BytesReadLocalThroughput         | METER        | Bytes throughput short-circuit read from local storage by this client |
| Client.BytesWrittenLocal                | COUNTER      | Total number of bytes short-circuit written to local storage by this client |
| Client.BytesWrittenLocalThroughput      | METER        | Bytes throughput short-circuit written to local storage by this client |
| Client.BytesWrittenUfs                  | COUNTER      | Total number of bytes write to goosefs UFS by this client    |
| Client.CacheBytesEvicted                | METER        | Total number of bytes evicted from the client cache.         |
| Client.CacheBytesReadCache              | METER        | Total number of bytes read from the client cache.            |
| Client.CacheBytesReadExternal           | METER        | Total number of bytes read from external storage due to a cache miss on the client cache. |
| Client.CacheBytesRequestedExternal      | METER        | Total number of bytes the user requested to read which resulted in a cache miss. This number may be smaller than Client.CacheBytesReadExternal due to chunk reads. |
| Client.CacheBytesWrittenCache           | METER        | Total number of bytes written to the client cache.           |
| Client.CacheCleanupGetErrors            | COUNTER      | Number of failures when cleaning up a failed cache read.     |
| Client.CacheCleanupPutErrors            | COUNTER      | Number of failures when cleaning up a failed cache write.    |
| Client.CacheCreateErrors                | COUNTER      | Number of failures when creating a cache in the client cache. |
| Client.CacheDeleteErrors                | COUNTER      | Number of failures when deleting cached data in the client cache. |
| Client.CacheDeleteNonExistingPageErrors | COUNTER      | Number of failures when deleting pages due to absence.       |
| Client.CacheDeleteNotReadyErrors        | COUNTER      | Number of failures when cache is not ready to delete pages. |
| Client.CacheDeleteStoreDeleteErrors     | COUNTER      | Number of failures when deleting pages due to failed delete in page stores. |
| Client.CacheGetErrors                   | COUNTER      | Number of failures when getting cached data in the client cache. |
| Client.CacheGetNotReadyErrors           | COUNTER      | Number of failures when cache is not ready to get pages.     |
| Client.CacheGetStoreReadErrors          | COUNTER      | Number of failures when getting cached data in the client cache due to failed read from page stores. |
| Client.CacheHitRate                     | GAUGE       | Cache hit rate: <# bytes read from cache >/<# bytes requested>. |
| Client.CachePages                       | COUNTER      | Total number of pages in the client cache.                   |
| Client.CachePagesEvicted                | METER        | Total number of pages evicted from the client cache.         |
| Client.CachePutAsyncRejectionErrors     | COUNTER      | Number of failures when putting cached data in the client cache due to failed injection to async write queue. |
| Client.CachePutBenignRacingErrors       | COUNTER      | Number of failures when adding pages due to racing eviction. This error is benign. |
| Client.CachePutErrors                   | COUNTER      | Number of failures when putting cached data in the client cache. |
| Client.CachePutEvictionErrors           | COUNTER      | Number of failures when putting cached data in the client cache due to failed eviction. |
| Client.CachePutInsufficientSpaceErrors  | COUNTER      | Number of failures when putting cached data in the client cache due to insufficient space made after eviction. |  
| Client.CachePutNotReadyErrors           | COUNTER      | Number of failures when cache is not ready to add pages.     |
| Client.CachePutStoreDeleteErrors        | COUNTER      | Number of failures when putting cached data in the client cache due to failed deletes in page store. |  
| Client.CachePutStoreWriteErrors         | COUNTER      | Number of failures when putting cached data in the client cache due to failed writes to page store. |   
| Client.CacheSpaceAvailable              | GAUGE        | Amount of bytes available in the client cache.               |
| Client.CacheSpaceUsed                   | GAUGE        | Amount of bytes used by the client cache.                    |
| Client.CacheSpaceUsedCount              | COUNTER      | Amount of bytes used by the client cache as a counter.       |
| Client.CacheState                       | COUNTER      | State of the cache: 0 (NOT_IN_USE), 1 (READ_ONLY) and 2 (READ_WRITE) |
| Client.CacheStoreDeleteTimeout          | COUNTER      | Number of timeouts when deleting pages from page store.      |
| Client.CacheStoreGetTimeout             | COUNTER      | Number of timeouts when reading pages from page store.       |
| Client.CacheStorePutTimeout             | COUNTER      | Number of timeouts when writing new pages to page store.     |
| Client.CacheStoreThreadsRejected        | COUNTER      | Number of rejection of I/O threads on submitting tasks to thread pool, likely due to unresponsive local file system. |
| Client.CacheUnremovableFiles            | COUNTER      | Amount of bytes unusable managed by the client cache.        |


## Process Monitoring Metrics

Process monitoring metrics are collected and aggregated from clusters, masters, and workers. Metrics are classified into JVM metrics, garbage collection metrics, and memory consumption metrics.

JVM metrics:

| **Metric** | **Description**           |
| ------------ | ---------------------- |
| name         | The name of the JVM    |
| uptime       | The uptime of the JVM  |
| vendor       | The current JVM vendor |

Garbage collection metrics:

| **Metric** | **Description**           |
| ------------------ | ------------------------------- |
| PS-MarkSweep.count | Total number of mark and sweep  |
| PS-MarkSweep.time  | The time used to mark and sweep |
| PS-Scavenge.count  | Total number of scavenge        |
| PS-Scavenge.time   | The time used to scavenge       |

Memory consumption metrics record the overall and detailed information about memory consumption. Some metrics are listed below:

| **Metric** | **Description**           |
| --------------------------------- | ------------------------------------------------------------ |
| total.committed                   | The amount of memory in bytes that is guaranteed to be available for use by the JVM |
| total.init                        | The amount of the memory in bytes that is available for use by the JVM | 
| total.max                         | The maximum amount of memory in bytes that is available for use by the JVM | 
| total.used                        | The amount of memory currently used in bytes                 |
| heap.committed                    | The amount of memory from heap area guaranteed to be available |
| heap.init                         | The amount of memory from heap area available at initialization |
| heap.max                          | The maximum amount of memory from heap area that is available |
| heap.usage                        | The amount of memory from heap area currently used in GB     |
| heap.used                         | The amount of memory from heap area that has been used       |
| pools.Code-Cache.used             | Used memory of collection usage from the pool from which memory is used for compilation and storage of native code |
| pools.Compressed-Class-Space.used | Used memory of collection usage from the pool from which memory is used for class metadata |
| pools.PS-Eden-Space.used          | Used memory of collection usage from the pool from which memory is initially allocated for most objects |
| pools.PS-Survivor-Space.used      | Used memory of collection usage from the pool containing objects that have survived the garbage collection of the Eden spac |
