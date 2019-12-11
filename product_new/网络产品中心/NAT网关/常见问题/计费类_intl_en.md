
### How is NAT gateway billed? 
NAT gateway fees consists of the following:
- Gateway fees (billed hourly).
- Internet access traffic fees.

For details, please see [Billing Overview](https://cloud.tencent.com/document/product/552/18172#.E8.AE.A1.E8.B4.B9.E8.AF.B4.E6.98.8E).
For additional VPC pricing information, please see [VPC Price Overview](https://cloud.tencent.com/doc/product/215/3079).

### Why am I charged for a created NAT gateway when I did not use it?
NAT Gateway features dual-server hot backup. The system sends a 5KB detection packet to the master and slave servers of NAT Gateway respectively every 3 seconds, so 0.2747GB of traffic will be generated every day.

### Access to the public network within a subnet is set to be made through NAT gateways in the routing table, but the CVMs in the subnet are configured with EIPs. Will these CVMs access the public network through NAT gateways or EIPs?
When there are multiple routing rules in a routing table, the following routing priority applies:

- VPC traffic
- Exact match routing
- Public IP

For details, please see [Routing Tables](https://cloud.tencent.com/doc/product/215/4954#.E8.B7.AF.E7.94.B1.E8.A7.84.E5.88.99.E4.BC.98.E5.85.88.E7.BA.A7). 
