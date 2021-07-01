- The default route table of a VPC cannot be deleted. 
- After a VPC is created, its route table will be automatically provided with a default route, indicating that all resources in this VPC are interconnected through the private network. This routing policy cannot be modified or deleted.

<table>
<tbody>
<tr>
<th>Destination</th>
<th>Next hop type</th>
<th>Next hop</th>
</tr>
<tr>
<td>Local</td>
<td>Local</td>
<td>Local</td>
</tr>
</tbody>
</table>

- Dynamic routing protocols such as BGP and OSPF are not supported.
- The support for ECMP varies with routes, as shown in the following table.

<table><tbody>
<tr><th>Next hop type</th><th>Forming ECMP with the same type</th><th>Forming ECMP with another type</th><th>Maximum number of ECMPs</th</tr>
<tr><td>NAT Gateway</td><td>Supported</td><td>Supported, with public IP of CVM</td><td>Same type: up to 8; different types: 1</td></tr>
<tr><td>Inter-region peering connection</td><td>Not supported</td><td>Not supported</td><td>N/A</td></tr>
<tr><td>Cross-region peering connection</td><td>Not supported</td><td>Supported, with CCN</td><td>Different types: 1</td></tr>
<tr><td>Direct connect gateway</td><td>Not supported</td><td>Supported, with CCN</td><td>Different types: 1</td></tr>
<tr><td>HAVIP</td><td>Not supported</td><td>Not supported</td><td>N/A</td></tr>
<tr><td>VPN gateway</td><td>Not supported</td><td>Not supported</td><td>N/A</td></tr>
<tr><td>CVM</td><td>Supported</td><td>Supported, with public IP of CVM</td><td>Same type: up to 8; different types: 1</td></tr>
<tr><td>CCN</td><td>Not supported</td><td>Supported, with direct connect gateway or cross-region peering connection</td><td>Different types: 1</td></tr>
</tbody> </table>

>?
>- Equal Cost Multi-path (ECMP) means there are multiple equal-cost routes to a single destination.
>- That public IP of CVM has a higher priority than that of NAT Gateway when routing to the same destination.
> - Because of different priorities, EIP and other types of routes are not considered for ECMP.
> - Direct connect gateway and CCN can form ECMP. However, it will not check the route’s health status, or automatically exclude unhealthy routes. To form ECMP with CCN, first [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- Multiple NAT Gateway routes can form ECMP. However, it will not check the route’s health status, or automatically exclude unhealthy routes.
>- Multiple CVM routes can form ECMP. However, it will not check the route’s health status, or automatically exclude unhealthy routes.

- Routes can be published to CCN.
The following routes can be published to CCN.

<table>
<tr>
<th>Next hop type</th>
<th>Publishing to CCN by default</th>
<th>Manually publishing or withdrawing</th>
<th>Description</th>
</tr>
<tr>
<td>Local</td>
<td>Supported</td>
<td>Not supported</td>
<td>Assigned by the system. The VPC IP range connecting to CCN will be automatically published to CCN, including primary and secondary CIDR blocks (except for TKE IP ranges).</td>
</tr>
<tr>
<td>VPN Gateway</td>
<td>Not supported</td>
<td>Supported</td>
<td>A custom route to VPN gateway. When the IP range is all 0 or the routing policy is disabled, the route cannot be published to CCN.</td>
</tr>
<tr>
<td>CVM</td>
<td>Not supported</td>
<td>Supported</td>
<td>A custom route to CVM. When the IP range is all 0 or the routing policy is disabled, the route cannot be published to CCN.</td>
</tr>
<tr>
<td>HAVIP</td>
<td>Not supported</td>
<td>Supported</td>
<td>Custom route to HAVIP. When the IP range is all 0 or the routing policy is disabled, the routes cannot be published to CCN.</td>
</tr>
</table>

>?
> - A disabled custom route cannot be published to CCN.
> - To disable a custom route that has been published to CCN, first withdraw it.

### Quota Limits

<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>Number of route tables per VPC</td>
<td>10</td>
</tr>
<tr>
<td>Number of route tables associated with each subnet</td>
<td>1</td>
</tr>
<tr>
<td>Number of routing policies per route table</td>
<td>50</td>
</tr>
</table>
