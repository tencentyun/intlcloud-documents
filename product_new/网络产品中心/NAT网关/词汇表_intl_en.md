
### Security Group
<a href="https://intl.cloud.tencent.com/document/product/213/12452" target="_blank">Security Group</a> is a virtual firewall with the state-based packet filtering feature, which is used to set network access control for one or more CVMs. You can add CVM instances with the same network security isolation requirements within the same region to the same security group, and filter the inbound and outbound traffic of the CVMs based on the network policies of the security group.



### Peering Connections
<a href="https://intl.cloud.tencent.com/doc/product/215/5000" target="_blank">Peering connection</a> is the connection established among different VPCs, supporting cross-account and cross-region communication between VPCs.



### Public network gateway
<a href="https://intl.cloud.tencent.com/document/product/215/4972" target="_blank"> public gateway</a> is a type of CVM that is able to forward the traffic between the Internet and VPCs. A CVM without a public IP can access the Internet via a public gateway.



### Route Table
A <a href="https://intl.cloud.tencent.com/doc/product/215/4954" target="_blank">route table</a> consists of a series of routing policies that are used to define the traffic direction of each subnet within the VPC. A subnet can be associated with only one route table, but a route table can be associated with multiple subnets in the same VPC.



### Routing Policy
A <a href="https://intl.cloud.tencent.com/document/product/215/4954" target="_blank">routing policy</a> defines a path that network traffic goes through. Each routing policy comprises three parameters:
1. Destination: Describes the destination IP address range. The destination cannot be the IP address range of the VPC in which the route table resides.
2. Next hop type: The next hop type for a VPC supports "public gateway", "VPN gateway", "Direct Connect gateway", etc. You need to create one of such gateways, otherwise you cannot pull the next hop type.
3. Next hop: Specifies the next hop gateway to which the subnet traffic associated with the route table is directed.
For details, refer to <a href="https://intl.cloud.tencent.com/document/product/216/19259" target="_blank">Configuring Route Tables</a>.



### Private IP
A private IP is an IP address assigned to an instance in the Tencent Cloud VPC or basic network, which cannot be accessed via the Internet but can be used for communication between instances in the VPC or basic network.



### NAT Gateway
<a href="https://intl.cloud.tencent.com/doc/product/215/4975" target="_blank">A [NAT gateway]</a> can translate the private IP address in a Virtual Private Cloud (VPC) to a public IP address if the private and public networks are isolated from each other, enabling the VPC to access the Internet. The NAT gateway supports a maximum of 5 Gbps traffic surge and 10,000,000 concurrent connections. As a highly available gateway, the NAT gateway also provides master/slave hot backup, enabling automatic switching in the event of a single point of failure with an imperceptible impact on your use of the services.




### Virtual Private Cloud
A virtual private cloud (VPC) builds a separate network space in Tencent Cloud, which is very similar to a traditional network run in your IDC, except that the services hosted in a VPC are your Tencent Cloud services such as <a href="https://intl.cloud.tencent.com/doc/product/213/495" target="_blank">Cloud Virtual Machine</a>, <a href="https://intl.cloud.tencent.com/doc/product/214/524" target="_blank">Cloud Load Balancer</a>, and <a href="https://intl.cloud.tencent.com/document/product/236" target="_blank">TencentDB</a>. You do not need to worry about the procurement and OPS of network devices; instead, you only need to customize IP ranges, IP addresses, routing policies, etc. through easy-to-use software programs. You can use <a href="https://intl.cloud.tencent.com/document/product/213/5733" target="_blank">EIPs</a>, <a href="https://intl.cloud.tencent.com/doc/product/215/4975" target="_blank">NAT gateways</a>, and <a href="https://intl.cloud.tencent.com/doc/product/215/4972" target="_blank">public gateways</a> to flexibly access the internet or interconnect a VPC with your IDC through <a href="https://intl.cloud.tencent.com/doc/product/215/4956" target="_blank">VPN</a> or <a href="https://intl.cloud.tencent.com/document/product/216" target="_blank">Direct Connect</a>. In addition, VPC’s <a href="https://intl.cloud.tencent.com/doc/product/215/5000" target="_blank">Peering Connection</a> can help you easily implement a unified server for global access and 2-region-3-DC disaster recovery, and the <a href="https://intl.cloud.tencent.com/document/product/213/12452" target="_blank">security groups</a> and <a href="https://intl.cloud.tencent.com/doc/product/215/5132" target="_blank">network ACLs</a> features of VPC ensures comprehensive network security.




### EIP
An <a href="https://intl.cloud.tencent.com/document/product/213/17152" target="_blank">elastic IP (EIP)</a> is a public IP address that can be applied for independently. It supports dynamic binding and unbinding. You can bind an EIP to or unbind it from a CVM (or NAT gateway instance) in the account. The main functions are as follows:
1. To retain an IP. ICP domain name licensing is required between a Mainland China IP and DNS.
2. To shield off instance failures. For example, a DNS name is mapped to an IP address through dynamic DNS mapping. It may take up to 24 hours to propagate this mapping to the entire Internet, while elastic IP enables the drift of an IP from one CVM to another.



### Public IP
A public IP can be accessed via the Internet and can be used for communication between instances and the Internet or other Tencent Cloud resources (such as databases) with public endpoints.



### Subnet
A <a href="https://intl.cloud.tencent.com/document/product/215/535" target="_blank">subnet</a> is a flexible way to segment a VPC into different IP ranges. Applications and services can be deployed in different subnets to securely and elastically host multi-layer web applications in a VPC.




### Direct Connect
<a href="https://intl.cloud.tencent.com/document/product/216" target="_blank">Direct Connect</a> is a fast way to connect Tencent Cloud with your local IDC. A connection can be established to communicate with Tencent Cloud resources in multiple regions for elastic and reliable hybrid cloud deployment. Direct connect supports two-line hot backup access mode free of single points of failure to meet the high networking requirements in demanding industries such as finance.
It consists of several components: 
1. Connection: The physical line to connect Tencent Cloud with customer IDCs. It can establish Direct Connect tunnels with Direct Connect gateways in multiple regions.
2. Direct Connect tunnel: The network linkage segmentation of the Physical Direct Connect. You can create Direct Connect tunnels connected to different Direct Connect gateways to achieve connectivity between local IDCs and multiple VPCs.
3. A Direct Connect gateway is a connection traffic entry for a VPC to which multiple dedicated tunnels can be connected for communication with multiple local IDCs.


