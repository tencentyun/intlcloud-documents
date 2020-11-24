## Selecting Cluster Type
There are three types of EMR clusters, and you can choose one as needed:
- **Hadoop cluster:** it provides open-source big data components such as Hadoop, HBase, Hive, Spark, Flink, and Presto and is mainly used in big data processing scenarios such as offline, real-time, and ad hoc data analysis.
- **ClickHouse cluster:** it provides the open-source column-oriented database component ClickHouse and is mainly used in analysis of events or log streams that have a clear and fixed structure.
- **Druid cluster:** it provides the distributed time-series database component Druid and is mainly used in queries of massive amounts of aggregated data based on time series.

## Selecting Billing Mode
Billing mode provided by EMR cluster:
- **Pay-as-you-go cluster**: the billing mode of all nodes in a cluster is pay-as-you-go. It is suitable for clusters that exist for only a short period of time or periodically.

For more information on node types, please see [Node Type Description](https://intl.cloud.tencent.com/document/product/1026/31094).

## Selecting Model Specification
EMR offers a wide variety of CVM instance models, including EMR Standard, EMR Compute, EMR High IO, EMR MEM-Optimized, and EMR Big Data (if you need CPM models, please contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category)).
>!
>- The minimum number of nodes in a high-availability (HA) Hadoop or Druid cluster is 8, including 2 master nodes, 3 common nodes, and at least 3 core nodes. A non-HA cluster adopts single-replica storage, which can be used for testing but is not recommended for use in production environments, and its minimum number of nodes is 3, including 1 master node and at least 2 core nodes.
>- The minimum number of nodes in a high-availability (HA) ClickHouse cluster is 5, including 2 core nodes and 3 common nodes. A non-HA cluster adopts single-replica storage, which can be used for testing but is not recommended for use in production environments, and it should contain at least 1 core node.

You can choose the most appropriate model based on your business needs and budget.
- If you require low latency for offline computation, you are recommended to choose the model with a local disk or the Big Data model.
- If you need to use the real-time database HBase, you are recommended to choose the EMR High IO model with a local SSD disk for optimal performance.

### Node specification recommendation
<table>
   <tr>
      <th width=13%>Node Type</th>
      <th width=17%>Cluster Type</th>
      <th width=70%>Recommended Specification</th>
   </tr>
   <tr>
      <td rowspan="3">Master node</td>
      <td>Hadoop cluster</td>
      <td>For master nodes, you are recommended to select instance specification with relatively large memory (at least 8 GB) and use cloud disks to achieve higher stability.</td>
   </tr>
   <tr>
      <td>ClickHouse cluster</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid cluster</td>
      <td>For master nodes, you are recommended to select instance specification with relatively large memory (at least 16 GB) and use SSDs as disks to achieve higher I/O performance.</td>
   </tr>
	    <tr>
      <td rowspan="3">Core node</td>
      <td>Hadoop cluster</td>
      <td><li>If most of your data is stored on COS, the core nodes will function in a way similar to task nodes and should have a capacity of at least 500 GB.<strong>Core nodes cannot be elastically scaled.</strong>
<li>If your architecture does not use COS, the core nodes are responsible for processing cluster computation and storage tasks, and three-replica backup is enabled by default on EMR. When estimating the data disk capacity, you need to consider the capacity for storing three replicas. Therefore, the Big Data model is recommended.
</td>
   </tr>
   <tr>
      <td>ClickHouse cluster</td>
      <td>For core nodes, you are recommended to select models with higher CPU and memory specifications. As data may lose if a local disk is corrupted, you are recommended to use cloud disks.</td>
   </tr>
   <tr>
      <td>Druid cluster</td>
      <td>For core nodes, you are recommended to select instance specification with relatively large memory (at least 16 GB) and use SSDs as disks to achieve higher I/O performance.</td>
   </tr>
	 <tr>
	 <td rowspan="3">Task node</td>
      <td>Hadoop cluster</td>
      <td><li>If your architecture does not use COS, task nodes are not required.
<li>If most of your data is stored on COS, task nodes can be used as elastic computation resources and deployed as needed.
</td>
   </tr>
   <tr>
      <td>ClickHouse cluster</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid cluster</td>
      <td><li>If your architecture does not use COS, task nodes are not required.
<li>If most of your data is stored on COS, task nodes can be used as elastic computation resources and deployed as needed.
</td>
   </tr>
	 <tr>
	 <td rowspan="3">Common node</td>
      <td>Hadoop cluster</td>
      <td>Common nodes are mainly used as ZooKeeper nodes. You are recommend to select the 2-core 4 GB MEM model with 100 GB cloud disk capacity so as to meet the requirement.</td>
   </tr>
   <tr>
      <td>ClickHouse cluster</td>
      <td>For common nodes, the CPU and memory configuration should be at least 4-core 16 GB MEM.</td>
   </tr>
   <tr>
      <td>Druid cluster</td>
      <td>Common nodes are mainly used as ZooKeeper nodes. You are recommend to select the 2-core 4 GB MEM model with 100 GB cloud disk capacity so as to meet the requirement.</td>
   </tr>
	 <tr>
	 <td rowspan="3">Router node</td>
      <td>Hadoop cluster</td>
      <td>A router node is mainly used to relieve the load of the master node and as a task submitter; therefore, you are recommended to select a model with larger memory, preferably not lower than the master node specification.</td>
   </tr>
   <tr>
      <td>ClickHouse cluster</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid cluster</td>
      <td>A router node is mainly used to relieve the load of the master node and as a task submitter; therefore, you are recommended to select a model with larger memory, preferably not lower than the master node specification.</td>
   </tr>
</table>

## Network and Security
To ensure the network security of the EMR cluster, it is placed in a VPC, and a security group policy is added to the VPC. In addition, to ensure that the web UI of Hadoop can be easily accessed, one of the master nodes is configured with a public IP which is billed by traffic. A router node has no public IPs by default. If you need one for it, you can bind it to an EIP in the [CVM Console](https://console.cloud.tencent.com/cvm/eip).
>!
>- A public IP is enabled for a master node when a cluster is created, but you can disable it based on the actual conditions.
- Enabling the public IP for the master node is mainly for SSH login and component viewing in the web UI.
- A master node with a public IP enabled is billed by traffic with a bandwidth of up to 5 Mbps. Once the cluster is created, you can make adjustments to its network in the console.
