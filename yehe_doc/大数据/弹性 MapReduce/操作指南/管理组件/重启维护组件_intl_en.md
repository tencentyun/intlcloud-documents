## Operation Scenarios

The component management feature enables restart at the component level and component adding. With advanced management, you can perform operations at the component service and node levels such as restart, pause, and maintenance.

**Definitions**
- **Restart:** the selected components and services will be restarted on a rolling basis by node.
- **Add Component:** you can use this feature to add components that were not selected when you created the cluster in the current version.
- **Pause:** the services in the selected node will be paused, which can then be resumed by using the **Start** feature.
- **Maintenance:** the process daemon will be stopped for the services on the selected node. When a process becomes exceptional for various reasons, no alarming or automatic recovery will occur. This is suitable for node debugging. You can use the **Exit Maintenance** feature to resume the daemon.

## Directions

Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and enter the **Component Management** page, where you can perform operations such as **Add Component**, **Restart Component**, and **Reset Native UI Password**. Select **Operation** > **Configure** for a component to enter its service/node-level management page.
 ![](https://main.qcloudimg.com/raw/e84b809ad2a4382b3edfd86b7dc57d4e.png)
 
### Adding component

Existing components in the cluster are selected by default and cannot be canceled. You can only add components that are currently not installed in the cluster.

![](https://main.qcloudimg.com/raw/992b4277cf5c859f8e9dbd8bdb1230b7.png)

### Restarting component
You can restart components in the console, and rolling restart is checked by default. Note: if rolling restart is disabled, all nodes will be restarted at the same time, and the services may become unavailable. Please do so with caution.
There are two policies for failure-handling when node restart fails: waiting for processing in case of failure or continuing processing in case of single node failure.

The restart methods supported by the service components are as follows:
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
			<td><li>For an HA cluster, run `saveNameSpace` on the standby NameNode.
Then, restart the component by running `hadoop-daemon.sh stop | start namenode`<li>For a non-HA cluster, the quick restart mode is used
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

![](https://main.qcloudimg.com/raw/06b14f43d86610fd8ffaf1c7d492181d.png)

### Role management
The **Service Status** column displays whether the current service is **running** or **paused**, and the **Maintenance Status** column displays whether the current service is under maintenance.
![](https://main.qcloudimg.com/raw/568c0002cafb3baf1077db9e8b11670c.png)
