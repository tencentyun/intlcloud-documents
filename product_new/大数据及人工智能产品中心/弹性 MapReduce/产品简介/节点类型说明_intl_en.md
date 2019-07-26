EMR offers five types of nodes:
<table>
   <tr>
      <th style="width: 80px;">Node Type</th>
      <th style="width: 100px;">Description</th>
      <th style="width: 80px;">HA Quantity</th>
      <th style="width: 110px;">Non-HA Quantity</th>
   </tr>
   <tr>
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
      <td>Processes such as NodeManger and PrestoWork are deployed here.</td>
      <td colspan="2">The number of task nodes can be changed at any time to achieve elastic scalability of the cluster. The minimum value is 0.</td>
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
      <td colspan="2">The number of router nodes can be changed at any time. The minimum value is 0.</td>
</table>

- A master node is a management node that ensures that the scheduling of the cluster works properly.
- A core node is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scale out, they cannot be scaled in.
- A task node is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time.
- A router is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time.
