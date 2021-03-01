| Metric Name | Unit | Description |
| ----------------------------- | ----- | ------------------------------------------------------- |
| BytesReadAlluxio | Bytes | Total number of bytes read from Alluxio storage reported by all workers |
| BytesReadUfsAll | Bytes | Total number of bytes read from Alluxio UFSes by all workers |
| BytesReadDomain | Bytes | Total number of bytes read from Alluxio storage via a domain socket reported by all workers |
| BytesReadLocal | Bytes | Total number of bytes short-circuit read from local storage by all clients |
| BytesReadPerUfs | Bytes | Total number of bytes read from a specific UFS by all workers |
| BytesWrittenUfsAll | Bytes | Total number of bytes written to all Alluxio UFSes by all workers |
| BytesWrittenDomain | Bytes | Total number of bytes written to Alluxio storage via a domain socket by all workers |
| BytesWrittenLocal | Bytes | Total number of bytes short-circuit written to local storage by all clients |
| BytesWrittenPerUfs | Bytes | Total number of bytes written to a specific Alluxio UFS by all workers |
| BytesReadAlluxioThroughput | Bytes | Throughput of bytes read from Alluxio storage by all workers |
| BytesReadUfsThroughput | Bytes | Throughput of bytes read from all Alluxio UFSes by all workers |
| BytesReadDomainThroughput | Bytes | Throughput of bytes read from Alluxio storage via a domain socket by all workers |
| BytesReadLocalThroughput | Bytes | Throughput of bytes short-circuit read from local storage by all clients |
| BytesWrittenAlluxioThroughput | Bytes | Throughput of bytes written to Alluxio storage by all workers |
| BytesWrittenUfsThroughput | Bytes | Throughput of bytes written to all Alluxio UFSes by all workers |
| BytesWrittenDomainThroughput | Bytes | Throughput of bytes written to Alluxio storage via a domain socket by all workers |
| BytesWrittenLocalThroughput | Bytes | Through of bytes written to local storage by all clients |
| CapacityFree | Bytes | Total free bytes on all tiers of all workers |
| CapacityTotal | Bytes | Total capacity on all tiers of all workers |
| CapacityUsed | Bytes | Total used bytes on all tiers of all workers |
| Workers | - | Total number of active workers in the cluster |
| CompleteFileOps | - | Total number of CompleteFile operations |
| FilesCompleted | - | Total number of successful CompleteFile operations |
| CreateDirectoryOps | - | Total number of CreateDirectory operations |
| DirectoriesCreated | - | Total number of successful CreateDirectory operations |
| CreateFileOps | - | Total number of CreateFile operations |
| FilesCreated | - | Total number of successful CreateFile operations |
| DeletePathOps | - | Total number of Delete operations |
| PathsDeleted | - | Total number of successful Delete operations |
| FreeFileOps | - | Total number of FreeFile operations |
| FilesFreed | - | Total number of successful FreeFile operations |
| GetFileBlockInfoOps | - | Total number of GetFileBlockInfo operations |
| FileBlockInfosGot | - | Total number of successful GetFileBlockInfo operations |
| GetFileInfoOps | - | Total number of GetFileInfo operations |
| FileInfosGot | - | Total number of successful GetFileInfo operations |
| GetNewBlockOps | - | Total number of GetNewBlock operations |
| NewBlocksGot | -  | Total number of successful GetNewBlock operations |
| MountOps | - | Total number of Mount operations |
| PathsMounted | - | Total number of successful Mount operations |
| UnmountOps | - | Total number of Unmount operations |
| PathsUnmounted | - | Total number of successful Unmount operations |
| RenamePathOps | - | Total number of Rename operations |
| PathsRenamed | - | Total number of successful Rename operations |
| SetAclOps | - | Total number of SetAcl operations |
| SetAttributeOps | - | Total number of SetAttribute operations |
| FilesPersisted | - | Total number of successfully saved files |
| FilesPinned | - | Total number of currently pinned files |
| TotalPaths  | - | Total number of files and directory in Alluxio namespace |
| YGC | - | Number of young GCs |
| FGC | - | Number of full GCs |
| FGCT | s | Time taken by full GCs |
| GCT | s | Time taken by GCs |
| YGCT | s  | Time taken by young GCs |
| S0  | % | Memory utilization of survivor space 0 |
| E  | % | Memory utilization of eden space |
| CCS | % | Memory utilization of compressed class space |
| S1 | % | Memory utilization of survivor space 1 |
| O | % | Memory utilization of old space |
| M | % | Memory utilization of metaspace space |
| MemNonHeapUsedM | MB | Number of used JVM NonHeapMemory |
| MemNonHeapCommittedM | MB | Number of committed JVM NonHeapMemory |
| MemHeapUsedM | MB | Number of used JVM HeapMemory |
| MemHeapCommittedM | MB | Number of committed JVM HeapMemory |
| MemHeapMaxM | MB | Number of configured JVM HeapMemory |
| MemHeapInitM | MB | Number of initial JVM HeapMem |
| MemNonHeapInitM | MB | Number of initial JVM NonHeapMem |
| AsyncCacheDuplicateRequests | - | Total number of duplicated async cache requests received by a worker |
| AsyncCacheRequests | - | Total number of async cache requests received by a worker |
| AsyncCacheFailedBlocks | - | Total number of blocks that fail to be async cached in a worker |
| AsyncCacheRemoteBlocks  | - | Total number of blocks that need to be async cached from the remote source |
| AsyncCacheSucceededBlocks | - | Total number of blocks that are async cached successfully in a worker |
| AsyncCacheUfsBlocks | - | Total number of blocks that need to be async cached from the local source |
| BlocksAccessed | - | Total number of times any one of the blocks in a worker is accessed |
| BlocksCached | - | Total number of blocks used for caching data in a worker |
| BlocksCancelled | - | Total number of aborted temporary blocks in a worker |
| BlocksDeleted | - | Total number of deleted blocks in a worker by external requests. |
| BlocksEvicted | - | Total number of evicted blocks in a worker |
| BlocksLost | - | Total number of lost blocks in a worker |
| BlocksPromoted | - | Total number of times any one of the blocks in a worker moved to a new tier |

 

