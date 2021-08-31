
### How is NAT gateway billed? 
NAT gateway fees consist of the following:
- Gateway fees (billed by the hour).
- Public network traffic fees

For more information on billing, see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1015/30248).
For additional VPC pricing information, see [VPC Price Overview](https://intl.cloud.tencent.com/document/product/215/35500).

### Why am I charged for a NAT gateway I did not use?
NAT gateways feature dual-server hot backup. The system sends a 5 KB detection packet to the master and slave NAT gateways every 3 seconds, thereby generating 0.2747 GB of traffic each day. The prices of traffic in Mainland China (not including Hong Kong, Macao, and Taiwan), Hong Kong, and North America are: 0.12 USD/GB, 0.12 USD/GB, and 0.077 USD/GB.

### Will I receive a reminder when my NAT gateway expires?

When the balance in your account becomes 0, you can still use your NAT gateway for 2 hours, but you will be charged for that time. If your account balance is still not greater than 0 after two hours, your NAT gateway stops to function and billing stops. If your account balance is still not greater than zero 24 hours after your NAT gateway stops working, the NAT gateway becomes unavailable, which means you cannot access it anymore. As soon as your account balance is greater than 0, your NAT gateway functions again and billing starts. If your account balance remains at or below 0 for more than 24 hours after your NAT gateway stops functioning, your NAT gateway is repossessed. We will alert the account owner and all collaborators via email and SMS when we repossess the NAT gateway.

### If I configure the routing table to allow one of my subnets to access the public network through a NAT gateway and the CVM instances in that subnet are configured with EIPs. Will these CVM instances access the public network through the NAT gateways or EIPs?
When there are multiple routing policies in a route table, the following routing priority applies, from high to low:
- VPC traffic
- Exact match routing
- Public IP

For more details, refer to [Route Tables](https://intl.cloud.tencent.com/document/product/215/31810).
