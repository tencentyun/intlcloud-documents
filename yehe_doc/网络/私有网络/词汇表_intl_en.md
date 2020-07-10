## C

### CIDR

See [CIDR](https://intl.cloud.tencent.com/document/product/215/4925)

## E

### EIP

See [Elastic IP]https://intl.cloud.tencent.com/document/product/215/4925.

## G

### Public IP

A public IP is an IP address that instances use to access the Internet or other Tencent Cloud resources (such as database resources) with public endpoints.

### Public gateway

A public gateway is a CVM that forwards the traffic between the Internet and VPCs. A CVM without a public IP can access the Internet via a public gateway.

## J

### Classic network

The classic network is the resource pool of public networks for all users on Tencent Cloud. CVMs in the classic network are assigned uniform private IP addresses by Tencent Cloud. The simple configuration and ease of use make it the right choice for users who have high usability requirements and need to get started with the CVM quickly. By contrast, VPCs are more suitable for users with network management capabilities and demands.
For more information, see [Communicating with Classic Network](https://intl.cloud.tencent.com/document/product/215/35505).

## K

## Availability zone

An availability zone is a physical IDC of Tencent Cloud with an independent power supply and network in a single region. The availability zone is designed to insulate from failures in other availability zones and maintain your businesses always online.

## N

### Private IP

A private IP is an IP address that is assigned to an instance for communication in a Tencent Cloud VPC or between the classic network instances but cannot be accessed via Internet.

## S

### VPC

A virtual private cloud closely resembles a traditional network hosted in your IDC that allows you to build an independent network space on Tencent Cloud to host your Tencent Cloud resources, including [CVMs](https://intl.cloud.tencent.com/document/product/213), [Cloud Load Balancers](https://intl.cloud.tencent.com/document/product/214), and [Database TencentDB](https://intl.cloud.tencent.com/document/product/236). You no longer have to worry about the purchase and OPS of network devices, so you only need to concentrate on selecting your own IP ranges, IP addresses, routing policies, etc. You can access the Internet easily via [EIP](https://intl.cloud.tencent.com/document/product/213/16586), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) and [public gateway](https://intl.cloud.tencent.com/document/product/213/34835), and connect VPC with your IDCs via [VPN](https://intl.cloud.tencent.com/document/product/1037)/[Direct Connect](https://intl.cloud.tencent.com/document/product/216). Also, Tencent Cloud VPC [peering connection](https://intl.cloud.tencent.com/document/product/553) can help you achieve "one server covering the globe" and "2-region-3-DC" disaster recovery. In addition, the security group and [network ACL](https://intl.cloud.tencent.com/document/product/215/31850) on Tencent Cloud VPC can meet your diversified network security requirements comprehensively.

## T

### EIP

An elastic IP is a public IP address that can be applied for independently. It supports dynamic binding and unbinding. You can bind it to or unbind it from the CVM (or NAT Gateway instance) under your account:

1. To retain an IP. ICP domain name filing is required for a Chinese IP and DNS.
2. To shield off instance failures. For example, a DNS name is mapped to an IP address through dynamic DNS mapping. It may take up to 24 hours to propagate this mapping to the entire Internet, while elastic IP enables the drift of an IP from one CVM to another. In case of a CVM failure, all you need to do is start another instance and remap it, thus responding rapidly to the instance failure.

## V

### VPC

- See [VPC](https://intl.cloud.tencent.com/document/product/215/4925)

## W

### CIDR

The Classless Inter-Domain Routing is a user-specified independent network space address block that combines IP with mask to achieve the overall division of the network. Taking `10.1.0.0/16` as an example, `10.1.0.0` is the IP address of the network block, and `16` is the mask of the network block. You can resize the network block by setting the length of mask. The number of IPs that the network block contains equals 2 ^ (32-mask), so the `10.1.0.0/16` network block contains up to 65,536 IP addresses.