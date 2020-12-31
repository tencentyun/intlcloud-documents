## Overview

>?Node pool feature is fully launched. You can continue to use the existing scaling groups in the cluster. However, TKE will stop upgrading of the legacy scaling group feature. Please convert the existing scaling groups to node pools as soon as possible (referring to [user guide of node pool](https://intl.cloud.tencent.com/document/product/457/35901)).
For any operations except the management of the existing scaling groups, please use the Node Pool feature.

To help you efficiently manage nodes in a Kubernetes cluster, TKE introduced the concept of node pool. Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in or out.
- When a Pod in the cluster cannot be scheduled due to insufficient resources, scale-out will be triggered automatically, reducing labor costs.
- When the scale-in conditions are met, for example, when a node is idle, scale-in will be triggered automatically, reducing resource costs.

The following figure shows the overall architecture of a node pool.
![](https://main.qcloudimg.com/raw/ee033cab974b375a1e59fb5a96aaa503.png)
Generally, all nodes in a node pool share the following attributes:

- Node-level operating system
- Billing type (currently pay-as-you-go and spot instances are supported)
- CPU/memory/GPU
- Launch parameters of Kubernetes components for nodes
- Custom launch script for nodes
- Kubernetes Label and Taints settings for nodes

In addition, TKE extends the following features for a node pool:
- Support managing node pool with CRD
- Maximum number of Pods for each node in a specific node pool
- Node-pool-level automatic repair and upgrade

## Use Cases
When you need to use a large-scale cluster, we recommend that you use a node pool to manage nodes to improve the usability of the large-scale cluster. The following table describes multiple use cases for managing large-scale clusters and shows the effect of node pools in each use case.

| Use Case | Effect |
| ---- | ---- |
| A cluster includes many heterogeneous nodes with different model configurations. | A node pool allows you to manage the nodes by groups in a unified manner. |
| A cluster needs to frequently scale nodes in and out. | A node pool reduces operating costs. |
| The scheduling rules for applications in a cluster are complex. | Node pool labels allow you to quickly specify service scheduling rules. |
| Routine maintenance is required for nodes in a cluster. | A node pool allows you to conveniently upgrade the Kubernetes version and the Docker version. |

## Key Concepts
TKE Auto Scaling is implemented based on Tencent Cloud AS and the [cluster-autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler) of the Kubernetes community. The key concepts are described as follows:
- CA: [cluster-autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler), an open-source component of the community.
- AS: autoscaler, the Tencent Cloud AS service
- ASG: as group, a specific scaling group
- ASA: as activity, a scaling activity
- ASC: as config, the AS launch configuration

## Node Types in a Node Pool
To meet the requirements of different scenarios, the nodes in a node pool can be classified into the following two types:

| Node Type | Node Source | Supporting Auto Scaling | Mode of Removal from Node Pool | Is Node Quantity Affected by **Adjust Node Number** |
|---------|---------|---------|---|---|
| Nodes in the scaling group | Auto scale-out or manual adjustment of the node quantity | Yes | Auto scale-in or manual adjustment of the node quantity | Yes |
| Nodes outside the scaling group | Manually added to the node pool by users | No | Manually removed by users | No |

## Principles of Node Pool Auto Scaling
Node-pool-level auto scaling has two levels of scaling policies: the cluster autoscaler (CA) feature provided by Kubernetes, and the Auto Scaling (AS) capability provided by the Tencent Cloud AS service.
> ?
>- When multiple node pools exist, the CA will select a suitable node pool to perform scaling for you and determine the specific number of nodes for scaling.
>- The CA will trigger AS, and AS is responsible for performing node pool scaling.


- **Node pool auto scale-out**
The CA will watch the pod and node resources in the cluster. When a pod in the cluster enters the pending state, the API of the cloud-provider, namely AS (scaling group), will be called to trigger scale-out. This adjusts the scaling groups to an expected quantity.
- **Node pool auto scale-in**
When the calculated value of node utilization in the cluster is smaller than the user-specified threshold, the scale-in API of the cloud-provider, namely AS, will be called to perform scale-in on the specified nodes.



## Features and Notes

<table>
<thead>
<tr>
<th width="14%">Feature</th>
<th width="45%">Description</th>
<th width="41%">Notes</th>
</tr>
</thead>
<tbody><tr>
<td>Create a node pool</td>
<td>Add a node pool</td>
<td>We recommend that you create no more than 20 node pools for a single cluster.</td>
</tr>
<tr>
<td>Delete a node pool</td>
<td><ul class="params"><li>When you delete a node pool, you can select whether to terminate nodes in the node pool.</li><li>If you select not to terminate the node, it will not be retained in the cluster.</li></ul></td>
<td>When you delete a node pool, if you select to terminate nodes, the nodes will not be retained. You can create new nodes later if required.</td>
</tr>
<tr>
<td>Enable auto scaling for a node pool</td>
<td>After you enable auto scaling for a node pool, the number of nodes in the node pool is automatically adjusted based on the workload of the cluster.</td>
<td rowspan=2>Do not enable or disable auto scaling in the Scaling Group console.</td>
</tr>
<tr>
<td>Disable auto scaling for a node pool</td>
<td>After you disable auto scaling for a node pool, the number of nodes in the node pool is not automatically adjusted based on the workload of the cluster.</td>
</tr>
<tr>
<td>Adjust the size of a node pool</td>
<td><ul class="params"><li>Support directly adjusting the number of nodes in a node pool.</li>
<li>If you decrease the number of nodes, a node in a scaling group is selected to scale in based on the removal policy (removing the earliest node by default). Note: because the scale-in is executed by scaling group, TKE cannot detect the specific scale-in node and cannot drain or cordon in advance.</li></ul></td>
<td><ul class="params"><li>After you enable auto scaling, we recommend that you do not manually adjust the size of a node pool.</li>
<li>Please do not directly adjust the desired capacity of a scaling group on the console.</li>
<li>Please scale in the node pool through auto scaling. During auto scaling, first mark the node as unschedulable. Then, drain or delete all Pods from the node. Finally release the node.</li>
</td>
</tr>
<tr>
<td>Modify the configuration of a node pool</td>
<td>This feature allows you to change the name of a node pool, the quantity range of nodes in a scaling group, and the Kubernetes Label and Taints attributes for nodes in the node pool.</td>
<td>Modifications of the Label and Taints attributes take effect for all nodes in a node pool and may cause Pods to be rescheduled.</td>
</tr>
<tr>
<td>Add an existing node to a node pool</td>
<td><ul class="params"><li>This feature allows you to add a non-clustered pod to a node pool if the following requirements are met:<ul><li>The pod and the cluster belong to the same VPC.</li><li>The pod is not used by other clusters and has the same model and billing mode configurations as the node pool.</li></ul></ul><ul class="params"><li>This feature allows you to add a node-without-pool to a node pool if the pods in the node have the same model and billing mode configurations as the node pool.</li></ul></td><td>Generally, it is recommended to create a node pool directly.</td>
</tr>
<tr>
<td>Delete a node from a node pool</td>
<td>This feature allows you to remove a manually added node from a node pool and retain the deleted node in the cluster. Nodes cannot be directly deleted from a scaling group.</td>
<td>We recommend that you add or delete a node in a node pool by adjusting the size of the node pool or enabling auto scaling.</td>
</tr>
<tr>
<td>Convert an existing scaling group to a node pool</td>
<td><ul class="params"><li>This feature allows you to convert an existing scaling group to a node pool. After the conversion, the node pool inherits all the features of the original scaling group, and the information about the scaling group will not be displayed.</li><li>After all existing scaling groups in a cluster are converted to node pools, the auto scaling feature is disabled.</li></td>
<td>This operation is irreversible. Therefore, ensure that you understand the features of node pools before performing the conversion.</td>
</tr>
</tbody></table>

## References
You can log in to the [TKE console](https://console.cloud.tencent.com/tke2) and perform node-pool-related operations based on the following documents:
- [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901)
- [Viewing a Node Pool](https://intl.cloud.tencent.com/document/product/457/35902)
- [Adjusting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35903)
- [Deleting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35904)


<style>
	.params{margin:0px !important}
</style>
