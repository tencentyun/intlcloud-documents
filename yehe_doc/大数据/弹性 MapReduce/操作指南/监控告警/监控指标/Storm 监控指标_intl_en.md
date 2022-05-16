### Storm - Nimbus
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
<td >	Young GC count</td>
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
<td >S0 </td>
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
<td >MemHeapCommittedM </td>
<td >MB </td>
<td >Size of HeapMemory committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>		
<td >MemHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM HeapMemory</td>
</tr><tr>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >	Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Size of NonHeapMemory committed by JVM</td>
</tr><tr>
<td >MemNonHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM NonHeapMemory</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >OpenFileDescriptorCount </td>
<td > - </td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td >MaxFileDescriptorCount </td>
<td > - </td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >CPU utilization</td>
<td >ProcessCpuLoad </td>
<td >% </td>
<td >Process CPU utilization</td>
</tr><tr>
<td rowspan=3>Worker threads</td>
<td >DaemonThreadCount </td>
<td > - </td>
<td >Number of daemon threads</td>
</tr><tr>
<td >PeakThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >ThreadCount </td>
<td > - </td>
<td >Total number of threads</td>
</tr><tr>
<td >Cumulative CPU usage time</td>
<td >ProcessCpuTime </td>
<td >ms </td>
<td >Cumulative CPU usage time</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime </td>
<td >s </td>
<td >Process execution duration</td>
</tr>
</table>

### Storm - supervisor
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
<td >	Young GC count</td>
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
<td >S0 </td>
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
<td >MemHeapCommittedM </td>
<td >MB </td>
<td >Size of HeapMemory committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM </td>
<td >MB </td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>		
<td >MemHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM HeapMemory</td>
</tr><tr>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >	Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM </td>
<td >MB </td>
<td >Size of NonHeapMemory committed by JVM</td>
</tr><tr>
<td >MemNonHeapInitM </td>
<td >MB </td>
<td >Size of initial JVM NonHeapMemory</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >OpenFileDescriptorCount </td>
<td > - </td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td >MaxFileDescriptorCount </td>
<td > - </td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >CPU utilization</td>
<td >ProcessCpuLoad </td>
<td >% </td>
<td >Process CPU utilization</td>
</tr><tr>
<td rowspan=3>Worker threads</td>
<td >DaemonThreadCount </td>
<td > - </td>
<td >Number of daemon threads</td>
</tr><tr>
<td >PeakThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>
<td >ThreadCount </td>
<td > - </td>
<td >Total number of threads</td>
</tr><tr>
<td >Cumulative CPU usage time</td>
<td >ProcessCpuTime </td>
<td >ms </td>
<td >Cumulative CPU usage time</td>
</tr><tr>
<td >Process execution duration</td>
<td >Uptime </td>
<td >s </td>
<td >Process execution duration</td>
</tr>
</table>
