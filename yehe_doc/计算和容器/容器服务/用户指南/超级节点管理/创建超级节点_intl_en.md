## Overview
This document describes how to deploy virtual node in the cluster through the TKE console, and deploy the cluster workload as an elastic container.

## Prerequisites

- You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- The cluster Kubernetes is v1.16 or later version.
- You have known the [Notes on Scheduling Pod to Virtual Node](https://intl.cloud.tencent.com/document/product/457/39760).

## Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the **Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. In the left sidebar, choose **Node Management** > **Node Pool** to open the **Node Pool List** page, as shown below:
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. Click **Create Node Pool** to open the “Create Node Pool” page. Specify the configurations according to the following descriptions.
   ![](https://main.qcloudimg.com/raw/8b270eb21ab8e68e9d13df112b7caf2a.png)
 - **Node Pool Name**: you can customize the name of the node pool based on service requirements to facilitate subsequent resource management.
 - **Node Pool Type**: **CVM** and **Virtual Node** types are supported currently. For the **Virtual Node** type, no physical or virtual server is added to the cluster. Instead, the virtual node is deployed in the cluster, and the Pod that meets the scheduling conditions will be scheduled to the virtual node maintained by [Elastic Kubernetes Service](https://intl.cloud.tencent.com/document/product/457/34040).
<dx-alert infotype="notice" title="">
Pods scheduled to the virtual node will be billed based on the amount of resources that the Pods apply for and the actual use period. For details, please see [Elastic Clusters Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Elastic Clusters Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Elastic Clusters Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).
</dx-alert>
 - **Supported Network**: the system will allocate IP addresses within the address range of the node network for servers in the cluster.

>!This configuration item is specified at the cluster level and therefore cannot be modified after configuration.

 - **Security Groups**: the default value is the security group specified when the cluster is created. You can replace the security group or add a security group as required.

>!
> - The security group configured for the virtual node is directly associated with Pods in the node. Please configure the network rules as required by the pods. For example, you need to open port 80 if the pods provide service via port 80.
> - This security group is the default security group bound to the Pod that is scheduled to the virtual node. You can specify other security group during scheduling. For more information, see [Notes on Scheduling Pod to Virtual Node](https://intl.cloud.tencent.com/document/product/457/39760).

 - **Container Network**: specify the network allocated when the Pod is scheduled to the virtual node. The Pods scheduled to virtual node are on the same VPC network plane as the Tencent Cloud services such as CVM and TencentDB. Each Pod will use an IP address of the VPC subnet. Please select a suitable subnet with sufficient available IP addresses based on the actual needs.

>!
> -  It is recommended to select the subnets of multiple AZs to ensure availability.
> -  A corresponding virtual node will be generated for each selected subnet. When Pod is scheduled in batches, it will be automatically distributed on multiple virtual nodes (subnets) by default.

5. (Optional) Click **More Settings** to view or configure more information.
  - **Cordon Initial Node**: after **Cordon this node** is selected, no new Pod can be scheduled to this node. To uncordon the node, you must manually uncordon the node or run the [Uncordon command](https://intl.cloud.tencent.com/document/product/457/30654) in custom data and specify the values as needed.
  - **Label**: click **New Label** and customize the settings of the label. The specified label here will be automatically added to virtual nodes created in the node pool to help filter and manage virtual nodes using labels.
  - **Taints**: the attributes of the node. This parameter is usually used with `Tolerations`. You can specify this parameter for all the virtual nodes of the node pool so that Pods that do not meet the relevant conditions cannot be scheduled to these nodes and any such Pods already on these nodes will be drained.

>?
>The value of Taints usually consists of `key`, `value`, and `effect`. Valid values of `effect`:
> - **PreferNoSchedule**: optional condition. Try not to schedule a Pod to a node with a taint that cannot be tolerated by the Pod.
> - **NoSchedule**: when a node contains a taint, a Pod without the corresponding toleration must not be scheduled.
> - **NoExecute**: when a node contains a taint, a Pod without the corresponding toleration to the taint will not be scheduled to the node and any such Pods already on the node will be drained.
Assume that Taints is set to `key1=value1:PreferNoSchedule`. The following figure shows the configurations in the TKE console:
![](https://main.qcloudimg.com/raw/77e4c8af7ff51bda12599819fffdce1b.png)

6. Click **Create Node Pool** to complete the creation of the virtual node.

## Relevant Operations

After the creation of the virtual node, please refer to [Managing a Virtual Node](https://intl.cloud.tencent.com/document/product/457/39758) for the subsequent management of the node pool.
