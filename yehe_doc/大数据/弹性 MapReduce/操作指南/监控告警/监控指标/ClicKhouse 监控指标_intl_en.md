### ClickHouse - metrics
<table>
<tr>
<th width=25%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>Network connections</td>
<td >tcp</td>
<td >-</td>
<td >Number of TCP server connections</td>
</tr><tr>
<td >http</td>
<td >-</td>
<td >Number of HTTP server connections</td>
</tr><tr>
<td >ZooKeeper event subscriptions</td>
<td >watches</td>
<td >-</td>
<td >Number of ZooKeeper event subscriptions</td>
</tr><tr>
<td >Ephemeral nodes held in ZooKeeper</td>
<td >ephemeralNode</td>
<td >-</td>
<td >Number of ephemeral nodes held in ZooKeeper</td>
</tr><tr>
<td rowspan=2>Active tasks in BackgroundPool</td>
<td >backgroundPoolTask</td>
<td >-</td>
<td >Number of active tasks in BackgroundProcessingPool</td>
</tr><tr>
<td >backgroundSchedulePoolTask</td>
<td >-</td>
<td >Number of active tasks in BackgroundSchedulePool</td>
</tr><tr>
<td >Threads waiting for locks in Context</td>
<td >contextLockWait</td>
<td >-</td>
<td >Number of threads waiting for locks in Context</td>
</tr><tr>
<td >Throttled INSERT queries</td>
<td >delayedInserts</td>
<td >-</td>
<td >Number of throttled INSERT queries</td>
</tr><tr>
<td >Requests in fly to data sources of dictionaries of cache type</td>
<td >dictCacheRequests</td>
<td >-</td>
<td >Number of requests in fly to data sources of dictionaries of cache type</td>
</tr><tr>
<td >Pending files to process for asynchronous insertion into distributed tables</td>
<td >distributedSend</td>
<td >-</td>
<td >Number of pending files to process for asynchronous insertion into distributed tables</td>
</tr><tr>
<td rowspan=4>Threads</td>
<td >global</td>
<td >-</td>
<td >Number of threads in the global thread pool</td>
</tr><tr>
<td >globalActive</td>
<td >-</td>
<td >Number of active threads in the global thread pool</td>
</tr><tr>
<td >local</td>
<td >-</td>
<td >Number of threads in the local thread pool</td>
</tr><tr>
<td >localActive</td>
<td >-</td>
<td >Number of active threads in the local thread pool</td>
</tr><tr>
<td >Replicas participating in leader election</td>
<td >leaderElection</td>
<td >-</td>
<td >Number of replicas participating in leader election</td>
</tr><tr>
<td rowspan=2>Replicated tables</td>
<td >leaderReplica</td>
<td >-</td>
<td >Number of replicated tables that are leaders</td>
</tr><tr>
<td >readonlyReplica</td>
<td >-</td>
<td >Number of replicated tables in read-only status</td>
</tr><tr>
<td rowspan=4>Total allocated memory size</td>
<td >memoryTracking</td>
<td >GB</td>
<td >Total memory size allocated to queries being executed</td>
</tr><tr>
<td >backgroundProcessingPool</td>
<td >GB</td>
<td >Total memory size allocated to the background processing pool</td>
</tr><tr>
<td >backgroundSchedulePool</td>
<td >GB</td>
<td >Total memory size allocated to the background scheduling pool</td>
</tr><tr>
<td >memoryTrackingForMerges</td>
<td >GB</td>
<td >Total memory size allocated to background merges</td>
</tr><tr>
<td >Merges being executed in the background</td>
<td >merge</td>
<td >-</td>
<td >Number of merges being executed in the background</td>
</tr><tr>
<td rowspan=2>Opened files</td>
<td >read</td>
<td >-</td>
<td >Number of opened readable files</td>
</tr><tr>
<td >write</td>
<td >-</td>
<td >Number of opened writable files</td>
</tr><tr>
<td >Table changes</td>
<td >partMutation</td>
<td >-</td>
<td >Number of table changes</td>
</tr><tr>
<td >Query processing threads</td>
<td >queryThread</td>
<td >-</td>
<td >Number of query processing threads</td>
</tr><tr>
<td >Stopped or waiting queries</td>
<td >queryPreempted</td>
<td >-</td>
<td >Number of stopped or waiting queries</td>
</tr><tr>
<td rowspan=2>System calls</td>
<td >read</td>
<td >-</td>
<td >Number of read system calls</td>
</tr><tr>
<td >write</td>
<td >-</td>
<td >Number of write system calls</td>
</tr><tr>
<td rowspan=3>Blocks</td>
<td >fetch</td>
<td >-</td>
<td >Number of blocks collected from replicas</td>
</tr><tr>
<td >send</td>
<td >-</td>
<td >Number of blocks sent to replicas</td>
</tr><tr>
<td >check</td>
<td >-</td>
<td >Number of blocks for consistency check</td>
</tr><tr>
<td >Server change</td>
<td >revision</td>
<td >-</td>
<td >Number of server changes</td>
</tr><tr>
<td >Version number</td>
<td >version</td>
<td >1</td>
<td >Version number</td>
</tr><tr>
<td rowspan=4>Threads waiting for read/write locks</td>
<td >waitingRead</td>
<td >-</td>
<td >Number of threads waiting for read/write locks to read from tables</td>
</tr><tr>
<td >waitingWrite</td>
<td >-</td>
<td >Number of threads waiting for read/write locks to write to tables</td>
</tr><tr>
<td >activeRead</td>
<td >-</td>
<td >Number of threads holding read locks on tables</td>
</tr><tr>
<td >activeWrite</td>
<td >-</td>
<td >Number of threads holding write locks on tables</td>
</tr><tr>
<td >Rows in buffer tables</td>
<td >storageBufferRows</td>
<td >-</td>
<td >Number of rows in buffer tables</td>
</tr><tr>
<td >Bytes in buffer tables</td>
<td >storageBufferBytes</td>
<td >MB</td>
<td >Number of bytes in buffer tables</td>
</tr>
</table>

