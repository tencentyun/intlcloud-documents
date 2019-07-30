## 1. Can a VPC connect to multiple IDCs through VPN connections?
Yes. Currently, a VPC can establish VPN gateways and set up multiple VPN tunnels on each VPN gateway. Each VPN tunnel can connect with one local IDC.

## 2. Can the communication between two VPCs be achieved via VPN connections?
Yes. You need to purchase VPN gateways, and configure VPN tunnels and peer gateways in two VPCs. Since the configuration is complicated, we recommend you use a peering connection. Peering connection uses Tencent Backbone Network to connect two VPCs, which can ensure the communication quality.

## 3. How is the network quality between the VPC and the IDC connected through the VPN ensured?
- The communication between the VPC and the IDC is made through a public network, which therefore depends on the quality of the public network. Latency, packet loss, and jitter are all possible. If you need more stable communication quality, we recommend that you use the Direct Connect service.
- The VPN backend will monitor the network quality throughout the day, including keepalive and network latency. If there are network anomalies, it will inform the O&M personnel to deal with them in a timely manner. You can also monitor the traffic status of VPN gateways and tunnels in real time in the console. Contact us if you find anomalies.
