A VPN connection is used to connect the customer IDC with a Virtual Private Cloud (VPC) or Cloud Connect Network (CCN) through an encrypted tunnel over the public network. After a VPN connection is established, you can configure routing policies in the route table to facilitate the communication. Tencent Cloud VPN connection consists of the following components:
- VPN gateway: an IPsec VPN gateway.
 - VPN gateway for VPC: VPN gateway can be created in a VPC. Each VPN gateway for VPC can create multiple VPN tunnels. Each VPN tunnel can connect one local IDC.
 - VPN gateway for CCN: VPN gateway can be associated with CCN. Each VPN gateway for CCN can create multiple VPN tunnels. Each VPN tunnel can connect one local IDC. The VPN gateway for CCN is now in beta test. To apply for it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- Customer gateway: a logical object that records the fixed public IP address of the IPsec VPN gateway on the IDC side.
- VPN tunnel: an encrypted IPsec VPN tunnel.

![](https://main.qcloudimg.com/raw/b408d142266092bc5f75a8bbd659c20a.png)


