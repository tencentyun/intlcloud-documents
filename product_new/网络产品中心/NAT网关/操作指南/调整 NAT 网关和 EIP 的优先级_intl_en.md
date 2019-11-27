## Description of NAT Gateway and EIP Priorities
When a subnet is associated with a NAT gateway, and the CVM in the subnet has a public IP address (or an EIP), the CVM accesses the Internet through the NAT gateway by default because the priority of the exact match route is higher than that of the public IP address. However, you can set a routing policy to allow the CVM to access the Internet through its public IP address. 

## Directions
1. View the route table associated with the subnet where the CVM resides. Ensure that a routing policy that points to the NAT gateway exists so that CVMs in the subnet that have no public IP addresses can still access the Internet through the NAT gateway.
 ![1](https://main.qcloudimg.com/raw/42fcb4ca21dba69ab24297e0dbe4bd91.png)
2. Add a routing policy with the next hop type set to the public IP of the CVM, and enter the destination.
 - Destination: Enter the specific public network range that your service needs to access or the default route (that is, 0.0.0.0/0, which indicates that the destination is not in the route table and all data packets are transmitted in the default route).
 - Next Hop Type: Public IP address of the CVM.
 
>
>- When the routing policy is configured with the same destination as the routing rules that are directed to the NAT gateway, the CVM, and the public gateway, this route will be matched first.
>- This routing policy affects all subnets associated with the route table, in which case please evaluate the impact of the operation. In other words, CVMs in these subnets that have public IP addresses (or elastic IP addresses) will access the Internet through their respective public IP address instead of the NAT gateway.
>- In the subnet associated with the route table, CVMs that have no public IP addresses can still access the Internet through the NAT gateway without being affected.

 ![2](https://main.qcloudimg.com/raw/8cd639ccf22fbf511c48a72c357e7b76.png)
