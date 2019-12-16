


### Customer Gateway
A customer gateway is a VPC gateway that is mapped to the IPsec VPN gateway in your IDC. It must be used with a VPN gateway. Encrypted VPN tunnels can be established between a VPN gateway and multiple customer gateways.

### IPsec VPN
<!--<a href="https://intl.cloud.tencent.com/document/product/215/4956" target="_blank">-->An IPsec VPN is an encrypted tunnel over a public network that is used to connect your IDC and a VPC.


### Route Table
A <a href="https://intl.cloud.tencent.com/doc/product/215/4954" target="_blank">route table</a> consists of a series of routing policies that are used to define the traffic direction of each subnet within the VPC. A subnet can be associated with only one route table, but a route table can be associated with multiple subnets in the same VPC.
### Routing Policy
A <a href="https://intl.cloud.tencent.com/doc/product/215/4954" target="_blank">routing policy</a> defines a path that network traffic goes through. Each routing policy comprises three parameters:
1. Destination: Describes the destination IP range. The destination cannot be an IP range in the VPC where the route table resides.
2. Next hop type: Specifies the next hop type for a VPC, for example, **Public Gateway**, **VPN Gateway**, or **Direct Connect Gateway**. You must create such a gateway before you select the next hop type.
3. Next hop: Specifies the next hop gateway to which the traffic of a subnet associated with the route table will be directed.

### VPC
A Virtual Private Cloud (VPC) is a separate network space in Tencent Cloud, which is similar to a traditional network running in your IDC. However, the services hosted in a VPC are your Tencent Cloud services, including: <a href="https://intl.cloud.tencent.com/doc/product/213/495" target="_blank">Cloud Virtual Machine (CVM)</a>, <a href="https://intl.cloud.tencent.com/doc/product/214/524" target="_blank">Cloud Load Balancer</a>, and <a href="https://intl.cloud.tencent.com/document/product/236" target="_blank">TencentDB</a>. You do not need to worry about the procurement and OPS of network devices, but can customize IP ranges, IP addresses, and routing policies by using software. You can use <a href="https://intl.cloud.tencent.com/document/product/213/17152" target="_blank">EIPs</a>, <a href="https://intl.cloud.tencent.com/doc/product/215/4975" target="_blank">NAT gateways</a>, and <a href="https://intl.cloud.tencent.com/doc/product/215/4972" target="_blank">public gateways</a> to flexibly access the Internet or connect a VPC to your IDC through <a href="https://intl.cloud.tencent.com/document/product/215/4956" target="_blank">VPN</a> or <a href="https://intl.cloud.tencent.com/document/product/215/4956" target="_blank">Direct Connect</a>. In addition, by using the <a href="https://intl.cloud.tencent.com/doc/product/215/5000" target="_blank">peering connections</a> of a Tencent Cloud VPC, you can easily provide a unified server for global access and three IDCs in two regionsn for disaster recovery. You can also use the <a href="https://intl.cloud.tencent.com/document/product/213/12452" target="_blank">security groups</a> and <a href="https://intl.cloud.tencent.com/document/product/215/5132" target="_blank">network ACLs</a> of the VPC to ensure comprehensive network security.


### VPN Gateway
A [VPN gateway](https://intl.cloud.tencent.com/document/product/1037/32680) is an IPsec VPN gateway in a VPC. It is used with a customer gateway (the IPsec VPN gateway in your IDC) to enable secure and reliable encrypted network communication between the VPC and your IDC.

### VPN Tunnel
A [VPN tunnel](https://intl.cloud.tencent.com/document/product/1037/32680) is an encrypted IPsec VPN tunnel over a public network. After the VPN gateway and customer gateway are created, a VPN tunnel can be established for encrypted communication between the VPC and your IDC.

### Subnet
A <a href="https://intl.cloud.tencent.com/document/product/215/535" target="_blank">subnet</a> is an IP range that is flexibly planned in a VPC. Applications and services can be deployed in different subnets to securely and flexibly host multi-layer web applications in the VPC.
