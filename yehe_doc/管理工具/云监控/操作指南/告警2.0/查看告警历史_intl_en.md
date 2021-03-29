Cloud Monitor provides the alarm records feature, allowing you to trace back and view the alarms in the last six months. You can also quickly subscribe to alarm policies on the alarm records page.

## Viewing Alarm Records

1. Log in to the Cloud Monitor Console and go to [Alarm Records](https://console.cloud.tencent.com/monitor/alarm2/history).
2. (Optional) Click the time filter button in the top-left corner to filter the time period in which to view alarm records. You can filter alarms generated today, yesterday, in the last 7 days, and in the last 30 days, and you can also select a custom time period. You can view the alarm records in the last six months at most.
3. (Optional) You can enter the information of an alarm object (such as instance name, public IP, and private IP) in the "Alarm Object" search box to search for corresponding records.
4. (Optional) You can also click **Advanced Filter** to search for alarm records by policy name, alarm content, user information, monitor type, and policy type.
![](https://main.qcloudimg.com/raw/9a6c5219abe5046587b9382215da78b5.png)

## Clearing Filter Conditions

After successfully filtering alarm records, click **Clear filter conditions** in the list.
![](https://main.qcloudimg.com/raw/7e67481b070a735f6b47cf3fc8acc5a8.png)

## Customizing List Fields

1. Log in to the Cloud Monitor Console and go to [Alarm Records](https://console.cloud.tencent.com/monitor/alarm2/history).
2. Click ![](https://main.qcloudimg.com/raw/e25c0821dbe69e0d0c6c1eaaaf531ba8.png) in the top-right corner. You can check the fields that need to be displayed on the left of the pop-up box and drag the field names on the right to adjust the sorting as shown below.
   ![](https://main.qcloudimg.com/raw/735bca6eed81ce1ad9f0551726b3b399.png)

## Subscribing to Policy

The alarm records feature allows the **current user logged in to the console** to quickly subscribe to alarm policies.

1. Log in to the Cloud Monitor Console and go to [Alarm Records](https://console.cloud.tencent.com/monitor/alarm2/history).
2. Find the alarm policy to be subscribed to and click **Subscribe** in the "Operation" column.
	- If the alarm object of the alarm policy is a recipient, click **OK** in the pop-up box.
	- If the alarm object of the alarm policy is a recipient group, click the **policy details page** link in the pop-up box. Then, you need to create a user group on the redirected page. For more information, please see Creating Alarm Recipient Group.
> ?
> - The alarm receiving channel is the channel set by the current policy. If it is not set, SMS and email channels will be used by default.
> - Alarm policies for platform events cannot be subscribed to.
> - Deleted alarm policies cannot be subscribed to.
>- To cancel the subscription, you need to do so on the policy details page instead of the alarm records page.

## Alarm Status


<table>
<tbody>
<tr>
<th width="15%">Alarm Status</th>
<th width="85%">Description</th>
</tr>
<tr>
<td>Not resolved</td>
<td>An alarm has not been processed or is being processed.</td>
</tr>
<tr>
<td>Resolved
</td><td>Normal status has been restored.
</td></tr>
<tr>
<td>Insufficient data
</td>
<td>
<li>The alarm policy that triggered an alarm has been deleted.<br><li>The CVM instance has been migrated from one project to another one.<br><li>No data is reported because Agent has not been installed or has been uninstalled.
</td>
<tr>
<td>Expired
</td>
<td>
<li>The alarm policy has changed.<br><li>The latest triggering time of the alarm has not been updated for more than 24 hours.<br></li>
</td>
</tr>
</tbody></table>
