## Overview
Peering Connection provides high-bandwidth, high-quality data links connecting Tencent Cloud resources. With Peering Connection, you can implement . For more information, refer to [Creating Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836).

>!
>- The directions in this document are based on an existing cluster with nodes. If you don't have one, please refer to [Creating Clusters](https://intl.cloud.tencent.com/document/product/457/40029).
>- Make sure that the peering connection is successfully created and the CVM instances can communicate with one another. If the peering connection does not work, go to the console and check if the **route table**, **CVM security groups**, and **subnet ACL** are configured properly.



## Directions

>?To implement interconnection between cross-region clusters, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) after completing the following steps to configure container routing to interconnect containers.

### Getting container information
1. Log in to the TKE console and select **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. [](id:step3)Click the ID/name of the cluster for which to set cluster interconnection to enter the management page of the cluster.
3. In the left sidebar, select "Basic information" to go to the "Basic information" page.
5. [](id:step5)Record the following information: **Region**, **Node Network**, and **Container Network**.
6. Repeat [step 3](#step3) to [step 5](#step5) for the other container in the different cluster.
For example, you can record the information of the container in Cluster B.


### Configuring route tables

1. Log in to the VPC console and select [**Peering Connection**](https://console.cloud.tencent.com/vpc/conn) on the left sidebar.
2. In the peering connection management page, record the **name/ID** of the peering connection.
3. [](id:VPCStep3)Select **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** on the left sidebar to enter the subnet management page.
4. Click the local end of the peering connection and specify the routing table associated with the subnet.
5. On the **Default Details** page of the associated route table, click **+ New routing policies**.
6. In the **Add a route** page, configure the following parameters:
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



