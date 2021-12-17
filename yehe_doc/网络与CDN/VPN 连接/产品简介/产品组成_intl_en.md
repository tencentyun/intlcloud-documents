Tencent Cloud VPN supports the virtual network connections using IPSec and SSL protocols. It realizes a full connection among IDC, private office network, mobile client, and Tencent Cloud VPC.

## IPsec VPN 

### IPSec VPN gateway
An IPSec VPN gateway is an egress gateway for VPC or CCN to establish a VPN connection. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted communication between a Tencent Cloud VPC or CCN and an external IDC. Tencent Cloud VPN gateway uses software virtualization and an active-active hot backup architecture. When one server fails, automatic switchover helps ensure the normal operation of your businesses.

Eight bandwidth caps are available for a VPN gateway: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, and 1,000 Mbps.
If you need [Anti-DDoS Pro](https://intl.cloud.tencent.com/zh/document/product/1029) to defend against DDoS and CC attacks with high-bandwidth protection, you can bind it to the VPN gateway.

### Customer Gateway
A customer gateway is a logical object accompanied by a Tencent Cloud VPN gateway to record the fixed public IP address of the IPsec VPN gateway on the IDC side. Each VPN gateway can create encrypted VPN tunnels with multiple customer gateways.

### VPN Tunnel
After the VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC or CCN and an external IDC for encrypted communication. Currently, a VPN tunnel supports the IPsec encryption protocol, which can meet the requirements of most VPN connections.
A VPN tunnel runs on an ISP's public network, therefore, congestion or jitter on the public network may affect the VPN performance. If your business is sensitive to latency and jitter, we recommend that you connect the VPC or CCN via Direct Connect. For details, see [Direct Connect](https://intl.cloud.tencent.com/zh/product/dc).

## SSL VPN 

### SSL VPN gateway
An SSL VPN gateway is an egress gateway for VPC to establish an SSL VPN connection. It is used with an SSL VPN client (on mobile devices) to establish an encrypted communication between a Tencent Cloud VPC and a mobile client.

If you need [Anti-DDoS Pro](https://intl.cloud.tencent.com/zh/document/product/1029) to defend against DDoS and CC attacks with high-bandwidth protection, you can bind it to the VPN gateway.

### SSL VPN Server
The SSL VPN server is a service module in VPN gateway, which is used to encapsulate and de-encapsulate data packets. The configuration parameters include server IP range, client IP range, communication protocol, port and algorithm, etc. For details, see [Creating SSL VPN Server](https://intl.cloud.tencent.com/zh/document/product/1037/43905).

###  SSL VPN Client
The SSL VPN client connects to VPC through OpenVPN. It enables you to download the corresponding client configuration files and certificates. The client and server need mutual authentication, and only the authenticated client can communicate with the server.

