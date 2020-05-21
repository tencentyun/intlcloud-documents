## VPN Connections
Pay attention to the following points when you use a VPN connection:
- After configuring VPN parameters, **you need to add routing policies for your VPN gateway in the route table associated with the subnet**, so that access requests from CVMs in the subnet to the customer IP range can reach the customer gateway through the VPN tunnel.
- After configuring the route table, **you need to ping an IP address in the customer IP range from a CVM in the VPC to activate the VPN tunnel.**
- The stability of the VPN connection depends on the performance of the ISP’s public network. Currently, no SLA can be assured.
- The limits on resources are as follows:
<table><tbody>
<tr><th>Resource</th><th>Limit (quantity)</th></tr>
<tr><td>Number of VPN gateways in a VPC</td><td>10</td></tr>
<tr><td>Number of customer gateways in a region</td><td>20</td></tr>
<tr><td>Number of VPN tunnels supported by a customer gateway</td><td>10</td></tr>
<tr><td>Number of VPN tunnels that can be created for a VPN gateway</td><td>20</td></tr>
<tr><td>Number of SPDs for a VPN tunnel</td><td>10</td></tr>
<tr><td>Number of customer IP ranges supported by an SPD</td><td>50</td></tr>
<tr><td>Number of VPN gateways for CCN in a region under an account</td><td>10</td></tr>
</tbody></table>

>
>- The number of tunnels supported by a customer gateway is the quota for the account.
>- Only one VPN tunnel can be established between one customer gateway and the same VPN gateway in a VPC.


## Customer Gateways
The following IP addresses cannot be used for a customer gateway:
- Multicast addresses with all being 0 or 225, or starting with 224.
- Loopback addresses: `127.x.x.x/8`.
- Addresses with host bits all being 0 or 1, for example:
 1. Class-A IP addresses that start with 1-126, such as `1-126.0.0.0` and `1-126.255.255.255`.
 2. Class-B IP addresses that start with 128-191, such as `128-191.x.0.0` and `128-191.x.255.255`.
 3. Class-C IP addresses that start with 192-223, such as `192-223.x.x.0` and `192-223.x.x.255`.
- Internal service addresses: `169.254.x.x/16`.

