Tencent Cloud Elastic MapReduce (EMR) is integrated with open-source frameworks and projects, such as Apache Hadoop, Apache Hive, Apache Spark, and Apache Storm. The cloud-based Hadoop services allow you to process vast amount of data securely, cost-efficiently, and elastically at scale. It has the following advantages:

## Auto Scaling
**Creating a cluster in minutes**
You can create a secure, stable, cloud-managed Hadoop cluster in just a few minutes in the console.

**Scaling in minutes**
Your EMR cluster can be smoothly scaled up or down just a few minutes as your computing needs change.

**API support**
EMR clusters can be easily created, scaled, and terminated in programs through APIs.

## Separation of Storage and Computation
 **Intra-cluster separation of storage and computation**
At the cluster level, cloud-based Hadoop clusters can be planned in a manner where storage nodes and compute nodes are separated, so that you can scale the compute nodes as needed to lower the hardware costs.

 **COS-based separation of storage and computation**
Massive amounts of data to be analyzed can be stored in COS. While the storage costs is reduced through COS, different versions of EMR clusters can be created to analyze the same data, which brings out extreme architectural flexibility.

## OPS Support
 **Monitoring and multi-channel alarming**
A comprehensive monitoring and OPS system is provided, which can detect exceptions in components such as Spark, Hive, and Presto and jobs within seconds after they occur to ensure the robust operations of big data clusters.

 **Technical support**
In addition to comprehensive technical documentation, Tencent Cloud also has a technical service system where complete technical support is provided through various channels such as ticket.

## Security
EMR uses security groups to control inbound and outbound traffic to your CVM instances. Components’ web UIs can only be accessed through one specified instance assigned with public IP, and the access requests must be authenticated by username and password. In addition, the security group of this instance only allows SSH ports and proxy access ports.
>Changing the project will cause the CVM instance to lose its security group.

