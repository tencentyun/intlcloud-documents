## Introduction
Peering Connection provides high-bandwidth, high-quality data links connecting Tencent Cloud resources. With Peering Connection, you can implement . For more information, refer to [Creating Peering Connections](https://intl.cloud.tencent.com/document/product/553/18836).

>
>- The directions in this document are based on an existing cluster with nodes. If you don't have one, please refer to [Creating Clusters](https://intl.cloud.tencent.com/document/product/457/11741).
>- Make sure that the peering connection is successfully created and the CVM instances can communicate with one another. If the peering connection does not work, go to the console and check if the **route table**, **CVM security groups**, and **subnet ACL** are configured properly.



## Directions

> If you need cross-region peering, please complete the following directions and [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to apply for container interconnection through routing.

### Getting container information
1. Log in to the TKE console and select **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** from the left sidebar.
2. <span id="step3">Click the ID/name of the desired cluster to go to its cluster management page.</span>
The following is the cluster management page of Cluster A.
![](https://main.qcloudimg.com/raw/37757652cd5c8fe05452c961ce35020a.png)
3. Select **Basic Information** from the left sidebar to go to the **Basic Information** page.
![](https://main.qcloudimg.com/raw/7e0db2c6133f1c6b0af40dfc833147d3.png)
4. <span id="step5">Record the following information: **Region**, **Node Network**, and **Container Network**.
5. Repeat [step 3](#step3) to [step 5](#step5) for the other container in the different cluster.
For example, you can record the information of the container in Cluster B.


### Configuring route tables

1. Log in to the VPC console and select [**Peering connection**](https://console.cloud.tencent.com/vpc/conn) from the left sidebar.
2. In the peering connection management page, record the **name/ID** of the peering connection.
3. <span id="VPCStep3">Select **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** from the left sidebar to go to the subnet management page.
4. Click the route table associated with the desired subnet.
![](https://main.qcloudimg.com/raw/fd61cd59e135f9f7de1b528a17a80779.png)
5. On the details page of the associated route table, click **+ New routing policies**.
6. In the **Add a route** page, configure the following parameters:
 - Destination: Enter the IP address range of the container in Cluster B.
 - Next hop type: Select **Peering connection**.
 - Next hop: Select the established peering connection.
7. <span id="VPCStep7">Click **OK**. This completes the configuration of route table at the local end.</span>
8. Repeat [step 3](#VPCStep3) to [step 7](#VPCStep7) to configure the route table of the opposite end.

### Expected Results
- **Intro-region peering**: the above directions should allow containers in different clusters to communicate.
- **Cross-region peering**: after creation of the peering connection, [submit a ticket](https://console.cloud.tencent.com/workorder/category/?level1_id=6&level2_id=350&source=undefined&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to apply for container interconnection through routing.

Refer to [Basic Remote Terminal Operations](https://intl.cloud.tencent.com/document/product/457/9120) on how to log in to a container, and verify the peering connection as instructed below:
1. Log in to the container in Cluster A and access the container in Cluster B.
![](https://main.qcloudimg.com/raw/18e74866a2bd8824b4537af65108b62a.png)
2. Log in to the container in Cluster B and access the container in Cluster A.
![](https://main.qcloudimg.com/raw/6ec462617b4130cc73e088a8632a406e.png)
