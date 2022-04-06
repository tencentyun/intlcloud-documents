
## Overview
To prevent the normal operation of your system from being affected when a monitoring metric reaches a certain value, you can configure alarm rules for these metrics. When the monitoring data meets the configured conditions, the system can automatically check it and send alarm notifications to the admin. This helps you stay on top of business exceptions and quickly solve them. 

## Billing
- CM allows you to configure alarm policies to monitor the key metrics of instances and offers a free trial.
- Currently, only **alarm SMS messages** are charged. For more information, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/248/18728).

## Prerequisites
- You have activated CM.
- The database instance is in **Running** status.
- You have collected the information of the recipients of alarm notifications, such as email address and phone number.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **instance list** on the right, select the region.
3. In the instance list, find the target instance.
4. In the row of the target instance, enter the **Create Policy** page of CM in any of the following ways:
   - Click <img src="https://qcloudimg.tencent-cloud.cn/raw/8e01de7cd5dd07c6d2626aaba4c2288c.png" style="zoom: 50%;" /> in the **Monitoring/Status/Task** column and click **Configure Alarms** in the top-right corner of the instance monitoring data panel.
     ![](https://main.qcloudimg.com/raw/ee9553aef95de034ecb4c505a573d75f.png)
   - Click the **instance ID** in blue to enter the **Instance Details** page. Then, click the **System Monitoring** tab, select the **Monitoring Metrics** tab, and click **Set Alarms**.
     ![](https://qcloudimg.tencent-cloud.cn/raw/9b942bdb2f05a028fda4639c3946065b.png)
5. On the **Create Policy** page, configure the policy as shown below. For more information on the basic concepts of alarm policy, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).
   ![](https://main.qcloudimg.com/raw/e164f26773457a00ca7e153383f51390.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Policy Name</td><td>Customize the alarm policy name for easier identification.</td></tr>
<tr>
<td>Remarks</td><td>Briefly describe the alarm policy for easier identification.</td></tr>
<tr>
<td>Monitoring Type</td><td>Select <strong>Cloud Product Monitoring</strong>.</td></tr>
<tr>
<td>Policy Type</td>
<td>Select <strong>TencentDB/Redis/Memory Edition (5-Second Granularity)/Redis Node</strong> or <strong>TencentDB/Redis/Memory Edition (1-Minute Granularity)/Redis Node</strong> as needed.</td></tr>
<tr>
<td>Project</td>
<td>Specify a project for the alarm policy. You can quickly locate all alarm policies of a project in the alarm policy list.</td></tr>
<tr>
<td>Alarm Object</td>
<td>Select the alarm object based on the <strong>instance ID</strong> or <strong>instance group</strong>. For more information on how to group instances, see <a href="https://intl.cloud.tencent.com/document/product/248/35268">Instance Group</a>.</td></tr>
<tr>
<td>Trigger Condition</td>
<td>Configure an alarm trigger condition by <strong>selecting a template</strong> or through <strong>manual configuration</strong>. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38916">Creating Alarm Policy</a>.</td></tr>
<tr>
<td>Alarm Notification</td>
<td>Select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most. For more information, see <a href="https://cloud.tencent.com/document/product/248/50394">Alarm Notification Template</a>.</td></tr>
</tbody></table>
6. After confirming that the configuration is correct, click **Complete**. For more information on alarms, see [Alarm Overview](https://Intl.cloud.tencent.com/document/product/248/6126).

## Related APIs
| API                                                 | Description |
| :----------------------------------------------------------- | :------------------- |
| [CreateAlarmPolicy](https://intl.cloud.tencent.com/document/product/248/39326) | Creates CM alarm policy |


