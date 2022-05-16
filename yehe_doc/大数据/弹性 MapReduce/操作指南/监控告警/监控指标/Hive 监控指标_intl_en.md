### Hive - HiveMetaStore 
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
<td rowspan=7>JVM memory</td>
<td >MemHeapUsedM </td>
<td >MB </td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM	</td>
<td >MB </td>
<td >Size of HeapMemory committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM HeapMem</td>
</tr><tr>
<td >MemNonHeapUsedM </td>
<td >MB </td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemNonHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM NonHeapMem</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >OpenFileDescriptorCount</td>
<td >-</td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td >MaxFileDescriptorCount</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td rowspan=2>CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >Process CPU utilization</td>
</tr><tr>
<td >SystemCpuLoad</td>
<td >%</td>
<td >System CPU Utilization</td>
</tr><tr>
<td >Percentage of CPU usage time</td>
<td >CPURate</td>
<td >seconds/second</td>
<td >Percentage of CPU usage time</td>
</tr><tr>
<td rowspan=2>Worker threads</td>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads</td>
</tr><tr>
<td >ThreadCount</td>
<td >-</td>
<td >Total number of threads</td>		
</tr><tr>
<td >Cumulative CPU usage time</td>
<td >ProcessCpuTime</td>
<td >ms</td>
<td >Cumulative CPU usage time</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td >GC extra sleep time</td>
<td >ExtraSleepTime</td>
<td >ms/s</td>
<td >GC extra sleep time</td>
</tr>
</table>

### Hive - HiveServer2
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
<td rowspan=7>JVM memory</td>
<td >MemNonHeapUsedM </td>
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
<td >MB </td>
<td >Size of initial JVM HeapMem</td>
</tr><tr>
<td >MemNonHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM NonHeapMem</td>
</tr><tr>
<td >Percentage of used heap memory</td>
<td >MemHeapUsedRate </td>
<td >% </td>
<td >Proportion of the heap memory size currently used by JVM to the heap memory size configured for JVM</td>
</tr><tr>
<td>CPU utilization</td>
<td> ProcessCpuLoad </td>
<td > % </td>
<td >CPU utilization</td>
</tr><tr>
<td>Percentage of CPU usage time</td>
<td> CPUUsedRate </td>
<td > seconds/second</td>
<td >Percentage of CPU usage time</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td>MaxFileDescriptorCount </td>
<td > - </td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td>OpenFileDescriptorCount </td>
<td > - </td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td>Cumulative CPU usage time</td>
<td>ProcessCpuTime </td>
<td > ms </td>
<td >Cumulative CPU usage time</td>
</tr><tr>
<td>Process execution duration</td>
<td> Uptime </td>
<td > s </td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>Worker threads</td>
<td> DaemonThreadCount </td>
<td > - </td>
<td > Number of daemon threads</td>
</tr><tr>
<td> ThreadCount </td>
<td > - </td>
<td >Total number of threads</td>
</tr><tr>
<td rowspan=2> Driver execution latency</td>
<td> 99th_percentile </td>
<td > ms </td>
<td >99th percentile of driver execution latency</td>
</tr><tr>
<td> Avg </td>
<td > ms </td>
<td >Average driver execution latency</td>
</tr><tr>
<td >Open connections</td>
<td>NumOpenConnections </td>
<td > - </td>
<td >Number of open connections</td>
</tr><tr>
<td >Current size of the pool of async HiveServer2 threads</td>
<td >PoolSize </td>
<td > - </td>
<td >Current size of the pool of async HiveServer2 threads</td>
</tr><tr>
<td >Current size of the queue for async HiveServer2 operations</td>
<td>QueueSize </td>
<td > - </td>
<td >Current size of the queue for async HiveServer2 operations</td>
</tr><tr>
<td rowspan=4>Hive operations</td>
<td> Closed </td>
<td > - </td>
<td >Number of closed operations</td>
</tr><tr>
<td>Finished </td>
<td > - </td>
<td >Number of completed operations</td>
</tr><tr>
<td>Canceled </td>
<td > - </td>
<td >Number of canceled operations</td>
</tr><tr>
<td>Error </td>
<td >-</td>
<td >Number of erroneous operations</td>
</tr><tr>
<td>GC extra sleep time</td>
<td> ExtraSleepTime </td>
<td >ms/s</td>
<td >GC extra sleep time</td>
</tr>
</table>

### Hive - HiveWebHcat
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
</tr>
</table>
