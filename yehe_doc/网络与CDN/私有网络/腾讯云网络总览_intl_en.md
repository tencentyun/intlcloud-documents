Currently, Tencent Cloud operates 20+ IDCs and 50+ AZs worldwide, with edge zones available in major Chinese provincial capitals. Relying on global IDC networks and premium IDC interconnection capabilities, it provides rich network solutions that can meet various needs, such as on-cloud network interconnection, cross-region and cross-account high-speed network interconnection, and on-cloud, off-cloud, and hybrid-cloud network interconnection.
![]()


## Network Service Overview
Tencent Cloud mainly provides the following network services:
<table >
<th width="15%">Category  </th>
<th width="20%">Sub-category  </th>
<th width="20%">Product</th>
<th>Use Case</th>
</th>
<tr>
<td rowspan="13" >On-cloud network</td>
<td  rowspan="3" >Within a VPC</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/215">Virtual Private Cloud</a></td>
<td >Independent, controllable, secure, and isolated dedicated on-cloud network space.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/576">Elastic Network Interface</a></td>
<td >A CVM instance can be bound to multiple ENIs, and an ENI can be bound to multiple private IPs.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/215/31817">Overview</a></td>
<td >A private IP assigned from the VPC subnet CIDR block, usually used with high-availability software to build high-availability primary and secondary clusters.</td>
</tr>
<tr >
<td rowspan="3" >Across VPCs<p>(in the same region)</td>
<td >Private connection</td>
<td >Enables one-way service access from one VPC to another.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/553">Peering Connection</a></td>
<td >Enables one-to-one private network interconnection between two VPCs in the same region.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/1003">Cloud Connect Network</a></td>
<td >Enables private network interconnection between multiple VPCs in the same region.</td>
</tr>
<tr >
<td rowspan="4">Public network connection</td>
<td>EIP</td>
<td >Used for flexible binding and unbinding of Tencent Cloud resources, commonly in use cases where a Tencent Cloud resource instance (such as a CVM instance bound to an EIP) is interconnected with the public network.</td>
</tr>
<tr >
<td >EIP IPv6</td>
<td >Enables the interconnection of IPv6 and the public network.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/1015">NAT Gateway</a></td>
<td >Enables multiple CVM instances to access the public network through a NAT gateway.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/214">Cloud Load Balancer</a></td>
<td >Distributes public network traffic to multiple backend CVM instances to enhance the availability of backend services.</td>
</tr>
<tr >
<td>Public network acceleration</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/644">Anycast Internet Acceleration</a></td>
<td >A dynamic acceleration network covering multiple regions to dramatically improve the public network access experience of your businesses.</td>
</tr>
<tr >
<td rowspan="2" >Network cost saving</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/684">Bandwidth Package</a></td>
<td >A multi-IP aggregated billing mode that enables aggregated bandwidth billing through shared bandwidth packages, saving bandwidth costs compared with purchasing bandwidth for each device.</td>
</tr>
<tr >
<td >Shared traffic package</td>
<td >All Tencent Cloud resources billed by traffic for the public network in the same region can be more cost-effective through shared traffic packages.</td>
</tr>
<tr >
<td colspan="2" rowspan="2" >Cross-region network</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/553">Peering Connection</a></td>
<td >Enables one-to-one interconnection between two VPCs across regions and accounts.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/1003">Cloud Connect Network</a></td>
<td >Enables network interconnection between multiple VPCs across regions and accounts.</td>
</tr>
<tr >
<td colspan="2" rowspan="4" >Hybrid cloud network</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a></td>
<td >Connects a local IDC to a VPC via an encrypted public network channel, with the network quality dependent on the public network.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/216">Direct Connect</a></td>
<td >Connects a VPC and a local IDC through a leased line, which delivers a dedicated network linkage, high security and guaranteed low network latency.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/1003">Cloud Connect Network</a></td>
<td >Connects a local IDC to CCN through a dedicated tunnel for connection with multiple on-cloud VPCs, thus implementing one connection for global connectivity.</td>
</tr>
<tr >
<td >SD-WAN connection service</td>
<td >Branches in different regions can be connected to CCN through edge devices of SD-WAN for hybrid cloud network connectivity.</td>
</tr>
<tr >
<td colspan="2" rowspan="2" >Network security</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/215/38750">Security Group Overview</a></td>
<td >Instance-level access control of inbound and outbound traffic of CVM, CLB, and other instances.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/1003">Network ACL</a></td>
<td >Subnet-level access control of inbound and outbound traffic.</td>
</tr>
<tr >
<td colspan="2" rowspan="6" >Network Ops</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/682">Flow Logs</a></td>
<td >Collects traffic within a specified scope (such as ENIs) and delivers it to CLS to view and search for data for troubleshooting, compliance audit, and other use cases.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/215/35522">Instance Port Verification</a></td>
<td >Checks the accessibility of security group ports of CVM instances to locate faults.</td>
</tr>
<tr >
<td ><a href="https://intl.cloud.tencent.com/document/product/215/35522">Network Probe</a></td>
<td >A service used to monitor the quality of VPC connections, including latency, packet loss rate, and other key metrics.</td>
</tr>
<tr >
<td >Gateway traffic control</td>
<td >Provides IP-level capabilities of gateways (such as NAT gateways and VPN Connections) to monitor and control bandwidth between private IPs and gateways.</td>
</tr>
<tr >
<td ><a href="https://www.tencentcloud.com/document/product/215/36389">Traffic Mirroring</a></td>
<td >Filters the traffic in the specified collection scope by different criteria and replicates and forwards it to CVM in a VPC, which is suitable for security audit, troubleshooting, and business analysis use cases.</td>
</tr>
<tr >
<td ><a href="https://www.tencentcloud.com/document/product/215/46787">Snapshot Policy</a></td>
<td >Sets backup policies for associated objects (such as security groups) and performs data backups, which can be used for disaster recovery and other use cases.</td>
</tr>
</table>

