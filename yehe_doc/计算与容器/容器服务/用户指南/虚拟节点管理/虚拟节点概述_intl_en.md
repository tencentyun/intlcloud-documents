## Overview

A virtual node is not an actual node, but a kind of scheduling capability based on the native K8s. It supports scheduling the Pods in a standard Kubernetes cluster to a virtual node that does not occupy the cluster server resource. In the TKE cluster that has enabled the virtual node feature, the Pods that meet the scheduling conditions will be scheduled to the virtual node maintained by [Elastic Kubernetes Service](https://intl.cloud.tencent.com/document/product/457/34040).

Pods deployed on the virtual nodes have the same security isolation as CVM, and have the same network isolation and network connectivity as Pods deployed on existing nodes in the cluster, as shown in the figure below:
![](https://main.qcloudimg.com/raw/db70da6395fa8bd34bda159b1f097df6.png)



## Concepts

#### Elastic Container

If a cluster has deployed a virtual node, the Pods scheduled to the virtual node are the elastic containers, which do not occupy the node resources of cluster server, nor is it restricted by the upper limit of server node resources.


#### Node pool

To help you efficiently manage nodes in a Kubernetes cluster, TKE introduced the concept of node pool. Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in or out.




## Billing Mode

Elastic container is a pay-as-you-go service. The fees are calculated based on the configured amount of resources and the actual period of using them. Fees will be calculated based on the specifications of the CPU, GPU, and memory for a workload and the running time of the workload. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055).

## Notes on Scheduling

Generally, a cluster with virtual node enabled will automatically scale out Pods to virtual node when the server node resources are insufficient, and scale in the Pods on the virtual node first when the server node resources are sufficient.


## Use Cases

#### Reducing the cluster resource buffer for long-term running service peaks

Virtual node can quickly deploy a large number of Pods without occupying cluster server node resources. It is suitable for long-term running applications with peaks and troughs of resource load.

Using virtual nodes, you can reduce the reserved cluster buffer, make the usage and reservation of cluster node resources more reasonable, and improve the resource utilization.

During the service peaks, Pods will be added to the existing nodes for scaling out. After the reserved resources of the existing nodes are consumed, Pods will be added to the virtual node for scaling out. These resources will be automatically returned as the Pods scaled in.


#### Replacing node scaling for short-term running tasks

The tasks that run in a short time and require a large amount of resources can be manually scheduled to the virtual node. There is no need to scale out or scale in the cluster nodes before and after the deployment of these loads, which saves the time and reduces the maintenance costs.

When deploying these tasks, you can specify the virtual node for scheduling, so that the node resources of other services running in the cluster will not be occupied. When the task ends, the Pod will automatically scaled in, the resources will be returned automatically, and the billing will stop, without manual or program OPS.

