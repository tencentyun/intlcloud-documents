## March 2023
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added table analysis in Kudu.</td>
<td><li>Supported viewing information by table, Tablet, and TabletServer. </li><li>Supported analyzing Tablet-level read and write QPS, storage size and other information.</li></td>
<td>2023-03-24</td>
<td><a href="https://www.tencentcloud.com/document/product/1026/54478">Kudu Table Analysis</a></td>
</tr>
<tr>
<td>Added statistics by Region in HBase.</td>
<td>Added Region-level read QPS, write QPS and other information to help locate hot spots.</td>
<td>2023-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46446">HBase Table Analysis</a></td>
</tr>
<tr>
<td>Added more monitoring metrics and alarms.</td>
<td><li>For HiveMetaStore, more than 14 monitoring metrics and alarms (including the number of opened and connected processes, Get Table requests, and currently active requests) were added.</li><li>For HiveServer2, more than 20 monitoring metrics and alarms (including the current requests and query submission time/average execution time) were added.</li><li>For YARN, alarms for the queue CPU and memory usage in percentages were added.</li></td>
<td>2023-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36884">Hive Monitoring Metrics</a>  <br><a href="https://intl.cloud.tencent.com/document/product/1026/36881">YARN Monitoring Metrics</a></td>
</tr>
<tr>
<td>Added more health status events.</td>
<td>Two events were added: exception in service role health status and timeout of service role health status.</td>
<td>2023-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36889">Cluster Events</a></td>
</tr>
<tr>
<td>Optimized log accuracy.</td>
<td>The log search accuracy was optimized, with search by keyword and by phrase supported.</td>
<td>2023-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/35372">Log Search</a></td>
</tr>
<tr>
<td>Released the Kafka cluster version: Kafka v2.0.0.</td>
<td>Released the Kafka cluster version Kafka v2.0.0, corresponding to the open-source Kafka v2.4.1.</td>
<td>2023-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456">Versions of Components</a></td>
</tr>
<tr> 
<td>Released the StarRocks cluster version: StarRocks v1.3.0.</td>
<td>Released the StarRocks cluster version StarRocks v1.3.0, corresponding to the open-source Kafka v2.4.3.</td>
<td>2023-03-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456">Versions of Components</a></td>
</tr>
<tr>
<td>Released the Hadoop cluster version: JDK11-Beta-based EMR v4.0.0.</td>
<td>Released the Hadoop cluster version JDK11-Beta-based EMR v4.0.0, with all of its components running in the JDK 11 environment.</td>
<td>2023-03-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456">Versions of Components</a></td>
</tr>
<tr>
<td>Suspended the provision of the container-based EMR service.</td>
<td>The container-based EMR service was unavailable for purchase for feature update in progress.</td>
<td>2023-03-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/48582">Overview</a></td>
</tr>
</tbody></table>


## February 2023
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added more metrics for job query in YARN.</td>
<td>Statistics of jobs submitted by users, resources consumed, and other information were added for job query in YARN.</td>
<td>2023-02-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41278" target="_blank">YARN Job Query</a></td>
</tr>
<tr>
<td>Added table analysis in Hive (based on Hive MetaStore).</td>
<td><li>Supported viewing global metrics at key dimensions such as total tables, total storage size, table count by access time, and trends.<li>Supported viewing multi-dimensional data of tables and their partitions.</td>
<td>2023-02-09</td>
<td><a href="https://www.tencentcloud.com/document/product/1026/54474" target="_blank">Hive Table Analysis</a></td>
</tr>
<tr>
<td>Added the file-level analysis feature in HDFS.</td>
<td><li>Supported viewing HDFS data distribution at key dimensions such as file count and file size.<li>Supported viewing and downloading the lists of top large files and top small files.</td>
<td>2023-02-09</td>
<td><a href="https://www.tencentcloud.com/document/product/1026/54472" target="_blank">HDFS File Storage Analysis</a></td>
</tr>
</tbody></table>

## January 2023
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>	
<tr>
<td>Supported automatic node replacement</td>
<td>Task and router nodes can be monitored, and abnormal nodes can be replaced automatically, mitigating the risk of service unavailability due to node exceptions.</td>
<td>2023-01-16</td>
<td><a href="https://cloud.tencent.com/document/product/589/85683" target="_blank">自动补偿</a></td>
</tr>	
<tr>
<td>Supported local disk repair</td>
<td>Local disk replacement events can be automatically monitored. After disk replacement, you can initialize the new disk in the console on your own.</td>
<td>2023-01-16</td>
<td><a href="https://cloud.tencent.com/document/product/589/85569" target="_blank">修复磁盘</a></td>
</tr>	
</tbody></table>


