## VPN Connections
Note the following when using a VPN connection:
- After configuring VPN parameters, **you need to add routing policies for your VPN gateway in the route table associated with the subnet**, so that network requests from CVMs in the subnet to access the peer IP range can reach the customer gateway through the VPN tunnel.
- After configuring the route table, **you need to ping an IP address in the peer IP range from a CVM in the VPC to activate the VPN tunnel.**
- The stability of the VPN connection depends on the ISP's public network.
- The limits on resources are as follows:
<table><tbody>
<tr>
<tr>Resource</th><th>Limit (quantity)</th>
</tr>
<tr>
<td>VPN gateways in one VPC</td>
<td>10</td>
<tr>
<td>Customer gateways in one region</td>
<td>20</td>
</tr>
<tr>
<td>VPN tunnels supported by one customer gateway</td>
<td>20</td>
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
<td>Number of CCN-type VPN gateways per account per region</td>
<td>10</td>
</tr>
<tr>
<td>Routes supported by each VPN gateway route table</td>
<td>1,000</td>
</tr>
<tr>
<td>Number of routes can be added at one time on the console</td>
<td>10</td>

</tr>
</tbody></table>

>?
>- The number of VPN tunnels supported by a customer gateway is the quota for the account.
>- Only one VPN tunnel can be established between a pair of customer gateway and VPN gateway in a VPC.
>- To increase the quota, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.
>

## Customer Gateway
The following IP addresses CANNOT be used as the public IPs for a customer gateway:
- Multicast addresses that are all 0, all 225, or start with 224.
- Loopback addresses: `127.x.x.x/8`.
- IP Addresses with host bits being all 0 or all 1, for example:
 1. Class-A IP addresses that start with 1-126, such as `1-126.0.0.0` and `1-126.255.255.255`.
 2. Class-B IP addresses that start with 128-191, such as `128-191.x.0.0` and `128-191.x.255.255`.
 3. Class-C IP addresses that start with 192-223, such as `192-223.x.x.0` and `192-223.x.x.255`.
- Internal service addresses: `169.254.x.x/16`.

