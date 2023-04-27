This document describes how to set an alarm for a key test metric, so that you can receive timely notifications when the metric is abnormal.

## Directions

1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy configuration page.
3. Click **Add** and configure a new alarm policy as detailed below:
<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="4"> Basics</td>
    <td>Policy name</td>
    <td>Name the policy</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>Add remarks for policy</td>
  </tr>
  <tr>
    <td>Test mode</td>
    <td>Select the CAT test mode.</td>
  </tr>
  <tr>
    <td>Policy type</td>
    <td>It can be <b>Network quality</b>, <b>Page performance</b>, <b>API monitoring</b>, <b>File transfer</b>, or <b>Audio/Video experience</b>.</td>
  </tr>
  <tr>
    <td rowspan="3">Configure alarm rule</td>
    <td>Filter condition (AND)</td>
    <td>You can filter objects that meet filter conditions for alarming, and the relationship between these conditions is AND. Only objects with reported data will be displayed after filtering.<ul>
		<li>Domain (required): You can set alarms by domain. Currently, you can select only one domain.</li>
		<li>Region: You can filter the test data in a certain region under a certain domain for alarming.</li>
		<li>City: You can filter the test data in a certain city under a certain domain for alarming.</li>
		<li>ISP: You can filter the test data for a certain ISP under a certain domain for alarming.</li></ul>
		If you filter by the <code>https://www.tencentcloud.com/</code> domain and Guangdong region, data meeting the conditions will be filtered for alarming.	</td>
	<tr>
    <td>Alarm object dimension</td>
    <td>You can customize the alarm objects displayed in the alarm notification. Suppose you select <b>Domain</b> and <b>ISP</b>, the following alarm objects will be displayed: <code>domain=xxx ISP=xxx</code>. If no objects are specified, only the domain information will be displayed by default.</td>
   </tr>
		<tr>
    <td>Alarm trigger</td>
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

4. After configuring the above information, click **Save**. When a metric is abnormal, alarm notifications will be sent through the alarm channels you configured.
>?For more information on the metrics, see [Cloud Automated Testing](https://www.tencentcloud.com/document/product/1169/52005).