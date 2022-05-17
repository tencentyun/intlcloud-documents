>? Metrics such as verification failure statistics, authentication failure statistics, and authentication success statistics currently don't have specific data, which will be available in the future.

### COSRanger - COSRangerServer
<table>
<tr>
<th width=30%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=35%>Description</th>
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
<td >CPU utilization</td>
<td >ProcessCpuLoad </td>
<td >% </td>
<td >	CPU utilization</td>
</tr><tr>
<td rowspan=2>File handles</td>
<td >MaxFileDescriptorCount </td>
<td > - </td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td >OpenFileDescriptorCount </td>
<td > - </td>
<td >Number of opened file descriptors</td>
</tr><tr>	
<td >CPU usage time</td>
<td >ProcessCpuTime </td>
<td >ms </td>
<td >Cumulative CPU usage time</td>
</tr><tr>	
<td >Process execution duration</td>
<td >Uptime </td>
<td >s </td>
<td >Process execution duration</td>
</tr><tr>	
<td rowspan=3>Worker threads</td>
<td >ThreadCount </td>
<td > - </td>
<td >Number of threads</td>
</tr><tr>
<td >PeakThreadCount </td>
<td > - </td>
<td >Peak number of threads</td>
</tr><tr>			
<td >DaemonThreadCount </td>
<td > - </td>
<td >Number of backend threads</td>
</tr><tr>
<td >- </td>
<td >Leader </td>
<td >-</td>
<td >Whether it is the COSRanger master node</td>
</tr><tr>
<td rowspan=3>Check statistics</td>		
<td >PermissionAllowCnt</td>
<td >count</td>
<td >Total number of permission allows</td>
</tr><tr>
<td >AuthDenyCnt</td>
<td >count</td>
<td >Total number of authentication failures</td>
</tr><tr>
<td >PermissionDenyCnt</td>
<td >count</td>
<td >Total number of permission denies</td>
</tr><tr>
<td rowspan=5>Authentication success statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>Authentication failure statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>Permission deny statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>Permission allow statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>	
<td rowspan=5>accessStat_DELETE operation statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>accessStat_LIST operation statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>accessStat_READ operation statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>accessStat_WRITE operation statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>rpc_getRangerAuthPolicy call count statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>rpc_checkPermission call count statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td > Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td > Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td > Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td > Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>rpc_getDelegationToken call count statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>rpc_renewDelegationToken call count statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>rpc_cancelDelegationToken call count statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=5>rpc_getSTS call count statistics</td>
<td >Qps</td>
<td >count</td>
<td >Number of queries per second</td>
</tr><tr>
<td >Total_5m</td>
<td >count</td>
<td >Total number of requests per five minutes</td>
</tr><tr>
<td >Total_1m</td>
<td >count</td>
<td >Total number of requests per minute</td>
</tr><tr>
<td >Qps_5m</td>
<td >count</td>
<td >Average number of requests per five minutes</td>
</tr><tr>
<td >Qps_1m</td>
<td >count</td>
<td >Average number of requests per minute</td>
</tr><tr>
<td rowspan=9>cosRpc_getSTS call duration</td>
<td >Cost_Avg</td>
<td >μs</td>
<td >Average duration in the current second</td>
</tr><tr>
<td >Cost_Avg_1m</td>
<td >μs</td>
<td >Average duration per minute</td>
</tr><tr>
<td >Cost_Avg_5m</td>
<td >μs</td>
<td >Average duration per five minutes</td>
</tr><tr>
<td >Cost_Max</td>
<td >μs</td>
<td >Maximum duration in the current second</td>
</tr><tr>
<td >Cost_Max_1m</td>
<td >μs</td>
<td >Maximum duration per minute</td>
</tr><tr>
<td >Cost_Max_5m</td>
<td >μs</td>
<td >Maximum duration per five minutes</td>
</tr><tr>
<td >Cost_Min</td>
<td >μs</td>
<td >Minimum duration in the current second</td>
</tr><tr>
<td >Cost_Min_1m</td>
<td >μs</td>
<td >Minimum duration per minute</td>
</tr><tr>
<td >Cost_Min_5m</td>
<td >μs</td>
<td >Minimum duration per five minutes</td>
</tr><tr>
<td rowspan=9>cosRpc_renewDelegationToken call duration</td>
<td >Cost_Avg</td>
<td >μs</td>
<td >Average duration in the current second</td>
</tr><tr>
<td >Cost_Avg_1m</td>
<td >μs</td>
<td >Average duration per minute</td>
</tr><tr>
<td >Cost_Avg_5m</td>
<td >μs</td>
<td >Average duration per five minutes</td>
</tr><tr>
<td >Cost_Max</td>
<td >μs</td>
<td >Maximum duration in the current second</td>
</tr><tr>
<td >Cost_Max_1m</td>
<td >μs</td>
<td >Maximum duration per minute</td>
</tr><tr>
<td >Cost_Max_5m</td>
<td >μs</td>
<td >Maximum duration per five minutes</td>
</tr><tr>
<td >Cost_Min</td>
<td >μs</td>
<td >Minimum duration in the current second</td>
</tr><tr>
<td >Cost_Min_1m</td>
<td >μs</td>
<td >Minimum duration per minute</td>
</tr><tr>
<td >Cost_Min_5m</td>
<td >μs</td>
<td >Minimum duration per five minutes</td>
</tr><tr>
<td rowspan=9>cosRpc_cancelDelegationToken call duration</td>
<td >Cost_Avg</td>
<td >μs</td>
<td >Average duration in the current second</td>
</tr><tr>
<td >Cost_Avg_1m</td>
<td >μs</td>
<td >Average duration per minute</td>
</tr><tr>
<td >Cost_Avg_5m</td>
<td >μs</td>
<td >Average duration per five minutes</td>
</tr><tr>
<td >Cost_Max</td>
<td >μs</td>
<td >Maximum duration in the current second</td>
</tr><tr>
<td >Cost_Max_1m</td>
<td >μs</td>
<td >Maximum duration per minute</td>
</tr><tr>
<td >Cost_Max_5m</td>
<td >μs</td>
<td >Maximum duration per five minutes</td>
</tr><tr>
<td >Cost_Min</td>
<td >μs</td>
<td >Minimum duration in the current second</td>
</tr><tr>
<td >Cost_Min_1m</td>
<td >μs</td>
<td >Minimum duration per minute</td>
</tr><tr>
<td >Cost_Min_5m</td>
<td >μs</td>
<td >Minimum duration per five minutes</td>
</tr><tr>
<td rowspan=9>cosRpc_getDelegationToken call duration</td>
<td >Cost_Avg</td>
<td >μs</td>
<td >Average duration in the current second</td>
</tr><tr>
<td >Cost_Avg_1m</td>
<td >μs</td>
<td >Average duration per minute</td>
</tr><tr>
<td >Cost_Avg_5m</td>
<td >μs</td>
<td >Average duration per five minutes</td>
</tr><tr>
<td >Cost_Max</td>
<td >μs</td>
<td >Maximum duration in the current second</td>
</tr><tr>
<td >Cost_Max_1m</td>
<td >μs</td>
<td >Maximum duration per minute</td>
</tr><tr>
<td >Cost_Max_5m</td>
<td >μs</td>
<td >Maximum duration per five minutes</td>
</tr><tr>
<td >Cost_Min</td>
<td >μs</td>
<td >Minimum duration in the current second</td>
</tr><tr>
<td >Cost_Min_1m</td>
<td >μs</td>
<td >Minimum duration per minute</td>
</tr><tr>
<td >Cost_Min_5m</td>
<td >μs</td>
<td >Minimum duration per five minutes</td>
</tr><tr>
<td rowspan=9>cosRpc_checkPermission call duration</td>
<td >Cost_Avg</td>
<td >μs</td>
<td >Average duration in the current second</td>
</tr><tr>
<td >Cost_Avg_1m</td>
<td >μs</td>
<td >Average duration per minute</td>
</tr><tr>
<td >Cost_Avg_5m</td>
<td >μs</td>
<td >Average duration per five minutes</td>
</tr><tr>
<td >Cost_Max</td>
<td >μs</td>
<td >Maximum duration in the current second</td>
</tr><tr>
<td >Cost_Max_1m</td>
<td >μs</td>
<td >Maximum duration per minute</td>
</tr><tr>
<td >Cost_Max_5m</td>
<td >μs</td>
<td >Maximum duration per five minutes</td>
</tr><tr>
<td >Cost_Min</td>
<td >μs</td>
<td >Minimum duration in the current second</td>
</tr><tr>
<td >Cost_Min_1m</td>
<td >μs</td>
<td >Minimum duration per minute</td>
</tr><tr>
<td >Cost_Min_5m</td>
<td >μs</td>
<td >Minimum duration per five minutes</td>
</tr><tr>
<td rowspan=9>cosRpc_getRangerAuthPolicy call duration</td>
<td >Cost_Avg</td>
<td >μs</td>
<td >Average duration in the current second</td>
</tr><tr>
<td >Cost_Avg_1m</td>
<td >μs</td>
<td >Average duration per minute</td>
</tr><tr>
<td >Cost_Avg_5m</td>
<td >μs</td>
<td >Average duration per five minutes</td>
</tr><tr>
<td >Cost_Max</td>
<td >μs</td>
<td >Maximum duration in the current second</td>
</tr><tr>
<td >Cost_Max_1m</td>
<td >μs</td>
<td >Maximum duration per minute</td>
</tr><tr>
<td >Cost_Max_5m</td>
<td >μs</td>
<td >Maximum duration per five minutes</td>
</tr><tr>
<td >Cost_Min</td>
<td >μs</td>
<td >Minimum duration in the current second</td>
</tr><tr>
<td >Cost_Min_1m</td>
<td >μs</td>
<td >Minimum duration per minute</td>
</tr><tr>
<td >Cost_Min_5m</td>
<td >μs</td>
<td >Minimum duration per five minutes</td>
</tr>
</table>
