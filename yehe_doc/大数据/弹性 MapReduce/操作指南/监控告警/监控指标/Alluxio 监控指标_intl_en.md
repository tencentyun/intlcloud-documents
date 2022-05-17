### Alluxio - cluster
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=4>Total data reads and writes</td>
<td >BytesReadAlluxio</td>
<td >Bytes</td>
<td >Total number of bytes read from Alluxio storage reported by all workers</td>
</tr><tr>
<td >BytesReadUfsAll</td>
<td >Bytes</td>
<td >Total number of bytes read by all workers from all Alluxio UFSes</td>
</tr><tr>
<td >BytesWrittenAlluxio</td>
<td >Bytes</td>
<td >Total number of bytes written to Alluxio storage in all workers</td>
</tr><tr>
<td >BytesWrittenUfsAll</td>
<td >Bytes</td>
<td >Total number of bytes written to all Alluxio UFSes by all workers</td>
</tr><tr>
<td rowspan=4>Data read and write throughput</td>
<td >BytesReadAlluxioThroughput</td>
<td >Bytes</td>
<td >Data read throughput from Alluxio storage by all workers</td>
</tr><tr>
<td >BytesReadUfsThroughput</td>
<td >Bytes</td>
<td >Read throughput from all Alluxio UFSes by all workers</td>
</tr><tr>
<td >BytesWrittenAlluxioThroughput</td>
<td >Bytes</td>
<td >Data write throughput to Alluxio storage by all workers</td>
</tr><tr>
<td >BytesWrittenUfsThroughput</td>
<td >Bytes</td>
<td >Write throughput to all Alluxio UFSes by all workers</td>
</tr><tr>
<td rowspan=3>Worker capacity on tiers</td>
<td >CapacityFree</td>
<td >Bytes</td>
<td >Total number of free bytes on all tiers of all workers</td>
</tr><tr>
<td >CapacityTotal</td>
<td >Bytes</td>
<td >Total capacity on all tiers of all workers</td>
</tr><tr>
<td >CapacityUsed</td>
<td >Bytes</td>
<td >Total number of used bytes on all tiers of all workers</td>
</tr><tr>
<td >Total workers</td>
<td >Workers</td>
<td >-</td>
<td >Total number of active workers inside the cluster</td>
</tr></table>

### Alluxio - master
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>CompleteFile operation</td>
<td >CompleteFileOps</td>
<td >-</td>
<td >Total number of CompleteFile operations</td>
</tr><tr>
<td >FilesCompleted</td>
<td >-</td>
<td >Total number of successful CompleteFile operations</td>
</tr><tr>
<td rowspan=2>CreateDirectory operation</td>
<td > CreateDirectoryOps</td>
<td >-</td>
<td >Total number of CreateDirectory operations</td>
</tr><tr>
<td >DirectoriesCreated</td>
<td >-</td>
<td >Total number of successful CreateDirectory operations</td>
</tr><tr>
<td rowspan=2>CreateFile operation</td>
<td > CreateFileOps</td>
<td >-</td>
<td >Total number of CreateFile operations</td>
</tr><tr>
<td >FilesCreated</td>
<td >-</td>
<td >Total number of successful CreateFile operations</td>
</tr><tr>
<td rowspan=2>Delete operation</td>
<td >DeletePathOps</td>
<td >-</td>
<td >Total number of Delete operations</td>
</tr><tr>
<td >PathsDeleted</td>
<td >-</td>
<td >Total number of successful Delete operations</td>
</tr><tr>
<td rowspan=2>FreeFile operation</td>
<td > FreeFileOps</td>
<td >-</td>
<td >Total number of FreeFile operations</td>
</tr><tr>
<td >FilesFreed</td>
<td >-</td>
<td >Total number of successful FreeFile operations</td>
</tr><tr>
<td rowspan=2>GetFileBlockInfo operation</td>
<td > GetFileBlockInfoOps</td>
<td >-</td>
<td >Total number of GetFileBlockInfo operations</td>
</tr><tr>
<td >FileBlockInfosGot</td>
<td >-</td>
<td >Total number of successful GetFileBlockInfo operations</td>
</tr><tr>
<td rowspan=2>GetFileInfo operation</td>
<td > GetFileInfoOps</td>
<td >-</td>
<td >Total number of GetFileInfo operations</td>
</tr><tr>
<td >FileInfosGot</td>
<td >-</td>
<td >Total number of successful GetFileInfo operations</td>
</tr><tr>
<td rowspan=2>GetNewBlock operation</td>
<td >GetNewBlockOps</td>
<td >-</td>
<td >Total number of GetNewBlock operations</td>
</tr><tr>
<td >NewBlocksGot</td>
<td >-</td>
<td >Total number of successful GetNewBlock operations</td>
</tr><tr>
<td rowspan=2>Mount operation</td>
<td >MountOps</td>
<td >-</td>
<td >Total number of Mount operations</td>
</tr><tr>
<td >PathsMounted</td>
<td >-</td>
<td >Total number of successful Mount operations</td>
</tr><tr>
<td rowspan=2>Unmount operation</td>
<td >UnmountOps</td>
<td >-</td>
<td >Total number of Unmount operations</td>
</tr><tr>
<td >PathsUnmounted</td>
<td >-</td>
<td >Total number of successful Unmount operations</td>
</tr><tr>
<td rowspan=2>Rename operation</td>
<td >RenamePathOps</td>
<td >-</td>
<td >Total number of Rename operations</td>
</tr><tr>
<td >PathsRenamed</td>
<td >-</td>
<td >Total number of successful Rename operations</td>
</tr><tr>
<td >SetAcl operation</td>
<td >SetAclOps</td>
<td >-</td>
<td >Total number of SetAcl operations</td>
</tr><tr>
<td >SetAttribute operation</td>
<td >SetAttributeOps</td>
<td >-</td>
<td >Total number of SetAttribute operations</td>
</tr><tr>
<td rowspan=2>Total files</td>
<td >FilesPersisted</td>
<td >-</td>
<td >Total number of successfully persisted files</td>
</tr><tr>
<td >FilesPinned</td>
<td >-</td>
<td >Total number of currently pinned files</td>
</tr><tr>
<td >Total file directories</td>
<td >TotalPaths</td>
<td >-</td>
<td >Total number of files and directories in the Alluxio namespace</td>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC </td>
<td >- </td>
<td >Young GC count</td>
</tr><tr>
<td >FGC </td>
<td >- </td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT </td>
<td >s </td>
<td >Full GC time</td>
</tr><tr>
<td >GCT </td>
<td >s </td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT </td>
<td >s </td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >% </td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E </td>
<td >% </td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS </td>
<td >% </td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1 </td>
<td >% </td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O </td>
<td >% </td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M </td>
<td >% </td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td rowspan=7>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB </td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapUsedM </td>
<td >MB </td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM </td>
<td >MB </td>
<td >Size of HeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapInitM </td>
<td >MB</td>
<td >Size of initial JVM HeapMem</td>
</tr><tr>
<td >MemNonHeapInitM </td>
<td >MB</td>
<td >Size of initial JVM NonHeapMem</td>
</tr></table>

