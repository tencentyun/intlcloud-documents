EMR offers five types of nodes for your choice based on the cluster type.

## Hadoop Cluster
<table>
<thead>
<tr>
<th>Node Type</th>
<th>Description</th>
<th>HA Node Quantity</th>
<th>Non-HA Node Quantity</th>
</tr>
</thead>
<tbody><tr>
<td>Master</td>
<td>Processes such as NameNode, ResourceManager, and HMaster are deployed here.</td>
<td>2</td>
<td>1</td>
</tr>
<tr>
<td>Core</td>
<td>Processes such as DataNode, NodeManager, and RegionServer are deployed here.</td>
<td>≥ 3</td>
<td>≥ 2</td>
</tr>
<tr>
<td>Task</td>
<td>Processes such as NodeManager and PrestoWork are deployed here.</td>
<td colspan=2>The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0.</td>
</tr>
<tr>
<td>Common</td>
<td>Distributed coordinator components such as ZooKeeper and JournalNode are deployed here.</td>
<td>≥ 3</td>
<td>0</td>
</tr>
<tr>
<td>Router</td>
<td>Hadoop packages, including software programs and processes such as Hive, Hue, and Spark, are deployed here.</td>
<td colspan=2>The number of router nodes can be changed at any time. The minimum value is 0.</td>
</tr>
</tbody></table>


- A master node is a management node that ensures that the scheduling of the cluster works properly.
- A core node is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scale out, they cannot be scaled in.
- A task node is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time.
- A common node provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster.
- A router is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time.

## ClickHouse Cluster
<table>
   <tr>
      <th style="width: 80px;">Node Type</th>
      <th style="width: 100px;">Description</th>
      <th style="width: 80px;">HA Node Quantity</th>
      <th style="width: 110px;">Non-HA Node Quantity</th>
   </tr>
   <tr>
      <td>Core</td>
      <td>The ClickHouseServer process is deployed here.</td>
      <td>≥ 2</td>
      <td>≥ 1</td>
   </tr>
   <tr>
      <td>Common</td>
      <td>Distributed coordinator components such as ZooKeeper are deployed here.</td>
      <td>≥ 3</td>
      <td>0</td>
   </tr>
</table>

- A core node is a compute and storage node.
- A common node provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster.

## Druid Cluster
<table>
<thead>
<tr>
<th>Node Type</th>
<th>Description</th>
<th>HA Node Quantity</th>
<th>Non-HA Node Quantity</th>
</tr>
</thead>
<tbody><tr>
<td>Master</td>
<td>Processes such as NameNode, ResourceManager, Overlord, coordinator, ZKFailoverController, and JobHistoryServer are deployed here.</td>
<td>2</td>
<td>1</td>
</tr>
<tr>
<td>Core</td>
<td>Processes such as DataNode, NodeManager, middlemanager, and historical are deployed here.</td>
<td>≥ 3</td>
<td>≥ 2</td>
</tr>
<tr>
<td>Task</td>
<td>Processes such as NodeManager and middlemanager are deployed here.</td>
<td colspan=2>The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0.</td>
</tr>
<tr>
<td>Common</td>
<td>Distributed coordinator components such as ZooKeeper and JournalNode are deployed here.</td>
<td>≥ 3</td>
<td>0</td>
</tr>
<tr>
<td>Router</td>
<td>Hadoop packages, including software programs and processes such as broker, are deployed here.</td>
<td colspan=2>The number of router nodes can be changed at any time. The minimum value is 0.</td>
</tr>
</tbody></table>

- A master node is a management node that ensures that the scheduling of the cluster works properly.
- A core node is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scale out, they cannot be scaled in.
- A task node is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time.
- A common node provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster.
- A router is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time.


## Kafka Cluster
<table>
   <tr>
      <th style="width: 80px;">Node Type</th>
      <th style="width: 100px;">Description</th>
      <th style="width: 80px;">HA Node Quantity</th>
      <th style="width: 110px;">Non-HA Node Quantity</th>
   </tr>
   <tr>
      <td>Core</td>
      <td>Processes such as Kafka and KafkaManager are deployed here.</td>
      <td>≥ 2</td>
      <td>≥ 1</td>
   </tr>
   <tr>
      <td>Common</td>
      <td>Distributed coordinator components such as ZooKeeper are deployed here.</td>
      <td>≥ 3</td>
      <td>0</td>
   </tr>
</table>

- A core node is a compute and storage node.
- A common node provides data sharing and syncing and HA fault tolerance services for the core nodes in an HA cluster.


## Doris Cluster
<table>
   <tr>
      <th style="width: 80px;">Node Type</th>
      <th style="width: 100px;">Description</th>
      <th style="width: 80px;">HA Node Quantity</th>
      <th style="width: 110px;">Non-HA Node Quantity</th>
   </tr>
	 <tr>
      <td>Master</td>
      <td>Processes such as FE Follower and Broker are deployed here.</td>
      <td>≥ 3</td>
      <td>≥ 1</td>
   </tr>
   <tr>
      <td>Core</td>
      <td>Processes such as BE and Broker are deployed here.</td>
      <td colspan=2>≥ 3</td>
   </tr>
   <tr>
      <td>Router</td>
      <td>Processes such as FE Observer and Broker are deployed here.</td>
      <td colspan=2>The number of router nodes can be changed at any time. The minimum value is 0.</td>
   </tr>
</table>

- A master node is a frontend module and provides the Web UI feature.
- A core node is a backend module and provides the data storage feature.
- A router node is a frontend module and helps achieve high read/write availability.