## December 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Supported Java-GC online analysis.</td>
<td>Java-GC online log analysis is supported to help you troubleshoot process exceptions due to GC, collect and record GC logs in real time, and analyze the logs.</td>
<td>2022-12-06</td>
<td><a href="https://cloud.tencent.com/document/product/589/84338" target="_blank">Java-GC 在线分析</a></td>
</tr>
<tr>
<td>Supported role-level monitoring of Kafka.</td>
<td>Kafka adds more than 70 role-level monitoring metrics and supports configuring alarms for core monitoring metrics.</td>
<td>2022-12-06</td>
<td><a href="https://cloud.tencent.com/document/product/589/84339" target="_blank">Kafka 监控指标</a></td>
</tr>
<tr>
<td>Added more default event-related metrics.</td>
<td>More event-related metrics are added, such as the UTC time and NTP time difference of the server, Kerberos response time, number of HDFS MissingBlocks, and safe mode for the HDFS NameNode.</td>
<td>2022-12-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36889" target="_blank">Cluster Event</a></td>
</tr>
<tr>
<td>Added more default alarm policies for Kudu.</td>
<td>Kudu adds more alarm policies, such as the number of teservers, number of failed data directories, and number of full data directories.</td>
<td>2022-12-06</td>
<td>-</td>
</tr>
<tr>
<td>Upgraded the configuration management feature.</td>
<td><li>The configuration status is added, and you can view the details of expired configuration and failed configuration.<li>More configuration files, configuration items, configuration item descriptions, and configuration filters are added.</td>
<td>2022-12-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31109" target="_blank">Configuration Management</a></td>
</tr>
<tr>
<td>Upgraded the YARN resource scheduling feature.</td>
<td>Label-based scheduling, queue deletion, and scheduling history viewing are supported.</td>
<td>2022-12-06</td>
<td><a href="https://cloud.tencent.com/document/product/589/83693" target="_blank">配置 Capacity Scheduler</a></td>
</tr>
<tr>
<td>Added client management.</td>
<td>The client management entry is added, and you can view the client information.</td>
<td>2022-12-06</td>
<td><a href="https://cloud.tencent.com/document/product/589/83701" target="_blank">客户端管理</a></td>
</tr>
<tr>
<td>Supported cloud disk adjustment.</td>
<td><li>You can adjust the cloud data disk models on nodes and expand and mount disks in the EMR console.<li>Heterogeneous capacity is supported by the heterogeneous capabilities of cloud disks.</td>
<td>2022-12-06</td>
<td><a href="https://cloud.tencent.com/document/product/589/83643" target="_blank">云硬盘扩容</a></td>
</tr>
<tr>
<td>Supported batch configuration of automatic renewal</td>
<td>You can batch enable/disable automatic renewal for nodes in the EMR console.</td>
<td>2022-12-06</td>
<td><a href="https://cloud.tencent.com/document/product/589/44851" target="_blank">集群续费</a></td>
</tr>
<tr>
<td>Supported batch configuration adjustment.</td>
<td>The configurations of nodes in the same billing mode and the same region can be batch adjusted.</td>
<td>2022-12-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31114" target="_blank">Adjusting Configuration</a></td>
</tr>
</tbody></table>

## November 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>	
<tr>
<td>Added more StarRocks monitoring metrics.		   	
</td>
<td>More basic monitoring metrics are added for various StarRocks roles.</td>
<td>2022-11-03</td>
<td><a href="https://cloud.tencent.com/document/product/589/82396" target="_blank">StarRocks 监控指标</a></td>
</tr>	
<tr>
<td>Supported Remote Shuffle Service (RSS) clusters for container-based EMR.</td>
<td><li>Container-based EMR supports RSS deployment in EKS.<li>Spark clusters can be associated with RSS clusters.</td>
<td>2022-11-01</td>
<td><a href="https://cloud.tencent.com/document/product/589/72672" target="_blank">Overview</a></td>
</tr>	
<tr>
<td>Supported managed scaling for automatic scaling.</td>
<td>The managed scaling feature continuously monitors the load system of the YARN cluster and automatically adds or removes compute nodes.</td>
<td>2022-11-01</td>
<td><a href="https://cloud.tencent.com/document/product/589/82668" target="_blank">托管伸缩使用配置</a></td>
</tr>
</tbody></table>

## October 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>	
<tr>
<td>Released a Hadoop cluster version of EMR v3.5.0</td>
<td>The Hadoop cluster version of EMR v3.5.0 is released to support Hive v3.1.3, Spark v3.2.2, HBase v2.4.5, Flink v1.14.5, Trino v389, Iceberg v0.13.1, Delta Lake v2.0.0, Hudi v0.12.0, Zeppelin v0.10.1, Superset v1.5.1, and Ranger v2.3.0.</td>
<td>2022-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456" target="_blank">Component Version</a></td>
</tr>	
</tbody></table>

## September 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>	
<tr>
<td>Supported Impala percentile distribution statistics.</td>
<td><li>Impala query supports statistics collection for execution status distribution and multidimensional percentile distribution.<li>More metrics are added for Impala queries, such as total/HDFS/Kudu scanned rows, memory peak, read/sent bytes, and internal total scanned/sent bytes.<li>Overview and structured profile features are provided for queries that take more than 3 seconds to execute.</td>
<td>2022-09-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41279" target="_blank">Impala Query Management</a></td>
</tr>	
<tr>
<td>Added more alarm policies for monitoring events.</td>
<td><li>100+ monitoring metrics are added for Druid in the "Elastic MapReduce (dynamic)" category in CM, for which dynamic alarm policies can be configured.<li>20 default monitoring metrics for eight services are added for default alarm policies.<li>Four Impala query events support alarm configuration through EventBridge.</td>
<td>2022-09-21</td>
<td>-</td>
</tr>	
<tr>
<td>Launched application comparison and application insights features for YARN job management.</td>
<td><li>You can view task information for TEZ jobs.<li>Application-level insights and comparison are supported for Tez/Spark/MapReduce jobs.<li>Task-level host monitoring metric comparison is supported for Tez/MapReduce jobs.<li>The experience to use YARN task information and filter task time is optimized.</td>
<td>2022-09-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41278" target="_blank">YARN Job Query</a></td>
</tr>	
</tbody></table>



## August 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>	
<tr>
<td>Released a StarRocks cluster version: StarRocks v1.1.0.</td>
<td>Added support for StarRocks v2.2.2.</td>
<td>2022-08-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456" target="_blank">Component Version</a></td>
</tr>	
<tr>
<td>Released a Druid cluster version: Druid v1.1.0.</td>
<td>Added support for Druid v0.23.0.</td>
<td>2022-08-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456" target="_blank">Component Version</a></td>
</tr>	
</tbody></table>

