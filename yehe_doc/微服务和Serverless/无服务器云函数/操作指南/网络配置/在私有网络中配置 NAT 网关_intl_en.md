## Operation Scenarios
* A function deployed in a VPC is isolated from the public network by default. If you want the function to have access to both private network and public network, you can add a NAT gateway to the VPC.



## Prerequisites
You have [created a function](https://intl.cloud.tencent.com/document/product/583/32742).

## Directions
## Creating NAT Gateway
NAT Gateway is a network cloud service that supports IP address translation and enables high-performance internet access for resources in Tencent Cloud. It can translate the private IP address in a VPC to a public IP address if the private and public networks are isolated from each other, enabling the VPC to access the internet. For more information, please see [NAT Gateway Overview](https://intl.cloud.tencent.com/document/product/1015/30226).

1. Log in to the [NAT Gateway Console](https://console.cloud.tencent.com/vpc/nat) and click **+ Create**.
2. Enter relevant information on the pop-up page. This document creates an NAT gateway as shown below:
>
> - The NAT gateway should be deployed in the same region as the function and VPC.
> - The network to which the NAT gateway belongs should be the VPC where the function is located.
> 
![](https://main.qcloudimg.com/raw/9162ede4dd44107b6f10014259c05a17.png)

## Creating Routing Policy 
Select **[Route Table](https://console.cloud.tencent.com/vpc/route)** on the left sidebar in the VPC Console, select the region where the route table is located, and click **+ Create** as shown below:
![](https://main.qcloudimg.com/raw/4c3cc4c6b5336699dc1141cbbc980cf8.png)
On the pop-up page, you can choose the corresponding configuration in the following two setting methods to manage the SCF access to the public network.

### Enabling SCF to access all public IP addresses
If you want SCF to have access to all public IP addresses, you can configure `IP:0.0.0.0/0` in the destination in the routing table and associate the routing table with the created NAT gateway and SCF subnet as shown below:
![](https://main.qcloudimg.com/raw/337f8d6e7f9396ed3d9de86822db3932.png)

### Enabling SCF to access certain public IP addresses
If you want SCF to have access to certain public IP addresses, you need to add the accessible IP addresses to the routing table and associate the routing table with the created NAT gateway and SCF subnet as shown below:
![](https://main.qcloudimg.com/raw/f28904a4c9e94719733c954cd935cf82.png)
After completing the selection, click **Create**.
