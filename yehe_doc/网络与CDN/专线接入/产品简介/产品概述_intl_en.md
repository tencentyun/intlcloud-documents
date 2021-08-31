## Direct Connect Overview
Direct Connect provides a fast and secure connection between Tencent Cloud and your local IDC. You can connect Tencent Cloud computing resources in multiple regions with a single connection to implement flexible and reliable hybrid cloud deployment.
- **Deploy hybrid cloud with Direct Connect (1)**
Connect your IDCs with Tencent Cloud VPCs using traditional dedicated tunnels.
If you want to connect to multiple VPCs over one connection, you need to create dedicated tunnels with different VLAN IDs.
![](https://main.qcloudimg.com/raw/ccc440bbebf174404c79f9c0eafe8ba4.png) 
- **Deploy hybrid cloud with Direct Connect (2)**
Interconnect your network instances by using Cloud Connect Network (CCN).
Advantage: you just need to create a connection to the CCN-based direct connect gateway and associate the gateway with CCN to enable interconnection within the CCN.
 ![](https://main.qcloudimg.com/raw/98f444d5e69a086d2dd2d7502ec54ca1.png)

## Components
Direct Connect is composed of connections, dedicated tunnels, and direct connect gateways.
- **Connection**
A connection is a physical line that connects customer’s local IDC to Tencent Cloud. Connections support dual-line hot backup access, dual-line access point power supply, and completely isolated network pipes.
- **Dedicated tunnel**
A dedicated tunnel is a network link segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your on-premises IDC and multiple VPCs.
- **Direct connect gateway**
 - Direct connect gateway is a traffic ingress for a VPC to which multiple dedicated tunnels can be connected for communication with multiple local IDCs. This cluster-based gateway eliminates the risk of single point of failure, and meets the interconnection requirements of the finance industry.
 - Direct connect gateway is used to connect VPC with connections. You can create a dedicated tunnel of connections and associate it with a direct connect gateway.
 - Direct connect gateway can connect to dedicated tunnels of connections to enable interconnection with multiple local IDCs.
 - You can create up to two direct connect gateways (one standard and the other supports NAT) for each VPC in the Direct Connect Gateway console. The direct connect gateway can connect with dedicated tunnels of different connections.

## Advantages over IPsec VPN
<table>
<thead>
<tr>
<th width="16%">Advantage</th>
<th width="40%">Direct Connect</th>
<th width="44%">IPsec VPN</th>
</tr>
</thead>
<tbody><tr>
<td>Low network latency</td>
<td>Network latency is stable and guaranteed. A Direct Connect instance accesses the network through dedicated links, and supports fixed routes, removing the pain of unstable latency caused by network congestion or failure bypass.</td>
<td>Network latency is unstable. An IPsec VPN connection accesses the Internet, which may be exposed to bypass due to network congestion.</td>
</tr>
<tr>
<td>Highly reliable disaster recovery</td>
<td>Access devices and network forwarding devices are deployed in distributed clusters to ensure high reliability of all links. It also supports dual-line access with protection to provide more than 99.95% of uptime.</td>
<td>Features an active-active hot backup architecture with high availability at the gateway layer. However, it cannot provide the same network availability as dedicated lines due to the unreliable Internet links.</td>
</tr>
<tr>
<td>Large bandwidth</td>
<td>It provides a bandwidth of up to 10 Gbps for each link. You can have multiple 10 Gbps links for network load balancing, so it can theoretically support unlimited bandwidth.</td>
<td>A single IPsec VPN gateway supports a bandwidth of up to 1 Gbps and a VPC can have multiple VPN gateways, which can meet the need for a VPN connection larger than 1 Gbps.</td>
</tr>
<tr>
<td>High security</td>
<td>Dedicated network links offer strong security without data leakage risks, satisfying the demanding network connection requirements of the finance and government sectors.</td>
<td>Network transmission is encrypted using IKE pre-shared key, which can satisfy the security requirements for most network transmission.</td>
</tr>
<tr>
<td>Network address translation</td>
<td>It supports configuring the network address translation service on gateways, as well as IP mapping on the two sides of Direct Connect and IP port mapping on the VPC side, to avoid address conflict in case of interconnection among multiple networks.</td>
<td>Not supported.</td>
</tr>
</tbody></table>
