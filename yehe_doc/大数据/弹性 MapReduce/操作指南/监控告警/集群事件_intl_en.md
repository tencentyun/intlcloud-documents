## Overview
Cluster events include event lists and event policies.
- Event list: It records key change events and abnormal events occurring in the cluster.
- Event policy: Event monitoring trigger policies can be customized based on the actual business conditions. Events with monitoring enabled can be set as cluster inspection items.

## Viewing Event List
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of a cluster in the cluster list to enter the cluster details page.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Events** > **Event List** to view all operation events in the current cluster.
![](https://main.qcloudimg.com/raw/5060d9a929e662b5b14c8fa78f3b6843.png)
The severity divides into the following:
 - Fatal: Exception events of a node or service that require manual intervention and will cause service interruption if left unattended. Such events may last for a period of time.
 - Severe: Alert events that currently have not caused service or node interruption but will cause fatal events if left unattended.
 - Moderate: Regular events occurring in the cluster that generally do not require special processing.

3. Click the value in the **Triggers today** column to view the event's trigger records, metrics, logs, and snapshots.
![](https://qcloudimg.tencent-cloud.cn/raw/d184a9581e1c72055b921964df069ec8.png)

## Setting Event Policies
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list.
2. On the cluster details page, select **Cluster Monitoring** > **Cluster Events** > **Event Policy** and you can customize the event monitoring trigger policies.
3. The event configuration list contains the event name, event trigger policy, severity (fatal, severe, and moderate), and option to enable/disable monitoring, which can be modified and saved.
![](https://main.qcloudimg.com/raw/7107d9b985db81e2b8fdbf921bf567c1.png)
4. Event trigger policies cover two types of events: fixed system policy events (which cannot be modified) and custom events (which can be configured based on the business standards).
![](https://qcloudimg.tencent-cloud.cn/raw/5fc474a988b252d0cf25f41cec7e7864.png)
5. You can select whether to enable event monitoring in an event policy. Only events with monitoring enabled can be selected as cluster inspection items. Monitoring is enabled by default for some events and is enabled by default and cannot be disabled for some other events. The following are the specific rules:
<table>
<thead>
<tr>
<th><strong>Category</strong></th>
<th><strong>Event Name</strong></th>
<th><strong>Description</strong></th>
<th><strong>Recommendations and Measure</strong></th>
<th><strong>Default Value</strong></th>
<th><strong>Severity</strong></th>
<th><strong>Disabling Allowed</strong></th>
<th><strong>Enabled by Default</strong></th>
</tr>
</thead>
<tbody><tr>
<td rowspan="24"><strong>Node</strong></td>
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
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The average CPU iowait utilization exceeds the threshold</td>
<td>The average CPU iowait utilization of the server in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Manually troubleshoot the issue</td>
<td>m=60, t=1800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The 1-second CPU load exceeds the threshold continuously</td>
<td>The 1-minute CPU load has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=8, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The 5-second CPU load exceeds the threshold continuously</td>
<td>The 5-minute CPU load has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
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
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The total number of system processes exceeds the threshold continuously</td>
<td>The total number of system processes has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=10,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average total number of fork subprocesses exceeds the threshold</td>
<td>The average total number of fork subprocesses in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Manually troubleshoot the issue</td>
<td>m=5,000, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>No Process OOM</td>
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
<td>The average disk utilization exceeds the threshold continuously</td>
<td>The average disk space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average disk I/O utilization exceeds the threshold continuously</td>
<td>The average disk I/O utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The node file handle utilization exceeds the threshold continuously</td>
<td>The node file handle utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=85, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of TCP connections to the node exceeds the threshold continuously</td>
<td>The number of TCP connections to the node has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Check whether there are connection leaks</td>
<td>m=10,000, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The configured node memory utilization exceeds the threshold</td>
<td>The memory utilization configured for all roles on the node exceeds the node's physical memory threshold</td>
<td>Adjust the allocated node process heap memory</td>
<td>90%</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The node process is unavailable</td>
<td>The node service process is unavailable</td>
<td>View the service logs to find out why the service failed to be pulled</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The node heartbeat is missing</td>
<td>The node heartbeat failed to be reported regularly</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Fatal</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>The hostname is incorrect</td>
<td>The node's hostname is incorrect</td>
<td>Manually troubleshoot the issue</td>
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
</tr>
<tr>
<td>The utilization of a single disk exceeds the threshold continuously</td>
<td>The single disk space utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The I/O utilization of a single disk exceeds the threshold continuously</td>
<td>The single disk I/O device utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The single disk inodes utilization exceeds the threshold continuously</td>
<td>The single disk inodes utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The difference between the UTC time and NTP time of the server exceeds the threshold</td>
<td>The difference between the UTC time and NTP time of the server exceeds the threshold (in ms)</td>
<td>1. Make sure that the NTP daemon is running <br>2. Make sure that the network communication with the NTP server is normal
</td>
<td>Difference=30000</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="19"><strong>HDFS</strong></td>
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
<td>Manually troubleshoot the issue</td>
<td>m=1, t=1,800</td>
<td>Normal</td>
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
<td>Manually troubleshoot the issue</td>
<td>m=300, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current NameNode connections exceeds the threshold continuously</td>
<td>The number of current NameNode connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=2,000, t=1,800</td>
<td>Normal</td>
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
<td>Manually troubleshoot the issue</td>
<td>m=300, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current DataNode connections exceeds the threshold continuously</td>
<td>The number of current DataNode connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=2,000, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A full GC event occurred on a DataNode</td>
<td>A full GC event occurred on a NameNode</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The DataNode JVM memory utilization exceeds the threshold continuously</td>
<td>The NameNode JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the DataNode heap memory size</td>
<td>m=85, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>Both NameNodes of HDFS are in Standby service status</td>
<td>Both NameNode roles are in Standby status at the same time</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The number of HDFS missing blocks exceeds the threshold</td>
<td>The number of missing blocks in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>We recommend you troubleshoot HDFS data block corruption and run the `hadoop fsck /` command to check the HDFS file distribution</td>
<td>m=1, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The HDFS NameNode entered the safe mode</td>
<td>The NameNode entered the safe mode (for 300 seconds continuously)</td>
<td>We recommend you troubleshoot HDFS data block corruption and run the `hadoop fsck /` command to check the HDFS file distribution</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="14"><strong>YARN</strong></td>
<td>The number of currently missing NodeManagers in the cluster exceeds the threshold continuously</td>
<td>The number of currently missing NodeManagers in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Check the NodeManager process status and check whether the network connection is smooth</td>
<td>m=1, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of pending containers exceeds the threshold continuously</td>
<td>The number of pending containers has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Reasonably specify resources that can be used by YARN jobs</td>
<td>m=90, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The cluster memory utilization exceeds the threshold continuously</td>
<td>The memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Scale out the cluster</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average cluster memory utilization exceeds the threshold</td>
<td>The average memory utilization in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Scale out the cluster</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The cluster CPU utilization exceeds the threshold continuously</td>
<td>The CPU utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Scale out the cluster</td>
<td>m=85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average cluster CPU utilization exceeds the threshold</td>
<td>The average CPU utilization in the last t (300 ≤ t ≤ 2,592,000) seconds has been greater than or equal to m</td>
<td>Scale out the cluster</td>
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
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The available memory in each queue is below the threshold continuously</td>
<td>The available memory in each queue has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Assign more resources to the queue</td>
<td>m=1,024, t=1,800</td>
<td>Normal</td>
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
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The available memory in NodeManager is below the threshold continuously</td>
<td>The available memory in a single NodeManager has been less than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NodeManager heap memory size</td>
<td>m=1, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The NodeManager JVM memory utilization exceeds the threshold continuously</td>
<td>The NodeManager JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Adjust the NodeManager heap memory size</td>
<td>m=85, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td rowspan="13"><strong>HBase</strong></td>
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
<td>Manually troubleshoot the issue</td>
<td>m=1, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The average number of regions in each RegionServer in the cluster exceeds the threshold continuously</td>
<td>The average number of regions in each RegionServer in the cluster has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Expand the node capacity or upgrade the node</td>
<td>m=300, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred on HMaster</td>
<td>A full GC event occurred on HMaster</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Normal</td>
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
<td>Manually troubleshoot the issue</td>
<td>m=1,000, t=1,800</td>
<td>Normal</td>
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
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of current RPC connections to RegionServer exceeds the threshold continuously</td>
<td>The number of current RPC connections to RegionServer has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=1,000, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of RegionServer StoreFiles exceeds the threshold continuously</td>
<td>The number of RegionServer StoreFiles has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Run the major compaction</td>
<td>m=50,000, t=1,800</td>
<td>Normal</td>
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
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>Both HMasters of HBase is in Standby service status</td>
<td>Both HMaster roles are in Standby status at the same time</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
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
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>A full GC event occurred in HiveWebHcat</td>
<td>A full GC event occurred in HiveWebHcat</td>
<td>Fine-tune the parameter settings</td>
<td>m=5, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan="2"><strong>ZooKeeper</strong></td>
<td>The number of ZooKeeper connections exceeds the threshold continuously</td>
<td>The number of ZooKeeper connections has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=65,535, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>The number of ZNodes exceeds the threshold continuously</td>
<td>The number of ZNodes has been greater than or equal to m for t (300 ≤ t ≤ 2,592,000) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=2,000, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td rowspan="8"><strong>Impala</strong></td>
<td>The ImpalaCatalog JVM memory utilization exceeds the threshold continuously</td>
<td>The ImpalaCatalog JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the ImpalaCatalog heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Impala daemon JVM memory utilization exceeds the threshold continuously</td>
<td>The Impala daemon JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Impala daemon heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The number of Impala Beeswax API client connections exceeds the threshold</td>
<td>The number of Impala Beeswax API client connections has been greater than or equal to m</td>
<td>Adjust the value of `fs_sevice_threads` in the `impalad.flgs` configuration in the console</td>
<td>m=64, t=120</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of Impala HiveServer2 client connections exceeds the threshold</td>
<td>The number of Impala HiveServer2 client connections has been greater than or equal to m</td>
<td>Adjust the value of `fs_sevice_threads` in the `impalad.flgs` configuration in the console</td>
<td>m=64, t=120</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The query execution duration exceeds the threshold</td>
<td>The query execution duration exceeds m seconds</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The total number of failed queries exceeds the threshold</td>
<td>The total number of failed queries has been greater than or equal to m for t seconds (300 ≤ t ≤ 604,800)</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The total number of committed queries exceeds the threshold</td>
<td>The total number of committed queries has been greater than or equal to m for t seconds (300 ≤ t ≤ 604,800)</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The query execution failure rate exceeds the threshold</td>
<td>The query execution failure rate has been greater than or equal to m for t seconds (300 ≤ t ≤ 604,800)</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr>



<tr>
<td rowspan="7"><strong>PrestoSQL</strong></td>
<td>The current number of failed PrestoSQL nodes exceeds the threshold continuously</td>
<td>The current number of failed PrestoSQL nodes has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of queuing resources in the current PrestoSQL resource group exceeds the threshold continuously</td>
<td>The number of queuing tasks in the PrestoSQL resource group has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>	Fine-tune the parameter settings</td>
<td>m=5,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed PrestoSQL queries exceeds the threshold</td>
<td>The number of failed PrestoSQL queries is greater than or equal to m</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>A full GC event occurred in a PrestoSQLCoordinator</td>
<td>A full GC event occurred in a PrestoSQLCoordinator</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The PrestoSQLCoordinator JVM memory utilization exceeds the threshold continuously</td>
<td>The PrestoSQLCoordinator JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the PrestoSQLCoordinator heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>A full GC event occurred on a PrestoSQL worker</td>
<td>A full GC event occurred on a PrestoSQL worker</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The PrestoSQLWorker JVM memory utilization exceeds the threshold continuously</td>
<td>The PrestoSQLWorker JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the PrestoSQLWorker heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td rowspan="7"><strong>Presto</strong></td>
<td>The current number of failed Presto nodes exceeds the threshold continuously</td>
<td>The current number of failed Presto nodes has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of queuing resources in the current Presto resource group exceeds the threshold continuously</td>
<td>The number of queuing tasks in the Presto resource group has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>	Fine-tune the parameter settings</td>
<td>m=5,000, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed Presto queries exceeds the threshold</td>
<td>The number of failed Presto queries is greater than or equal to m</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>A full GC event occurred on a PrestoSQL coordinator</td>
<td>A full GC event occurred on a PrestoSQL coordinator</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Presto coordinator JVM memory utilization exceeds the threshold continuously</td>
<td>The Presto coordinator JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Presto coordinator heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>A full GC event occurred on a Presto worker</td>
<td>A full GC event occurred on a Presto worker</td>
<td>Fine-tune the parameter settings</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Presto worker JVM memory utilization exceeds the threshold continuously</td>
<td>The Presto worker JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Presto worker heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td rowspan="6"><strong>Alluxio</strong></td>
<td>The current total number of Alluxio workers is below the threshold continuously</td>
<td>The current total number of Alluxio workers has been smaller than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=1, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The utilization of the capacity on all tiers of the current Alluxio worker exceeds the threshold</td>
<td>The utilization of the capacity on all tiers of the current Alluxio worker has been greater than or equal to the threshold for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Fine-tune the parameter settings</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>A full GC event occurred on an Alluxio master</td>
<td>A full GC event occurred on an Alluxio master</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Alluxio master JVM memory utilization exceeds the threshold continuously</td>
<td>The Alluxio master JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously	</td>
<td>Adjust the Alluxio worker heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>A full GC event occurred on an Alluxio worker</td>
<td>A full GC event occurred on an Alluxio worker</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The Alluxio worker JVM memory utilization exceeds the threshold continuously</td>
<td>The Alluxio worker JVM memory utilization has been greater than or equal to m for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Adjust the Alluxio master heap memory size</td>
<td>m=0.85, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td rowspan="10"><strong>kudu</strong></td>
<td>The cluster replica skew exceeds the threshold</td>
<td>The cluster replica skew has been greater than or equal to the threshold for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Run the `rebalance` command to balance the replicas</td>
<td>m=100, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The hybrid clock error exceeds the threshold</td>
<td>The hybrid clock error has been greater than or equal to the threshold for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>	Make sure that the NTP daemon is running and the network communication with the NTP server is normal</td>
<td>m=5,000,000, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of running tablets exceeds the threshold</td>
<td>The number of running tablets has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Too many tablets on a node can affect the performance. We recommend you clear unnecessary tables and partitions or expand the capacity as needed.</td>
<td>m=1,000, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed tablets exceeds the threshold</td>
<td>The number of failed tablets has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously	</td>
<td>Check whether any disk is unavailable or data file is corrupted</td>
<td>		m=1, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of failed data directories exceeds the threshold</td>
<td>The number of failed data directories has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously	</td>
<td>	Check whether the path configured in the `fs_data_dirs` parameter is available</td>
<td>		m=1, t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of full data directories exceeds the threshold</td>
<td>The number of full data directories has been greater than or equal to m for t (120 ≤ t ≤ 3,600) seconds continuously</td>
<td>Clear unnecessary data files or expand the capacity as needed</td>
<td>m=1, t=120</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of write requests rejected due to queue overloading exceeds the threshold</td>
<td>The number of write requests rejected due to queue overloading has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously		</td>
<td>Check whether the number of write hotspots or worker threads is small</td>
<td>m=10, t=300	</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr><tr>
<td>The number of expired scanners exceeds the threshold</td>
<td>The number of expired scanners has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Be sure to call the method for closing a scanner after reading data</td>
<td>m=100, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of error logs exceeds the threshold</td>
<td>The number of error logs has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=10, t=300	</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr><tr>
<td>The number of RPC requests that timed out while waiting in the queue exceeds the threshold</td>
<td>The number of RPC requests that timed out while waiting in the queue has been greater than or equal to m for t (300 ≤ t ≤ 3,600) seconds continuously</td>
<td>Check whether the system load is too high</td>
<td>m=100, t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan=1><strong>Kerberos</strong></td>
<td>The Kerberos response time exceeds the threshold</td>
<td>The Kerberos response time has been greater than or equal to m (ms) for t (300 ≤ t ≤ 604,800) seconds continuously</td>
<td>Manually troubleshoot the issue</td>
<td>m=100, t=1,800</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td rowspan=11><strong>Cluster</strong></td>
<td>The auto scaling policy has failed</td>
<td>1. The scale-out rule failed due to insufficient subnet EIPs associated with the cluster.
<br>2. The scale-out rule failed due to insufficient expansion resource inventory of the preset specifications.
<br>3. The scale-out rule failed due to insufficient account balance.
<br>4. An internal error occurred.</td>
<td>1. Switch to another subnet in the same VPC.
<br>2. Switch to specifications of resources that are sufficient or submit a ticket to contact developers.
<br>3. Top up the account to ensure that the account balance is sufficient.
<br>4. <a href="https://console.cloud.tencent.com/workorder/category">Submit a ticket</a> to contact developers.
</td>
<td>-</td>
<td>Severe</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>The execution of the auto scaling policy has timed out</td>
<td>1. Scaling cannot be performed temporarily as the cluster is in the cooldown period.
<br>2. Scaling is not triggered because the retry period upon expiration is too short.
<br>3. The cluster in the current status cannot be scaled out.
</td>
<td>1. Adjust the cooldown period for the scaling rule.
<br>2. Extend the retry period upon expiration.
<br>3. Try again later or <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to contact developers.
</td>
<td>-</td>
<td>Severe</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>The auto scaling policy is not triggered</td>
<td>1. The scale-out rule cannot be triggered because no expansion resource specification is set.
<br>2. The scale-out rule cannot be triggered because the maximum number of nodes for elastic resources is reached.
<br>3. The scale-in rule cannot be triggered because the minimum number of nodes for elastic resources is reached.	
<br>4. The time range for scaling has expired.
<br>5. The scale-in rule cannot be triggered because there are no elastic resources in the cluster.
</td>
<td>1. Set at least one elastic resource specification for the rule.
<br>2. Modify the maximum number of nodes to continue scaling out if the upper limit is reached.
<br>3. Modify the minimum number of nodes to continue scaling in if the lower limit is reached.
<br>4. Modify the effective time range of the rule if you want to continue using the rule for auto scaling.
<br>5. Execute the scale-in rule after adding elastic resources.
</td>
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>Auto scaling partially succeeded</td>
<td>1. Only partial resources were supplemented because the resource inventory was less than the required quantity for scale-out.
<br>2. Only partial resources were supplemented because the required quantity for scale-out exceeded the actual quantity of resources delivered.
<br>3. The scale-out rule was partially successful because the maximum number of nodes for elastic resources was reached.
<br>4. The scale-in rule was partially successful because the minimum number of nodes for elastic resources was reached.
<br>5. The resource supplement failed due to insufficient subnet EIPs associated with the cluster.
<br>6. The resource supplement failed due to insufficient expansion resource inventory of the preset specifications.
<br>7. The resource supplement failed due to insufficient account balance.
</td>
<td>1. Use the available resources for manual scaling to supplement the resources for auto scaling.
<br>2. Use the available resources for manual scaling to supplement the resources for auto scaling.
<br>3. Modify the maximum number of nodes to continue scaling out if the upper limit is reached.
<br>4. Modify the minimum number of nodes to continue scaling in if the lower limit is reached.
<td>5. Switch to another subnet in the same VPC.
<br>6. Switch to specifications of resources that are sufficient or submit a ticket to contact developers.
<br>7. Top up the account to ensure that the account balance is sufficient.
<td>-</td>
<td>Normal</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>The node process is unavailable</td>
<td>The node process is unavailable</td>
<td>Manually troubleshoot the issue</td>
<td>-</td>
<td>Normal</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>The process is killed by OOMKiller</td>
<td>The process OOM is killed by OOMKiller</td>
<td>Adjust the process heap memory size</td>
<td>-</td>
<td>Severe</td>
<td>No</td>
<td>Yes</td>
</tr>
<tr>
<td>A JVM or OLD exception occurred</td>
<td>A JVM or OLD exception occurred</td>
<td>Manually troubleshoot the issue</td>
<td>1. The OLD utilization reaches 80% for 5 consecutive minutes <br>Or 2. The JVM memory utilization reaches 90%</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>Timeout of service role health status occurred</td>
<td>The service role health status has timed out for t seconds (180 ≤ t ≤ 604,800)</td>
<td>The service role health status has timed out for minutes. To resolve this issue, check the logs of the corresponding service role and perform necessary actions accordingly.</td>
<td>t=300</td>
<td>Normal</td>
<td>Yes</td>
<td>No</td>
</tr>
<tr>
<td>A service role health status exception occurred</td>
<td>The service role health status has been abnormal for t seconds (180 ≤ t ≤ 604,800)</td>
<td>The service role health status has been unavailable for minutes. To resolve this issue, check the logs of the corresponding service role and perform necessary actions accordingly.</td>
<td>t=300</td>
<td>Severe</td>
<td>Yes</td>
<td>Yes</td>
</tr>
<tr>
<td>Auto scaling failed</td>
<td>This alert indicates that the auto scaling process has failed (either completely or partially)</td>
<td>Manually troubleshoot the issue</td>
<td>/</td>
<td>Severe</td>
<td>No</td>
<td>Yes</td>
</tr>
</tbody>
</table>

