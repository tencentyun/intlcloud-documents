### YARN - overview
<table>
<tr>
<th width=27%>Title</th>
<th width=20%>Metric</th>
<th width=8%>Unit</th>
<th width=45%>Description</th>
</tr><tr><td rowspan=4>Nodes</td>
<td >NumActiveNMs </td>
<td > - </td>
<td >Number of live NodeManagers</td>
</tr><tr>
<td >NumDecommissionedNMs </td>
<td > - </td>
<td >Number of decommissioned NodeManagers</td>
</tr><tr>
<td >NumLostNMs </td>
<td > - </td>
<td >Number of lost NodeManagers</td>
</tr><tr>
<td >NumUnhealthyNMs </td>
<td > - </td>
<td >Number of unhealthy NodeManagers</td>
</tr><tr><td rowspan=4>CPU cores</td>
<td >AllocatedVCores </td>
<td >-</td>
<td >Number of allocated VCores in the current queue</td>
</tr><tr>
<td >ReservedVCores </td>
<td >-</td>
<td >Number of reserved VCores in the current queue</td>
</tr><tr>
<td >AvailableVCores </td>
<td >-</td>
<td >Number of available VCores in the current queue</td>
</tr><tr>
<td >PendingVCores </td>
<td >-</td>
<td >Number of pending VCores in resource requests in the current queue</td>
</tr><tr><td rowspan=11>Total applications</td>
<td >AppsSubmitted</td>
<td >-</td>
<td >Number of submitted jobs in the current queue</td>
</tr><tr>
<td >AppsRunning</td>
<td >-</td>
<td >Number of running jobs in the current queue</td>
</tr><tr>
<td >AppsPending</td>
<td >-</td>
<td >Number of pending jobs in the current queue</td>
</tr><tr>
<td >AppsCompleted</td>
<td >-</td>
<td >Number of completed jobs in the current queue</td>
</tr><tr>
<td >AppsKilled</td> 
<td >-</td>
<td >Number of killed jobs in the current queue</td>
</tr><tr>
<td >AppsFailed</td>
<td >-</td>
<td >Number of failed jobs in the current queue</td>
</tr><tr>
<td >ActiveApplications</td>
<td >-</td>
<td >Number of active jobs in the current queue</td>
</tr><tr>
<td >running_0</td>
<td >-</td>
<td >Number of running jobs in the current queue that have run for less than 60 minutes</td>
</tr><tr>
<td >running_60</td>
<td >-</td>
<td >Number of running jobs in the current queue that have run for 60–300 minutes</td>
</tr><tr>
<td >running_300</td>
<td >-</td>
<td >Number of running jobs in the current queue that have run for 300–1,440 minutes</td>
</tr><tr>
<td >running_1440</td>
<td >-</td>
<td >Number of running jobs in the current queue that have run for more than 1,440 minutes</td>
</tr><tr>
<td rowspan=4>Memory size</td>
<td >AllocatedMB</td>
<td >MB</td>
<td >Amount of allocated memory in the current queue</td>
</tr><tr>
<td >AvailableMB</td>
<td >MB</td>
<td >Amount of available memory in the current queue</td>
</tr><tr>
<td >PendingMB</td>
<td >MB</td>
<td >Amount of pending memory in resource requests in the current queue</td>
</tr><tr>
<td >ReservedMB</td>
<td >MB</td>
<td >Amount of reserved memory in the current queue</td>
</tr><tr>
<td rowspan=3>Containers</td>
<td >AllocatedContainers</td>
<td >-</td>
<td >Number of allocated containers in the current queue</td>
</tr><tr>
<td >PendingContainers</td>
<td >-</td>
<td >Number of pending containers in resource requests in the current queue</td>
</tr><tr>
<td >ReservedContainers</td>
<td >-</td>
<td >Number of reserved containers in the current queue</td>
</tr><tr>
<td rowspan=2>Total allocated/released containers</td>
<td >AggregateContainersAllocated</td>
<td >-</td>
<td >Total number of allocated containers in the current queue</td>
</tr><tr>
<td >AggregateContainersReleased</td>
<td >-</td>
<td >Total number of released containers in the current queue</td>
</tr><tr>
<td >Users</td>
<td >ActiveUsers</td>
<td >-</td>
<td >Number of active users in the current queue</td>
</tr><tr>
<td rowspan=4>Memory</td>
<td >allocatedMB</td>
<td >MB</td>
<td >Amount of allocated memory in the cluster</td>
</tr><tr>
<td >availableMB</td>
<td >MB</td>
<td >Amount of available memory in the cluster</td>
</tr><tr>
<td >reservedMB</td>
<td >MB</td>
<td >Amount of reserved memory in the cluster</td>
</tr><tr>
<td >totalMB</td>
<td >MB</td>
<td >Total amount of memory in the cluster</td>
</tr><tr>
<td rowspan=6>Applications</td>
<td >completed</td>
<td >-</td>
<td >Number of completed jobs in the cluster during the statistical period</td>
</tr><tr>
<td >failed</td>
<td >-</td>
<td >Number of failed jobs in the cluster during the statistical period</td>
</tr><tr>
<td >killed</td>
<td >-</td>
<td >Number of killed jobs in the cluster during the statistical period</td>
</tr><tr>
<td >pending</td>
<td >-</td>
<td >Number of pending jobs in the cluster during the statistical period</td>
</tr><tr>
<td >running</td>
<td >-</td>
<td >Number of running jobs in the cluster during the statistical period</td>
</tr><tr>
<td >submitted</td>
<td >-</td>
<td >Number of submitted jobs in the cluster during the statistical period</td>
</tr><tr>
<td rowspan=3>Containers</td>
<td >containersAllocated</td>
<td >-</td>
<td >Number of allocated containers in the cluster</td>
</tr><tr>
<td >containersPending</td>
<td >-</td>
<td >Number of pending containers in the cluster</td>
</tr><tr>
<td >containersReserved</td>
<td >-</td>
<td >Number of reserved containers in the cluster</td>
</tr><tr>
<td >Memory utilization</td>
<td >usageRatio</td>
<td >%</td>
<td >Current memory utilization of the cluster</td>
</tr><tr>
<td rowspan=4>Cores</td>
<td >allocatedVirtualCores</td>
<td >-</td>
<td >Number of allocated CPU cores in the cluster</td>
</tr><tr>
<td >availableVirtualCores</td>
<td >-</td>
<td >Number of available CPU cores in the cluster</td>
</tr><tr>
<td >reservedVirtualCores</td>
<td >-</td>
<td >Number of reserved CPU cores in the cluster</td>
</tr><tr>
<td >totalVirtualCores</td>
<td >-</td>
<td >Total number of CPU cores in the cluster</td>
</tr><tr>
<td >CPU utilization</td>
<td >usageRatio</td>
<td >%</td>
<td >Current CPU utilization of the cluster</td>
</tr><tr>
<td >Launched AMs</td>
<td >AMLaunchDelayNumOps</td>
<td >-</td>
<td >Launched AMs</td>
</tr><tr>
<td >Average time for RM to launch AM</td>
<td >AMLaunchDelayAvgTime</td>
<td >ms</td>
<td >Average time for RM to launch AM</td>
</tr><tr>
<td >Total registered AMs</td>
<td >AMRegisterDelayNumOps</td>
<td >-</td>
<td >Total registered AMs</td>
</tr><tr>
<td >Average time for AM to register with RM</td>
<td >AMRegisterDelayAvgTime</td>
<td >ms</td>
<td >Average time for AM to register with RM</td>
</tr>
<tr>
<td >Queue CPU utilization</td>
<td >YARN.RM.QUEUE.VCORES.RATIO</td>
<td >-</td>
<td >Utilization of CPU allocated for the current queue</td>
</tr>
<tr>
<td >Queue memory utilization</td>
<td >YARN.RM.QUEUE.MEM.RATIO</td>
<td >-</td>
<td >Utilization of memory allocated for the current queue</td>
</tr>
</table>