## July 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Launched the overview page in the console.</td>
<td>The cluster overview page displays various information, such as cluster status, health status of running services, and event statistics.</td>
<td>2022-07-22</td>
<td>-</td>
</tr>	
<tr>
<td>Upgraded the cluster overview feature.</td>
<td><li>The cluster directory navigation is optimized and upgraded.</li><li>The health status information of deployed services is refined to display real-time statistics of cluster events.
</li></td>
<td>2022-07-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31117" target="_blank">Cluster Overview</a></td>
</tr>	
<tr>
<td>Added new Impala query dimension and inspection items.</td>
<td><li>Dimensions of session ID, coordinator, and single-point memory peak are added.
</li><li>Four inspection items are added for Impala: query timeouts, total query failures, total query commits, and query execution failure rate.
</li></td>
<td>2022-07-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41279" target="_blank">Impala Query Management</a></td>
</tr>	
<tr>
<td>Added the Impala daemon role.</td>
<td>Over 70 visual Impala daemon metrics are added, which can trigger alarms in CM.</td>
<td>2022-07-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/42358" target="_blank">Impala Monitoring Metrics</a></td>
</tr>	
<tr>
<td>Added new application APIs.</td>
<td>The API for collecting YARN application queue statistics is added.</td>
<td>2022-07-22</td>
<td><a href="https://cloud.tencent.com/document/product/589/77586" target="_blank">Query Application Statistics </a></td>
</tr>	
<tr>
<td>Released a Hadoop cluster version—EMR v2.7.0.</td>
<td>Added support for Hive 2.3.9, Spark 3.2.1, HBase 2.4.5, Flink 1.14.3, Trino 385, ZooKeeper 3.6.3, Iceberg 0.13.0, Hudi 0.11.0, Alluxio 2.8.0, Zeppelin 0.10.1, Superset 1.4.1, and Ranger 2.1.0.</td>
<td>2022-07-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456" target="_blank">Component Version</a></td>
</tr>	
<tr>
<td>Improved the availability of the automatic scaling feature.</td>
<td>Scale-out rules support the hybrid deployment of multiple resource specifications as well as pay-as-you-go/spot instances.</td>
<td>2022-07-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/39660" target="_blank">Auto Scaling</a></td>
</tr>	
<tr>
<td>Added support for the RIT fixing tool for HBase.</td>
<td>Regions in the RIT status can be fixed.</td>
<td>2022-07-07</td>
<td><a href="https://cloud.tencent.com/document/product/589/77258" target="_blank">HBase RIT Fixing</a></td>
</tr>	
<tr>
<td>Started the open beta test for container-based EMR clusters.</td>
<td>Container-based EMR clusters become available in Beijing, Shanghai, and Guangzhou regions.</td>
<td>2022-07-07</td>
<td><a href="https://cloud.tencent.com/document/product/589/72672" target="_blank">Container-Based EMR</a></td>
</tr>
</tbody></table>

## June 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Optimized the configuration management feature.</td>
<td><li>Configuration management is upgraded to support configuration filtering, categorization, and comparison.
<li>The delivery priority rules for configurations at different levels are optimized to support delivery at the minimum level first.
<li>A configuration group can be specified for the selected components.
</td>
<td>2022-06-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31109" target="_blank">Configuration Management</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/31113" target="_blank">Cluster Scale-Out</a></td>
</tr>	
<tr>
<td>Added support for Hive query management.</td>
<td>The Hive service supports query management.</td>
<td>2022-06-07</td>
<td><a href="https://cloud.tencent.com/document/product/589/75229" target="_blank">Hive Query Management</a></td>
</tr>	
<tr>
<td>Optimized the YARN job query.</td>
<td>YARN job query supports displaying task information and querying task logs.</td>
<td>2022-06-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41278" target="_blank">YARN Job Query</a></td>
</tr>	
<tr>
<td>Connected to Pricing Center.</td>
<td>The pricing of EMR is connected to the Pricing Center, where you can query EMR node fees.</td>
<td>2022-06-07</td>
<td><a href="https://buy.cloud.tencent.com/price/emr" target="_blank">Pricing</a></td>
</tr>	
</tbody></table>


## May 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Optimized the scaling feature.</td>
<td><li>New subnets can be added to expand cluster node capacity.<li>The Kyuubi service supports scaling.</td>
<td>2022-05-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31113" target="_blank">Cluster Scale-Out</a></td>
</tr>	
<tr>
<td>Enhanced role management and user management.</td>
<td><li>User management supports batch import and export of users through APIs.<li>Resource management supports displaying client information.<li>The `DescribeClusterPhysicalMetaInfo` API is added for resource-level authentication.</td>
<td>2022-05-17</td>
<td>-</td>
</tr>	
</tbody></table>


## April 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the EMR v3.4.0 for the Hadoop cluster.</td>
<td><li>Added support for Spark 3.2.1, Trino 372, Flink 1.14.3, HBase 2.4.5, ZooKeeper 3.6.3, Impala 4.0.0, Zeppelin 0.10.1, Alluxio 2.8.0, Hudi 0.10.1, Iceberg 0.13.1, and GooseFS 1.2.0.<li>Renamed PrestoSQL as Trino in the new version and added support for Ranger. Monitoring metric alarms need to be configured according to Trino in the new version.</td>
<td>2022-04-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456" target="_blank">Component Version</a><br><a href="https://cloud.tencent.com/document/product/589/72846" target="_blank">Trino Monitoring Metrics</a></td>
</tr>	
<tr>
<td>Enriched monitoring.</td>
<td><li>Launched the new version of the interactive features of the event list.<li>Added event-related metrics such as node single-disk inode utilization, single-disk space utilization, single-disk IO utilization, all HBase HMasters standby, and all HDFS NameNodes standby.<li>Added monitoring metrics of the HDFS-Data node, including the block count, used disk space, available disk space, and reserved disk space.</td>
<td>2022-04-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36889" target="_blank">Cluster Event</a><br><a href="https://intl.cloud.tencent.com/document/product/1026/36880" target="_blank">HDFS Monitoring Metrics</a></td>
</tr>	
<tr>
<td>Added support for container-based EMR clusters.</td>
<td>Added support for Spark deployment based on EKS in Beijing, Shanghai, Guangzhou, and Nanjing regions.</td>
<td>2022-04-12</td>
<td><a href="https://cloud.tencent.com/document/product/589/72672" target="_blank">Overview</a></td>
</tr>	
</tbody></table>


