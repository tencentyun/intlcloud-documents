


## Customer Gateway
Customer Gateway is your IDC's IPsec VPN service gateway that is mapped in a VPC, which needs to be used in conjunction with a VPN gateway. A VPN gateway can establish encrypted VPN tunnels with multiple customer gateways.

### IPsec VPN
<a href="/doc/product/215/4956" target="_blank">IPsec VPN</a> (Internet Protocol Security VPN) is used to connect your IDC and a VPC through an encrypted tunnel over public networks.


### Route table
A <a href="/doc/product/215/4954" target="_blank">route table</a> consists of a series of routing policies that are used to define the traffic direction of each subnet within the VPC. A subnet can be associated with only one route table, but a route table can be associated with multiple subnets in the same VPC.
### Routing policy
A <a href="/document/product/215/4925?lang=cn#.E8.B7.AF.E7.94.B1.E7.AD.96.E7.95.A5" target="_blank">routing policy</a> is used to specify the routing rules of network traffic, which contains three parameters:
1. Destination: Describes the destination IP address range. The destination cannot be the IP address range of the VPC in which the route table resides.
2. Next hop type: The next hop type for a VPC supports "public gateway", "VPN gateway", "Direct Connect gateway", etc. You need to create one of such gateways, otherwise you cannot pull the next hop type.
3. Next hop: Specifies the next hop gateway to which the subnet traffic associated with the route table is directed.

### VPC
VPC (Virtual Private Cloud) allows you to build an independent network space on Tencent Cloud, similar to a traditional network hosted in your IDC. However, those hosted in Tencent Cloud VPC are your service resources on Tencent Cloud, including <a href="/doc/product/213/495" target="_blank">CVM</a>, <a href="/doc/product/214/524" target="_blank">Load Balancer</a>, <a href="/document/product/236" target="_blank">Database</a> and other resources of cloud services on your Tencent Cloud. Without a need to consider the purchase and OPS of network devices, you only have to focus on the customization of IP address range segmentation, IP addresses, routing policies, etc., using software. You can access the Internet easily via the <a href="/doc/product/213/1941" target="_blank">EIP</a>, <a href="/doc/product/215/4975" target="_blank">NAT gateway</a> and <a href="/doc/product/215/4972" target="_blank">public gateway</a>, and connect the VPC with your IDCs via <a href="/doc/product/215/4956" target="_blank">VPN</a>/<a href="/doc/product/215/4976" target="_blank">Direct Connect</a>. Also, the Tencent Cloud VPC <a href="/doc/product/215/5000" target="_blank">Peering Connection</a> can help you share a server across the globe and implement 2-region-3-DC disaster recovery. In addition, <a href="/doc/product/213/500" target="_blank">security groups</a> and <a href="/doc/product/215/5132" target="_blank">network ACLs</a> on the Tencent Cloud VPC can satisfy your network security requirements in a multi-dimensional and all-round manner.


### VPN gateway
[VPN gateway](/document/product/554/19276#vpn-.E7.BD.91.E5.85.B3) is an IPsec VPN gateway in a VPC, which is used in conjunction with a customer gateway (your IDC's IPsec VPN service gateway). It is mainly used to establish a secure and reliable encrypted network communication between the VPC and your IDC.

### VPN tunnel
[VPN tunnel](/document/product/554/19276#vpn-.E9.80.9A.E9.81.93) is an encrypted IPsec VPN tunnel over public networks. After the VPN gateway and the customer gateway are established, the VPN tunnel can be established for encrypted communication between the VPC and your IDC.

### Physical Direct Connect
Physical Direct Connect is the physical line to connect Tencent Cloud with local IDCs. It can be used to establish Direct Connect tunnels with Direct Connect gateways in multiple regions.

### Subnet
A <a href="/doc/product/215/4927" target="_blank">subnet</a> is a flexible division of VPC IP address ranges. You can deploy applications and services across different subnets and host multi-layer web applications safely and flexibly in the Tencent Cloud VPC.

### Direct Connect
<a href="/doc/product/215/4976" target="_blank">Direct Connect</a> provides a fast approach to connect Tencent Cloud with local IDCs. You can access Tencent Cloud computing resources in multiple regions in one go using Physical Direct Connect, to achieve a flexible and reliable hybrid cloud deployment. Direct Connect supports connection via dual-line hot backup without SPOF to meet high network connectivity requirements of fields such as finance.

### Direct Connect tunnel
Direct Connect tunnel is the network linkage segmentation of the Physical Direct Connect. You can create Direct Connect tunnels connected to different Direct Connect gateways to achieve connectivity between local IDCs and multiple VPCs.

### Direct Connect gateway
Direct Connect gateway is the Direct Connect traffic entry for the VPC, by which you can connect multiple Direct Connect tunnels with different local IDCs.

