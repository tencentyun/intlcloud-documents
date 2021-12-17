VPN Connections aims to create a secure network connection over the public network. It can securely connect the customer IDC to the private office network and the Tencent Cloud VPC through an encrypted tunnel over the public network.

Tencent Cloud VPN supports both IPsec and SSL network security protocols. 


## IPsec VPN
Tencent Cloud VPN Connections consists of the following components:
- VPN gateway: an IPsec VPN gateway.
 - VPN gateway for VPC: if you need to communicate with a single VPC, you can connect to the VPC via the VPN gateway for VPC.
 - VPN gateway for CCN: if you need to communicate with multiple VPCs, you can connect to CCN via the VPN gateway for CCN to realize traffic interconnection.
>? Each VPN gateway can create multiple VPN tunnels, each of which can connect the VPC to a local IDC.
>
- Customer gateway: a logical object that records the fixed public IP address of the IPsec VPN gateway on the IDC side.
- VPN tunnel: an encrypted IPsec VPN tunnel.
![](https://main.qcloudimg.com/raw/b408d142266092bc5f75a8bbd659c20a.png)


## SSL VPN
>? The SSL VPN is in beta test now. To try it out, please [submit an application.] (https://console.cloud.tencent.com/workorder/category).
>
Tencent Cloud SSL VPN Connections consists of the following components:
- SSL VPN gateway: a VPN gateway using the SSL protocol
- SSL VPN server: a module providing SSL services
- SSL VPN client: providing a certificate for connecting the mobile client to the server
![]()
