
[](id:01)
### How do I specify the local and peer IP ranges when I create an SSL VPN server?
- Tencent Cloud IP range: Enter the Tencent Cloud IP range to be accessed by mobile clients, which is the IP range of the subnet in which your VPN gateway resides. For example, enter 10.0.0.0/24, 10.0.0.0/26, 10.0.0.0/28, or 10.0.0.0/30 for the 10.0.0.0/18 subnet.
- Client IP range: Enter the IP range that the SSL VPN gateway assigns to the client for communication with Tencent Cloud. You can enter any IP range whose subnet mask is less than or equal to 24. Take note that the IP range must not conflict with the VPC CIDR of Tencent Cloud or your local private network.
  

[](id:02)
### Why does the SSL connection fail?
1. The public network connection failed. Check the connectivity of the public network.
2. The public IP address is invalid. You cannot use a cross-border public IP address to access cloud resources.
3. Subnet routing is not configured. For more information about how to configure subnet routing, see [Step 4: Configure the Tencent Cloud Routing Policy](https://intl.cloud.tencent.com/document/product/1037/43902).
4. The SSL client certificate is used by multiple users. Only one user can use the SSL client certificate.

[](id:03)
### Can I change the number of SSL connections?
No. You must plan the number of SSL connections in advance. 

[](id:04)
### Does an SSL VPN require fixed public IP addresses?
No. SSL VPN connections do not require fixed IP addresses on the user side. An SSL VPN allows Windows, MAC, and Linux clients, as well as mobile phones that use OpenVPN, to connect to instances on Tencent Cloud VPCs.

[](id:05)
## Can I switch an SSL VPN to an IPsec VPN?
No, you cannot change the VPN gateway type.

[](id:06)
### Can multiple clients use the same certificate?
No, each SSL client configuration certificate can be used only by one client.

[](id:07)
### What is the maximum number of SSL connections allowed?
The maximum number of SSL connections allowed varies based on the bandwidth specification. A bandwidth specification of [5 Mbps, 100 Mbps] supports up to 100 SSL connections. A bandwidth specification of [200 Mbps, 500 Mbps] supports up to 500 SSL connections. A bandwidth specification of 1000 Mbps supports up to 1000 SSL connections.
