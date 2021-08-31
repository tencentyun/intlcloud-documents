## Introduction
This document describes how to view an existing node pool of a cluster and query the details of the node pool via the TKE console for subsequent node pool management.




## Prerequisites
You have created a node pool for the cluster. For more information on how to create a node pool, see [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901).


## Directions
<span id="ViewNodePoolsList"></span>
### Viewing the node pool list page
1. Log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the “Cluster Management” page, click the desired cluster ID to open the “Deployment” page.
3. On the left sidebar, choose **Node Management** -> **Node Pool** to open the “Node pool list” page. You can view existing node pools and global node pool configurations, as shown in the following figure.
![](https://main.qcloudimg.com/raw/2e8aca5a76690724c78987537d09ce4c.png)
Node pool information and configurations are as follows:
 - **Global Configuration**: the common configuration items for all node pools of the cluster. You can click **Edit** in the upper-right corner of the module to modify the values. For more information, see [Adjusting Global Node Pool Configurations](https://intl.cloud.tencent.com/document/product/457/35903#adjustGlobalNodePool).
    - **Auto scale-down**: this feature is disabled in this example. If this feature is enabled, auto scale-down is triggered when a large amount of node resources in the cluster is idle. For more information, see [Cluster Scaling](https://intl.cloud.tencent.com/document/product/457/30638).
    - **Scale-up Algorithm**: the value is “Random” by default in this example, indicating that a scaling group in the node pool is randomly selected for scale-up. TKE further supports the following scale-up algorithms and you can modify the value as required:
      - **most-pods**: scales up the scaling group that can schedule the most Pods.
      - **least-waste**: scales up the scaling group that has the fewest remaining resources after Pod scheduling.
    - **Max cluster size**: displays the size information of the current cluster. When you adjust the number of existing node pools or recreate a node pool, note the size limit specified by this parameter and properly specify the number of nodes in a node pool.
 - **Node pool card page**: the node pool sorting area is located under the Global Configuration area. Each node pool is displayed as a card that includes the following information:
>When many node pools are displayed, you can enter the node pool ID or node pool name in the search box in the upper-right corner of the area to filter node pools.
>  
>
    - **Node pool ID (which is the name of the node pool)**: the value is np-***(test) in this example. Click the ID to open the details page of the node pool. You can view more information about the node pool on the page.
    - **Node pool status**: the value is “Normal” in this example, indicating that the node pool is in the normal state.
    - **Node pool operation**: the operations include **Edit**, **Adjust Number**, and **More**. For more information, see [Adjusting Node Pool Configurations](https://intl.cloud.tencent.com/document/product/457/35903#.E8.B0.83.E6.95.B4.E8.8A.82.E7.82.B9.E6.B1.A0.E9.85.8D.E7.BD.AE).
    - **Number of available nodes/Total number of nodes in the node pool**: the value is “1 available/1 in total” in this example.
    - **Model**: the model of all the nodes in the node pool.
    - **Billing Mode**: the billing mode of all the nodes in the node pool. The value is “Pay-as-you-go” in this example, indicating that the instance is billed based on actual usage. For more information on billing, see [Payment Modes](https://intl.cloud.tencent.com/document/product/213/2180).
    - **Auto scaling**: the value is “On” in this example.

### Viewing a single node pool

1. On the “Node pool card” page, click the desired node pool ID, as shown in the following figure.
![](https://main.qcloudimg.com/raw/7e6f25fbb6a1401c1d7e9ee63501f498.png)
2. On the details page of the node pool, you can view more basic information and node information of the node pool, as shown in the following figure.
![](https://main.qcloudimg.com/raw/df047f354ca9f326f87975456f6b249b.png)


## Relevant Operations
For more information on the features of node pools, see the following documents:
- [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901)
- [Adjusting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35903)
- [Deleting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35904)
