This document describes how to create an alarm policy.

## Use Cases

You can set threshold alarms for the performance consumption metrics of the monitor types supported by Cloud Monitor. You can also set event alarms for the service status of Tencent Cloud service instances or the underlying platform infrastructure. This way, when an exception occurs, you will promptly receive notifications, which will allow you to take appropriate measures. An alarm policy consists of five required parameters: name, policy type, alarm trigger condition, alarm object, and alarm notification template. You can create alarm policies by following the directions below:

## Concepts

<table>
<thead>
<tr>
<th width="15%">Term</th>
<th width="85%">Definition</th>
</tr>
</thead>
<tbody><tr>
<td width="15%">Alarm policy</td>
<td width="85%">It consists of alarm name, alarm policy type, alarm trigger condition, alarm object, and alarm notification template</td>
</tr>
<tr>
<td>Alarm policy type</td>
<td>Alarm policy type identifies policy category and corresponds to specific Tencent Cloud products. For example, if you choose the CVM policy, you can customize metric alarms for CPU utilization, disk utilization, and more</td>
</tr>
<tr>
<td>Alarm trigger condition</td>
<td>An alarm trigger condition is a semantic condition consisting of metric, comparison, threshold, statistical period, and N consecutive monitoring data points</td>
</tr>  
<tr>
<td>Monitor type</td>
<td>Types include Tencent Cloud service monitoring, application performance monitoring, frontend performance monitoring, and cloud automated testing</td>
</tr>
<tr>
<td>Notification template</td>
 <td>A notification template can be quickly reused for multiple policies, making it suitable for alarm receipt in various use cases. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38922">Creating Alarm Notification Template</a></td>
</tr>
</tbody></table>



## Directions



1. Log in to the [Tencent Cloud Observability Platform](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy configuration page.
3. Click **Add** and configure a new alarm policy as shown below:

<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="5"> Basic info</td>
    <td>Policy name</td>
    <td>Custom policy name</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>Custom policy remarks</td>
  </tr>
  <tr>
    <td>Monitor type</td>
    <td>Types include Tencent Cloud service monitoring, application performance monitoring, frontend performance monitoring, and cloud automated testing</td>
  </tr>
  <tr>
    <td>Policy type</td>
    <td>Select the desired policy type for monitoring Tencent Cloud services.</td>
  </tr>
  <tr>
    <td>Projects</td>
    <td>This configuration item has two functions:<br>   
         <ul>
             <li>Manage alarm policies. Alarm policies of a project can be quickly located in the alarm policy list.</li>
             <li>It manages instances. Choose a project based on your needs. Then, in "Alarm Object", you can quickly select instances under the project. You can assign Tencent Cloud services to each project based on your business types. If you want to create a project, see <a href="https://intl.cloud.tencent.com/document/product/378/34726">Project Management</a>. After creating a project, you can use the console of each Tencent Cloud service to assign projects to resources. Some Tencent Cloud services such as TencentDB for MySQL do not support project assignment. In that case, you can refer to <a href="https://intl.cloud.tencent.com/document/product/236/8460">Specifying Project for Instance</a> to assign projects to the corresponding instances. If you do not have project permissions, see <a href="https://intl.cloud.tencent.com/document/product/248/36744">Cloud Access Management (CAM)</a> to get permissions.</li></td>   
  </tr>
  <tr>
    <td rowspan="4">Configure alarm rule</td>
    <td>Alarm object</td>
    <td>
      <ul>
			         <li>If you select "instance ID", the alarm policy will be associated with the selected instance.</li>
               <li>If you select "instance group", the alarm policy will be associated with the selected instance group.</li>
		            <li><b>All Objects</b>: associate the policy with all instances under the current account (permission required)</li>
           </ul>
        </td>
				<tr>
    <td>Trigger condition<br>(choosing <b>Manual Configuration</b>)</td>
    <td>
      <ul>
        <li>An alarm trigger condition is a semantic condition consisting of metric, comparison, threshold, measurement period, and N monitoring data points. You can set an alarm threshold according to the trend of metric change in the chart. <br>For example, if the metric is CPU utilization, the comparison is `>`, the threshold is `80%`, the measurement period is `5 minutes`, and the consecutive monitoring data points is `2 data points`, <br>then data on the CPU utilization of a CVM instance will be collected once every 5 minutes, and an alarm will be triggered if the CPU utilization exceeds 80% for two consecutive periods.
        </li>
    <li>Alarm frequency: you can set a repeated notification policy for each alarm rule. This way, an alarm notification will be sent repeatedly at a specified frequency when an alarm is triggered.<br>Frequency options: do not repeat, once every 5 minutes, once every 10 minutes, at an exponentially increasing interval, and other frequency options.<br><ul><li type="square">An exponentially increasing interval means that a notification is sent when an alarm is triggered the first time, second time, fourth time, eighth time, and so on. In other words, the alarm notification will be sent less and less frequently as time goes on to reduce the disturbance caused by repeated notifications.</li>
      <li>Default logic for repeated alarm notifications: the alarm notification will be sent to you at the configured frequency within 24 hours after the alarm is triggered. After 24 hours, the alarm notification will be sent once a day by default.</li></ul></li>
      </ul></td>
  </tr>
  <tr>
    <td>Configure manually <br>(event alarm)</td>
    <td>You can create event alarms so that when the Tencent Cloud service resources or the underlying infrastructure services encounter any errors, you will promptly receive notifications and can then take measures accordingly. </td>
  </tr>
  <tr>
    <td>Select template</td>
    <td>Click <b>Select template</b> and select a configured template from the drop-down list. For detailed configurations, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If a newly created template is not displayed, click <b>Refresh</b> on the right.</td>
  </tr>
   <tr>
        <td >Configure alarm notification</td>
        <td>Alarm notification</td>
        <td>You can select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38922">Notification Template</a>.</li></td>
    </tr>
		<tr>
      <td>Advanced configuration</td>
      <td >Auto scaling</td>
      <td>After this option is enabled and configured successfully, an auto scaling policy will be triggered for scaling when the alarm condition is met.</td>
     </tr>
</table>

4. After configuring the above information, click **Save**.

>? CVM alarms can be sent normally only after the monitoring [Agent](https://intl.cloud.tencent.com/document/product/248/6211) has been installed on CVM instances and reports monitoring metric data. On the Cloud Monitor page, you can view CVM instances that do not have Agent installed and download the IP address list.
