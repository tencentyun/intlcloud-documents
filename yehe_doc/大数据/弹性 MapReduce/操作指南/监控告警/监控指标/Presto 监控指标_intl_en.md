### Presto - overview
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=3>Nodes</td>
<td>Active</td>
<td >-</td>
<td >Number of active nodes</td>
</tr><tr>
<td >Total</td>
<td >-</td>
<td >Total number of nodes</td>
</tr><tr>
<td >Failed</td>
<td >-</td>
<td >Number of failed nodes</td>
</tr><tr>
<td rowspan=2>Query</td>
<td >RunningQueries</td>
<td >-</td>
<td >Total number of running queries</td>
</tr><tr>
<td >QueuedQueries</td>
<td >-</td>
<td >Total number of waiting queries</td>
</tr><tr>
<td  rowspan=5>Query frequency</td>
<td >FailedQueries</td>
<td >count/min</td>
<td >Total number of failed queries</td>
</tr><tr>
<td >AbandonedQueries</td>
<td >count/min</td>
<td >Total number of abandoned queries</td>
</tr><tr>
<td >CanceledQueries</td>
<td >count/min</td>
<td >Total number of canceled queries</td>
</tr><tr>
<td >CompletedQueries</td>
<td >count/min</td>
<td >Total number of completed queries</td>
</tr><tr>	
<td >StartedQueries</td>
<td >count/min</td>
<td >Total number of started queries</td>
</tr><tr>	
<td rowspan=2>Data volume input/output per minute</td>
<td >InputDataSizeOneMinute</td>
<td >GB/min</td>
<td >Data input rate</td>
</tr><tr>
<td >OutputDataSizeOneMinute</td>
<td >GB/min</td>
<td >Data output rate</td>
</tr>
</table>

### Presto - worker
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
<td rowspan=2>Data input/output rate</td>
<td >InputDataSize.OneMinute.Rate </td>
<td >GB/min </td>
<td >Data input rate</td>
</tr><tr>
<td >OutputDataSize.OneMinute.Rate</td>
<td >GB/min </td>
<td >Data output rate</td>
</tr><tr>
<td rowspan=3>Processes</td>
<td >PeakThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >ThreadCount</td>
<td > - </td>
<td >Number of threads</td>
</tr><tr>
<td >DaemonThreadCount</td>
<td > - </td>
<td >Number of backend threads</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td >Process start time</td>
<td >StartTime</td>
<td >s</td>
<td >Process start time</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >MaxFileDescriptorCount</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >OpenFileDescriptorCount</td>
<td >-</td>
<td >Number of opened file descriptors</td>
</tr>
</table >

### Presto - coordinator
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
<td rowspan=3>Processes</td>
<td >PeakThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >ThreadCount</td>
<td > - </td>
<td >Number of threads</td>
</tr><tr>
<td >DaemonThreadCount</td>
<td > - </td>
<td >Number of backend threads</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td >Process start time</td>
<td >StartTime</td>
<td >s</td>
<td >Process start time</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >MaxFileDescriptorCount</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >OpenFileDescriptorCount</td>
<td >-</td>
<td >Number of opened file descriptors</td>
</tr>
</table >
