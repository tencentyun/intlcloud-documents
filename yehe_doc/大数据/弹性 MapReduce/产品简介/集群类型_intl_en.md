EMR supports six cluster types and their respective use cases and defines five node types. Different cluster types and their respective use cases support different node types, numbers of deployed nodes, and deployed services. You can select the most appropriate cluster type and use case based on your business needs when creating a cluster.

## Cluster Type Description
### Hadoop cluster
<table>
<thead>
<tr>
<th width=10%>Use Case</th>
<th width=20%>Description</th>
<th width=60%>Node Deployment Description</th>
</tr>
</thead>
<tbody><tr>
<td >Default use case</td>
<td >Based on open-source Hadoop and the components that form a Hadoop ecosystem, it provides big data solutions for massive data storage, offline/real-time data analysis, streaming data compute, and machine learning.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a management node that ensures the scheduling of the cluster works properly. Processes such as NameNode, ResourceManager, and HMaster are deployed here. The number of master nodes is 1 in non-HA mode or 2 in HA mode.
<br><b>Note: If Kudu is included in the deployed components, the cluster supports only the HA mode, and the number of master nodes is 3.</b>
<li/><b>Core node:</b>It is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scaled out, they cannot be scaled in. Processes such as DataNode, NodeManager, and RegionServer are deployed here. The number of core nodes is ≥2 in non-HA mode or ≥3 in HA mode.
<li/><b>Task node:</b>It is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time. Processes such as NodeManager and PrestoWork are deployed here. The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0. 
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster. Distributed coordinator components such as ZooKeeper and JournalNode are deployed here. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.
<li/><b>Router node:</b>It is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time. Hadoop packages, including software programs and processes such as Hive, Hue, and Spark, are deployed here. The number of router nodes can be changed at any time. The minimum value is 0.</ul></td>
</tr><tr>
<td >ZooKeeper</td>
<td >It is suitable for creating a distributed, high-availability coordination service for large clusters.</td>
<td><ul style="margin:0"><li/><b>Common node:</b>Distributed coordinator components such as ZooKeeper are deployed here. The number of deployed nodes must be odd and at least three common nodes. Common nodes support only the HA mode.</ul></td>
</tr><tr>
<td >HBase</td>
<td >It is suitable for storing massive amounts of unstructured or semi-structured data. It provides a high-reliability, high-performance, column-oriented, scalable distributed storage system that supports real-time data read/write.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a management node that ensures the scheduling of the cluster works properly. Processes such as NameNode, ResourceManager, and HMaster are deployed here. The number of master nodes is 1 in non-HA mode or 2 in HA mode.
<li/><b>Core node:</b>It is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scaled out, they cannot be scaled in. Processes such as DataNode, NodeManager, and RegionServer are deployed here. The number of core nodes is ≥2 in non-HA mode or ≥3 in HA mode.
<li/><b>Task node:</b>It is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time. Processes such as NodeManager are deployed here. The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0.
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster. Distributed coordinator components such as ZooKeeper and JournalNode are deployed here. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.
<li/><b>Router node:</b>It is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time. The number of router nodes can be changed at any time. The minimum value is 0.
</ul></td>
</tr><tr>
<td >Presto</td>
<td >It provides an open-source distributed SQL query engine for quick query and analysis of massive amounts of data. It is suitable for interactive analytical queries.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a management node that ensures the scheduling of the cluster works properly. Processes such as NameNode and ResourceManager are deployed here. The number of master nodes is 1 in non-HA mode or 2 in HA mode.
<li/><b>Core node:</b>It is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scaled out, they cannot be scaled in. Processes such as DataNode and NodeManager are deployed here. The number of core nodes is ≥2 in non-HA mode or ≥3 in HA mode.
<li/><b>Task node:</b>It is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time. Processes such as NodeManager and PrestoWork are deployed here. The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0.
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster. Distributed coordinator components such as ZooKeeper and JournalNode are deployed here. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.
<li/><b>Router node:</b>It is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time. The number of router nodes can be changed at any time. The minimum value is 0.
</ul></td>
</tr><tr>
<td >Kudu</td>
<td >It provides a distributed and scalable columnar storage manager and supports random reads/writes and OLAP analysis to process frequently updated data.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a management node that ensures the scheduling of the cluster works properly. Processes such as NameNode and ResourceManager are deployed here. The number of master nodes is 1 in non-HA mode or 2 in HA mode.
<li/><b>Core node:</b>It is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scaled out, they cannot be scaled in. The number of core nodes is ≥2 in non-HA mode or ≥3 in HA mode.
<li/><b>Task node:</b>It is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time. The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0.
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster. Distributed coordinator components such as ZooKeeper and JournalNode are deployed here. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.
<li/><b>Router node:</b>It is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time. The number of router nodes can be changed at any time. The minimum value is 0.
</ul></td>
</tr>
</tbody>
</table>

