### How will I be billed for the NAT gateway?

The charges for the NAT gateway includes the following components:

- Charges for the gateway (billed by hour).
- Fees for traffic generated during access to the Internet.

For more information, see [Billing Overview](https://cloud.tencent.com/document/product/552/18172#.E8.AE.A1.E8.B4.B9.E8.AF.B4.E6.98.8E)..

### Why am I charged for the created NAT gateway when I did not use it?

As the NAT gateway features master/slave hot backup, the system sends a 5 KB detection packet to the master/slave servers of the NAT gateway every three seconds. This results in a traffic of 0.2747 GB each day.

### Will I receive a reminder when my NAT gateway expires?

Starting from the moment your account balance becomes 0, you can use the NAT gateway for a further period of 2 hours with the usage being further billed. If your account balance fails to be topped up to an amount greater than 0 after 2 hours, the NAT gateway service is automatically suspended and the billing is stopped. The NAT gateway will remain unavailable until your account balance is topped up to an amount greater than 0 within 24 hours after the suspension of the service. When your account balance has been topped up to an amount greater than 0, the gateway will become available and the billing will start over again. When your account balance has remained below 0 for 24 hours after the suspension of the NAT gateway service, the NAT gateway is reclaimed immediately. The Tencent Cloud account creator and all the collaborators will be notified of the reclaim via email and SMS.

### How will I be charged for my use of the VPC/subnet/route table/NAT gateway/peering connection/public gateway/VPN connection/network ACL?

- The services that use CVMs or licenses are chargeable, including the cross-region peering connection, public gateway, NAT gateway, and VPN gateway. For more information, see [Billing Details](/doc/product/215/3079).
- Other services are not chargeable.

### In the route table, the access to the public network within a subnet is set to be made through NAT gateways, but the CVMs in the subnet are configured with EIPs. Will these CVMs access the public network through NAT gateways or EIPs?

When there are multiple routing rules in a route table, the following routing priority applies:

- Traffic in the VPC.
- Exact match routing.
- Public IP.

For more information, see [Routing Rule Priority](https://cloud.tencent.com/doc/product/215/4954#.E8.B7.AF.E7.94.B1.E8.A7.84.E5.88.99.E4.BC.98.E5.85.88.E7.BA.A7) .
