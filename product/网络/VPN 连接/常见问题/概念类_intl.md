### What is VPN Connection?
VPN Connection is used to connect your customer IDC and VPC through an encrypted tunnel over public networks. For more information, see [Related Concepts](/document/product/215/4956?&_ga=1.2210355.205113617.1532487250#.E7.AE.80.E4.BB.8B).

## What is VPN tunnel?
After the VPN gateway and the customer gateway are established, a VPN tunnel can be established for encrypted communication between the VPC and the external IDC. For more information, see [Related Concepts](/document/product/215/4956?&_ga=1.2210355.205113617.1532487250#vpn-.E9.80.9A.E9.81.93).
## What is VPN gateway?
VPN gateway is an egress gateway used to establish VPN connections from your VPC. It is used with customer gateway (IPsec VPN gateway on IDC side) to establish an encrypted tunnel between a Tencent Cloud VPC and an external IDC for secure and reliable network communication. Tencent Cloud VPN gateway is implemented based on software virtualization. With a dual-server hot backup mechanism, it switches to another server automatically in case of a fault of one server, without affecting the normal operation of business.
- Based on the bandwidth cap, VPN gateway is available in 5 bandwidth levels: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps and 100 Mbps. You can adjust the VPN gateway bandwidth setting at any time and the change takes effect immediately.
- If you need Dayu Anti-DDoS to provide ultra-large bandwidth DDoS and CC defense for the VPN gateway, you can bind a Dayu high defense package to the VPN gateway for security protection.

### What is IPsec VPN?
 [IPsec VPN](/doc/product/215/4956) is used to connect your IDC and a VPC through an encrypted tunnel over public networks. Tencent Cloud VPC IPsec VPN connection consists of the following components:
- **VPN gateway**: Refers to an IPsec VPN gateway in a VPC, which is used in conjunction with a customer gateway (your IDC's IPsec VPN service gateway). It is mainly used to establish a secure and reliable encrypted network communication between the VPC and your IDC.
- **Customer gateway**: Refers to your IDC's IPsec VPN service gateway that is mapped in a VPC, which needs to be used in conjunction with a VPN gateway. A VPN gateway can establish encrypted VPN tunnels with multiple customer gateways.
- **VPN tunnel**: Refers to an encrypted IPsec VPN tunnel over public networks. After the VPN gateway and the customer gateway are established, the VPN tunnel can be established for encrypted communication between the VPC and your IDC.

### What is the function of VPN gateway traffic control?
VPN gateway traffic control provides the "monitoring" and "controlling" capabilities at the granularity of IP-gateway. For more information about its function and advantages, see [VPN Gateway Traffic Control](/document/product/215/4956?&_ga=1.2210355.205113617.1532487250#vpn-.E7.BD.91.E5.85.B3.E6.B5.81.E6.8E.A7).

### What are the limitations on using VPN?
 When using a VPN, pay attention to the limitations on the VPN connection and the IP address of its customer gateway. For more information, see [Usage Constraints](/document/product/215/4956?&_ga=1.2210355.205113617.1532487250#.E4.BD.BF.E7.94.A8.E7.BA.A6.E6.9D.9F).
 


### How many VPN gateways and VPN tunnels can I create?
It depends on the limitations of specific resources. For more information, see [Detailed Resource Quota in the VPC](/document/product/215/537). [Submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) to apply for a higher quota if needed.

### Can a VPC connect to multiple IDCs through VPN connections?
Yes. You can create VPN gateways in a VPC and create multiple VPN tunnels on each VPN gateway, with each VPN tunnel establishing a connection between the VPC and a local IDC.

### Can two VPCs communicate with each other via VPN?
Yes. But you need to purchase VPN gateway, and configure VPN tunnel and customer gateway in the two VPCs respectively through a complicated process. You're recommended to use peering connection, which establishes a connection between the two VPCs using the Tencent backbone network to ensure a more reliable communication.

### How do I ensure the network stability between the VPC and IDC connected via VPN?
- The communication between the VPC and the IDC is made through a public network, which therefore depends on the quality of the public network. Latency, packet loss, and jitter are all possible. If you need more stable communication quality, we recommend that you use the Direct Connect service.
- The VPN backend will monitor the network quality throughout the day, including keepalive and network latency. In case of a network exception, it will inform the OPS personnel to deal with it in a timely manner. You can also monitor the traffic status of VPN gateways and tunnels in real time in the console. Contact us if you find exceptions.


### What is the difference between Direct Connect and VPN Connection?
- VPN Connection uses public network and IPsec protocol to establish an encrypted network connection between your IDC and VPC. The purchase, activation and configuration of a VPN gateway can be completed within minutes. But a VPN connection may be broken due to problems of public network such as jitter and congestion. It allows for fast deployment and is a cost-effective choice for the businesses that are not sensitive to the network condition.
- Direct Connect provides a network connection solution dedicated to your business. It takes a longer time to be set up, but can provide a highly reliable network connection. It is suitable for the businesses that have a higher requirement for the network condition and security.

### What is the difference between Direct Connect and IPSec VPN Connection?
- IPsec VPN Connection uses public network and IPsec protocol to establish an encrypted network connection between your IDC and VPC. The purchase, activation and configuration of a VPN gateway can be completed within minutes. But a VPN connection may be broken due to problems of public network such as jitter and congestion. It allows for fast deployment and is a cost-effective choice for the businesses that are not sensitive to the network condition.
- Direct Connect provides a network connection solution dedicated to your business. It takes a longer time to be set up, but can provide a highly reliable network connection. It is suitable for the businesses that have a higher requirement for the network condition and security.

Here are the specific differences between them:

| Advantage | Direct Connect |  IPsec VPN|
|-|-|-|
| Stable network latency | Tencent Cloud Direct Connect delivers a reliable network latency with a performance guarantee of over 99.5%. You can configure a fixed routing to avoid unstable latency due to bypass resulted from link congestion or failure. | Tencent Cloud IPsec VPN allows network access over the Internet, and may lead to unstable latency due to routing bypass resulted from link congestion during network peak. |
| Highly reliable disaster recovery access | Access devices and network forwarding devices of Tencent Cloud Direct Connect employ distributed cluster deployment with highly reliable full link configurations, and support protected dual-line access, thus meeting your stringent availability requirement of higher than 99.95%. | Tencent Cloud IPSec VPN gateway adopts master/slave hot backup configuration to ensure high reliability at the gateway layer. But it cannot provide Direct Connect-level network reliability due to unreliable Internet network linkage. |
| Large bandwidth | Tencent Cloud Direct Connect supports up to 10 Gbps bandwidth connection in a single line, and can also access multiple 10 Gbps links for network load balancing. Theoretically, there is no upper limit. | A Tencent Cloud IPsec VPN gateway supports 100 Mbps bandwidth at most. You can configure multiple VPN gateways for a VPC to implement VPN access of larger than 100 Mbps. |
| High security | The network link of Tencent Cloud Direct Connect is exclusive to ensure zero data leakage and high security, thus meeting the high demand of financial industry, governments and enterprises for network connectivity. | Tencent Cloud IPsec VPN network transmission is based on the PSK encryption of IKE protocol, which meets the security requirements for network transmission. |
| Network address translation | Tencent Cloud Direct Connect supports configuring the network address translation service on gateways, as well as IP mapping at the two ends of Direct Connect and IP port mapping at the VPC end, to avoid address conflict in case of interconnection among multiple third-party networks. | Not supported |




### Why there is no traffic on both ends of a connected VPN tunnel or the Ping test between the both ends failed?
For specific reasons, see [Common Connection Problems with VPC](/document/product/215/17011).

### Can I access the Internet through a VPN connection?
No. Tencent Cloud VPN Connection product provides services by abiding by relevant national policies and regulations. A VPN gateway only supports connecting to a VPC, but is not used to access the Internet.

