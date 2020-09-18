## Introduction

>The node pool feature is currently in beta. To join the beta test, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


To help you better manage nodes in a Kubernetes cluster, TKE introduced the concept of a node pool. Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in and out.
- When a Pod in the cluster cannot be scheduled due to insufficient resources, scale-out will be triggered automatically, reducing labor costs.
- When a scale-in condition is met, such as when a node is idle, scale-in will be triggered automatically, reducing resource costs.

The following figure shows the overall architecture of a node pool.
![](https://main.qcloudimg.com/raw/ee033cab974b375a1e59fb5a96aaa503.png)

Generally, all nodes in a node pool share the following attributes:
- Node operating system
- Launch parameters of Kubernetes components for nodes
- Custom launch script for nodes
- Kubernetes Label and Taints settings for nodes

In addition, TKE extends the following attributes for a node pool:
- Node pool-level operating system
- Maximum number of Pods for each node in a specific node pool

## Use Cases
When you need to use a large-scale cluster, we recommend that you use a node pool to manage nodes to improve the usability of the large-scale cluster. The following table describes multiple use cases for managing large-scale clusters and shows the effect of node pools in each use case.

| Use Case | Effect |
| ---- | ---- |
| A cluster includes many heterogeneous nodes with different model configurations. | A node pool allows you to manage the nodes by groups in a unified manner. |
| A cluster needs to frequently scale nodes in and out. | A node pool reduces operating costs. |
| The scheduling rules for applications in a cluster are complex. | Node pool labels allow you to quickly specify service scheduling rules. |
| Routine maintenance is required for nodes in a cluster. | A node pool allows you to conveniently upgrade the Kubernetes version and the Docker version. |


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
<td>Create</td>
<td>Add a node pool</td>
<td>We recommend that you do not create more than 20 node pools for a single cluster.</td>
</tr>
<tr>
<td>Delete</td>
<td><ul class="params"><li>When you delete a node pool, you can select whether to terminate nodes in the node pool. </li><li>Retained nodes do not belong to any scaling group or node pool.</li></ul></td>
<td>When you delete a node pool, if you select to terminate nodes, the nodes will not be retained. You can create new nodes later if required.</td>
</tr>
<tr>
<td>Enable auto scaling</td>
<td>When auto scaling is enabled for a node pool, the number of nodes in the node pool is automatically adjusted according to the workload of the cluster.</td>
<td rowspan=2>Do not enable or disable auto scaling in the Scaling Group console.</td>
</tr>
<tr>
<td>Disable auto scaling</td>
<td>When auto scaling is disabled for a node pool, the number of nodes in the node pool is not automatically adjusted according to the workload of the cluster.</td>
</tr>
<tr>
<td>Adjust node pool size</td>
<td>You can directly adjust the number of nodes in a node pool. If you decrease the number of nodes, a random node in a scaling group will be removed. </td>
<td>It’s not recommended to manually adjust the size of a node pool when auto scaling is enabled.</td>
</tr>
<tr>
<td>Adjust node pool configurations</td>
<td>You can modify the node pool name, the number range of nodes in a scaling group, and the Kubernetes Label and Taints attributes for nodes in the node pool.</td>
<td>Modifications of the Label and Taints attributes take effect for all the nodes in a node pool and may cause Pods to be rescheduled.</td>
</tr>
<tr>
<td>Add an existing node</td>
<td>You can add a non-clustered Pod to a node pool if the following requirements are met:<ul class="params"><li>The Pod and the cluster belong to the same VPC.</li><li>The Pod is not used by other clusters and has the same model and billing mode configurations as the node pool.</li></ul>You can also add a node-without-pool to a node pool if the Pods in the node have the same model and billing mode configurations as the node pool.</td>
<td>In normal cases, we recommend that you directly create a node pool instead of adding an existing node to a node pool.</td>
</tr>
<tr>
<td>Remove a node</td>
<td>You can remove a manually added node from a node pool and retain the t in the cluster. Nodes cannot be directly removed from a scaling group.</td>
<td>We recommend that you add or remove nodes in a node pool by adjusting the size of the node pool.</td>
</tr>
<tr>
<td>Convert a scaling group into a node pool</td>
<td><ul class="params"><li>You can convert an existing scaling group into a node pool. After conversion, the node pool fully inherits the features of the original scaling group and the information about the scaling group will not be displayed.</li><li>After all existing scaling groups in a cluster have been converted into node pools, this feature is disabled.</li></td>
<td>This operation is irreversible. Be sure you understand the features of node pools before conversion.</td>
</tr>
</tbody></table>



## Relevant Operations
You can log in to the [Tencent Kubernetes Engine console](https://console.cloud.tencent.com/tke2) and perform node pool-related operations according to the following documents:
- [Creating a Node Pool](https://intl.cloud.tencent.com/document/product/457/35901)
- [Viewing a Node Pool](https://intl.cloud.tencent.com/document/product/457/35902)
- [Adjusting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35903)
- [Deleting a Node Pool](https://intl.cloud.tencent.com/document/product/457/35904)


<style>
	.params{margin:0px !important}
</style>