## March 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added the StarRocks cluster type.</td>
<td>Added the StarRocks cluster type and integrated open-source StarRocks.</td>
<td>2022-03-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46453" target="_blank">StarRocks Development Guide</a></td>
</tr>
<tr>
<td>Added support for adding nodes without assigning ApplicationMasters by default.</td>
<td>Added support for adding nodes without assigning ApplicationMasters by default, ensuring that the running ApplicationMaster will not be terminated and the job can be performed normally.</td>
<td>2022-03-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41045" target="_blank">Automatically Adding Task Nodes Without Assigning ApplicationMasters</a></td>
</tr><tr>
<td>Added load-based scaling metrics.</td>
<td>Added load-based scaling metrics such as ContainerPending, AppPending, and AppRunning.</td>
<td>2022-03-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/39660" target="_blank">Auto Scaling</a></td>
</tr><tr>
<td>Added support for setting node labels for added host resources.</td>
<td>Added support for setting YARN node labels for added host resources to increase the resource utilization efficiency.</td>
<td>2022-03-08</td>
<td>-</td>
</tr>	
</tbody></table>

## January 2022
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Doris cluster version—Doris v1.2.0.</td>
<td>Released Doris v0.15.</td>
<td>2022-01-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46456" target="_blank">Component Version</a></td>
</tr>
<tr>
<td>Added support for sharing component configurations.</td>
<td>Added support for sharing the components of an existing cluster with other clusters without deploying such components again. This makes it easier to manage multiple clusters with the same component configurations.</td>
<td>January 14, 2022</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46451" target="_blank">Component Configuration Sharing</a></td>
</tr>
<tr>
<td>Added monitoring metrics.</td>
<td>Added Kylin, Zeppelin, Oozie, Storm, Livy, and Kyuubi monitoring metrics.<br>Added new CosRanger monitoring metrics.</td>
<td>-</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46448" target="_blank">Kylin Monitoring Metrics</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/46436" target="_blank">Zeppelin Monitoring Metrics</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/46437" target="_blank">Oozie Monitoring Metrics</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/46438" target="_blank">Storm Monitoring Metrics</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/46439" target="_blank">Livy Monitoring Metrics</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/46440" target="_blank">Kyuubi Monitoring Metrics</a>
<br><a href="https://intl.cloud.tencent.com/document/product/1026/42330" target="_blank">CosRanger Monitoring Metrics</a>
</td>
</tr>
<tr>
<td>Optimized log search.</td>
<td>Added support for more components and global regions and optimized log search interactions.</td>
<td>-</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/35372"  target="_blank">Log Search</a></td>
</tr>
</tbody></table>

## December 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added four use cases for the Hadoop cluster type.</td>
<td>Added the ZooKeeper, HBase, Presto, and Kudu use cases for the Hadoop cluster type to help you quickly create a cluster based on your business scenario.</td>
<td>2021-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31094" target="_blank">Cluster Types</a></td>
</tr>
<tr>
<td>Launched a new purchase page.</td>
<td>Optimized the existing cluster creation process to support the placement group node dimension for unified resource management.</td>
<td>2021-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31099" target="_blank">Creating EMR Cluster</a></td>
</tr>
<tr>
<td>Added support for system disk selection.</td>
<td>Added support for selecting the system disk type and size as needed.</td>
<td>2021-12-17</td>
<td>-</td>
</tr>
<tr>
<td>Optimized the task center.</td>
<td>Added support for viewing the details of all tasks of the current cluster inside the cluster, and optimized the interaction path of the task center for easier viewing and use.</td>
<td>2021-12-17</td>
<td>-</td>
</tr>
<tr>
<td>Launched diversified component operation features.</td>
<td>Added support for visually setting instruction-level operations of components such as HDFS and YARN.</td>
<td>2021-12-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46444" target="_blank">Service Operation</a></td>
</tr>
<tr>
<td>Added monitoring metrics.</td>
<td>Added Doris monitoring metrics.<br>Adjusted the original HBase table load to HBase table-level monitoring.</td>
<td>2021-12-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/46445" target="_blank">Doris Monitoring Metrics</a><br><a href="https://intl.cloud.tencent.com/document/product/1026/46446" target="_blank">HBase Table-Level Monitoring</a></td>
</tr>
<tr>
<td>Upgraded the operating system.</td>
<td>Upgraded the operating systems of all EMR versions of the Hadoop type to TencentOS Server to provide a more stable, secure, and high-performance cloud native runtime environment.
If you encounter any security issues related to the operating system of an existing cluster, contact us for assistance.</td>
<td>2021-12-03</td>
<td><a href="https://cloud.tencent.com/document/product/213/38027" target="_blank">Product Overview of TencentOS Server</a></td>
</tr>
</tbody></table>


## September 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Hadoop cluster version—EMR v3.3.0.</td>
<td>Added support for HBase v2.3.5, Phoenix v5.1.2, Kudu v1.15.0, Hue v4.10.0, Hudi v0.8.0, Tez v0.10.1, Livy v0.8.0, Ganglia v3.7.2, Kyuubi v1.1.0, and LDAP v2.4.44.</td>
<td>September 28, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
<tr>
<td>Added monitoring metrics.</td>
<td>Enriched Alluxio service monitoring metrics and added COSRanger monitoring metrics.</td>
<td>September 15, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/39434" target="_blank">Alluxio Monitoring Metrics</a><br/><a href="https://intl.cloud.tencent.com/document/product/1026/42330" target="_blank">COSRanger Monitoring Metrics</a></td>
</tr>
<tr>
<td>Connected to Cloud Monitor's default alarms</td>
<td>Cloud Monitor supports default alarm policies for Elastic MapReduce metrics/events.</td>
<td>September 15, 2021</td>
<td>-</td>
</tr>
</tbody></table>


