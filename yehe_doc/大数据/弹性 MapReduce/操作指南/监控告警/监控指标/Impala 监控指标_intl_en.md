>! Currently, only Impala v3.4.0 and later support Impala metrics.
### Impala - catalog
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td >Resident set size</td>
<td >RSS</td>
<td >bytes</td>
<td >Resident set size</td>
</tr><tr>
<td rowspan=7>JVM memory</td>
<td >MemHeapInitM</td>
<td >MB</td>
<td >Peak size of initial JVM HeapMemory</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Size of HeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapInitM</td>
<td >MB</td>
<td >Size of initial JVM NonHeapMemory</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td rowspan=5>Interval between heartbeats from the daemon process to StateStore</td>
<td >Last</td>
<td >s</td>
<td >Latest interval between heartbeats from the daemon process to StateStore</td>
</tr><tr>
<td >Max</td>
<td >s</td>
<td >Maximum interval between heartbeats from the daemon process to StateStore</td>
</tr><tr>
<td >Mean</td>
<td >s</td>
<td >Average interval between heartbeats from the daemon process to StateStore</td>
</tr><tr>
<td >Min</td>
<td >s</td>
<td >Minimum interval between heartbeats from the daemon process to StateStore</td>
</tr><tr>
<td >Stddev</td>
<td >s</td>
<td >Standard deviation in the interval between heartbeats from the daemon process to StateStore</td>
</tr><tr>
<td rowspan=5>TCMalloc memory</td>
<td >Used</td>
<td >bytes</td>
<td >Number of bytes used by the program</td>
</tr><tr>
<td >PageheapFreeBytes</td>
<td >bytes</td>
<td >Number of bytes of free mapped pages in the page heap</td>
</tr><tr>
<td >PageheapUnmappedBytes</td>
<td >bytes</td>
<td >Number of bytes of free unmapped pages in the page heap</td>
</tr><tr>
<td >PhysicalBytesReserved</td>
<td >bytes</td>
<td >Amount of physical memory used by the process</td>
</tr><tr>
<td >TotalBytesReserved</td>
<td >bytes</td>
<td >Number of bytes of system memory reserved by TCMalloc</td>
</tr><tr>
<td >Active connections</td>
<td >Thrift_Server_Connections_Used</td>
<td >-</td>
<td >Number of active connections</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >MaxFileDescriptorCount</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >OpenFileDescriptorCount</td>
<td >-</td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td rowspan=2>Threads</td>
<td >ThreadCount</td>
<td >-</td>
<td >Total number of threads</td>
</tr><tr>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads</td>
</tr><tr>
<td rowspan=1>CPU utilization</td>
<td >SystemCpuLoad</td>
<td >-</td>
<td >System CPU Utilization</td>
</tr></table>

### Impala - StateStore
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td >Resident set size</td>
<td >RSS</td>
<td >bytes</td>
<td >Resident set size</td>
</tr><tr>
<td rowspan=5>TCMalloc memory</td>
<td >Used</td>
<td >bytes</td>
<td >Number of bytes used by the program</td>
</tr><tr>
<td >PageheapFreeBytes</td>
<td >bytes</td>
<td >Number of bytes of free mapped pages in the page heap</td>
</tr><tr>
<td >PageheapUnmappedBytes</td>
<td >bytes</td>
<td >Number of bytes of free unmapped pages in the page heap</td>
</tr><tr>
<td >PhysicalBytesReserved</td>
<td >bytes</td>
<td >Amount of physical memory used by the process</td>
</tr><tr>
<td >TotalBytesReserved</td>
<td >bytes</td>
<td >Number of bytes of system memory reserved by TCMalloc</td>
</tr><tr>
<td >Connections</td>
<td >Used</td>
<td >-</td>
<td >Number of active connections</td>
</tr><tr>
<td >Running threads</td>
<td >Count</td>
<td >-</td>
<td >Number of running threads</td>
</tr><tr>
<td >StateStore subscribers</td>
<td >Count</td>
<td >-</td>
<td >Number of StateStore subscribers</td>
</tr></table>

