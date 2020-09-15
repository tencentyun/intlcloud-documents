### How can I establish communication between different subnets of a VPC?
- Each VPC supports private network interconnection by default, and you can find the default route in the corresponding route table. This route indicates that all resources in this VPC can connect with each other over the private network.
- Subnets in different VPC instances are not interconnected over the private network. To interconnect these subnets, establish [peering connection](https://intl.cloud.tencent.com/document/product/553) or use [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003).

### Can CVMs be deployed in different availability zones in the same VPC?
Yes. A VPC is a regional (such as Guangzhou, Beijing, or Seoul) resource, and the subnets in the VPC are resources in availability zones (such as Guangzhou Zone 1 or Guangzhou Zone 2). Therefore, subnets in one VPC can be deployed in different availability zones in the same region. A CVM is also availability zone specific as the subnet it belongs to. So, if you purchase CVMs under subnets in availability zones, you can deploy them in different availability zones.

### How can I establish communication between CVMs and databases in different availability zones?
- In the same VPC: CVMs and databases in the same VPC are interconnected by default. If the interconnection fails, you can first troubleshoot the firewall policies of the security group and the [network ACL](https://intl.cloud.tencent.com/document/product/215/31850).
- In different VPCs: CVMs and databases are isolated by default. If the interconnection is required, you can establish private network interconnection between VPC instances using [peering connection](https://intl.cloud.tencent.com/document/product/553) or [CCN](https://intl.cloud.tencent.com/document/product/1003).

### How many private IP addresses can each VPC provide for Tencent Cloud service instances?
A VPC supports a maximum of 65,533 private IP addresses for Tencent Cloud service instances.

### What is a CIDR block?
Classless Inter-Domain Routing (CIDR) is a user-specified independent network space address block. It combines IP and masking to achieve network division. Without the traditional Class A, B and C IP addresses as well as subnet, it allocates IP address spaces more effectively. To create a VPC and subnet, you need to create IP ranges in CIDR format. In the `10.0.16.0 - 10.0.17.255` example, 
This IP range changes to `00001010.00000000.00010000.00000000 - 00001010.00000000.00010001.11111111` in binary format that has the same first 23 digits, and to `10.0.16.0/23` in CIDR format.

