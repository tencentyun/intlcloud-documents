### Hive - HiveMetaStore 
<table>
<tr>
<th width=20%>Title</th>
<th width=20%>Metric</th>
<th width=15%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=2>GC count</td>
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td> 
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td rowspan=7>JVM memory</td>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Size of HeapMemory committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapInitM</td>
<td >MB</td>
<td >Size of initial JVM HeapMem</td>
</tr><tr>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemNonHeapInitM</td>
<td >MB</td>
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
<td >System CPU utilization</td>
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
</tr><tr>
<td>ALTER TABLE request duration</td>
<td>HIVE.HMS.API_ALTER_TABLE</td>
<td>ms</td>
<td>Average duration of ALTER TABLE requests</td>
</tr>
<tr>
<td>ALTER TABLE WITH ENV CONTEXT request duration</td>
<td>HIVE.HMS.API_ALTER_TABLE_WITH_ENV_CONTEXT</td>
<td>ms</td>
<td>Average duration of ALTER TABLE WITH ENV CONTEXT requests</td>
</tr>
<tr>
<td>CREATE TABLE request duration</td>
<td>HIVE.HMS.API_CREATE_TABLE</td>
<td>ms</td>
<td>Average duration of CREATE TABLE requests</td>
</tr>
<tr>
<td>CREATE TABLE WITH ENV CONTEXT request duration</td>
<td>HIVE.HMS.API_CREATE_TABLE_WITH_ENV_CONTEXT</td>
<td>ms</td>
<td>Average duration of CREATE TABLE WITH ENV CONTEXT requests</td>
</tr>
<tr>
<td>DROP TABLE request duration</td>
<td>HIVE.HMS.API_DROP_TABLE</td>
<td>ms</td>
<td>Average duration of DROP TABLE requests</td>
</tr>
<tr>
<td>DROP TABLE WITH ENV CONTEXT request duration</td>
<td>HIVE.HMS.API_DROP_TABLE_WITH_ENV_CONTEXT</td>
<td>ms</td>
<td>Average duration of DROP TABLE WITH ENV CONTEXT requests</td>
</tr>
<tr>
<td>GET TABLE request duration</td>
<td>HIVE.HMS.API_GET_TABLE</td>
<td>ms</td>
<td>Average duration of GET TABLE requests</td>
</tr>
<tr>
<td>GET TABLES request duration</td>
<td>HIVE.HMS.API_GET_TABLES</td>
<td>ms</td>
<td>Average duration of GET TABLES requests</td>
</tr>
<tr>
<td>GET MULTI TABLE request duration</td>
<td>HIVE.HMS.API_GET_MULTI_TABLE</td>
<td>ms</td>
<td>Average duration of GET MULTI TABLE requests</td>
</tr>
<tr>
<td>GET TABLE REQ request duration</td>
<td>HIVE.HMS.API_GET_TABLE_REQ</td>
<td>ms</td>
<td>Average duration of GET TABLE REQ requests</td>
</tr>
<tr>
<td>GET DATABASE request duration</td>
<td>HIVE.HMS.API_GET_DATABASE</td>
<td>ms</td>
<td>Average duration of GET DATABASE requests</td>
</tr>
<tr>
<td>GET DATABASES request duration</td>
<td>HIVE.HMS.API_GET_DATABASES</td>
<td>ms</td>
<td>Average duration of GET DATABASES requests</td>
</tr>
<tr>
<td>GET ALL DATABASES request duration</td>
<td>HIVE.HMS.API_GET_ALL_DATABASES</td>
<td>ms</td>
<td>Average duration of GET ALL DATABASES requests</td>
</tr>
<tr>
<td>GET ALL FUNCTIONS request duration</td>
<td>HIVE.HMS.API_GET_ALL_FUNCTIONS</td>
<td>ms</td>
<td>Average duration of GET ALL FUNCTIONS requests</td>
</tr>
<tr>
<td>Current number of active CREATE TABLE requests</td>
<td>HIVE.HMS.ACTIVE_CALLS_API_CREATE_TABLE</td>
<td>-</td>
<td>Current number of active CREATE TABLE requests</td>
</tr>
<tr>
<td>Current number of active DROP TABLE requests</td>
<td>HIVE.HMS.ACTIVE_CALLS_API_DROP_TABLE</td>
<td>-</td>
<td>Current number of active DROP TABLE requests</td>
</tr>
<tr>
<td>Current number of active ALTER TABLE requests</td>
<td>HIVE.HMS.ACTIVE_CALLS_API_ALTER_TABLE</td>
<td>-</td>
<td>Current number of active ALTER TABLE requests</td>
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
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr><tr>
<td rowspan=7>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently used by JVM</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Size of NonHeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Size of HeapMemory currently used by JVM</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Size of HeapMemory currently committed by JVM</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Size of HeapMemory configured by JVM</td>
</tr><tr>
<td >MemHeapInitM</td>
<td >MB</td>
<td >Size of initial JVM HeapMem</td>
</tr><tr>
<td >MemNonHeapInitM</td>
<td >MB</td>
<td >Size of initial JVM NonHeapMem</td>
</tr><tr>
<td >Percentage of used heap memory</td>
<td >MemHeapUsedRate</td>
<td >%</td>
<td >Proportion of the heap memory size currently used by JVM to the heap memory size configured for JVM</td>
</tr><tr>
<td>CPU utilization</td>
<td>ProcessCpuLoad</td>
<td >%</td>
<td >CPU utilization</td>
</tr><tr>
<td>Percentage of CPU usage time</td>
<td>CPUUsedRate</td>
<td >seconds/second</td>
<td >Percentage of CPU usage time</td>
</tr><tr>
<td rowspan=2>File descriptors</td>
<td>MaxFileDescriptorCount</td>
<td >-</td>
<td >Maximum number of file descriptors</td>
</tr><tr>
<td>OpenFileDescriptorCount</td>
<td >-</td>
<td >Number of opened file descriptors</td>
</tr><tr>
<td>Cumulative CPU usage time</td>
<td>ProcessCpuTime</td>
<td >ms</td>
<td >Cumulative CPU usage time</td>
</tr><tr>
<td>Process execution duration</td>
<td>Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>Worker threads</td>
<td>DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads</td>
</tr><tr>
<td>ThreadCount</td>
<td >-</td>
<td >Total number of threads</td>
</tr><tr>
<td rowspan=2>Driver execution latency</td>
<td>99th_percentile</td>
<td >ms</td>
<td >99th percentile of driver execution latency</td>
</tr><tr>
<td>Avg</td>
<td >ms</td>
<td >Average driver execution latency</td>
</tr><tr>
<td >Open connections</td>
<td>NumOpenConnections</td>
<td >-</td>
<td >Number of open connections</td>
</tr><tr>
<td >Current size of the pool of async HiveServer2 threads</td>
<td >PoolSize</td>
<td >-</td>
<td >Current size of the pool of async HiveServer2 threads</td>
</tr><tr>
<td >Current size of the queue for async HiveServer2 operations</td>
<td>QueueSize</td>
<td >-</td>
<td >Current size of the queue for async HiveServer2 operations</td>
</tr><tr>
<td rowspan=4>Hive operations</td>
<td>Closed</td>
<td >-</td>
<td >Number of closed operations</td>
</tr><tr>
<td>Finished</td>
<td >-</td>
<td >Number of completed operations</td>
</tr><tr>
<td>Canceled</td>
<td >-</td>
<td >Number of canceled operations</td>
</tr><tr>
<td>Error</td>
<td >-</td>
<td >Number of erroneous operations</td>
</tr><tr>
<td>GC extra sleep time</td>
<td>ExtraSleepTime</td>
<td >ms/s</td>
<td >GC extra sleep time</td>
</tr><tr>
<td rowspan=5>Number of API requests</td>
<td rowspan=5>HIVE.H2.ACTIVE.CALLS.API</td>
<td>Count</td>
<td>Current number of serializePlan requests</td>
</tr>
<tr>
<td>Count</td>
<td>Current number of semanticAnalyze requests</td>
</tr>
<tr>
<td>Count</td>
<td>Current number of runtask requests</td>
</tr>
<tr>
<td>Count</td>
<td>Current number of releaseLocks requests</td>
</tr>
<tr>
<td>Count</td>
<td>Current number of getSplits requests</td>
</tr>
<tr>
<td>Duration of SQL tasks in PENDING status</td>
<td>HIVE.H2.SQL.OPERATION.PENDING</td>
<td>ms</td>
<td>Average duration of SQL tasks in PENDING status</td>
</tr>
<tr>
<td>Duration of SQL tasks in RUNNING status</td>
<td>HIVE.H2.SQL.OPERATION.RUNNING</td>
<td>ms</td>
<td>Average duration of SQL tasks in RUNNING status</td>
</tr>
<tr>
<td>Current number of active users</td>
<td>HIVE.H2.SQL.OPERATION</td>
<td>Count</td>
<td>Current number of active users</td>
</tr>
<tr>
<td>Query execution time</td>
<td>HIVE.H2.EXECUTING.QUERIES</td>
<td>ms</td>
<td>Average query execution time</td>
</tr>
<tr>
<td>Query submission time</td>
<td>HIVE.H2.SUBMITTED.QUERIES</td>
<td>ms</td>
<td>Query submission time</td>
</tr>
<tr>
<td>Number of submitted Hive on MR jobs</td>
<td>HIVE.H2.MR.TASKS</td>
<td>Count</td>
<td>Number of submitted Hive on MR jobs</td>
</tr>
<tr>
<td>Number of submitted Hive on Spark jobs</td>
<td>HIVE.H2.SPARK.TASKS</td>
<td>Count</td>
<td>Number of submitted Hive on Tez jobs</td>
</tr>
<tr>
<td>Number of submitted Hive on Tez jobs</td>
<td>HIVE.H2.TEZ.TASKS</td>
<td>Count</td>
<td>Number of submitted Hive on Spark jobs</td>
</tr>
<tr>
<td>Failed queries</td>
<td>HIVE.H2.FAILED.QUERIES.RATE</td>
<td>Count/min</td>
<td>Number of failed queries per minute</td>
</tr>
<tr>
<td rowspan=7>Number of worker threads</td>
<td rowspan=7>HIVE.H2.THREAD.COUNT</td>
<td>-</td>
<td>Number of JVM blocked threads</td>
</tr>
<tr>
<td>-</td>
<td>Number of JVM terminate threads</td>
</tr>
<tr>
<td>-</td>
<td>Number of JVM deadlock threads</td>
</tr>
<tr>
<td>-</td>
<td>Number of JVM new threads</td>
</tr>
<tr>
<td>-</td>
<td>Number of JVM runnable threads</td>
</tr>
<tr>
<td>-</td>
<td>Number of JVM timed_waiting threads</td>
</tr>
<tr>
<td>-</td>
<td>Number of JVM waiting threads</td>
</tr>
<tr>
<td>Number of sessions</td>
<td>HIVE.H2.OPEN.SESSIONS</td>
<td>-</td>
<td>Number of open sessions</td>
</tr>
<tr>
<td>Current number of active sessions</td>
<td>HIVE.H2.ACTIVE.SESSIONS</td>
<td>-</td>
<td>Number of active sessions</td>
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
<td >YGC</td>
<td >-</td>
<td >Young GC count</td>
</tr><tr>
<td >FGC</td>
<td >-</td>
<td >Full GC count</td>
</tr><tr>
<td rowspan=3>GC time</td>
<td >FGCT</td>
<td >s</td>
<td >Full GC time</td>
</tr><tr>
<td >GCT</td>
<td >s</td>
<td >Garbage collection time</td>
</tr><tr>
<td >YGCT</td>
<td >s</td>
<td >Young GC time</td>
</tr><tr>
<td rowspan=6>Memory zone proportion</td>
<td >S0</td>
<td >%</td>
<td >Percentage of used Survivor 0 memory</td>
</tr><tr>
<td >E</td>
<td >%</td>
<td >Percentage of used Eden memory</td>
</tr><tr>
<td >CCS</td>
<td >%</td>
<td >Percentage of used compressed class space memory</td>
</tr><tr>
<td >S1</td>
<td >%</td>
<td >Percentage of used Survivor 1 memory</td>
</tr><tr>
<td >O</td>
<td >%</td>
<td >Percentage of used Old memory</td>
</tr><tr>
<td >M</td>
<td >%</td>
<td >Percentage of used Metaspace memory</td>
</tr>
</table>
