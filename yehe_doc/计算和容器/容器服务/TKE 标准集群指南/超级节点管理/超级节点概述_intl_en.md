## Overview

A super node is not an actual node, but a kind of scheduling capability based on the native K8s. It supports scheduling the Pods in a standard Kubernetes cluster to a super node that does not occupy the cluster server resource. In the TKE cluster that has enabled the super node feature, the Pods that meet the scheduling conditions will be scheduled to the super node maintained by [Elastic Kubernetes Service](https://intl.cloud.tencent.com/document/product/457/34040).

Pods deployed on the super nodes have the same security isolation as CVM, and have the same network isolation and network connectivity as Pods deployed on existing nodes in the cluster, as shown in the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/c0860c9bad76f589e02820564d4f37ad.png)


## Concepts

#### Elastic container

If a cluster has deployed a super node, the Pods scheduled to the super node are the elastic containers, which do not occupy the node resources of cluster server, nor is it restricted by the upper limit of server node resources.


#### Node pool

To help you efficiently manage nodes in a Kubernetes cluster, TKE introduced the concept of node pool. Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in or out.


## Benefits

#### Making elasticity faster and more efficient
With compared to node pool and scaling group, scaling out and in process for super nodes simplifies server purchase, initialization and returning. This improves the speed of elasticity greatly, reduces possible failures in scaling out to the largest extent, and makes elasticity more efficient.
- The scaling out process of super node is in seconds.
![](https://qcloudimg.tencent-cloud.cn/raw/44a63e4d52d5715ab27daf0efa56daea.png)


- The scaling in process of super node is short. It can scale in instantaneously with non-stop service.
![](https://qcloudimg.tencent-cloud.cn/raw/2ee65b1450485c3d1d1f2e16967bfb51.png)

#### Cost saving
Super nodes have the advantages of second-level elasticity and serverless, on-demand product form, which makes them have a great advantage in terms of costs.
- Use on demand to reduce the cluster resource buffer. Because the specifications of the Pods scheduled to real nodes cannot completely match the node specifications, there will always be some fragmented resources that cannot be used but are still billed. Super nodes are used on demand to avoid the generation of fragmented resources, therefore, it can improve the resource utilization of the overall cluster, reduce buffer and save costs.

- Reduce the billing duration of elastic resources and save costs. Because the super node is scaling out in seconds and scaling in instantaneously, it will greatly reduce the costs in scaling.

## Billing

Fees are not charged for super nodes, but charged based on the Pod resources scheduled to the super nodes.

Elastic container on the super node is a pay-as-you-go service. The fees are calculated based on the configured amount of resources and the actual period of using them. Fees will be calculated based on the specifications of the CPU, GPU, and memory for a workload and the running time of the workload. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055).

## Notes on scheduling

Generally, a cluster with super node enabled will automatically scale out Pods to a super node when the server node resources are insufficient, and scale in the Pods on the super node first when the server node resources are sufficient. You can also schedule the Pods to a super node manually. For details, please see [Notes on Scheduling Pod to Super Node](https://intl.cloud.tencent.com/document/product/457/39760).


## Operations

#### Scaling out in seconds to deal with burst traffic easily
For irregular burst traffic, it is difficult to guarantee timely node scaling. If resource specifications are configured with high traffic as a baseline, only a small portion of resources will be used when the traffic is stable, which is a serious waste of resources. It is recommended to configure super nodes without additional preset resources to deal with burst traffic.

- High elasticity: scale out in seconds, and deal with burst traffic easily. It will automatically terminate the Pods when service traffic drops. Scale in with non-stop service.
- Low costs: avoid resources idling costs and improve utilization of resources.

#### Reducing the cluster resource buffer for long-term running service peaks

For long-term running applications with tidal resource loads, super nodes can quickly deploy a large number of Pods without occupying cluster server node resources. When the Pods need to scale out at the service peak, they will be automatically scheduled to the nodes first, consuming the reserved node resources, and then be scheduled to the super nodes to supply more temporary resources to the cluster. These resources will be automatically returned as the Pods scale in.

- High elasticity: scale out in seconds, automatically terminate Pods when service traffic drops, and scale in with non-stop service.
- Low costs: you can reduce the reserved cluster buffer, make the usage and reservation of cluster node resources more reasonable, improve the resource utilization, and reduce costs.


#### Replacing node scaling for short-term running tasks
For tasks that run in a short term and have high resource demands, it is generally necessary to manually scale out a large number of nodes to ensure resources, then schedule the Pods, and return the server after the task is completed. Node resources have buffer, which causes a waste of resource. It is recommended to use super nodes and schedule Pods to super nodes manually without the need of node management.

- No node scaling is required: No need to scale out and in the cluster nodes before and after deployment of these loads, which reduces the time period and maintenance cost of nodes scaling. When the task is completed and the Pod exits, resources will be returned automatically and billing will be stopped. No need for human or program intervention.
- Use on demand to reduce cost: creating Pods based on resources required to avoid resource buffer.

