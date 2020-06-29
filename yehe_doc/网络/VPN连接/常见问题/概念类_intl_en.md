### What is a VPN connection?
A VPN connection is used to connect your customer IDC and a VPC through an encrypted tunnel on a public network. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1037/32679).

### What is a VPN tunnel?
After VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC and an external IDC for encrypted communication. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1037/32679).

### What is a VPN gateway?
A VPN gateway is an egress gateway for VPC to establish a VPN connection. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted communication between a Tencent Cloud VPC and an external IDC. Tencent Cloud VPN gateway uses software virtualization and an active-active hot backup architecture. When one server fails, automatic switchover helps ensure the normal operation of your businesses.
- Eight bandwidth caps are available for a VPN gateway: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, and 1000 Mbps. You can adjust the bandwidth setting for a VPN gateway, and the adjustment takes effect immediately for a pay-as-you-go VPN gateway.
- You can bind an Anti-DDoS instance to a VPN gateway to defend against DDoS and CC attacks with high-bandwidth protection.

### What is an IPsec VPN?
 [IPsec VPN](https://intl.cloud.tencent.com/document/product/1037/32680) is used to connect customer IDC with a VPC through an encrypted tunnel over a public network. Tencent Cloud IPsec VPN connection consists of the following components:
- **VPN gateway**: an IPsec VPN gateway in a VPC. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted communication between the VPC and your IDC.
- **Customer gateway**: an IPsec VPN gateway on the IDC side that is mapped to the VPC. It is used with a VPN gateway. Each VPN gateway can create encrypted VPN tunnels with multiple customer gateways.
- **VPN tunnel**: an encrypted IPsec VPN tunnel over the public network. After the VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC and an external IDC for encrypted communication.

### What roles does the VPN gateway bandwidth limit play?
The VPN gateway bandwidth limit provides **monitoring** and **control** capabilities at IP-gateway granularity. For more information about its roles and advantages, see the “VPN gateway bandwidth limit” section in [Features](https://intl.cloud.tencent.com/document/product/1037/32681)

### What are the limitations on using a VPN?
 To use a VPN, take notice of the limitations on IP addresses of the VPN connection and the customer gateway. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/1037/32682).

### How many VPN gateways and VPN tunnels can I create?
The creation limit varies depending on the resources. To increase the limit, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC).

### Can a VPC connect to multiple IDCs through VPN connections?
Yes. You can create VPN gateways in a VPC and create multiple VPN tunnels for each VPN gateway. Each VPN tunnel connects the VPC to one local IDC.

### Can two VPCs communicate with each other through a VPN connection?
Yes. You need to separately purchase VPN gateways and configure VPN tunnels and customer gateways in the two VPCs, but the configuration is complex. So we recommend using [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/product/ccn) to connect two VPCs over the Tencent Cloud private network and help ensuring the communication quality.

### How do I ensure the network quality between a VPC and a VPN-connected IDC?
- Because a VPC connects to an IDC through a VPN connection on the public network, latency, packet loss, or jitter on the public network may affect the VPN connection. If you require more stable communication, we recommend that you use [Direct Connect](https://intl.cloud.tencent.com/doc/product/216).
- Tencent Cloud provides 24-hour monitoring on your VPN gateways and reports alarms for exceptions. OPS personnel are available for emergencies. You can also monitor the traffic of your VPN gateways and tunnels on the Console in real time. In case of any exceptions, [contact us](https://intl.cloud.tencent.com/support) promptly.

### What is the difference between a Direct Connect and an IPSec VPN Connection?
- An IPsec VPN connection uses the public network and IPsec protocol to establish an encrypted network connection between your IDC and a VPC. You can purchase, configure and validate a VPN gateway in several minutes. However, the VPN connection may be interrupted due to jitter or congestion on the public network. When your business does not require quality network connections, you can use this option for a quick and cost-effective deployment.
- A Direct Connect provides a network connection solution dedicated to your business. The configuration may take a longer time, but it can provide a highly reliable network connection. When your businesses have a higher requirement for the network quality and security, this option fits in.

The table below lists their specific differences.
<table>
<thead>
<tr>
<th width="20%">Advantage</th>
<th>Direct Connect</th>
<th>IPsec VPN</th>
</tr>
</thead>
<tbody><tr>
<td>Stable network latency</td>
<td>Network latency is stable and guaranteed. A Direct Connect accesses the network through dedicated links, which you can configure with fixed routes, removing the pain of unstable latency caused by network congestion or the need to bypass failures.</td>
<td>Network latency is unstable. An IPsec VPN accesses the network over Internet, which may be exposed to bypass due to network congestion.</td>
</tr>
<tr>
<td>Highly reliable disaster recovery access</td>
<td>Access devices and network forwarding devices are deployed in distributed clusters to ensure high reliability of all links. It also supports dual-line access with protection to guarantee an availability that is higher than 99.95%. </td>
<td>Feature an active-active hot backup architecture with high availability at the gateway layer. However, it cannot provide the same network availability as dedicated lines due to the unreliable Internet links.</td>
</tr>
<tr>
<td>Large bandwidth</td>
<td>It provides up to 10 Gbps for each link and you can also have multiple 10 Gbps links for network load balancing, so it can theoretically support unlimited bandwidth.</td>
<td>A single IPsec VPN supports a bandwidth of up to 100 Mbps and a VPC can have multiple VPN gateways, which can meet the need for a VPN connection larger than 100 Mbps.</td>
</tr>
<tr>
<td>High security</td>
<td>Exclusive network links offer high security with no risk of data leakage, satisfying the demanding network connection requirements of the finance and government sectors.</td>
<td>Network transmission is secured by pre-shared key encryption based on the IKE protocol, which can satisfy the security requirements for most network transmission.</td>
</tr>
<tr>
<td>Network address translation</td>
<td>If supports configuring the network address translation service on gateways, as well as IP mapping on the two sides of Direct Connect and IP port mapping on the VPC side, to avoid address conflict in case of interconnection among multiple third-party networks.</td>
<td>Not supported.</td>
</tr>
</tbody></table>

### Why is there no traffic on both sides of a connected VPN tunnel, or why does a ping test between both sides fail?
Check that the SPD policy (proxy identity), route table, and security group are properly configured.
1. Check the SPD policies configured on both sides.
Check that the proxy identity is properly configured on both sides of the VPN tunnel. If VPN traffic passes a NAT device, ensure that active traffic accessing Tencent Cloud flows to and activates the VPN tunnel rather than being matched by the NAT device.
2. Check the routing configurations on both sides.
Make sure that a routing policy destined for the customer private network has been created in the route table and the route points to the VPN gateway.
3. Check the security policies configured on both sides to verify the following points:
 - The security group's outbound policy of your CVM allows to access the customer IP range, and the inbound policy allows the customer IP range to access your CVM.
 - The security policy of your customer VPN gateway allows the interconnection between your private network server and the CVM.
 - There is no security restriction on the communication between your customer private network server and the VPN device.
 - The subnet of the VPC is bound to a network ACL, and the access IP range is opened.

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) to contact us.

### Can I access the Internet through a VPN connection?
No. VPN gateways only provide access to VPCs but not to the Internet.
