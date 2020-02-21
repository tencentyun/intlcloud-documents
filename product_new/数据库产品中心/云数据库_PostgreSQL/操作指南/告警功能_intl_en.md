## Operation Scenarios
The alarming feature is used to trigger alarms and send alarm messages when the status of a TencentDB instance changes. The created alarm can periodically determine whether an alarm notification should be sent based on the difference between the monitored metric and the given threshold.

You can take appropriate precautionary or remedial measures timely when an alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information, please see [Alarm Configuration](https://cloud.tencent.com/doc/product/248/1073) in Cloud Monitor.

If you want to send an alarm message for a specific status of a product, you need to create an alarm policy first, which is composed of three mandatory components: name, type, and alarm trigger. Each alarm policy is a set of alarm triggers in the logical OR relationship, i.e., as long as one of the triggers is satisfied, the alarm will be triggered. The alarm notification will be sent to all users associated with the alarm policy. They can take appropriate actions after receiving the notification.

>Please make sure that you have set the default alarm recipient; otherwise, the default alarm policy of TencentDB won't be able to send notifications.

## Directions
### Step 1. Create an alarm policy
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. In the alarm policy list, click **Create**.
3. Set the policy name, policy type, target product, alarm object, and trigger.
 - An alarm trigger is a semantic condition composed of metric, comparison, threshold, statistical period, and duration. For example, if trigger conditions are configured as follows: the metric is disk utilization, the comparison is >, the threshold is 80%, the statistical period is 5 minutes, and the duration is two statistical periods, then the data on disk utilization of a database will be collected by Cloud Monitor once every five minutes, and an alarm will be triggered if the disk utilization exceeds 80% for two consecutive times.
 - The object instance to be associated with can be found by selecting the region where the object is located or searching for the instance ID of the object.
4. After confirming that everything is correct, click **Complete**.

### Step 2. Associate with an object
After the alarm policy is created, you can associate alarm objects with it. When an alarm object satisfies an alarm trigger, an alarm notification will be sent.
1. In the [alarm policy](https://console.cloud.tencent.com/monitor/policylist) list, click the name of an alarm policy to enter the alarm policy management page.
2. On the alarm policy management page, click **Create Object**.
3. Select a desired Tencent Cloud product and click **Apply** to associate it with the alarm policy.

### Step 3. Set an alarm recipient
Alarm recipients are those who will receive alarm messages.
1. In the [alarm policy](https://console.cloud.tencent.com/monitor/policylist) list, click the name of an alarm policy.
2. On the alarm policy management page, select **Alarm Recipient** and click **Edit**.
3. Select the user group to be notified, set relevant options, and click **Save**.
