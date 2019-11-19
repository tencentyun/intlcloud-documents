## Operation Scenario
You can create an alarm to trigger alarms and send alarm messages when the status of a Tencent Cloud product changes. The created alarm can periodically determine whether an alarm notification should be sent based on the difference between the monitored metric and the given threshold.
You can take appropriate precautionary or remedial measures in a timely manner when the alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, see [Alarm Configuration](https://intl.cloud.tencent.com/document/product/248/6215) in Cloud Monitor.

If you want to send an alarm message for a specific status of a product, you need to create an alarm policy first, which is composed of three mandatory components: name, type, and alarm trigger. Each alarm policy is a set of alarm triggers in the logical OR relationship, i.e., as long as one of the triggers is satisfied, the alarm will be triggered. The alarm notification will be sent to all users associated with the alarm policy. They can take appropriate actions after receiving the notification.

>Make sure that you have set the default alarm recipient; otherwise, the default alarm policy of TencentDB won't be able to send notifications.

## Directions
### Creating an Alarm Policy
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
3. In the alarm policy list, click **Create**.
![](https://main.qcloudimg.com/raw/4aee1fdfc8d4f507a778e96b8f0a3f27.png)
4. Set the policy name, policy type, target product, alarm object, and trigger.
 - An alarm trigger is a semantic condition composed of metric, comparison, threshold, statistical period, and duration. For example, if the metric is disk utilization, the comparison is >, the threshold is 80%, the statistical period is 5 minutes, and the duration is two statistical periods, then the data on disk utilization of a database will be collected once every five minutes, and an alarm will be triggered if the disk utilization exceeds 80% for two consecutive times.
 - The object instance to be associated with can be found by selecting the region where the object is located or searching for the instance ID of the object.
 ![](https://main.qcloudimg.com/raw/127a76e637a94c3b4ab2a52f4e959633.png)
5. After confirming everything is correct, click **Complete**.

### Associating with an Object
After the alarm policy is created, you can associate some alarm objects with it. When an alarm object satisfies an alarm trigger, an alarm notification will be sent.
1. In the alarm policy list, click the name of an alarm policy to enter the alarm policy management page.
2. Click **Create**.
![](https://main.qcloudimg.com/raw/f8e744311d7f2ba5bbcdacbdfbb2558d.png)
3. Select a desired Tencent Cloud product and click **Apply** to associate it with the alarm policy.
![](https://main.qcloudimg.com/raw/546f61d49555ae6df646326904880a3c.png)

### Setting an Alarm Recipient
Alarm recipients are those who will receive alarm messages.
1. In the alarm policy list, click the name of an alarm policy.
2. On the alarm policy management page, select **Alarm Recipient Group** and click **Edit**.
![](https://main.qcloudimg.com/raw/18a927b9147e65db5982e43e52c7a164.png)
3. Select the user group to be notified, set relevant options, and click **Save**.
![](https://main.qcloudimg.com/raw/ddd28af0d55b8dc8286908e6cb93975b.png)
