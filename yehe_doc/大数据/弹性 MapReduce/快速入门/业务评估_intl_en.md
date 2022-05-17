## Selecting a Cluster Type

Elastic MapReduce (EMR) provides six types of clusters for you to choose from based on your business needs.
- Hadoop cluster: Based on open-source Hadoop and the components that form a Hadoop ecosystem, it offers five use cases, including the default use case, ZooKeeper, HBase, Presto, and Kudu, and provides big data solutions for massive data storage, offline/real-time data analysis, streaming data compute, and machine learning.
- Druid cluster: Druid is a high-performance real-time analytics database. It supports big data queries in milliseconds and multiple data ingestion methods. It is suitable for real-time big data query scenarios.
- ClickHouse cluster: ClickHouse is a column-oriented database management system. It is suitable for data warehouse analysis scenarios such as real-time wide table analysis, real-time BI report analysis, and user behavior analysis.
- Doris cluster: Doris is an MPP analytical database product that supports sub-second queries on PB-level, structured data. It is compatible with MySQL protocol and uses the standard SQL syntax. It is suitable for historical report analysis, real-time data analysis, interactive data analysis, etc.
- Kafka cluster: Kafka is a distributed, partitioned, multi-replica, and multi-subscriber message processing system based on ZooKeeper coordination. It is suitable for asynchronous processing, message communication, and streaming data receiving and distribution.
- StarRocks cluster: StarRocks adopts full vectorization technology. It supports extremely fast and unified OLAP databases. It is suitable for many data analysis scenarios, such as multidimensional, real-time, and high-concurrency analysis.

## Selecting Billing Mode
Billing mode for EMR clusters:
- **Pay-as-you-go:** All nodes in a cluster are charged on a pay-as-you-go basis. This is suitable for clusters that exist for a short time or periodically.

>! Select the shutdown mode with caution when shutting down a pay-as-you-go EMR cluster node in the CVM console, because EMR nodes do not support the "no charges when shut down" mode.

## Selecting Model and Specification

EMR offers a wide variety of CVM models, including EMR Standard, EMR Compute, EMR High IO, EMR MEM Optimized, and EMR Big Data. If you need the CPM model, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to us.

You can choose a model based on your business needs and budget.
- If you require low latency for offline compute, we recommend you select a model with local disks or the Big Data model.
- If you need to use the real-time database HBase, we recommend you select the EMR High IO model with local SSD disks for optimal performance.

