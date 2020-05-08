Watch the following video to understand what is Direct Connect, its components and how it is different from and better than IPsec VPN.
<div class="doc-video-mod"><iframe src="https://cloud.tencent.com/edu/learning/quick-play/1670-12008?source=gw.doc.media&withPoster=1&notip=1"></iframe></div>

## Overview
Direct Connect provides fast and secure connections from on-premises IDCs to Tencent Cloud. You can access Tencent Cloud computing resources in multiple regions and use the connection to implement flexible and reliable hybrid cloud deployments.
- **Hybrid cloud deployment with Direct Connect** (1)
  Connect your IDCs with cloud VPCs using traditional dedicated tunnels.
  If you want to connect to multiple VPCs over one connection, you need to create dedicated tunnels with different VLAN IDs.
  

- **Deploy hybrid cloud with Direct Connect** (2)
Interconnect your network instances by using Cloud Connect Network (CCN).
Advantage: you just need to create a connection to the CCN Direct Connect gateway and load the gateway with CCN to enable multiple network instances within the CCN to interconnect with each other.


## Components
Direct Connect is composed of connections, dedicated tunnels, and Direct Connect gateways.
- **Connection**
Connections are physical cables that connect Tencent Cloud with on-premises IDCs. Connections support dual-line hot backup access, dual-line access point power supply, and complete isolation of network pipes.
- **Dedicated tunnel**
Dedicated tunnels are network link segmentation of a connection. You can create dedicated tunnels that connect to different Direct Connect gateways to enable communication between your on-premises IDC and multiple VPCs.
- **Direct Connect gateway**
 - Direct Connect gateways act as dedicated ingress points to VPCs and can connect to multiple IDCs by creating multiple dedicated tunnels. Direct Connect gateways are implemented as a cluster to eliminate the risk of single point of failure and meeting the requirements of the finance industry.
 - Direct Connect gateway is used to bridge VPCs and connections. You can create a dedicated tunnel using a connection and associated it with a Direct Connect gateway.
 - The Direct Connect gateway can interconnect with multiple on-premises IDCs by connecting with Direct Connect tunnels from multiple connections.
 - You can use the Direct Connect gateway console to create one and only one Direct Connect gateway for each VPC. The gateway can connect with dedicated tunnels from different connections.

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
<td>Stable network latency</td>
<td>Network latency is stable and guaranteed. Access networks are based on dedicated links, which you can configure with fixed routes. This removes the pain of unstable latency caused by network congestion or the need to bypass failures.</td>
<td>Access networks are based on the Internet, which may be subject to unstable latency caused by unoptimal routing due to traffic peaks and network congestion.</td>
</tr>
<tr>
<td>Highly reliable disaster recovery</td>
<td>Access devices and network forwarding devices are deployed in distributed clusters to ensure high reliability of the full link. It also supports dual-line access with protection to provide more than 99.95% of uptime. </td>
<td>Dual-server hot backup ensures that the gateway is highly availability. However, it cannot provide the same network availability as dedicated lines due to the unreliable Internet links.</td>
</tr>
<tr>
<td>Large bandwidth</td>
<td>Each link supports up to 10Gbps and you can have multiple 10Gbps links for network load balancing. Technically, there is no limit to how much bandwidth you can have.</td>
<td>A single gateway supports up to 100Mbps of bandwidth and a VPC can have multiple VPN gateways to support VPN connections larger than 100Mbps.</td>
</tr>
<tr>
<td>Highly secure</td>
<td>Dedicated network links offer strong security with no risk of data leakage. This is ideal for the demanding network connection requirements of the finance and government sectors.</td>
<td>Network transmission uses IKE to encrypt trafic with pre-shared key, which can satisfy the security requirements for most network transmission.</td>
</tr>
<tr>
<td>Network address translation</td>
<td>Network address translation can be configured on gateways. IP mapping on both ends of a Direct Connect and IP port mapping at the VPC side are supported, resolving the address conflicts when multiple networks are interconnected.</td>
<td>Not supported.</td>
</tr>
</tbody></table>
