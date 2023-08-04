## Overview

This document describes how to create, modify, enable, disable, copy, and delete an alarm policy in the alarm module of iPaaS.

You can use an alarm policy to set a threshold alarm for metrics such as number of execution failures for a launched integration app. In this way, you will promptly receive notifications and can then take measures accordingly when an exception occurs. An alarm policy consists of alarm name, alarm object, alarm condition, and alarm notification template.

## Basic Concepts

<table>
<thead>
<tr>
<th width="15%">Term</th>
<th width="85%">Definition</th>
</tr>
</thead>
<tbody><tr>
<td width="15%">Alarm policy</td>
<td width="85%">It consists of alarm name, description (optional), alarm condition, alarm object, and alarm notification template.</td>
</tr>
<tr>
<td>Alarm name</td>
<td>It is the name of an alarm policy.</td>
</tr>
<tr>
<td>Description</td>
<td>The alarm description is a simple definition of the purpose of the alarm policy.</td>
</tr>
<tr>
<td>Alarm object</td>
<td>It can be a launched integration app.</td>
</tr>
<tr>
<td>Alarm condition</td>
<td>An alarm condition is a semantic condition consisting of metric, judgment logic, judgment condition, statistical period, and number of consecutive monitoring periods.</td>
</tr>  
<tr>
<td>Notification template</td>
 <td>A notification template can be quickly reused for multiple alarm policies, making it suitable for alarm receipt in various use cases. For more information, see <a href="https://www.tencentcloud.com/document/product/1165/51641#new">Creating notification template</a>.</td>
</tr>
</tbody></table>

## Use Limits

| Feature | Limit |
|---------|---------|
| Alarm object | Up to three items can be added. |
| Alarm condition | Up to four items can be added. |

## Directions

### Creating an alarm policy

1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login).
2. On the left sidebar, select **Ops center** > **Alarm settings** > **Alarm policies** to enter the alarm policy settings page.
3. Click **Create** and configure a new alarm policy as detailed below:
<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="2">Configure basic information</td>
    <td>Policy name</td>
    <td>Custom policy name.</td>
  </tr>
  <tr>
    <td>Description</td>
    <td>Custom policy description.</td>
  </tr>
  <tr>
    <td rowspan="2">Configure alarm rule</td>
    <td>Alarm object</td>
    <td>
		<ul style="margin:0;">
	 <li>Select an app name. The alarm policy will be bound to the selected app and all of the app’s flows.
	  <li>Select one or more target regions. Only the integration app in the selected regions will be triggered when the trigger condition is met.
		</ul>
		</td>
				<tr>
    <td>Alarm condition</td>
    <td>
      <ul style="margin:0;">
        <li><b>Alarm trigger condition: </b>It is a semantic condition consisting of metric, judgment logic, judgment condition, statistical period, and number of consecutive periods. You can set an alarm threshold based on the trend shown in the chart. <br>For example, if the metric is set to `Number/Total number of app triggers`, judgment logic to `>`, judgment condition to `10`, statistical period to `1` minute, and the number of consecutive periods to `Last 3 periods`, <br>the number/total number of app triggers is collected once every minute, and if the number/total number of triggers of an app is greater than 10 for three consecutive times, an alarm will be triggered.
        </li>   
    <li><b>Alarm frequency: </b>You can set a repeated notification policy for each alarm rule. In this way, an alarm notification will be sent at a specified frequency when an alarm is triggered.<br>Frequency options: Once every 5 minutes, once every 15 minutes, once every 30 minutes, once every 12 hours, and other frequency options.
      </ul></td>
			 </tr>
   <tr>
        <td >Configure alarm notification</td>
				  <td>Notification template</td>
        <td>You can create a custom alarm notification template. Each alarm policy can be associated with one template. For more information, see <a href="https://www.tencentcloud.com/document/product/1165/51641">Notification Template</a>.</li></td>
    </tr>
</table>
4. After configuring the above information, click **Confirm**.

>?For the metric description, see [Monitoring Metric Description](https://www.tencentcloud.com/document/product/1165/51635#vocabulary).

### Modifying an alarm policy

1. Log in to the iPaaS console and go to the [**Alarm policies**](https://ipaas.tencentcloud.com/login) page.
2. Click the name of the target alarm policy.
3. On the **Edit alarm policy** page, directly modify the relevant information and click **Confirm**.

### Enabling/Disabling an alarm policy

You can use the alarm toggle feature to enable or disable an alarm policy as needed. This allows you to disable unwanted alarm policies to get rid of redundant messages. You can also quickly enable the disabled alarm policy again when needed. 

1. Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login).
2. Select **Alarm settings** on the left sidebar and click **Alarm policies** to enter the management page.
3. Click the toggle in the **Status** column of the target policy to enable or disable alarms for the policy.
   ![](https://qcloudimg.tencent-cloud.cn/raw/254522f162fc66cbf5da010fd473f820.png)

### Copying an alarm policy

1. Log in to the iPaaS console and go to the [**Alarm policies**](https://ipaas.tencentcloud.com/login) page.
2. Click **Copy** in the **Operation** column of the target alarm policy.
3. Modify the information of the copied alarm policy on the redirected page and click **Complete**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/f87da39f21b3f0beea4208ba65c53778.png)

### Deleting an alarm policy

1. Log in to the iPaaS console and go to the [**Alarm policies**](https://ipaas.tencentcloud.com/login) page.
2. Click **Delete** in the **Operation** column of the target alarm policy and confirm the deletion in the pop-up window.
> ?Only disabled policies can be deleted.
>
![](https://qcloudimg.tencent-cloud.cn/raw/ab3e8e8a8b437e7074f84fece463f6fb.png)
