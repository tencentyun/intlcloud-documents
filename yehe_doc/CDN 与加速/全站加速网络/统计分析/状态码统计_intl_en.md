ECDN status code statistics allows you to query monitoring data of status codes. You can log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Statistics Analysis** on the left sidebar to enter the [Status Code Statistics](https://console.cloud.tencent.com/dsa/statistics/status) page and try out this feature.

## Query Condition Description
+ Time Period: you can query data in the last 12 calendar months with a maximum time span of 31 days.
+ Project: you can query usage by project.
+ Domain Name: you can query usage of the specified domain name.
+ Granularity: it indicates the granularity of queried data and is related to the selected time period.
	1. If the selected time period is 1 day, you can query data at a granularity of 5 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, and 4 hours.
	2. If the selected time period is 2–3 days, you can query data at a granularity of 15 minutes, 30 minutes, 1 hour, 2 hours, and 4 hours.
	3. If the selected time period is 4–7 days, you can query data at a granularity of 30 minutes, 1 hour, 2 hours, and 4 hours.
	4. If the selected time period is 8–30 days, you can query data at a granularity of 1 hour, 2 hours, and 4 hours.
	
## Notes on Status Code Data Display
Status code data is displayed in two modes: status data distribution pie chart and status code trend curve. All data can be exported.
- Domain names that are connected in 30 days, including deleted ones, will all be added to the **All Domain Names** drop-down list.
- The real-time monitoring data on the current day is delayed for about 5 minutes. If you perform a query at 14:26:00, the query result will generally be data between 00:00:00 and 14:21:00 on that day.
- Monitoring statistics are grouped based on granularity. For example, if the query granularity is 5 minutes, statistics data between 10:00:00 and 10:04:59 will be grouped to the `10:00:00` sample point.
- If the specified query time period is longer than that during which the domain name has been connected, only the statistics of the time period for the connected domain name will be displayed, excluding the time period during which the domain name has not been connected or deleted.
- To query monitoring data of multiple domain names or metrics, you can use the [monitoring data query API](https://cloud.tencent.com/document/product/570/17942).

## Status Code Description
<table>
   <tr>
      <th style="text-align: center">Category</th>
      <th style="text-align: center">Status Code</th>
      <th style="text-align: center">Meaning</th>
      <th style="text-align: center">Recommended Solution</th>
   </tr>
   <tr>
      <td rowspan="2">2XX</td>
      <td>200</td>
      <td>The access succeeds.</td>
      <td rowspan="2">A 2XX status code generally indicates a normal access state.</td>
   </tr>
   <tr>
      <td>206</td>
      <td>The access succeeds.</td>
   </tr>
   <tr>
      <td rowspan="3">3XX</td>
      <td>301</td>
      <td>The content to be accessed has been permanently migrated.</td>
      <td rowspan="3">A 3XX status code generally indicates a normal access state.</td>
   </tr>
    <tr>
      <td>302</td>
      <td>The access is redirected.</td>
   </tr>
   <tr>
      <td>304</td>
      <td>The content to be accessed does not change.</td>
   </tr>
   <tr>
      <td rowspan="6">4XX</td>
      <td>400</td>
      <td>A request parameter is incorrect.</td>
      <td rowspan="6">A 4XX status code generally indicates that the client request is incorrect or the acceleration service of the domain name is disabled.</td>
   </tr>
   <tr>
       <td>401</td>
       <td>The access request fails to be verified.</td>
   </tr>
   <tr>
      <td>403</td>
      <td>The content is prohibited from being accessed.</td>
   </tr>
   <tr>
      <td>404</td>
      <td>The content to be accessed cannot be found.</td>
   </tr>
   <tr>
      <td>405</td>
      <td>The request method is not supported.</td>
   </tr>
   <tr>
      <td>416</td>
      <td>The range is invalid.</td>
   </tr>
   <tr>
      <td rowspan="10">5XX</td>
      <td>500</td>
      <td>An internal error of the server occurs.</td>
      <td rowspan="2">Check whether the origin server service is exceptional; and if not, please <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> for assistance.</td>
   </tr>
   <tr>
      <td>502</td>
      <td>The server fails to serve.</td>
   </tr>
    <tr>
      <td>501</td>
      <td>The request method is not supported by the server and cannot be processed.</td>
      <td>Please check the request method.</td>
   </tr>
    <tr>
      <td>513</td>
      <td>The ECDN edge server is overloaded, which is generally caused by user request surge or CC attacks.</td>
      <td>Please check whether the request surge of the domain name business is normal.</td>
   </tr>
    <tr>
      <td>522</td>
      <td>Internal HTTP ECDN connection fails to be established, or HTTP ECDN origin-pull connection fails to be established.</td>
      <td>Please check whether the origin server port 80 has been opened.</td>
   </tr>
   <tr>
      <td rowspan="2">529</td>
			<td >The routing configuration for the new domain name has not taken effect.</td>
      <td>It takes the platform 5–10 minutes to deploy the configuration. Please confirm that the configuration has taken effect before switching to the CNAME resolution.</td>
   </tr>
	 <tr>
     <td >The ping command is blocked by the origin server, and the origin-pull route information cannot be obtained.</td>
      <td>You need to grant the ping permission on your ECDN origin-pull nodes. You can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to get the list of IPs of ECDN origin-pull nodes.</td>
   </tr>
   </tr>
    <tr>
      <td>533</td>
      <td>ECDN edge and relay transfer fails, read times out, or connection fails to be established.</td>
      <td>Please<a href='https://console.cloud.tencent.com/workorder/category'> submit a ticket </a>for assistance.</td>
   </tr>
    <tr>
      <td>538</td>
      <td>HTTPS SSL handshake fails, Internal ECDN transfer fails, or ECDN origin-pull SSL handshake fails.</td>
      <td>Please check whether the origin server port 443 has been opened and SSL handshake is normal.</td>
   </tr>
    <tr>
      <td>564</td>
      <td>ECDN origin-pull times out.</td>
      <td>Please check whether there is network jitter on the origin server egress.</td>
   </tr>
   <tr>
      <td>Others</td>
      <td>0</td>
      <td>The client actively closes the connection during response.</td>
      <td>Generally, it is caused by the client's network problem or that the user actively stops access. If you have confirmed that user access is affected, you can<a href='https://console.cloud.tencent.com/workorder/category'> submit a ticket </a>for assistance.</td>
   </tr>
</table>
