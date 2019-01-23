## Product Overview
Direct Connect provides a fast and secure approach to connecting Tencent Cloud with local IDCs. You can access to Tencent Cloud computing resources in multiple regions using one Connection, to achieve a flexible and reliable hybrid cloud deployment.

Two topology graphs below to show you how Direct Connect works in Tencent Cloud.

A. Traditional
![](https://main.qcloudimg.com/raw/ac8a373590053d1c08e617157696a3f2.png)

B. Cloud Connect Network
![](https://main.qcloudimg.com/raw/5b47ce3321400dc8260d6b4ed23b30f5.png)


## Components
Direct Connect consists of three parts: Connection, Dedicated Tunnel and Direct Connect gateway.
1. **Connection**: The physical line to connect Tencent Cloud with local IDCs. Connection supports connection via dual-line hot backup, dual-line connection point power supply, and complete isolation of network tunnel.
2. **Dedicated Tunnel**: The network link segmentation of the Connection. You can create Dedicated Tunnels connected to different Direct Connect gateways to achieve interconnection between local IDCs and multiple VPCs.
3. **Direct Connect gateway**: Direct Connect traffic entry for VPC, which can interconnect with different IDCs by connecting with multiple Dedicated Tunnels. Cluster-based Direct Connect gateway can meet the finance-level network interconnection requirements without SPOF risk in the full path.

Direct Connect gateway is used to connect VPCs to Connections. You can create a Dedicated Tunnel associated with a Direct Connect gateway in a Connection. The Direct Connect gateway can interconnect with multiple ICDs by connecting with Dedicated Tunnels from more than one Connections. You can create only one Direct Connect gateway for each VPC in the Direct Connect gateway console. The gateway can connect with Dedicated Tunnels from different Connections.

## Direct Connect vs. IPsec VPN
| Advantage | Direct Connect |  IPsec VPN |
|---------|---------|---------|
| Stable network latency | Tencent Cloud Direct Connect delivers a reliable network latency with a performance guarantee of over 99.5%. You can configure a fixed routing to avoid unstable latency due to bypass resulted from link congestion or failure. | Tencent Cloud IPsecVPN allows network access over the Internet, and may lead to unstable latency due to routing bypass resulted from link congestion during network peak. |
| Highly reliable disaster recovery access | Access devices and network forwarding devices of Tencent Cloud Direct Connect employ distributed cluster deployment with highly reliable full link configurations, and support protected dual-line access, thus meeting your stringent availability requirement of higher than 99.95%. | Tencent Cloud IPSec VPN gateway adopts master/slave hot backup configuration to ensure high reliability at the gateway layer. But it cannot provide Direct Connect-level network reliability due to unreliable Internet network linkage. |
| Large bandwidth | Tencent Cloud Direct Connect supports up to 10 Gbps bandwidth connection in a single line, and can also access multiple 10 Gbps links for network load balancing. Theoretically, there is no upper limit. | A Tencent Cloud IPsec VPN gateway supports 100 Mbps bandwidth at most. You can configure multiple VPN gateways for a VPC to implement VPN access of larger than 100 Mbps. |
| High security | The network link of Tencent Cloud Direct Connect is exclusive to ensure zero data leakage and high security, thus meeting the high demand of financial industry, governments and enterprises for network connectivity. | Tencent Cloud IPsec VPN network transmission is based on the PSK encryption of IKE protocol, which meets the security requirements for network transmission. |
| Network address translation | Tencent Cloud Direct Connect supports configuring the network address translation service on gateways, as well as IP mapping at the two ends of Direct Connect and IP port mapping at the VPC end, to avoid address conflict in case of interconnection among multiple third-party networks. | Not supported |





