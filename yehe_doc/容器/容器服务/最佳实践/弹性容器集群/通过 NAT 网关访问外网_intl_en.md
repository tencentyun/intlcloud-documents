## Overview
Elastic Kubernetes Service (EKS) allows you to enable services in a cluster to access internet by configuring the [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) and [route table](https://intl.cloud.tencent.com/document/product/215/31810). This document guides you through the configuration.

## Directions
### Checking whether pods can access internet
1. Log in to the TKE console and click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar.
2. On the **Elastic Cluster** list page, click the ID of the target cluster to go to the management page of the cluster.
3. Click **Remote Login** for the target container and run a ping command to check whether its pods can access internet.
If the returned result is as follows, data packets cannot be received, which indicates that the pods cannot access internet.
<img style="width:50%" src="https://main.qcloudimg.com/raw/af87237f0752799e3fdf654aca37a0b7.png"></img>

<span id="createNAT"></span>
### Creating a NAT Gateway
1. Log in to the Tencent Cloud VPC console and click **[NAT Gateway](https://console.cloud.tencent.com/vpc/nat)** in the left sidebar.
2. On the **NAT Gateway** page, click **+Create**.
3. In the **Create NAT Gateway** window that appears, create a NAT Gateway in the same region and same VPC as the EKS cluster. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).
<span id="createRouting"></span>
### Creating a route table for the NAT Gateway
1. In the left sidebar, click **[Route Table](https://console.cloud.tencent.com/vpc/route)** to go to the **Route Table** management page.
2. On the **Route Table** management page, click **+Create**.
3. In the **Create Route Table** window that appears, create a route table in the same region and same VPC as the EKS cluster.
![](https://main.qcloudimg.com/raw/927234784ea77fba3d1f1ce0de322a5f.png)
The main parameters are described as follows:
 - **Destination**: select the public IP address to be accessed. You can configure a CIDR block for this parameter. For example, if you enter `0.0.0.0/0`, all traffic will be forwarded to the NAT Gateway.
 - **Next Hop Type**: select **NAT Gateway**.
 - **Next Hop**: select the NAT Gateway created in [Creating a NAT Gateway](#createNAT).
4. Click **Create**.

### Associating subnets with the route table
After configuring routes, you need to select subnets and associate them with the route table. Then, traffic from the selected subnets to internet will be routed to the NAT Gateway. 
1. On the **Route Table** page, find the route table created in the [Creating a route table for the NAT Gateway](#createRouting) step and click **Associate Subnets** on the right.
2. In the **Associate Subnets** window that appears, select the subnets to be associated and click **OK**.
After associating the route table with the subnets, resources in the same VPC can access internet through the public IP address of the NAT Gateway.

## Configuration Verification
1. On the **Elastic Cluster** list page, click the ID of the target cluster to go to the management page of the cluster.
2. Click **Remote Login** for the target container and run a ping command to check whether its pods can access internet.
If the returned result is as follows, the pods can access internet normally.
<img style="width:50%" src="https://main.qcloudimg.com/raw/d5c4f53e62ca216c7d41d078d16f6f84.png"></img>
