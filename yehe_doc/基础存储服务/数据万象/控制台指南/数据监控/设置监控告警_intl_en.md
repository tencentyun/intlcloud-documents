## Overview

You can leverage the alarm policy feature of Cloud Monitor to set threshold-reaching alarms for CI monitoring metrics. An alarm policy must include the policy name, policy type, trigger condition, alarm object, and alarm notification template. You can create an alarm policy for CI as instructed below.

>? Tencent Cloud's Cloud Monitor enables users to monitor cloud resources in real time and provides alarm services. Users can set alarm policies for CI monitoring metrics to query the alarm history and receive alarm notifications. For more information, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
>

## Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci). On the **Overview** page, click **Configure Alarm Policy** in the **Alarm Configuration** section.
2. Click **Create**.
3. On the **Create alarm policy** page, configure a new alarm policy.

Notes:
<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="5"> Basic info</td>
    <td>Policy name</td>
    <td>A custom policy name</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>Remarks for the policy</td>
  </tr>
  <tr>
    <td>Monitor Type</td>
    <td>Choose <b>Cloud Product Monitoring</b>.</td>
  </tr>
  <tr>
    <td>Policy type</td>
    <td>Select CI.</td>
  </tr>
  <tr>
    <td>Project</td>
    <td>Setting the policy project allows you to:<br>   
         <ul>
             <li>Manage alarm policies. Alarm policies of a project can be quickly located in the alarm policy list.</li>
             <li>Manage instances. You can select the project as needed. Instances of the project can be quickly located in **Alarm Object**. You can distribute Tencent Cloud services to the desired project according to your business types. After the project is created, you can distribute resources to projects in the console of each Tencent Cloud service. Some Tencent Cloud services cannot be distributed to a project. If you do not have project permission, see <a href="https://intl.cloud.tencent.com/document/product/248/36744">Cloud Access Management (CAM)</a> for authorization.</li></td>   
  </tr>
  <tr>
    <td rowspan="3">Configure alarm rule</td>
    <td>Alarm object</td>
    <td>
      <ul>
			         <li>If you choose <b>Instance ID</b> in the drop-down list, select the bucket you want to add an alarm to. </li>
               <li>If you choose <b>Instance Group</b> in the drop-down list, the alarm policy is bound to the selected instance group. If there is no instance group, you can click <b>Create Instance Group</b> on the right to create a group for the bucket first. </li>
		            <li>If you choose <b>All Objects</b> in the drop-down list, the alarm policy is bound to all buckets the current account has permission on. </li>
           </ul>
        </td>
  </tr>
	<tr>
    <td>Select template</td>
    <td>Select a configured template from the drop-down list. For more information on the configuration, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If the newly created template is not displayed, click <b>Refresh</b> on the right.</td>
  </tr>
	<tr>
    <td>Manual configuration<br>(Metric alarm)</td>
    <td>
      <ul>
        <li>Trigger condition: Consists of metric, comparison, threshold, statistical period, and the number of consecutive periods.<br>For example, if the metric is set to `Total usage of basic image processing`, comparison to `>`, threshold to 100 MB, statistical period to 1 minute, and number of consecutive data points to 2, <br>the total usage of basic image processing will be collected once every minute, and an alarm will be triggered if a bucket's usage of basic image processing is greater than 100 MB for two consecutive times.
				<br><li>Alarm frequency: You can set a repeated notification policy for each alarm rule. In this way, an alarm notification will be sent repeatedly at a specified frequency when an alarm is triggered.<br>Frequency options: do not repeat, once every 5 minutes, once every 10 minutes, at an exponentially increasing interval, and other frequency options.<br><ul><li type="square">An exponentially increasing interval means that a notification is sent when an alarm is triggered the 1st time, 2nd time, 4th time, 8th time, and so on. In other words, the alarm notification will be sent less and less frequently as time goes on to reduce the disturbance caused by repeated notifications.</li>
      <li>Default logic for repeated alarm notifications: The alarm notification will be sent to you at the configured frequency within 24 hours after the alarm is triggered. After 24 hours, the alarm notification will be sent once a day by default.</li></ul></li>
      </ul></td>
  </tr>
   <tr>
        <td >Configure alarm notification</td>
        <td>Alarm notification</td>
        <td>Select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most. For more information, see <a href="https://www.tencentcloud.com/document/product/248/38906">Alarm Notification</a>.</td>
    </tr>
		<tr>
      <td>Advanced configuration</td>
      <td >Auto scaling</td>
      <td>If enabled, the auto scaling policy can be triggered when the alarm condition is met.</td>
     </tr>
</table>
5. After configuring the above items, click **Save**.
