Note the following when using NAT gateways:
- If a NAT gateway is deleted, its EIP is disassociated from it, but the EIP will not be released.

- Security groups cannot be associated with the NAT gateway, but can be bound with the instances within the private subnet in order to control the traffic flow in and out of these instances.

- You cannot directly use the network ACL to control the traffic that flows in and out of the NAT gateway. Instead, you can use it to control the traffic of the associated subnet that flows in and out of the NAT gateway.

- You cannot use VPC Peering Connection, VPN Connection, or Direct Connect to route traffic to a NAT gateway. The NAT gateway cannot be used for resources that are connected to the other end.
For example, the flow of all traffic from VPC 1 to the Internet can be implemented by a NAT gateway. When a peering connection is established between VPC 1 and VPC 2, all the resources within VPC 2 can access all the resources within VPC 1, but none of the resources within VPC 2 can access the Internet through the NAT gateway.

- The NAT gateway supports TCP, UDP and ICMP, while ESP and AH for the GRE tunnel and IPSec cannot be used for the NAT gateway, and ALG technologies are also not supported. This results from the characteristics of the NAT gateway, and has nothing to do with the service provider. Most Internet applications use TCP, and 99% of Internet applications use TCP or UDP.

- The following table lists the restrictions on the supported resources for the NAT gateway. <!--For more information, see [Use Limits]()-->
<table>
<tbody>
<tr>
<th >Resource</th>
<th >Limit</th>
</tr>
<tr>
<td >Number of NAT gateways per VPC</td>
<td >3</td>
</tr>
<tr>
<td >Number of EIPs per NAT gateway</td>
<td>10</td>
</tr>
<tr>
<td >Maximum forwarding capability per NAT gateway</td>
<td>5 Gbps</td>
</tr>
<tr>
<td >Maximum number of port forwardings per NAT gateway</td>
<td >200</td>
</tr>
</tbody></table>
