## Feature Overview
After a component configuration item is modified, the corresponding service needs to be restarted for the configuration to take effect. To minimize or eliminate the impact of service restart on the business continuity, the service can be restarted on a rolling basis. For instances in master/slave architecture, the slave instance will be restarted first before the master instance. Rolling restart takes more time than normal restart.

- You can restart services in the console, and rolling restart is checked by default. Note: if rolling restart is disabled, all nodes will be restarted at the same time, and the services may become unavailable. Please do so with caution.
- There are two policies for failure-handling when node restart fails: waiting for processing in case of failure or continuing processing in case of single node failure.

## Directions
1. Log in to the [EMR Console](https://console.cloud.tencent.com/emr), select **Cluster List**, and click the ID/Name of the target cluster to enter the cluster details page.
2. In **Cluster Service**, click **Restart Service**, or select the block of the component to be restarted, check the service **role** to be restarted in **Operation** > **Role Management**, and click **Restart Service**.
 - When restarting the service directly on the cluster details page, you need to select the service name, service role, restart method, whether to enable rolling restart, and failure-handling policy.
![](https://main.qcloudimg.com/raw/b3117cc5580453d007ed0e888bb18fc2.png)
 - When restarting the service in the component block, you only need to select the restart method and failure-handling policy.
![](https://main.qcloudimg.com/raw/821cdec6cb6ee7649c9d33bfb1528b35.png)
4. The restart methods supported by the service components are as follows:
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
			<td>It can be restarted by running `hadoop-daemon.sh stop | start namenode`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>NameNode</td>
      <td>Safe restart mode</td>
			<td>For an HA cluster, run `saveNameSpace` on the standby NameNode.
Then, restart the component by running `hadoop-daemon.sh stop | start namenode` . For a non-HA cluster, the quick restart mode is used
</td>
			<td>Only rolling restart is supported</td>
   </tr>
   <tr>
      <td>DataNode</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hadoop-daemon.sh stop | start datanode`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>JournalNode</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hadoop-daemon.sh stop | start journalnode`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>zkfc</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hadoop-daemon.sh stop | start zkfc`</td>
			<td>-</td>
   </tr>
   <tr>
      <td rowspan="4">YARN</td>
      <td>ResourceManager</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `sbin/yarn-daemon.sh stop | start resourcemanager`</td>
			<td>Only rolling restart is supported</td>
   </tr>
   <tr>
      <td>NodeManager</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `sbin/yarn-daemon.sh stop | start nodemanager`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>JobHisotryServer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `sbin/yarn-daemon.sh stop| start historyserver`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>TimeLineServer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `sbin/yarn-daemon.sh stop | start timelineserver`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="4">HBASE</td>
      <td>HbaseThrift</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hbase-daemon.sh stop | start thrift`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>HMaster</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hbase-daemon.sh stop | start master`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>HRegionServer</td>
      <td>Quick restart mode</td>
			<td>It can be restarted by running `hbase-daemon.sh stop | start regionserver`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>HRegionServer</td>
      <td>Safe restart mode</td>
			<td>It can be restarted by running `graceful_stop.sh --restart --reload`</td>
			<td>-</td>
   </tr>
	  <tr>
      <td rowspan="3">HIVE</td>
      <td>HiveMetaStore</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hcat_server.sh stop | strat`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>HiveServer2</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `hive-daemon.sh stop-h2 | start-h2`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>HiveWebHcat</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `webhcat_server.sh stop | start`</td>
			<td>-</td>
   </tr>
	  <tr>
      <td rowspan="2">PRESTO</td>
      <td>PrestoCoordinator</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/launcher stop | start`</td>
			<td>Only rolling restart is supported</td>
   </tr>
   <tr>
      <td>PrestoWorker</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/launcher stop | start`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>ZooKeeper</td>
      <td>QuorumPeerMain</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/zkServer.sh stop | start`</td>
			<td>-</td>
   </tr>
	  <tr>
      <td>Spark</td>
      <td>SparkJobHistoryServer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `sbin/stop-history-server.sh | sbin/start-history-server.sh`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>Hue</td>
      <td>Hue</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `build/env/bin/start.sh` and `build/env/bin/sop.sh`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>Oozie</td>
      <td>Oozie</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `oozied.sh stop | start`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="4">Storm</td>
      <td>Nimbus</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/storm-daemon.sh nimbus stop | start`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>Supervisor</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/storm-daemon.sh supervisor stop | start`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>LogViewer</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/storm-daemon.sh nimbus stop | start`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>UI</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/storm-daemon.sh nimbus stop | start`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td>Ranger</td>
      <td>Ranger</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `sbin/ranger-daemon.sh stop | start`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="2">Alluxio</td>
      <td>AlluxioMaster</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/alluxio-stop.sh master` and `bin/alluxio-start.sh master`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>AlluxioWorker</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `bin/alluxio-stop.sh worker` and `bin/alluxio-start.sh worker`</td>
			<td>-</td>
   </tr>
	 <tr>
      <td rowspan="3">Ganglia</td>
      <td>Httpd</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `/sbin/service http stop | start`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>gmetad</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `/sbin/service gmetad stop | start`</td>
			<td>-</td>
   </tr>
   <tr>
      <td>gmond</td>
      <td>Default restart mode</td>
			<td>It can be restarted by running `/sbin/service gmon stop | start`</td>
			<td>-</td>
   </tr>
</table>
