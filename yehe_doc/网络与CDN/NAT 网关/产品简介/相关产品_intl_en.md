This document describes the network products related to NAT Gateway.
## EIP
The NAT Gateway and the EIP are two ways for a CVM instance to access the public network. You can use either or both of them in your public network access architecture.

### Method 1: using NAT Gateway only
The CVM instance without any public IP uses the public IP of the NAT Gateway to access the public network. Traffic to the public network is forwarded to the NAT Gateway via the private network.

### Method 2: using the EIP only
The CVM instance uses EIPs to access the public network without any NAT Gateway. Traffic to the public network will be forwarded from the EIP.

### Method 3: using NAT Gateway and EIP

>? For more information about EIPs, see [Elastic IP](https://intl.cloud.tencent.com/document/product/213/16586).
>

The CVM instance is bound with an EIP, and the route table directs all traffic from the subnet to the public network to the NAT Gateway.
- All traffic from the CVM instance to the public network **uses the NAT Gateway through the private network**, and the response packets are returned through the NAT Gateway. If you want to use the EIP to access the public network, you can [adjust priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).
- When the traffic from the public network uses the EIPs to access CVM, the CVM response packets are returned through the EIPs.


## Bandwidth Package
If your NAT Gateway is bound with multiple EIPs, you can add them to the IP bandwidth package to share the bandwidth and save public network costs. For more information, see [Product Overview](https://intl.cloud.tencent.com/document/product/684/15245).

## Other Products
The table below lists other products related to the NAT Gateway:

| Product Name | Relationship |
|---------|---------|
| [CVM](https://intl.cloud.tencent.com/document/product/213/495) | The NAT Gateway and the EIP are two ways for CVM instances to access the Internet. |
| [EIP](https://intl.cloud.tencent.com/document/product/213/16586) | The EIP and the NAT Gateway are two ways for CVM instances to access the Internet. |
| [VPC](https://intl.cloud.tencent.com/document/product/215/535) | NAT Gateway is part of VPC. |
| [Route Table](https://intl.cloud.tencent.com/document/product/215/31810) | After creating a NAT Gateway, you need to configure routing policies to direct the subnet traffic to the NAT Gateway. |
| [Public Gateway](https://intl.cloud.tencent.com/document/product/213/34835) | A public gateway is a CVM with the forwarding feature enabled and can be accessed by NAT Gateway. |
| [Anti-DDoS Pro](https://intl.cloud.tencent.com/zh/document/product/1029/31742) | Anti-DDoS Pro instance can be bound to a NAT Gateway to defend against DDoS and CC attacks. |
| [Network ACL](https://intl.cloud.tencent.com/document/product/215/31850) | Use network ACL to finely control the inbound and outbound traffic of subnets.|

