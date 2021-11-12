### How do I apply for a public IP if one was not assigned at the time of purchasing the CVM?
If a public IP was not assigned when you purchased the CVM, then there is no way to re-apply for an ordinary public IP for this CVM. However, the same function can be accomplished using [EIPs](https://intl.cloud.tencent.com/document/product/213/5733). For more information on how to use this, please see [Applying for EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
- An EIP is a type of public IP that is fixed to a specific public IP address in a certain region. Unlike an ordinary public IP, it is bound to your account. In other words, you can bind and unbind an EIP with different CVMs as required (only one can be bound at a time).
- Due to the special nature of an EIP, if you apply for an EIP but do not bind it to an instance, IP resource fees will be incurred. For details, please see [EIP Billing](https://intl.cloud.tencent.com/zh/document/product/213/17156).

### How can an instance (CVM or database) access the public network without a public IP address?
An instance without a public IP can apply for an EIP (see the previous question) or can access the public network through NAT gateway.
[NAT gateway](https://intl.cloud.tencent.com/document/product/1015) can provide SNAT and DNAT features for CVM instances in VPCs. If you have multiple instances and want them to access the public network through the same public IP, you can use a NAT gateway.

### Can the public IP of a CVM be changed?
Yes.
- If your CVM instance uses the public IP assigned at the time of purchase, please see [Changing Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/16642).
- If your CVM instance is bound to an EIP, you need to [unbind the EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) first and then [apply for another EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) or bind an existing EIP.
> ! We recommend you immediately release the EIP after it is converted from a public IP. Otherwise, the EIP that is not bound to an instance will incur [IP resource fees](https://intl.cloud.tencent.com/document/product/213/17156). 

### Can a previously used public IP be recovered? Can a specific EIP be applied for?
You can recover public IPs that you have previously used and are not currently assigned to other users. Recovered public IPs are all EIPs. For more information, please see [Retrieve the public network IP address](https://intl.cloud.tencent.com/document/product/213/32719).

### Can an increased quota be requested after the number of EIPs reaches the top limit?
Due to the limited EIP resources, you can apply for only 20 ones per account per region, and you cannot request an increased quota. CVM instances without public IPs can use NAT gateways and other methods to access the public network.

### How does a CVM access the public network if it has a public IP or EIP and its subnet is also associated with a NAT gateway?

If a CVM has a public IP or EIP and its subnet is also associated with a NAT gateway (meaning the route table specifies that the next hop for the traffic of this subnet to access the public network is a NAT gateway), then the default setting is for all the traffic of this CVM to access the public network through the NAT gateway.

If you need to modify the priority so that the traffic from the CVM instance to the public network passes the public IP, please see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).

### When a CVM instance accesses the public network through public gateway or NAT gateway, will the network fee be charged twice?

No, the network fee will only be charged once. When accessing the public network through public gateway or NAT gateway, only the corresponding public gateway network fee or NAT gateway network fee will be charged. 

