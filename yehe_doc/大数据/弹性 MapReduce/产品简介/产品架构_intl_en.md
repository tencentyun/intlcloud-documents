The logical architecture of EMR is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/e88c4f1b833b7d7cb86ae593be4630e8.png)
An EMR cluster consists mainly of three parts: open-source components, Tencent Cloud infrastructure, and cluster management.
- Open-source components
	- EMR integrates dozens of cutting-edge open-source big data components from the Apache community, such as Hadoop, Hive, Spark, HBase, Presto, Flink, Alluxio, and Iceberg. For more information, see [Product Releases and Component Versions](https://intl.cloud.tencent.com/document/product/1026/46456).
	- Based on optimized Iceberg, Alluxio and other open-source components, EMR offers Iceberg Z-Order algorithm, Alluxio transparent URI and other enhanced features.
- Tencent Cloud infrastructure
	- EMR can be deployed based on multiple types of underlying computing resources, including CVM and CBM. It supports containerized deployment.
	- Data can be stored in a local disk, cloud disk, COS bucket, or CHDFS instance.
	- VPCs, network ACLs, and security groups provide EMR with a securely isolated network environment.
- Cluster Management
	- EMR supports smart cloud deployment management, including fast creation, flexible scaling, and auto scaling.
	- EMR offers a great variety of convenient Ops tools, such as service configuration management, batch node management, and visual service Ops.
	- EMR provides complete cluster monitoring and diagnosis capabilities ranging from multidimensional metric monitoring, event, and inspection to alarming and log search.
