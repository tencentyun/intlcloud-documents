## Overview
You can use CM to set alarm rules for important metrics during data sync. CM will send notifications to you as soon as a metric becomes abnormal, so you can take corresponding measures.  

This document describes how to set notification rules for metric alarms, including the trigger condition and scope of metric alarms, form of notifications, time period for notifications, and recipient group. 

## Adding an alarm policy
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. Select **Alarm Configuration** > **Alarm Policy** on the left sidebar to enter the alarm policy configuration page.
3. Click **Create** and configure a new alarm policy as detailed below:
<table>
<tr>
<th width="10%">Configuration Type</th><th width="15%">Configuration Item</th><th width="80%">Description</th></tr>
<tr>
<td  rowspan="4"> Basic Info</td>
<td>Policy Name</td><td>Enter a custom policy name.</td></tr>
<tr>
<td>Remarks</td><td>Enter custom policy remarks.</td></tr>
<tr>
<td>Monitoring Type</td><td>Select <b>Tencent Cloud services</b>.</td></tr>
<tr>
<td>Policy Type</td>
<td>Select the desired policy type of the Tencent Cloud service to be monitored. Here, select <strong>DTS/Data sync</strong>.
<ul>
<li>Data migration: Metrics in data migration scenarios are monitored.</li>
<li>Data sync: Metrics in data sync scenarios are monitored.</li>
<li>Data subscription (Kafka Edition): Metrics in data subscription (Kafka Edition) in New DTS are monitored.</li>
<li>Data subscription: Metrics in data subscription in Old DTS are monitored.</li></ul></td></tr>
<tr>
<td rowspan="3">Alarm Policy</td>
<td>Alarm Object</td>
<td>
<ul>
<li>If you select <b>Instance ID</b>, the alarm policy will be associated with the selected instance.</li>
<li>If you select <b>Instance Group</b>, the alarm policy will be associated with the selected instance group.</li>
<li>If you select <b>All Objects</b>, the alarm policy will be associated with all instances under the current account.</li></ul></td>
<tr>
<td>Configure manually<br></td>
<td>
<ul>
<li>Trigger Condition: You can choose to make the alarm triggered when <strong>any</strong> or <strong>all</strong> metrics meet the set condition.<ul><li>Configuration example: The metric is "RPS read from source database", the statistical period is 1 minute, the comparison relation is "<", the threshold is "1", and the consecutive monitoring duration is "3 consecutive data points".</li>
<li>Configuration effect: The "RPS read from source database" metric is collected once every minute. If the number of rows read by DTS from the source database per second is below 1 for three consecutive times, an alarm will be triggered.</li> </ul></li>
<li>Alarm frequency: You can customize the frequency for repeated alarm notifications, such as once every hour, 2 hours, or day.</li></ul></td></tr>
<tr>
<td>Select template</td>
<td>Click <b>Select template</b> and select a configured template from the drop-down list. For detailed configurations, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If a newly created template is not displayed, click <strong>Refresh</strong> on the right.</td></tr>
<tr>
<td>Configure Alarm Notification</td>
<td>Notification Template</td>
<td>You can select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most.</li></td></tr>
</table>

4. After configuring the above items, click **Save**.

## Modifying an alarm policy
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. Select **Alarm Configuration** > **Alarm Policy** on the left sidebar and click the name/ID of the policy to be modified to enter the alarm policy management page.
3. Modify information such as trigger condition, alarm object, and alarm notification.
