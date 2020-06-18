## Operation Scenarios
This document describes how to create an EMR cluster in the EMR Console.

## Directions
Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click **Create Cluster** on the cluster list page.

### 1. AZ and software configuration
- **Billing Mode**: pay-as-you-go billing is supported.
 - Pay-as-you-go: you are charged by usage duration of the cluster. This billing mode requires identity verification and will freeze the amount of 1 hour's usage fees when the cluster is created (vouchers cannot be used here). After this cluster is terminated, the frozen amount will be returned.
- **Region and AZ**: currently supported regions include Guangzhou, Shanghai, Beijing, Singapore, Silicon Valley, Chengdu, and Mumbai. Tencent Cloud products in different regions cannot communicate with one another over the private network.
- **Version and Components**: EMR recommends some commonly used combinations of components for Hadoop. You can also combine the components based on your needs.
- **[Kerberos Secure Cluster](https://intl.cloud.tencent.com/document/product/1026/31163)**: it specifies whether to enable Kerberos authentication for the cluster. This feature is not required for individual users and disabled by default.
- **[Software Configuration](https://intl.cloud.tencent.com/document/product/1026/34530)**: you can create a cluster by entering custom parameters as required. The external cluster access feature is provided as well, so that you can read/write external cluster data after configuring the correct address information in relevant parameters.
  ![](https://main.qcloudimg.com/raw/0c634886e7ecae2295fa0f45110274ae.png)
  You can click the icon next to "Software Configuration" to view instructions.
  ![](https://main.qcloudimg.com/raw/1f9d7eb49c4647c56c43c6fc2d817915.png)

### 2. Hardware configuration
- **High Node Availability**: after selecting **Enable High-Availability**, 2 master nodes, at least 3 core nodes, and 3 common nodes will be enabled by default. For more information on node types, please see [Node Type Description](https://intl.cloud.tencent.com/document/product/1026/31094).
- **Hardware Configuration**: node specification configuration. EMR provides a variety of node specifications, and you can choose the node type, core quantity, memory size, and disk type and size based on your business needs.
>Currently, up to 5 cloud disks in multiple types can be mounted to a core node (one type can be selected only once).

- **Cluster Network**: to ensure security of the EMR cluster, all nodes of the cluster are placed in a VPC; therefore, you need to set up a VPC before you can successfully create the EMR cluster.
![](https://main.qcloudimg.com/raw/0c54dcbc87b1e24bab76a291a8057fa7.png)
![](https://main.qcloudimg.com/raw/f8191b84dcfa90995e694b910c18d982.png)


### 3. Basic configuration
- **Cluster Name**: EMR clusters are differentiated by cluster name.
- **Security Group**: the security group has a firewall feature used to set the network access control of the CVM instance. If there is no security group, EMR will automatically create one for you; otherwise, you can choose to use an existing one directly. If the number of security groups has achieved the upper limit and new ones cannot be created, you can delete some obsolete ones after checking the [security groups](https://console.cloud.tencent.com/cvm/securitygroup) that are being used.
 - Create Security Group: EMR will create a security group for you and open ports 22 and 30001 and the necessary IP range for communication over the private network.
 - Select Existing EMR Security Group: select an existing EMR security group as the security group for the current instance and open ports 22 and 30001 and the necessary IP range for communication over the private network.
- **Remote Login**: port 22 is usually used for remote login and opened on the newly created security group by default. You can close it based on your business needs.
- **COS**: after COS is activated, the EMR cluster can directly compute the data stored in COS to implement computation/storage separation and reduce the costs of big data processing. To ensure that EMR has access to the data in COS, you need to enter the API key of COS.
- **Add Bootstrap Action**: a bootstrap action is a custom script executed when a cluster is created to help you modify the cluster environment, install third-party software, and use your own data.
- **Tag**: you can add tags to clusters or node resources during resource creation to facilitate resource management. Up to 5 tags can be bound, and the tag key must be unique.
![](https://main.qcloudimg.com/raw/cc34a62041e39edcb95224a0c10e4f0b.png)

### 4. Complete the creation
After completing the configuration items above, click **Purchase** and make the payment. After the payment is successfully made, the EMR cluster will enter the creation process. The newly created cluster can be viewed in the EMR Console after about 10 minutes.
>You can view the instance information of each node in the CVM Console. To ensure the normal operations of the EMR cluster, do not modify the configuration information of these instances in the CVM Console.