### Node specification recommendations
EMR offers five types of nodes for your choice based on the cluster type.
<table>
<tr>
<th width=13%>Cluster Type</th>
<th width=13%>Use Case</th>
<th width=14%>Node Type</th>
<th width=60%>Recommended Specification</th>
</tr><tr>
<td rowspan="21">Hadoop</td>
<td rowspan="5">Default use case</td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud disks for high stability.</td>
</tr><tr>
<td>Core</td>
<td><li/>If most of your data is stored on COS, core nodes will function in a way similar to task nodes and should have a capacity of at least 500 GB. Core nodes cannot be elastically scaled.<li/>If your architecture does not use COS, core nodes are responsible for processing cluster compute and storage tasks, and three-replica backup is enabled by default. When estimating the data disk capacity, you need to consider the capacity for storing three replicas. In this case, the Big Data model is recommended.</td>
</tr><tr>
<td>Task</td>
<td><li/>If your architecture does not use COS, task nodes are not required.<li/>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.</td>
</tr><tr>
<td>Common</td>
<td>Common node: It is mainly used as ZooKeeper nodes. You need to select a specification of at least 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
</tr><tr>
<td>Router</td>
<td>Router node: It is mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
</tr><tr>
<td>ZooKeeper</td>
<td>Common</td>
<td>Common node: It is mainly used as ZooKeeper nodes. You need to select a specification of at least 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
</tr><tr>
<td rowspan="5">HBase</td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud disks for high stability.</td>
</tr><tr>
<td>Core</td>
<td><li/>If most of your data is stored on COS, core nodes will function in a way similar to task nodes and should have a capacity of at least 500 GB.</li>Note: Core nodes cannot be elastically scaled.<li/>If your architecture does not use COS, core nodes are responsible for processing cluster compute and storage tasks.</td>
</tr><tr>
<td>Task</td>
<td><li/>If your architecture does not use COS, task nodes are not required.<li/>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.</td>
</tr><tr>
<td>Common</td>
<td>Common node: It is mainly used as ZooKeeper nodes. You need to select a specification of at least 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
</tr><tr>
<td>Router</td>
<td>Router node: It is mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
</tr><tr>
<td rowspan="5"> Kudu </td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud disks for high stability.</td>
</tr><tr>
<td>Core</td>
<td><li/>If most of your data is stored on COS, core nodes will function in a way similar to task nodes and should have a capacity of at least 500 GB.</li>Note: Core nodes cannot be elastically scaled.<li/>If your architecture does not use COS, core nodes are responsible for processing cluster compute and storage tasks, and three-replica backup is enabled by default. When estimating the data disk capacity, you need to consider the capacity for storing three replicas. In this case, the Big Data model is recommended.</td>
</tr> <tr>
<td>Task</td>
<td><li/>If your architecture does not use COS, task nodes are not required.<li/>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.</td>
</tr><tr>
<td>Common</td>
<td>Common node: It is mainly used as ZooKeeper nodes. You need to select a specification of at least 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
</tr><tr>
<td>Router</td>
<td>Router node: It is mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
</tr><tr>
<td rowspan="5"> Presto </td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud disks for high stability.</td>
</tr><tr>
<td>Core</td>
<td><li/>If most of your data is stored on COS, core nodes will function in a way similar to task nodes and should have a capacity of at least 500 GB.</li>Note: Core nodes cannot be elastically scaled.<li/>If your architecture does not use COS, core nodes are responsible for processing cluster compute and storage tasks, and three-replica backup is enabled by default. When estimating the data disk capacity, you need to consider the capacity for storing three replicas. In this case, the Big Data model is recommended.</td>
</tr> <tr>
<td>Task</td>
<td><li/>If your architecture does not use COS, task nodes are not required.<li/>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.</td>
</tr><tr>
<td>Common</td>
<td>Common node: It is mainly used as ZooKeeper nodes. You need to select a specification of at least 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
</tr><tr>
<td>Router</td>
<td>Router node: It is mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
</tr> <tr>
<td rowspan="2">ClickHouse</td>	
<td rowspan="2">Default use case</td>
<td>Core</td>
<td>Core node: We recommend you select a model with high CPU and a large memory size. Because data may be lost if a local disk is corrupted, cloud disks are recommended.</td>
</tr><tr>
<td>Common</td>
<td>Common node: The CPU and memory configuration should be at least 4 cores and 16 GB.</td>
</tr><tr>
<td rowspan="2">Kafka</td>
<td rowspan="2">Default use case</td>
<td>Core</td>
<td>Core node: We recommend you select a model with high CPU and a large memory size. Because data may be lost if a local disk is corrupted, cloud disks are recommended.</td>
</tr><tr>
<td>Common</td>
<td>Common node: The CPU and memory configuration should be at least 4 cores and 16 GB.</td>
</tr><tr>
<td rowspan="3">Doris</td>
<td rowspan="3">Default use case</td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 8 GB) and store all the metadata of master nodes in the memory.</td>
</tr><tr>
<td>Core</td>
<td>Core node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud SSD for better IO performance and stability.</td>
</tr><tr>
<td>Router</td>
<td>Router node: The frontend module is deployed here for high read/write availability. Therefore, we recommend you select a model with a large memory size, preferably not less than that of master nodes.</td>
</tr><tr>
<td rowspan="5">Druid</td>
<td rowspan="5">Default use case</td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 16 GB) and use SSD disks for better IO performance.</td>
</tr><tr>
<td>Core</td>
<td>Core node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud SSD for better IO performance and stability.</td>
</tr><tr>
<td>Task</td>
<td><li/>If your architecture does not use COS, task nodes are not required.<li/>If most of your data is stored on COS, task nodes can be used as elastic compute resources and deployed as needed.
</td><tr>
<td>Common</td>
<td>Common node: It is mainly used as ZooKeeper nodes. We recommend you select the specification of 2 cores, 4 GB memory, and 100 GB cloud disk capacity to meet the requirements.</td>
</tr><tr>
<td>Router</td>
<td>Router node: It is mainly used to relieve the load of master nodes and as a task submitter. Therefore, we recommend you select a model with a large memory size, preferably not lower than the specification of master nodes.</td>
</tr><tr>
<td rowspan="3">StarRocks</td>
<td rowspan="3">Default use case</td>
<td>Master</td>
<td>Master node: We recommend you select an instance specification with a large memory size (at least 8 GB) and store all the metadata of master nodes in the memory.</td>
</tr><tr>
<td>Core</td>
<td>Core node: We recommend you select an instance specification with a large memory size (at least 8 GB) and use cloud SSD for better IO performance and stability.</td>
</tr><tr>
<td>Router</td>
<td>Router node: The frontend module is deployed here for high read/write availability. Therefore, we recommend you select a model with a large memory size, preferably not less than that of master nodes.</td>
</tr>
</table>

>!
>- Different cluster types have different requirements for the node specification. Currently, the system automatically recommends the configuration that meets the cluster's requirements by default. You can adjust the model specification based on your business needs, and the recommended model is for reference only.
>- Core nodes cannot be elastically scaled. If your architecture does not use COS, core nodes are responsible for processing cluster compute and storage tasks, and three-replica backup is enabled by default. When estimating the data disk capacity, you need to consider the capacity for storing three replicas. In this case, the Big Data model is recommended.

## Network and Security
To ensure the network security, the EMR cluster is placed in a VPC, and a security group policy is added to the VPC. In addition, to ensure easy access to the WebUI of Hadoop, a public IP is enabled for one of the master nodes and the node is billed by traffic. A public IP is not enabled for router nodes by default. However, you can bind a router node to an EIP in the [CVM console](https://console.cloud.tencent.com/cvm/eip?rid=1) to enable a public IP for it.

>!
>- A public IP is enabled for master nodes when a cluster is created. You can disable it as needed.
>- Enabling a public IP for master nodes is mainly for SSH login and component WebUI access.
>- Master nodes with a public IP enabled are billed by traffic with a bandwidth of up to 5 Mbps. You can adjust the network in the console after creating a cluster.