## August 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for YARN resource scheduling.</td>
<td>Added support for UI-based YARN resource scheduling configuration.</td>
<td>August 31, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/42328" target="_blank">YARN Resource Scheduling</a></td>
</tr>
<tr>
<td>Added support for user management.</td>
<td>Added support for visually managing Kerberos and Ranger users.</td>
<td>August 31, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/43326" target="_blank">Managing Users</a></td>
</tr>
</tbody></table>



## July 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Hadoop cluster version—EMR v2.6.0.</td>
<td>Added support for Spark v3.0.2, Impala v3.4.0, GooseFS v1.0.0, OpenLDAP v2.4.44, Kyuubi v1.1.0, etc.</td>
<td>July 15, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
</tbody></table>


## June 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for YARN job query.</td>
<td>Added detailed metric statistics for YARN jobs.</td>
<td>June 24, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41278" target="_blank">YARN Job Query</a></td>
</tr>
<tr>
<td>Added support for Impala query management.</td>
<td>Added detailed metric statistics for Impala query jobs.</td>
<td>June 24, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/41279" target="_blank">Impala Query Management</a></td>
</tr>
<tr>
<td>Added support for automatic scaling for the spot instance mode.</td>
<td>Added support for automatically adding compute nodes of the spot instance mode.</td>
<td>June 3, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/39660" target="_blank">Auto Scaling</a></td>
</tr>
<tr>
<td>Added support for graceful scale-in.</td>
<td>When a scale-in action is triggered, nodes that are executing tasks will not be released immediately. Instead, they will be released after completing the tasks.</td>
<td>June 3, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/40694" target="_blank">Graceful Scale-In</a></td>
</tr>
<tr>
<td>Added support for integrating Knox with Tez.</td>
<td>Added support for viewing Tez tasks via UI.</td>
<td>June 3, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/40686" target="_blank">Integrating Knox with Tez</a></td>
</tr>
<tr>
<td>Added availability zones.</td>
<td>Added support for Singapore Zone 3 and Tokyo Zone 2.</td>
<td>June 3, 2021</td>
<td>-</td>
</tr>
<tr>
<td>Added regions.</td>
<td>Added support for regions such as Moscow, Frankfurt, Virginia, Bangkok, Mumbai, Tokyo, Toronto, and Seoul.</td>
<td>June 3, 2021</td>
<td>-</td>
</tr>
</tbody></table>

## May 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Kafka cluster version—Kafka v1.0.0.</td>
<td>Added support for Kafka v1.1.1, KafkaManager v2.0.0.2, Knox v1.2.0, and ZooKeeper v3.6.1.</td>
<td>May 13, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/40256" target="_blank">Kafka Development Guide</a></td>
</tr>
  <tr>
<td>Released a Doris cluster version—Doris v1.0.0.</td>
<td>Added support for Doris v0.13.0 and Knox v1.2.0.</td>
<td>May 13, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/40258" target="_blank">Doris Development Guide</a></td>
</tr>
</tbody></table>


## April 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Hadoop cluster version—EMR v3.2.0.</td>
<td>Added support for Hadoop v3.2.2, Spark v3.0.2, Presto v350, Flink v1.12.1, Alluxio v2.5.0, Ranger v2.1.0, Iceberg v0.11.0, and Hudi v0.7.0.</td>
<td>April 30, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
  <tr>
<td>Added the **Start/Stop Services** feature.</td>
<td>Added support for starting or stopping all services on a node.</td>
<td>April 27, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/40259" target="_blank">Starting/Stopping Services</a></td>
</tr>
<tr>
<td>Released a Hadoop cluster version—EMR v2.5.1.</td>
<td>Added support for Alluxio v2.5.0 and Hudi v0.5.1. Alluxio supports COS Transparent-URI.</td>
<td>April 10, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/40172" target="_blank">Support for COS Transparent-URI</a></td>
</tr>
</tbody></table>

## March 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Supported cluster restoration</td>
<td>You can renew monthly subscribed clusters in isolated status to restore them.</td>
<td> 2021-03-17 </td>
<td><a href="https://cloud.tencent.com/document/product/589/54107" target="_blank">  集群恢复  </a></td>
</tr>
</tbody></table>

## February 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the EMR service in new regions on Tencent Cloud Chinese.</td>
<td>Added support for the Bangkok, Seoul, Tokyo, Virginia, and Toronto regions on Tencent Cloud Chinese.</td>
<td>February 2, 2021</td>
<td>-</td>
</tr>
</tbody></table>


## January 2021
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added the cluster script feature.</td>
<td>Added support for running a specified script on multiple nodes at a time for higher efficiency.</td>
<td>January 26, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/39664" target="_blank">Cluster Scripts</a></td>
</tr>
<tr>
<td>Added support for cross-model configuration change.</td>
<td>You can select other models to change the node configuration when the current model is sold out.</td>
<td>January 26, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31114" target="_blank">  Adjusting Configuration</a></td>
</tr>
<tr>
<td>Added the auto scaling feature.</td>
<td>The auto scaling feature automatically adds or removes task nodes, helping you save costs while meeting the requirement for cluster computing power.</td>
<td>January 26, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/39660" target="_blank">Auto Scaling</a></td>
</tr>
<tr>
<td>Added monitoring metrics.</td>
<td><ol style="margin:0"><li>Added new monitoring metrics for the HDFS, Yarn, HBase, Hive, and Druid services.</li><li>Added support for monitoring on the Kudu and Alluxio services.</li></ol></td>
<td>January 13, 2021</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36879" target="_blank">Node Monitoring Metrics</a></td>
</tr>
<tr>
<td>Released the EMR service in Singapore on the international version.</td>
<td>Added support for Singapore Zone 1 and Singapore Zone 2 on the international version.</td>
<td>January 13, 2021</td>
<td>-</td>
</tr>
</tbody></table>

