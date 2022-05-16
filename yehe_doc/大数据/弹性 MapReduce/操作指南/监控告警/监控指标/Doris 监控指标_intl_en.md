### Doris - FE
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=3>Node information</td>
<td >FeNodeNum </td>
<td >count </td>
<td >Total number of FE nodes</td>
</tr><tr>
<td >BeAliveNum </td>
<td >count </td>
<td >Number of alive BE nodes</td>
</tr><tr>
<td >BkDeadNum </td>
<td >count </td>
<td >Number of dead broker nodes</td>
</tr><tr>			
<td >Connections</td>
<td >Num </td>
<td >count </td>
<td >	Number of FE node JVM connections</td>
</tr><tr>		
<td rowspan=2>JVM threads</td>
<td >Total </td>
<td >count </td>
<td >Total number of threads in the JVM of the FE node, including daemon threads and non-daemon threads</td>
</tr><tr>		
<td >Peak </td>
<td >count </td>
<td >Peak number of threads in the JVM of the FE node</td>
</tr><tr>		
<td rowspan=2>GC count</td>
<td >YoungGC </td>
<td >count </td>
<td >	FE node JVM Young GC count</td>
</tr><tr>
<td >OldGC </td>
<td >count </td>
<td >	FE node JVM Old GC count</td>
</tr><tr>
<td rowspan=2>GC time</td>
<td >YoungGC </td>
<td >s </td>
<td >FE node JVM Young GC time</td>
</tr><tr>
<td >OldGC </td>
<td >s </td>
<td >FE node JVM Old GC time</td>
</tr><tr>
<td rowspan=4>FE query latency</td>
<td >Quantile75 </td>
<td >ms </td>
<td >75th percentile of the FE query latency</td>
</tr><tr>
<td >Quantile95 </td>
<td >ms </td>
<td >95th percentile of the FE query latency</td>
</tr><tr>
<td >Quantile99 </td>
<td >ms </td>
<td >99th percentile of the FE query latency</td>
</tr><tr>
<td >Quantile999 </td>
<td >ms </td>
<td >99.9th percentile of the FE query latency</td>
</tr><tr>
<td >Maximum compaction score of tablet</td>
<td >MAX </td>
<td >score </td>
<td >Maximum compaction score of FE tablet</td>
</tr><tr>
<td >Scheduled tablets</td>
<td >ScheduledTablet </td>
<td >count </td>
<td >Number of scheduled tablets in FE</td>
</tr><tr>
<td rowspan=2>Request response</td>
<td >QPS </td>
<td >count </td>
<td >Number of queries per second</td>
</tr><tr>			
<td >RPS </td>
<td >count </td>
<td >Number of requests that can be processed per second</td>
</tr><tr>			
<td >Query failure rate</td>
<td >ErrRate </td>
<td >% </td>
<td >Query error rate</td>
</tr><tr>			
<td rowspan=6>Cache query</td>
<td >SqlModelHitQuery </td>
<td >count </td>
<td >Number of queries that hit the SQL model</td>
</tr><tr>			
<td >PartitionModelHitQuery </td>
<td >count </td>
<td >Number of queries that hit the partition model</td>
</tr><tr>			
<td >SqlModelQuery </td>
<td >count</td>
<td >Number of queries in the SQL cache model</td>
</tr><tr>		
<td >PartitionModelQuery </td>
<td >count </td>
<td >Number of queries in the partition cache model</td>
</tr><tr>			
<td >CachePartitionHit </td>
<td >count </td>
<td >Number of partitions that hit the cache in the query</td>
</tr><tr>			
<td >CachePartitionScan </td>
<td >count</td>
<td >Number of all partitions scanned in the query</td>
</tr><tr>		
<td rowspan=2>Routine load rows</td>
<td >TotalRows </td>
<td >count</td>
<td >Number of FE routine load rows</td>
</tr><tr>		
<td >ErrorRows </td>
<td >count</td>
<td >Number of FE routine load error rows</td>
</tr><tr>		
<td rowspan=4>Transaction status statistics</td>
<td >Reject </td>
<td >count</td>
<td >Number of rejected transactions on FE</td>
</tr><tr>		
<td >Begin </td>
<td >count</td>
<td >Number of transactions that have begun on FE</td>
</tr><tr>		
<td >Success </td>
<td >count</td>
<td >Number of successful transactions on FE</td>
</tr><tr>		
<td >Failed </td>
<td >count</td>
<td >Number of failed transactions on FE</td>
</tr><tr>		
<td rowspan=2>Images</td>
<td >Write </td>
<td >count</td>
<td >	Number of image writes on FE</td>
</tr><tr>		
<td >Push </td>
<td >count</td>
<td >	Number of image pushes on FE</td>
</tr><tr>		
<td rowspan=2>ALTER job statistics</td>
<td >RollupRunning </td>
<td >count</td>
<td >	Number of running alter jobs of ROLLUP type</td>
</tr><tr>		
<td >SchemaChangeRunning </td>
<td >count</td>
<td >	Number of running alter jobs of SCHEMA_CHANGE type</td>
</tr><tr>		
<td rowspan=7>UNKNOWN load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of UNKNOWN type in CANCELLED status</td>
</tr><tr>		
<td rowspan=7>SPARK load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of SPARK type in CANCELLED status</td>
</tr><tr>	
<td rowspan=7>DELETE load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of DELETE type in CANCELLED status</td>
</tr><tr>	
<td rowspan=7>INSERT load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of INSERT type in CANCELLED status</td>
</tr><tr>	
<td rowspan=7>BROKER load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of BROKER type in CANCELLED status</td>
</tr><tr>	
<td rowspan=7>MINI load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of MINI type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of MINI type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of MINI type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of MINI type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of MINI type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of MINI type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of MINI type in CANCELLED status</td>
</tr><tr>	
<td rowspan=7>HADOOP load job statistics</td>
<td >UNKNOWN </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in UNKNOWN status</td>
</tr><tr>		
<td >PENDING </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in PENDING status</td>
</tr><tr>		
<td >ETL </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in ETL status</td>
</tr><tr>		
<td >LOADING </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in LOADING status</td>
</tr><tr>		
<td >COMMITTED </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in COMMITTED status</td>
</tr><tr>		
<td >FINISHED </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in FINISHED status</td>
</tr><tr>		
<td >CANCELLED </td>
<td >count</td>
<td >	Number of load jobs of HADOOP type in CANCELLED status</td>
</tr>
</table>

