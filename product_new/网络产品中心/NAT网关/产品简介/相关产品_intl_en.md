This document describes the network products related to NAT Gateway.
## EIP
The NAT gateway and the EIP are two ways for the CVM to access the Internet. You can use either or both of them to formulate your public network access architecture.
### Method 1: Using the NAT Gateway Only
In this method, the CVM is not bound to any EIP. The traffic for accessing the Internet is forwarded to the NAT gateway via the private network and is not subject to the maximum public network bandwidth that you specified when purchasing the CVM. In addition, the traffic fee generated from the NAT gateway is excluded from the billing of the public network bandwidth egress of the CVM.

### Method 2: Using the EIP Only
In this method, the CVM instance is solely bound with an ElP but does not use a NAT gateway. In this case, all the traffic of the instance accessing the Internet flows out through the EIP and is subject to the maximum public network bandwidth that you specified when purchasing the instance. The fee for accessing the Internet is charged based on the billing method of the network where the instance resides.

### Method 3: Using Both the NAT Gateway and EIP
In this method, the CVM is bound to an EIP. Meanwhile, all traffic from the subnet route accessing the Internet is directed to the NAT gateway.
- All traffic from the CVM accessing the Internet **can only be forwarded to the NAT gateway through the private network**, and the returning packets will also be returned to the CVM through the NAT gateway. This traffic will is not subject to the maximum public network bandwidth that you specified when purchasing the CVM, nor will the traffic fee generated from the NAT gateway be included into the billing of the public bandwidth egress of the CVM.
- If the traffic from the Internet actively accesses the EIP of the CVM, the returning packets of the CVM will be uniformly returned through the EIP. The resulting outbound traffic of the public network will be subject to the maximum public network bandwidth that you specified when purchasing the CVM. The fee for accessing the Internet is charged based on the billing method of the network where the CMV instance resides.

> **Note:**
> If the bandwidth package (BWP) feature is enabled for your account, the fee of the outbound traffic generated from the NAT gateway will be deducted from the BWP. This means that the network traffic will not be repeatedly billed. We recommend that you limit the outbound bandwidth of the NAT gateway to avoid a high BWP fee due to excessive outbound bandwidth usage.

For more information about the EIP, see [EIP Overview](https://cloud.tencent.com/document/product/215/11143).

## Other Products
For information about related products, see the table below:

| Product Name | Relationship with NAT Gateway |
|---------|---------|
| [CVM](https://intl.cloud.tencent.com/document/product/213/495) | The NAT gateway and the EIP are two ways for the CVM to access the Internet. |
| [EIP](https://cloud.tencent.com/document/product/215/11143) | The EIP and the NAT gateway are two ways for the CVM to access the Internet. |
| [VPC](https://cloud.tencent.com/document/product/215/535) | NAT Gateway is a sub-product of VPC. |
| [Route Table](https://cloud.tencent.com/document/product/215/4954) | After creating a NAT gateway, you need to configure routing rules to direct the subnet traffic to the NAT gateway. |
| [Public Gateway](https://cloud.tencent.com/document/product/215/11119) | A public gateway is a CVM with forwarding enabled and can be accessed by NAT. |
| [Anti-DDoS Pro](https://cloud.tencent.com/document/product/297/15344) | Bind Anti-DDoS Pro to the NAT gateway for DDoS and CC protection. |
| [Network ACL](https://cloud.tencent.com/document/product/215/5132) | After the network ACL is bound to the subnet where the backend CVM resides, the inbound and outbound traffic of subnets can be precisely controlled. |

