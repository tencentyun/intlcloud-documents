## VPN Connections
Note the following when using a VPN connection:
- After configuring VPN parameters, **you need to add routing policies for your VPN gateway in the route table associated with the subnet**, so that network requests from CVMs in the subnet to access the customer IP range can reach the customer gateway through the VPN tunnel.
- After configuring the route table, **you need to ping an IP address in the customer IP range from a CVM in the VPC to activate the VPN tunnel.**
- The stability of the VPN connection depends on the ISP’s public network.
- The limits on resources are as follows:
<table><tbody>
<tr><th>Resource</th><th>Limit (quantity)</th></tr>
<tr><td>Number of VPN gateways in a VPC</td><td>10</td></tr>
<tr><td>Number of customer gateways in a region</td><td>20</td></tr>
<tr><td>Number of VPN tunnels supported by a customer gateway</td><td>10</td></tr>
<tr><td>Number of VPN tunnels can be created for a VPN gateway</td><td>20</td></tr>
<tr><td>Number of SPDs for a VPN tunnel</td><td>10</td></tr>
<tr><td>Number of customer IP ranges supported by an SPD</td><td>50</td></tr>
<tr><td>Number of VPN gateways for CCN in a region under an account</td><td>10</td></tr>
<tr><td>Number of routes supported by an VPN gateway route table</td><td>1000</td></tr>
<tr><td>Number of routes can be added once on the <b>Add a  route</b> page</td><td>10</td></tr>
</tbody></table>

>?
>- The number of VPN tunnels supported by a customer gateway is the quota for the account.
>- Only one VPN tunnel can be established between a pair of customer gateway and VPN gateway in a VPC.

## Customer Gateways
The following IP addresses cannot be used as the public IPs for a customer gateway:
- Multicast addresses that are all 0, all 225, or start with 224.
- Loopback addresses: `127.x.x.x/8`.
- IP Addresses with host bits being all 0 or all 1, for example:
 1. Class-A IP addresses that start with 1-126, such as `1-126.0.0.0` and `1-126.255.255.255`.
 2. Class-B IP addresses that start with 128-191, such as `128-191.x.0.0` and `128-191.x.255.255`.
 3. Class-C IP addresses that start with 192-223, such as `192-223.x.x.0` and `192-223.x.x.255`.
- Internal service addresses: `169.254.x.x/16`.