## Practical Guidance
The following describes the Tencent Cloud network services that can be used in different use cases.

### On-cloud network

#### Use case 1. One CVM instance accessing the internet
+  If you purchase a CVM instance and assign a common public IP, the instance is interconnected with the internet.
+  If no common public IP is assigned during CVM instance purchase, you can apply for an EIP and bind it to the CVM instance. Then, the CVM instance is interconnected with the internet via the EIP. For more information, see [CVM Access to Internet Through EIP](https://intl.cloud.tencent.com/document/product/215/45484). For more information on how to implement IPv6 public network access, see Setting up IPv6 VPC.
   

#### Use case 2. Multiple CVM instances accessing the internet
If multiple CVM instances in a VPC need to access the internet, you can purchase a NAT gateway and use its SNAT service, so that these CVM instances can access the internet through the same public IP. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/1015/30251).

#### Use case 3. Internet traffic distribution
Cloud Load Balancer (CLB) provides a secure and fast traffic distribution service. When the internet accesses Tencent Cloud services, the access traffic can be automatically distributed to multiple CVM instances via CLB, which expands the system's service capabilities and eliminates single points of failure. For more information, see [Getting Started with CLB](https://intl.cloud.tencent.com/document/product/214/8975).

#### Use case 4. Network cost saving
+ When a shared traffic package is used, all your CVM instances, EIPs, EIP IPv6 addresses, CLB instances, and NAT gateways billed by traffic for the public network can be more cost-effective.
+ Bandwidth package (BWP) is a multi-IP aggregated billing mode that can significantly save public network costs. When the public network traffic peaks of your businesses are distributed over different time periods, you can use BWP to aggregate the fees, which is cheaper than purchasing bandwidth for each device. For more information, see [Billing Modes](https://intl.cloud.tencent.com/document/product/684/15255).

### Cross-region network interconnection
Tencent Cloud supports interconnection of VPCs in different regions, which can be implemented in the following ways:

#### Use case 1. Connecting two VPCs in different regions
VPCs in different regions (under the same account or different accounts) can be interconnected through a peering connection. For more information, see [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18835).

#### Use case 2. Connecting multiple VPCs in different regions
Multiple VPCs in multiple regions (under the same account or different accounts) can be interconnected over CCN. For more information, see [Cloud Connect Network](https://intl.cloud.tencent.com/document/product/1003/30045).


### Hybrid cloud network interconnection
Tencent Cloud provides the following service capabilities to interconnect a VPC and a local IDC.
+ If you want to quickly interconnect a VPC and a local IDC with an insensitive latency, you can use VPN Connections. For more information, see [VPN Connections](https://intl.cloud.tencent.com/document/product/1037/43324).
+ If you want to interconnect a VPC and a local IDC with a high security, sensitive latency, and dedicated network linkage, you can use Direct Connect. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/216/7557).
+ If you want to interconnect a local IDC with multiple VPCs or other IDCs over the entire network, you can use CCN simply by associating the target VPCs and IDCs with the same CCN instance. For more information, see [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985).
