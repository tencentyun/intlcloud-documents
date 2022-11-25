## StarRocks - BE
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
<td rowspan=3>Delta data handled by compaction</td>
<td>Cumulative</td>
<td>rowsets</td>
<td>Amount of delta data handled by cumulative compaction</td>
</tr>
<tr>
<td>Base</td>
<td>rowsets</td>
<td>Amount of delta data handled by base compaction</td>
</tr>
<tr>
<td>Update</td>
<td>rowsets</td>
<td>Amount of delta data handled by update compaction</td>
</tr>
<tr>
<td rowspan=3>Data handled by compaction</td>
<td>Cumulative</td>
<td>bytes</td>
<td>Amount of data handled by cumulative compaction</td>
</tr>
<tr>
<td>Base</td>
<td>bytes</td>
<td>Amount of data handled by base compaction</td>
</tr>
<tr>
<td>Update</td>
<td>bytes</td>
<td>Amount of data handled by update compaction</td>
</tr>
<tr>
<td rowspan=2>Maximum compaction score of tablet</td>
<td>CumulativeMax</td>
<td>score</td>
<td>Maximum cumulative compaction score of tablet</td>
</tr>
<tr>
<td>BaseMax</td>
<td>score</td>
<td>Maximum base compaction score of tablet</td>
</tr>
<tr>
<td rowspan=7>Engine request failure statistics (1)</td>
<td>base_compaction</td>
<td>count</td>
<td>Number of failed engine requests of base_compaction type</td>
</tr>
<tr>
<td>clone</td>
<td>count</td>
<td>Number of failed engine requests of clone type</td>
</tr>
<tr>
<td>create_rollup</td>
<td>count</td>
<td>Number of failed engine requests of create_rollup type</td>
</tr>
<tr>
<td>create_tablet</td>
<td>count</td>
<td>Number of failed engine requests of create_tablet type</td>
</tr>
<tr>
<td>cumulative_compaction</td>
<td>count</td>
<td>Number of failed engine requests of cumulative_compaction type</td>
</tr>
<tr>
<td>delete</td>
<td>count</td>
<td>Number of failed engine requests of delete type</td>
</tr>
<tr>
<td>finish_task</td>
<td>count</td>
<td>Number of failed engine requests of finish_task type</td>
</tr>
<tr>
<td rowspan=6>Engine request failure statistics (2)</td>
<td>publish</td>
<td>count</td>
<td>Number of failed engine requests of publish type</td>
</tr>
<tr>
<td>report_all_tablets</td>
<td>count</td>
<td>Number of failed engine requests of report_all_tablets type</td>
</tr>
<tr>
<td>report_disk</td>
<td>count</td>
<td>Number of failed engine requests of report_disk type</td>
</tr>
<tr>
<td>report_tablet</td>
<td>count</td>
<td>Number of failed engine requests of report_tablet type</td>
</tr>
<tr>
<td>report_task</td>
<td>count</td>
<td>Number of failed engine requests of report_task type</td>
</tr>
<tr>
<td>schema_change</td>
<td>count</td>
<td>Number of failed engine requests of schema_change type</td>
</tr>
<tr>
<td rowspan=8>Engine request statistics (1)</td>
<td>base_compaction</td>
<td>count</td>
<td>Number of failed engine requests of base_compaction type</td>
</tr>
<tr>
<td>clone</td>
<td>count</td>
<td>Number of failed engine requests of clone type</td>
</tr>
<tr>
<td>create_rollup</td>
<td>count</td>
<td>Number of failed engine requests of create_rollup type</td>
</tr>
<tr>
<td>create_tablet</td>
<td>count</td>
<td>Number of failed engine requests of create_tablet type</td>
</tr>
<tr>
<td>cumulative_compaction</td>
<td>count</td>
<td>Number of failed engine requests of cumulative_compaction type</td>
</tr>
<tr>
<td>delete</td>
<td>count</td>
<td>Number of failed engine requests of delete type</td>
</tr>
<tr>
<td>drop_tablet</td>
<td>count</td>
<td>Number of failed engine requests of drop_tablet type</td>
</tr>
<tr>
<td>finish_task</td>
<td>count</td>
<td>Number of failed engine requests of finish_task type</td>
</tr>
<tr>
<td rowspan=7>Engine request statistics (2)</td>
<td>publish</td>
<td>count</td>
<td>Number of failed engine requests of publish type</td>
</tr>
<tr>
<td>report_all_tablets</td>
<td>count</td>
<td>Number of failed engine requests of report_all_tablets type</td>
</tr>
<tr>
<td>report_disk</td>
<td>count</td>
<td>Number of failed engine requests of report_disk type</td>
</tr>
<tr>
<td>report_tablet</td>
<td>count</td>
<td>Number of failed engine requests of report_tablet type</td>
</tr>
<tr>
<td>report_task</td>
<td>count</td>
<td>Number of failed engine requests of report_task type</td>
</tr>
<tr>
<td>schema_change</td>
<td>count</td>
<td>Number of failed engine requests of schema_change type</td>
</tr>
<tr>
<td>storage_migrate</td>
<td>count</td>
<td>Number of failed engine requests of storage_migrate type</td>
</tr>
<tr>
<td rowspan=2>Fragment statistics</td>
<td>PlanFragment</td>
<td>count</td>
<td>Number of plan fragments</td>
</tr>
<tr>
<td>Endpoint</td>
<td>count</td>
<td>Number of DataStreams</td>
</tr>
<tr>
<td>Fragment request duration</td>
<td>Duration</td>
<td>μs</td>
<td>Fragment request duration</td>
</tr>
<tr>
<td rowspan=4>Transaction request statistics</td>
<td>begin</td>
<td>count</td>
<td>Number of transaction requests of begin type</td>
</tr>
<tr>
<td>commit</td>
<td>count</td>
<td>Number of transaction requests of commit type</td>
</tr>
<tr>
<td>exec</td>
<td>count</td>
<td>Number of transaction requests of exec type</td>
</tr>
<tr>
<td>rollback</td>
<td>count</td>
<td>Number of transaction requests of rollback type</td>
</tr>
<tr>
<td>Data imported by streaming load</td>
<td>LoadTotal</td>
<td>bytes</td>
<td>Amount of data imported by streaming load</td>
</tr>
<tr>
<td rowspan=2>Streaming load statistics</td>
<td>CurrentProcessing</td>
<td>count</td>
<td>Number of existing streaming load processes</td>
</tr>
<tr>
<td>PipeCount</td>
<td>count</td>
<td>Number of streaming load pipes</td>
</tr>
<tr>
<td>Streaming load duration</td>
<td>Duration</td>
<td>ms</td>
<td>Streaming load duration</td>
</tr>
<tr>
<td rowspan=2>BE memory</td>
<td>Total</td>
<td>bytes</td>
<td>Size of BE memory pool</td>
</tr>
<tr>
<td>Allocated</td>
<td>bytes</td>
<td>Size of allocated BE memory</td>
</tr>
<tr>
<td rowspan=3>Process file handles</td>
<td>Used</td>
<td>count</td>
<td>Number of file handles used by BE process</td>
</tr>
<tr>
<td>SoftLimit</td>
<td>count</td>
<td>Soft limit on file handles for BE process</td>
</tr>
<tr>
<td>HardLimit</td>
<td>count</td>
<td>Hard limit on file handles for BE process</td>
</tr>
<tr>
<td>Running threads in process</td>
<td>Thread</td>
<td>count</td>
<td>Number of threads running in BE process</td>
</tr>
<tr>
<td rowspan=3>Used thrifts</td>
<td>Broker</td>
<td>count</td>
<td>Number of thrifts used by broker</td>
</tr>
<tr>
<td>Backend</td>
<td>count</td>
<td>Number of thrifts used by BE</td>
</tr>
<tr>
<td>Frontend</td>
<td>count</td>
<td>Number of thrifts used by FE</td>
</tr>
<tr>
<td>Tablet write statistics</td>
<td>Writer</td>
<td>count</td>
<td>Statistics of tablet writes on BE</td>
</tr>
</tbody></table>

