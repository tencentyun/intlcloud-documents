## Overview
TKE Serverless allows services in a cluster to access the internet by configuring the [NAT Gateway](https://www.tencentcloud.com/document/product/1015) and [route table](https://intl.cloud.tencent.com/document/product/215/31810). This document guides you through the configuration.

## Directions



### Creating a NAT gateway[](id:createNAT)
1. Log in to the Tencent Cloud VPC console and click **[NAT Gateway](https://console.cloud.tencent.com/vpc/nat)** in the left sidebar.
2. On the **NAT gateway** page, click **+Create**.
3. In the pop-up **Create NAT gateway** window, create a NAT gateway in the same region and same VPC as the TKE Serverless cluster. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).

### Creating a route table pointing to the NAT gateway[](id:createRouting)
1. On the left sidebar, click **[Route Table](https://console.cloud.tencent.com/vpc/route)** to go to the **Route table** management page.
2. On the **Route table** management page, click **+Create**.
3. In the pop-up **Create route table** window, create a route table in the same region and same VPC as the TKE Serverless cluster.
![](https://main.qcloudimg.com/raw/927234784ea77fba3d1f1ce0de322a5f.png)
The main parameters are described as follows:
 - **Destination**: Select the public IP address to be accessed. You can configure a CIDR block for this parameter. For example, if you enter `0.0.0.0/0`, all traffic will be forwarded to the NAT gateway.
 - **Next hop type**: Select **NAT gateway**.
 - **Next hop**: Select the NAT gateway created in [Creating a NAT gateway](#createNAT).
4. Click **Create**.

### Associating subnets with the route table
After configuring routes, you need to select subnets and associate them with the route table. Then, traffic from the selected subnets to internet will be routed to the NAT gateway.
1. On the **Route table** page, find the route table created in the [Creating a route table for the NAT gateway](#createRouting) step and click **Associate subnets** on the right.
2. In the pop-up **Associate subnets** window, select the subnets to be associated and click **OK**.
<dx-alert infotype="explain" title="">
This subnet is not a Service CIDR block but a container network.
</dx-alert>
After associating the route table with the subnets, resources in the same VPC can access internet through the public IP address of the NAT gateway.

## Configuration Verification
1. On the cluster management page, click the ID of the target Serverless cluster to enter the cluster details page.
2. Click **Remote login** for the target container and run a ping command to check whether its Pods can access the internet. If the results in the figure below are returned, it means the Pods have successfully accessed the internet.
![](https://main.qcloudimg.com/raw/35fec47afacbe6d9407f61be565bbb24.png)

## Notes
The NAT gateway does not automatically adjust the bandwidth of the bound EIP anymore. When the problems (such as image pulling timeout) occur, and the upper limit for bandwidth of the NAT gateway is not reached, you can check the EIP bandwidth and set the upper limit as needed.
