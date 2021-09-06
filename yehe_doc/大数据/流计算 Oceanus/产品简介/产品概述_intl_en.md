Oceanus is a stream data aggregation and computing service in the cloud. With it, you can easily build various applications in just a few minutes, such as website clickstream analysis, targeted ecommerce recommendation, and IoT. Oceanus is developed based on Apache Flink and provides fully managed cloud services, so you don't need to care about the OPS of infrastructure. It can also be connected to data sources in the cloud for a complete set of supporting services.    

Oceanus comes with a convenient console for you to write SQL analysis statements, upload and run custom JAR packages, and manage jobs. Based on the Flink technology, it can achieve a sub-second processing latency in petabyte-scale datasets.

Currently, Oceanus is available in the dedicated cluster mode, where you can run various jobs and manage related resources in your own cluster.

>? Based on this architecture, Oceanus needs to be authorized under your account before it can access resources in your VPC.

You can create your own dedicated cluster in the [Oceanus console](https://console.cloud.tencent.com/oceanus/cluster). The cluster has completely independent resources (CPU, memory, disk, and network) isolated from other users, ensuring the security and isolation of the Flink jobs when they are running. The dedicated cluster is isolated through VPC, so it supports user-defined JAR jobs and UDF functions to meet your custom business needs.

After the VPC of your dedicated cluster is interconnected with the VPC you specify, JAR jobs can access all the network-reachable resources in the specified VPC, including but not limited to various Tencent Cloud services in it, such as message queue, database, API service, and CVM.

In addition, if you purchase a [NAT gateway](https://intl.cloud.tencent.com/document/product/1015) in the specified VPC and properly configure a routing table, you can access internet addresses on the public network (such as public network APIs and components of other cloud vendors) to further enhance the processing capabilities of Oceanus.
![](https://main.qcloudimg.com/raw/b7983dd52cfb0c2d9b0e30e3a0d7956f.png)