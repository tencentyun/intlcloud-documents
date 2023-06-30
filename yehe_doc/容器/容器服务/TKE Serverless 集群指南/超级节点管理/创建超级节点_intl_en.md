## Super Node Introduction 

Super nodes are created in TKE Serverless clusters for Pod scheduling. A super node is created in each subnet of the container network when you create a TKE Serverless cluster.

In the following scenarios, you can resolve the issues by creating super nodes:

- When you run a large-scale workload in a TKE Serverless cluster, a Pod cannot be created due to exhaustion of IPs in the subnet of availability zone where the service is located. It is recommended that you create super nodes in a new subnet to have more IPs.
- As the scale of services expands, services need to be automatically distributed in multiple availability zones. It is recommended that you create super nodes in a new subnet to expand availability zones of the resources.
- When you create a workload, Pod pending is caused by resource shortage for the availability zone. This may be reflected as the following cluster events:
```
EVENT REASON : “FailedCreatePodSandBox”

EVENT MESSAGE : “Failed to create pod sandbox in underlay (will retry): insufficient resource”
```
  You can create super nodes in other availability zones to expand resources available in the cluster.



## Billing Overview

Fees are not charged for super nodes and the cost will be calculated based on the CPU, GPU, memory value and the running time of the workload. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/457/34054), [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055), and [Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).



## Overview

This document describes how to create a super node in a TKE Serverless cluster in the TKE console.


## Prerequisites

- You have created a TKE Serverless cluster. For operation details, see [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- You have known [Notes on Pod Scheduled to Super Nodes](https://intl.cloud.tencent.com/document/product/457/39760).



## Directions

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. On the cluster management page, click the ID of the target Serverless cluster to enter the basic information page.
3. Click **Super node** in the left sidebar and click **Create**.
4. On the **Create super node** page, configure the parameters as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/6301a4a22b9aafe021b123bf681ea0ba.png)
 - **Billing mode**: Only pay-as-you-go is available.
 - **Operating system**: Select the operating system type (**Linux** or **Windows**) supported by the subnet. If you select **Windows**, Windows containers can run on the subnet. By default, **Linux** is selected.
 - **Container network**: Specify the network allocated when Pods are scheduled to a super node. The Pods scheduled to the super node are on the same VPC as Tencent Cloud services such as CVM and TencentDB. Each Pod will occupy an IP address of the VPC subnet. You can select any subnet of the VPC where the Serverless cluster is located, as long as it has sufficient IP addresses to meet your needs.
 - **Security group**: The security group works as a firewall to control access to the CVM network. For more information, see [TKE Security Group Settings](https://intl.cloud.tencent.com/document/product/457/9084).
5. Click **Confirm** to complete the process.



## More

After the creation of the super node, please refer to [Managing a Super Node](https://intl.cloud.tencent.com/document/product/457/41743) for subsequent management.




