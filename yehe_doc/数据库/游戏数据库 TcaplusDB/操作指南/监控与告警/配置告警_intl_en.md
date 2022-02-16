## Operation Scenarios
You can create an alarm to warn you of the status change of a cloud product and send related messages. The created alarm determines whether an alarm notification needs to be triggered according to the comparison results between a monitoring metric and a specific threshold at every interval.
You can take appropriate precautionary or remedial measures in a timely manner when the alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, please see [Alarm Configuration](https://intl.cloud.tencent.com/document/product/248/38916) in Cloud Monitor.

If you want to send an alarm message for a specific status of a product, you need to create an alarm policy first, which is composed of three mandatory components: name, type, and alarm trigger condition. Each alarm policy is a set of alarm trigger conditions in the logical OR relationship, i.e., as long as one of the trigger conditions is satisfied, the alarm will be triggered. The alarm notification will be sent to all users associated with the alarm policy. They can take appropriate actions after receiving the notification.

>Make sure that you have set the default alarm recipient; otherwise, the default alarm policy of TencentDB won't be able to send notifications.


## Directions
### Creating alarm policy
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. In the alarm policy list, click **Add**.
3. Set the policy name, policy type, target product, alarm object, and trigger condition.
 - Policy Type: select "TcaplusDB".
 - Alarm Object: select all objects or specified tables. The object to be associated with can be found by selecting the region where the object is located or searching for the ID of the object.
 - Trigger Condition: an alarm trigger is a semantic condition consisting of metric, comparison relationship, threshold, statistical period, and duration.
 - Supported alarm channel include SMS and email.
4. After confirming that everything is correct, click **Complete**.

### Associating object
After the alarm policy is created, you can associate some alarm objects with it. When an alarm object satisfies an alarm trigger condition, an alarm notification will be sent.
1. In the alarm policy list, click the name of an alarm policy to enter the alarm policy management page.
2. Click **Add Object** on the alarm policy management page.
![](https://main.qcloudimg.com/raw/00833b7ad2a481ec65b1eb14c0d2cad4.png)
3. Select a desired Tencent Cloud service and click **Apply** to associate it with the alarm policy.

### Setting alarm recipient
Alarm recipients are those who will receive alarm messages.
1. In the alarm policy list, click the name of an alarm policy.
2. On the alarm policy management page, select **Alarm Recipient Object** and click **Edit**.
3. Select the user group to be notified, set relevant options, and click **Save**.