### Impala - daemon
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=7>JVM memory</td>
<td >MemHeapInitM</td>
<td >MB</td>
<td >Peak size of initial JVM HeapMemory</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Size of HeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapInitM</td>
<td >MB</td>
<td >Size of initial JVM NonHeapMemory</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td rowspan=5>TCMalloc memory</td>
<td >Used</td>
<td >bytes</td>
<td >Number of bytes used by the program</td>
</tr><tr>
<td >PageheapFreeBytes</td>
<td >bytes</td>
<td >Number of bytes of free mapped pages in the page heap</td>
</tr><tr>
<td >PageheapUnmappedBytes</td>
<td >bytes</td>
<td >Number of bytes of free unmapped pages in the page heap</td>
</tr><tr>
<td >PhysicalBytesReserved</td>
<td >bytes</td>
<td >Amount of physical memory used by the process</td>
</tr><tr>
<td >TotalBytesReserved</td>
<td >bytes</td>
<td >Number of bytes of system memory reserved by TCMalloc</td>
</tr><tr>
<td rowspan=2>Threads</td>
<td >ThreadCount</td>
<td >-</td>
<td >Total number of threads</td>
</tr><tr>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >MaxFileDescriptorCount</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >OpenFileDescriptorCount</td>
<td >-</td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td rowspan=1>CPU utilization</td>
<td >SystemCpuLoad</td>
<td >-</td>
<td >System CPU Utilization</td>
</tr>
<tr>
<td rowspan=4>Beeswax API client connections</td>
<td >Use</td>
<td >-</td>
<td >Number of active Beeswax API connections</td>
</tr><tr>
<td >Conn_In_Use</td>
<td >-</td>
<td >Number of active Beeswax API connections to this Impala daemon</td>
</tr>
<tr>
<td >TotalConns</td>
<td >-</td>
<td >Total number of active Beeswax API connections to this Impala daemon</td>
</tr>
<tr>
<td >ConnSetupQueueSize</td>
<td >-</td>
<td >Number of Beeswax API connections that this Impala daemon has received and are waiting to establish</td>
</tr>
<tr>
<td rowspan=4>HS2 API client connections</td>
<td >Use</td>
<td >-</td>
<td >Number of active HS2 API connections</td>
</tr><tr>
<td >Conn_In_Use</td>
<td >-</td>
<td >Number of active HS2 API connections</td>
</tr>
<tr>
<td >TotalConns</td>
<td >-</td>
<td >Total number of HS2 API connections this Impala daemon has established during the lifecycle</td>
</tr>
<tr>
<td >ConnSetupQueueSize</td>
<td >-</td>
<td >Number of HS2 API connections that this Impala daemon has received and are waiting to establish</td>
</tr>
<tr>
<td rowspan=2>Thread manager</td>
<td >RunningThreads</td>
<td >-</td>
<td >Number of running threads</td>
</tr><tr>
<td >TotalCreatedThreads</td>
<td >-</td>
<td >Number of threads created during the lifecycle</td>
</tr>
<tr>
<td rowspan=1>Memory manager limit</td>
<td >Limit</td>
<td >Bytes</td>
<td >Memory beyond the memory limit (default value: -1)</td>
</tr><tr>
<td rowspan=1>Amount of memory beyond the memory limit (default value: -1)</td>
<td >OverLimit</td>
<td >Bytes</td>
<td >Number of threads created during the lifecycle</td>
</tr>
<tr>
<td rowspan=6>HS2 API client wait time for connection establishment</td>
<td >P20</td>
<td rowspan=6>us</td>
<td rowspan=6>HS2 API client wait time for connection establishment</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr>
<tr>
<td rowspan=6>Beeswax API client wait time for service thread establishment</td>
<td >P20</td>
<td rowspan=6>us</td>
<td rowspan=6>Beeswax API client wait time for service thread establishment</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr>
<tr>
<td rowspan=1>Timed-out Beeswax API connections</td>
<td >TimeOutCnncRequests</td>
<td >-</td>
<td >Number of timed-out Beeswax API connections</td>
</tr><tr>
<td rowspan=1>Time spent parsing requests from request pool (milliseconds)</td>
<td >Total</td>
<td >ms</td>
<td >Time spent parsing requests from request pool (milliseconds)</td>
</tr><tr>
<td rowspan=1>Cache misses in external data source cache class</td>
<td >Misses</td>
<td >-</td>
<td >Number of cache misses in external data source cache class</td>
</tr><tr>
<td rowspan=1>Impala backend server connection requests that timed out waiting for setup</td>
<td >ConnSetupQueueSize</td>
<td >-</td>
<td >Number of Impala backend server connection requests that timed out waiting for setup</td>
</tr><tr>
<td rowspan=1>Impala backend connection requests that timed out waiting for setup</td>
<td >TimeOutCnncRequests</td>
<td >-</td>
<td >Number of Impala backend connection requests that timed out waiting for setup</td>
</tr>
<tr>
<td rowspan=1>Total Impala backend client connections to this Impala daemon</td>
<td >TotalConnections</td>
<td >-</td>
<td >Total number of Impala backend client connections to this Impala daemon</td>
</tr>
<tr>
<td rowspan=8>Time spent by Impala backend client waiting for connection establishment</td>
<td >P20</td>
<td rowspan=8>us</td>
<td rowspan=8>Time spent by Impala backend client waiting for connection establishment</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr><tr>
<td >Count</td>
</tr>
<tr>
<td >Sum</td>
</tr>
<tr>
<td rowspan=8>Time spent by Impala backend client waiting for service thread</td>
<td >P20</td>
<td rowspan=8>us</td>
<td rowspan=8>Time spent by Impala backend client waiting for service thread</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr><tr>
<td >Count</td>
</tr>
<tr>
<td >Sum</td>
</tr><tr>
<td rowspan=8>HS2 API client wait time for service thread establishment</td>
<td >P20</td>
<td rowspan=8>us</td>
<td rowspan=8>HS2 API client wait time for service thread establishment</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr><tr>
<td >Count</td>
</tr>
<tr>
<td >Sum</td>
</tr><tr>
<td rowspan=8>HS2 HTTP API client wait time for service thread</td>
<td >P20</td>
<td rowspan=8>us</td>
<td rowspan=8>HS2 HTTP API client wait time for service thread</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr><tr>
<td >Count</td>
</tr>
<tr>
<td >Sum</td>
</tr>
<tr>
<td >DataStreamService: Rejected service queue overflows </td>
<td >RpcsQueueOverflow</td>
<td >-</td>
<td >DataStreamService: Number of rejected service queue overflows </td>
</tr>
<tr>
<td >ControlStreamService: Rejected service queue overflows </td>
<td >RpcsQueueOverflow</td>
<td >-</td>
<td >ControlStreamService: Number of rejected service queue overflows </td>
</tr>
<tr>
<td rowspan=2>DataStreamService: Used bytes</td>
<td >PeakUsageBytes</td>
<td >Bytes</td>
<td >Peak number of bytes used by Memtracker DataStreamService</td>
</tr><tr>
<td >CurrentUsageBytes</td>
<td >Bytes</td>
<td >Current number of bytes used by Memtracker DataStreamService</td>
</tr>
<tr>
<td rowspan=2>ControlService: Used bytes</td>
<td >PeakUsageBytes</td>
<td >Bytes</td>
<td >Peak number of bytes used by Memtracker ControlService</td>
</tr><tr>
<td >CurrentUsageBytes</td>
<td >Bytes</td>
<td >Current number of bytes used by Memtracker ControlService</td>
</tr>
<tr>
<td >Resident set size (RSS) for this process</td>
<td >RSS</td>
<td >Bytes</td>
<td >Resident set size (RSS) for this process</td>
</tr>
<tr>
<td >Total backends registered in StateStore</td>
<td >Total</td>
<td rowspan=1>-</td>
<td rowspan=1>Total number of backends registered in StateStore</td>
</tr>
<tr>
<td rowspan=8>Query release delay</td>
<td >P20</td>
<td rowspan=8>us</td>
<td rowspan=8>Query release delay</td>
</tr>
<tr>
<td >P50</td>
</tr>
<tr>
<td >P70</td>
</tr><tr>
<td >P90</td>
</tr>
<tr>
<td >P95</td>
</tr>
<tr>
<td >P99.9</td>
</tr><tr>
<td >Count</td>
</tr>
<tr>
<td >Sum</td>
</tr>
<tr>
<td >Opened HDFS filed</td>
<td >NumFilesOpenForInsert</td>
<td >-</td>
<td >Number of opened HDFS files</td>
</tr>
<tr>
<td >Scan range read during the lifecycle of the process</td>
<td >ScanRangesTotal</td>
<td >-</td>
<td >Scan range read during the lifecycle of the process</td>
</tr>
<tr>
<td >Opened Beeswax sessions</td>
<td >NumOpenBeeswaxSessions</td>
<td >-</td>
<td >Number of opened Beeswax sessions</td>
</tr>
<tr>
<td >Total query fragments processed during the lifecycle of the process</td>
<td >NumFragments</td>
<td >-</td>
<td >Total number of query fragments processed during the lifecycle of the process</td>
</tr>
<tr>
<td >Total scan ranges read during the lifecycle of the process without volume metadata</td>
<td >ScanRangesNumMissingVolumId</td>
<td >-</td>
<td >Total number of scan ranges read during the lifecycle of the process without volume metadata</td>
</tr>
<tr>
<td >Hedged read attempts</td>
<td >HedgedReadOps</td>
<td >-</td>
<td >Number of hedged read attempts</td>
</tr>
<tr>
<td >Total queries processed during the lifecycle of the process</td>
<td >NumQueries</td>
<td >-</td>
<td >Total number of queries processed during the lifecycle of the process</td>
</tr>
<tr>
<td >Total rows supporting caching HS2 FETCH_FIRST</td>
<td >ResultSetCacheTotalNumRows</td>
<td >-</td>
<td >Total number of rows supporting caching HS2 FETCH_FIRST</td>
</tr><tr>
<td >Total queries registered on this Impala server</td>
<td >NumQueriesRegistered</td>
<td >-</td>
<td >Total number of queries registered on this Impala server</td>
</tr>
<tr>
<td >Total backend queries</td>
<td >NumQueriesExecuted</td>
<td >-</td>
<td >Total number of backend queries</td>
</tr>
<tr>
<td >Sessions terminated due to inactivity</td>
<td >NumSessionsExpired</td>
<td >-</td>
<td >Number of sessions terminated due to inactivity</td>
</tr>
<tr>
<td >Queries terminated due to inactivity</td>
<td >NumQueriesExpired</td>
<td >-</td>
<td >Number of queries terminated due to inactivity</td>
</tr>
<tr>
<td >Opened HS2 sessions</td>
<td >NumOpenHS2Sessions</td>
<td >-</td>
<td >Number of opened HS2 sessions</td>
</tr>
<tr>
<td >Tables in catalog</td>
<td >NumTables</td>
<td >-</td>
<td >	Number of tables in catalog</td>
</tr>
<tr>
<td >Databases in catalog</td>
<td >NumDatabases</td>
<td >-</td>
<td >	Number of databases in catalog</td>
</tr>
<tr>
<td >Bytes written to the disk by the I/O manager</td>
<td >BytesWritten</td>
<td >-</td>
<td >	Number of bytes written to the disk by the I/O manager</td>
</tr>
<tr>
<td >Files opened by the I/O manager</td>
<td >NumOpenFiles</td>
<td >-</td>
<td >Number of files opened by the I/O manager</td>
</tr>
<tr>
<td >Used HDFS file handles</td>
<td >NumFileHandlesOutstanding</td>
<td >Bytes</td>
<td >Number of used HDFS file handles</td>
</tr>
<tr>
<td >Read local bytes</td>
<td >LocalBytesRead</td>
<td >Bytes</td>
<td >Number of local bytes read by the I/O manager</td>
</tr>
</table>


	
	
	
	

			
			
