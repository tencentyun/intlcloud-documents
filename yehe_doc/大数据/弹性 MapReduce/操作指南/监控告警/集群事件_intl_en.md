## Feature Overview
Cluster events include event lists and event policies.
- Event list: it records key change events and exceptional events occurring in the cluster.
- Event policy: event monitoring trigger policies can be customized based on the actual business conditions. Events with monitoring enabled can be set as cluster inspection items.

## Viewing Event List
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click the **ID/name** of the target cluster in **Cluster List** to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Events** > **Event List** to view all operation events in the current cluster.
![](https://main.qcloudimg.com/raw/3e97621eafcf8ff5fd86fe47a9fb1190.png)
The severity divides into the following:
 - Fatal: exception events of a server or service that require manual intervention and will cause service interruption if left unattended. Such events may last for a period of time.
 - Severe: alert events that currently have not caused service or server interruption but will cause fatal events if left unattended.
 - Moderate: regular events occurring in the cluster that generally do not require special processing.

## Setting Event Policy
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click the **ID/name** of the target cluster in **Cluster List** to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Events** > **Event Policy** and you can customize the event monitoring trigger policies.
3. The event configuration list contains the event name, event trigger policy, severity (fatal, severe, and moderate), and option to enable/disable monitoring, which can be modified and saved.
![](https://main.qcloudimg.com/raw/3a4879afe4313cd7443b6a676cf33a80.png)
4. Event trigger policies cover two types of events: fixed system policy events (which cannot be modified) and custom events (which can be configured based on the business standards).
![](https://main.qcloudimg.com/raw/555bed19ffd53a753b49e0994a8f2c75.png)
5. You can select whether to enable event monitoring in an event policy. Only events with monitoring enabled can be selected as cluster inspection items. Monitoring is enabled by default for some events and is enabled by default and cannot be disabled for some other events. The following are the specific rules:
<table>
<thead>
<tr>
<th ><strong>Type</strong></th>
<th><strong>Event Name</strong></th>
<th><strong>Description</strong></th>
<th><strong>Recommended Measure</strong></th>
<th><strong>Default Value</strong></th>
<th><strong>Severity</strong></th>
<th><strong>Disableable</strong></th>
<th><strong>Enabled by Default</strong></th>
</tr>
</thead>
<tbody><tr>
<td rowspan="19"><strong>Node</strong></td>
<td>The CPU utilization exceeds the threshold continuously</td>
<td>The server CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average CPU utilization exceeds the threshold</td>
<td>The average server CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average CPU iowait utilization exceeds the threshold</td>
<td>The average CPU iowait utilization of the server in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Troubleshoot</td>
<td>m=60, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The 1-second CPU load exceeds the threshold continuously</td>
<td>The 1-second CPU load has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=8, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The 5-second CPU load exceeds the threshold continuously</td>
<td>The 5-second CPU load has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=8, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The memory utilization exceeds the threshold continuously</td>
<td>The memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The swap space exceeds the threshold continuously</td>
<td>The server swap memory has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.1, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The total number of system processes exceeds the threshold continuously</td>
<td>The total number of system processes has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=10,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average total number of fork subprocesses exceeds the threshold</td>
<td>The average total number of fork subprocesses in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Troubleshoot</td>
<td>m=5,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The process does not exist due to OOM</td>
<td>An OOM error occurred in the process</td>
<td>Adjust the process heap memory size</td>
<td>-</td>
<td>Severe</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>A disk I/O error occurred (this event is not supported currently)</td>
<td>A disk I/O error occurred</td>
<td>Replace the disk</td>
<td>-</td>
<td>Fatal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The disk space utilization exceeds the threshold continuously</td>
<td>The disk space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The disk I/O device utilization exceeds the threshold continuously</td>
<td>The disk I/O device utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The node file handle utilization exceeds the threshold continuously</td>
<td>The node file handle utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=85, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of TCP connections to the node exceeds the threshold continuously</td>
<td>The number of TCP connections to the node has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Check whether there are connection leaks</td>
<td>m=10,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The node process is missing</td>
<td>The node service process is missing</td>
<td>View the service logs to find out why the service failed to be pulled</td>
<td>-</td>
<td>Moderate</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>The node heartbeat is missing</td>
<td>The node heartbeat failed to be reported regularly</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Fatal</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>Incorrect hostname</td>
<td>The node's hostname is incorrect</td>
<td>Troubleshoot</td>
<td>-</td>
<td>Fatal</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>Failed to ping the metadatabase</td>
<td>The TencentDB instance heartbeat failed to be reported regularly</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td></td>
</tr>
<tr>
<td rowspan="16"><strong>HDFS</strong></td>
<td>The total number of HDFS files exceeds the threshold continuously</td>
<td>The total number of files in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Increase the NameNode memory</td>
<td>m=50,000,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average total number of HDFS files exceeds the threshold</td>
<td>The average total number of files in the cluster in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Increase the NameNode memory</td>
<td>m=50,000,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The total number of HDFS blocks exceeds the threshold continuously</td>
<td>The total number of blocks in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Increase the NameNode memory or the block size</td>
<td>m=50,000,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average total number of HDFS blocks exceeds the threshold</td>
<td>The average total number of HDFS blocks in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Increase the NameNode memory or the block size</td>
<td>m=50,000,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of HDFS data nodes marked as dead exceeds the threshold continuously</td>
<td>The number of data nodes marked as dead has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The HDFS storage space utilization exceeds the threshold continuously</td>
<td>The HDFS storage space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Clear files in HDFS or expand the cluster capacity</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average HDFS storage space utilization exceeds the threshold</td>
<td>The average HDFS storage space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Clear files in HDFS or expand the cluster capacity</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>Active/Standby NameNodes were switched</td>
<td>Active/Standby NameNodes were switched</td>
<td>Locate the cause of NameNode switch</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The NameNode RPC request processing latency exceeds the threshold continuously</td>
<td>The RPC request processing latency has been greater than or equal to m milliseconds for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=300, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current NameNode connections exceeds the threshold continuously</td>
<td>The number of current NameNode connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=2,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred on a NameNode</td>
<td>A full GC event occurred on a NameNode</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The NameNode JVM memory utilization exceeds the threshold continuously</td>
<td>The NameNode JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NameNode heap memory size</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The DataNode RPC request processing latency exceeds the threshold continuously</td>
<td>The RPC request processing latency has been greater than or equal to m milliseconds for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=300, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current DataNode connections exceeds the threshold continuously</td>
<td>The number of current DataNode connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=2,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred on a DataNode</td>
<td>A full GC event occurred on a DataNode</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The DataNode JVM memory utilization exceeds the threshold continuously</td>
<td>The DataNode JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the DataNode heap memory size</td>
<td>m=85, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="14"><strong>YARN</strong></td>
<td>The number of currently missing NodeManagers in the cluster exceeds the threshold continuously</td>
<td>The number of currently missing NodeManagers in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Check the NodeManager process status and check whether the network connection is smooth</td>
<td>m=1, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of pending containers exceeds the threshold continuously</td>
<td>The number of pending containers has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Reasonably specify resources that can be used by YARN jobs</td>
<td>m=90, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The cluster memory utilization exceeds the threshold continuously</td>
<td>The memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average cluster memory utilization exceeds the threshold</td>
<td>The average memory utilization in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The cluster CPU utilization exceeds the threshold continuously</td>
<td>The CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average cluster CPU utilization exceeds the threshold</td>
<td>The average CPU utilization in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Expand the cluster capacity</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of available CPU cores in each queue is below the threshold continuously.</td>
<td>The number of available CPU cores in each queue has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Assign more resources to the queue</td>
<td>m=1, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The available memory in each queue is below the threshold continuously</td>
<td>The available memory in each queue has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Assign more resources to the queue</td>
<td>m=1,024, t=1800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>Active/Standby ResourceManagers were switched</td>
<td>Active/Standby ResourceManagers were switched</td>
<td>Check the ResourceManager process status and view the standby ResourceManager logs to locate the cause of active/standby switch</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in a ResourceManager</td>
<td>A full GC event occurred in a ResourceManager</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The ResourceManager JVM memory utilization exceeds the threshold continuously</td>
<td>The ResourceManager JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the ResourceManager heap memory size</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in a NodeManager</td>
<td>A full GC event occurred in a NodeManager</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The available memory in NodeManager is below the threshold continuously</td>
<td>The available memory in a single NodeManager has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NodeManager heap memory size</td>
<td>m=1, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The NodeManager JVM memory utilization exceeds the threshold continuously</td>
<td>The NodeManager JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NodeManager heap memory size</td>
<td>m=85, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td rowspan="12"><strong>HBase</strong></td>
<td>The number of regions in RIT status in the cluster exceeds the threshold continuously</td>
<td>The number of regions in RIT status in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>If the HBase version is below 2.0, run `hbase hbck -fixAssigment`</td>
<td>m=1, t=60</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The number of dead RegionServers exceeds the threshold continuously</td>
<td>The number of dead RegionServers has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average number of regions in each RegionServer in the cluster exceeds the threshold continuously</td>
<td>The average number of regions in each RegionServer in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=300, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred on HMaster</td>
<td>A full GC event occurred on HMaster</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The HMaster JVM memory utilization exceeds the threshold continuously</td>
<td>The HMaster JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the HMaster heap memory size</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The number of current HMaster connections exceeds the threshold continuously</td>
<td>The number of current HMaster connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred in RegionServer</td>
<td>A full GC event occurred in RegionServer</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The RegionServer JVM memory utilization exceeds the threshold continuously</td>
<td>The RegionServer JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the RegionServer heap memory size</td>
<td>m=85, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current RPC connections to RegionServer exceeds the threshold continuously</td>
<td>The number of current RPC connections to RegionServer has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=1,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of RegionServer StoreFiles exceeds the threshold continuously</td>
<td>The number of RegionServer StoreFiles has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Run the major compaction</td>
<td>m=50,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred in HBase Thrift</td>
<td>A full GC event occurred in HBase Thrift</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The HBase Thrift JVM memory utilization exceeds the threshold continuously</td>
<td>The HBase Thrift JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the HBase Thrift heap memory size</td>
<td>m=85, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td rowspan="4"><strong>Hive</strong></td>
<td>A full GC event occurred in HiveServer2</td>
<td>A full GC event occurred in HiveServer2</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The HiveServer2 JVM memory utilization exceeds the threshold continuously</td>
<td>The HiveServer2 JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the HiveServer2 heap memory size</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in HiveMetaStore</td>
<td>A full GC event occurred in HiveMetaStore</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in HiveWebHcat</td>
<td>A full GC event occurred in HiveWebHcat</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Moderate</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="2"><strong>ZooKeeper</strong></td>
<td>The number of ZooKeeper connections exceeds the threshold continuously</td>
<td>The number of ZooKeeper connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=65,535, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of ZNodes exceeds the threshold continuously</td>
<td>The number of ZNodes has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Troubleshoot</td>
<td>m=2,000, t=1,800</td>
<td>Moderate</td>
<td>Yes</td>
<td>No</td>
</tr>
</tbody></table>

