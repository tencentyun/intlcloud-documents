

## Introduction of Virtual Node

Virtual node is a scheduling capability provided by the elastic cluster. When an elastic cluster is created, a virtual node is created in each subnet where the container network is located.

When you meet the following scenarios, you can resolve the issues by creating virtual nodes:

- When you run a large scale of workload in an elastic cluster, a Pod cannot be created due to exhaustion of IP resources of the subnet of availability zone where the service is located. It is recommended that you create virtual nodes in the new subnet to increase IP quantities.
- As the scale of services expands, services need to be automatically broken up and distributed in multiple availability zones. It is recommended that you create virtual nodes in the new subnet to expand the resource availability zone.
- When you create workload, Pod pending is caused by resource shortage for availability zone. This may be reflected as the following cluster events:
```
EVENT REASON : “FailedCreatePodSandBox”

EVENT MESSAGE : “Failed to create pod sandbox in underlay (will retry): insufficient resource”
```
  You can create virtual nodes associated with other availability zones to expand available resources for the cluster.



## Billing Mode

Fees are not charged for virtual nodes and the cost will be calculated based on the CPU, GPU, memory value and the running time of the workload. For details, please see [Elastic Clusters Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Elastic Clusters Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Elastic Clusters Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).



## Overview

This document describes how to create virtual nodes in an elastic cluster through TKE console.


## Prerequisites

- Please ensure the elastic cluster has been created.
- You have known [Notes on Scheduling Pod to Virtual Node](https://intl.cloud.tencent.com/zh/document/product/457/39760).



## Operation Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Elastic Container** > **Elastic Cluster** in the left sidebar.
2. On the **Elastic Cluster** page, click the desired cluster ID to open the **Deployment** page.
3. Click **Virtual Node” in the left sidebar to open the list page of virtual nodes.
4. Click **Create Node**. In the **Create Virtual Node** pop-up, refer to the following tips to set. 
 - Container Network: specify the network allocated when the Pod is scheduled to the virtual node. The Pods scheduled to virtual node are on the same VPC network plane as the Tencent Cloud services such as CVM and TencentDB. Each Pod will use an IP address of the VPC subnet. You can select any subnet of the VPC where the elastic cluster is located. Please select a suitable subnet with sufficient available IP addresses based on the actual needs.
5. Click **OK** to complete the creation.



