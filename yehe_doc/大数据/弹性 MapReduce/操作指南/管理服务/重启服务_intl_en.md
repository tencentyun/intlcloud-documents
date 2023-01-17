## Overview
After modifying the configuration of a component, you need to restart the service for the configuration to take effect. To minimize or avoid the impact of the service restart on your business, restart the service on a rolling basis. For instances with active and standby attributes, standby instances will be restarted first before active instances. Rolling restart takes longer than regular restart.
- Services can be restarted in the console, and rolling restart is selected by default. Note that when rolling restart is disabled, restarting all nodes at the same time may make the service unavailable.
- There are two policies for failure handling when node restart fails: waiting for processing in case of failure or continuing processing in case of single node failure.

## Directions

1. 	Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click the **ID/Name** of the target cluster in the cluster list to enter the cluster details page.
2. 	To restart the entire component, select **Operation** > **Restart Service** on the target component block of the **Cluster Service** page, or go to the component details page and select **More** > **Restart All Services** in the top-right corner. To restart a role instance, select **Operation** > **Role Management** on the target component block of the **Cluster Service** page, select the target service role, and click **Restart Service**.
 - When restarting a service on the component block or component details page, you need to select the target service role, restart method, rolling restart switch status, and failure handling policy.
If you set **Service Role** to **All**, the entire component will be restarted.
![](https://qcloudimg.tencent-cloud.cn/raw/410ac102072f0f7345152ba3fb6fb2b8.png)
 - When restarting the service on the **Role Management** page, you only need to select the restart method and failure handling policy.
![](https://qcloudimg.tencent-cloud.cn/raw/410ac102072f0f7345152ba3fb6fb2b8.png)
4. The restart methods supported by service components are as follows:
<table>
   <tr>
      <th width=10%>Component</th>
      <th width=10%>Service</th>
      <th width=15%>Restart Mode</th>
			<th width=55%>Description</th>
			<th width=15%>Remarks</th>
   </tr>
   <tr>
      <td rowspan="5">HDFS</td>
      <td>NameNode</td>
      <td>Quick restart mode</td>
			<td>It can be restarted by running <code>hadoop-daemon.sh stop | start namenode</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>NameNode</td>
      <td>Safe restart mode</td>
			<td>For an HA cluster, run `saveNameSpace` on the standby NameNode.
Then, restart the component by running <code>hadoop-daemon.sh stop | start namenode</code>. For a non-HA cluster, the quick restart mode is used.
</td>
			<td>Only rolling restart is supported.</td>
   </tr>
   <tr>
      <td>DataNode</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hadoop-daemon.sh stop | start datanode</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>JournalNode</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hadoop-daemon.sh stop | start journalnode</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>zkfc</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hadoop-daemon.sh stop | start zkfc</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td rowspan="4">YARN</td>
      <td>ResourceManager</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>sbin/yarn-daemon.sh stop | start resourcemanager</code>.</td>
			<td>Only rolling restart is supported.</td>
   </tr>
   <tr>
      <td>NodeManager</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>sbin/yarn-daemon.sh stop | start nodemanager</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>JobHisotryServer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>sbin/yarn-daemon.sh stop| start historyserver</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>TimeLineServer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>sbin/yarn-daemon.sh stop | start timelineserver</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="4">HBase</td>
      <td>HbaseThrift</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hbase-daemon.sh stop | start thrift</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>HMaster</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hbase-daemon.sh stop | start master</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>HRegionServer</td>
      <td>Quick restart mode</td>
			<td>It can be restarted by running <code>hbase-daemon.sh stop | start regionserver</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>HRegionServer</td>
      <td>Safe restart mode</td>
			<td>It can be restarted by running <code>graceful_stop.sh --restart --reload</code>.</td>
			<td>-</td>
   </tr>
	  <tr>
      <td rowspan="3">Hive</td>
      <td>HiveMetaStore</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hcat_server.sh stop | strat</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>HiveServer2</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>hive-daemon.sh stop-h2 | start-h2</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>HiveWebHcat</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>webhcat_server.sh stop | start</code>.</td>
			<td>-</td>
   </tr>
	  <tr>
      <td rowspan="2">Presto</td>
      <td>PrestoCoordinator</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/launcher stop | start</code>.</td>
			<td>Only rolling restart is supported.</td>
   </tr>
   <tr>
      <td>PrestoWorker</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/launcher stop | start</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>ZooKeeper</td>
      <td>QuorumPeerMain</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/zkServer.sh stop | start</code>.</td>
			<td>-</td>
   </tr>
	  <tr>
      <td>Spark</td>
      <td>SparkJobHistoryServer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>sbin/stop-history-server.sh | sbin/start-history-server.sh</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>Hue</td>
      <td>Hue</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>build/env/bin/start.sh</code> and <code>build/env/bin/stop.sh</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>Oozie</td>
      <td>Oozie</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>oozied.sh stop | start</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="4">Storm</td>
      <td>Nimbus</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/storm-daemon.sh nimbus stop | start</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>Supervisor</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/storm-daemon.sh supervisor stop | start</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>LogViewer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/storm-daemon.sh nimbus stop | start</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>UI</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/storm-daemon.sh nimbus stop | start</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>Ranger</td>
      <td>Ranger</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>sbin/ranger-daemon.sh stop | start</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="2">Alluxio</td>
      <td>AlluxioMaster</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/alluxio-stop.sh master</code> and <code>bin/alluxio-start.sh master</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>AlluxioWorker</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>bin/alluxio-stop.sh worker</code> and <code>bin/alluxio-start.sh worker</code>.</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="3">Ganglia</td>
      <td>Httpd</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>/sbin/service http stop | start</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>Gmetad</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>/sbin/service gmetad stop | start</code>.</td>
			<td>-</td>
   </tr>
   <tr>
      <td>Gmond</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running <code>/sbin/service gmon stop | start</code>.</td>
			<td>-</td>
   </tr>
</table>
