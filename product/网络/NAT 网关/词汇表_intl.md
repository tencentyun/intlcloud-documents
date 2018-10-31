
### Security group
A <a href="/doc/product/213/500" target="_blank">security group</a> is a virtual firewall with the state-based packet filtering feature, which is used to set network access control for one or more CVMs. You can add CVM instances with the same network security isolation requirements in the same region to the same security group, to securely filter the inbound and outbound traffic of the CVM through the network policies of the security group.



### Peering connection
A <a href="/doc/product/215/5000" target="_blank">peering connection</a> is the connection established by different VPCs, which can be used to connect the traffic between VPCs of different accounts or regions.



### Public gateway
A <a href="/doc/product/215/4972" target="_blank">public gateway</a> is a type of CVM that is able to forward the traffic between the Internet and VPCs. A CVM without a public IP can access the Internet via a public gateway.



### Route table
A <a href="/doc/product/215/4954" target="_blank">route table</a> consists of a series of routing policies that are used to define the traffic direction of each subnet within the VPC. A subnet can be associated with only one route table, but a route table can be associated with multiple subnets in the same VPC.



### Routing policy
A <a href="https://cloud.tencent.com/document/product/215/4925?lang=cn#.E8.B7.AF.E7.94.B1.E7.AD.96.E7.95.A5" target="_blank">routing policy</a> is used to specify the routing rules of network traffic, which contains three parameters:
1. Destination: Describes the destination IP address range. The destination cannot be the IP address range of the VPC in which the route table resides.
2. Next hop type: The next hop type for a VPC supports "public gateway," "VPN gateway," "Direct Connect gateway," etc. You need to create one of such gateways, otherwise you cannot pull the next hop type.
3. Next hop: Specifies the next hop gateway to which the subnet traffic associated with the route table is directed.
View <a href="/document/product/216/1674" target="_blank">routing policy setting details</a>



### Private IP
A private IP is an IP address assigned to an instance in the Tencent Cloud VPC or basic network, which cannot be accessed via the Internet but can be used for communication between instances in the VPC or basic network.



### NAT gateway
A <a href="/doc/product/215/4975" target="_blank">NAT (network address translation) gateway</a> can translate private and public IP addresses within a VPC when the private and public networks are isolated, allowing the VPC to access the Internet. The NAT gateway supports a maximum of 5 Gbps traffic surge and 10,000,000 concurrent connections. As a highly available gateway, the NAT gateway also provides master/slave hot backup, allowing automatic switching when a single server suffers a failure without affecting your use of the services.




### VPC
VPC (Virtual Private Cloud) allows you to build an independent network space on Tencent Cloud, similar to a traditional network hosted in your IDC. However, those hosted in Tencent Cloud VPC are your service resources on Tencent Cloud, including <a href="/doc/product/213/495" target="_blank">CVM</a>, <a href="https://cloud.tencent.com/doc/product/214/524" target="_blank">Load Balancer</a>, <a href="/document/product/236" target="_blank">Database</a> and other resources of cloud services on your Tencent Cloud. Without a need to consider the purchase and OPS of network devices, you only have to focus on the customization of IP address range segmentation, IP addresses, routing policies, etc., using software. You can access the Internet easily via the <a href="/doc/product/213/1941" target="_blank">EIP</a>, <a href="/doc/product/215/4975" target="_blank">NAT gateway</a>, and <a href="/doc/product/215/4972" target="_blank">public gateway</a>, and connect the VPC with your IDCs via <a href="/doc/product/215/4956" target="_blank">VPN</a>/<a href="/doc/product/215/4976" target="_blank">Direct Connect</a>. Also, the Tencent Cloud VPC <a href="/doc/product/215/5000" target="_blank">Peering Connection</a> can help you share a server across the globe and implement 2-region-3-DC disaster recovery. In addition, <a href="/doc/product/213/500" target="_blank">security groups</a> and <a href="/doc/product/215/5132" target="_blank">network ACLs</a> on the Tencent Cloud VPC can satisfy your network security requirements in a multi-dimensional and all-round manner.




### EIP
An <a href="/doc/product/213/1941" target="_blank">elastic IP (EIP)</a> is a public IP address that can be applied for independently. It supports dynamic binding and unbinding. You can bind an EIP to or unbind it from a CVM (or NAT gateway instance) in the account. Here are the main functions:
1. To retain an IP. ICP domain name licensing is required between a domestic IP and DNS.
2. To shield off instance failures. For example, a DNS name is mapped to an IP address through dynamic DNS mapping. It may take up to 24 hours to propagate this mapping to the entire Internet, while elastic IP enables the drift of an IP from one CVM to another. In case of a CVM failure, all you need to do is start another instance and remap it, thus responding rapidly to the instance failure.



### Public IP
A public IP can be accessed via the Internet and can be used for communication between instances and the Internet or other Tencent Cloud resources (such as databases) with public endpoints.



### Subnet
A <a href="/doc/product/215/4927" target="_blank">subnet</a> is a flexible division of VPC IP address ranges. You can deploy applications and services across different subnets and host multi-layer web applications safely and flexibly in the Tencent Cloud VPC.




### Direct Connect
<a href="/doc/product/215/4976" target="_blank">Direct Connect</a> provides a fast approach to connect Tencent Cloud with local IDCs. You can access Tencent Cloud computing resources in multiple regions in one go using Physical Direct Connect, to achieve a flexible and reliable hybrid cloud deployment. Direct Connect supports connection via dual-line hot backup without SPOF to meet high network connectivity requirements of fields such as finance.
It consists of several components: 
1. Physical Direct Connect: The physical line to connect Tencent Cloud with local IDCs. Physical Direct Connect can be used to establish Direct Connect tunnels with Direct Connect gateways in multiple regions.
2. Direct Connect tunnel: The network linkage segmentation of the Physical Direct Connect. You can create Direct Connect tunnels connected to different Direct Connect gateways to achieve connectivity between local IDCs and multiple VPCs.
3. Direct Connect gateway: The Direct Connect traffic entry for the VPC, by which you can connect multiple Direct Connect tunnels with different local IDCs.



