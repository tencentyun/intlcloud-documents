### What is an IPsec VPN?
 [IPsec VPN](https://cloud.tencent.com/document/product/554/19276) is used to connect your IDC and a VPC through an encrypted tunnel over a public network. The IPsec VPN connection to a Tencent Cloud VPC consists of the following parts:
- **VPN gateway**: An IPsec VPN gateway in a VPC. It is used with a customer gateway (the IPsec VPN gateway in your IDC) to establish an encrypted network tunnel between the VPC and your IDC for secure and reliable communication.
- **Customer gateway**: A VPC gateway that is mapped to the IPsec VPN gateway in your IDC. It is used with a VPN gateway. Encrypted VPN tunnels can be established between a VPN gateway and multiple customer gateways.
- **VPN tunnel**: An encrypted IPsec VPN tunnel over a public network. After the VPN gateway and customer gateway are created, a VPN tunnel can be established for encrypted communication between the VPC and your IDC.

### Can a VPC connect to multiple IDCs through VPN connections?
Yes. You can create VPN gateways in a VPC and create multiple VPN tunnels for each VPN gateway. Each VPN tunnel connects the VPC to a local IDC.

### Can two VPCs communicate with each other through a VPN?
Yes. You need to separately purchase VPN gateways and configure VPN tunnels and customer gateways in the two VPCs, but the configuration is complex. It is recommended that you use [Cloud Connect Network (CCN)](https://cloud.tencent.com/product/ccn). CCN connects two VPCs via Tencent’s private network, ensuring the quality of communication.

### How do I ensure the network quality between a VPC and IDC that are connected through a VPN?
- Packets are transmitted over public networks through the VPN connection between a VPC and an IDC. Therefore, the overall network quality depends on the quality of the public networks. When delay, packet loss, or jitter occurs on the public networks, the VPN connection is also affected. If you require more stable communication, it is recommended that you use [Direct Connect](https://cloud.tencent.com/doc/product/215/4976).
- Tencent Cloud provides 24-hour monitoring on your VPN gateways and reports alarms for exceptions. OPS personnel are available for emergencies. You can also monitor the traffic of your VPN gateways and tunnels on the console in real time. If any exceptions occur, [contact us](https://cloud.tencent.com/about/connect) promptly.

### Why is there no traffic at both ends of a connected VPN Tunnel, or why does a ping test between both ends fail?
Check whether the SPD policy (proxy identity), route table, and security group are properly configured.
1. Check the SPD policies configured at both ends.
Check whether the proxy identity is properly configured at both ends of the VPN tunnel. If VPN traffic passes a NAT device, prevent the traffic accessing Tencent Cloud from missing the VPN tunnel due to matching by the NAT device, which will otherwise cause the VPN tunnel to be inactive because no active traffic is available.
2. Check the routing configurations at both ends.
Make sure that a routing policy with the customer private network as a destination has been created in the route table and the route points to the VPN gateway.
3. Check the security policies configured at both ends to verify the following points:
 - Whether the security group's outbound policy of your CVM allows to access the customer IP range, and the inbound policy allows the customer IP range to access your CVM.
 - Whether your customer VPN gateway's security policy allows mutual access between your private network server and the CVM.
 - Whether there is any security restriction on the communication between your customer private network server and the VPN device.
 - Whether the subnet of the VPC is bound to a network ACL (if so, the access to the related IP range must be allowed).

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) to contact us.

### Can I access the Internet through a VPN connection?
No. VPN gateways only provide access to VPCs but not to the Internet.
