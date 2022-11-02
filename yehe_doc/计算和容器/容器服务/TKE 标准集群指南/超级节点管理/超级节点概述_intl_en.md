
## Super Node Overview
A super node is a brand new node form of Tencent Cloud that provides AZ-level node capabilities with custom specifications. Using a super node is like using a large-capacity CVM instance, which simplifies resource management and scaling. Super nodes are **pay-as-you-go**.
- In pay-as-you-go mode, you don't need to specify node specifications, and node resources are elastic and billed by CPU and memory usage. This mode applies to elastic computing power scenarios, where pay-as-you-go super nodes can be added to support resource elasticity during peak hours, so as to further reduce cluster resource costs.

Pods deployed on super nodes have the same security isolation as CVM instances and the same network isolation and connectivity as Pods deployed on existing general nodes in the cluster.

## Benefits

Super nodes have the following advantages over general nodes:

### Reduced costs

Pay-as-you-go super nodes feature elasticity within seconds and on-demand use, making them quite competitive for cost reduction in elastic business scenarios.

- On-demand use reduces the cluster resource buffer. Pay-as-you-go super nodes are truly used on demand to avoid fragmented resources and increase the overall resource utilization. With a reduced resource buffer, costs are lowered.
- The billable usage of elastic resources is shortened to save costs. As pay-as-you-go super nodes are scaled out within seconds and scaled in instantaneously, scaling costs are greatly reduced.

### Easy management

In the past, multiple nodes needed to be maintained and managed in an AZ, but now only one node needs to be managed in an AZ, facilitating resource management. With pay-as-you-go super nodes, elastic resources deliver higher efficiency than general node pools and scaling groups. Elasticity requirements can be better met, while costs are reduced.

**Node management comparison:**

| **Scenario** | **General Node**                                   | **Super Node**                                                 |
| -------- | ---------------------------------------------- | ------------------------------------------------------------ |
| Purchase     | Node types, specifications, and quantities need to be planned and purchased multiple times. | Only the total resource specifications in an AZ need to be collected, and only one super node with custom specifications needs to be purchased.      |
| Resource scale-out | Nodes need to be added or node specifications need to be batch adjusted.         | <li>Long-term scale-out: Super node configurations are upgraded, and the total specifications are adjusted.</li><li>Short-term scale-out: Pay-as-you-go super nodes are used, and elastic resources are scheduled to them by default.</li> |
| Resource scale-in | Nodes need to be returned, and losses need to be borne.                         |<li>Long-term scale-in: Super node configurations are downgraded, and the total specifications are adjusted. The downgrade can be performed once a month, and the configurations of three super nodes can be downgraded.</li><li>Short-term scale-in: No action is required for pay-as-you-go super nodes.</li>  |
| Node management | Multiple nodes need to be managed.                                 | Only one node needs to be managed in an AZ.                                 |

### More efficient elasticity

Compared with node pools and scaling groups, pay-as-you-go super nodes simplify server purchase, initialization, and returning during scaling processes. This greatly accelerates elasticity and minimizes possible scaling failures.

- Pay-as-you-go super nodes shorten the general scaling process of 4–6 minutes to seconds, greatly increasing the efficiency.
- Pay-as-you-go super nodes avoid the CA, cordoning, and Pod draining processes, truly implementing lossless and instantaneous scale-in.

## Billing Mode

Super nodes are pay-as-you-go.

| Instance Billing Mode |  Pay-as-You-Go                                                     |
| :----------- | :----------------------------------------------------------- |
| Payment mode     |  [Fees are frozen](https://intl.cloud.tencent.com/document/product/555/12039) upon purchase and settled hourly |
| Billing unit     | USD/second                                                        |
| Unit price         | High                                                     |
| Minimum usage duration | The service is billed by second and settled hourly. You can purchase or release the service at any time                       |
| Configuration adjustment     |  There are no specification limits                                                   |
| Application scenario     | It is suitable for scenarios where the demand for computing power fluctuates greatly                           |

Note:
- Adding pay-as-you-go super nodes is free of charge, and fees will be charged after Pods are scheduled to super nodes. The backend will calculate the fees based on the CPU, GPU, and memory resources requested by workloads and the execution duration of workloads. You don't need to pay any fees in advance.

## Kubernetes Version
- Pay-as-you-go super nodes are supported by clusters on v1.16 or later.

## Pods Schedulable to Super Nodes
- 0.25C–16C Pods are supported.
- Pods with a CPU to memory ratio of up to 1:8 are supported.
- GPU Pods are supported.

For more information, see [Notes on Pod Scheduled to Supernodes](https://intl.cloud.tencent.com/document/product/457/39760).


## Scheduling to Super Nodes

When node resources are sufficient, TKE clusters with pay-as-you-go super nodes will preferably release Pods on those super nodes. In addition, Pods can be manually scheduled to super nodes.

For more information, see [How to Schedule a Pod to a Supernodes](https://intl.cloud.tencent.com/document/product/457/45561).

## Applications

The pay-as-you-go billing mode of super nodes is suitable for elastic scenarios.

### Pay-as-you-go super nodes for elastic businesses 
**Strengths**: Low costs and high elasticity

In elastic business scenarios, pay-as-you-go super nodes allow for scale-out within seconds to accommodate traffic surges and require less resource buffer to reduce costs.
High elasticity: Scale-outs are performed within seconds to accommodate traffic surges. Pods are automatically terminated when business traffic drops, implementing lossless scale-in.
Low costs: The reserved cluster buffer is reduced, making the utilization and reservation of cluster node resources more reasonable while reducing costs.

