A VPN connection consists of a VPN gateway, a customer gateway, and a VPN tunnel.
## VPN Gateway
A VPN gateway is an egress gateway for VPC or CCN to establish a VPN connection. It is accompanied by a customer gateway (IPsec VPN gateway on the IDC side) to establish encrypted communication between a Tencent Cloud VPC or CCN and an external IDC. Tencent Cloud VPN gateway uses the software virtualization technology and a dual-server hot backup architecture. Therefore, when one server fails, the automatic switchover to the other server can still ensure the normal operation of your business.

Eight bandwidth caps are available for a VPN gateway: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, and 1,000 Mbps.
If you need [Anti-DDoS Pro](https://intl.cloud.tencent.com/zh/document/product/1029) to defend against DDoS and CC attacks with high-bandwidth protection, you can bind it to the VPN gateway.

## Customer Gateway
A customer gateway is a logical object accompanied by a Tencent Cloud VPN gateway to record the fixed public IP address of the IPsec VPN gateway on the IDC side. Each VPN gateway can create encrypted VPN tunnels with multiple customer gateways.

## VPN Tunnel
After the VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC or CCN and an external IDC for encrypted communication. Currently, a VPN tunnel supports the IPsec encryption protocol, which can meet the requirements of most VPN connections.
A VPN tunnel runs on an ISP's public network, therefore, congestion or jitter on the public network may affect the VPN performance. If your business is sensitive to latency and jitter, we recommend that you connect the VPC or CCN via Direct Connect. For more information, see [Direct Connect](https://intl.cloud.tencent.com/product/dc).
