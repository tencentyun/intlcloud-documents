This document describes how to set an alarm for a key frontend performance metric, so that you can receive timely notifications when the metric is exceptional.

## Directions

1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Alarm Configuration** to enter the alarm policy configuration page.
3. Click **Add** and configure a new alarm policy as shown below:

<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="4">Basic Info</td>
    <td>Policy Name</td>
    <td>Custom policy name.</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>Custom policy remarks.</td>
  </tr>
  <tr>
    <td>Monitoring Type</td>
    <td>Select the application performance monitoring type.</td>
  </tr>
  <tr>
    <td>Policy Type</td>
    <td>The following policy types are supported: error log, page performance, static resource, API monitoring, custom event, and custom speed test.</td>
  </tr>
  <tr>
    <td rowspan="3">Alarm Policy</td>
    <td>Filter Condition (AND)</td>
    <td>You can filter objects that meet filter conditions for alarming, and the relationship between these conditions is AND. Only objects with reported data will be displayed after filtering. You can select the alarm object as needed.
	<tr>
    <td>Alarm Object Dimension</td>
    <td>You can customize the alarm objects displayed in the alarm notification. Suppose you select business system, application, and call role, the following alarm objects will be displayed: business system=xxx,  application=xxx, call role=xxx.</td>
   </tr>
		<tr>
    <td>Trigger Condition</td>
    <td>You can specify whether to trigger an alarm when any condition or all conditions are met.
</td>
  </tr>
		<tr>
      <td>Alarm Notification</td>
      <td >Notification Template</td>
            <td>The system provides default notification templates. You can also create a custom one as instructed in <a href="https://intl.cloud.tencent.com/document/product/248/38922">Creating Notification Template</a>.</td>
     </tr>
		<tr>
      <td>Advanced Configuration</td>
      <td >Auto Scaling</td>
      <td>After this option is enabled and configured successfully, an auto scaling policy will be triggered for scaling when the alarm condition is met.</td>
     </tr>
</table>
4. After configuring the above information, click **Save**. When a metric is exceptional, alarm notifications will be sent through the alarm channels you configured.
