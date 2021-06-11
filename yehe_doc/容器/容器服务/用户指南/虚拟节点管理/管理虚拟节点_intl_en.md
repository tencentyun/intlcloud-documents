## Overview

This document describes how to manage the node pool of virtual node type in the cluster, including how to adjust the node pool of virtual node type and adjust the virtual nodes in the node pool.

## Prerequisites

- You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- The cluster Kubernetes is v1.16 or later version.
- There is already a node pool of virtual node type in the cluster.
- You have known [Notes on Scheduling Pod to Virtual Node](https://intl.cloud.tencent.com/document/product/457/39760).

## Adjusting a Node Pool of Virtual Node Type
### Managing a node pool of virtual node type
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Node Pool** to open the **Node Pool List** page, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. Select a node pool of virtual node type that you want to modify and click **Edit**.
5. On the **Adjust node pool configuration** page, modify the information of the node pool, such as name, Labels, and Taints, as shown in the figure below:
>! The modifications of Labels and Taints will take effect on all virtual nodes in the node pool. Please note that if there are special scheduling policies.
>
![](https://main.qcloudimg.com/raw/82c7582937d53291993dac45dd1fc7c8.png)

### Deleting a node pool of virtual node type
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Node Pool** to open the **Node Pool List** page, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. Select a node pool of virtual node type that you want to modify and click **More** > **Delete**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/38a8adb117764e1fd7df8c332e4c6e44.png)
5. On the **Delete Virtual Node Pool** page, click **OK** to delete the node pool, as shown in the figure below:
>! The virtual node with a running Pod cannot be deleted. If you select **Forced deletion**, all Pods in the node pool will be drained and rebuilt. Please ensure that all Pods can be rescheduled to other node pools.
>
![](https://main.qcloudimg.com/raw/1fe5613c4695322373025632319e04bb.png)

## Adjusting a Virtual Node
### Creating a virtual node
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Node Pool** to open the **Node Pool List** page, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. Select a node pool of virtual node type that you want to modify and click the node pool ID to go to its details page. You can edit the basic information, create or delete a virtual node, and drain, cordon/uncordon a specific virtual node, as shown in the figure below:
![](https://main.qcloudimg.com/raw/c31042c6068e6c1c8283d8c1e270b634.png)
5. On the node pool details page, click **Create Node** to add virtual node to the current node pool. You only need to specify the VPC subnet associated with the new virtual node. Please ensure that the specified subnet has sufficient available IP addresses.
>! The new virtual node will use the configurations of the node pool, such as the VPC, security group, Labels, and Taints.
>


### Removing a virtual node
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Node Pool** to open the **Node Pool List** page, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/ad7d2bd9637c9faa853e570b0873bfb9.png)
4. Select a node pool of virtual node type that you want to modify and click the node pool ID to go to its details page.
5. On the node pool details page, select a virtual node and click **Remove** to delete it, as shown in the figure below:
>! The virtual node with a running Pod cannot be deleted. If you select **Forced deletion**, all Pods on the virtual nodes will be drained and rebuilt. Please ensure that all Pods can be rescheduled to other nodes.
>
![](https://main.qcloudimg.com/raw/1fe5613c4695322373025632319e04bb.png)


### Managing a virtual node
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Node Pool** to open the **Node Pool List** page, as shown in the figure below:
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. Select a node pool of virtual node type that you want to modify and click the node pool ID to go to its details page. 
5. Click the virtual node name to go to its details page. You can manage the Pods on the virtual node, view virtual node events, YAML and other information.
![](https://main.qcloudimg.com/raw/e33c4df8ab26e13a4038cc65842618bf.png)

