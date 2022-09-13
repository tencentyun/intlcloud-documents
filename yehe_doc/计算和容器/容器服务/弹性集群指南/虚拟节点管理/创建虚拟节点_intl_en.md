

## Introduction on Super Node 

A super node is a scheduling capability provided by an elastic cluster. When an elastic cluster is created, a super node is created in each subnet where the container network is located.

You can create a super node in the following use cases:

- When you run a large scale of Workloads in an elastic cluster, a Pod cannot be created due to the exhaustion of IP resources of the subnet in the AZ where the service is located. We recommend you create super nodes in a new subnet to obtain more IP resources.
- As service scale expands, services need to be automatically broken down and distributed in multiple AZs. We recommend you create super nodes in a new subnet to expand the resource AZ.
- When you create a Workload, Pod pending will be caused by resource shortage in the AZ. This may be reflected in the following cluster events:
```
EVENT REASON : "FailedCreatePodSandBox"

EVENT MESSAGE : "Failed to create pod sandbox in underlay (will retry): insufficient resource"
```
  You can create super nodes associated with other AZs to expand the available resources in the cluster.



## Billing Mode

Super nodes are not billed, and fees will be charged based on the CPU, GPU, and memory applied for a workload as well as the workload running time. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).



## Overview

This document describes how to create super nodes in an elastic cluster in the TKE console.


## Prerequisites

- Make sure that an elastic cluster has been created.
- You have read [Notes on Pod Scheduled to Super Node](https://intl.cloud.tencent.com/document/product/457/39760).



## Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Elastic Container** > **Elastic Cluster** in the left sidebar.
2. On the **Elastic cluster** list page, click the target cluster ID to enter the **Deployment** page.
3. Click **Super node** in the left sidebar to enter the super node list page.
4. Click **Create node**. In the **Create super node** pop-up window, set the fields as instructed below.
 - **Container network**: Specify the network allocated when Pods are scheduled to a super node. The Pods scheduled to the super node are on the same VPC as Tencent Cloud services such as CVM and TencentDB. Each Pod will occupy an IP address of the VPC subnet. You can select any subnet of the VPC where the elastic cluster is located, as long as it has sufficient IP addresses to meet your needs.
5. Click **OK**.



## Related Operations

After a super node is created, see [Managing a Super Node](https://intl.cloud.tencent.com/document/product/457/41743) for other operations.