### Doris - BE
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=4>Thrift utilization</td>
<td >Broker </td>
<td >count </td>
<td >Number of thrifts used by broker</td>
</tr><tr>
<td >Backend </td>
<td >count </td>
<td >Number of thrifts used by BE</td>
</tr><tr>
<td >Extdatasource </td>
<td >count </td>
<td >Number of thrifts used by extdatasource</td>
</tr><tr>
<td >Frontend </td>
<td >count </td>
<td >Number of thrifts used by FE</td>
</tr><tr>
<td rowspan=3>Streaming load statistics</td>
<td >RequestsTotal </td>
<td >count </td>
<td >Number of streaming load requests</td>
</tr><tr>
<td >CurrentProcessing </td>
<td >count </td>
<td >Number of existing streaming load processes</td>
</tr><tr>
<td >PipeCount </td>
<td >count </td>
<td >Number of streaming load pipes</td>
</tr><tr>
<td >Streaming load time</td>
<td >Duration </td>
<td >ms </td>
<td >Streaming load duration</td>
</tr><tr>
<td >Streaming load data volume</td>
<td >LoadTotal </td>
<td >bytes </td>
<td >Size of data imported by streaming load</td>
</tr><tr>
<td rowspan=3>Fragment statistics</td>
<td >PlanFragment </td>
<td >count </td>
<td >Number of plan fragments</td>
</tr><tr>
<td >Endpoint </td>
<td >count </td>
<td >Number of DataStreams</td>
</tr><tr>
<td >RequestsTotal </td>
<td >count </td>
<td >Number of fragment requests</td>
</tr><tr>
<td >Fragment request duration</td>
<td >Duration </td>
<td >μs</td>
<td >Fragment request duration</td>
</tr><tr>
<td rowspan=2>BE memory</td>
<td >Total </td>
<td >bytes</td>
<td >Size of BE memory pool</td>
</tr><tr>
<td >Allocated </td>
<td >bytes</td>
<td >Size of allocated BE memory</td>
</tr><tr>
<td rowspan=2>Maximum compaction score of tablet</td>
<td >CumulativeMax </td>
<td >score</td>
<td >Maximum cumulative compaction score of tablet</td>
</tr><tr>
<td >BaseMax </td>
<td >score</td>
<td >Maximum base compaction score of tablet</td>
</tr><tr> 			
<td rowspan=2>Data handled by compaction</td>
<td >Cumulative </td>
<td >bytes</td>
<td >Amount of data handled by cumulative compaction</td>
</tr><tr> 						
<td >Base </td>
<td >bytes</td>
<td >Amount of data handled by base compaction</td>
</tr><tr> 					
<td rowspan=2>Delta data handled by compaction</td>
<td >Cumulative </td>
<td >bytes</td>
<td >Amount of delta data handled by cumulative compaction</td>
</tr><tr> 						
<td >Base </td>
<td >bytes</td>
<td >Amount of delta data handled by base compaction</td>
</tr><tr> 		
<td >MemPools used by compaction</td>
<td >CurrentConsumption </td>
<td >count</td>
<td >Sum of MemPools used by compaction (all compaction threads)</td>
</tr><tr> 		
<td rowspan=3>Process file handles</td>
<td >Used </td>
<td >count</td>
<td >	Number of file handles used by BE process</td>
</tr><tr>
<td >SoftLimit </td>
<td >count</td>
<td >	Soft limit on file handles for BE process</td>
</tr><tr> 
<td >HardLimit </td>
<td >count</td>
<td >	Hard limit on file handles for BE process</td>
</tr><tr> 
<td >Running threads in process</td>
<td >NUM </td>
<td >count</td>
<td >	Number of threads running in BE process</td>
</tr><tr> 
<td rowspan=4>Engine request statistics</td>
<td >FailedBaseCompaction </td>
<td >count</td>
<td >	Number of failed engine requests of base_compaction type</td>
</tr><tr>
<td >FailedCultCompt </td>
<td >count</td>
<td >	Number of failed engine requests of cumulative_compaction type</td>
</tr><tr> 
<td >TotalBaseCompaction </td>
<td >count</td>
<td >	Total number of engine requests of base_compaction type</td>
</tr><tr> 
<td >TotalCultCompt </td>
<td >count</td>
<td >	Total number of engine requests of cumulative_compaction type</td>
</tr>
</table>

### Doris - BK
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
</tr></table>
