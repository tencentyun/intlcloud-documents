### How do I fix failed operations on the EMR master node due to low configuration?
#### Symptoms
As the master node's configuration is too low, Hive or Spark jobs submitted to it report errors or are directly killed.

#### Cause analysis
The memory of the master node is insufficient, causing other applications to be killed due to OOM.

#### Solution
1. Too many businesses are deployed on the EMR master node, which usually becomes the bottleneck of the entire cluster. However, the master node cannot be scaled out; instead, it can only be upgraded as described below:
 - First, find the node where the standby NameNode resides in the cluster.
    - Run the following command on the standby NameNode to enter the safe mode.
```
hdfs dfsadmin -fs 10.0.0.9(standby node IP):4007 -safemode enter   Enter the safe mode
```
     - Run the following command on the standby NameNode to save the metadata.
```
hdfs dfsadmin -fs 10.0.0.9(standby node IP):4007 -saveNamespace   Save the metadata
```
    - Run the following command on the standby NameNode to exit the safe mode.
```
hdfs dfsadmin -fs 10.0.0.9(standby node IP):4007 -safemode leave   Exit the safe mode
```
 - Then, in the EMR Console (or the CVM Console for a legacy cluster), upgrade the active node.
 - Upgrade the standby node and make the configuration of the master's active node the same as that of the standby node.
>If your cluster is not a high-availability one, then it will become unavailable for a while during the upgrade.
2. In Spark, jobs are committed in client mode by default, and the driver runs on the master node. You can change the mode to master mode and then commit jobs.
3. For the Hive component, enable the router node, migrate HiveServer2 to it, and then disable the Hive component on the master node. For detailed directions, please see [Migrating HiveServer2 to Router](https://intl.cloud.tencent.com/document/product/1026/35066).
4. Disable components that are not commonly used on the master node or migrate Hue to the router node.
Directions for migrating Hue to the router node:
 - Enter the EMR Console, Add a router node on the Cloud Hardware Management page, and select the Hue component.
 - After the scale-out, disable the original Hue component on the master node, retain that on the router node, bind a public EIP to the router node, and open the source policy and ports in the security group.

#### Preset values of memory size for master node components in EMR cluster and recommendations
1. List of heap memories of common components
<table>
   <tr>
      <th style="width: 80px;">Component</th>
      <th style="width: 100px;">Process</th>
      <th style="width: 80px;">Configuration File</th>
      <th style="width: 110px;">Configuration Item</th>
			<th style="width: 110px;">Default Heap Memory (in MB)</th>
   </tr>
   <tr>
      <td>HDFS</td>
      <td>Namenode</td>
      <td>hadoop-env.sh</td>
      <td>NNHeapsize</td>
      <td>4,096</td>
   </tr>
   <tr>
      <td>YARN</td>
      <td>Resourcemanager</td>
      <td>yarn-env.sh</td>
      <td>Heapsize</td>
      <td>2,000</td>
   </tr>
   <tr>
      <td>Hive</td>
      <td>Hiveserver2</td>
      <td>hive-env.sh</td>
			<td>HS2Heapsize</td>
      <td>4,096</td>
   </tr>
   <tr>
      <td>HBase</td>
      <td>Hmaster</td>
      <td>hbase-env.sh</td>
      <td>Heapsize</td>
      <td>1,024</td>
   </tr>
   <tr>
      <td>Presto</td>
      <td>Coordinator</td>
      <td>jvm.config</td>
      <td>Maximum JVM</td>
      <td>3,072</td>
	 </tr>
	  <tr>
      <td>Spark</td>
      <td>spark-driver</td>
      <td>spark-defaults.conf</td>
      <td>spark.driver.memory</td>
      <td>1,024</td>
	 </tr>
	 <tr>
      <td>Oozie</td>
      <td>Oozie</td>
      <td>-</td>
      <td>-</td>
      <td>1,024</td>
	 </tr>
	  <tr>
      <td>Storm</td>
      <td>Nimbus</td>
      <td>-</td>
      <td>-</td>
      <td>1,024</td>
	 </tr>
</table>
2. Suggested preset values for components
<table>
   <tr>
      <th style="width: 80px;">Component</th>
      <th style="width: 100px;">Suggested Heap Memory Size</th>
   </tr>
   <tr>
      <td>HDFS (NameNode)</td>
      <td>Minimum heap memory = 250 x number of files + 290 x number of directories + 368 x number of blocks</td>
   </tr>
   <tr>
      <td>YARN (ResourceManager) </td>
      <td>It can be increased as needed</td>
   </tr>
   <tr>
      <td>Hive (HiveServer2)</td>
      <td>It can be increased as needed</td>
   </tr>
   <tr>
      <td>HBase (HMaster)</td>
      <td>The master node only receives DDL requests and performs load balancing. The default size of 1 GB is generally sufficient</td>
   </tr>
   <tr>
      <td>Presto (Coordinator)</td>
      <td>Use the default value</td>
	 </tr>
	  <tr>
      <td>Spark (spark-driver)</td>
      <td>It can be increased as needed</td>
	 </tr>
	 <tr>
      <td>Oozie (oozie)</td>
      <td>Use the default value</td>
	 </tr>
	  <tr>
      <td>Storm (Nimbus)</td>
      <td>Use the default value</td>
	 </tr>
</table>
3. Suggested idle memory size for servers: 10–20% of the total memory size.
4. You can deploy EMR components in independent mode or hybrid mode as needed.
 - Independent deployment: it is suitable for HDFS clusters for storage, HBase clusters for analysis of massive amounts of data, and Spark clusters for job computation.
 - Hybrid deployment: multiple components can be deployed in a cluster in this mode, which is suitable for testing clusters or scenarios where the business volume is not high or resource preemption is negligible.
