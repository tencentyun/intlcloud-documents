## Prerequisite
The local private IP range and the Tencent Cloud VPC cannot overlap.

## Configuration
![]()
1. [Create an IPSec VPN gateway](https://intl.cloud.tencent.com/document/product/1037/39688)
    Create a VPN gateway using the IPSec protocol.
2. [Create a customer gateway](https://intl.cloud.tencent.com/document/product/1037/39691)
   Specify the Tencent Cloud IP range and the client IP range to connect in the SSL VPN server.
3. [Create a VPN tunnel](https://intl.cloud.tencent.com/document/product/1037/39634)
    The client uses certificate and key to connect with the VPN gateway. The client and the server verify their certificates bidirectionally. After verification, the server assigns an IP from the client IP address pool to the client for connecting with CVM in VPC.
4. Configure a local gateway.
    Complete the gateway configuration at the client side.
>! Tencent IPSec VPN supports the mainstream client gateway (firewall) in the industry. See [Local Gateway Configurations](https://intl.cloud.tencent.com/document/product/1037/40708).
>
5. [Configure a route within VPC](https://intl.cloud.tencent.com/document/product/1037/39690).
    Configure the routing and forwarding policies for the IDC to connect with Tencent Cloud VPC. Set the the IP range of the opposite network as the destination address, and VPN tunnel or CCN as the next hop type.
  - **VPN tunnel**: select an existing VPN tunnel
  - **CCN**: the CCN instance associated with the VPN gateway is displayed here
6. Test the connectivity 
    Use `ping` to verify the connectivity of IPSec VPN connection after the above configurations.
