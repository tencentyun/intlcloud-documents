This document describes the network products related to NAT gateways.

## EIP

The NAT gateway and EIP are two ways for the CVM to access the Internet. You can use either one of them or both of them to design your public network access architecture.

### Method 1: Use NAT gateway only

The CVM is not bound to any EIP. The traffic for accessing the Internet is forwarded to the NAT gateway via the private network and is not subject to the upper limit of the public network bandwidth specified when you purchased the CVM. And the traffic generated from the NAT gateway does not occupy the public network bandwidth egress of the CVM.

### Method 2: Use EIP only

The CVM is only bound to an EIP, and does not use the NAT gateway. All the traffic of the CVM accessing the Internet flows via the EIP and is subject to the upper limit of the public network bandwidth specified when you purchased the CVM. The cost resulting from accessing the public network will be charged based on the network billing mode of the CVM.

### Method 3: Use both NAT gateway and EIP

The CVM is bound to an EIP. Meanwhile all traffic from the subnet route accessing the Internet is directed to the NAT gateway.

- All traffic from the CVM actively accessing the Internet **can only be forwarded to the NAT gateway through the private network**, and the returning packets will be returned to the CVM through the NAT gateway as well. This traffic will not be subject to the upper limit of the public network bandwidth specified when the CVM was purchased, nor will the traffic generated at the NAT gateway occupy the public bandwidth egress of the CVM.
- If the traffic from the Internet actively accesses the EIP of the CVM, the returning packets of the CVM will be uniformly returned through the EIP. The resulting outbound traffic of the public network will be subject to the upper limit of the public network bandwidth specified when the CVM was purchased. The cost resulting from accessing the public network will be charged based on the network billing mode of the CVM.

> **Note:**
>For accounts with a bandwidth package for bandwidth sharing, the fee for the outbound traffic from the NAT gateway is covered by the bandwidth package (the network traffic fee is not charged additionally). It is recommended that you set a limit on the outbound bandwidth of the NAT gateway to avoid high bandwidth package fees due to excessive use of the outbound bandwidth of the NAT gateway.



## Other Products

For information on relevant products, see the table below:

| Product Name | Relationship with NAT Gateway |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [CVM](/document/product/213/495) | The NAT gateway and EIP are two ways for the CVM to access the Internet |
| [VPC](/document/product/215/535) | The NAT gateway is a sub-product of the VPC |
| [Route Table](/document/product/215/4954) | After creating a NAT gateway, you need to configure the routing rules to direct the subnet traffic to the NAT gateway |
| [Public Gateway](/document/product/215/11119) | The public gateway is a CVM on which the forwarding feature is enabled, and supports NAT connections |
| [Dayu Anti DDoS Pro](/document/product/297/15344) | Bind the Dayu Anti-DDoS Pro service pack to the NAT gateway for DDoS and CC protection |
| [Network ACL](/document/product/215/5132) | After the network ACL is bound to the subnet in which the backend CVM resides, the inbound and outbound traffic of subnets can be accurately controlled |
