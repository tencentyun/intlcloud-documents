A cluster is the basic unit where ES provides hosted Elasticsearch services and you use and manage such services. This document describes how to quickly create an Elasticsearch cluster in the Tencent Cloud Console.

## Prerequisites

You have a Tencent Cloud account. For more information on how to create an account, please see [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Logging in to the console

Log in to the [ES Console](https://console.cloud.tencent.com/es) and click **Create** to enter the creation and purchase page.

### Creating a cluster

#### 1. Select configuration information

- Billing Mode: select **Pay-as-You-Go**.  
- Region: currently, ES is available in the following regions: Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong (China), Silicon Valley, Toronto, Singapore, Mumbai, Seoul, and Frankfurt.
- Deployment Mode: single-AZ (where the ES cluster is deployed in one AZ) or multi-AZ (where the cluster is deployed in two AZs in the same region). Multi-AZ mode can improve the disaster recovery capability of the cluster and ensure the stability of online businesses. The multi-AZ feature is currently in beta test, and application for eligibility has been suspended. The feature will be made fully available in near future. Please stay tuned and check the announcements posted on the official website.
- Network: select a VPC in the current region. The same VPC is accessible from multiple AZs in the same region. In multi-AZ deployment mode, you should also select the same VPC.
- AZ and Subnet: ES is deployed in a VPC. To ensure smooth access to the ES cluster over the private network, you are recommended to select a VPC in the region where your existing cloud-based businesses reside. The ES cluster can only be accessed in the same VPC.

> The VPC cannot be changed or adjusted once the ES cluster is created.
> 
> **Special notes on network selection**
 - Cross-VPC access: if you need to access an ES cluster from a CVM instance located in another VPC in the same region, consider the [peering connection](https://console.cloud.tencent.com/vpc/conn) scheme which can interconnect two different VPCs in the same region.
 - Basic network access: if your business is deployed in the basic network and you have never used a VPC, you can bind the CVM instance located in the basic network to the VPC where the ES cluster resides through Classiclink.
  Classiclink only supports VPCs in the IP range of `10.[0–47].0.0/16`. If you need to access the ES cluster from the basic network, please select a VPC in this range when creating the ES cluster.
	
- Cluster name: name the cluster as desired. This name is not a globally unique identifier and can be set as a business-related description.
- Version: Elasticsearch version. Currently, versions 7.5.1, 6.8.2, 6.4.3, and 5.6.4 are supported.
- Elastic Stack (formerly X-Pack): Elasticsearch's official commercial features, including capabilities such as data permission management, SQL JDBC, alerting, and machine learning. The features available vary by edition: the Platinum Edition has all the advanced features, the Basic Edition has some advanced features, and the Open Source Edition has only the open-source features. For more information, please see [Elastic Stack (X-Pack)](https://intl.cloud.tencent.com/document/product/845/30943).
- Node model: specifications of each node model in the cluster. The core quantity and memory size available vary by model. For more information on the node models supported by ES and how to select an appropriate type, please see [Node Type and Storage Configuration](https://intl.cloud.tencent.com/document/product/845/19551).
- Node storage type: premium or SSD cloud disk.
- Single-node storage: the disk capacity configured for each node. The storage capacity of the entire cluster is the single-node storage multiplied by the number of nodes.
- Configure dedicated master nodes: if the cluster is large, you can [configure dedicated master nodes](https://intl.cloud.tencent.com/document/product/845/19879) to further ensure the cluster stability.
- Dedicated master node model: a dedicated master node can use a different model from that of the data nodes.
- Number of dedicated master nodes: 3 or 5. An odd number of nodes ensures high availability and prevents the risk of split-brain.
- Username: this is the username used to access Kibana and Elasticsearch Platinum Edition clusters, which is defaulted to `elastic` and cannot be modified. In the Basic Edition and Open Source Edition, secure user authentication is not enabled, so no username or password is required when a cluster is accessed through an API, and this username is only used to log in to Kibana. In the Platinum Edition, user authentication is enabled, so the corresponding username and password are required when a cluster is accessed through an API.
- Password: the password corresponding to the aforementioned username. Please set it as required. If you forgot it, you can reset it on the details page.
![](https://main.qcloudimg.com/raw/9f1f7bfe2988f7e57235c66f5162c20c.jpg)

#### 2. Set the name and password
Click **Next: Set Name and Password**.
![](https://main.qcloudimg.com/raw/9eab152498cd0bfa0ae0531243c7fe5f.jpg)

#### 3. Confirm and purchase

Click **Next: Confirm Configuration Information** to confirm the configuration.
![](https://main.qcloudimg.com/raw/d151fbccf049b07854c9f2420994088a.jpg)

- Click **Activate** to create the cluster directly if the pay-as-you-go billing mode is selected. You do not need to confirm the order or pay for it, as your account balance will be deducted on an hourly basis during cluster use.

#### 4. Complete the creation
Once successful activated, the pay-as-you-go cluster just created can be viewed in the [console](https://console.cloud.tencent.com/es) and will be completely created in a matter of minutes.

## Cluster Application Development and Management

### Accessing cluster

To help you get started quickly, ES provides several types of clients for accessing clusters. For more information, please see [ES Access Method Overview](https://intl.cloud.tencent.com/document/product/845/19539).

### Monitoring cluster

ES provides a rich set of monitoring metrics to help you view the status of clusters during use. For more information, please see [Viewing Monitoring Metrics](https://intl.cloud.tencent.com/document/product/845/30947).

In the Basic Edition and Platinum Edition, Kibana also offers monitoring metrics on the **Monitor** page on the left sidebar.

### Adjusting cluster configuration

With the increase in volumes of business data and access requests, the cluster configuration can be elastically adjusted. For more information, please see [Adjusting Configuration](https://intl.cloud.tencent.com/document/product/845/30944).