## December 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Hadoop cluster version—EMR v3.1.0.</td>
<td>Added support for Impala v3.4.0, Flink v1.10.0, HBase v2.3.3, Phoenix v5.0.0, Alluxio v2.3.0, Kudu v1.13.0, and ZooKeeper v3.6.1.</td>
<td>December 14, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
</tbody></table>

## November 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released the EMR TianQiong edition.</td>
<td>Added support for Spark materialized views.</td>
<td>November 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a><br><a href="https://intl.cloud.tencent.com/document/product/1026/38962" target="_blank">EMR TianQiong Introduction</a></td>
</tr>
<tr>
<td>Optimized monitoring and alarming.</td>
<td><li>Added support for setting alarms for disk monitoring metrics in Cloud Monitor (CM).
<li>Added support for customizing EMR monitoring dashboard in CM dashboard.
<li>Added support for subscribing to EMR event monitoring alarms in CM.
</td>
<td>November 20, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/248/38461" target="_blank">Dashboard</a></td>
</tr>
</tbody></table>

## October 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for Cloud Object Storage (COS) password-free access.</td>
<td>Added support for authorizing access to COS through roles. Authorized users do not need to enter an authorization key and private key.</td>
<td>2020-10-26</td>
<td>-</td>
</tr>
<tr>
<td>Added new service inspection items to the inspection system.</td>
<td>Added the HDFS, Yarn, HBase, Hive, and ZooKeeper service inspection items, enhancing the health check of metrics.</td>
<td>2020-10-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36890" target="_blank">Cluster Inspection</a></td>
</tr>
<tr>
<td>Added support for customizing event policies.</td>
<td>Added support for customizing event policies so you can identify cluster events more efficiently.</td>
<td>2020-10-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36889" target="_blank">Cluster Event</a></td>
</tr>
</tbody></table>

## September 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Hadoop cluster version—EMR v2.5.0.</td>
<td>Upgraded the Alluxio component to the stable version 2.3.0, which delivers better performance in the use cases where compute and storage are separated.</td>
<td>September 17, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
</tbody></table>

## August 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Released a Hadoop cluster version—EMR v2.4.0.</td>
<td>Added the Kudu component and upgraded some existing components.</td>
<td>August 27, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
<tr>
<td>Added support for data migration in ClickHouse clusters.</td>
<td>Improved cluster resource utilization for data security.</td><td>August 17, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/38165" target="_blank">ClickHouse Data Migration Guide</a></td>
</tr>
</tbody></table>

## July 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for custom configuration files.</td>
<td>Added support for custom configuration files, which improves the flexibility of configuration management.</td><td>July 29, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31109" target="_blank">Configuration Management</a></td>
</tr>
<tr>
<td>Optimized configuration item editing.</td>
<td>Added descriptions for configuration items and support for restoring them to defaults.</td>
<td>2020-07-29</td>
<td>-</td>
</tr>
</tbody></table>

## June 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody>
<tr>
<td>Added support for Druid service monitoring and HBase Thrift role monitoring.</td>
<td>Improved troubleshooting efficiency.</td><td>June 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36888" target="_blank">Druid Monitoring Metrics</a></td>
</tr>
<tr>
<td>Released a Hadoop cluster version—EMR v2.3.0.</td>
<td>Added support for the TensorFlow and Jupyter Notebook components.</td>
<td>June 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36892" target="_blank">TensorFlow Overview</a><br><a href="https://intl.cloud.tencent.com/document/product/1026/36894" target="_blank">Jupyter Notebook Overview</a></td>
</tr>
<tr>
<td>Released ClickHouse v1.1.0 for ClickHouse clusters.</td>
<td>Upgraded the ClickHouse component version to the LTS version, and added support for the Superset component.</td><td>June 15, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Added support for cluster events and cluster inspections.</td>
<td>Added support for recording major change events and exception events in clusters in the console for improved efficiency of cluster troubleshooting. Added support for one-time inspections and periodical inspections, making it easier to keep track of the health of your clusters and to deal with exceptions and risks in time.
 </td><td>June 4, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36889" target="_blank">Cluster Event</a><br><a href="https://intl.cloud.tencent.com/document/product/1026/36890" target="_blank">Cluster Inspection</a></td>
</tr>
</tbody></table>

## May 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Optimized console interactions, UI, and operation paths.</td>
<td>Improved operation path hierarchy for easier service management.</td><td>May 15, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Added support for service monitoring for ClickHouse clusters.</td>
<td>Made it easier to keep track of the operation status of ClickHouse clusters.</td><td>May 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36887" target="_blank">ClickHouse Monitoring Metrics</a></td>
</tr>
<tr>
<td>Added support for monitoring status for role management.</td>
<td>Made it easier to keep track of the real-time status of role processes.</td>
<td>May 15, 2020</td>
<td>-</td>
</tr>
</tbody></table>


