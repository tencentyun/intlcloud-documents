### How Do I Apply for a Public IP Address if None Was Assigned When I Purchased the CVM?
If no public IP address was assigned when you purchased the CVM, you cannot re-apply for a common public IP address for this CVM. However, you can achieve this purpose by using [EIPs](https://intl.cloud.tencent.com/document/product/213/5733). For details on how to apply for EIPs, see [Applying for EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
- An EIP is a public IP address that is fixed to a specific IP address in a certain region. Unlike a common public IP address, it is bound to your account. In other words, you can bind an EIP with and unbind it from different CVMs as required (only one EIP can be bound at a time.)
- Due to the nature of EIPs, if you apply for an EIP but do not bind it with an instance, idleness fees incur. For details, see [EIP Billing](https://intl.cloud.tencent.com/document/product/213/17156).

### How Can an Instance (CVM or Database) Access the Internet Without a Public IP Address?
An instance without a public IP address can apply for an EIP (see the previous question) or can access the Internet through the NAT gateway.
A [NAT gateway](https://intl.cloud.tencent.com/document/product/1015) provides CVMs in a VPC with the SNAT and DNAT features. If you have multiple CVMs that need to access the Internet through a public IP address, you can use a NAT gateway.

### Can I Change the Public IP Address of a CVM?
Yes, you can.
- If your CVM was assigned a common public IP address at the time of purchase, see [Changing Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/16642).
- If your CVM is bound to an EIP, you need to [unbind the EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) and [apply for an EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) again or bind it to an existing EIP.

> After you convert a public IP address into an EIP, we recommend that you immediately release the EIP. Otherwise, the EIP that is not bound to any instance will incur [resource occupation fees](https://intl.intl.cloud.tencent.com/document/product/213/17156). 

### Can I Retrieve a Previously Used Public IP Address, and Can I Apply for a Specific EIP?
- Public IP addresses cannot be recovered after being released.
- EIPs that were once used by you and have not yet been assigned to other users can be recovered. For details, see [Recovering Public IP Addresses](https://intl.cloud.tencent.com/document/product/213/32719).

### Can I Increase the Quota After the Number of EIPs Reaches the Upper Limit?
Due to the limits on EIP resources, each account can apply for up to 20 EIPs in each region, and this quota cannot be increased. CVMs without public IP addresses can access the Internet through a NAT gateway or other means.

### How Does a CVM Access the Internet if It Has a Public IP Address or EIP and Its Subnet Is Also Associated with a NAT Gateway?

If a CVM has a public IP address or EIP and its subnet is associated with a NAT gateway, the route table specifies that the next hop for the traffic of this subnet to access the Internet is a NAT gateway. In this case, all the traffic of this CVM to access the Internet flows through the NAT gateway by default.

If you need to modify the priorities to redirect the traffic of the CVM to access the Internet through a public IP address, see [Adjusting the Priorities of NAT Gateways and Public IP Addresses](https://intl.cloud.tencent.com/document/product/1015/30012).

### If a CVM Accesses the Internet Through a Public Gateway or a NAT Gateway, Will the Network Fees Be Charged Twice?

No, the network fees will be charged only once. When you access the Internet through a public gateway or NAT gateway, only the network fee for using the public gateway or NAT gateway will be charged. 
