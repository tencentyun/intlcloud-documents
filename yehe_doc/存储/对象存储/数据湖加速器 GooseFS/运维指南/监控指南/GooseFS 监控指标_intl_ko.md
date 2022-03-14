## 모니터링 지표 개요

Goosefs 모니터링 지표는 클라이언트, 클러스터, Master 노드, Worker 노드 및 프로세스의 실행 상태를 기록합니다.

1. 통계적 차원에 따라 모니터링 지표는 다음 네 가지 범주로 나눌 수 있습니다.
 - **Gauge**: 이벤트의 순간 값을 기록하며, 해당 값은 증감할 수 있으며 일반적으로 시스템의 실행 상태를 반영하는 데 사용됩니다.
 - **Meter**: 이벤트의 빈도, 즉, 고정된 시간 주기 내의 이벤트 발생 횟수, 1분, 5분, 15분 내의 요청 수를 통계합니다.
 - **Counter**: 총 이벤트 발생 횟수를 통계합니다. Gauge와 차이는 이 값은 증가만 하고 감소하지 않는다는 점입니다. 일반적으로 액세스 요청 횟수 등의 데이터를 기록하는 데 사용됩니다.
 - **Timer**: 이벤트의 빈도와 분포를 계산합니다. 이 지표는 Histogram 과 Meter 지표의 조합으로 간주될 수 있습니다. Histogram은 시간 소모적인 분포를 계산하는 데 사용되며 Meter는 QPS를 계산하는 데 사용됩니다. 주파수와 소비량을 동시에 계산해야 할 경우 이 지표를 사용할 수 있습니다.

