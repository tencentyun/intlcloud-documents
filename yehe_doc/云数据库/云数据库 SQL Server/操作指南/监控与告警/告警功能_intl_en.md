
## Overview
You can create an alarm to warn you of the status change of a cloud product and send related messages. The created alarm determines whether an alarm notification needs to be triggered according to the comparison results between a monitoring metric and a specific threshold at every interval.

You can take appropriate precautionary or remedial measures in a timely manner when the alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, please see [Alarm Configuration](https://intl.cloud.tencent.com/document/product/248/38916) in Cloud Monitor.

If you want to send an alarm message for a specific status of a product, you need to create an alarm policy first, which is composed of three mandatory components: name, type, and alarm trigger condition. Each alarm policy is a set of alarm trigger conditions in the logical OR relationship, i.e., as long as one of the trigger conditions is satisfied, the alarm will be triggered. The alarm notification will be sent to all users associated with the alarm policy. They can take appropriate actions after receiving the notification.

>!Make sure that you have set the default alarm recipient; otherwise, the default alarm policy of TencentDB won't be able to send notifications.

## Directions
### Creating alarm policy
1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. In the alarm policy list, click **Add**.
3. Set the policy name, policy type, target project, alarm object, and trigger condition.
 - **Policy Type**: select TencentDB for SQL Server.
 - **Alarm Object**: the object instance to be associated with can be found by selecting the region where the object is located or searching for the instance ID of the object.
 - **Trigger Condition**: it is a semantic condition composed of metric, comparison, threshold, statistical period, and duration. For example, if the metric is disk utilization, the comparison is >, the threshold is 80%, the statistical period is 5 minutes, and the duration is two statistical periods, then the data on disk utilization of a database will be collected once every five minutes, and an alarm will be triggered if the disk utilization exceeds 80% for two consecutive times. For suggested alarm threshold values, please see the metric optimization suggestions in [Monitoring Feature](https://intl.cloud.tencent.com/document/product/238/7524).
 - **Configure Alarm Notification**: you can select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most.
 ![](https://main.qcloudimg.com/raw/797c0d83a473b42796ce3ac1f6c71126.png)
4. After confirming that everything is correct, click **Complete**.

### Associating object
After the alarm policy is created, you can associate some alarm objects with it. When an alarm object satisfies an alarm trigger condition, an alarm notification will be sent.
1. In the [alarm policy list](https://console.cloud.tencent.com/monitor/alarm2/policy), click the name of an alarm policy to enter the alarm policy management page.
2. Click **Alarm Object** > **Add Object** on the alarm policy management page.
![](https://main.qcloudimg.com/raw/335f5dee96fe2a58098009b6c9bd74b8.png)
3. In the pop-up window, select a desired alarm object and click **OK** to associate it with the alarm policy.


