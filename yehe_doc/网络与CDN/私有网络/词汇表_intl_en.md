## C

### CIDR

See [CIDR](https://intl.cloud.tencent.com/document/product/215/4925).

## E

### EIP

See [Elastic IP](https://intl.cloud.tencent.com/document/product/215/4925).

## G

### Public IP

A public IP can be accessed over the Internet and is used for communication between the instance and the Internet or other Tencent Cloud resources (such as database resources) with public endpoints.

### Public gateway

A public gateway is a CVM that can forward the traffic between the Internet and VPCs. A CVM without a public IP can access the Internet via a public gateway.

## J

### Classic network

The classic network is the public network resource pool for all Tencent Cloud users. Tencent Cloud assigns private IPs to CVMs in the classic network. It features simple configuration and ease of use, making it suitable for users who need high usability and quick start with CVMs. By contrast, VPC is suitable for users with network management capabilities and needs.
For more information, see [Communicating with Classic Network](https://intl.cloud.tencent.com/document/product/215/35505).

## K

## Availability zone

An availability zone is a physical IDC of Tencent Cloud with independent power supply and network in a single region. It can ensure business stability, as failures in one AZ are isolated without affecting other AZs in the same region.

## N

### Private IP

A private IP is an IP address assigned to an instance in a Tencent Cloud VPC or classic network and cannot be accessed via the Internet. It can be used for communication between instances in a VPC or classic networks.

## S

### VPC

VPC builds an isolated network space on Tencent Cloud, which is similar to a traditional network run in your IDCs. VPC hosts your Tencent Cloud resources, including [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213), [Cloud Load Balancers](https://intl.cloud.tencent.com/document/product/214), [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236), etc. Instead of worrying about the purchase and OPS of network devices, you can focus on customizing IP ranges, IP addresses, routing policies, etc. You can access the Internet easily through [EIP](https://intl.cloud.tencent.com/document/product/213/16586), [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015) and [Public Gateway](https://intl.cloud.tencent.com/document/product/213/34835), and connect the VPC with your IDCs through [VPN](https://intl.cloud.tencent.com/document/product/1037)/[Direct Connect](https://intl.cloud.tencent.com/document/product/216). Tencent Cloud VPC [Peering Connection](https://intl.cloud.tencent.com/document/product/553) allows you to implement a unified server for global access and 2-region-3-DC disaster recovery. In addition, the security group and [network ACL](https://intl.cloud.tencent.com/document/product/215/31850) of Tencent Cloud VPC can fully meet your needs for network security.

## T

### EIP

An elastic IP is a public IP address that can be applied for independently. It supports dynamic binding and unbinding. You can bind it to or unbind it from the CVM (or NAT Gateway instances) under your account. Its main uses are:

1. To retain an IP. ICP domain name filing is required for Chinese mainland IP and DNS.
2. To mask an instance failure. For example, a DNS name is mapped to an IP address through dynamic DNS mapping. It may take up to 24 hours to propagate this mapping to the entire Internet, while an elastic IP enables quick remapping of an IP from one CVM to another. When one CVM fails, you can just launch and remap another instance to quickly respond to instance failures.

## V

### VPC

See [VPC](https://intl.cloud.tencent.com/document/product/215/4925).

## W

### CIDR

Classless Inter-Domain Routing is a user-specified independent network space address block. It combines IP and masking to achieve network division. In the `10.1.0.0/16` example, `10.1.0.0` is the IP address of the network block, and `16` is the mask of the network block. You can resize the network block by adjusting the mask size. The number of IPs in a network block equals 2 ^ (32-mask), and the `10.1.0.0/16` network block has at most 65,536 IP addresses.