### Alluxio - worker
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>Async cache request</td>
<td >AsyncCacheDuplicateRequests</td>
<td >-</td>
<td >Total number of duplicate async cache requests received by worker</td>
</tr><tr>
<td >AsyncCacheRequests</td>
<td >-</td>
<td >Total number of async cache requests received by worker</td>
</tr><tr>
<td rowspan=4>Async cache blocks</td>
<td >AsyncCacheFailedBlocks</td>
<td >-</td>
<td >Total number of failed async cache blocks in worker</td>
</tr><tr>
<td >AsyncCacheRemoteBlocks</td>
<td >-</td>
<td >Total number of blocks that need to be asynchronously cached from remote sources</td>
</tr><tr>
<td >AsyncCacheSucceededBlocks</td>
<td >-</td>
<td >Total number of blocks that were asynchronously cached successfully in the worker</td>
</tr><tr>
<td >AsyncCacheUfsBlocks</td>
<td >-</td>
<td >Total number of blocks that need to be asynchronously cached from local sources</td>
</tr><tr>
<td rowspan=7>Blocks</td>
<td >BlocksAccessed</td>
<td >-</td>
<td >Total number of blocks accessed in worker</td>
</tr><tr>
<td >BlocksCached</td>
<td >-</td>
<td >Total number of blocks used for caching data in worker</td>
</tr><tr>
<td >BlocksCancelled</td>
<td >-</td>
<td >Total number of temporary blocks canceled in worker</td>
</tr><tr>
<td >BlocksDeleted</td>
<td >-</td>
<td >Total number of blocks deleted from worker by external requests</td>
</tr><tr>
<td >BlocksEvicted</td>
<td >-</td>
<td >Total number of blocks evicted from worker</td>
</tr><tr>
<td >BlocksLost</td>
<td >-</td>
<td >Total number of blocks lost in worker</td>
</tr><tr>
<td >BlocksPromoted</td>
<td >-</td>
<td >Total number of blocks moved to a new tier in worker</td>
</tr><tr>
<td rowspan=3>Worker capacity on tiers</td>
<td >CapacityFree</td>
<td >Bytes</td>
<td >Total free bytes on all tiers of worker</td>
</tr><tr>
<td >CapacityTotal</td>
<td >Bytes</td>
<td >Total capacity on all tiers of worker</td>
</tr><tr>
<td >CapacityUsed</td>
<td >Bytes</td>
<td >Total used bytes on all tiers of worker</td>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC </td>
<td >- </td>
<td >Young GC count</td>
</tr><tr>
<td >FGC </td>
<td >- </td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT </td>
<td >s </td>
<td >Full GC time</td>
</tr><tr>
<td >GCT </td>
<td >s </td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT </td>
<td >s </td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >% </td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E </td>
<td >% </td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS </td>
<td >% </td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1 </td>
<td >% </td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O </td>
<td >% </td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M </td>
<td >% </td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td rowspan=7>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB </td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapUsedM </td>
<td >MB </td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM </td>
<td >MB </td>
<td >Size of HeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapInitM </td>
<td >MB</td>
<td >Size of initial JVM HeapMem</td>
</tr><tr>
<td >MemNonHeapInitM </td>
<td >MB</td>
<td >Size of initial JVM NonHeapMem</td>
</tr>
</table>