### ClickHouse - events
<table>
<tr>
<th width=25%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=3>Queries</td>
<td >total</td>
<td >-</td>
<td >Total number of queries that may be executed</td>
</tr><tr>
<td >select</td>
<td >-</td>
<td >Number of SELECT queries that may be executed</td>
</tr><tr>
<td >insert</td>
<td >-</td>
<td >Number of INSERT queries that may be executed</td>
</tr><tr>
<td >Inserted rows</td>
<td >insertedRows</td>
<td >-</td>
<td >Number of rows inserted into all tables</td>
</tr><tr>
<td >Inserted bytes</td>
<td >insertedBytes</td>
<td >-</td>
<td >Number of bytes inserted into all tables</td>
</tr><tr>
<td rowspan=2>Total time waiting for system calls</td>
<td >read</td>
<td >μs</td>
<td >Total time waiting for read system calls</td>
</tr><tr>
<td >write</td>
<td >μs</td>
<td >Total time waiting for write system calls</td>
</tr><tr>
<td >Opened files</td>
<td >fileOpen</td>
<td >-</td>
<td >Number of opened files</td>
</tr><tr>
<td rowspan=2>Reads/Writes from/to file descriptors</td>
<td >read</td>
<td >-</td>
<td >Number of reads from file descriptors</td>
</tr><tr>
<td >write</td>
<td >-</td>
<td >Number of writes to file descriptors</td>
</tr><tr>
<td  rowspan=2>Bytes read/written from/to file descriptors</td>
<td >read</td>
<td >MB</td>
<td >Number of bytes read from file descriptors</td>
</tr><tr>
<td >write</td>
<td >MB</td>
<td >Number of bytes written to file descriptors</td>
</tr><tr>
<td rowspan=3>Total time processing threads</td>
<td >realtime</td>
<td >μs</td>
<td >Total time processing threads</td>
</tr><tr>
<td >user</td>
<td >μs</td>
<td >Total time processing threads executing CPU instructions in user space</td>
</tr><tr>
<td >system</td>
<td >μs</td>
<td >Total time processing threads executing CPU instructions in OS kernel space</td>
</tr><tr>
<td >Compiled regular expressions</td>
<td >regexpCreated</td>
<td >-</td>
<td >Number of compiled regular expressions</td>
</tr>
</table>

### ClickHouse - asynchronous metrics

<table>
<tr>
<th width=25%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td >Size of cache of marks of StorageMergeTree</td>
<td >markCacheBytes</td>
<td >MB</td>
<td >Size of cache of marks of StorageMergeTree</td>
</tr><tr>
<td >Cache files of marks of StorageMergeTree</td>
<td >markCacheFiles</td>
<td >-</td>
<td >Number of cache files of marks of StorageMergeTree</td>
</tr><tr>
<td >Maximum number of active blocks</td>
<td >maxPartCountForPartition</td>
<td >-</td>
<td >Number of largest active data blocks in partition</td>
</tr><tr>
<td >Databases</td>
<td >databaseCount</td>
<td >-</td>
<td >Number of databases</td>
</tr><tr>
<td >Data tables</td>
<td >tableCount</td>
<td >-</td>
<td >Number of data tables</td>
</tr><tr>
<td rowspan=2>Maximum replica latency</td>
<td >absolute</td>
<td >μs</td>
<td >Maximum replica queue latency</td>
</tr><tr>
<td >relative</td>
<td >μs</td>
<td >Maximum difference of the absolute latency from other blocks</td>
</tr><tr>
<td >Size of the queue for the operations to be performed</td>
<td >replicasMaxQueueSize</td>
<td >-</td>
<td >Size of the queue for the operations to be performed</td>
</tr>
</table>
