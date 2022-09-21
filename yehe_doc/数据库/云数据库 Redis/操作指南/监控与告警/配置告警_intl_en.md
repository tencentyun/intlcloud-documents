
## Overview
You can configure alarm rules for monitoring metrics to prevent your system operations from being disrupted when these metrics reach a certain value. When monitoring data meets the configured conditions, the system can check it automatically and send alarm notifications to the admin. This allows you to stay on top of business exceptions and solve them quickly. 

## Billing
- CM allows you to configure alarm policies to monitor the key metrics of instances and offers a free trial.
- Currently, only **alarm SMS messages and phone calls** are charged. For more information, see [Billing Overview](https://cloud.tencent.com/document/product/248/50130).

## Prerequisites
- You have activated CM.
- The database instance is in **Running** status.
- You have collected the information of the recipients of alarm notifications, such as email address and phone number.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **Instance List** on the right, select the region.
3. In the instance list, find the target instance.
4. In the row of the target instance, enter the **Create Policy** page of CM in any of the following ways:
   - Click <img src="https://qcloudimg.tencent-cloud.cn/raw/8e01de7cd5dd07c6d2626aaba4c2288c.png" style="zoom: 50%;" /> in the **Monitoring/Status/Task** column and click **Configure Alarms** in the top-right corner of the instance monitoring data panel.
     <img src="https://main.qcloudimg.com/raw/ee9553aef95de034ecb4c505a573d75f.png" style="zoom:150%;" />
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
<td>Monitoring Type</td><td>Select <strong>Tencent Cloud services</strong>.</td></tr>
<tr>
<td>Policy Type</td>
<td>Select <strong>TencentDB/Redis/Memory Edition (5-Second Granularity)/Redis Node</strong> or <strong>TencentDB/Redis/Memory Edition (1-Minute Granularity)/Redis Node</strong> as needed.</td></tr>
<tr>
<td>Project</td>
<td>Specify a project for the alarm policy. You can quickly locate all alarm policies of a project in the alarm policy list.</td></tr>
<tr>
<td>Alarm Object</td>
<td><ul><li>Select <strong>Instance ID</strong> to bind the alarm policy to the specified database instance.</li><li>Select <strong>Instance Group</strong> to bind the alarm policy to the specified database instance group. For more information on how to create an instance group, see <a href="https://intl.cloud.tencent.com/document/product/248/35268">Instance Group</a>.</li><li>Select <strong>All Objects</strong> to bind the alarm policy to all instances on which the current account has permissions.</li><li>Select <strong>Tag</strong> to bind the alarm policy to all instances associated with the current tag key and value.</li></ul></td></tr>
<tr>
<td>Trigger Condition</td>
<td><ul><li>If you select <strong>Select template</strong>, you can select a template file in the drop-down list, and alarms will be reported based on the trigger conditions preset in the template. For specific configurations, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If you select <strong>Configure manually</strong>, you need to configure the threshold for triggering an alarm for each metric in the <strong>Metric Alarm</strong> section below.</li>
<li><strong>Threshold Type</strong> in the <strong>Metric Alarm</strong> section: If you select **Static**, you can manually set a fixed threshold, and alarms will be triggered when the threshold is reached. If you select <strong>Dynamic</strong>, exceptions will be determined based on the dynamic threshold boundaries calculated by machine learning algorithms. </li>For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38916">Creating Alarm Policy</a>.</ul></td>
</tr>
<tr>
<td>Alarm Notification</td>
<td>Select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most. For more information, see <a href="https://cloud.tencent.com/document/product/248/50394">Alarm Notification Template</a>.</td></tr>
</tbody></table>
6. After confirming that the configuration is correct, click **Complete**. For more information on alarms, see [Overview](https://www.tencentcloud.com/document/product/248/6126).

## Related APIs
| API                                                 | Description |
| :----------------------------------------------------------- | :------------------- |
| [CreateAlarmPolicy](https://cloud.tencent.com/document/api/248/51287) | Creates a CM alarm policy |


