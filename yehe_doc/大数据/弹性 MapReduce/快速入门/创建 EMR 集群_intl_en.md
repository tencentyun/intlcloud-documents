## Overview
This document describes how to create an EMR cluster in the EMR console.

## Directions
Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Create Cluster** on the cluster list page.

### 1. Software configuration
**Region**: A region is the physical location of an IDC. Currently supported regions include Guangzhou, Shanghai, Beijing, Singapore, Silicon Valley, Chengdu, Nanjing, and Mumbai. Tencent Cloud products in different regions cannot communicate with each other over a private network.

- **Cluster Type**: There are six types of EMR clusters, namely, Hadoop cluster, ClickHouse cluster, Druid cluster, Doris cluster, Kafka cluster, and StarRocks cluster. You can choose one to deploy as needed.
**Use Cases**: Hadoop clusters support five use cases, namely, the default use case, ZooKeeper, HBase, Presto, and Kudu. You can choose one to deploy as needed.
**Product Version and Components to Deploy**: EMR recommends some commonly used combinations of components for Hadoop. You can also combine the components based on your needs.
**Kerberos Secure Cluster**: It specifies whether to enable Kerberos authentication for the cluster. This feature is not required for individual users and disabled by default.
**Software Configuration**: You can create a cluster by entering custom parameters as required. The external cluster access feature is provided as well, so that you can read/write external cluster data after configuring the correct address information in relevant parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/ad3886cbd826622ecb46acef07af6506.png)

### 2. Region and hardware configuration
**Billing Mode**: Pay-as-you-go.

- Pay-as-you-go: You are charged by usage duration of the cluster. This billing mode requires identity verification and will freeze the amount of one hour's usage fees when the cluster is created (vouchers cannot be used here). After this cluster is terminated, the frozen amount will be refunded.
**AZ**: Different AZs in the same region support different models and specifications. Tencent Cloud products in different regions cannot communicate with each other over a private network. The AZ cannot be changed after purchase. We recommend you select a latest AZ close to the region of your business data so as to reduce the access latency and increase the download speed.
**Cluster Network**: To ensure the security of the EMR cluster, all nodes of the cluster are placed in a VPC; therefore, you need to set up a VPC before you can successfully create the EMR cluster.
- **Security Group**: The security group has a firewall feature used to set the network access control of the CVM instance. If there is no security group, EMR will automatically create one for you; otherwise, you can choose to use an existing one directly. If the number of security groups has reached the upper limit and new ones cannot be created, you can delete some obsolete ones after checking the security groups that are being used.
- Create Security Group: EMR will create a security group for you and open ports 22 and 30001 and the necessary IP range for communication over the private network.
- Select Existing EMR Security Group: Select an existing EMR security group as the security group for the current instance and open ports 22 and 30001 and the necessary IP range for communication over the private network.
**Remote Login**: Port 22 is usually used for remote login and opened on the newly created security group by default. You can close it based on your business needs.
**High Availability**: High availability is enabled by default. The deployed number of different types of nodes varies by cluster type and use case under HA or non-HA mode. For more information, see [Cluster Types].
**Node Configuration**: EMR offers multiple node types. You can select an appropriate model configuration for each node type based on your business needs.

>?Currently, up to 15 cloud disks in multiple types can be mounted to a core, task, or router node (one type can be selected only once).

![](https://qcloudimg.tencent-cloud.cn/raw/1c47ba7e2c724bae4d06cfe5257c9a13.png)
![](https://qcloudimg.tencent-cloud.cn/raw/430ff289e6a1f17e8bf78e576f417cb3.png)
![](https://qcloudimg.tencent-cloud.cn/raw/09d58fbf9349382a073a83973bbd539b.png)

**Placement Group**: It is a policy for distributing and placing CVM instances on the underlying hardware. For more information, see [Placement Group].
**Hive Metadatabase**: When you choose to deploy the Hive component, there are two storage methods for Hive metadata: you can store the metadata in a MetaDB instance separately purchased for the cluster (default method) or associate the metadata with EMR-MetaDB or a self-built MySQL database. In the latter case, metadata will be stored in the associated database and will not be deleted when the cluster is terminated.

### 3. Basic configuration
**Project**: Assign the current cluster to a project. To assign an instance to a new project, create a project first. For detailed directions, see [Creating Project].
**Cluster Name**: EMR clusters are differentiated by cluster name.
**Login Method**: Currently, EMR provides two ways to log in to cluster services, nodes, and MetaDB: custom password and associated key. SSH keys are only used for logging in to the EMR-UI quick entry. The default username is "root", and the username for the WebUI quick entry of the Superset component is "admin".
**Add Bootstrap Action**: A bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.
**Tag**: You can add tags to clusters or node resources during resource creation to facilitate resource management. Up to 5 tags can be bound, and the tag key must be unique.
![](https://qcloudimg.tencent-cloud.cn/raw/db41f384910cbf3a166f388793d0a5c3.png)

### 4. Configuration information confirmation
**Auto-Renewal**: From seven days before the cluster expires, the system will check whether your account balance is sufficient every day in order to renew the cluster resources with auto-renewal enabled.
After completing the configurations above, click **Purchase** to make the payment. Your EMR cluster will be automatically created once the payment is received. Wait for about ten minutes and then you will find the cluster you just created in the EMR console.
![](https://qcloudimg.tencent-cloud.cn/raw/f9640a224bcca49cd4d311d9cc9aaa75.png)

>! You can view the information of each node in the CVM console. To ensure your EMR cluster works properly, do not modify such information.

### Subsequent steps
After the cluster is successfully created, you can log in to it accordingly to perform further configuration and other operations on it. For specific operations, see the following documents:
- [Logging in to Clusters](https://intl.cloud.tencent.com/document/product/1026/31101)
- **Cluster configuration**: [Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34530), [Mounting CHDFS](https://intl.cloud.tencent.com/document/product/1026/35773), and [Unified Management of Hive Metadata](https://intl.cloud.tencent.com/document/product/1026/36299)
- **Cluster management**: [Setting Tag](https://intl.cloud.tencent.com/document/product/1026/34532), [Bootstrap Actions](https://intl.cloud.tencent.com/document/product/1026/34521), and [Cluster Termination](https://intl.cloud.tencent.com/document/product/1026/31106)
