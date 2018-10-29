## VPN Connection
Please note the following when using VPN Connection:
- After the VPN parameters are configured, **you need to add routing policies for your VPN gateway in the route table associated with the subnet**, so that the access requests from CVMs within the subnet to customer IP address ranges can reach the customer gateway through the VPN tunnel.
- After the route table is configured, **you need to ping an IP in the customer IP address range from a CVM in the VPC to activate the VPN tunnel.**
- The stability of VPN connection depends on the performance of public network provided by ISPs. We cannot guarantee relevant service level with an SLA contract.
- Here are the limits on resources:
<table><tbody>
<tr><th>Resource</th><th>Limit</th></tr>
<tr><td>Number of VPN gateways per VPC</td><td>10</td></tr>
<tr><td>Number of customer gateways in a region</td><td>20</td></tr>
<tr><td>Number of VPN tunnels per customer gateway</td><td>10</td></tr>
<tr><td>Number of VPN tunnels that can be created in a VPN gateway</td><td>20</td></tr>
<tr><td>Number of SPDs per VPN tunnel</td><td>10</td></tr>
<tr><td>Number of customer IP address ranges per SPD</td><td>50</td></tr>
</tbody></table>

## Customer Gateway
The following IP addresses are not supported for the customer gateway:
- Multicast addresses all starting with 0 or 225/224.
- Loopback addresses: 127.x.x.x/8.
- Addresses with host bits all being 0 or 1, for example:
 1. Addresses starting with 1-126 in Class A, such as 1-126.0.0.0 and 1-126.255.255.255.
 2. Addresses starting with 128-191 in Class B, such as 128-191.x.0.0 and 128-191.x.255.255.
 3. Addresses starting with 192-223 in Class C, such as 192-223.x.x.0 and 192-223.x.x.255.
- Internal service addresses: 169.254.x.x/16.

