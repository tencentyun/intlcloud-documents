### Alluxio - Overview

| Metric Name | Unit | Description |
| -------------------------------------------- | -------- | ------------------------------------------------------- |
| Total amount of data read/written\_BytesReadAlluxio | Bytes | Total number of bytes read from Alluxio storage reported by all workers |
| Total amount of data read/written\_BytesReadUfsAll | Bytes | Total number of bytes read from Alluxio UFSes by all workers |
| Total amount of data read/written\_BytesReadDomain | Bytes | Total number of bytes read from Alluxio storage via a domain socket reported by all workers |
| Total amount of data read/written\_BytesReadLocal | Bytes | Total number of bytes short-circuit read from local storage by all clients |
| Total amount of data read/written\_BytesReadPerUfs | Bytes | Total number of bytes read from a specific UFS by all workers |
| Total amount of data read/written\_BytesWrittenAlluxio             | Bytes    | Total number of bytes written to Alluxio storage by all workers                    |
| Total amount of data read/written\_BytesWrittenUfsAll | Bytes | Total number of bytes written to all Alluxio UFSes by all workers |
| Total amount of data read/written\_BytesWrittenDomain | Bytes | Total number of bytes written to Alluxio storage via a domain socket by all workers |
| Total amount of data read/written\_BytesWrittenLocal | Bytes | Total number of bytes short-circuit written to local storage by all clients |
| Total amount of data read/written\_BytesWrittenPerUfs | Bytes | Total number of bytes written to a specific Alluxio UFS by all workers |
| Data read/write throughput\_BytesReadAlluxioThroughput | Bytes | Throughput of bytes read from Alluxio storage by all workers |
| Data read/write throughput\_BytesReadUfsThroughput | Bytes | Throughput of bytes read from all Alluxio UFSes by all workers |
| Data read/write throughput\_BytesReadDomainThroughput | Bytes | Throughput of bytes read from Alluxio storage via a domain socket by all workers |
| Data read/write throughput\_BytesReadLocalThroughput | Bytes | Throughput of bytes short-circuit read from local storage by all clients |
| Data read/write throughput\_BytesWrittenAlluxioThroughput | Bytes | Throughput of bytes written to Alluxio storage by all workers |
| Data read/write throughput\_BytesWrittenUfsThroughput | Bytes | Throughput of bytes written to all Alluxio UFSes by all workers |
| Data read/write throughput\_BytesWrittenDomainThroughput | Bytes | Throughput of bytes written to Alluxio storage via a domain socket by all workers |
| Data read/write throughput\_BytesWrittenLocalThroughput | Bytes | Throughput of bytes written to local storage by all clients |
| Worker capacity\_CapacityFree | Bytes | Total free bytes on all tiers of all workers |
| Worker capacity\_CapacityTotal | Bytes | Total capacity on all tiers of all workers |
| Worker capacity\_CapacityUsed | Bytes | Total used bytes on all tiers of all workers |
| Worker count\_Workers                           | -       | Total number of active workers in the cluster |


### Alluxio - Master

