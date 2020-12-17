## Selecting a Cluster Type
Elastic MapReduce (EMR) provides three types of clusters for you to choose from based on your business needs.
-**Hadoop cluster:** comes in two editions — Standard and TianQiong. A Hadoop cluster provides open source big data components such as Hadoop, HBase, Hive, Spark, Flink, and Presto. It is mainly used for offline data analysis, real-time data analysis, ad hoc, and other big data processing scenarios.
-**Druid cluster:** provides the Druid component, which is a distributed time series database and mainly used for data aggregations and queries based on time series.
-**ClickHouse cluster:** provides the ClickHouse component, which is an open source column-oriented database and mainly used for the analysis of well-structured, clear, and immutable events or log streams.

## Selecting a Billing Mode
Billing mode for EMR clusters:
- **Pay-as-you-go:** all nodes in a cluster are charged on a pay-as-you-go basis. This is suitable for clusters that exist for a short time or periodically.

For information on node types, see [Node Type Description](https://intl.cloud.tencent.com/document/product/1026/31094).

## Selecting a Model and Specification
EMR offers a wide variety of CVM models, including EMR Standard, EMR Compute, EMR High IO, EMR MEM-optimized, and EMR Big Data. If you need the CPM model, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to us.
>!
>- A high availability (HA) Hadoop or Druid cluster contains at least eight nodes, including two master nodes, three common nodes, and three core nodes. A non-HA Hadoop or Druid cluster adopts single-replica storage, which can be used for testing but is not recommended in production environment. It contains at least three nodes, including one master node and at least two core nodes.
>- An HA ClickHouse cluster contains at least five nodes, including two core nodes and three common nodes. A non-HA ClickHouse cluster adopts single-replica storage, which can be used for testing but is not recommended in production environment. It contains at least one core node.

You can choose a model based on your business needs and budget.
- If you require low latency for offline compute, we recommend you select a model with local disks or the Big Data model.
- If you need to use the real-time database HBase, we recommend you select the EMR High IO model with local SSD disks for optimal performance.

### Node specification recommendations
<table>
   <tr>
      <th width=13%>Node Type</th>
      <th width=17%>Cluster Type</th>
      <th width=70%>Recommended Specification</th>
   </tr>
   <tr>
      <td rowspan="3">Master</td>
      <td>Hadoop</td>
      <td>For master nodes, we recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud disks for high stability.</td>
   </tr>
   <tr>
      <td>ClickHouse</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid</td>
      <td>For master nodes, we recommend you select an instance specification with a large memory size (at least 16 GB) and use SSD disks for better IO performance.</td>
   </tr>
	    <tr>
      <td rowspan="3">Core</td>
      <td>Hadoop</td>
      <td><li>If most of your data is stored on COS, core nodes will function in a way similar to task nodes and should have a capacity of at least 500 GB. <strong>Core nodes cannot be elastically scaled.</strong>
<li>If your architecture does not use COS, core nodes are responsible for processing cluster compute and storage tasks, and three-replica backup is enabled by default. When estimating the data disk capacity, you need to consider the capacity for storing three replicas. In this case, the Big Data model is recommended.
</td>
   </tr>
   <tr>
      <td>ClickHouse</td>
      <td>For core nodes, we recommend you select a model with high CPU and a large memory size. Because data may be lost if a local disk is corrupted, cloud disks are recommended.</td>
   </tr>
   <tr>
      <td>Druid</td>
      <td>For core nodes, we recommend you select an instance specification with a large memory size (at least 16 GB) and use SSD disks for better IO performance.</td>
   </tr>
	 <tr>
	 <td rowspan="3">Task</td>
      <td>Hadoop</td>
      <td><li>If your architecture does not use COS, task nodes are not required.
<li>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.
</td>
   </tr>
   <tr>
      <td>ClickHouse</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid</td>
      <td><li>If your architecture does not use COS, task nodes are not required.
<li>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.
</td>
   </tr>
	 <tr>
	 <td rowspan="3">Common</td>
      <td>Hadoop</td>
      <td>Common nodes are mainly used as ZooKeeper nodes. We recommend you select the specification of 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
   </tr>
   <tr>
      <td>ClickHouse</td>
      <td>For common nodes, the CPU and memory configuration should be at least 4 cores and 16 GB.</td>
   </tr>
   <tr>
      <td>Druid</td>
      <td>Common nodes are mainly used as ZooKeeper nodes. We recommend you select the specification of 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
   </tr>
	 <tr>
	 <td rowspan="3">Router</td>
      <td>Hadoop</td>
      <td>Router nodes are mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
   </tr>
   <tr>
      <td>ClickHouse</td>
      <td>-</td>
   </tr>
   <tr>
      <td>Druid</td>
      <td>Router nodes are mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
   </tr>
</table>

## Network and Security
To ensure the network security, the EMR cluster is placed in a VPC, and a security group policy is added to the VPC. In addition, to ensure easy access to the WebUI of Hadoop, a public IP is enabled for one of the master nodes and the node is billed by traffic. A public IP is not enabled for router nodes by default. However, you can bind a router node to an EIP on the [CVM console](https://console.cloud.tencent.com/cvm/eip) to enable a public IP for it.
>!
>- A public IP is enabled for master nodes when a cluster is created. You can disable it as needed.
- Enabling a public IP for master nodes is mainly for SSH login and component WebUI access.
- Master nodes with a public IP enabled are billed by traffic with a bandwidth of up to 5 Mbps. You can adjust the network on the console after creating a cluster.
