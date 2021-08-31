This document describes how to create an alarm policy and configure an object to receive alarms in the Cloud Monitor Console.

## Operation Scenarios
You can create an alarm to warn you of the status change of a cloud product and send related messages. The created alarm determines whether an alarm-related notification needs to be triggered according to the comparison results between a monitoring metric and a specific threshold at every interval.
You can take appropriate precautionary or remedial measures in a timely manner when the alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, please see [Alarm Configuration](https://intl.cloud.tencent.com/document/product/248/1073) in Cloud Monitor.

If you want to send an alarm message for a specific status of a product, you need to create an alarm policy first, which is composed of three mandatory components: name, type, and alarm trigger condition. Each alarm policy is a set of alarm trigger conditions in the logical OR relationship, i.e., as long as one of the trigger conditions is satisfied, the alarm will be triggered. The alarm notification will be sent to all users associated with the alarm policy. They can take appropriate actions after receiving the notification.

>Make sure that you have set the default alarm recipient; otherwise, the default alarm policy of TencentDB won't be able to send notifications.

## Directions
### Creating alarm policy
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. In the alarm policy list, click **Create**.
3. Set the policy name, policy type, target product, alarm object, and trigger condition.
 - Policy type: it divides into master monitoring and slave monitoring, which are applicable to different types of instances.
    - Deploy monitoring on the master: when the monitored instance is a master instance which is not a slave of any instance, replicating relevant monitoring data from the master won't work, and the IO and SQL threads are disabled. Replicating relevant monitoring data can work and the IO and SQL threads can be enabled only when the monitored instance is a disaster recovery or a read-only instance.
    - Deploy monitoring on the slave: the master instance and disaster recovery instance in high-availability edition come in a master/slave architecture by default. As a result, replicating relevant monitoring data from the slave can work only when the monitored instance is a master or disaster recovery instance. Such data can be used to reflect the delay distance and time between the master or disaster recovery instance and its hidden slave nodes. You are recommended to keep an eye out for the relevant monitoring data of the slave. If the master or disaster recovery instance fails, its monitored hidden slave nodes can be promoted into the master instance quickly.
 - Trigger condition: it is a semantic condition composed of metric, comparison, threshold, statistical period, and duration. For example, if the metric is disk utilization, the comparison is >, the threshold is 80%, the statistical period is 5 minutes, and the duration is two statistical periods, then the data on disk utilization of a database will be collected once every five minutes, and an alarm will be triggered if the disk utilization exceeds 80% for two consecutive times.
 - The object instance to be associated with can be found by selecting the region where the object is located or searching for the instance ID of the object.
 ![](https://main.qcloudimg.com/raw/169e4abc7354e1e1f391a4eb80a1c9ca.png)
4. After confirming that everything is correct, click **Complete**.

### Associating objects
After the alarm policy is created, you can associate some alarm objects with it. When an alarm object satisfies an alarm trigger condition, an alarm notification will be sent.
1. In the alarm policy list, click the name of an alarm policy to enter the alarm policy management page.
2. Click **Add Object** on the alarm policy management page.
![](https://main.qcloudimg.com/raw/00833b7ad2a481ec65b1eb14c0d2cad4.png)
3. Select a desired Tencent Cloud product and click **Apply** to associate it with the alarm policy.

### Setting alarm recipient
Alarm recipients are those who will receive alarm messages.
1. In the alarm policy list, click the name of an alarm policy.
2. On the alarm policy management page, select **Alarm Recipient** and click **Edit**.
3. Select the user group to be notified, set relevant options, and click **Save**.

