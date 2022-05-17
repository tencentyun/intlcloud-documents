### ZooKeeper

<table>
<thread>
<tr>
<th width=18%>Title</th>
<th width=20%>Metric</th>
<th width=22%>Unit</th>
<th width=40%>Description</th>
</tr></thread>
<tbody><tr>
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
<td >CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >CPU utilization</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td >zk_max_file_descriptor_count</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >zk_open_file_descriptor_count</td>
<td >-</td>
<td >Number of opened file descriptors</td>
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
<td rowspan=2>Worker threads</td>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads</td>
</tr><tr>
<td >ThreadCount</td>
<td >-</td>
<td >Total number of threads</td>
</tr><tr>
<td >Connections</td>
<td >zk_num_alive_connections</td>
<td >-</td>
<td >Number of current connections</td>
</tr><tr>
<td rowspan=3>Latency</td>
<td >zk_avg_latency</td>
<td >ms</td>
<td >Average ZooKeeper processing latency</td>
</tr><tr>
<td >zk_max_latency</td>
<td >ms</td>
<td >Maximum ZooKeeper processing latency</td>
</tr><tr>
<td >zk_min_latency</td>
<td >ms</td>
<td >Minimum ZooKeeper processing latency</td>
</tr><tr>
<td rowspan=3>Zondes</td>
<td >zk_watch_count</td>
<td >-</td>
<td >Number of ZooKeeper watches</td></tr><tr>
<td >zk_znode_count</td>
<td >-</td>
<td >Number of ZooKeeper znodes</td></tr><tr>
<td >zk_ephemerals_count</td>
<td >-</td>
<td >Number of ephemeral ZooKeeper nodes</td>
</tr><tr>
<td >Data size</td>
<td >zk_approximate_data_size</td>
<td >Byte</td>
<td >Volume of data stored in ZooKeeper</td>
</tr><tr>
<td >Node status</td>
<td >zk_server_state</td>
<td >1: Master. 0: Slave. 2: Standalone</td>
<td >ZooKeeper node type</td>
</tr><tr>
<td rowspan=2>Received/Sent packets</td>
<td >zk_packets_received</td>
<td >count/s</td>
<td >ZooKeeper packet receiving rate</td>
</tr><tr>
<td >zk_packets_sent</td>
<td >count/s</td>
<td >ZooKeeper packet sending rate</td>
</tr><tr>
<td >Queuing requests</td>
<td >zk_outstanding_requests</td>
<td >-</td>
<td >Number of queuing requests</td>
</tr>
</tbody>
</table>
