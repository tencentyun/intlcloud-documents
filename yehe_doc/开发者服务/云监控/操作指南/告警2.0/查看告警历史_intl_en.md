Alarm records are a feature of Cloud Monitor that allows you to look back and view alarms in the past six months. On the alarm records page, you can also quickly subscribe to alarm policies.

## Viewing Alarm Records

1. Log in to the Cloud Monitor console and go to [Alarm Records](https://console.cloud.tencent.com/monitor/alarm2/history).
2. (Optional) To view alarm records for a certain time period, click the time filter button in the top-left corner. You can filter alarms generated today, yesterday, and in the last 7 days or 30 days, and you can also select a custom time period. You can view the alarm records in the last six months at most.
3. (Optional) You can enter the information of an alarm object (such as instance name, public IP, and private IP) in the "Alarm Object" search box to search for corresponding records.
4. (Optional) You can also click **Advanced Filter** to search for alarm records by policy name, alarm content, user information, monitor type, and policy type.
![](https://main.qcloudimg.com/raw/9a6c5219abe5046587b9382215da78b5.png)

## Clearing Filter Conditions

After successfully filtering alarm records, click **Clear filter conditions** in the list.
![](https://main.qcloudimg.com/raw/7e67481b070a735f6b47cf3fc8acc5a8.png)

## Customizing List Fields

1. Log in to the Cloud Monitor console and go to [Alarm Records](https://console.cloud.tencent.com/monitor/alarm2/history).
2. Click ![](https://main.qcloudimg.com/raw/e25c0821dbe69e0d0c6c1eaaaf531ba8.png) in the top-right corner. You can check the fields that need to be displayed on the left of the pop-up box and drag the field names on the right to adjust the sorting as shown below.
![](https://main.qcloudimg.com/raw/735bca6eed81ce1ad9f0551726b3b399.png)


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
<li>The alarm policy that triggered an alarm has been deleted.<br><li>The CVM instance has been migrated from one project to another.<br><li>No data is reported because Agent has not been installed or has been uninstalled.
</td>
<tr>
<td>Expired
</td>
<td>
<li>Threshold modification<br><li>Policy deletion<br></li><li>Policy enablement/disablement<br></li><li>Instance unbinding<br></li></li><li>Instance termination<br></li>
</td>
</tr>
</tbody></table>
