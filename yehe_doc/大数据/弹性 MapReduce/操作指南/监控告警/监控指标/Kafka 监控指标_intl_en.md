<table>
<thead>
<tr>
<th>Title</th>
<th>Metric</th>
<th>Unit</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>CPU utilization</td>
<td>ProcessCpuLoad</td>
<td>%</td>
<td>Process CPU utilization</td>
</tr>
<tr>
<td>CPU usage time</td>
<td>ProcessCpuTime</td>
<td>ms</td>
<td>Cumulative CPU usage time</td>
</tr>
<tr>
<td rowspan=2>GC count</td>
<td>YGC</td>
<td>-</td>
<td>Young GC count</td>
</tr>
<tr>
<td>FGC</td>
<td>-</td>
<td>Full GC count</td>
</tr>
<tr>
<td rowspan=3>GC time</td>
<td>GCT</td>
<td>s</td>
<td>Garbage collection time</td>
</tr>
<tr>
<td>FGCT</td>
<td>s</td>
<td>Full GC time</td>
</tr>
<tr>
<td>YGCT</td>
<td>s</td>
<td>Young GC time</td>
</tr>
<tr>
<td rowspan=6>Memory zone proportion</td>
<td>O</td>
<td>%</td>
<td>Percentage of used Old memory</td>
</tr>
<tr>
<td>M</td>
<td>%</td>
<td>Percentage of used Metaspace memory</td>
</tr>
<tr>
<td>CCS</td>
<td>%</td>
<td>Percentage of used compressed class space memory</td>
</tr>
<tr>
<td>S0</td>
<td>%</td>
<td>Percentage of used Survivor 0 memory</td>
</tr>
<tr>
<td>S1</td>
<td>%</td>
<td>Percentage of used Survivor 1 memory</td>
</tr>
<tr>
<td>E</td>
<td>%</td>
<td>Percentage of used Eden memory</td>
</tr>
<tr>
<td rowspan=7>JVM memory</td>
<td>MemHeapInitM</td>
<td>MB</td>
<td>Size of initial JVM HeapMemory</td>
</tr>
<tr>
<td>MemNonHeapInitM</td>
<td>MB</td>
<td>Size of initial JVM NonHeapMemory</td>
</tr>
<tr>
<td>MemHeapMaxM</td>
<td>MB</td>
<td>Size of HeapMemory configured by JVM</td>
</tr>
<tr>
<td>MemHeapCommittedM</td>
<td>MB</td>
<td>Size of HeapMemory currently committed by JVM</td>
</tr>
<tr>
<td>MemHeapUsedM</td>
<td>MB</td>
<td>Size of HeapMemory currently used by JVM</td>
</tr>
<tr>
<td>MemNonHeapCommittedM</td>
<td>MB</td>
<td>Size of NonHeapMemory currently committed by JVM</td>
</tr>
<tr>
<td>MemNonHeapUsedM</td>
<td>MB</td>
<td>Size of NonHeapMemory currently used by JVM</td>
</tr>
<tr>
<td rowspan=2>File handles</td>
<td>OpenFileDescriptorCount</td>
<td>count/s</td>
<td>Number of opened file descriptors</td>
</tr>
<tr>
<td>MaxFileDescriptorCount</td>
<td>count/s</td>
<td>Maximum number of file descriptors</td>
</tr>
<tr>
<td>Process execution duration</td>
<td>Uptime</td>
<td>s</td>
<td>Process execution duration</td>
</tr>
<tr>
<td rowspan=3>Worker threads</td>
<td>PeakThreadCount</td>
<td>count/s</td>
<td>Peak number of threads</td>
</tr>
<tr>
<td>ThreadCount</td>
<td>count/s</td>
<td>Total number of threads</td>
</tr>
<tr>
<td>DaemonThreadCount</td>
<td>count/s</td>
<td>Number of Daemon threads</td>
</tr>
<tr>
<td>Production traffic of Broker</td>
<td>OneMinuteRate</td>
<td>bytes/s</td>
<td>Rate of message production by the Broker per minute</td>
</tr>
<tr>
<td>Consumption traffic of Broker</td>
<td>OneMinuteRate</td>
<td>bytes/s</td>
<td>Rate of message consumption by the Broker per minute</td>
</tr>
<tr>
<td>Rejected consumption traffic</td>
<td>OneMinuteRate</td>
<td>bytes/s</td>
<td>Rate of Topic request rejection per minute</td>
</tr>
<tr>
<td>Failed Fetch requests</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of Fetch request failures per minute</td>
</tr>
<tr>
<td>Failed Produce requests</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of Produce request failures per minute</td>
</tr>
<tr>
<td>Produced messages</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of message production per minute</td>
</tr>
<tr>
<td>Read traffic from other Brokers</td>
<td>OneMinuteRate</td>
<td>bytes/s</td>
<td>Amount of traffic read from other Brokers per minute</td>
</tr>
<tr>
<td>Read traffic to other Brokers</td>
<td>OneMinuteRate</td>
<td>bytes/s</td>
<td>Amount of traffic read to other Brokers per minute</td>
</tr>
<tr>
<td>Fetch requests</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of Fetch requests per minute</td>
</tr>
<tr>
<td>Produce requests</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of Produce requests per minute</td>
</tr>
<tr>
<td>ControllerBroker</td>
<td>IsControllerBroker</td>
<td>-</td>
<td>The metric value is 1 on the Broker where Controller is located and is 0 on other Brokers.</td>
</tr>
<tr>
<td>LeaderElection rate</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of LeaderElections per minute</td>
</tr>
<tr>
<td rowspan=3>LeaderElection latencies</td>
<td>99thPercentile</td>
<td rowspan=3>ms</td>
<td>The 99th percentile of LeaderElection latencies</td>
</tr>
<tr>
<td>999thPercentile</td>
<td>The 99.9th percentile of LeaderElection latencies</td>
</tr>
<tr>
<td>Mean</td>
<td>Mean value of LeaderElection latencies</td>
</tr>
<tr>
<td>UncleanLeaderElections rate</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>Rate of UncleanLeaderElections per minute</td>
</tr>
<tr>
<td>GlobalPartition count</td>
<td>GlobalPartitionCount</td>
<td>count/s</td>
<td>Number of global partitions observed by the controller</td>
</tr>
<tr>
<td>OfflinePartitions count</td>
<td>OfflinePartitionCount</td>
<td>count/s</td>
<td>Number of offline partitions observed by the controller</td>
</tr>
<tr>
<td>GlobalTopic count</td>
<td>GlobalTopicCount</td>
<td>count/s</td>
<td>Number of global topics observed by the controller</td>
</tr>
<tr>
<td>Offline log directory count</td>
<td>OfflineLogDirectory</td>
<td>count/s</td>
<td>Number of offline log directories</td>
</tr>
<tr>
<td>LogFlush rate</td>
<td>OneMinuteRate</td>
<td>calls/s</td>
<td>Rate of message log flush per minute</td>
</tr>
<tr>
<td rowspan=3>LogFlush latencies</td>
<td>99thPercentile</td>
<td rowspan=3>ms</td>
<td>The 99th percentile of LogFlush latencies</td>
</tr>
<tr>
<td>999thPercentile</td>
<td>The 99.9th percentile of LogFlush latencies</td>
</tr>
<tr>
<td>Mean</td>
<td>Mean value of LogFlush latencies</td>
</tr>
<tr>
<td>Average network processor idleness rate</td>
<td>NetworkProcessorAvgIdlePercent</td>
<td>-</td>
<td>Average idleness rate of threads in a network thread pool</td>
</tr>
<tr>
<td>ISR expansion rate</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>In-sync replica (ISR) expansion rate per minute</td>
</tr>
<tr>
<td>ISR shrinkage rate</td>
<td>OneMinuteRate</td>
<td>count/s</td>
<td>ISR shrinkage rate per minute</td>
</tr>
<tr>
<td rowspan=2>Replicas count</td>
<td>LeaderReplicaCount</td>
<td>count/s</td>
<td>Number of offline replicas</td>
</tr>
<tr>
<td>OfflineReplicaCount</td>
<td>count/s</td>
<td>Number of leader replicas</td>
</tr>
<tr>
<td rowspan=3>Partitions count</td>
<td>PartitionCount</td>
<td rowspan=3>count</td>
<td>Number of partitions</td>
</tr>
<tr>
<td>UnderMinIsrPartitionCount</td>
<td>Number of partitions under the minimum ISR count</td>
</tr>
<tr>
<td>UnderReplicatedPartitions</td>
<td>Number of UnderReplicatedPartitions</td>
</tr>
<tr>
<td rowspan=3>FetchConsumer request latencies</td>
<td>99thPercentile</td>
<td rowspan=3>ms</td>
<td>The 99.9th percentile of FetchConsumer request latencies</td>
</tr>
<tr>
<td>999thPercentile</td>
<td>The 99.9th percentile of FetchConsumer request latencies</td>
</tr>
<tr>
<td>Mean</td>
<td>Mean value of FetchConsumer request latencies</td>
</tr>
<tr>
<td rowspan=3>FetchFollower request latencies</td>
<td>99thPercentile</td>
<td rowspan=3>ms</td>
<td>The 99.9th percentile of FetchFollower request latencies</td>
</tr>
<tr>
<td>999thPercentile</td>
<td>The 99.9th percentile of FetchFollower request latencies</td>
</tr>
<tr>
<td>Mean</td>
<td>Mean value of FetchFollower request latencies</td>
</tr>
<tr>
<td rowspan=3>Produce request latency</td>
<td>99thPercentile</td>
<td rowspan=3>ms</td> 
<td>The 99.9th percentile of Produce request latencies</td>
</tr>
<tr>
<td>999thPercentile</td>
<td>The 99.9th percentile of Produce request latencies</td>
</tr>
<tr>
<td>Mean</td>
<td>Mean value of Produce request latencies</td>
</tr>
<tr>
<td>Size of the request queue</td>
<td>RequestQueueSize</td>
<td>size</td>
<td>Size of the request queue</td>
</tr>
<tr>
<td rowspan=2>Purgatory size</td>
<td>Fetch</td>
<td>size</td>
<td>Number of requests waiting in fetch purgatory</td>
</tr>
<tr>
<td>Produce</td>
<td>-</td>
<td>Number of requests waiting in producer purgatory</td>
</tr>
<tr>
<td>Average request handler idleness rate</td>
<td>OneMinuteRate</td>
<td>-</td>
<td>Idleness rate of request handlers per minute</td>
</tr>
<tr>
<td rowspan=3>ZooKeeper request latencies</td>
<td>99thPercentile</td>
<td rowspan=3>ms</td>
<td>The 99th percentile of ZooKeeper request latencies</td>
</tr>
<tr>
<td>999thPercentile</td>
<td>The 99.9th percentile of ZooKeeper request latencies</td>
</tr>
<tr>
<td>Mean</td>
<td>Mean value of ZooKeeper request latencies</td>
</tr>
</tbody></table>
