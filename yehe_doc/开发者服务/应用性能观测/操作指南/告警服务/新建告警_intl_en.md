This document describes how to set an alarm for a key application performance metric, so that you can receive timely notifications when the metric is abnormal.

## Directions

1. Log in to the [APM console](https://console.cloud.tencent.com/apm/monitor).
2. On the left sidebar, click **Alarm configuration** to enter the alarm policy configuration page.
3. Click **Create** and configure a new alarm policy as follows:

<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="4"> Basic information</td>
    <td>Policy name</td>
    <td>The custom policy name.</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>The custom policy remarks.</td>
  </tr>
  <tr>
    <td>Monitoring type</td>
    <td>Select the application performance monitoring type.</td>
  </tr>
  <tr>
    <td>Policy type</td>
    <td>Performance metrics are selected by default.</td>
  </tr>
  <tr>
    <td rowspan="3">Alarm policy</td>
    <td>Filter condition (AND)</td>
    <td>You can filter objects that meet filter conditions for alarming, and the relationship between these conditions is AND. Only objects with reported data will be displayed after filtering.
		<li>Business system (required): You can set alarms by business system. Currently, you can select only a single business system.</li>
		<li>Application (required): You can filter the performance data of a specific application in a specific business system for alarm detection.</li>
		<li>Call role (required): You can filter the performance data of a specific call role in a specific application for alarm detection.</li>
		<li>Instance: You can filter the performance data of a specific instance in a specific business system for alarm detection.</li>
		<li>API: You can filter the performance data of a specific API in a specific application for alarm detection.</li>
	<tr>
    <td>Alarm object dimension</td>
    <td>You can customize the alarm objects displayed in the alarm notification. Suppose you select business system, application, and call role, the following alarm objects will be displayed: business system=xxx,  application=xxx, call role=xxx.</td>
   </tr>
		<tr>
    <td>Trigger condition</td>
    <td>You can specify whether to trigger an alarm when any condition or all conditions are met.
</td>
  </tr>
		<tr>
      <td>Alarm notification</td>
      <td >Notification template</td>
            <td>The system provides default notification templates. You can also create a custom one as instructed in <a href="https://intl.cloud.tencent.com/document/product/248/38922">Creating Notification Template</a>.</td>
     </tr>
		<tr>
      <td>Advanced configuration</td>
      <td >Auto scaling</td>
      <td>If enabled, the auto scaling policy can be triggered when the alarm condition is met.</td>
     </tr>
</table>
4. After configuring the above information, click <b>Save</b>. When a metric is abnormal, alarm notifications will be sent through the alarm channels you configured.
