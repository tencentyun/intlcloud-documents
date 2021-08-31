This document describes how to create and delete alarm policies and set the default alarm policy.

## Use Cases

You can set threshold alarms for the performance consumption metrics of the Tencent Cloud service resources supported by Cloud Monitor. You can also set event alarms for the service status of Tencent Cloud service instances or the underlying platform infrastructure. This way, when an exception occurs, you will promptly receive notifications, which will allow you to take appropriate measures. An alarm policy consists of five required parameters: name, policy type, alarm trigger condition, alarm object, and alarm channel. You can create alarm policies by following the directions below:

## Directions

### Creating an alarm policy

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor).
2. Choose **Alarm Configuration** > **Alarm Policy** to access the alarm policy configuration page.
3. Click **Add** and configure a new alarm policy, as shown below:
   ![](https://main.qcloudimg.com/raw/35ab944e14b549e22225592ca93e4f4a.png)
<table>
	<tr>
		<th>Configuration Type</th>
		<th width="18%">Configuration Item</th>
		<th>Description</th>
	</tr>
	<tr>
		<td  rowspan="5">Basic configurations</td>
		<td>Policy names</td>
		<td>Custom policy names</td>
	</tr>
	<tr>
		<td>Notes</td>
		<td>Notes on custom policies</td>
	</tr>
	<tr>
		<td>Policy types</td>
		<td>Select the desired policy type for monitoring Tencent Cloud services.</td>
	</tr>
	<tr>
		<td>Projects</td>
		<td>This configuration item has two functions:<br>   
         <ul>
             <li>It manages alarm policies. After setting a project, you can quickly locate the alarm policies of a project in the alarm policy list.</li>
             <li>It manages instances. Choose a project based on your needs. Then, in **Alarm Object**, you can quickly select instances under the project. You can assign Tencent Cloud services to each project based on your business types. If you want to create a project, see <a href="https://intl.cloud.tencent.com/document/product/378/34726">Project Management</a>. After creating a project, you can use the console of each Tencent Cloud service to assign projects to resources. Some Tencent Cloud services such as TencentDB for MySQL do not support project assignment. In that case, you can refer to <a href="https://intl.cloud.tencent.com/document/product/236/8460">Specifying Projects for Instances</a> to assign projects to the corresponding instances. If you do not have project permissions, see <a href="https://intl.cloud.tencent.com/document/product/248/36744">Cloud Access Management (CAM)</a> to obtain permissions.</li></td>   
	</tr>
	<tr>
		<td>Alarm objects</td>
		<td>
			<ul>
			   <li>If you select "all objects", the alarm policy will be associated with all instances under the current account.</li>
               <li>If you select "some objects", the alarm policy will be associated with the selected instances.</li>
               <li>If you select "instance group", the alarm policy will be associated with the selected instance group.</li>
           </ul>
        </td>
	</tr>
	<tr>
		<td rowspan="3">Alarm trigger conditions</td>
		<td>Configuring trigger conditions<br> (metric alarms)</td>
		<td>
			<ul>
				<li>An alarm trigger condition is a semantic condition consisting of metric, comparison, threshold, measurement period, and duration.<br>For example, if the metric is CPU utilization, the comparison is `>`, the threshold is `80%`, the measurement period is `5 minutes`, and the duration is `2 periods`,<br>then data on the CPU utilization of a CVM will be collected once every 5 minutes, and an alarm will be triggered if the CPU utilization exceeds 80% for three consecutive periods.
				</li>
		<li>Alarm frequency: you can set a repeated notification policy for each alarm rule. This way, an alarm notification will be sent repeatedly at a specified frequency when an alarm is triggered.<br>Frequency options: do not repeat, once every 5 minutes, once every 10 minutes, at an exponentially increasing interval, and other frequency options.<br><ul><li type="square">An exponentially increasing interval means that a notification is sent when an alarm is triggered the first time, second time, fourth time, eighth time, and so on. In other words, the alarm notification will be sent less and less frequently as time goes on to reduce the disturbance caused by repeated notifications.</li>
			<li>Default logic for repeated alarm notifications: the alarm notification will be sent to you at the configured frequency within 24 hours after an alarm is triggered. After 24 hours, the alarm notification will be sent once every day by default.</li></ul></li>
	    </ul></td>
	</tr>
	<tr>
		<td>Configuring trigger conditions<br> (event alarms)</td>
		<td>You can create event alarms so that when the Tencent Cloud service resources or the underlying infrastructure services encounter any errors, you will promptly receive notifications and can then take measures accordingly. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/32821">Event Center</a>.</td>
	</tr>
	<tr>
		<td>Trigger condition templates</td>
		<td>Enable "Trigger Condition Template" and select a configured template from the drop-down list. For detailed configurations, see <a href="https://intl.cloud.tencent.com/document/product/248/32817">Configuring trigger condition templates</a>. If the created template is not displayed, click **Refresh** on the right.</td>
	</tr>
   <tr>
        <td rowspan="3">Alarm channels</td>
        <td>Receiving objects</td>
        <td>You can configure the receiving group or recipient as needed. If you do not have the permission to bind the receiving object, refer to <a href="https://intl.cloud.tencent.com/document/product/248/36744">Cloud Access Management (CAM)</a> to obtain permissions.</td>
    </tr>
    <tr>
    	<td>Effective periods</td>
    	<td>You can set custom effective periods for alarm notifications. By default, the effective period is all day (00:00:00 - 23:59:59).</td>
    </tr>
    <tr>
    	<td>Receiving channels</td>
    	<td>Email and SMS are supported.
    		<ul>
    			<li>Before configuring the email/SMS receiving channel, go to the <a href="https://console.cloud.tencent.com/cam" >Cloud Access Management</a> console to check whether your email and SMS have been verified. If they have not been verified, you will not be able to receive alarm notifications. For each alarm type, each user has a monthly quota of 1,000 free text messages per month. After this quota is exceeded, you will not be able to receive SMS alarm notifications. You can refer to 
    				<a href="https://intl.cloud.tencent.com/document/product/248/32815">SMS Channel</a> to purchase a higher SMS quota.
    			</li>
    		</ul>
    		</td>
     </tr>
     <tr>
     	<td>API callbacks</td>
     	<td align="center">-</td>
     	<td>Your system can directly receive Tencent Cloud alarm notifications through the callback API. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/9066">Callback API</a>.</td>
     </tr>
</table>
4. After configuring the above information, click **Save**. The alarm policy has been created successfully.
>? CVM alarms can be sent normally only after the monitoring [Agent](https://intl.cloud.tencent.com/document/product/248/6211) has been installed on CVM instances and reports monitoring metric data. On the Cloud Monitor page, you can view CVM instances that do not have Agent installed and download the IP address list.


### Deleting an alarm policy

>? The **Enabled/Instances** field in the alarm policy list displays the number of [alarm objects](/doc/product/248/6216) associated with the alarm policy. If the value is not 0, the policy cannot be deleted. Only when all alarm objects are disassociated can the policy can be deleted.

**Case 1: the alarm policy is not associated with instances.** 

Click **Delete** in the alarm policy list.
   ![](https://main.qcloudimg.com/raw/16366d1fef2d920375b378d6768d7ce8.png)

**Case 2: the alarm policy is associated with instances.** 

1. On the alarm policy list, click the name of the alarm policy you want to delete to go to the alarm policy management page.
2. In the **Alarm Object** module, click **Disassociate All** and confirm the disassociation in the pop-up window. If instances are deployed in multiple regions, you need to repeat this step until all instances in all regions have been disassociated.
	 ![](https://main.qcloudimg.com/raw/35faa0b32fd61997ee9c5821a4a8ec51.png)
3. After all instances are disassociated from the policy, return to the alarm policy list page and click **Delete**.

### Default alarm policy

Currently, the default alarm policy is only supported for: CVM-basic monitoring, TencentDB for MongoDB, TencentDB for MySQL-CVM monitoring, TencentDB for Redis, TencentDB for CynosDB-MySQL, TencentDB for CynosDB-PostgreSQL, Messaging Service CKafka-Instance, and Elasticsearch.

- When you successfully purchase a Tencent Cloud service that supports the default policy for the first time, Cloud Monitor will automatically create the default alarm policy for you. For more information on the metrics/events supported by the default policy or alarm rules, see [the default policy of Tencent Cloud services](#step1).
- You can also manually create an alarm policy and set it as the default alarm policy. After the default policy is set, newly purchased instances will be automatically associated with the default policy without requiring manual addition.
  ![](https://main.qcloudimg.com/raw/bbacd03b65c9c2ffbdb064f85df18a97.png)



>? Only one default policy is allowed for each policy type in each project.

The default alarm policy cannot be deleted.

  <span id="step1"></span>

  The default policy of Tencent Cloud services is as follows:

  <table>
  	<tr>
  		<th>Tencent Cloud Service</th>
  		<th>Alarm Type</th>
  		<th>Metric/Event Name</th>
  		<th>Alarm Rules</th>
  	</tr>
  	<tr>
  		<td rowspan="5">CVM</td>
  		<td rowspan="4">Metric alarms</td>
  		<td>CPU utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>
  	</tr>
  	<tr>
  		<td>Memory utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>	
  	</tr>
  	<tr>
  		<td>Disk utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>	
  	</tr>
  	<tr>
  		<td>Public bandwidth utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>	
  	</tr>
  	<tr>
  		<td>Event alarm</td>
  		<td>Disk read-only</td>
  		<td>-</td>
  	</tr>
  	<tr>
  		<td rowspan="3">TencentDB <br>for MySQL-CVM monitoring</td>
  		<td rowspan="2">Metric alarms</td>
  		<td>Disk utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
  	</tr>
  	<tr>
  		<td>CPU utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
  	</tr>
  	<tr>
  		<td>Event alarm</td>
  		<td>Memory OOM</td>
  		<td>-</td>
  	</tr>
  	    <td rowspan="2">TencentDB <br>for MongoDB</td>
  	    <td rowspan="2">Metric alarms</td>
  	    <td>Disk usage</td>
  	    <td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td>Connection usage</td>
      	<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td nowrap="nowrap">TencentDB <br>for Redis-CKV version/community version</td>
      	<td>Metric alarm</td>
      	<td>Capacity usage</td>
      	<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td rowspan="2">TencentDB <br>for CynosDB-MySQL</td>
      	<td rowspan="2">Event alarms</td>
      	<td>Memory OOM</td>
      	<td rowspan="2">-</td>
      </tr>
      <tr>
      	<td>Instance read-only (disk capacity limit exceeded)</td>
      </tr>
          <td rowspan="2">TencentDB <br>for CynosDB-PostgreSQL</td>
          <td rowspan="2">Event alarms</td>
          <td>Insufficient memory</td>
          <td rowspan="2">-</td>
      </tr>
      <tr>
      	<td>Memory OOM</td>
      </tr>
      <tr>
          <td>Message Queue<br> CKafka-Instance</td>
          <td>Metric alarm</td>
      	<td>Disk usage percentage</td>
      	<td>The measurement period is 1 minute; the threshold is >85%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td rowspan="4">Elasticsearch service</td>
      	<td rowspan="4">Metric alarms</td>
      	<td>Avg disk usage</td>
      	<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
     </tr>
     <tr>
     	    <td>Avg CPU usage</td>
     	    <td>The measurement period is 1 minute; the threshold is >90%; the duration is 5 periods</td>
     </tr>
     <tr>
     	    <td>Avg JVM memory usage</td>
     	    <td>The measurement period is 1 minute; the threshold is >85%; the duration is 5 periods</td>
     </tr>
     <tr>
     	    <td>Cluster health</td>
     	    <td>The measurement period is 1 minute; the threshold is >=1; the duration is 5 periods</td>
     </tr>
  </table>
