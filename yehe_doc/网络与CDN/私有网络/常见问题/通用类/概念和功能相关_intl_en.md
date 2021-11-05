### How do you establish communication between different subnets of a VPC?
- Each VPC has private network interconnections by default, and you can see a default route in the corresponding route table. This route indicates that all resources in this VPC can connect with each other by private network.
- Subnets in different VPCs cannot interconnect over the private network and can communicate with each other only by using [Peering Connections](https://intl.cloud.tencent.com/zh/document/product/553) or [CCN](https://intl.cloud.tencent.com/zh/document/product/1003).

### Can different CVMs be deployed in different availability zones in the same VPC?
Yes. A VPC has a region attribute (such as Guangzhou, Beijing, or Seoul), and the subnets in the VPC have an availability zone attribute (such as Guangzhou Zone 1 or Guangzhou Zone 2), so subnets in the same VPC can be deployed in different availability zones in the same region. The availability zone attribute of a CVM inherits that of the subnet it belongs to, and CVMs are purchased under subnets in availability zones. Therefore, it is possible for different CVMs to be deployed in different availability zones.

### How do you establish communication between CVMs and databases in different availability zones?
- Same VPC: there is interconnection by default. If they do not connect, you can give priority to troubleshooting the firewall policies of the [security group](https://intl.cloud.tencent.com/document/product/215/38750) and the [network ACL](https://intl.cloud.tencent.com/document/product/215/31850) .
- Different VPCs: you can use [Peering Connections](https://intl.cloud.tencent.com/zh/document/product/553) or [CCN](https://intl.cloud.tencent.com/zh/document/product/1003) to implement interconnection over the private network between two VPCs.

### How many private IP addresses can each VPC provide for Tencent Cloud service instances?
Each VPC can provide up to 65,533 private IP addresses for Tencent Cloud service instances.

### What is CIDR?
Classless Inter-Domain Routing (CIDR) implements overall division of the network by using the independent network space address block designated by you together with IP and mask. It eliminates the traditional concepts of class A, class B, and class C address ranges and subnetting and allocates IP address space more effectively. When creating a VPC and subnet, you need to create the corresponding IP range in the form of CIDR block. For example, to create an IP range of `10.0.16.0 - 10.0.17.255`, then:
Convert `10.0.16.0 - 10.0.17.255` to the binary format `00001010.00000000.00010000.00000000 - 00001010.00000000.00010001.11111111`, with the first 23 bits being the same. The CIDR block format after conversion is `10.0.16.0/23`.


### Why can't I delete the VPC and subnet after manually terminating a TencentDB for Redis instance?
If there is only one TencentDB for Redis instance in the VPC, after the instance is manually terminated, it will be moved to the TencentDB recycle bin. At this time, the Redis resources have not really been released, so the VPC cannot be deleted immediately. You can solve this problem in the following ways:
+ In the TencentDB recycle bin, **eliminate** the TencentDB for Redis instance and then delete the VPC and subnet.
+ Wait for the TencentDB for Redis instance to automatically expire in the TencentDB recycle bin and then delete the VPC and subnet.
For more information, please see [Terminating Instance](https://intl.cloud.tencent.com/document/product/239/31937).


### Why does an application for an EIP fail?
When the EIP quota is exceeded, the application for EIP will fail. For more information on how to view the quota details, please see [EIP quota limit]().
