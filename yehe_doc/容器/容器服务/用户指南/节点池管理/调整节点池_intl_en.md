## Overview
This document describes how to adjust the configuration of a node pool via the TKE console, including adjusting the global node pool configurations, the node pool configurations, and the number of nodes in the node pool and enabling or disabling auto scaling.


## Prerequisites

- You have created an available node pool. For more information, please see [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901).
- You have opened the Node pool list page. For more information, see [Viewing a Node Pool](https://intl.cloud.tencent.com/document/product/457/35902).

## Directions

<span id="adjustGlobalNodePool"></span>
### Adjusting global node pool configurations

1. On the “Node pool list” page, click **Edit** in the upper-right corner of the “Global Configuration” module.
![](https://main.qcloudimg.com/raw/b4903a06aa4d95593190e8d7cc49c626.png)
2. In the “Set Global Configurations for Cluster Scaling” window, specify the configuration settings according to the following descriptions. 
![](https://main.qcloudimg.com/raw/36cdb1310cfa3c8518973ff0616d3611.png) 
Main parameters are described as follows:
 - **Auto Scale-in**: this option is not selected by default. If this option is selected, auto scale-in is triggered when a large amount of node resources in the cluster is idle. For more information, see [Cluster Scaling](https://intl.cloud.tencent.com/document/product/457/30638).
 - **Scale-in Configuration**: this configuration item appears only when Auto Scale-in is selected. Specify the configuration settings as needed.
    - **Max Concurrent Scale-in Volume**: this parameter indicates the maximum number of nodes that can be scaled in concurrently. The default value is 10. You can specify the value as needed.
>!Only completely idle, empty nodes are scaled in here. If any node in the node pool contains a Pod, a maximum of one node is scaled in each time.

    - **When the ratio between the occupied resource and allocable resource is smaller than**: you can specify this value to trigger a check of scale-in conditions when the ratio of **Resources occupied by Pods or allocable resources** is less than the value. Value range: 0 to 80.
    - **Node Idle Time Threshold**: you can specify this parameter to terminate a node when the continuous idle time of a node exceeds the specified value by several minutes.
    - **Rechecking Scale-out Conditions**: this parameter allows you to specify the time when the cluster first checks the scale-out conditions.
    - **Nodes not be Scaled in**: select the following configuration items as needed to ensure that the following types of nodes will not be scaled in:
        - Nodes with locally stored Pods
        - Nodes with Pods that are located in the kube-system namespace and are not managed by DaemonSet
 - **Scale-out Algorithm**: the algorithm based on which the cluster is scaled out. Valid values:
    - **Random**: randomly selects a scaling group for scale-out.
    - **most-pods**: scales out the scaling group that can schedule the most Pods.
    - **least-waste**: scales out the scaling group that has the fewest remaining resources after Pod scheduling.
3. Click **OK**.

### Adjusting configurations of a node pool
1. On the card page of the desired node pool, click **Edit** in the upper-right corner.
![](https://main.qcloudimg.com/raw/78c2ad6771aaaa705e8734a5c850db9a.png)
2. On the “Adjust node pool configurations” page, specify the configuration settings according to the following descriptions.
![](https://main.qcloudimg.com/raw/d67c48fefa24d43101c1107aaecb2c55.png)
 - **Node Pool Name**: you can customize the name of the node pool based on your business needs to facilitate subsequent resource management.
 - **Auto Scaling**: you can select this option as needed.
 - **Number of Nodes**: The value is automatically adjusted within the specified node number range and will not exceed the specified range.
 >! This number range affects the operation of [Adjusting the number of nodes in a node pool](#adjustNodePool). For example, when the number of nodes in the current node pool has reached the maximum value within the range, the number of nodes cannot be increased again.

  - **Label**: the specified label here will be automatically added to nodes created in the node pool to help filter and manage nodes using labels. Click **New Label** to customize the label.
 - **Taints**: the attributes of the node. This parameter is usually used with `Tolerations`. You can specify this parameter for all the nodes of the node pool so that Pods that do not meet the relevant conditions cannot be scheduled to these nodes and will be drained from these nodes.
 >?The value of Taints usually consists of `key`, `value`, and `effect`. Valid values of `effect`:
> - **PreferNoSchedule**: optional condition. Try not to schedule a Pod to a node with a taint that cannot be tolerated by the Pod.
> - **NoSchedule**: when a node contains a taint, a Pod without the corresponding toleration to the taint will never be scheduled to the node.
> - **NoExecute**: when a node contains a taint, a Pod without the corresponding toleration to the taint will not be scheduled to the node and any such Pods already on the node will be drained.

Assume that Taints is set to `key1=value1:PreferNoSchedule`. The following figure shows the configurations in the TKE console:
![](https://main.qcloudimg.com/raw/019a6924bfcc0d454a0816260eb90bee.png)

3. Click **OK** and wait until the configurations are updated.


<span id="adjustNodePool"></span>
### Adjusting the number of nodes in a node pool
1. On the card page of the desired node pool, click **Adjust quantity** in the upper-right corner.
![](https://main.qcloudimg.com/raw/633abae62af2dc91a37b42e3fa575695.png)
2. On the “Adjust quantity” page, adjust the number of nodes as needed. The number of nodes cannot exceed the upper limit of the node pool, as shown in the figure below:
> ?When auto scaling is enabled for the node pool, this number is automatically adjusted based on the workload of the cluster. However, the actual number of nodes may be inconsistent with the number that is specified during adjustment.

![](https://main.qcloudimg.com/raw/22c617ed3b3ae00246804aea2cea3a93.png)
3. Click **OK** and wait until the number is adjusted.


### Enabling and disabling auto scaling
>? We recommend that you enable or disable auto scaling in the node pool on the TKE side to ensure that the status can be synchronized to Cluster-autoscaler.

1. On the card page of the desired node pool, click **More** in the upper-right corner.
![](https://main.qcloudimg.com/raw/0dccca5810605714c8fe11987eb7add0.png)
2. Select **Enable auto-scaling** or **Disable auto-scaling** as needed and then click **OK** in the window that appears.

## References
For more information on the features and operations of node pools, see the following documents:
- [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901)
- [Viewing a Node Pool](https://intl.cloud.tencent.com/document/product/457/35902)
- [Deleting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35904)




