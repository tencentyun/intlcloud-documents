## Overview
Elastic Kubernetes Service (EKS) allows you to enable services in a cluster to access internet by configuring the [NAT Gateway](https://www.tencentcloud.com/document/product/1015) and [route table](https://intl.cloud.tencent.com/document/product/215/31810). This document guides you through the configuration.

## Directions



### Creating a NAT gateway[](id:createNAT)
1. Log in to the Tencent Cloud VPC console and click [**NAT gateway**](https://console.cloud.tencent.com/vpc/nat) on the left sidebar.
2. On the **NAT gateway** page, click **+ New**.
3. In the **Create a NAT gateway** pop-up window, create a NAT gateway in the same region and same VPC as the TKE serverless cluster. For detailed directions, see [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).

### Creating a route table pointing to the NAT gateway[](id:createRouting)
1. On the left sidebar, click [**Route table**](https://console.cloud.tencent.com/vpc/route) to enter the route table management page.
2. On the route table management page, click **+ New**.
3. In the **Create route table** pop-up window, create a route table in the same region and same VPC as the TKE serverless cluster as shown below:
![](https://main.qcloudimg.com/raw/927234784ea77fba3d1f1ce0de322a5f.png)
The main parameters are described as follows:
 - **Destination**: select the public IP address to be accessed. You can configure a CIDR block for this parameter. For example, if you enter `0.0.0.0/0`, all traffic will be forwarded to the NAT gateway.
 - **Next Hop Type**: select **NAT Gateway**.
 - **Next Hop**: select the NAT gateway created in [Creating a NAT Gateway](#createNAT).
4. Click **Create**.

### Associating subnets with the route table
After configuring routes, you need to select subnets and associate them with the route table. Then, traffic from the selected subnets to internet will be routed to the NAT gateway.
1. On the **Route table** page, click **Associated subnets** on the right of the route table created in [Creating a route table pointing to the NAT gateway](#createRouting).
2. In the **Associated subnets** pop-up window, select the target subnets and click **Confirm**.
<dx-alert infotype="explain" title=" ">
This subnet is not a Service CIDR block but a container network.
</dx-alert>
After associating the route table with the subnets, resources in the same VPC can access internet through the public IP address of the NAT gateway.

## Configuration Verification
1. On the serverless cluster list page, click the ID of the target cluster to enter its management page.
2. Click **Remote Login** on the right of the target container and run a ping command to check whether its Pods can access the internet. If the returned result is as shown below, the Pods have successfully accessed the internet.
![](https://main.qcloudimg.com/raw/35fec47afacbe6d9407f61be565bbb24.png)
