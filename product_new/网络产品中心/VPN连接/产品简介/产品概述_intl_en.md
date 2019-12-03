
A VPN connection is used to connect your customer IDC and a Virtual Private Cloud (VPC) through an encrypted tunnel over a public network. As shown in the figure below, a VPN connection consists of the following parts:
- VPN gateway: An IPsec VPN gateway that is created for your VPC.
- Customer gateway: A logical object that records the public IP address of the IPsec VPN gateway on the IDC side.
- VPN tunnel: An encrypted IPsec VPN tunnel.

![](https://main.qcloudimg.com/raw/1b5ea6f4bbda1d71400ccd5d4618849b.png)
You can create a VPN gateway in a VPC and create multiple VPN tunnels for each VPN gateway. Each VPN tunnel can connect the VPC to a local IDC.
>**Notes:**
>After establishing a VPN connection, you need to configure routing policies in a route table to enable communication.
