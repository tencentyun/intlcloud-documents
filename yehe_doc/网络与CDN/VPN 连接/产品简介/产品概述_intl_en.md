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
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ThnQ702_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230228164524.png)

## SSL VPN
Tencent Cloud SSL VPN Connections consists of the following components:
- SSL VPN gateway: a VPN gateway using the SSL protocol
- SSL VPN server: a service module that provides SSL services and is used to encapsulate and de-encapsulate data packets and negotiate the communication port, encryption algorithm, and IP ranges for interconnection.
- SSL VPN client: a VPN client that is deployed on user terminals and is considered a logical instance on Tencent Cloud.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vLki069_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230228164543.png)
