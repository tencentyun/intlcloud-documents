A cluster is the basic unit where ES provides hosted Elasticsearch services and you use and manage such services. This document describes how to quickly create an Elasticsearch cluster in the Tencent Cloud Console.

## Prerequisites

You have a Tencent Cloud account. For more information about how to create an account, see [Signing up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Logging in to the Console

Log in to the [ES Console](https://console.cloud.tencent.com/es) and click **Create** to enter the creation and purchase page.

### Creating a Cluster

#### 1. Select configuration information

- Billing type: **Pay-as-you-go**. After you purchase a cluster, it will be billed by the actual usage and can be terminated at any time. After its termination, no more fees will be incurred.
- Region: Currently, ES is available in 9 regions, including Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong, Silicon Valley, Toronto, Shanghai Finance, and Shenzhen Finance. To use it in Shanghai Finance and Shenzhen Finance regions, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- Deployment mode: Single-AZ (where the ES cluster is deployed in one AZ) or multi-AZ (where the cluster is deployed in two AZs in the same region). Multi-AZ mode can improve the disaster recovery capability of the cluster and ensure the stability of online businesses. It is currently in beta. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) if you wish to choose this mode. Please note that this mode can only be selected if there are multiple AZs and sufficient resources in the region.
- Network: Select a VPC in the current region. The same VPC is accessible from multiple AZs in the same region. In multi-AZ deployment mode, you should also select the same VPC.
- AZ and subnet: ES is deployed in a VPC. To ensure smooth access to the ES cluster over a private network, you are recommended to select a VPC in the region where your existing cloud-based businesses reside. The ES cluster can only be accessed in the same VPC.

> The VPC cannot be changed or adjusted once the ES cluster is created.

 **Special note on network selection**
 - Cross-VPC access: If you need to access an ES cluster from a CVM instance located in another VPC in the same region, consider the [Peering Connection](https://intl.cloud.tencent.com/document/product/215/5000) solution which can interconnect two different VPCs in the same region.
 - Basic network access: If your business is deployed in a basic network and you have never used a VPC, you can bind the CVM instance located in the basic network to the VPC where the ES cluster resides through Classiclink. For more information, see [Classiclink](https://intl.cloud.tencent.com/document/product/215/5002).
    Classiclink only supports VPCs in the IP range of `10.[0~47].0.0/16`. If you need to access the ES cluster from the basic network, please select a VPC in this range when creating the ES cluster.
	
- Cluster name: Name the cluster as desired. This name is not a globally unique identifier and can be set as a business-related description.
- Version: Elasticsearch version. Currently, versions 5.6.4 and 6.4.3 are supported.
- Elastic Stack (formerly X-Pack): Elasticsearch's official commercial features, including capabilities such as data permission management, SQL JDBC, alerting, and machine learning. The features available vary by edition: the Platinum edition has all the advanced features, the Basic edition has some advanced features, and the Open Source edition has only the open-source features. For more information, see [Elastic Stack (Formerly X-Pack)](https://intl.cloud.tencent.com/document/product/845/30943).
- Node model: Specifications of each node model in the cluster. The core quantity and memory size available vary by model. For more information about the node models supported by ES and how to select an appropriate type, see [Suggestions on Node Type and Storage Configuration](https://intl.cloud.tencent.com/document/product/845/19551).
- Node storage type: Premium or SSD cloud disk.
- Single-node storage: The disk capacity configured for each node. The storage capacity of the entire cluster is the single-node storage multiplied by the number of nodes.
- Configure dedicated master nodes: If the cluster is large, you can [configure dedicated master nodes](https://intl.cloud.tencent.com/document/product/845/19879) to further ensure the cluster stability.
- Dedicated master node model: A dedicated master node can use a different model from the data nodes.
- Number of dedicated master nodes: 3 or 5. An odd number of nodes ensures high availability and prevents the risk of split-brain.
- Username: This is the username used to access Kibana and Platinum edition Elasticsearch clusters, which is defaulted to "elastic" and cannot be modified. In the Basic and Open Source editions, secure user authentication is not enabled, so no username or password is required when a cluster is accessed through an API, and this username is only used to log in to Kibana. In the Platinum edition, user permission verification is enabled, so the corresponding username and password are required when a cluster is accessed through an API.
- Password: The password corresponding to the above-mentioned username. Please set it as required. If you forgot it, you can reset it on the details page.
- Auto-renewal: Optional. 
![Create a cluster](https://main.qcloudimg.com/raw/0ce3c265c2e9d14f7f5ee0d5e24e8bb1.png)
#### 2. Confirm and purchase

Click **Next: Confirm Configuration Information** to confirm the configuration.

![Confirm the configuration](https://main.qcloudimg.com/raw/5265296302f5110d6f6069d7ab5aaebf.png)

- Click **Activate** to create the cluster directly if the pay-as-you-go billing method is selected. You do not need to confirm the order or pay for it, as your account balance will be deducted on an hourly basis during cluster use.

#### 3. Complete the creation

Once successful activated, the cluster just created can be viewed in the [console](https://console.cloud.tencent.com/es) and will be completely deployed in a matter of minutes.

## Cluster Application Development and Management

### Cluster Access

To help you get started quickly, ES provides several types of clients for accessing clusters. 

<!-- For more information, see [ES Access Method Overview](https://cloud.tencent.com/document/product/845/19539). -->

### Cluster Monitoring

ES provides a rich set of monitoring metrics to help you view the status of clusters during their use. 

<!-- For more information, see [Viewing Monitoring Metrics](https://cloud.tencent.com/document/product/845/16995). -->

In the Basic and Platinum editions, Kibana also offers monitoring metrics on the **Monitor** page in the left menu.

### Adjusting Cluster Configuration

With the increase in volumes of business data and access requests, the cluster configuration can be elastically adjusted. For more information, see [Adjusting Configuration](https://intl.cloud.tencent.com/document/product/845/30944).

