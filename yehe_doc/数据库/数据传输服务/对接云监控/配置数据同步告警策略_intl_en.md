## Overview
You can use CM to set alarm rules for important metrics and events during data sync. If a metric is exceptional or an event is triggered, CM will promptly send notifications to you, so you can take appropriate measures.  

DTS supports default alarm configuration for some critical events, which means it will automatically monitor events when a task is started without having you to configure options and will notify you of triggered events. Currently, this feature is supported for the "data sync task interruption" event. 

## Adding Alarm Policy
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy configuration page.
3. Click **Add** and configure a new alarm policy as shown below:
<table>
<tr>
<th width="10%">Configuration Type</th><th width="15%">Configuration Item</th><th width="80%">Description</th></tr>
<tr>
<td  rowspan="4">Basic Info</td>
<td>Policy Name</td><td>Custom policy name.</td></tr>
<tr>
<td>Remarks</td><td>Custom policy remarks.</td></tr>
<tr>
<td>Monitoring Type</td><td>Cloud product monitoring.</td></tr>
<tr>
<td>Policy Type</td>
<td>Select the desired policy type of the Tencent Cloud service to be monitored. Here, select <strong>DTS/Data sync</strong>.
<ul>
<li>Data migration: metrics and events in data migration scenarios are monitored.</li>
<li>Data sync: metrics and events in data sync scenarios are monitored.</li>
<li>Data subscription (Kafka Edition): metrics and events in data subscription (Kafka Edition) in new DTS are monitored.</li>
<li>Data subscription: metrics and events in data subscription in old DTS are monitored.</li></ul></td></tr>
<tr>
<td rowspan="4">Alarm Policy</td>
<td>Alarm Object</td>
<td>
<ul>
<li>If you select **Instance ID**, the alarm policy will be associated with the selected instance.</li>
<li>If you select **Instance Group**, the alarm policy will be associated with the selected instance group.</li>
<li>If you select "All Objects", the alarm policy will be associated with all instances under the current account.</li></ul></td>
<tr>
<td>Configure manually<br>(metric alarm)</td>
<td>
<ul>
<li>Alarm trigger condition: you can choose to make the alarm triggered when <strong>any</strong> or <strong>all</strong> metrics meet the set condition.<ul><li>Configuration example: the metric is "RPS read from source database", the statistical period is 1 minute, the comparison relation is "<", the threshold is "1", and the consecutive monitoring duration is "3 consecutive data points".</li>
<li>Configuration effect: the "RPS read from source database" metric is collected once every minute. If the number of rows read by DTS from the source database per second is below 1 for three consecutive times, an alarm will be triggered.</li> </ul></li>
<li>Alarm frequency: you can customize the frequency for repeated alarm notifications, such as once every hour, 2 hours, and 1 day.</li></ul></td></tr>
<tr>
<td>Configure manually <br>(event alarm)</td>
<td>Select the event to be monitored. The "data sync task interruption" event has already been configured in the system by default.</td></tr>
<tr>
<td>Select template</td>
<td>Click *Select template** and select a configured template from the drop-down list. For detailed configurations, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If a newly created template is not displayed, click <strong>Refresh</strong> on the right.</td></tr>
<tr>
<td>Configure Alarm Notification</td>
<td>Notification Template</td>
<td>You can select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most.</li></td></tr>
<tr>
<td>Advanced Configuration</td>
<td >Auto Scaling</td>
<td>After this option is enabled and configured successfully, an auto scaling policy will be triggered for scaling when the alarm condition is met.</td></tr>
</table>
4. After configuring the above information, click **Save**.

## Modifying Alarm Policy
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** and click the name/ID of the policy to be modified to enter the alarm policy management page
3. Modify information such as trigger condition, alarm object, and alarm notification.
