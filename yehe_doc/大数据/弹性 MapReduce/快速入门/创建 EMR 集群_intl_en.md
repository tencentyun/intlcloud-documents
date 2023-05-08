## Overview
This document describes how to create an EMR cluster in the EMR console.

## Directions
Log in to the [EMR console](https://console.cloud.tencent.com/emr) and click **Create cluster** on the cluster list page.

### 1. Software configuration
**Region**: A region is the physical location of an IDC. Currently supported regions include Guangzhou, Shanghai, Beijing, Singapore, Silicon Valley, Chengdu, Nanjing, and Mumbai. Tencent Cloud products in different regions cannot communicate with each other over a private network.
- **Cluster type**: There are six types of EMR clusters, namely, Hadoop, ClickHouse, Druid, Doris, Kafka, and StarRocks. You can choose one to deploy as needed.
**Use cases**: Hadoop clusters support five use cases, namely, Hadoop-Default, ZooKeeper, HBase, Presto, and Kudu. You can choose one to deploy as needed.
- **Product version** and **Components to deploy**: EMR recommends some commonly used combinations of components for Hadoop. You can also combine the components based on your needs.
**Kerberos mode**: It specifies whether to enable Kerberos authentication for the cluster. This feature is not required for individual users and disabled by default.
**Software configuration**: You can create a cluster by entering custom parameters as required. The external cluster access feature is provided as well, so that you can read/write external cluster data after configuring the correct address information in relevant parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/ad3886cbd826622ecb46acef07af6506.png)

### 2. AZ and hardware configuration
- **Billing mode**: Pay-as-you-go is supported.

- Pay-as-you-go: You are charged by usage duration of the cluster. This billing mode requires identity verification and the amount of two hours' usage fees will be frozen when the cluster is created (vouchers cannot be used here). After this cluster is terminated, the frozen amount will be refunded.

**AZ**: Different AZs in the same region support different models and specifications. Tencent Cloud products in different regions cannot communicate with each other over a private network. The AZ cannot be changed after purchase. We recommend you select a new AZ closest to the region of your business data to reduce the access latency and increase the download speed.
- **Cluster network**: To ensure the security of the EMR cluster, all nodes of the cluster are placed in a VPC; therefore, you need to set up a VPC before creating the EMR cluster.
- **Security group**: The security group has a firewall feature and is used to set the network access control of the CVM instance. You can use an existing security group. If there is no existing one, EMR will automatically create one for you. If the number of security groups has reached the upper limit and new ones cannot be created, you can delete some unnecessary ones after checking the security groups that are being used.
- Create a security group: EMR will create a security group that allows traffic going through ports 22 and 30001 as well as all traffic from the necessary private network IP range.
- Use an existing EMR security group: Select an existing EMR security group as the security group for your instance. Open ports 22 and 30001 as well as the required IP range for communication over the private network.

- **Remote login**: Port 22 is usually used for remote login and opened on the newly created security group by default. You can close it based on your business needs.
**High availability (HA)**: High availability is enabled by default. The number of different types of nodes deployed varies by cluster type and use case under HA or non-HA mode. For more information, see [Cluster Types](https://intl.cloud.tencent.com/document/product/1026/31094).
**Node configuration**: EMR offers multiple node types. You can select an appropriate model configuration for each node type based on your business needs.

>?Currently, up to 15 cloud disks of multiple types (one type can be selected only once) can be mounted to a core, task, or router node.

![](https://qcloudimg.tencent-cloud.cn/raw/1c47ba7e2c724bae4d06cfe5257c9a13.png)
![](https://qcloudimg.tencent-cloud.cn/raw/04fd650c32541d90a1fbd7b47cca9ed9.png)
![](https://qcloudimg.tencent-cloud.cn/raw/430ff289e6a1f17e8bf78e576f417cb3.png)

**Placement group**: It is a policy for distributing and placing CVM instances on the underlying hardware. For more information, see [Placement Group].
**Hive metadatabase**: If you choose to deploy the Hive component, there are two storage methods for Hive metadata. You can store the metadata in a MetaDB instance separately purchased for the cluster, or associate the metadata with EMR-MetaDB or a self-created MySQL database. In the latter case, metadata will be stored in an associated database and not be cleared when the cluster is terminated.

### 3. Basic configuration
**Project**: Assign the current cluster to a project. To assign an instance to a new project, create a project first. For detailed directions, see [Creating Project].
**Cluster name**: Use names to differentiate EMR clusters.
**Login method**: Currently, EMR provides two ways to log in to cluster services, nodes, and MetaDB, namely, custom password and associated key. SSH keys are only used for logging in to the EMR-UI via the quick entry. The default username is "root", and the username for the WebUI quick entry of the Superset component is "admin".
**Advanced settings**:
- **Bootstrap actions**: A bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.
- **Tag**: You can add tags to clusters or node resources during resource creation to facilitate resource management. Up to 5 tags can be bound to a cluster, and the tag keys must be unique.
![](https://qcloudimg.tencent-cloud.cn/raw/db41f384910cbf3a166f388793d0a5c3.png)

### 4. Configuration confirmation
**Auto-renewal**: During the seven days before the cluster expires, the system will check whether your account balance is sufficient every day in order to renew the cluster resources with auto-renewal enabled.
After completing the configurations above, click **Purchase** to make the payment. Your EMR cluster will be automatically created once the payment is received. You will find the cluster you just created in the EMR console after about 10 minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/f9640a224bcca49cd4d311d9cc9aaa75.png)

>!You can view the information of each node in the CVM console. To ensure your EMR cluster works properly, do not modify such information.

### Subsequent operations
After the cluster is successfully created, you can log in to it and further configure and perform other operations on it. For specific operations, see the following documents:
- [Logging In to Clusters](https://intl.cloud.tencent.com/document/product/1026/31101)
- **Cluster configuration**: [Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34530), [Mounting CHDFS Instance](https://intl.cloud.tencent.com/document/product/1026/35773), and [Unified Management of Hive Metadata](https://intl.cloud.tencent.com/document/product/1026/36299)
- **Cluster management**: [Setting Tag](https://intl.cloud.tencent.com/document/product/1026/34532), [Bootstrap Actions](https://intl.cloud.tencent.com/document/product/1026/34521), and [Cluster Termination](https://intl.cloud.tencent.com/document/product/1026/31106)
