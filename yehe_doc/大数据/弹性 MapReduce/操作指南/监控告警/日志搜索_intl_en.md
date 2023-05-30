## Overview
The log search feature collects component operation logs. Then, you can search for core service logs of the current cluster and node system logs by keyword to quickly view key service logs without logging in to nodes.

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list.
2. On the cluster details page, choose **Cluster Monitoring** > **Log Search** to filter and view log content by current cluster, log file, node IP, and time range.
	Alternatively, choose **Cluster Service** > target component block > **Role Management**, click a **Node IP** in **Role List** to enter the page where the node monitoring metrics are displayed, and then click **Role Log** to enter the **Log Search** page.
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/VSB5235_%E5%9B%BD%E9%99%85%E7%AB%9934.png)
	Click a **Node IP** to enter the **Node Status** page, or click **Log Source** to enter the page where the node monitoring metrics are displayed.
	![](https://staticintl.cloudcachetci.com/yehe/backend-news/fECE443_%E5%9B%BD%E9%99%8535.png)
	**Keyword description:**
	- Supports full-text search based on keywords.
	- Supports search by using special symbols, including hyphen (-), period (.), asterisk (*), greater-than sign (>), less-than sign (<), equal sign (=), exclamation mark (!), brackets (() and {}), and forward slash (/).
	- Supports phrase-based search. Example: `address=/ip:port`.
3. During troubleshooting, you usually need to pay attention to contextual logs of keywords. On the **Log Search** page, click **View Context** to enter the **Log Context** page.

## Service Types Supported for Log Search
>!
>- Currently, only logs in the past 15 days can be searched for.
>- If log collection has not been enabled on your cluster, you can contact your Tencent Cloud rep for assistance.

<table>
<thread>
<tr>
<th width=15%>Component</th>
<th width=15%>Role</th>
<th width=45%>Log</th>
<th width=25%>Description</th>
</tr>
</thread>
<tr>
<td rowspan=5>HDFS</td>
<td >NameNode</td>
<td >	/data/emr/hdfs/logs/hadoop-hadoop-namenode.log</td>
<td >NameNode runtime log</td>
</tr><tr>
<td >ZKFC</td>
<td >	/data/emr/hdfs/logs/hadoop-hadoop-zkfc.log</td>
<td >ZKFC runtime log</td>
</tr><tr>
<td >DataNode</td>
<td >/data/emr/hdfs/logs/hadoop-hadoop-datanode.log</td>
<td >DataNode runtime log</td>
</tr><tr>
<td >JournalNode</td>
<td >/data/emr/hdfs/logs/hadoop-hadoop-journalnode.log</td>
<td >JournalNode runtime log</td>
</tr><tr>
<td >DFSRouter</td>
<td >/data/emr/hdfs/logs/hadoop-hadoop-dfsrouter.log</td>
<td >DFRouter runtime log</td>
</tr><tr>
<td rowspan=3>YARN</td>
<td >ResourceManager</td>
<td >	/data/emr/yarn/logs/yarn-hadoop-resourcemanager.log</td>
<td >ResourceManager runtime log</td>
</tr><tr>
<td >NodeManager</td>
<td >	/data/emr/yarn/logs/yarn-hadoop-nodemanager.log</td>
<td >NodeManager runtime log</td>
</tr><tr>
<td >JobHistoryServer</td>
<td >/data/emr/yarn/logs/mapred-hadoop-historyserver.log</td>
<td >JobHistoryServer runtime log</td>			
</tr><tr>
<td rowspan=3>HBase</td>
<td >HMaster</td>
<td >	/data/emr/hbase/logs/hbase-hadoop-master.log</td>
<td >HMaster runtime log</td>
</tr><tr>
<td >ThriftServer</td>
<td >	/data/emr/hbase/logs/hbase-hadoop-thrift.log</td>
<td >ThriftServer runtime log</td>
</tr><tr>
<td >RegionServer</td>
<td >/data/emr/hbase/logs/hbase-hadoop-regionserver.log</td>
<td >RegionServer runtime log</td>			
</tr><tr>
<td >ClickHouse</td>
<td >ClickHouse-server</td>
<td >/data/clickhouse/clickhouse-server/logs/clickhouse-server.log</td>
<td >ClickHouse-server runtime log</td>			
</tr><tr>
<td rowspan=6>Druid</td>
<td >Broker</td>
<td >	/data/emr/druid/var/log/druid/broker.log</td>
<td >	Broker runtime log</td>
</tr><tr>
<td >Coordinator</td>
<td >/data/emr/druid/var/log/druid/coordinator.log</td>
<td >Coordinator runtime log</td>
</tr><tr>
<td >Router</td>
<td >/data/emr/druid/var/log/druid/router.log</td>
<td >Router runtime log</td>			
</tr><tr>
<td >Overload</td>
<td >	/data/emr/druid/var/log/druid/overload.log</td>
<td >Overload runtime log</td>			
</tr><tr>
<td >Historical</td>
<td >/data/emr/druid/var/log/druid/historical.log</td>
<td >Historical runtime log</td>			
</tr><tr>
<td >MiddleManager</td>
<td >/data/emr/druid/var/log/druid/middleManager.log	</td>
<td >MiddleManager runtime log</td>			
</tr><tr>
<td >Zookeeper</td>
<td >Zookeeper</td>
<td >/data/emr/zookeeper/logs/zookeeper-root-server.log	</td>
<td >ZooKeeper runtime log</td>			
</tr><tr>
<td >Hive</td>
<td >HiveServer2</td>
<td >/data/emr/hive/logs/hadoop-hive</td>
<td >HiveServer2 runtime log</td>			
</tr><tr>
<td rowspan=2>Kudu</td>
<td >KuduMaster</td>
<td >/data/emr/kudu/logs/kudu-master.WARNING</td>
<td >KuduMaster runtime log</td>			
</tr><tr>
<td >KuduServer</td>
<td >	/data/emr/kudu/logs/kudu-tserver.WARNING</td>
<td >KuduServer runtime log</td>			
</tr><tr>
<td rowspan=2>Alluxio</td>
<td >AlluxioMaster</td>
<td >/data/emr/alluxio/logs/master.log</td>
<td >AlluxioMaster runtime log</td>			
</tr><tr>
<td >AlluxioWorker</td>
<td >/data/emr/alluxio/logs/worker.log</td>
<td >AlluxioWorker runtime log</td>			
</tr><tr>
<td >Ranger</td>
<td >EmbeddedServer</td>
<td >/data/emr/ranger/logs/ranger-admin.log</td>
<td >EmbeddedServer runtime log</td>			
</tr><tr>
<td >CosRanger</td>
<td >CosRangerServer</td>
<td >/usr/local/service/cosranger/log/info.log</td>
<td >COSRanger runtime log</td>			
</tr><tr>
<td rowspan=3>Impala</td>
<td >Catalogd</td>
<td >/data/emr/impala/logs/catalogd.INFO</td>
<td >Cataloged runtime log</td>		
</tr><tr>
<td >Statestored</td>
<td >/data/emr/impala/logs/statestored.INFO</td>
<td >Statestored runtime log</td>
</tr><tr>
<td >Impalad</td>
<td >/data/emr/impala/logs/impalad.INFO</td>
<td >Impalad runtime log</td>
</tr><tr>
<td >Spark</td>
<td >HistoryServer</td>
<td >/data/emr/spark/logs/spark-hadoop.log</td>
<td >HistoryServer runtime log</td>
</tr><tr>
<td >Kylin</td>
<td >Kylin</td>
<td >/data/emr/kylin/logs/kylin.log</td>
<td >Kylin runtime log</td>
</tr><tr>
<td >Zeppelin</td>
<td >ZeppelinServer</td>
<td >/data/emr/zepplin/logs/zeppelin-hadoop.log</td>
<td >ZeppelinServer runtime log</td>
</tr><tr>
<td >Knox</td>
<td >Gateway</td>
<td >/data/emr/knox/logs/gateway.log</td>
<td >Gateway runtime log</td>
</tr><tr>
<td rowspan=3>Doris</td>
<td >BrokerBootstrap</td>
<td >	/data/emr/doris/broker/log/apache_hdfs_broker.log</td>
<td >BrokerBootstrap runtime log</td>
</tr><tr>
<td >PaloFe</td>
<td >	/data/emr/doris/fe/log/fe.log</td>
<td >PaloFe runtime log</td>
</tr><tr>
<td >PaloBe</td>
<td >/data/emr/doris/be/log/be.INFO</td>
<td >PaloBe runtime log</td>
</tr><tr>
<td >Kafka</td>
<td >Kafka</td>
<td >/user/local/service/kafka/logs/server.log</td>
<td >Kafka runtime log</td>
</tr>
</table>

## Minimum Log Level Supported by Services

| Service | Default Minimum Log Level | 
|---------|---------|
| Impala and Kudu | 	INFO| 
| Other services 	| WARN| 

## Query Rules for the Minimum Log Level
<table>
<thread>
<tr>
<th width=50%>Minimum Log Level</th>
<th width=50%>Queryable Log Levels</th>
</tr>
</thread>
<tr>
<td >INFO</td>
<td >INFO, WARN, ERROR, FATAL</td>
</tr><tr>
<td >WARN</td>
<td >WARN, ERROR, FATAL</td>
</tr><tr>
<td >ERROR</td>
<td >	ERROR, FATAL</td>
</tr><tr>
<td >FATAL</td>
<td >	FATAL</td>
</tr>
</table>