### YARN - ResourceManager
<table>
<tr>
<tr><th width=27%>Title</th>
<th width=20%>Metric</th>
<th width=8%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
<td rowspan=4>RPC authentications/authorizations</td>
<td >RpcAuthenticationFailures</td>
<td >-</td>
<td >Number of failed RPC authentications</td>
</tr><tr>
<td >RpcAuthenticationSuccesses</td>
<td >-</td>
<td >Number of successful RPC authentications</td>
</tr><tr>
<td >RpcAuthorizationFailures</td>
<td >-</td>
<td >Number of failed RPC authorizations</td>
</tr><tr>
<td >RpcAuthorizationSuccesses</td>
<td >-</td>
<td >Number of successful RPC authorizations</td>
</tr><tr>
<td rowspan=2>Data received/sent by RPC</td>
<td >ReceivedBytes</td>
<td >bytes/s</td>
<td >Amount of data received by RPC</td>
</tr><tr>
<td >SentBytes</td>
<td >bytes/s</td>
<td >Amount of data sent by RPC</td>
</tr><tr>
<td >RPC connections</td>
<td >NumOpenConnections</td>
<td >-</td>
<td >Current number of open connections</td>
</tr><tr>
<td rowspan=2>RPC requests</td>
<td >RpcProcessingTimeNumOps</td>
<td >-</td>
<td >Number of RPC requests</td>
</tr><tr>
<td >RpcQueueTimeNumOps</td>
<td >-</td>
<td >Number of RPC requests</td>
</tr><tr>
<td >RPC queue length</td>
<td >CallQueueLength</td>
<td >-</td>
<td >Length of the current RPC queue</td>
</tr><tr>
<td rowspan=2>Average RPC processing time</td>
<td >RpcProcessingTimeAvgTime</td>
<td >s</td>
<td >Average RPC request processing time</td>
</tr><tr>
<td >RpcQueueTimeAvgTime</td>
<td >s</td>
<td >Average time of RPC in the queue</td>
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
<td rowspan=6>JVM threads</td>
<td >ThreadsNew </td>
<td > - </td>
<td >Number of threads in NEW status</td>
</tr><tr>
<td >ThreadsRunnable </td>
<td > - </td>
<td >Number of threads in RUNNABLE status</td>
</tr><tr>
<td >ThreadsBlocked </td>
<td > - </td>
<td >Number of threads in BLOCKED status</td>
</tr><tr>
<td >ThreadsWaiting </td>
<td > - </td>
<td >Number of threads in WAITING status</td>
</tr><tr>
<td >ThreadsTimedWaiting </td>
<td > - </td>
<td >Number of threads in TIMED WAITING status</td>
</tr><tr>
<td >ThreadsTerminated </td>
<td > - </td>
<td >Number of threads in Terminated status</td>
</tr><tr>
<td  rowspan=4>JVM logs</td>
<td >LogFatal </td>
<td > - </td>
<td >Number of Fatal logs</td>
</tr><tr>
<td >LogError </td>
<td > - </td>
<td >Number of Error logs</td>
</tr><tr>
<td >LogWarn </td>
<td > - </td>
<td >Number of Warn logs</td>
</tr><tr>
<td >LogInfo </td>
<td > - </td>
<td >Number of Info logs</td>
</tr><tr>
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Non-heap memory size used by process</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Non-heap memory size committed to process</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Heap memory size used by process</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Heap memory size committed to process</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Maximum heap memory size available to process</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB</td>
<td >Maximum memory size available to process</td>
</tr><tr>
<td >CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >CPU utilization</td>
</tr><tr>
<td >Cumulative CPU usage time</td>
<td >ProcessCpuTime</td>
<td >ms</td>
<td >Cumulative CPU usage time</td>
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
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>Worker threads</td>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads in the process</td>
</tr><tr>
<td >ThreadCount</td>
<td >-</td>
<td >Number of threads in the process</td>
</tr><tr>
<td >Node status</td>
<td >haState</td>
<td >1:Active,0:Standby</td>
<td >ResourceManager active/standby status</td>
</tr><tr>
<td >Active/Standby switch</td>
<td >switchOccurred</td>
<td >-</td>
<td >ResourceManager active/standby switch</td>
</tr>
</table>

