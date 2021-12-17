>? SSL VPN is in beta test. To try it out, please [submit an application](https://cloud.tencent.com/apply/p/xhfe94i9u8f).
>

## Prerequisites
- The local private IP range and the Tencent Cloud VPC cannot overlap. 
- The client has connected to the public network.

## Configuration
![](https://qcloudimg.tencent-cloud.cn/raw/aa83c71919f5f685999a1a5690ab90c2.png)
1. [Create an SSL VPN gateway](https://intl.cloud.tencent.com/document/product/1037/43919).
Create a VPN gateway using the SSL protocol
2. [Create an SSL VPN server](https://intl.cloud.tencent.com/document/product/1037/43905).
Specify the Tencent Cloud IP range and the client IP range to connect in the SSL VPN server.
3. [Create an SSL VPN client](https://intl.cloud.tencent.com/document/product/1037/43920).
The client uses certificate and key to connect with the VPN gateway. The client and the server verify each other’s certificate. After verification, the server assigns an IP from the client IP address pool to the client for connecting with CVMs in VPC.
4. [Configure a route within VPC](https://intl.cloud.tencent.com/document/product/1037/39690).
Configure the routing and forwarding policies for the mobile client to connect with Tencent Cloud VPC. Set an address of the client IP range as the destination, and VPN tunnel as the next hop type. Next hop to SSL VPN gateway.
5. Configure the client on the mobile device.
Configure the SSL certificate on the mobile device.
6. Test the connectivity 
 Use `ping` to verify the connectivity of SSL VPN connection after the above configurations.
