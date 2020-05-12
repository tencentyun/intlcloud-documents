This article describes the network products related to NAT Gateways.
## EIP
The NAT gateway and the EIP are the two ways for a CVM instance to access the public network. You can use either or both of them in your public network access architecture.
### Method 1: Using NAT gateways only
CVM instances use the NAT gateway to access the public network without binding any EIP. Traffic to the public network is forwarded to the NAT gateway via the private network and is not subject to the maximum public network bandwidth that you specified when purchasing the CVM instance. NAT gateway traffic does not use the public network egress of the CVM instance and it is billed separately.

### Method 2: Using EIPs Only
CVM instances use EIPs to access the public network without any NAT gateway. Traffic is limited by the public network bandwidth you specified when purchasing the instance. Charges for such traffic depends on the network billing plan of the instance.

### Method 3: Using NAT Gateways and EIPs
The CVM instance is bound with an EIP, and the routing table directs all traffic from the subnet to the public network to the NAT gateway.
- All traffic from the CVM instance to the public network **uses the NAT gateway through the private network**, and the response packets are returned through the NAT gateway. This traffic is not subject to the public network bandwidth that you specified when purchasing the CVM instance. NAT gateway traffic does not use the public bandwidth egress of the CVM instance.
- Responses to incoming traffic (to the CVM instance) that uses the EIP use the EIP to get on the public network as well. This traffic is affected by the public network bandwidth that you specified when purchasing the CVM instance. The fee for accessing the public network applies and is based on the network billing plan of the CMV instance.

> If you use a bandwidth package (BWP), your NAT gateway traffic is billed as part of the package, which means you are not subjected to the 0.12 USD/GB charge. We recommend that you limit the outbound bandwidth of the NAT gateway to avoid high BWP fees due to excessive outbound bandwidth usage.

For more information about EIPs, see [EIP Overview](https://intl.cloud.tencent.com/document/product/213/16586).

## Other Products
The table below lists products related to the NAT gateway:

| Product Name | How is it related |
|---------|---------|
| [CVM](https://intl.cloud.tencent.com/document/product/213/495) | The NAT gateway and the EIP are two ways for CVM instances to access the Internet. |
| [EIP](https://intl.cloud.tencent.com/document/product/213/16586) | The EIP and the NAT gateway are two ways for CVM instances to access the Internet. |
| [VPC](https://intl.cloud.tencent.com/document/product/215/535) | NAT Gateway is part of the VPC. |
| [Route Table](https://intl.cloud.tencent.com/document/product/215/31810) | After creating a NAT gateway, you need to configure routing rules to direct the subnet traffic to the NAT gateway. |
| [Public Gateway](https://intl.cloud.tencent.com/document/product/213/34835) | A public gateway is a CVM instance with forwarding enabled and can be accessed by NAT. |
| [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/31742) | Bind Anti-DDoS Pro to the NAT gateway for DDoS and CC protection. |
| [Network ACL](https://intl.cloud.tencent.com/document/product/215/31850) | Use network ACL to finely control the inbound and outbound traffic of subnets. |

