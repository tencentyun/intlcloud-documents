Tencent Cloud provides an extensive range of solutions to enable instances within a VPC instance, such as CVMs and databases, to connect to the Internet, connect to instances in other VPC instances, or interconnect with local IDCs.
## Connecting to the Internet
You can use the following products or features to enable access between a VPC instance and the Internet.

<table>
<thead>
<tr>
<th width="12%">Product</th>
<th width="40%">Features</th>
<th width="48%">Characteristics</th>
</tr>
</thead>
<tbody><tr>
<th>Common public IP address</th>
<td>Enables mutual access between the CVM and internet.</td>
<td>You can only obtain a common public IP address while purchasing of a CVM. If you do not obtain one during the purchase, you can use <a xiugaihref="https://intl.cloud.tencent.com/document/product/213/5733" target="_blank">elastic public IP address</a> or <a href="https://intl.cloud.tencent.com/document/product/1015" target="_blank">NAT gateway</a>.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/5733" target="_blank">Elastic public IP address<br>(EIP)</a></td>
<td>A single CVM can be bound to one or more EIPs for internet access.</td>
<td><li>It is an IP resource that can be independently purchased and held. For more information, see <a href="https://intl.cloud.tencent.com/document/product/213/17156" target="_blank">EIP Billing</a>. </li><li>Binds it to or unbinds it from CVM and NAT gateway at any time. </li><li><a href="https://intl.cloud.tencent.com/document/product/213/16586#.E8.B0.83.E6.95.B4.E5.B8.A6.E5.AE.BD" target="_blank">Adjusts the EIP bandwidth limit</a> according to your business needs at any time.</li></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1015" target="_blank">NAT gateway</a></td>
<td><li>SNAT: enables multiple CVMs within a VPC instance to actively access the Internet by using the same public IP address. </li><li>DNAT: maps the private IP addresses, protocols, and ports of CVMs within a VPC instance to public IP addresses, protocols, and ports, so that services on the CVMs can be accessed by the Internet.</li></td>
<td><li>Enables multiple CVMs to access the Internet. </li><li>Allows you to <a href="https://intl.cloud.tencent.com/document/product/1015/30239" target="_blank">adjust the NAT gateway bandwidth limit</a> according to your business needs at any time.</li></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/214" target="_blank">Cloud Load Balancer (CLB)</a></td>
<td>Provides services to internet by averagely distributing access traffic to multiple CVMs.</td>
<td><li>Provides layer-4 and layer-7 load balancing features based on ports, and allows users to access CVMs from the Internet through the CLB.</li><li>Eliminates single points of failure (SPOFs) and enhances the availability of application systems.</li></td>
</tr>
<tr>
<td>Public gateway</td>
<td>It is a type of CVM with the forwarding feature enabled. CVMs without public IP addresses can access the Internet through public gateways in different subnets.</td>
<td><li>The difference between the public gateways and CVMs with common public IP addresses is that public gateways can forward the Internet access traffic of CVMs in other subnets, whereas CVMs with common public IP addresses can only satisfy their own demand for Internet access. </li><li>You can choose whether to configure a CVM as a public gateway only during the purchase of the CVM. If no public gateway is created during the purchase, we recommend that you use <a href="https://intl.cloud.tencent.com/document/product/1015" target="_blank">NAT gateways</a>.</li></td>
</tr>
</tbody></table>

## Connecting to Other VPC Instances
You can use the following products or features to enable inter-VPC communication.

| Product | Features | Characteristics |
|---------|---------|---------|
| [Peering connection](https://intl.cloud.tencent.com/document/product/553) | It is used for communication between VPC instances through a private network. | <li>The CIDR blocks of both VPC instances cannot overlap. </li><li>Manual routing configuration is required. </li><li>Interconnection between VPC instances under different accounts in different regions is supported.</li>|
| [CCN](https://intl.cloud.tencent.com/document/product/1003) | It is used for communication between two or more VPC instances through a private network. | <li>The CIDR blocks of subnets cannot overlap. </li><li>The configuration is simple, and routing is automatically delivered. </li><li>After being added to CCN, all instances are interconnected by default. Routing can be enabled or disabled as needed. </li><li>Interconnection between VPC instances under different accounts in different regions is supported. Interconnection between VPC instances and IDCs is also supported.</li> |

## Connecting to Local IDCs
You can use the following products or features to enable interconnection between VPC instances and local IDCs.

<table>
<thead>
<tr>
<th width="10%">Product</th>
<th width="40%">Features</th>
<th width="50%">Characteristics</th>
</tr>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1037/32680#vpn-.E7.BD.91.E5.85.B3" target="_blank">VPN connection</a></td>
<td>Connects local IDCs and VPC instances through encrypted public network channels.</td>
<td><li>Network quality depends on the Internet. </li><li>Network transmission is based on the PSK encryption of the IKE protocol.</li></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/216" target="_blank">Direct connect</a></td>
<td>Connects VPC instances and local IDCs through direct physical connections.</td>
<td><li>A static network latency is guaranteed. </li><li>Network links are exclusive, which ensures high security. </li><li>The network address translation service can be configured on gateways to resolve address conflict.</li></td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1003" target="_blank">CCN</a></td>
<td>Connects VPC instances and local IDCs through Tencent Cloud’s private network, which enables communication with all VPC instances and IDCs.</td>
<td><li>The configuration is simple, and routing is automatically delivered. </li><li>After instances are added to CCN, interconnection with multiple VPC instances and IDCs is supported. Routing can be enabled or disabled as needed. </li><li>Interconnection between intra-region instances is free of charge.</li></td>
</tr>
</tbody></table>

## Connecting to the Basic Network
You can use the following products or features to enable interconnection between VPC instances and the basic network.

| Product | Features | Characteristics |
|---------|---------|---------|
| Classiclink | Associates CVMs within a basic network with a designated VPC, which enables the CVMs in the basic network to communicate with CVMs, databases, and other cloud services within the VPC. | <li>CVMs in the basic network can access CVMs, cloud databases, private network CLBs, cloud cache, and other cloud resources in the VPC. </li> <li>CVMs in the VPC can access only the CVMs in the basic network with which they are interconnected, but cannot access other computing resources in the basic network.</li> |
| Terminal connection | Enables instances within a VPC to communicate with non-CVM instances in a basic network through a private network. | <li>Basic network products that support terminal connection include: CLB, MySQL, Memcached, Redis, and MongoDB. </li><li>Terminal connection does not support cross-region or cross-account connection. If you need to establish terminal connections, submit a <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">ticket to apply</a>.</li> |