## April 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added new cluster types.</td>
<td>Added support for the ClickHouse and Druid clusters to provide more real-time query solutions.</td><td>April 15, 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/35872" target="_blank">ClickHouse Overview</a><br><a href="https://intl.cloud.tencent.com/document/product/1026/35875" target="_blank">Druid Overview</a></td>
</tr>
<tr>
<td>Optimized bootstrap actions.</td>
<td>Added support for the running occasions of bootstrap actions before a cluster starts. Added support for adjusting bootstrap actions after a cluster is created, so you can change your bootstrap actions based on business changes.</td><td>April 15, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Optimized service restart policies.</td>
<td>Added support for setting service restart policies, so you can select a proper restart method and a policy for handling restart exceptions.</td>
<td>2020-04-15</td>
<td>-</td>
</tr>
</tbody></table>


## March 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Optimized the cluster monitoring page.</td>
<td>Optimized the cluster overview, service monitoring, and node monitoring pages for improved readability. Monitoring metrics now support customization and heat maps about nodes.</td><td>March 2020</td>
<td>-</td>
</tr>
<tr>
<td>Added support for log search.</td>
<td>Added support for filtering by log file, node IP, and time range, and viewing cluster log content. <strong>(Currently, this feature is supported only in Guangzhou region.)</strong></td><td>2020-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/35372"  target="_blank">Log Search</a></td>
</tr>
<tr>
<td>Released EMR v2.2.0.</td>
<td>Upgraded Hadoop to v2.8.5. Upgraded common components such as Spark, Hive, and HBase. Added the Hudi, Superset, Livy, Impala, Zeppelin, and Kylin components.</td>
<td>2020-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
</tbody></table>

## February 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for sharing Hive metadatabase.</td>
<td>Added support for associating an external Hive metadatabase to store the Hive metadata of a new cluster, so multiple Hive clusters can share metadata.</td><td>February 2020</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/35013" target="_blank">Hive Metadata Management</a></td>
</tr>
<tr>
<td>Optimized cluster operation logs.</td>
<td>Added display items for cluster operation logs to increase the readability of operation logs.</td><td>February 2020</td>
<td>-</td>
</tr>
<tr>
<td>Released the international version.</td>
<td>Released the international version in Beijing, Shanghai, Guangzhou, and Mumbai regions.</td><td>2020-02</td>
<td>-</td>
</tr>
</tbody></table>

## January 2020
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for cloud disk encryption.</td>
<td>Added support for cloud disk encryption for Cloud Block Storage (CBS) users on the allowlist when creating an EMR cluster.</td><td>January 2020</td>.
<td><a href="https://intl.cloud.tencent.com/document/product/362/33139" target="_blank">Cloud Disk Encryption</a></td>
</tr>
<tr>
<td>Added support for mounting cloud disks to a task node.</td>
<td>Added support for mounting cloud disks to a task node when creating or scaling out a cluster.</td><td>January 2020</td>
<td>-</td>
</tr>
<tr>
<td>Released EMR in Nanjing region.</td>
<td>Released EMR in Nanjing region.</td><td>2020-01</td>
<td>-</td>
</tr>
</tbody></table>

## December 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released the feature of delivering group configuration.</td>
<td>Added support for delivering group configuration. If the configuration of a node is different from that of the configuration group to which the node belongs, the configuration of the configuration group can be delivered to the node.</td><td>December 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of resource-level CAM authorization.</td>
<td>Added support for CAM authorization at the resource level.</td><td>December 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of associating CHDFS.</td>
<td>Added support for associating CHDFS and reading/writing data on CHDFS.</td><td>December 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/35773" target="_blank">Mounting CHDFS</a></td>
</tr>
<tr>
<td>Released the AMD model.</td>
<td>Released the AMD Standard SA2 model in Beijing, Shanghai, and Guangzhou regions.</td><td>2019-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/213/11518" target="_blank">Instance Types</a></td>
</tr>
<tr>
<td>Added the cluster monitoring overview page.</td>
<td>Added the cluster monitoring overview page, which provides the views about the cluster, node, and service status.</td><td>December 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31117" target="_blank">Cluster Overview</a></td>
</tr>
<tr>
<td>Added support for selecting metric display granularity as needed on the service monitoring page.</td>
<td>Optimized the service monitoring page, so you can select a metric display granularity as needed.</td><td>December 2019</td>
<td>-</td>
</tr>
<tr>
<td>Added support for node service deployment and load status views on the node monitoring page.</td>
<td>Optimized the node monitoring page, which provides the views about node service deployment and load status.</td><td>December 2019</td>
<td>-</td>
</tr>
</tbody></table>

## November 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added support for node specification management.</td>
<td>Added support for setting the default specification of nodes based on their billing mode. The default specification is pay-as-you-go.</td><td>2019-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/34533" target="_blank">Node Specification Management</a></td>
</tr>
<tr>
<td>Added support for the configuration of the ZooKeeper, Alluxio, and Flink components.</td>
<td>Added support for the configuration of the ZooKeeper, Alluxio, and Flink components.</td><td>November 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of tagging clusters and nodes.</td>
<td>Added support for tagging clusters and nodes.</td><td>November 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/34532" target="_blank">Setting Tag</a></td>
</tr>
<tr>
<td>Released new models in Beijing, Shanghai, and Guangzhou regions.</td>
<td>Released the S5, M5, C3, and CN3 models in Beijing, Shanghai, and Guangzhou regions.</td><td>2019-11</td>
<td>-</td>
</tr>
</tbody></table>

## October 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released EMR v3.0.0.</td>
<td>Released EMR v3.0.0 with updated versions of major components.</td><td>October 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
</tbody></table>

## September 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added full support for TencentCloud API 3.0.</td>
<td>Added full support for TencentCloud API 3.0. Standardized the output/input parameters of certain existing v3.0 APIs. Added full support for v2.0 APIs in v3.0.</td><td>September 2019</td>
<td>-</td>
</tr>
<tr>
<td>Modified console configuration.</td>
<td>Disused the escape feature for special characters.</td><td>September 2019</td>
<td>-</td>
</tr>
<tr>
<td>Added support for CM alarm policy configuration.</td>
<td>Added support for configuring alarm policies in CM (in the Elastic MapReduce product category) for key metrics for node and service monitoring.</td><td>September 2019</td>
<td>-</td>
</tr>
</tbody></table>