>! 모니터링 지표의 더 많은 카테고리는 [Metrics Library 문서](https://metrics.dropwizard.io/3.1.0/getting-started)를 참고하십시오. 현재 GooseFS는 위의 4가지 모니터링 지표만 제공하고 있습니다.
>

2. 데이터 수집 출처에 따라 모니터링 지표는 다음 두 가지 범주로 나눌 수 있습니다.
 - **클러스터 상태 지표**: 클러스터 상태 지표는 Cluster, Master 및 Worker 차원의 모니터링 데이터를 포함하며, 이러한 모니터링 지표는 전체 클러스터 및 클러스터 아래의 각 노드의 실행 상태를 반영할 수 있습니다. 이러한 지표의 기록 형식은 다음과 같습니다.
```plaintext
Master.[metricName].[tag1].[tag2]...
[Worker_ip].[metricName].[tag1].[tag2]...
```
 - **프로세스 처리 지표**: 프로세스 처리 지표는 클러스터의 요청 수, 지연, CPU 사용량, RPC 호출 횟수 등 정보를 자세히 기록하는 데 사용되며 이러한 지표는 제 3자 모니터링 툴에 푸시하여 표시할 수 있습니다. 이러한 지표의 기록 형식은 다음과 같습니다.
```plaintext
[processType].[metricName].[tag1].[tag2]...[hostName]
```

## Cluster 모니터링 지표

GooseFS 클러스터 배포 시, 클라이언트와 Worker 노드는 주기적으로 하트 비트를 통해 Master 노드에 모니터링 지표를 보내며, goosefs.master.worker.heartbeat.interval과 goosefs.user.metrics.heartbeat.interval를 통해 Worker 노드와 클라이언트 모니터링 지표의 하트비트 주기를 각각 설정할 수 있습니다.

Cluster 레벨의 모니터링 지표 목록은 다음과 같습니다.

| **지표 이름**             | **지표 유형** | **지표 설명**                         |
| ------------------------------------ | ------------ | ------------------------------------------------------------ |
| Cluster.BytesReadDomain       | COUNTER   | Total number of bytes read from GooseFS storage via domain socket reported by all workers |
| Cluster.BytesReadDomainThroughput  | GAUGE    | Bytes read throughput from GooseFS storage via domain socket by all workers |
| Cluster.BytesReadLocal        | COUNTER   | Total number of bytes short-circuit read from local storage by all clients |
| Cluster.BytesReadLocalThroughput   | GAUGE    | Bytes throughput short-circuit read from local storage by all clients |
| Cluster.BytesReadPerUfs       | COUNTER   | Total number of bytes read from a specific UFS by all workers |
| Cluster.BytesReadRemote       | COUNTER   | Total number of bytes read from GooseFS storage or underlying UFS if data does not exist in GooseFS storage reported by all workers. This does not include short-circuit local reads and domain socket reads |
| Cluster.BytesReadRemoteThroughput  | GAUGE    | Bytes read throughput from GooseFS storage or underlying UFS if data does not exist in GooseFS storage reported by all workers. This does not include short-circuit local reads and domain socket reads |
| Cluster.BytesReadUfsAll       | COUNTER   | Total number of bytes read from a all GooseFS UFSes by all workers |
| Cluster.BytesReadUfsThroughput    | GAUGE    | Bytes read throughput from all GooseFS UFSes by all workers |
| Cluster.BytesWrittenDomain      | COUNTER   | Total number of bytes written to GooseFS storage via domain socket by all workers |
| Cluster.BytesWrittenDomainThroughput | GAUGE    | Throughput of bytes written to GooseFS storage via domain socket by all workers |
| Cluster.BytesWrittenLocal      | COUNTER   | Total number of bytes short-circuit written to local storage by all clients |
| Cluster.BytesWrittenLocalThroughput | GAUGE    | Bytes throughput written to local storage by all clients   |
| Cluster.BytesWrittenPerUfs      | COUNTER   | Total number of bytes written to a specific GooseFS UFS by all workers | 
| Cluster.BytesWrittenRemote      | COUNTER   | Total number of bytes written to GooseFS storage in all workers or the underlying UFS. This does not include short-circuit local writes and domain socket writes. |
| Cluster.BytesWrittenRemoteThroughput | GAUGE    | Bytes write throughput to GooseFS storage in all workers or the underlying UFS. This does not include short-circuit local writes and domain socket writes. |
| Cluster.BytesWrittenUfsAll      | COUNTER   | Total number of bytes written to all GooseFS UFSes by all workers |
| Cluster.BytesWrittenUfsThroughput  | GAUGE    | Bytes write throughput to all GooseFS UFSes by all workers  |
| Cluster.CapacityFree         | GAUGE    | Total free bytes on all tiers, on all workers of GooseFS   |
| Cluster.CapacityTotal        | GAUGE    | Total capacity (in bytes) on all tiers, on all workers of GooseFS |
| Cluster.CapacityUsed         | GAUGE    | Total used bytes on all tiers, on all workers of GooseFS   |
| Cluster.RootUfsCapacityFree     | GAUGE    | Free capacity of the GooseFS root UFS in bytes        |
| Cluster.RootUfsCapacityTotal     | GAUGE    | Total capacity of the GooseFS root UFS in bytes       |
| Cluster.RootUfsCapacityUsed     | GAUGE    | Used capacity of the GooseFS root UFS in bytes        |
| Cluster.Workers           | GAUGE    | Total number of active workers inside the cluster      |


## Master 모니터링 지표

Master 모니터링 지표는 두 가지 종류가 있는데, 하나는 Master 실행 과정 중 기본적으로 기록되는 지표이며, 다른 하나는 동적 모니터링 지표입니다. 기본 Master 모니터링 지표는 다음과 같습니다.

| **지표 명칭**             | **지표 유형** | **지표 설명**                         |
| ------------------------------------ | ------------ | ------------------------------------------------------------ |
| Master.CompleteFileOps        | COUNTER   | Total number of the CompleteFile operations         |
| Master.CreateDirectoryOps      | COUNTER   | Total number of the CreateDirectory operations        |
| Master.CreateFileOps         | COUNTER   | Total number of the CreateFile operations          |
| Master.DeletePathOps         | COUNTER   | Total number of the Delete operations            |
| Master.DirectoriesCreated      | COUNTER   | Total number of the succeed CreateDirectory operations    |
| Master.EdgeCacheEvictions      | GAUGE    | Total number of edges (inode metadata) that was evicted from cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheHits         | GAUGE    | Total number of hits in the edge (inode metadata) cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheLoadTimes      | GAUGE    | Total load times in the edge (inode metadata) cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheMisses        | GAUGE    | Total number of misses in the edge (inode metadata) cache. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeCacheSize         | GAUGE    | Total number of edges (inode metadata) cached. The edge cache is responsible for managing the mapping from (parentId, childName) to childId. |
| Master.EdgeLockPoolSize       | GAUGE    | The size of master edge lock pool              |
| Master.FileBlockInfosGot       | COUNTER   | Total number of succeed GetFileBlockInfo operations     |
| Master.FileInfosGot         | COUNTER   | Total number of the succeed GetFileInfo operations      |
| Master.FilesCompleted        | COUNTER   | Total number of the succeed CompleteFile operations     |
| Master.FilesCreated         | COUNTER   | Total number of the succeed CreateFile operations      |
| Master.FilesFreed          | COUNTER   | Total number of succeed FreeFile operations         |
| Master.FilesPersisted        | COUNTER   | Total number of successfully persisted files         |
| Master.FilesPinned          | GAUGE    | Total number of currently pinned files            |
| Master.FreeFileOps          | COUNTER   | Total number of FreeFile operations             |
| Master.GetFileBlockInfoOps      | COUNTER   | Total number of GetFileBlockInfo operations         |
| Master.GetFileInfoOps        | COUNTER   | Total number of the GetFileInfo operations          |
| Master.GetNewBlockOps        | COUNTER   | Total number of the GetNewBlock operations          |
| Master.InodeCacheEvictions      | GAUGE    | Total number of inodes that was evicted from the cache.   |
| Master.InodeCacheHits        | GAUGE    | Total number of hits in the inodes (inode metadata) cache.  |
| Master.InodeCacheLoadTimes      | GAUGE    | Total load times in the inodes (inode metadata) cache.    |
| Master.InodeCacheMisses       | GAUGE    | Total number of misses in the inodes (inode metadata) cache. |
| Master.InodeCacheSize        | GAUGE    | Total number of inodes (inode metadata) cached.       |
| Master.InodeLockPoolSize       | GAUGE    | The size of master inode lock pool              |
| Master.JournalFlushFailure      | COUNTER   | Total number of failed journal flush             |
| Master.JournalFlushTimer       | TIMER    | The timer statistics of journal flush            |
| Master.JournalGainPrimacyTimer    | TIMER    | The timer statistics of journal gain primacy         |
| Master.LastBackupEntriesCount    | GAUGE    | The total number of entries written in the last leading master metadata backup |
| Master.LastBackupRestoreCount    | GAUGE    | The total number of entries restored from backup when a leading master initializes its metadata |
| Master.LastBackupRestoreTimeMs    | GAUGE    | The process time of the last restore from backup       |
| Master.LastBackupTimeMs       | GAUGE    | The process time of the last backup             |
| Master.ListingCacheSize       | GAUGE    | The size of master listing cache               |
| Master.MountOps           | COUNTER   | Total number of Mount operations               |
| Master.NewBlocksGot         | COUNTER   | Total number of the succeed GetNewBlock operations      |
| Master.PathsDeleted         | COUNTER   | Total number of the succeed Delete operations        |
| Master.PathsMounted         | COUNTER   | Total number of succeed Mount operations           |
| Master.PathsRenamed         | COUNTER   | Total number of succeed Rename operations          |
| Master.PathsUnmounted        | COUNTER   | Total number of succeed Unmount operations          |
| Master.RenamePathOps         | COUNTER   | Total number of Rename operations              |
| Master.SetAclOps           | COUNTER   | Total number of SetAcl operations              |
| Master.SetAttributeOps        | COUNTER   | Total number of SetAttribute operations           |
| Master.TotalPaths          | GAUGE    | Total number of files and directory in Goosefs namespace   |
| Master.UfsJournalCatchupTimer    | TIMER    | The timer statistics of journal catchup           |
| Master.UfsJournalFailureRecoverTimer | TIMER    | The timer statistics of ufs journal failure recover     |
| Master.UfsJournalInitialReplayTimeMs | GAUGE    | The process time of the ufs journal initial replay      |
| Master.UnmountOps          | COUNTER   | Total number of Unmount operations              |

동적 지표는 아래와 같습니다.

| **지표 이름**         | **지표 유형** | **지표 설명**                         |
| ---------------------------- | ------------ | ------------------------------------------------------------ |
| Master.CapacityTotalTier   | GAUGE    | Total capacity in tier of the Goosefs file system in bytes  |
| Master.CapacityUsedTier   | GAUGE    | Used capacity in tier of the Goosefs file system in bytes  |
| Master.CapacityFreeTier   | GAUGE    | Free capacity in tier of the Goosefs file system in bytes  |
| Master.UfsSessionCount-Ufs: | COUNTER   | The total number of currently opened UFS sessions to connect to the given |
| Master..UFS:.UFS_TYPE:.User: | GAUGE    | The details UFS rpc operation done by the current master   |
| Master.PerUfsOp.UFS:     | TIMER    | The aggregated number of UFS operation ran on UFS by leading master |
| Master.           | TIMER    | The duration statistics of RPC calls exposed on leading master |


## Worker 모니터링 지표

Worker 모니터링 지표에는 크게 두 가지 범주가 있는데, 하나는 Worker 실행 과정 중 기본적으로 기록되는 기본 지표이고 다른 하나는 동적 모니터링 지표입니다. 기본 Worker 모니터링 지표는 다음과 같습니다.

| **지표 이름**            | **지표 유형** | **지표 설명**                       |
| --------------------------------------- | ------------ | ------------------------------------------------------------ |
| Worker.AsyncCacheDuplicateRequests   | COUNTER   | Total number of duplicated async cache request received by this worker |
| Worker.AsyncCacheFailedBlocks      | COUNTER   | Total number of async cache failed blocks in this worker   |  
| Worker.AsyncCacheRemoteBlocks      | COUNTER   | Total number of blocks that need to be async cached from remote source |
| Worker.AsyncCacheRequests        | COUNTER   | Total number of async cache request received by this worker |
| Worker.AsyncCacheSucceededBlocks    | COUNTER   | Total number of async cache succeeded blocks in this worker |
| Worker.AsyncCacheUfsBlocks       | COUNTER   | Total number of blocks that need to be async cached from local source |
| Worker.BlockRemoverBlocksToRemovedCount | COUNTER   | The total number of blocks removed from this worker by asynchronous block remover. |
| Worker.BlockRemoverRemovingBlocksSize  | GAUGE    | The size of blocks is removing from this worker by asynchronous block remover. |
| Worker.BlockRemoverTryRemoveBlocksSize | GAUGE    | The size of blocks to be removed from this worker by asynchronous block remover. |
| Worker.BlockRemoverTryRemoveCount    | COUNTER   | The total number of blocks tried to be removed from this worker by asynchronous block remover. |
| Worker.BlocksAccessed          | COUNTER   | Total number of times any one of the blocks in this worker is accessed. |
| Worker.BlocksCached           | GAUGE    | Total number of blocks used for caching data in an goosefs worker |
| Worker.BlocksCancelled         | COUNTER   | Total number of aborted temporary blocks in this worker.   |
| Worker.BlocksDeleted          | COUNTER   | Total number of deleted blocks in this worker by external requests. |
| Worker.BlocksEvicted          | COUNTER   | Total number of evicted blocks in this worker.        |
| Worker.BlocksLost            | COUNTER   | Total number of lost blocks in this worker.         |
| Worker.BlocksPromoted          | COUNTER   | Total number of times any one of the blocks in this worker moved to a new tier. |
| Worker.BytesReadDomain         | COUNTER   | Total number of bytes read from goosefs storage via domain socket by this worker |
| Worker.BytesReadDomainThroughput    | METER    | Bytes read throughput from goosefs storage via domain socket by this worker |
| Worker.BytesReadPerUfs         | COUNTER   | Total number of bytes read from a specific goosefs UFS by this worker |
| Worker.BytesReadRemote         | COUNTER   | Total number of bytes read from goosefs storage managed by this worker and underlying UFS if data cannot be found in the goosefs storage. This does not include short-circuit local reads and domain socket reads. |
| Worker.BytesReadRemoteThroughput    | METER    | Total number of bytes read from goosefs storage managed by this worker and underlying UFS if data cannot be found in the goosefs storage. This does not include short-circuit local reads and domain socket reads. |
| Worker.BytesReadUfsThroughput      | METER    | Bytes read throughput from all goosefs UFSes by this worker |
| Worker.BytesWrittenDomain        | COUNTER   | Total number of bytes written to goosefs storage via domain socket by this worker |
| Worker.BytesWrittenDomainThroughput   | METER    | Throughput of bytes written to goosefs storage via domain socket by this worker |
| Worker.BytesWrittenPerUfs        | COUNTER   | Total number of bytes written to a specific goosefs UFS by this worker |
| Worker.BytesWrittenRemote        | COUNTER   | Total number of bytes written to goosefs storage or the underlying UFS by this worker. This does not include short-circuit local writes and domain socket writes. |
| Worker.BytesWrittenRemoteThroughput   | METER    | Bytes write throughput to goosefs storage or the underlying UFS by this workerThis does not include short-circuit local writes and domain socket writes. |
| Worker.BytesWrittenUfsThroughput    | METER    | Bytes write throughput to all goosefs UFSes by this worker  |
| Worker.CapacityFree           | GAUGE    | Total free bytes on all tiers of a specific goosefs worker  |
| Worker.CapacityTotal          | GAUGE    | Total capacity (in bytes) on all tiers of a specific goosefs worker |
| Worker.CapacityUsed           | GAUGE    | Total used bytes on all tiers of a specific goosefs worker  |

동적 모니터링 지표는 아래와 같습니다.

| **지표 이름**            | **지표 유형** | **지표 설명**                       |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| Worker.UfsSessionCount-Ufs | GAUGE    | The total number of currently opened UFS sessions to connect to the given |
| Worker.          | TIMER    | The duration statistics of RPC calls exposed on workers   |


## 클라이언트 모니터링 지표

클라이언트 모니터링 지표는 지정된 사용자 ID 또는 클라이언트의 IP 차원을 통해 집계되며, 사용자 ID가 GooseFS에 등록되어 있으면 우선적으로 사용자 ID 차원에 따라 집계됩니다. 사용자 ID는 goosefs.user.app.id로 지정할 수 있습니다. 클라이언트 모니터링 지표는 다음과 같습니다.

| **지표 이름**            | **지표 유형** | **지표 설명**                       |
| --------------------------------------- | ------------ | ------------------------------------------------------------ |
| Client.BytesReadLocal          | COUNTER   | Total number of bytes short-circuit read from local storage by this client |
| Client.BytesReadLocalThroughput     | METER    | Bytes throughput short-circuit read from local storage by this client |
| Client.BytesWrittenLocal        | COUNTER   | Total number of bytes short-circuit written to local storage by this client |
| Client.BytesWrittenLocalThroughput   | METER    | Bytes throughput short-circuit written to local storage by this client |
| Client.BytesWrittenUfs         | COUNTER   | Total number of bytes write to goosefs UFS by this client  |
| Client.CacheBytesEvicted        | METER    | Total number of bytes evicted from the client cache.     |
| Client.CacheBytesReadCache       | METER    | Total number of bytes read from the client cache.      |
| Client.CacheBytesReadExternal      | METER    | Total number of bytes read from external storage due to a cache miss on the client cache. |
| Client.CacheBytesRequestedExternal   | METER    | Total number of bytes the user requested to read which resulted in a cache miss. This number may be smaller than Client.CacheBytesReadExternal due to chunk reads. |
| Client.CacheBytesWrittenCache      | METER    | Total number of bytes written to the client cache.      |
| Client.CacheCleanupGetErrors      | COUNTER   | Number of failures when cleaning up a failed cache read.   |
| Client.CacheCleanupPutErrors      | COUNTER   | Number of failures when cleaning up a failed cache write.  |
| Client.CacheCreateErrors        | COUNTER   | Number of failures when creating a cache in the client cache. |
| Client.CacheDeleteErrors        | COUNTER   | Number of failures when deleting cached data in the client cache. |
| Client.CacheDeleteNonExistingPageErrors | COUNTER   | Number of failures when deleting pages due to absence.    |
| Client.CacheDeleteNotReadyErrors    | COUNTER   | Number of failures when when cache is not ready to delete pages. |
| Client.CacheDeleteStoreDeleteErrors   | COUNTER   | Number of failures when deleting pages due to failed delete in page stores. |
| Client.CacheGetErrors          | COUNTER   | Number of failures when getting cached data in the client cache. |
| Client.CacheGetNotReadyErrors      | COUNTER   | Number of failures when cache is not ready to get pages.   |
| Client.CacheGetStoreReadErrors     | COUNTER   | Number of failures when getting cached data in the client cache due to failed read from page stores. |
| Client.CacheHitRate                     | GAUGE       | Cache hit rate: <# bytes read from cache >/<# bytes requested>. |
| Client.CachePages            | COUNTER   | Total number of pages in the client cache.          |
| Client.CachePagesEvicted        | METER    | Total number of pages evicted from the client cache.     |
| Client.CachePutAsyncRejectionErrors   | COUNTER   | Number of failures when putting cached data in the client cache due to failed injection to async write queue. |
| Client.CachePutBenignRacingErrors    | COUNTER   | Number of failures when adding pages due to racing eviction. This error is benign. |
| Client.CachePutErrors          | COUNTER   | Number of failures when putting cached data in the client cache. |
| Client.CachePutEvictionErrors      | COUNTER   | Number of failures when putting cached data in the client cache due to failed eviction. |
| Client.CachePutInsufficientSpaceErrors | COUNTER   | Number of failures when putting cached data in the client cache due to insufficient space made after eviction. |  
| Client.CachePutNotReadyErrors      | COUNTER   | Number of failures when cache is not ready to add pages.   |
| Client.CachePutStoreDeleteErrors    | COUNTER   | Number of failures when putting cached data in the client cache due to failed deletes in page store. |  
| Client.CachePutStoreWriteErrors     | COUNTER   | Number of failures when putting cached data in the client cache due to failed writes to page store. |  
| Client.CacheSpaceAvailable       | GAUGE    | Amount of bytes available in the client cache.        |
| Client.CacheSpaceUsed          | GAUGE    | Amount of bytes used by the client cache.          |
| Client.CacheSpaceUsedCount       | COUNTER   | Amount of bytes used by the client cache as a counter.    |
| Client.CacheState            | COUNTER   | State of the cache: 0 (NOT_IN_USE), 1 (READ_ONLY) and 2 (READ_WRITE) |
| Client.CacheStoreDeleteTimeout     | COUNTER   | Number of timeouts when deleting pages from page store.   |
| Client.CacheStoreGetTimeout       | COUNTER   | Number of timeouts when reading pages from page store.    |
| Client.CacheStorePutTimeout       | COUNTER   | Number of timeouts when writing new pages to page store.   |
| Client.CacheStoreThreadsRejected    | COUNTER   | Number of rejection of I/O threads on submitting tasks to thread pool, likely due to unresponsive local file system. |
| Client.CacheUnremovableFiles      | COUNTER   | Amount of bytes unusable managed by the client cache.    |


## 프로세스 모니터링 지표

프로세스 모니터링 지표는 Cluster, Master 및 Worker에서 수집 및 집계할 수 있습니다. 주로 JVM 정보, 가비지 컬렉션 정보, 메모리 사용량 정보의 세 가지 범주로 구성됩니다.

JVM 정보는 다음 내용을 포함합니다.

| **지표 이름**           | **지표 설명**                       |
| ------------ | ---------------------- |
| name     | The name of the JVM  |
| uptime    | The uptime of the JVM |
| vendor    | The current JVM vendor |

가비지 콜렉션 모니터링 지표에는 다음이 포함됩니다.

| **지표 이름**           | **지표 설명**                       |
| ------------------ | ------------------------------- |
| PS-MarkSweep.count | Total number of mark and sweep |
| PS-MarkSweep.time | The time used to mark and sweep |
| PS-Scavenge.count | Total number of scavenge    |
| PS-Scavenge.time  | The time used to scavenge    |

메모리 사용량 모니터링 지표는 메모리 사용량에 대한 개요 및 세부 정보를 기록합니다. 모니터링 지표 중 일부는 다음과 같습니다.

| **지표 이름**           | **지표 설명**                         |
| --------------------------------- | ------------------------------------------------------------ |
| total.committed          | The amount of memory in bytes that is guaranteed to be available for use by the JVM |
| total.init            | The amount of the memory in bytes that is available for use by the JVM | 
| total.max             | The maximum amount of memory in bytes that is available for use by the JVM | 
| total.used            | The amount of memory currently used in bytes         |
| heap.committed          | The amount of memory from heap area guaranteed to be available |
| heap.init             | The amount of memory from heap area available at initialization |
| heap.max             | The maximum amount of memory from heap area that is available |
| heap.usage            | The amount of memory from heap area currently used in GB   |
| heap.used             | The amount of memory from heap area that has been used    |
| pools.Code-Cache.used       | Used memory of collection usage from the pool from which memory is used for compilation and storage of native code |
| pools.Compressed-Class-Space.used | Used memory of collection usage from the pool from which memory is use for class metadata |
| pools.PS-Eden-Space.used     | Used memory of collection usage from the pool from which memory is initially allocated for most objects |
| pools.PS-Survivor-Space.used   | Used memory of collection usage from the pool containing objects that have survived the garbage collection of the Eden spac |
