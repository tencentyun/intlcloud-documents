### HBase - overview
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>Cluster regions in RIT status</td>
<td >ritCount</td>
<td >-</td>
<td >Number of regions in transition</td>
</tr><tr>
<td >ritCountOverThreshold</td>
<td >-</td>
<td >Number of regions that have been in transition for more than the threshold time</td>
</tr><tr>
<td >Cluster RIT time</td>
<td >ritOldestAge</td>
<td >ms</td>
<td >Age of the longest region in transition</td>
</tr><tr>
<td >Average number of regions per RegionServer</td>
<td >averageLoad</td>
<td >-</td>
<td >Average number of regions per RegionServer</td>
</tr><tr>
<td rowspan=2>Cluster RegionServers</td>
<td >numRegionServers</td>
<td >-</td>
<td >Number of live RegionServers</td>
</tr><tr>
<td >numDeadRegionServers</td>
<td >-</td>
<td >Number of dead RegionServers</td>
</tr><tr>
<td rowspan=2>Data read/written from/to HMaster</td>
<td >receivedBytes</td>
<td >bytes/s</td>
<td >Amount of data received by cluster</td>
</tr><tr>
<td >sentBytes</td>
<td >bytes/s</td>
<td >Amount of data sent by cluster</td>
</tr><tr>
<td >Total cluster API requests</td>
<td >clusterRequests</td>
<td >count/s</td>
<td >Total number of cluster requests</td>
</tr><tr>
<td rowspan=2>Cluster assignment manager operation</td>
<td >Assign_num_ops</td>
<td >-</td>
<td >Number of region assignments</td>
</tr><tr>
<td >BulkAssign_num_ops</td>
<td >-</td>
<td >Number of bulk region assignments</td>
</tr><tr>
<td >Cluster load balancing operations</td>
<td >BalancerCluster_num_ops</td>
<td >-</td>
<td >Number of cluster load balancing operations</td>
</tr>
</table>

### HBase - HMaster
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
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
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM </td>
<td >MB </td>
<td >Non-heap memory size used by process</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Non-heap memory size committed to process</td>
</tr><tr>
<td >MemHeapUsedM </td>
<td >MB </td>
<td >Heap memory size used by process</td>
</tr><tr>
<td >MemHeapCommittedM </td>
<td >MB </td>
<td >Heap memory size committed to process</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Maximum heap memory size available to process</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB </td>
<td >Maximum memory size available to process</td>
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
<td >Number of threads currently in TERMINATED status</td>
</tr><tr>
<td >RPC connections</td>
<td >numOpenConnections</td>
<td >-</td>
<td >Number of RPC connections</td>
</tr><tr>
<td rowspan=6>RPC exceptions</td>
<td >FailedSanityCheckException</td>
<td >-</td>
<td >Number of FailedSanityCheckException exceptions</td>
</tr><tr>
<td >NotServingRegionException</td>
<td >-</td>
<td >Number of NotServingRegionException exceptions</td>
</tr><tr>
<td >OutOfOrderScannerNextException</td>
<td >-</td>
<td >Number of OutOfOrderScannerNextException exceptions</td>
</tr><tr>
<td >RegionMovedException</td>
<td >-</td>
<td >Number of RegionMovedException exceptions</td>
</tr><tr>
<td >RegionTooBusyException</td>
<td >-</td>
<td >Number of RegionTooBusyException exceptions</td>
</tr><tr>
<td >UnknownScannerException</td>
<td >-</td>
<td >Number of UnknownScannerException exceptions</td>
</tr><tr>
<td rowspan=2>RPC queue requests</td>
<td >numCallsInPriorityQueue</td>
<td >-</td>
<td >Number of requests in the general queue</td>
</tr><tr>
<td >numCallsInReplicationQueue</td>
<td >-</td>
<td >Number of RPC requests in the replication queue</td>
</tr><tr>
<td rowspan=2>Process start time</td>
<td >masterActiveTime</td>
<td >s</td>
<td >Master active time</td>
</tr><tr>
<td >masterStartTime</td>
<td >s</td>
<td >Master process start time</td>
</tr>
</table>