| Metric Name | Unit | Description |
| ---------------------------------------- | -------- | --------------------------------------- |
| YGC | - | Number of young GCs |
| FGC | - | Number of full GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |
| YGCT | s | Time taken by young GCs |
| S0 | % | Percentage of used survivor 0 memory |
| E | % | Percentage of used eden memory |
| CCS | % | Percentage of used compressed class space memory |
| S1 | % | Percentage of used survivor 1 memory |
| O | % | Percentage of used old memory |
| M | % | Percentage of used metaspace memory |
| MemNonHeapUsedM | MB | Amount of NonHeapMemory used by the JVM |
| MemNonHeapCommittedM | MB | Amount of NonHeapMemory committed by the JVM |
| MemHeapUsedM | MB | Amount of HeapMemory used by the JVM |
| MemHeapCommittedM | MB | Amount of HeapMemory committed by the JVM |
| MemHeapMaxM | MB | Amount of HeapMemory configured for the JVM |
| MemHeapInitM | MB | Initial amount of HeapMem for the JVM |
| MemNonHeapInitM | MB | Initial amount of NonHeapMem for the JVM |
| CompleteFile operations\_CompleteFileOps | - | Total number of CompleteFile operations |
| CompleteFile operations\_FilesCompleted          | -       | Total number of successful CompleteFile operations              |
| CreateDirectory operations\_CreateDirectoryOps  | - | Total number of CreateDirectory operations |
| CreateDirectory operations\_DirectoriesCreated | - | Total number of successful CreateDirectory operations |
| CreateFile operations\_CreateFileOps | - | Total number of CreateFile operations |
| CreateFile operations\_FilesCreated | - | Total number of successful CreateFile operations |
| Delete operations\_DeletePathOps | - | Total number of Delete operations |
| Delete operations\_PathsDeleted | - | Total number of successful Delete operations |
| FreeFile operations\_FreeFileOps | - | Total number of FreeFile operations |
| FreeFile operations\_FilesFreed | - | Total number of successful FreeFile operations |
| GetFileBlockInfo operations\_GetFileBlockInfoOps | - | Total number of GetFileBlockInfo operations                |
| GetFileBlockInfo operations\_FileBlockInfosGot | - | Total number of successful GetFileBlockInfo operations |
| GetFileInfo operations\_GetFileInfoOps | - | Total number of GetFileInfo operations |
| GetFileInfo operations\_FileInfosGot | - | Total number of successful GetFileInfo operations |
| GetNewBlock operations\_GetNewBlockOps | - | Total number of GetNewBlock operations |
| GetNewBlock operations\_NewBlocksGot | -  | Total number of successful GetNewBlock operations |
| Mount operations\_MountOps | - | Total number of Mount operations |
| Mount operations\_PathsMounted | - | Total number of successful Mount operations |
| Unmount operations\_UnmountOps | - | Total number of Unmount operations |
| Unmount operations\_PathsUnmounted | - | Total number of successful Unmount operations |
| Rename operations\_RenamePathOps | - | Total number of Rename operations |
| Rename operations\_PathsRenamed | - | Total number of successful Rename operations |
| SetAcl operations\_SetAclOps | - | Total number of SetAcl operations |
| SetAttribute operations\_SetAttributeOps | - | Total number of SetAttribute operations |
| Operated file count\_FilesPersisted | - | Total number of successfully saved files |
| Operated file count\_FilesPinned | - | Total number of currently pinned files |
| File and directory count\_TotalPaths  | - | Total number of files and directory in Alluxio namespace |

### Alluxio - Worker

| Metric Name | Unit | Description |
| ----------------------------------------- | -------- | ------------------------------------------ |
| YGC | - | Number of young GCs |
| FGC | - | Number of full GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |
| YGCT | s | Time taken by young GCs |
| S0 | % | Percentage of used survivor 0 memory |
| E | % | Percentage of used eden memory |
| CCS | % | Percentage of used compressed class space memory |
| S1 | % | Percentage of used survivor 1 memory |
| O | % | Percentage of used old memory |
| M | % | Percentage of used metaspace memory |
| MemNonHeapUsedM | MB | Amount of NonHeapMemory used by the JVM |
| MemNonHeapCommittedM | MB | Amount of NonHeapMemory committed by the JVM |
| MemHeapUsedM | MB | Amount of HeapMemory used by the JVM |
| MemHeapCommittedM | MB | Amount of HeapMemory committed by the JVM |
| MemHeapMaxM | MB | Amount of HeapMemory configured for the JVM |
| MemHeapInitM | MB | Initial amount of HeapMem for the JVM |
| MemNonHeapInitM | MB | Initial amount of NonHeapMem for the JVM |
| Async cache requests\_AsyncCacheDuplicateRequests | - | Total number of duplicated async cache requests received by a worker |
| Async cache requests\_AsyncCacheRequests | - | Total number of async cache requests received by a worker |
| Async cache block count\_AsyncCacheFailedBlocks | - | Total number of blocks that fail to be async cached in a worker |
| Async cache block count\_AsyncCacheRemoteBlocks  | - | Total number of blocks that need to be async cached from the remote source |
| Async cache block count\_AsyncCacheSucceededBlocks | - | Total number of blocks that are async cached successfully in a worker |
| Async cache block count\_AsyncCacheUfsBlocks | - | Total number of blocks that need to be async cached from the local source |
| BlocksAccessed | - | Total number of times any one of the blocks in a worker is accessed |
| BlocksCached | - | Total number of blocks used for caching data in a worker |
| BlocksCancelled | - | Total number of aborted temporary blocks in a worker |
| BlocksDeleted | - | Total number of deleted blocks in a worker by external requests. |
| BlocksEvicted | - | Total number of evicted blocks in a worker |
| BlocksLost | - | Total number of lost blocks in a worker |
| BlocksPromoted | - | Total number of times any one of the blocks in a worker moved to a new tier |
| Worker capacity\_CapacityFree             | Bytes    | Total free bytes on all tiers of all workers               |
| Worker capacity\_CapacityTotal            | Bytes    | Total capacity on all tiers of all workers                   |
| Worker capacity\_CapacityUsed | Bytes | Total used bytes on all tiers of all workers |

 
