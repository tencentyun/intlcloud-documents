## Overview
This document describes how to manually or automatically scale a cluster to meet the resource requirements of the applications. You can scale a cluster in one of the following ways:
- [Manually adding/removing a node](#ManuallyAddAndRemove)
- [Automatically adding/removing a node via auto scaling](#AutomaticAddAndRemove)
- [Completing scaling of application layer via supernode (without scaling node)](#AddPod)

## Prerequisites

1. You have logged in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. You have [created a cluster](https://intl.cloud.tencent.com/document/product/457/30637).

## Directions

[](id:ManuallyAddAndRemove)
### Manually adding/removing a node
To scale out a cluster, you can manually add a node by creating a node or adding an existing node. To scale in a cluster, you can remove a node.

#### Creating a node
When creating a node, you can configure a new CVM on the **Create Node** page for cluster scale-out.
For details, see [Adding a Node](https://intl.cloud.tencent.com/document/product/457/30652).


#### Adding an existing node
>!
>- Currently, you can only add CVMs in the same VPC.
>- If you choose to add an existing node to the cluster, the operating system of the CVM will be reinstalled according to your settings.
>- If you choose to add an existing node to the cluster, the project of the CVM will be migrated to the project set for the cluster.
>- When adding a node with only one data disk to the cluster, you can choose to set the related parameters of data disk mounting.


When adding a node, you can select and configure the CVM you want to add to the cluster on the **Add Existing Node** page.
For details, see [Adding a Node > Adding an Existing Node](https://intl.cloud.tencent.com/document/product/457/30652).

#### Removing a node
For directions on how to scale in a cluster, see [Removing a Node](https://intl.cloud.tencent.com/document/product/457/30653).

[](id:AutomaticAddAndRemove)

### Automatically adding/removing a node via auto scaling

Auto scaling relies on the community component Cluster Autoscaler (CA), which can dynamically adjust the number of nodes in a cluster to meet your resource requirements. For details on auto scaling, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).

[](id:AddPod)

### Scaling out via supernode

Supernode is a kind of scheduling capability. It supports scheduling the Pods in a standard Kubernetes cluster to a supernode that does not occupy the cluster server resource to implement dynamic scaling out when resources are insufficient. For more information, see [supernode Overview](https://intl.cloud.tencent.com/document/product/457/39759).


## FAQs

For issues related to scaling, see [Auto-scaling Related](https://intl.cloud.tencent.com/document/product/457/31425).
