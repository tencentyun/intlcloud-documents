A direct connect gateway is a traffic entry for Direct Connect that is used to connect Tencent Cloud VPCs with connections (dedicated tunnels). There are two types: VPC-based direct connect gateway and CCN-based direct connect gateway, which are suitable for different use cases.

## Use Limits
A standard direct connect gateway supports propagating secondary CIDR blocks. Note the following limits:
- Up to 10 secondary CIDR blocks can be propagated.
- This feature is unavailable to a NAT direct connect gateway.
- Direct Connect clears gateway resources that meet all of the following conditions:
  - Resources created more than 180 days ago.
  - Resources not bound to a dedicated tunnel for over 90 consecutive days.
  - Resources generating no business traffic for over 90 consecutive days.

## VPC-based Direct Connect Gateway
As shown in the Direct Connect network architecture, dedicated tunnel mode will affect the destination IP range of the IDC routes to Tencent Cloud VPCs. See the following table for details.
<table>
<tr>
<th>Dedicated Tunnel Mode</th>
<th>IDC Routes to Tencent Cloud</th>
</tr>
<tr>
<td>Static</td>
<td>The IDC routes to Tencent Cloud VPCs are configured in the local router.</td>
</tr>
<tr>
<td>BGP</td>
<td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
</tr>
</table>
For example, if a VPC-based direct connect gateway is used between a Tencent Cloud VPC and an IDC in the Direct Connect network architecture, the routes for different dedicated tunnels are configured as follows:

- For a static dedicated tunnel, the destination IP range of IDC routes to a Tencent Cloud VPC is configured in the local router, such as VPC CIDR block (`172.21.0.0/16`).
<img width="80%" src="https://main.qcloudimg.com/raw/71f3699ac26a9df2fbb410ba3b31bf27.png" style="zoom:67%;" />
- For a BGP dedicated tunnel, the destination IP range of IDC routes to a Tencent Cloud VPC is the VPC CIDR block (`172.21.0.0/16`) obtained by the local router based on the BGP protocol.
<img width="80%" src="https://main.qcloudimg.com/raw/ab36e0aa7080f7804a2073692455f62a.png" style="zoom:67%;" />


## CCN-based Direct Connect Gateway
A CCN-based direct connect gateway can associate one CCN with multiple dedicated tunnels to implement the interconnection between VPCs in the CCN and IDCs. As shown in the Direct Connect network architecture, both the creation time of the direct connect gateway and dedicated tunnel mode will affect the destination IP range of the IDC routes to Tencent Cloud VPCs. See the following table for details.
<table>
<tr>
<th>Creation Time</th>
<th>Dedicated Tunnel Mode</th>
<th>IDC Routes to Tencent Cloud</th>
</tr>
<tr>
<td rowspan="2">Before 00:00:00 on September 15, 2020</td>
<td>Static</td>
<td>The IDC routes to Tencent Cloud VPCs are configured in the local router.</td>
</tr>
<tr>
<td>BGP</td>
<td>The IDC automatically obtains the VPC subnet CIDR block based on the BGP protocol.</td>
</tr>
<tr>
<td rowspan="2">After 00:00:00 on September 15, 2020</td>
<td>Static</td>
<td>The IDC routes to Tencent Cloud VPCs are configured in the local router.</td>
</tr>
<tr>
<td>BGP</td>
<td>The IDC automatically obtains the VPC CIDR block based on the BGP protocol.</td>
</tr>
</table>
In a Direct Connect network architecture, if the direct connect gateways A and B are created before and after September 15, 2020, 00:00:00 respectively, the routes for different dedicated tunnel modes are as follows:

- When both dedicated tunnels are static, the destination IP range of IDC routes to Tencent Cloud VPCs is the VPC CIDR block (`172.21.0.0/16`) configured in the local router. The direct connect gateways A and B have the same routes and receive local IDC traffic evenly.
<img width="80%" src="https://main.qcloudimg.com/raw/b1802fe849f2ef09589fa9b9061c827d.png" style="zoom:67%;" />
- When both dedicated tunnels are BGP, the destination IP range synced from the direct connect gateway A to the local router based on the BGP protocol is the subnet CIDR blocks (`172.21.0.0/20`, `172.21.16.0/20`), while that synced from the direct connect gateway B is the VPC CIDR block (`172.21.0.0/16`). The route with the longest mask will be matched and used for forwarding. Therefore, the local router will forward all traffic to the direct connect gateway A. The traffic will be forwarded to the direct connect gateway B only when the direct connect gateway A fails and loses routes.
>?For a direct connect gateway created before September 15, 2020, 00:00:00, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to change its routing policy to VPC CIDR block.
>
<img width="80%" src="https://main.qcloudimg.com/raw/cf9aff5217e067582a04f8c50551f56b.png" style="zoom:67%;" />

