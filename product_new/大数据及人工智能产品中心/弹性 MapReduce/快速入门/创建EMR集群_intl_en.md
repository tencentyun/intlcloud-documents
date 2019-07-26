## Application Scenario
This document describes how to create an EMR cluster in the EMR Console.

## Directions
Log in to the [EMR Console](https://console.cloud.tencent.com/emr) and click **Create Cluster** on the cluster list page.

### 1. AZ and Software Configuration
- **Region and AZ**: Currently supported regions include Guangzhou, Shanghai, Beijing, and Silicon Valley. Tencent Cloud products in different regions cannot communicate with each another over a private network.
- **Version and Components**: EMR recommends some commonly used combinations of components for Hadoop. You can also combine the components based on your needs.
- **[Kerberos Secure Cluster](https://intl.cloud.tencent.com/document/product/1026/31163)**: This specifies whether to enable Kerberos authentication for the cluster. This feature is not required for individual users and disabled by default.
  ![](https://main.qcloudimg.com/raw/94cc76b09d7fa3f74ac2f96ff9441666.png)

### 2. Hardware Configuration
- **High-availability (HA) cluster**: By default, once you’ve selected **Enable high availability**, 2 master nodes, at least 3 core nodes, and 3 common nodes will be enabled. For more information about node types, see [Node Type Descriptions](https://intl.cloud.tencent.com/document/product/1026/31094).
- **Hardware Configuration**: Node specification. EMR provides a variety of node specifications. You can choose your node type, core quantity, memory size,  disk type, and disk size to meet your business needs.
- **Cluster Network**: To ensure the security of the EMR cluster, all nodes of the cluster are placed in a VPC; therefore, you need to set up a VPC before your can successfully create the EMR cluster.
![](https://main.qcloudimg.com/raw/0c72b936cebb5874ed9b6f6ea0ecfe13.png)

### 3. Basic Configuration
- **Cluster Name**: EMR clusters are differentiated by cluster name.
- **Security Group**: Security groups act as a virtual firewall and control inbound and outbound traffic for CVM instances. Create a new security group if you don’t have one. Otherwise, choose an existing one.
 - Create a security group: EMR will create a security group that allows traffic going through ports 22 and 30001 as well as all traffic from the necessary private network IP range.
 - Use an existing EMR security group: Select an existing EMR security group as the security group for your instance. Open ports 22 and 30001 as well as the required IP range for communication over the private network.
- **COS**: After COS is enabled, the EMR cluster can directly compute the data stored in COS so that the compute and storage can be separated, thus reducing the costs of big data processing. To ensure that EMR can access to your data stored in COS, please enter your COS API key.
![](https://main.qcloudimg.com/raw/677791aeb03fdec7f2bb1df48e439751.png)

### 4. Completing the Creation
After completing the configurations above, click **Purchase** to make the payment. Your EMR cluster will be automatically created once the payment is received. Wait for about 10 minutes, then you will find the cluster you just created in the EMR Console. 
> To ensure your EMR cluster working properly, you can view, but please **do not** modify the configuration information of each instance in the CVM Console.