### Druid cluster
<table>
<thead>
<tr>
<th width=10%>Use Case</th>
<th width=20%>Description</th>
<th width=60%>Node Deployment Description</th>
</tr>
</thead>
<tbody><tr>
<td >Default use case</td>
<td >It supports high-performance real-time analysis, big data queries in milliseconds, and multiple data ingestion methods. It is suitable for real-time big data query scenarios.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a management node that ensures the scheduling of the cluster works properly. Processes such as NameNode and ResourceManager are deployed here. The number of master nodes is 1 in non-HA mode or 2 in HA mode.
<li/><b>Core node:</b>It is a compute and storage node. All your data in HDFS is stored in core nodes. Therefore, in order to ensure data security, once core nodes are scaled out, they cannot be scaled in. Processes such as DataNode and NodeManager are deployed here. The number of core nodes is ≥2 in non-HA mode or ≥3 in HA mode.
<li/><b>Task node:</b>It is a pure compute node and does not store any data. The computed data comes from a core node or COS. Therefore, it is often used as an elastic node and can be scaled in or out at any time. Processes such as NodeManager are deployed here. The number of task nodes can be changed at any time to scale the cluster. The minimum value is 0.
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster. Distributed coordinator components such as ZooKeeper and JournalNode are deployed here. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.
<li/><b>Router node:</b>It is used to share the load of a master node or as the task submitter of the cluster. It can be scaled in or out at any time. The number of router nodes can be changed at any time. The minimum value is 0.
</ul></td>
</tr>
</tbody>
</table>

### ClickHouse cluster
<table>
<thead>
<tr>
<th width=10%>Use Case</th>
<th width=20%>Description</th>
<th width=60%>Node Deployment Description</th>
</tr>
</thead>
<tbody><tr>
<td >Default use case</td>
<td >It provides a column-oriented database management system. It is suitable for data warehouse analysis scenarios such as real-time wide table analysis, real-time BI report analysis, and user behavior analysis.</td>
<td><ul style="margin:0"><li/><b>Core node:</b>It is a compute and storage node. ClickHouseServer is deployed here.
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the master nodes in an HA cluster. Distributed coordinator components such as ZooKeeper are deployed here. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.
</ul></td>
</tr>
</tbody>
</table>

### Doris cluster
<table>
<thead>
<tr>
<th width=10%>Use Case</th>
<th width=20%>Description</th>
<th width=60%>Node Deployment Description</th>
</tr>
</thead>
<tbody><tr>
<td >Default use case</td>
<td >It provides an MPP analytical database product that supports sub-second queries on PB-scale, structured data. It is compatible with MySQL protocol and uses the standard SQL syntax. It is suitable for historical report analysis, real-time data analysis, interactive data analysis, etc.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a frontend module and provides the Web UI feature. Processes such as FE Follower and Broker are deployed here. The number of master nodes is ≥1 in non-HA mode or ≥3 in HA mode.
<li/><b>Core node:</b>It is a backend module and provides the data storage feature. Processes such as BE and Broker are deployed here. The number of core nodes is ≥3.
<li/><b>Router node:</b>It is a frontend module and helps achieve high read/write availability. Processes such as FE Observer and Broker are deployed here. Router nodes can be scaled out but not scaled in.
</ul></td>
</tr>
</tbody>
</table>

### Kafka cluster
<table>
<thead>
<tr>
<th width=10%>Use Case</th>
<th width=20%>Description</th>
<th width=60%>Node Deployment Description</th>
</tr>
</thead>
<tbody><tr>
<td >Default use case</td>
<td >It provides a distributed, partitioned, multi-replica, and multi-subscriber message processing system based on ZooKeeper coordination. It is suitable for asynchronous processing, message communication, and streaming data receiving and distribution.</td>
<td><ul style="margin:0"><li/><b>Core node:</b>It provides a distributed, partitioned, multi-replica, and multi-subscriber message processing system based on ZooKeeper coordination. It is suitable for asynchronous processing, message communication, and streaming data receiving and distribution.
<li/><b>Common node:</b>It provides data sharing and syncing and HA fault tolerance services for the core nodes in an HA cluster. The number of common nodes is 0 in non-HA mode or ≥3 in HA mode.</ul></td>
</tr>
</tbody>
</table>

### StarRocks cluster
<table>
<thead>
<tr>
<th width=10%>Use Case</th>
<th width=20%>Description</th>
<th width=60%>Node Deployment Description</th>
</tr>
</thead>
<tbody><tr>
<td >Default use case</td>
<td >StarRocks adopts full vectorization technology. It supports extremely fast and unified OLAP databases. It is suitable for many data analysis scenarios, such as multidimensional, real-time, and high-concurrency analysis.</td>
<td><ul style="margin:0"><li/><b>Master node:</b>It is a frontend module and provides the Web UI feature. Processes such as FE Follower and Broker are deployed here. The number of master nodes is ≥1 in non-HA mode or ≥3 in HA mode.
<li/><b>Core node:</b>It is a backend module and provides the data storage feature. Processes such as BE and Broker are deployed here. The number of core nodes is ≥3.
<li/><b>Router node:</b>It is a frontend module and helps achieve high read/write availability. Processes such as FE Observer and Broker are deployed here. Router nodes can be scaled out but not scaled in.
</ul></td>
</tr>
</tbody>
</table>