### HBase - RegionServer
<table>
<tr>
<th width=23%>Title</th>
<th width=20%>Metric</th>
<th width=12%>Unit</th>
<th width=45%>Description</th>
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
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM </td>
<td >MB </td>
<td >Non-heap memory size used by process</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Non-heap memory size committed to process</td>
</tr><tr>
<td >MemHeapUsedM </td>
<td >MB </td>
<td >Heap memory size used by process</td>
</tr><tr>
<td >MemHeapCommittedM </td>
<td >MB </td>
<td >Heap memory size committed to process</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Maximum heap memory size available to process</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB </td>
<td >Maximum memory size available to process</td>
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
<td >Number of threads currently in TERMINATED status</td>
</tr><tr>
<td >Regions</td>
<td >regionCount</td>
<td >-</td>
<td >Number of regions</td>
</tr><tr>
<td >Region localization</td>
<td >percentFilesLocal  </td>
<td >%</td>
<td >Percentage of HFiles on the local HDFS data node in the region</td>
</tr><tr>
<td >Region replica localization</td>
<td >percentFilesLocalSecondaryRegions</td>
<td >%</td>
<td >Percentage of HFiles on the local HDFS data node in the region replica</td>
</tr><tr>
<td rowspan=2>RPC authentications</td>
<td >authenticationFailures</td>
<td >-</td>
<td >Number of RPC authentication failures</td>
</tr><tr>
<td >authenticationSuccesses</td>
<td >-</td>
<td >Number of RPC authentication successes</td>
</tr><tr>
<td >RPC connections</td>
<td >numOpenConnections</td>
<td >-</td>
<td >Number of RPC connections</td>
</tr><tr>
<td rowspan=6>RPC exceptions</td>
<td >FailedSanityCheckException</td>
<td >-</td>
<td >Number of FailedSanityCheckException exceptions</td>
</tr><tr>
<td >NotServingRegionException</td>
<td >-</td>
<td >Number of NotServingRegionException exceptions</td>
</tr><tr>
<td >OutOfOrderScannerNextException</td>
<td >-</td>
<td >Number of OutOfOrderScannerNextException exceptions</td>
</tr><tr>
<td >RegionMovedException</td>
<td >-</td>
<td >Number of RegionMovedException exceptions</td>
</tr><tr>
<td >RegionTooBusyException</td>
<td >-</td>
<td >Number of RegionTooBusyException exceptions</td>
</tr><tr>
<td >UnknownScannerException</td>
<td >-</td>
<td >Number of UnknownScannerException exceptions</td>
</tr><tr>
<td rowspan=4>RPC handlers</td>
<td >numActiveHandler</td>
<td >-</td>
<td >Number of active RPC handlers</td>
</tr><tr>
<td >numActiveWriteHandler</td>
<td >-</td>
<td >Number of active read RPC handlers</td>
</tr><tr>
<td >numActiveReadHandler</td>
<td >-</td>
<td >Number of active write RPC handlers</td>
</tr><tr>
<td >numActiveScanHandler</td>
<td >-</td>
<td >Number of active scan RPC handlers</td>
</tr><tr>
</tr><tr>
<td rowspan=6>RPC queue requests</td>
<td >numCallsInPriorityQueue</td>
<td >-</td>
<td >Number of requests in the priority queue</td>
</tr><tr>
<td >numCallsInReplicationQueue</td>
<td >-</td>
<td >Number of RPC requests in the replication queue</td>
</tr><tr>
<td >numCallsInPriorityQueue</td>
<td >-</td>
<td >Number of requests in the general queue</td>
</tr><tr>
<td >numCallsInWriteQueue</td>
<td >-</td>
<td >Number of RPC calls in the write call queue</td>
</tr><tr>
<td >numCallsInReadQueue</td>
<td >-</td>
<td >Number of RPC calls in the read call queue</td>
</tr><tr>
<td >numCallsInScanQueue</td>
<td >-</td>
<td >Number of RPC calls in the scan call queue</td>
</tr><tr>
<td >WAL files</td>
<td >hlogFileCount</td>
<td >-</td>
<td >Number of WAL files</td>
</tr><tr>
<td >WAL file size</td>
<td >hlogFileSize</td>
<td >Byte</td>
<td >WAL file size</td>
</tr><tr>
<td >MemStore size</td>
<td >memStoreSize</td>
<td >MB</td>
<td >MemStore size</td>
</tr><tr>
<td >Stores</td>
<td >storeCount</td>
<td >-</td>
<td >Number of stores</td>
</tr><tr>
<td >StoreFiles</td>
<td >storeFileCount</td>
<td >-</td>
<td >Number of StoreFiles</td>
</tr><tr>
<td >StoreFile size</td>
<td >storeFileSize</td>
<td >MB</td>
<td >StoreFile size</td>
</tr><tr>
<td >Disk write rate</td>
<td >flushedCellsSize</td>
<td >bytes/s</td>
<td >Disk write rate</td>
</tr><tr>
<td rowspan=4>Average latency</td>
<td >Append_mean</td>
<td >ms</td>
<td >Average Append latency</td>
</tr><tr>
<td >Replay_mean</td>
<td >ms</td>
<td >Average Replay latency</td>
</tr><tr>
<td >Get_mean</td>
<td >ms</td>
<td >Average GET latency</td>
</tr><tr>
<td >updatesBlockedTime</td>
<td >ms</td>
<td >Number of milliseconds updates have been blocked so the memstore can be flushed</td>
</tr><tr>
<td >RegionServer disk writes</td>
<td >FlushTime_num_ops</td>
<td >-</td>
<td >Number of MemStore flushes</td>
</tr><tr>
<td rowspan=3>Requests in operation queue</td>
<td >splitQueueLength</td>
<td >-</td>
<td >Length of the split queue</td>
</tr><tr>
<td >compactionQueueLength</td>
<td >-</td>
<td >Length of the compaction queue</td>
</tr><tr>
<td >flushQueueLength</td>
<td >-</td>
<td >Length of the region flush queue</td>
</tr><tr>
<td >Replay operations</td>
<td >Replay_num_ops</td>
<td >-</td>
<td >Number of Replay operations</td>
</tr><tr>
<td rowspan=5>Slow operations</td>
<td >slowAppendCount</td>
<td >-</td>
<td >Number of Append requests that took over 1s to complete</td>
</tr><tr>
<td >slowDeleteCount</td>
<td >-</td>
<td >Number of Delete requests that took over 1s to complete</td>
</tr><tr>
<td >slowGetCount</td>
<td >-</td>
<td >Number of Get requests that took over 1s to complete</td>
</tr><tr>
<td >slowIncrementCount</td>
<td >-</td>
<td >Number of Increment requests that took over 1s to complete</td>
</tr><tr>
<td >slowPutCount</td>
<td >-</td>
<td >Number of Put requests that took over 1s to complete</td>
</tr><tr>
<td rowspan=2>Split request</td>
<td >splitRequestCount</td>
<td >-</td>
<td >Number of split requested</td>
</tr><tr>
<td >splitSuccessCount</td>
<td >-</td>
<td >Number of successfully executed splits</td>
</tr><tr>
<td rowspan=3>Cache blocks</td>
<td >blockCacheCount</td>
<td >-</td>
<td >Number of blocks in the block cache</td>
</tr><tr>
<td >blockCacheHitCount</td>
<td >-</td>
<td >Number of block cache hits</td>
</tr><tr>
<td >blockCacheMissCount</td>
<td >-</td>
<td >Number of block cache misses</td>
</tr><tr>
<td >Cache read hit rate</td>
<td >blockCacheExpressHitPercent</td>
<td >%</td>
<td >Cache read hit rate</td>
</tr><tr>
<td >Memory size used by the cache block</td>
<td >blockCacheSize</td>
<td >Byte</td>
<td >Memory size used by the cache block</td>
</tr><tr>
<td rowspan=3>Index size</td>
<td >staticBloomSize</td>
<td >Byte</td>
<td >Uncompressed size of static bloom filters</td>
</tr><tr>
<td >staticIndexSize</td>
<td >Byte</td>
<td >Uncompressed size of static indexes</td>
</tr><tr>
<td >storeFileIndexSize</td>
<td >Byte</td>
<td >Size of indexes in StoreFiles on disk</td>
</tr><tr>
<td rowspan=2>Received bytes</td>
<td >receivedBytes</td>
<td >bytes/s</td>
<td >Received bytes</td>
</tr><tr>
<td >sentBytes</td>
<td >bytes/s</td>
<td >Sent bytes</td>
</tr><tr>
<td rowspan=11>Read and write requests</td>
<td >Total</td>
<td >count/s</td>
<td >Total number of requests. When there are scan requests, this value will be smaller than the sum of read and write requests</td>
</tr><tr>
<td >Read</td>
<td >count/s</td>
<td >Number of read requests</td>
</tr><tr>
<td >Write</td>
<td >count/s</td>
<td >Number of write requests</td>
</tr><tr>
<td >Append_num_ops</td>
<td >count/s</td>
<td >Number of Append requests</td>
</tr><tr>
<td >Mutate_num_ops</td>
<td >count/s</td>
<td >Number of Mutate requests</td>
</tr><tr>
<td >Delete_num_ops</td>
<td >count/s</td>
<td >Number of Delete requests</td>
</tr><tr>
<td >Increment_num_ops</td>
<td >count/s</td>
<td >Number of Increment requests</td>
</tr><tr>
<td >Get_num_ops</td>
<td >count/s</td>
<td >Number of Get requests</td>
</tr>
<tr>
<td >Put_num_ops</td>
<td >count/s</td>
<td >Number of Put requests</td>
</tr>
<tr>
<td >ScanTime_num_ops</td>
<td >count/s</td>
<td >Scan requests (time)</td>
</tr><tr>
<td >ScanSize_num_ops</td>
<td >count/s</td>
<td >Scan requests (size)</td>
</tr>
<tr>
<td >Mutations</td>
<td >mutationsWithoutWALCount</td>
<td >-</td>
<td >Number of mutations</td>
</tr><tr>
<td >Mutation size</td>
<td >mutationsWithoutWALSize</td>
<td >Byte</td>
<td >Mutation size</td>
</tr><tr>
<td >Process start time</td>
<td >regionServerStartTime</td>
<td >s</td>
<td >Process start time</td>
</tr><tr>
<td >Log sync</td>
<td >   source.sizeOfLogQueue</td>
<td >-</td>
<td >Total length of synced logs </td>
</tr><tr>
<td >Sync duration</td>
<td >   source.ageOfLastShippedOp</td>
<td >ms</td>
<td >Sync duration</td>
</tr><tr>
<td rowspan=2>Requests</td>
<td >   ReadRequestCount</td>
<td >   count/s</td>
<td >Read requests/s</td>
</tr><tr>
<td >   WriteRequestCount</td>
<td >   count/s</td>
<td >Write requests/s</td>
</tr><tr>
<td rowspan=2>Requests</td>
<td >   Read</td>
<td >   count/s</td>
<td >Read requests/s</td>
</tr><tr>
<td >   Write</td>
<td >   count/s</td>
<td >Write requests/s</td>
</tr><tr>
<td rowspan=2>Store size</td>
<td >   memstoreSize</td>
<td >   Byte</td>
<td >MemStore size</td>
</tr><tr>
<td >  storeFileSize</td>
<td >  Byte</td>
<td>StoreFile size</td>
</tr><tr>
<td rowspan=6>Table-level request latency</td>      
<td >getTime_99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td >scanTime_99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td >putTime_99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td >incrementTime_99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td >appendTime_99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td >deleteTime_99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td rowspan=2>Request processing latency</td>
<td >99th_percentile</td>
<td >ms</td>
<td >99th percentile of request processing latency</td>
</tr><tr>
<td >99.9th_percentile</td>
<td >ms</td>
<td >99.9% request processing latency</td>
</tr><tr>
<td rowspan=2>Request queueing latency</td>
<td >99th_percentile</td>
<td >ms</td>
<td >99th percentile of request queueing latency</td>
</tr><tr>
<td >99.9th_percentile</td>
<td >ms</td>
<td >99.9% request queueing latency</td>
</tr><tr>
<td rowspan=3>Scan size</td>
<td >max</td>
<td >bytes</td>
<td >Maximum scan size</td>
</tr><tr>
<td >mean</td>
<td >bytes</td>
<td >Average scan size</td>
</tr><tr>
<td >min</td>
<td >bytes</td>
<td >Minimum scan size</td>
</tr><tr>
<td rowspan=3>Scan time</td>
<td >max</td>
<td >s</td>
<td >Maximum scan time</td>
</tr><tr>
<td >mean</td>
<td >s</td>
<td >Average scan time</td>
</tr><tr>
<td >min</td>
<td >s</td>
<td >Minimum scan time</td>
</tr>	
</table>
