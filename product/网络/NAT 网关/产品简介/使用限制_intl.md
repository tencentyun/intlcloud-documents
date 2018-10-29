Take note of the following when using NAT gateways:
- If a NAT gateway is deleted, its EIP is disassociated from it, but not released from the account.

- Security groups cannot be associated with the NAT gateway, but can be bound with the instances within the private subnet in order to control the traffic flowing in and out of these instances.

- You cannot use a network ACL to control the traffic flowing in and out of a NAT gateway, but you can use it to control the associated subnet's traffic flowing in and out of the NAT gateway.

- You cannot use VPC Peering Connection, VPN Connection, or Direct Connect to route traffic to a NAT gateway. The NAT gateway cannot be used for resources that are connected to the other end.
For example, the flow of all the traffic from VPC 1 to the Internet is enabled by a NAT gateway. When a peering connection is established between VPC 1 and VPC 2, all the resources within VPC 2 can access all the resources within VPC 1, but none of the resources within VPC 2 can access the Internet through the NAT gateway.

- Supported protocols for the NAT gateway include TCP, UDP, and ICMP, while ESP and AH for the GRE tunnel and IPSec cannot be used for the NAT gateway. This is a result of the characteristics of the NAT gateway itself, and has nothing to do with the ISP. Nonetheless, TCP is a dominant type of application in the Internet field, and, together with UDP, account for 99% of all Internet applications.

- The restrictions on the supported resources for the NAT gateway are shown below. You can also refer to [Use Limits on Other VPC Products](/doc/product/215/537).
<table>
<tbody>
<tr>
<th >Resources</th>
<th >Limit</th>
</tr>
<tr>
<td >Number of NAT gateways per VPC</td>
<td >3</td>
</tr>
<tr>
<td >Number of EIPs per NAT gateway</td>
<td >10</td>
</tr>
<tr>
<td >Maximum forwarding capacity per NAT gateway</td>
<td >5 Gbps</td>
</tr>
<tr>
<td >Maximum port forwarding entries per NAT gateway</td>
<td >200</td>
</tr>
</tbody></table>

