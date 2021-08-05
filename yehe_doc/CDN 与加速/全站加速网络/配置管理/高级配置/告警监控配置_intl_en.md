>? If your application has been migrated to the CDN console, you can go to the console for operation by referring to [Content Delivery Network](https://intl.cloud.tencent.com/document/product/228).
## Description of Connecting ECDN to Cloud Monitor

ECDN has been connected to Tencent Cloud Monitor. The following alarming metrics are supported in the current version:

<table style="display:table;">
	<tbody>
		<tr>
			<th colspan="1" style="text-align: center;width: 100px;"> Category </th>
			<th colspan="1" style="text-align: center"> Metric </th>
			<th colspan="1" style="text-align: center"> 1-Minute Alarming Granularity Supported</th>
			<th colspan="1" style="text-align: center"> 5-Minute Alarming Granularity Supported</th>
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
			<td colspan="1" style="text-align: center"> Number of failed origin-pull </td>
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
			<td colspan="1" style="text-align: center"> Number of 200, 206, 2XX, etc. status code occurrences and their ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Number of 302, 304, 3XX, etc. status code occurrences and their ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Number of 401, 403, 404, 416, 4XX, etc. status code occurrences and their ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
		<tr>
			<td colspan="1" style="text-align: center"> Number of 500, 502, 5XX, etc. status code occurrences and their ratio </td>
			<td colspan="1" style="text-align: center"> Yes </td>
			<td colspan="1" style="text-align: center"> Yes </td>
		</tr>
	</tbody>
</table>

>?  
>- You can activate and use Cloud Monitor free of charge.
>- The system sends alarm messages through email, WeChat, and callback APIs free of charge, and you can enjoy a free tier of SMS alarm messages every month.
>- If the monthly free tier of SMS alarm messages is exceeded, you need to purchase a higher tier for receiving more alarm messages through SMS.
>- Alarm data is collected and reported in real time and may have certain deviation, as the data is delayed for about 5 minutes.
>- Alarm data monitoring can be used only to assist in operation and cannot be used as the basis for billing or SLA.



## Monitoring Configuration Entry
Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/policylist) and click **Alarm Policy** on the left sidebar to enter the management page.
![](https://main.qcloudimg.com/raw/02656ec03060812cd5f6267856ff779f.png)

## Adding Alarm
The steps for adding an alarm policy are as follows:
1. Enter the policy name and remarks and select the ECDN alarm policy type.
![](https://main.qcloudimg.com/raw/66f0a21eef4f94a5ec9f515e67e73463.png)
2. Select the alarm object.
![](https://main.qcloudimg.com/raw/a979482d128fc858621a7ba4b658867e.png)
3. Set the alarm trigger condition. Multiple conditions can be set at a time.
![](https://main.qcloudimg.com/raw/a4582abf188e52c1d10a3b9c44525c29.png)
4. Set the alarm recipient, alarm time period, and alarm method.
![](https://main.qcloudimg.com/raw/2224745dd2e051f2ec0e174c1d16a20d.png)
5. Set the alarm callback API.
![](https://main.qcloudimg.com/raw/153f990bd1cd08087c68254ac9ddb253.png)
6. Click **Complete** to submit the settings.


## Viewing Alarm
On the historical alarm page in Cloud Monitor, you can view the list of alarm details.
![](https://main.qcloudimg.com/raw/03155da8d30984811d6c820428c79aac.png)

## Other Alarm Policies
For more information on how to configure alarm policies, please see [Creating Alarm Policies](https://intl.cloud.tencent.com/zh/document/product/248/38908).