## August 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released the software configuration feature.</td>
<td>Added support for software configuration, which enables you to create a cluster with custom component parameters. The feature of accessing external clusters was added as well.</td><td>August 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/34530" target="_blank">Software Configuration</a></td>
</tr>
<tr>
<td>Added support for configuring the remote login port when you purchase a cluster.</td>
<td>Added support for enabling or disabling the remote login port when you purchase a cluster.</td><td>August 2019</td>
<td>-</td>
</tr>
<tr>
<td>Added support for mounting multiple cloud disks to a new cluster.</td>
<td>Added support for mounting multiple cloud disks to a new cluster.</td><td>August 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of scaling specified components.</td>
<td>Added support for scaling specified components.</td><td>August 2019</td>
<td>-</td>
</tr>
<tr>
<td>Added monitoring metrics.</td>
<td>Added new monitoring metrics for the Spark, Hive, Presto, and ZooKeeper components.</td><td>August 2019</td>
<td>-</td>
</tr>
</tbody></table>

## July 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released the feature of HBase table-level monitoring.</td>
<td>Added support for HBase table-level monitoring, which covers the number of read and write requests and storage of each table in HBase.</td><td>July 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31118" target="_blank">Service Monitoring</a></td>
</tr>
<tr>
<td>Released EMR in new regions.</td>
<td>Added support for the Singapore, Mumbai, and Chengdu regions.</td><td>July 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released new models.</td>
<td>Released the Standard S4 and Standard Network-Optimized SN3ne models in Beijing, Shanghai, and Guangzhou regions.</td><td>2019-07</td>
<td>-</td>
</tr>
<tr>
<td>Optimized the interactions of monitoring pages and added new monitoring metrics.</td>
<td>Optimized the interactions of monitoring pages and added new monitoring metrics.</td><td>July 2019</td>
<td>-</td>
</tr>
<tr>
<td>Optimized WebUI proxy address.</td>
<td>Optimized WebUI proxy address.</td><td>July 2019</td>
<td>-</td>
</tr>
</tbody></table>

## June 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released the feature of accessing external clusters.</td>
<td>Added support for accessing external clusters.</td>
<td>June 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of setting bootstrap actions.</td>
<td>Added support for setting bootstrap actions.</td>
<td>June 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/34521" target="_blank">Bootstrap Actions</a></td>
</tr>
<tr>
<td>Released the feature of delivering component parameter configuration to nodes.</td>
<td>Added support for delivering component parameter configuration to nodes.</td>
<td>June 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of rolling back parameter configuration.</td>
<td>Added support for rolling back parameter configuration.</td>
<td>June 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/34524" target="_blank">Configuration Rollback</a></td>
</tr>
</tbody></table>

## May 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released EMR v2.1.0.</td>
<td>Released EMR v2.1.0 with updated versions of main components.</td>
<td>May 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31095" target="_blank">Component Version</a></td>
</tr>
<tr>
<td>Added support for Kerberos security clusters.</td>
<td>Added support for creating security clusters. The open source components in clusters are launched in Kerberos security mode. In this security environment, only authenticated clients can access the services (such as HDFS) of the clusters.</td>
<td>May 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31163" target="_blank">Kerberos Introduction</a></td>
</tr>
<tr>
<td>Optimized monitoring metrics.</td>
<td>Optimized the Node, HDFS, YARN, and HBase monitoring metrics.</td>
<td>May 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/36879" target="_blank">Node Monitoring Metrics</a></td>
</tr>
<tr>
<td>Optimized the style of console.</td>
<td>Improved the style of console for a better interactive experience.</td>
<td>May 2019</td>
<td>-</td>
</tr>
<tr>
<td>Optimized CVM and TencentDB naming.</td>
<td>Optimized CVM and TencentDB naming with the EMR cluster serial number for easier locating of cluster information.</td>
<td>May 2019</td>
<td>-</td>
</tr>
<tr>
<td>Changed the setting of public IPs of master nodes to optional.</td>
<td>Changed the setting of public IPs of master nodes to optional.</td>
<td>May 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released the feature of adjusting the number of common nodes.</td>
<td>Added support for adjusting the number of common nodes as needed.</td>
<td>May 2019</td>
<td>-</td>
</tr>
</tbody></table>

## March 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Released new models.</td>
<td>Released the I3 model in Beijing, Shanghai, and Guangzhou regions. This model is included in the CVM allowlist, and you can purchase it only if you are in the I3 allowlist.</td>
<td>March 2019</td>
<td>-</td>
</tr>
<tr>
<td>Released EMR in a new region.</td>
<td>Made the purchase of EMR clusters available in the Silicon Valley region.</td>
<td>March 2019</td>
<td>-</td>
</tr>
<tr>
<td>Added support for router nodes.</td>
<td>Added support for router nodes, which are mainly used to relieve the load of master nodes and as task submitters.</td>
<td>March 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31094" target="_blank">Node Type Description</a></td>
</tr>
<tr>
<td>Released the feature of adjusting node configuration.</td>
<td>Added support for adjusting node configuration. Nodes can be upgraded to a higher configuration.</td>
<td>March 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31114" target="_blank">Adjusting Configuration</a></td>
</tr>
</tbody></table>

## January 2019
<table>
<thead>
<tr>
<th width=20%>Update</th>
<th width=45%>Description</th>
<th width=15%>Release Date</th>
<th width=20%>Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Added new components to existing clusters.</td>
<td>Added support for adding new components to existing clusters.</td>
<td>January 2019</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1026/31108" target="_blank">Adding Components</a></td>
</tr>
</tbody></table>