## NAT Direct Connect Gateway
A NAT direct connect gateway prevents IP conflicts between your cloud network space and local IDCs by translating IP addresses.
![](https://qcloudimg.tencent-cloud.cn/raw/b69865bf6415f8ee55f335916187152e.png)

 - We recommend that you use BGP dedicated tunnels, so that a local IDC automatically obtains the CIDR block for traffic to the destination VPC.
 - When you configure routing rules for a VPC NAT gateway, SNAT-Local-Layer-3, SNAT-Local-Layer-4, and DNAT-Peer-Layer-4 rules are mapped automatically. Peer-Layer-3 rules cannot be mapped. In addition, the VPC CIDR block is not published by default. Therefore, you must use a Peer-Layer-3 rule with a Local-Layer-3 or Local-Layer-4 rule.
 - NAT Direct Connect Gateway was optimized in March 2023. You can bind a private NAT gateway to the direct connect gateway, and configure the IP mappings at the NAT gateway. The following table compares the old and new configuration methods:
<table>
<tr>
<th>Previous Parameter</th>
<th colspan="2">New Parameter</th>
</tr>
<tr>
<td>Local IP Translation</td>
<td>Mapping Direction: Local</td>
<td>Mapping Type: Layer-3</td>
</tr>
<tr>
<td>Peer IP Translation</td>
<td>Mapping Direction: Peer</td>
<td>Mapping Type: Layer-3</td>
</tr>
<tr>
<td>Local Source IP Port Translation</td>
<td>Mapping Direction: Local</td>
<td>Mapping Type: Layer-4</td>
</tr>
<tr>
<td>Local Destination IP Port Translation</td>
<td>Mapping Direction: Peer</td>
<td>Mapping Type: Layer-4</td>
</tr>
</table>
Local: translates the private IP addresses of the VPC.
Peer: translates the private IP addresses of the network on the opposite end of the VPC. For example, if the peer is an IDC, IP addresses of the IDC are translated.
Layer 3: translates only IP addresses.
Layer 4: maps IP addresses and ports to random ports within a specified IP pool.

## High Availability Overview[](id:dc-dsr)
A direct connect gateway is a bridge connecting cloud network and user IDC off the cloud, thus its high availability is critical to stable operation of business.

### DSR overview
Tencent’s self-developed Disaggregated Software-Defined Router (DSR) is a new generation of software router system based on SDN, NFV and microservice techniques. It is used to replace classic business routers to avoid single-point failures at the layers of system architecture, routing control and data forwarding. Currently, it is broadly deployed in Tencent’s large-scale, high-performance and highly elastic cloud network system.
Compared to classic network physical devices, DSR supports multiple cloud computing virtualization techniques such as NFV and microservice. It adopts a distributed architecture to effectively prevent overall impact caused by the failure of a single component, so as to discover, isolate and recover from failures at the component level automatically.

### High availability design for direct connect gateways
![](https://main.qcloudimg.com/raw/e1223de6586b26115d721c55245544f5.png)
Tencent Cloud Direct Connect inherits the high availability feature of DSR to significantly increase the availability of the direct connect gateways.

- At the route forwarding plane, DSR provides two active-active routing systems for each dedicated tunnel through multi-site active-active technique with each routing system distributed independently in a different DSR cluster. Meanwhile, the DSR clusters provide two Tencent Cloud border IP addresses to implement active-active routing system at the control plane. Thus, the local router on IDC side has created BGP neighbor adjacency with the two clusters respectively via BGP protocol to effectively ensure high availability of business in case of DSR cluster upgrade or single cluster failure and avoid impact on business caused by single BGP neighbor adjacency interruption and route convergence.
- At the data forwarding plane, DSR implements distributed forwarding of massive data and traffic through large-scale cluster control and self-developed cluster scaling technique. It adjusts and removes exceptional service nodes dynamically through real-time monitoring mechanism in the cluster to ensure the availability of single cluster. Meanwhile, it adopts large-scale cluster scaling technique to enable horizontal scaling among multiple clusters for the business to ensure availability across clusters.

### Recommended configuration
1. Tencent Cloud side: DSR learns the routes from Tencent Cloud to user IDC via BGP protocol. The next hop is the user’s local router.
2. User IDC side: user’s local router learns the routes to Tencent Cloud VPC via BGP protocol. The next hop is the IP addresses of the two DSR clusters.
