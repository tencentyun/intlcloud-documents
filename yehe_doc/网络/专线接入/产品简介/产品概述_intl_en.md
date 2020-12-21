## What is Direct Connect?
Direct Connect provides a fast and secure connection between Tencent Cloud and your local IDC. You can connect Tencent Cloud computing resources in multiple regions with a single connection to implement flexible and reliable hybrid cloud deployment.
- **Deploy hybrid cloud with Direct Connect (1)**
  Connect your IDCs with cloud VPCs using traditional dedicated tunnels.
  If you want to connect multiple VPCs over one connection, you need to create dedicated tunnels with different VLAN IDs.
![](https://main.qcloudimg.com/raw/ccc440bbebf174404c79f9c0eafe8ba4.png)  
- **Deploy hybrid cloud with Direct Connect (2)**
Interconnect your network instances by using Cloud Connect Network (CCN).
Advantage: you just need to create a connection to the CCN-based direct connect gateway and load the gateway with CCN to enable multiple network instances within the CCN to interconnect with each other.
 ![](https://main.qcloudimg.com/raw/98f444d5e69a086d2dd2d7502ec54ca1.png)

## Components
Direct Connect is composed of connections, dedicated tunnels, and direct connect gateways.
- **Connection**
Connections are physical lines that connect Tencent Cloud with local IDCs. Connections support dual-line hot backup access which features independent power supply and complete isolation of network channels.
- **Dedicated tunnel**
Dedicated tunnels are network link segmentation of a connection. You can create dedicated tunnels that connect to different direct connect gateways to enable communication between your local IDC and multiple VPCs.
- **Direct connect gateway**
 - Direct connect gateway is a direct connect traffic entry for a VPC to which multiple dedicated tunnels can be connected for communication with multiple local IDCs. This cluster-based gateway eliminates the risk of single point of failure, meeting the interconnection requirements of the finance industry.
 - Direct connect gateway is used to bridge VPCs and connections. You can create a dedicated tunnel using a connection and associate it with a direct connect gateway.
 - Direct connect gateway can connect dedicated tunnels of connections to enable interconnection with multiple local IDCS.
 - You can create only one direct connect gateway for each VPC in the Direct Connect Gateway console. The gateway can connect with dedicated tunnels of different connections.

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
<td>Network latency is stable and guaranteed. Access networks are based on dedicated links, which you can configure with fixed routes, avoiding a unstable latency caused by network congestion or failure bypass.</td>
<td>Access networks are based on the Internet, which may be subject to unstable latency caused by non-optimal routes during traffic peaks and network congestion.</td>
</tr>
<tr>
<td>Highly reliable disaster recovery</td>
<td>Access devices and network forwarding devices are deployed in distributed clusters to ensure full-link high reliability. It also supports dual-line access with protection to provide more than 99.95% of uptime.</td>
<td>Dual-server hot backup ensures that the gateway is highly available. However, it cannot provide the same network availability as dedicated lines due to the unreliable Internet links.</td>
</tr>
<tr>
<td>Large bandwidth</td>
<td>Each link supports up to 10 Gbps of bandwidth and you can have multiple links for network load balancing. Technically, there is no limit to how much bandwidth you can have.</td>
<td>A single gateway supports up to 1 Gbps of bandwidth and a VPC can have multiple VPN gateways to support VPN connections larger than 1 Gbps.</td>
</tr>
<tr>
<td>Highly secure</td>
<td>Dedicated network links offer strong security without data leakage risks. This is ideal for the demanding network connection requirements of the finance and government sectors.</td>
<td>Network transmission is encrypted using IKE pre-shared key, which can satisfy the security requirements for most network transmission.</td>
</tr>
<tr>
<td>Network address translation</td>
<td>Network address translation can be configured on gateways. IP mapping on both ends of a Direct Connect and IP port mapping at the VPC side are supported, resolving the address conflicts when multiple networks are interconnected.</td>
<td>Not supported</td>
</tr>
</tbody></table>
