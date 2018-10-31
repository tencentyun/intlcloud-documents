
VPN Connection is used to connect your customer IDC and Virtual Private Cloud (VPC) through an encrypted tunnel over public networks. As shown below, Tencent Cloud VPN Connection consists of the following components:
- VPN gateway: The IPsec VPN gateway created for your VPC.
- Customer gateway: The logical object that records the public IP address of the IPsec VPN gateway on IDC side.
- VPN tunnel: Encrypted IPsec VPN tunnel.

![](https://main.qcloudimg.com/raw/f0a32bf4771754cab3d6dbaf7da253d0.png)
You can create VPN gateways in a VPC and create multiple VPN tunnels on each VPN gateway, with each VPN tunnel establishing a connection between the VPC and a local IDC.
>**Note:**
>After establishing a VPN connection, you need to configure routing policies in the route table to enable real communication.

