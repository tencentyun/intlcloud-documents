## Overview
Elastic Kubernetes Service (EKS) allows you to enable services in a cluster to access internet by configuring the [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) and [route table](https://intl.cloud.tencent.com/document/product/215/31810). This document guides you through the configuration.

## Directions

[](id:createNAT)

### Creating an NAT gateway
1. Log in to the Tencent Cloud VPC console and click **[NAT Gateway](https://console.cloud.tencent.com/vpc/nat)** on the left sidebar.
2. On the **NAT Gateway** page, click **+Create**.
3. In the pop-up **Create NAT Gateway** window, create an NAT gateway in the same region and same VPC as the EKS cluster. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).

[](id:createRouting)

### Creating a route table for the NAT gateway

1. On the left sidebar, click **[Route Table](https://console.cloud.tencent.com/vpc/route)** to go to the **Route Table** management page.
2. On the **Route Table** management page, click **+Create**.
3. In the pop-up **Create Route Table** window, create a route table in the same region and same VPC as the EKS cluster, as shown in the figure below:
![](https://main.qcloudimg.com/raw/927234784ea77fba3d1f1ce0de322a5f.png)
Main parameters are described as follows:
 - **Destination**: select the public IP address to be accessed. You can configure a CIDR block for this parameter. For example, if you enter `0.0.0.0/0`, all traffic will be forwarded to the NAT gateway.
 - **Next Hop Type**: select **NAT Gateway**.
 - **Next Hop**: select the NAT gateway created in [Creating an NAT Gateway](#createNAT).
4. Click **Create**.

### Associating subnets with the route table
After configuring routes, you need to select subnets and associate them with the route table. Then, traffic from the selected subnets to internet will be routed to the NAT gateway.
1. On the **Route Table** page, find the route table created in the [Creating a route table for the NAT gateway](#createRouting) step and click **Associate Subnets** on the right.
2. In the pop-up **Associate Subnets** window, select the subnets to be associated and click **OK**.
<dx-alert infotype="explain" title="">
This subnet is not a Service CIDR block but a container network.
</dx-alert>
After associating the route table with the subnets, resources in the same VPC can access internet through the public IP address of the NAT gateway.

## Configuration Verification
1. On the **Elastic Cluster** list page, click the ID of the target cluster to go to the management page of the cluster.
2. Click **Remote Login** for the target container and run a ping command to check whether its pods can access internet. If the results in the figure below are returned, it means the pods have successfully accessed the internet.
![](https://main.qcloudimg.com/raw/35fec47afacbe6d9407f61be565bbb24.png)
