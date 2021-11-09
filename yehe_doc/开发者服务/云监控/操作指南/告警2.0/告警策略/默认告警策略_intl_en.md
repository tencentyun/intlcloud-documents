
[](id:step1)
## Overview

Currently, the default alarm policy is only supported for CVM - basic monitoring, TencentDB for MongoDB, TencentDB for MySQL - server monitoring, TencentDB for Redis, TDSQL for MySQL, TDSQL for PostgreSQL, CKafka - instance, ES, DTS, and EMR.

- When you successfully purchase a Tencent Cloud service that supports the default policy for the first time, Cloud Monitor will automatically create the default alarm policy for you. For more information on the metrics/events supported by the default policy or alarm rules, please see the [default policy description](#step1).
- You can also manually create an alarm policy and set it as the default alarm policy. After the default policy is set, newly purchased instances will be automatically associated with the default policy without requiring manual addition.
![](https://main.qcloudimg.com/raw/acb5a0ed0f4f44b65a87337d910e17c1.png)

## Default Metric Description

[](id:step1)

<table>
    <tr>
        <th>Product Name</th>
        <th>Alarm Type</th>
        <th>Metric/Event Name</th>
        <th>Alarm Rule</th>
    </tr>
    <tr>
        <td rowspan="5">CVM</td>
        <td rowspan="4">Metric alarm</td>
        <td>CPU utilization</td>
        <td>The statistical period is 1 minute, the threshold is >95%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Memory utilization</td>
        <td>The statistical period is 1 minute, the threshold is >95%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Disk utilization</td>
        <td>The statistical period is 1 minute, the threshold is >95%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Public network bandwidth utilization</td>
        <td>The statistical period is 1 minute, the threshold is >95%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Event alarm</td>
        <td>Read-only disk</td>
        <td>-</td>
    </tr>
    <tr>
        <td rowspan="3">TencentDB for MySQL<br> - server monitoring</td>
        <td rowspan="2">Metric alarm</td>
        <td>Disk utilization</td>
        <td>The statistical period is 1 minute, the threshold is >80%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>CPU utilization</td>
        <td>The statistical period is 1 minute, the threshold is >80%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Event alarm</td>
        <td>OOM</td>
        <td>-</td>
    </tr>
    <td rowspan="2">TencentDB for <br>MongoDB</td>
    <td rowspan="2">Metric alarm</td>
    <td>Disk utilization</td>
    <td>The statistical period is 1 minute, the threshold is >80%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Connection utilization</td>
        <td>The statistical period is 1 minute, the threshold is >80%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td nowrap="nowrap">TencentDB for Redis<br> - CKV version/community version</td>
        <td>Metric alarm</td>
        <td>Capacity utilization</td>
        <td>The statistical period is 1 minute, the threshold is >80%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td rowspan="2">TDSQL for MySQL<br></td>
        <td rowspan="2">Event alarm</td>
        <td>OOM</td>
        <td rowspan="2">-</td>
    </tr>
    <tr>
        <td>Instance read-only status (disk overrun)</td>
    </tr>
    <td rowspan="2">TDSQL for PostgreSQL<br></td>
    <td rowspan="2">Event alarm</td>
    <td>Insufficient memory</td>
    <td rowspan="2">-</td>
    </tr>
    <tr>
        <td>OOM</td>
    </tr>
    <tr>
        <td>CKafka<br> - instance</td>
        <td>Metric alarm</td>
        <td>Disk utilization</td>
        <td>The statistical period is 1 minute, the threshold is >85%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td rowspan="4">ES</td>
        <td rowspan="4">Metric alarm</td>
        <td>Average disk utilization</td>
        <td>The statistical period is 1 minute, the threshold is >80%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Average CPU utilization</td>
        <td>The statistical period is 1 minute, the threshold is >90%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Average JVM memory utilization</td>
        <td>The statistical period is 1 minute, the threshold is >85%, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td>Cluster health</td>
        <td>The statistical period is 1 minute, the threshold is >=1, and the continuous monitoring duration is 5 monitoring data points</td>
    </tr>
    <tr>
        <td rowspan="3">DTS</td>
        <td rowspan="3">Event alarm</td>
        <td>Data migration task interruption</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Data sync task interruption</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Data subscription task interruption</td>
        <td>-</td>
    </tr>
    <tr>
        <td rowspan="2"><span>EMR - server monitoring - disk</span></td>
        <td  rowspan="2"><span>Metric alarm</span></td>
        <td><span>Disk utilization (used_all)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;80%, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>inode utilization</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;50%, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td ><span>EMR - server monitoring - CPU</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>CPU utilization (idle)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &lt;2%, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - server monitoring - memory</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>Memory utilization (used_percent)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;95%, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - server monitoring - network</span></td>
        <td><span>Event alarm</span></td>
        <td><span>Metadatabase ping failure</span></td>
        <td><span>-</span></td>
    </tr>
    <tr>
        <td><span>EMR - cluster monitoring</span></td>
        <td><span>Event alarm</span></td>
        <td><span>Elastic scaling failure</span></td>
        <td><span>-</span></td>
    </tr>
    <tr>
        <td rowspan="2"><span>EMR - HBase - overview</span></td>
        <td  rowspan="2"><span>Metric alarm</span></td>
        <td><span>Number of cluster RSs (numDeadRegionServers)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of cluster regions in RIT state (ritCountOverThreshold)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - HBase - HMaster</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="3"><span>EMR - HBase - RegionServer</span></td>
        <td rowspan="3"><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of regions (regionCount)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;600, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of requests in operation queue (compactionQueueLength)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;500, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="3"><span>EMR - HDFS - NameNode</span></td>
        <td rowspan="2"><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of missing blocks (NumberOfMissingBlocks)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Event alarm</span></td>
        <td><span>NameNode master/slave switch</span></td>
        <td><span>-</span></td>
    </tr>
    <tr>
        <td rowspan="2"><span>EMR - HDFS - DataNode</span></td>
        <td rowspan="2"><span>Metric alarm</span></td>
        <td><span>Number of XCeivers (XceiverCount)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;1,000, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="4"><span>EMR - HDFS - overview</span></td>
        <td rowspan="4"><span>Metric alarm</span></td>
        <td><span>Disk failure</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of cluster DataNodes (NumDeadDataNodes)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of cluster DataNodes (NumStaleDataNodes)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>HDFS storage space utilization (capacityusedrate)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is 90%, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - Presto - Presto_Coordinator</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - Presto - Presto_Worker</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - Presto - overview</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>Number of nodes (Failed)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - ClickHouse - server</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>Number of largest active data blocks in partition</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;250, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="3"><span>EMR - Hive - HiveMetaStore</span></td>
        <td rowspan="3"><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>DaemonThreadCount</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;2,000, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>ThreadCount</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;2,000, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="3"><span>EMR - Hive - HiveSever2</span></td>
        <td rowspan="3"><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>DaemonThreadCount</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;2,000, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>ThreadCount</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;2,000, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="2"><span>EMR - YARN - overview</span></td>
        <td rowspan="2"><span>Metric alarm</span></td>
        <td><span>Number of nodes (NumUnhealthyNMs)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of nodes (NumLostNMs)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;0, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>EMR - YARN - NodeManager</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td rowspan="2"><span>EMR - YARN - ResourceManger</span></td>
        <td><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Event alarm</span></td>
        <td><span>ResourceManager master/slave switch</span></td>
        <td><span>-</span></td>
    </tr>
    <tr>
        <td rowspan="3"><span>EMR - ZooKeeper - ZooKeeper</span></td>
        <td rowspan="3"><span>Metric alarm</span></td>
        <td><span>GC time (FGCT)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;5s, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of Znodes (zk_znode_count)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;100,000, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
    <tr>
        <td><span>Number of queuing requests (zk_outstanding_requests)</span></td>
        <td><span>The statistical period is 1 minute, the threshold is &gt;50, and an alarm will be triggered once every 5 consecutive times the conditions are met</span></td>
    </tr>
</table>
