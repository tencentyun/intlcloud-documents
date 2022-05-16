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
<td rowspan=2>CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >Process CPU utilization</td>
</tr><tr>
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
<td rowspan=2>CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >Process CPU utilization</td>
</tr><tr>
<td >SystemCpuLoad</td>
<td >-</td>
<td >System CPU Utilization</td>
</tr>
<tr>
<td >Beeswax API client connections</td>
<td >Use</td>
<td >-</td>
<td >Number of active Beeswax API connections</td>
</tr>
<tr>
<td >HiveServer2 API client connections</td>
<td >Use</td>
<td >-</td>
<td >Number of active HiveServer2 API connections</td>
</tr>
</table>

