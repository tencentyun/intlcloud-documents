A VPN connection is used to connect your customer IDC to a Virtual Private Cloud (VPC) or Cloud Connect Network (CCN) through an encrypted tunnel over public networks. After establishing a VPN connection, you need to configure routing policies in the route table to facilitate the communication. As shown below, a Tencent Cloud VPN connection consists of:
- VPN gateway: an IPsec VPN gateway that is created for your VPC or CCN.
 - VPN gateway for VPC: you can create a VPN gateway in a VPC and create multiple VPN tunnels for each VPN gateway. Each VPN tunnel can connect a local IDC to VPC.
 - VPN gateway for CCN: you can associate a VPN gateway with a CCN and create multiple VPN tunnels for each VPN gateway. Each VPN tunnel can connect a local IDC to CCN. The VPN gateway for CCN is now in beta. To apply for it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Customer gateway: a logical object that records the fixed public IP address of the IPsec VPN gateway on the IDC side.
- VPN tunnel: an encrypted IPsec VPN tunnel.

![](https://main.qcloudimg.com/raw/394a25aeec1f1250aed35b97fdbb1793.png)


