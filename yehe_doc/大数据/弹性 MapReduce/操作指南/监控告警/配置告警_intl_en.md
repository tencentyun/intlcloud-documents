## Overview
Elastic MapReduce (EMR) has been connected to Cloud Monitor (CM). You can configure alarm policies for EMR nodes and service monitoring metrics in the CM console.

>?
>- EMR has been connected to CM's default alarms. CM will automatically create a default alarm policy. For information about metrics/events or alarm rules supported by the EMR default policy, see [Default Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38914).
>- You can manually create an alarm policy and set it as the default alarm policy. After the default policy is set, newly purchased instances will be automatically associated with the default policy without requiring manual addition.

## Directions
1. Log in to the Cloud Monitor console and click **Alarm Configuration** > [Alarm Policy](https://console.cloud.tencent.com/monitor/alarm2/policy) on the left sidebar.
2. On the **Alarm Policy** page, click **Create**.
3. In the pop-up window, configure the basic information, alarm policy, and notification template as instructed below.
<table>
<tr>
<th>Configuration Type</th>
<th colspan="2">Configuration Item</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="5">Basic information</td>
<td  colspan="2">Policy name</td>
<td>Custom policy name</td>
</tr>
<tr>
<td colspan=2>Remarks</td>
<td>Custom policy remarks</td>
</tr>
<tr>
<td colspan="2">Monitoring type</td>
<td>Supported cloud service monitoring type</td>
</tr>
<tr>
<td colspan="2">Policy type</td>
<td>Select the desired policy type for monitoring Tencent Cloud services.</td>
</tr>
<tr>
<td colspan="2">Project</td>
<td>You can filter to find alarm policies under a project in the alarm policy list.</td>
</tr>
<tr>
<td  rowspan="5">Alarm rule configuration</td>
<td colspan="2">Alarm object</td>
<td><ul/><li>If you select an instance ID, the alarm policy will be associated with the selected instance.<li>If you select an instance group, the alarm policy will be associated with the selected instance group.<li>If you select all objects, the alarm policy will be associated all instances that the current account has permission on.</td>
</tr>
<tr>
<td  rowspan="3">Trigger condition</td>
<td>Manual configuration (metric alarm)</td>
<td>Trigger condition: consists of metric, comparison, threshold, statistical period, and the number of consecutive periods. You can expand the trigger condition to view the metric trend, and based on which, set a proper threshold.</td>
</tr>
<tr>
<td>Manual configuration (event alarm)</td>
<td>Create an event alarm policy to get notifications in case of service resources or underlying infrastructure exceptions.</td>
</tr>
<tr>
<td>Select template</td>
<td>Select a configured template in the drop-down list. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>.</td>
</tr>
<tr>
<td>Configure alarm notification (optional)</td>
<td>Notification template</td>
<td>You can use the preset notification template (alarms will be notified to the root account administrator via SMS and email. This template is selected by default.) or customize one. Up to three notification templates can be bound to each alarm policy. For more information about notification template configuration, see <a href="https://intl.cloud.tencent.com/document/product/248/38922">Creating Notification Template</a>.</td>
</tr>
</table>
4. Click **Complete**.

