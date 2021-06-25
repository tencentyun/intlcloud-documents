ECDN status code statistics allow you to query monitoring data of status codes. You can log in to the [ECDN Console](https://console.cloud.tencent.com/dsa), then click **Statistics** on the left sidebar to enter the [Status Code Statistics](https://console.cloud.tencent.com/dsa/statistics/status) page and try out this feature.

## Query Filters
+ Period: queries data in the last 12 calendar months with a maximum time span of 31 days.
+ Project: queries usage by project.
+ Domain Name: queries usage of the specified domain name.
+ Granularity: indicates an interval in which you query data and is subject to the selected period.
	1. For a 1-day period, you can query data at a granularity of 5 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, 4 hours, or 24 hours.
	2. For a period of 2–3 days, you can query data at a granularity of 15 minutes, 30 minutes, 1 hour, 2 hours, or 4 hours.
	3. For a period of 4–7 days, you can query data at a granularity of 30 minutes, 1 hour, 2 hours, or 4 hours.
	4. For a period of 8–30 days, you can query data at a granularity of 1 hour, 2 hours, 4 hours or 24 hours.
+ Region: queries usage by geographic area (regions within Mainland China or outside, or global regions).
	

![](https://main.qcloudimg.com/raw/3398341767d97905383a3ac3edb96a17.png)

## Status Code Data Display
Status code data is displayed in a pie chart and a trend curve. All data can be exported.
- All domain names that were connected in the last 30 days, including deleted ones, will be included in the **All Domain Names** drop-down list.
- The real-time monitoring data you query will have a near 5-minute lag. If you run a query at 14:26:00, you will get the 00:00:00–14:21:00 data.
- Monitoring data is tracked over a time interval. For a 5-minute interval, a query start at 10:00:00–10:04:59 will start at the 10:00:00 sample point.
- If the time you query is longer than that of domain name connection, you will only get the connection statistics rather than those unconnected or deleted.
- To query monitoring data of multiple domain names or metrics, you can use the DescribeEcdnStatistics API.

![](https://main.qcloudimg.com/raw/745bd6a24240811422187aa3433b1438.png)



## Status Code Description
<table>
   <tr>
      <th style="text-align: center">Category</th>
      <th style="text-align: center">Status Code</th>
      <th style="text-align: center">Description</th>
      <th style="text-align: center">Solution</th>
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
      <td>The accessed content has been permanently migrated.</td>
      <td rowspan="3">A 3XX status code generally indicates a normal access state.</td>
   </tr>
    <tr>
      <td>302</td>
      <td>The access is redirected.</td>
   </tr>
   <tr>
      <td>304</td>
      <td>The content to be accessed has not changed.</td>
   </tr>
   <tr>
      <td rowspan="6">4XX</td>
      <td>400</td>
      <td>A request parameter is incorrect.</td>
      <td rowspan="6">A 4XX status code generally indicates that the client request is incorrect or the acceleration service of the domain name has been disabled.</td>
   </tr>
   <tr>
       <td>401</td>
       <td>The access request verification fails.</td>
   </tr>
   <tr>
      <td>403</td>
      <td>Access to the content is denied.</td>
   </tr>
   <tr>
      <td>404</td>
      <td>The requested content cannot be found.</td>
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
      <td>An internal server error occurs.</td>
      <td rowspan="2">Please check whether the origin server service is exceptional; if not, please<a href='https://console.cloud.tencent.com/workorder/category'> submit a ticket </a>for assistance.</td>
   </tr>
   <tr>
      <td>502</td>
      <td>The server cannot provide service currently.</td>
   </tr>
    <tr>
      <td>501</td>
      <td>The request method is not supported by the server and cannot be processed.</td>
      <td>Please check the request method.</td>
   </tr>
    <tr>
      <td>513</td>
      <td>The ECDN edge server is overloaded, which is generally caused by user request surge or CC attacks.</td>
      <td>Please check that the business request surge of the domain name is normal.</td>
   </tr>
    <tr>
      <td>522</td>
      <td>Internal HTTP ECDN connection establishment fails, or HTTP ECDN origin-pull connection establishment fails.</td>
      <td>Please check that the origin server port 80 has been opened.</td>
   </tr>
   <tr>
      <td rowspan="2">529</td>
			<td >The domain name is newly added, and the route configuration has not taken effect.</td>
      <td>It takes 5–10 minutes for the platform to deploy the configuration. Please confirm that the configuration has taken effect before switching to the CNAME resolution.</td>
   </tr>
	 <tr>
     <td >The ping command is blocked by the origin server, and the origin-pull route information cannot be obtained.</td>
      <td>You need to grant the ping permission on your ECDN intermediate nodes. You can <a href='https://console.cloud.tencent.com/workorder/category'> submit a ticket </a> to get the list of IPs of ECDN intermediate nodes.</td>
   </tr>
   </tr>
    <tr>
      <td>533</td>
      <td>ECDN edge or relay transfer fails, read times out, or connection establishment fails.</td>
      <td>Please<a href='https://console.cloud.tencent.com/workorder/category'> submit a ticket </a>for assistance.</td>
   </tr>
    <tr>
      <td>538</td>
      <td>HTTPS SSL handshake fails, internal ECDN transfer fails, or ECDN origin-pull SSL handshake fails.</td>
      <td>Please check that the origin server port 443 has been opened and SSL handshake is normal.</td>
   </tr>
    <tr>
      <td>564</td>
      <td>ECDN origin-pull times out.</td>
      <td>Please check whether there are jitters on the origin server egress network.</td>
   </tr>
   <tr>
      <td>Other</td>
      <td>0</td>
      <td>The client actively closes the connection during response.</td>
      <td>Generally, it is caused by a client network problem or active stop of access by the user.</td>
   </tr>
</table>
