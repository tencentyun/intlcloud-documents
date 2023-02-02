## Overview
Peering Connection is a high-bandwidth and high-quality connectivity service that supports communication among Tencent Cloud resources. You can achieve **intra-region and cross-region** communication among different clusters through a peering connection.

## Prerequisites

- The directions in this document are based on an existing cluster with nodes. If no such a cluster exists, create one by referring to [Quickly Creating a Standard Cluster](https://intl.cloud.tencent.com/document/product/457/40029).
- Create a peering connection by referring to [Creating Intra-account Peering Connection](https://intl.cloud.tencent.com/document/product/553/18836). Make sure that the peering connection is successfully created and the CVM instances can communicate with one another. If the peering connection does not work, go to the console and check if the **route table**, **CVM security groups**, and **subnet ACL** are configured properly.



## Directions

>?To implement interconnection between cross-region clusters, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) after completing the following steps to configure container routing to interconnect containers.

### Getting container information
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
3. [](id:step3)Click the target cluster ID/name to go to the cluster details page. For example, go to the basic information page of cluster A.
4. [](id:step4)Record the following information: **Region**, **Node Network**, and **Container Network**.
5. Repeat [step 3](#step3) to [step 4](#step4) for the other container in the different cluster.
For example, go to the basic information page of cluster B, record the **Region**, **Node Network**, and **Container Network** of the cluster B container.


### Configuring route tables

1. Log in to the VPC console and select [**Peering connection**](https://console.cloud.tencent.com/vpc/conn) from the left sidebar.
2. On the peering connection management page, record the **name/ID** of the peering connection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5Yue662_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223184401.png)
3. [](id:VPCStep3)Select **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** from the left sidebar to go to the subnet management page.
4. Click the route table associated with the desired subnet.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EPD9296_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223184548.png)
5. On the details page of the associated route table, click **+ New routing policies**.
6. On the **Add a route** page, configure the following parameters:
 - Destination: Enter the IP address range of the container in Cluster B.
 - Next hop type: Select **Peering connection**.
 - Next hop: Select the established peering connection.
7. [](id:VPCStep7)Click **OK** to complete the configuration of the local route table.
8. Repeat [step 3](#VPCStep3) to [step 7](#VPCStep7) to configure the route table of the opposite end.

### Expected Results
- **Intro-region peering**: the above directions should allow containers in different clusters to communicate.
- **Cross-region cluster**: after the peering connection is established successfully, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category ) to configure container routing to interconnect the containers.

Refer to [Basic Remote Terminal Operations](https://intl.cloud.tencent.com/document/product/457/9120) on how to log in to a container, and verify the peering connection as instructed below:
1. Log in to the container in Cluster A and access the container in Cluster B.
![](https://qcloudimg.tencent-cloud.cn/raw/cce639e7fb41f375a9612dadf662b37a.png)
2. Log in to the container in Cluster B and access the container in Cluster A.
![](https://main.qcloudimg.com/raw/6ec462617b4130cc73e088a8632a406e.png)


