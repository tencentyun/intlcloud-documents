## Description of Connecting ECDN to Cloud Monitor

ECDN has been connected to Tencent Cloud Monitor. The following alarming metrics are supported in the current version:

<table style="display:table;">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center;width: 100px;"> Category </th>
			<th colspan="1" style="text-align: center"> Metric </th>
			<th colspan="1" style="text-align: center"> Support for 1-minute Alarming Granularity </th>
			<th colspan="1" style="text-align: center"> Support for 5-minute Alarming Granularity </th>
		</tr>
		<tr>
			<td rowspan="4" style="text-align: center;width: 100px;"> Access traffic metrics </td>
			<td colspan="1" style="text-align: center"> Total number of requests </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Access bandwidth </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Access traffic (upstream) </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Access traffic (downstream) </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td rowspan="4" style="text-align: center;width: 100px;"> Origin-pull traffic metrics </td>
			<td colspan="1" style="text-align: center"> Total number of origin-pulls </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Number of origin-pull failures </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Origin-pull failure rate </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Origin-pull bandwidth </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td rowspan="1" style="text-align: center;width: 100px;"> Access performance metrics </td>
			<td colspan="1" style="text-align: center"> Average response time </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td rowspan="4" style="text-align: center;width: 100px;"> Status code metrics </td>
			<td colspan="1" style="text-align: center"> 200, 206, 2XX, etc. status code occurrence numbers and ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 302, 304, 3XX, etc. status code occurrence numbers and ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 401, 403, 404, 416, 4XX, etc. status code occurrence numbers and ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> 500, 502, 5XX, etc. status code occurrence numbers and ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
	</tbody>
</table>

> 
- You can activate and use Cloud Monitor free of charge.
- The system sends alarm messages through email, WeChat, and callback APIs free of charge, and you can enjoy a free tier of SMS alarm messages every month.
- If the monthly free tier of SMS alarm messages is exceeded, you need to purchase a higher tier to continue receiving alarm messages through SMS.
- Alarm data is collected and reported in real time and may have certain deviation, as the data is delayed for about 5 minutes.
- Alarm data monitoring can be used only to assist operation and cannot be billed or used as an SLA proof.



## Monitoring Configuration Entry
Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/policylist) and click **Alarm Policy** on the left sidebar to enter the management page.
![](https://main.qcloudimg.com/raw/b8bc205767f178371c4bde3ce995482e.png)

## Adding Alarm
The steps for adding an alarm policy are as shown below.
1. Enter the policy name and remarks and select the ECDN dynamic acceleration alarm policy type.
![](https://main.qcloudimg.com/raw/41886628b7a7148ae64e51fdbfcddf7d.png)
2. Select the alarm object.
![](https://main.qcloudimg.com/raw/d203babf3d633d0f453d96dcf0844fc7.png)
3. Set the alarm trigger condition. Multiple conditions can be set at a time.
![](https://main.qcloudimg.com/raw/639e37cb80e69691ab248c9c8df99bef.png)
4. Set the alarm recipient, alarm time period, and alarm method.
![](https://main.qcloudimg.com/raw/7b39510054f9815c213565323560d048.png)
5. Set the alarm callback API.
![](https://main.qcloudimg.com/raw/e4b7d897120d3297510ebafd97dc060b.png)
6. Click **Complete** to submit the settings.


## Viewing Alarm
On the historical alarm page in Cloud Monitor, you can view the list of alarm details.
![](https://main.qcloudimg.com/raw/6b7f10c1bc752046cb844d660a378da3.png)

## Other Alarm Policies
For more information on how to configure alarm policies, please see [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215).
