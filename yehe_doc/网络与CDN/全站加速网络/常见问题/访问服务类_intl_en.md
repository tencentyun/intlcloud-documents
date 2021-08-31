### How do I get the cache node IP accessed by a client?

The ECDN platform uses the `X-Forwarded-For` header field to pass user's real IP address for origin-pull by default.

### Why is the obtained client IP address different from the user's real IP address?

If the client IP address obtained by the origin server from the `X-Forwarded-For` field is different from the user's real IP address, it may be caused by the following factors and can be solved in the following ways:

<table style="display:table;" width="100%">
	<thead>
		<tr>
			<th colspan="1" style="text-align: center" width=20%> Cause </th>
			<th colspan="1" style="text-align: center" width=15%> Scope of Affection </th>
			<th colspan="1" style="text-align: center" width=25%> Other Characteristics </th>
			<th colspan="1" style="text-align: center" width=40%> Solution </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>The user uses a proxy server for access </td>
			<td>Specific users </td>
			<td>The IP obtained when the user directly accesses the origin server is also exceptional </td>
			<td>This problem is on the client. Cancel proxy or allow getting the proxy server IP </td>
		</tr>
		<tr>
			<td>The origin server load balancer modifies the header </td>
			<td>All users</td>
			<td>The obtained IP is the ECDN intermediate node IP</br>The user can directly access the origin server normally </td>
			<td>Modify the origin server load balancer configuration, but do not modify the content of `X-Forwarded-For` </td>
		</tr>
		<tr>
			<td>User access is hijacked </td>
			<td>Users in specific regions</td>
			<td>The obtained HTTP request IP is exceptional</br>The obtained HTTPS request IP is normal </td>
			<td><a href='https://console.cloud.tencent.com/workorder/category'>Submit a ticket</a> for assistance </td>
		</tr>
		<tr>
			<td>Node features are exceptional </td>
			<td>Users in specific regions or ISPs</td><td>The IP obtained when the user directly accesses the origin server is normal </td>
			<td>This problem generally does not occur. If it occurs, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> for assistance </td>
		</tr>
	</tbody>
</table>

### What should I do if an exceptional status code is returned for access with ECDN?

The causes and solutions for common exceptional ECDN status codes are as follows:

<table style="display:table;" width="100%">
	<thead>
		<tr>
			<th rowspan="1" style="text-align: center" width=10%> Status Code </th>
			<th colspan="1" style="text-align: center" width=35%> Cause </th>
			<th colspan="1" style="text-align: center" width=55%> Solution </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td rowspan="2" style="text-align: center">404</td>
			<td>The content requested by the user does not exist on or has been deleted from the origin server </td>
			<td>Check whether the requested content exists on the origin server or modify the request link. </td>
		</tr>
		<tr>
			<td>The domain name acceleration service has not been enabled, or the domain name has not been connected to ECDN </td>
			<td>Connect the domain name to ECDN and enable the acceleration service. </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center">522</td>
			<td>The content of origin server's response is invalid </td>
			<td>The content of the origin server's response obtained by the node is incomplete or is in an incompatible format. You can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> for assistance. </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center">513</td>
			<td>Access requests from a certain region surge and are therefore blocked </td>
			<td>Access requests from a certain region surge, which are suspected as attack traffic and automatically blocked by the platform. If you are sure that they are not attack traffic, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to apply for canceling the access limit. </td>
		</tr>
		<tr>
			<td rowspan="2" style="text-align: center">529</td>
			<td>The domain name is newly added, and the route configuration has not taken effect </td>
			<td>It takes 5–10 minutes for the platform to deploy the configuration. Please confirm that the configuration has taken effect before switching the CNAME resolution.</td>
		</tr>
		<tr>
			<td>The ping command is blocked by the origin server, and the origin-pull route information cannot be obtained </td>
			<td>You need to grant the ping permission on your ECDN intermediate nodes. You can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to get the list of IPs of ECDN intermediate nodes. </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center">538</td>
			<td>SSL handshake between the node and origin server fails </td>
			<td>Generally, this problem is caused by origin server network, SSL protocol, or algorithm incompatibility. You can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> for assistance. </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center">564</td>
			<td>HTTPS origin-pull connection is closed due to exception </td>
			<td><li>If the 564 error occurs for a high number of requests on the ECDN platform, it is generally caused by node egress network exceptions. </li><li>If the 564 error occurs on certain origin servers, it is generally caused by egress network exceptions of your origin servers.</li> </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center">Other errors</td>
			<td>Troubleshoot based on the specific error message </td>
			<td><li>Check whether the error status code is a response from the origin server. </li><li>If not, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> for assistance. </li></td>
		</tr>
	</tbody>
</table>



### How do I quickly locate a domain name access exception?

1. Check for the domain name resolution problem.
   - Check whether the domain name resolution takes effect through DNS resolution and check whether the problem is caused by incorrect authoritative DNS resolution.
   - Check whether the client can get the node IP normally to confirm whether the user's local DNS resolution is exceptional.
2. Compare the response content before and after the acceleration.
   - If the response of direct access to the origin server is exceptional, the access failure may be caused by exceptional origin server service.
   - If the response of direct access to the origin server is normal, the problem may be related to the ECDN platform and needs further troubleshooting. 
3. Confirm the affection scope.
   - If access requests of only a small number of users are exceptional, the problem is generally caused by the client network. In this case, you can change the access network or access node and try again.
   - If affected users are in a certain region or ISP, the problem may be caused by service exceptions on some nodes, and you should immediately [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
   - If access requests of all users are affected, the problem may be related to the origin server or acceleration platform, and you should immediately [submit a ticket](https://console.cloud.tencent.com/workorder/category) for troubleshooting.
4. Check whether the problem can be reproduced.
   - The problem is occasional and cannot be reproduced. It is generally caused by ISP network jitters and can be recovered automatically.
   - The problem can be reproduced when the access request is sent again. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) describing the access environment and error symptoms for assistance.

### What information should I provide when contacting the customer service for assistance?

If you cannot solve a problem by yourself, please [contact us](https://intl.cloud.tencent.com/support) to report the fault and provide the following information for faster troubleshooting:

- Problem description and whether the problem can be reproduced.
- Information of domain name/origin server address where the problem occurs.
- Screenshots of the status code and error page.
- Screenshots of pinging acceleration domain name when the problem occurs.