## StarRocks - FE


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
<td rowspan=2>ALTER job statistics</td>
<td>RollupRunning</td>
<td>count</td>
<td>Number of running alter jobs of rollup type</td>
</tr>
<tr>
<td>SchemaChangeRunning</td>
<td>count</td>
<td>Number of running alter jobs of schema_change type</td>
</tr>
<tr>
<td rowspan=2>Image statistics</td>
<td>Write</td>
<td>count</td>
<td>Number of image writes on FE</td>
</tr>
<tr>
<td>Push</td>
<td>count</td>
<td>Number of image pushes on FE</td>
</tr>
<tr>
<td>Scheduled tablets</td>
<td>ScheduledTablet</td>
<td>count</td>
<td>Number of scheduled tablets on FE</td>
</tr>
<tr>
<td rowspan=4>Transaction status statistics</td>
<td>Reject</td>
<td>count</td>
<td>Number of rejected transactions on FE</td>
</tr>
<tr>
<td>Begin</td>
<td>count</td>
<td>Number of started transactions on FE</td>
</tr>
<tr>
<td>Success</td>
<td>count</td>
<td>Number of successful transactions on FE</td>
</tr>
<tr>
<td>Failed</td>
<td>count</td>
<td>Number of failed transactions on FE</td>
</tr>
<tr>
<td rowspan=3>Heap memory in JVM</td>
<td>max</td>
<td>bytes</td>
<td>Maximum amount of heap memory</td>
</tr>
<tr>
<td>committed</td>
<td>bytes</td>
<td>Amount of committed heap memory</td>
</tr>
<tr>
<td>used</td>
<td>bytes</td>
<td>Amount of used heap memory</td>
</tr>
<tr>
<td rowspan=2>Non-heap memory in JVM</td>
<td>committed</td>
<td>bytes</td>
<td>Amount of committed non-heap memory</td>
</tr>
<tr>
<td>used</td>
<td>bytes</td>
<td>Amount of used non-heap memory</td>
</tr>
<tr>
<td rowspan=3>Old memory in JVM</td>
<td>used</td>
<td>bytes</td>
<td>Amount of used old memory</td>
</tr>
<tr>
<td>peak_used</td>
<td>bytes</td>
<td>Maximum amount of used old memory</td>
</tr>
<tr>
<td>max</td>
<td>bytes</td>
<td>Maximum amount of old memory</td>
</tr>
<tr>
<td rowspan=3>Young memory in JVM</td>
<td>used</td>
<td>bytes</td>
<td>Amount of used young memory</td>
</tr>
<tr>
<td>peak_used</td>
<td>bytes</td>
<td>Maximum amount of used young memory</td>
</tr>
<tr>
<td>max</td>
<td>bytes</td>
<td>Maximum amount of young memory</td>
</tr>
<tr>
<td>Routine load queue size</td>
<td>report queue</td>
<td>count</td>
<td>Size of FE report queue</td>
</tr>
<tr>
<td rowspan=2>Routine load rows</td>
<td>TotalRows</td>
<td>count</td>
<td>Number of FE routine load rows</td>
</tr>
<tr>
<td>ErrorRows</td>
<td>count</td>
<td>Number of FE routine load error rows</td>
</tr>
<tr>
<td>Routine load size</td>
<td>Receive</td>
<td>bytes</td>
<td>Size of FE routine load</td>
</tr>
<tr>
<td>Maximum compaction score of tablet</td>
<td>MAX</td>
<td>score</td>
<td>Maximum compaction score of FE tablet</td>
</tr>
<tr>
<td rowspan=5>EditLog write latency</td>
<td>Quantile75</td>
<td>ms</td>
<td>75th percentile of the FE EditLog write latency</td>
</tr>
<tr>
<td>Quantile95</td>
<td>ms</td>
<td>95th percentile of the FE EditLog write latency</td>
</tr>
<tr>
<td>Quantile98</td>
<td>ms</td>
<td>98th percentile of the FE EditLog write latency</td>
</tr>
<tr>
<td>Quantile99</td>
<td>ms</td>
<td>99th percentile of the FE EditLog write latency</td>
</tr>
<tr>
<td>Quantile999</td>
<td>ms</td>
<td>99.9th percentile of the FE EditLog write latency</td>
</tr>
<tr>
<td rowspan=2>GC count</td>
<td>YoungGC</td>
<td>count</td>
<td>FE node JVM Young GC count</td>
</tr>
<tr>
<td>OldGC</td>
<td>count</td>
<td>FE node JVM Old GC count</td>
</tr>
<tr>
<td rowspan=2>GC time</td>
<td>YoungGC</td>
<td>Sec</td>
<td>FE node JVM Young GC time</td>
</tr>
<tr>
<td>OldGC</td>
<td>Sec</td>
<td>FE node JVM Old GC time</td>
</tr>
<tr>
<td rowspan=2>JVM threads</td>
<td>Total</td>
<td>count</td>
<td>Total number of threads in the JVM of the FE node</td>
</tr>
<tr>
<td>Peak</td>
<td>count</td>
<td>Peak number of threads in the JVM of the FE node</td>
</tr>
<tr>
<td rowspan=7>BROKER load job statistics</td>
<td>UNKNOWN</td>
<td>count</td>
<td>Number of load jobs of BROKER type in UNKNOWN status</td>
</tr>
<tr>
<td>PENDING</td>
<td>count</td>
<td>Number of load jobs of BROKER type in PENDING status</td>
</tr>
<tr>
<td>ETL</td>
<td>count</td>
<td>Number of load jobs of BROKER type in ETL status</td>
</tr>
<tr>
<td>LOADING</td>
<td>count</td>
<td>Number of load jobs of BROKER type in LOADING status</td>
</tr>
<tr>
<td>COMMITTED</td>
<td>count</td>
<td>Number of load jobs of BROKER type in COMMITTED status</td>
</tr>
<tr>
<td>FINISHED</td>
<td>count</td>
<td>Number of load jobs of BROKER type in FINISHED status</td>
</tr>
<tr>
<td>CANCELLED</td>
<td>count</td>
<td>Number of load jobs of BROKER type in CANCELLED status</td>
</tr>
<tr>
<td rowspan=7>DELETE load job statistics</td>
<td>UNKNOWN</td>
<td>count</td>
<td>Number of load jobs of DELETE type in UNKNOWN status</td>
</tr>
<tr>
<td>PENDING</td>
<td>count</td>
<td>Number of load jobs of DELETE type in PENDING status</td>
</tr>
<tr>
<td>ETL</td>
<td>count</td>
<td>Number of load jobs of DELETE type in ETL status</td>
</tr>
<tr>
<td>LOADING</td>
<td>count</td>
<td>Number of load jobs of DELETE type in LOADING status</td>
</tr>
<tr>
<td>COMMITTED</td>
<td>count</td>
<td>Number of load jobs of DELETE type in COMMITTED status</td>
</tr>
<tr>
<td>FINISHED</td>
<td>count</td>
<td>Number of load jobs of DELETE type in FINISHED status</td>
</tr>
<tr>
<td>CANCELLED</td>
<td>count</td>
<td>Number of load jobs of DELETE type in CANCELLED status</td>
</tr>
<tr>
<td rowspan=7>HADOOP load job statistics</td>
<td>UNKNOWN</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in UNKNOWN status</td>
</tr>
<tr>
<td>PENDING</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in PENDING status</td>
</tr>
<tr>
<td>ETL</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in ETL status</td>
</tr>
<tr>
<td>LOADING</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in LOADING status</td>
</tr>
<tr>
<td>COMMITTED</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in COMMITTED status</td>
</tr>
<tr>
<td>FINISHED</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in FINISHED status</td>
</tr>
<tr>
<td>CANCELLED</td>
<td>count</td>
<td>Number of load jobs of HADOOP type in CANCELLED status</td>
</tr>
<tr>
<td rowspan=7>INSERT load job statistics</td>
<td>UNKNOWN</td>
<td>count</td>
<td>Number of load jobs of INSERT type in UNKNOWN status</td>
</tr>
<tr>
<td>PENDING</td>
<td>count</td>
<td>Number of load jobs of INSERT type in PENDING status</td>
</tr>
<tr>
<td>ETL</td>
<td>count</td>
<td>Number of load jobs of INSERT type in ETL status</td>
</tr>
<tr>
<td>LOADING</td>
<td>count</td>
<td>Number of load jobs of INSERT type in LOADING status</td>
</tr>
<tr>
<td>COMMITTED</td>
<td>count</td>
<td>Number of load jobs of INSERT type in COMMITTED status</td>
</tr>
<tr>
<td>FINISHED</td>
<td>count</td>
<td>Number of load jobs of INSERT type in FINISHED status</td>
</tr>
<tr>
<td>CANCELLED</td>
<td>count</td>
<td>Number of load jobs of INSERT type in CANCELLED status</td>
</tr>
<tr>
<td rowspan=5>Routine load job statistics</td>
<td>NEED_SCHEDULE</td>
<td>count</td>
<td>Number of routine load jobs in NEED_SCHEDULE status</td>
</tr>
<tr>
<td>RUNNING</td>
<td>count</td>
<td>Number of routine load jobs in RUNNING status</td>
</tr>
<tr>
<td>PAUSED</td>
<td>count</td>
<td>Number of routine load jobs in PAUSED status</td>
</tr>
<tr>
<td>STOPPED</td>
<td>count</td>
<td>Number of routine load jobs in STOPPED status</td>
</tr>
<tr>
<td>CANCELLED</td>
<td>count</td>
<td>Number of routine load jobs in CANCELLED status</td>
</tr>
<tr>
<td rowspan=7>SPARK load job statistics</td>
<td>UNKNOWN</td>
<td>count</td>
<td>Number of load jobs of SPARK type in UNKNOWN status</td>
</tr>
<tr>
<td>PENDING</td>
<td>count</td>
<td>Number of load jobs of SPARK type in PENDING status</td>
</tr>
<tr>
<td>ETL</td>
<td>count</td>
<td>Number of load jobs of SPARK type in ETL status</td>
</tr>
<tr>
<td>LOADING</td>
<td>count</td>
<td>Number of load jobs of SPARK type in LOADING status</td>
</tr>
<tr>
<td>COMMITTED</td>
<td>count</td>
<td>Number of load jobs of SPARK type in COMMITTED status</td>
</tr>
<tr>
<td>FINISHED</td>
<td>count</td>
<td>Number of load jobs of SPARK type in FINISHED status</td>
</tr>
<tr>
<td>CANCELLED</td>
<td>count</td>
<td>Number of load jobs of SPARK type in CANCELLED status</td>
</tr>
<tr>
<td>FE MASTER</td>
<td>FE Master</td>
<td>count</td>
<td>Whether it is the FE master. Valid values: 1: Master; 0: Follower.</td>
</tr>
<tr>
<td rowspan=5>Node information</td>
<td>FeNodeNum</td>
<td>count</td>
<td>Total number of FE nodes</td>
</tr>
<tr>
<td>BeNodeNum</td>
<td>count</td>
<td>Total number of BE nodes</td>
</tr>
<tr>
<td>BeAliveNum</td>
<td>count</td>
<td>Number of live BE nodes</td>
</tr>
<tr>
<td>BeDecommissionedNum</td>
<td>count</td>
<td>Number of live BE nodes</td>
</tr>
<tr>
<td>BkDeadNum</td>
<td>count</td>
<td>Number of dead broker nodes</td>
</tr>
<tr>
<td rowspan=2>Request response</td>
<td>QPS</td>
<td>count/s</td>
<td>Number of queries per second</td>
</tr>
<tr>
<td>RPS</td>
<td>count/s</td>
<td>Number of requests that can be processed per second</td>
</tr>
<tr>
<td rowspan=5>FE query statistics</td>
<td>total</td>
<td>count</td>
<td>Total number of FE queries</td>
</tr>
<tr>
<td>err</td>
<td>count</td>
<td>Total number of FE query errors</td>
</tr>
<tr>
<td>timeout</td>
<td>count</td>
<td>Number of timed-out FE queries</td>
</tr>
<tr>
<td>success</td>
<td>count</td>
<td>Total number of successful FE queries</td>
</tr>
<tr>
<td>slow</td>
<td>count</td>
<td>Total number of slow FE queries</td>
</tr>
<tr>
<td>Query failure rate</td>
<td>ErrRate</td>
<td>%</td>
<td>Query error rate</td>
</tr>
<tr>
<td rowspan=4>FE query latency</td>
<td>Quantile75</td>
<td>ms</td>
<td>75th percentile of the FE query latency</td>
</tr>
<tr>
<td>Quantile95</td>
<td>ms</td>
<td>95th percentile of the FE query latency</td>
</tr>
<tr>
<td>Quantile99</td>
<td>ms</td>
<td>99th percentile of the FE query latency</td>
</tr>
<tr>
<td>Quantile999</td>
<td>ms</td>
<td>99.9th percentile of the FE query latency</td>
</tr>
<tr>
<td>Connections</td>
<td>Num</td>
<td>count</td>
<td>Number of FE node connections</td>
</tr>
</tbody></table>


## StarRocks - Broker

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
<td>count</td>
<td>Number of opened file descriptors</td>
</tr>
<tr>
<td>MaxFileDescriptorCount</td>
<td>count</td>
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
<td>count</td>
<td>Peak number of threads</td>
</tr>
<tr>
<td>ThreadCount</td>
<td>count</td>
<td>Total number of threads</td>
</tr>
<tr>
<td>DaemonThreadCount</td>
<td>count</td>
<td>Number of Daemon threads</td>
</tr>
</tbody></table>
