NAT Gateway provides different types of packages. Select the package that meets your needs.
### Configuration Specifications
NAT Gateway supports binding up to 10 EIPs, and a maximum of 5 Gbps traffic surge and 10,000,000 concurrent connections, while providing three configuration specifications:
- Small-scale (a maximum of 1000,000 connections)
- Medium-scale (a maximum of 3000,000 connections) 
- Large-scale (a maximum of 10,000,000 connections)

>?Restricted by standard protocols, for the NAT gateways with the same protocol/destination IP/destination port, the number of maximum connections = the number of bound EIPs × 55000. To increase the number of connections, bind new EIPs or adjust the destination IP/port.
>

### Maximum Public Network Outbound Bandwidth
Available maximum public network outbound bandwidths of the NAT gateway (in Mbps): 10, 20, 50, 100, 200, 500, 1,000, 2,000, and 5,000.

### Maximum Public Network Inbound Bandwidth
- The maximum public network inbound bandwidth of a NAT gateway is 5 Gbps by default, which is unchangeable for now.
- The traffic cost of NAT Gateway is calculated based on the maximum public network outbound bandwidth regardless of the public network inbound bandwidth.

For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1015/30248).