### YARN - JobHistoryServer
<table>
<tr>
<tr><th width=25%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=45%>Description</th>
</tr><tr>
</tr><tr>
<td rowspan=6>JVM threads</td>
<td >ThreadsNew </td>
<td > - </td>
<td >Number of threads in NEW status</td>
</tr><tr>
<td >ThreadsRunnable </td>
<td > - </td>
<td >Number of threads in RUNNABLE status</td>
</tr><tr>
<td >ThreadsBlocked </td>
<td > - </td>
<td >Number of threads in BLOCKED status</td>
</tr><tr>
<td >ThreadsWaiting </td>
<td > - </td>
<td >Number of threads in WAITING status</td>
</tr><tr>
<td >ThreadsTimedWaiting </td>
<td > - </td>
<td >Number of threads in TIMED WAITING status</td>
</tr><tr>
<td >ThreadsTerminated </td>
<td > - </td>
<td >Number of threads in Terminated status</td>
</tr><tr>
<td rowspan=4>JVM logs</td>
<td >LogFatal </td>
<td > - </td>
<td >Number of FATAL-level logs</td>
</tr><tr>
<td >LogError </td>
<td > - </td>
<td >Number of ERROR-level logs</td>
</tr>			<tr>
<td >LogWarn </td>
<td > - </td>
<td >Number of WARN-level logs</td>
</tr><tr>
<td >LogInfo </td>
<td > - </td>
<td >	Number of INFO-level logs</td>
</tr><tr>
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Non-heap memory size used by process</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Non-heap memory size committed to process</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Heap memory size used by process</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Heap memory size committed to process</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Maximum heap memory size available to process</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB</td>
<td >Maximum memory size available to process</td>
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
<td >CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >CPU utilization</td>
</tr><tr>
<td >Cumulative CPU usage time</td>
<td >ProcessCpuTime</td>
<td >ms</td>
<td >Cumulative CPU usage time</td>
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
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>Worker threads</td>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads in the process</td>
</tr><tr>
<td >ThreadCount</td>
<td >-</td>
<td >Number of threads in the process</td>
</tr>
</table>

