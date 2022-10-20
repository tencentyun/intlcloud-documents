## Feature Limits


<table>
	<tr>
		<th>Feature</th>
		<th nowrap="nowrap">Module</th>
		<th>Limit</th>
	</tr>
	<tr>
		<td rowspan="2" nowrap="nowrap">Dashboard</td>
		<td nowrap="nowrap">Monitoring dashboard</td>
		<td>You can create up to 30 monitoring dashboards by default. To increase the limit, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
	</tr>
	<tr>
		<td nowrap="nowrap">Monitoring chart</td>
		<td>A monitoring chart can display the monitoring data of up to 50 instances by default. To increase the limit, <a href="https://console.intl.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
	</tr>
	<tr>
		<td rowspan="4">Alarm</td>
		<td nowrap="nowrap">Alarm policy</td>
		<td>You can create up to 300 alarm policies for each policy type or project. This quota cannot be modified.</td>
	</tr>
	<tr>
		<td nowrap="nowrap">Default policy</td>
		<td>There is only one default policy for each policy type or project. This quota cannot be modified.</td>
	</tr>
	<tr>
		<td nowrap="nowrap">Alarm SMS quota</td>
		<td>Alarm SMS type: Basic alarm SMS and Cloud Automated Testing alarm SMS. <br>The alarm SMS quota is set to 1,000 per user for each SMS type on the first day of every month, and unused monthly quota is not carried over to the next month.</td>
	</tr>
	<tr>
		<td>Alarm record</td>
		<td>Alarm records can be stored for up to six months. For details, see <a href="#.E7.9B.91.E6.8E.A7.E6.95.B0.E6.8D.AE.E5.AD.98.E5.82.A8.E6.97.B6.E9.95.BF">Monitoring Data Storage Period</a></td>
	</tr>
	<tr>
		<td>Instance group</td>
		<td>Instance group</td>
		<td>Each group can contain up to 2,000 instances, with up to 200 instances added at a time. The two quotas cannot be modified.</td>
	</tr>
		<tr>
		<td>Metric monitoring data pulling (GetMonitorData)</td>
		<td>API call</td>
		<td>Each root account has a free tier of one million API requests per month. If you still want to pull monitoring data via APIs after the free tier is used up, enable “Pay-as-You-Go Billing for API Requests” first.</td>
	</tr>
</table>



## Monitoring Data Storage Period

Currently, monitoring data can be stored for up to six months. You can only query the monitoring data in the past six months.

| Monitoring Granularity | Storage Period |
| ------------ | -------- |
| In seconds         | 1 day      |
| 1 minute | 15 days     |
| 5 minutes | 31 days     |
| 1 hour        | 93 days     |
| 1 day          | 186 days    |

>?The monitoring data of 1-minute granularity metrics related to CPU, memory, and network for CVM are stored for 31 days.

## Permission Control

Cloud Monitor (CM) is available to all users with a Tencent Cloud account.
CM offers separate permission control systems for root accounts and sub-accounts. A root account has the permission to view the monitoring and alarming information of all services, while a sub-account has no permissions by default. For more permission information, see [Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/248/36744).
