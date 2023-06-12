## VPN Connections
Note the following when using a VPN connection:
 - After configuring VPN parameters, you need to add routing policies for your VPN gateway in the route table associated with the subnet, so that network requests from CVMs in the subnet to access the peer IP range can reach the customer gateway through the VPN tunnel.
 - For a VPN gateway v1.0, after configuring the route table, you need to ping an IP address in the peer IP range from a CVM in the VPC to activate the VPN tunnel.
 - The stability of the VPN connection depends on the ISP's public network.
 - The VPN connection only supports the PSK authentication method rather than CA authentication.
 - SPD or route IP ranges of the VPN connection cannot be specified as the following IP ranges:
   - Multicast addresses that are all 0, all 225, or start with 224.
   - Loopback addresses: 127.x.x.x/8.
   - IPv6 IP ranges.

## VPN Gateway
 - VPN Connections is a region-level service, but you can also connect to your VPN gateway in any region over the internet.
 - You cannot specify a public IP or the ISP of the public IP for the VPN gateway. IPv6 and anycast IP addresses are also not supported.
 

## Customer Gateway
 - You must specify the IP address of the customer gateway. The public IP of the customer gateway cannot be the following IP addresses:
   - Multicast addresses that are all 0, all 225, or start with 224.
   - Loopback addresses: 127.x.x.x/8.
   - IP Addresses with host bits being all 0 or all 1, for example:
     - Class-A IP addresses that start with 1-126, such as `1-126.0.0.0` and `1-126.255.255.255`.
     - Class-B IP addresses that start with 128-191, such as `128-191.x.0.0` and `128-191.x.255.255`.
     - Class-C IP addresses that start with 192-223, such as `192-223.x.x.0` and `192-223.x.x.255`.
   - Internal service addresses: `169.254.x.x/16`.
   - IPv6 addresses.
 - If you use an IPsec VPN connection to interconnect resources in two VPCs, the VPCs are each other's customer gateway, and their IP ranges cannot overlap.

## SSL VPN Server
 - The server supports only UDP but not TCP.
 - To modify information such as port, authentication method, and encryption algorithm, you need to download the client configuration again.
 - The client and local IP ranges cannot overlap.
 - Identity verification relies on an EIAM application and cannot be directly interconnected with other identity providers (IdPs) for verification. You can use EIAM to interconnect with the verification source of your enterprise. You can also select a verification method supported by EIAM, such as SMS, WeCom, and AD. Currently, identity verification is in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
 - You can use CAM if identity verification is enabled.

## SSL VPN Client
 - You need to prepare the client on your own. An SSL VPN connection supports the open-source OpenVPN client or other compatible commercial clients.
 - Each client can use only one SSL client configuration certificate. You cannot use the same certificate for multiple clients.
 - Supported OpenVPN versions: 2.4.8–3.x.
 - Identity verification is supported only by OpenVPN 3.x or other compatible clients.

## Resource Limits

### Limits on IPsec VPN
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>VPC IPsec VPN gateways per region per account</td>
<td>10</td>
</tr>
<tr>
<td>CCN IPsec VPN gateways per region per account</td>
<td>10</td>
</tr>
<tr>
<td>Customer gateways in one region</td>
<td>20</td>
</tr>
<tr>
<td>VPN tunnels supported by one customer gateway</td>
<td>20

<dx-alert infotype="explain" title="">
- The number of VPN tunnels supported by a customer gateway is the quota for the account.
- Only one VPN tunnel can be established between a pair of customer gateway and VPN gateway.
</dx-alert>
</td>
</tr>
<tr>
<td>VPN tunnels that can be created on one VPN gateway</td>
<td>20</td>
</tr>
<tr>
<td>SPDs in a VPN tunnel</td>
<td>10</td>
</tr>
<tr>
<td>Peer IP ranges supported by a SPD</td>
<td>50</td>
</tr>
<tr>
<td>Routes supported by each VPN gateway route table</td>
<td>1,000</td>
</tr>
<tr>
<td>Number of routes can be added at one time on the console</td>
<td>10</td>
</tr>
</table>

### Limits on SSL VPN
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>VPC SSL VPN Gateways per Region per Account</td>
<td>10</td>
</tr>
<tr>
<td>SSL VPN servers that can be created for an SSL VPN gateway</td>
<td>1</td>
</tr>
<tr>
<td>Local IP ranges that can be added on an SSL VPN server</td>
<td>100</td>
</tr>
<tr>
<td>Client IP ranges that can be added on an SSL VPN server</td>
<td>1
<dx-alert infotype="explain" title="">
To ensure that all your clients can be assigned an IP address, we recommend you specify a client IP range containing IP addresses more than the SSL VPN connections.
</dx-alert>
</td>
</tr>
<tr>
<td>Validity period of the SSL VPN client certificate</td>
<td>In 3</td>
</tr>
<tr>
<td>SSL VPN connections</td>
<td><ul><li>A [5,100] Mbps SSL VPN gateway can sustain up to 100 SSL VPN connections.</li><li>A 200/500 Mbps SSL VPN gateway can sustain up to 500 SSL VPN connections.</li><li>A 1,000 Mbps SSL VPN gateway can sustain up to 1,000 SSL VPN connections.</li></ul>
<dx-alert infotype="explain" title="">
The maximum number of SSL VPN connections is the number of connections to the client. Once it is configured, it cannot be modified. Therefore, plan an appropriate value before configuration.
</dx-alert>
</td>
</tr>
<tr>
<td>Ports not supported by the SSL VPN server</td>
<td>The protocol port cannot be 123, 53, 22, 36000, 54000, 50051, 68, 500, or 4500.</td>
</tr>
</table>