### YARN - NodeManager
<table>
<tr>
<th width=28%>Title</th>
<th width=20%>Metric</th>
<th width=7%>Unit</th>
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
<td rowspan=6>JVM threads</td>
<td >ThreadsNew </td>
<td > - </td>
<td >Number of threads in NEW status</td>
</tr><tr>
<td >ThreadsRunnable </td>
<td > - </td>
<td >Number of threads in RUNNABLE status</td>
</tr><tr>
<td >ThreadsBlocked </td>
<td > - </td>
<td >Number of threads in BLOCKED status</td>
</tr><tr>
<td >ThreadsWaiting </td>
<td > - </td>
<td >Number of threads in WAITING status</td>
</tr><tr>
<td >ThreadsTimedWaiting </td>
<td > - </td>
<td >Number of threads in TIMED WAITING status</td>
</tr><tr>
<td >ThreadsTerminated </td>
<td > - </td>
<td >Number of threads currently in TERMINATED status</td>
</tr><tr>
<td rowspan=4>JVM logs</td>
<td >LogFatal </td>
<td > - </td>
<td >Number of FATAL-level logs</td>
</tr><tr>
<td >LogError </td>
<td > - </td>
<td >Number of ERROR-level logs</td>
</tr>			<tr>
<td >LogWarn </td>
<td > - </td>
<td >Number of WARN-level logs</td>
</tr><tr>
<td >LogInfo </td>
<td > - </td>
<td >	Number of INFO-level logs</td>
</tr><tr>
<td rowspan=6>JVM memory</td>
<td >MemNonHeapUsedM</td>
<td >MB</td>
<td >Non-heap memory size used by process</td>
</tr><tr>
<td >MemNonHeapCommittedM</td>
<td >MB</td>
<td >Non-heap memory size committed to process</td>
</tr><tr>
<td >MemHeapUsedM</td>
<td >MB</td>
<td >Heap memory size used by process</td>
</tr><tr>
<td >MemHeapCommittedM</td>
<td >MB</td>
<td >Heap memory size committed to process</td>
</tr><tr>
<td >MemHeapMaxM</td>
<td >MB</td>
<td >Maximum heap memory size available to process</td>
</tr><tr>
<td >MemMaxM </td>
<td >MB</td>
<td >Maximum memory size available to process</td>
</tr><tr>
<td rowspan=7>Total containers</td>
<td >ContainersLaunched</td>
<td >-</td>
<td >Number of launched containers</td>
</tr><tr>
<td >ContainersCompleted</td>
<td >-</td>
<td >Number of completed containers</td>
</tr><tr>
<td >ContainersFailed</td>
<td >-</td>
<td >Number of failed containers</td>
</tr><tr>
<td >ContainersKilled</td>
<td >-</td>
<td >Number of killed containers</td>
</tr><tr>
<td >ContainersIniting</td>
<td >-</td>
<td >Number of containers being initialized</td>
</tr><tr>
<td >ContainersRunning</td>
<td >-</td>
<td >Number of running containers</td>
</tr><tr>
<td >AllocatedContainers</td>
<td >-</td>
<td >Number of containers allocated by NodeManager</td>
</tr><tr>
<td >Average container launch time</td>
<td >ContainerLaunchDurationAvgTime</td>
<td >ms</td>
<td >Average container launch time</td>
</tr><tr>
<td >Container launches</td>
<td >ContainerLaunchDurationNumOps</td>
<td >-</td>
<td >Container launches</td>
</tr><tr>
<td rowspan=2>CPU cores</td>
<td >AvailableVCores</td>
<td >-</td>
<td >Number of VCores available to NodeManager</td>
</tr><tr>
<td >AllocatedVCores</td>
<td >-</td>
<td >Number of VCores allocated by NodeManager</td>
</tr><tr>
<td rowspan=2>Memory size</td>
<td >AllocatedGB</td>
<td >GB</td>
<td >Amount of memory allocated by NodeManager</td>
</tr><tr>
<td >AvailableGB</td>
<td >GB</td>
<td >Amount of memory available to NodeManager</td>
</tr><tr>
<td >CPU utilization</td>
<td >ProcessCpuLoad</td>
<td >%</td>
<td >CPU utilization</td>
</tr><tr>
<td >Cumulative CPU usage time</td>
<td >ProcessCpuTime</td>
<td >ms</td>
<td >Cumulative CPU usage time</td>
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
<td >Process execution duration</td>
<td >Uptime</td>
<td >s</td>
<td >Process execution duration</td>
</tr><tr>
<td rowspan=2>Worker threads</td>
<td >DaemonThreadCount</td>
<td >-</td>
<td >Number of daemon threads in the process</td>
</tr><tr>
<td >ThreadCount</td>
<td >-</td>
<td >Number of threads in the process</td>
</tr>
</table>
