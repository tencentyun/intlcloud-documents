### Use Limits
- The default route table of a VPC cannot be deleted. 
- After a VPC is created, its route table will be automatically provided with a default route, indicating that all resources in this VPC are interconnected through the private network. This routing policy cannot be modified or deleted.
<table><tbody>
<tr><th>Destination</th><th>Next hop type</th><th>Next hop</th></tr>
<tr><td>Local</td><td>Local</td><td>Local</td></tr>
</tbody> </table>
- Dynamic routing protocols such as BGP and OSPF are not supported.
- The support for ECMP varies with routes, as shown in the following table.
<table><tbody>
<tr><th>Next hop type</th><th>Forming ECMP with the same type</th><th>Forming ECMP with another type</th><th>Maximum ECMP</th</tr>
<tr><td>NAT Gateway</td><td>Supported</td><td>Supported, with public IP of CVM</td><td>Up to 8 for the same type, and 1 for a different type</td></tr>
<tr><td>Inter-region peering connection</td><td>Not supported</td><td>Not supported</td><td>N/A</td></tr>
<tr><td>Cross-region peering connection</td><td>Not supported</td><td>Supported, with CCN</td><td>Up to 1 for a different type</td></tr>
<tr><td>Direct connect gateway</td><td>Not supported</td><td>Supported, with CCN</td><td>Up to 1 for a different type</td></tr>
<tr><td>HAVIP</td><td>Not supported</td><td>Not supported</td><td>N/A</td></tr>
<tr><td>VPN gateway</td><td>Not supported</td><td>Not supported</td><td>N/A</td></tr>
<tr><td>Public IP of CVM</td><td>Not supported</td><td>Supported, with CVM or NAT Gateway</td><td>Up to 1 for a different type</td></tr>
<tr><td>CVM</td><td>Supported</td><td>Supported, with public IP of CVM</td><td>Up to 8 for the same type, and 1 for a different type</td></tr>
<tr><td>CCN</td><td>Not supported</td><td>Supported, with direct connect gateway or cross-region peering connection</td><td>Up to 1 for a different type</td></tr>
</tbody> </table>

 >?
>+ Equal Cost Multi-path (ECMP) means that multiple equal-cost routes to a single destination exist.
>+ To the same destination, the public IP of CVM has a higher priority than that of NAT Gateway.
>+ Direct connect gateway and CCN can form ECMP. However, the route’s health status will not be checked, and unhealthy routes will not be automatically restricted.
>+ Multiple NAT Gateway routes can form ECMP. However, the route’s health status will not be checked, and unhealthy routes will not be automatically restricted.
>+ Multiple CVM routes can form ECMP. However, the route’s health status will not be checked, and unhealthy routes will not be automatically restricted.


### Quota Limits
<table>
<tr>
<th>Resource</th>
<th>Limit</th>
</tr>
<tr>
<td>Number of route tables per VPC </td>
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
