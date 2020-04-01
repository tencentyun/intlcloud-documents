## Scenarios
If you want to send an alarm notification regarding the specific status of a product, you need to create an alarm policy first. It consists of three mandatory components: name, type, and alarm trigger. You can create an alarm policy as instructed below.

## Directions
>The **Enabled/Instances** field in the alarm policy list displays the number of [alarm objects](https://intl.cloud.tencent.com/document/product/248/6216) associated with the alarm policy. If the value is not 0, the policy cannot be deleted. Only when all alarm objects are disassociated can the policy can be deleted.

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to enter the alarm policy configuration page.
3. Click **Add** to configure an alarm policy.
4. Configure the basic items as shown below:
 - Policy Name: enter a policy name.
 - Remarks: add remarks to the policy.
 - Policy Type: select the monitoring metric.
 - Project: select a project as needed.
![](https://main.qcloudimg.com/raw/4f122237bff63a3699d767157b94b1d9.png)
5. Configure alarm objects.
 - If you select "all objects", the alarm policy will be associated with all instances under the current account.
 - If you select "some objects", the alarm policy will be associated with the selected instances.
 - If you select "Instance group", the alarm policy will be associated with the selected instance group.
![](https://main.qcloudimg.com/raw/e085a6ea7899220604c96682893b3f79.png)
6. Set the alarm trigger. You can either choose a trigger condition template or configure one on your own.
 - Trigger condition template
 Enable "Trigger Template" and select a configured template from the drop-down list. For detailed configurations, please see [Configuring Trigger Templates](https://intl.cloud.tencent.com/document/product/248/32817). If a newly create template is not displayed, click **Refresh** on the right.
![](https://main.qcloudimg.com/raw/6690243b816e73fe97332eaaad6a2b7e.png)
 - Configure trigger condition
Enable "Configure trigger conditions", which includes "Indictor alarm" and "Event alarm".
An alarm trigger is a semantic condition consisting of metric, comparison, threshold, statistical period, and duration. <br>For example, if the metric is CPU utilization, the comparison is `>`, the threshold is `80%`, the statistical period is `5 minutes`, and the duration is `2 periods`, then data on CPU utilization of the CVM will be collected once every 5 minutes, and an alarm will be triggered if the CPU utilization exceeds 80% for three consecutive periods.
You can set a repeated notification policy for each alarm rule, so an alarm notification will be sent repeatedly at specified frequency when an alarm is triggered.
Frequency options: never repeat, every 5 minutes, every 10 minutes, and other frequencies that increase exponentially.
Exponential increase means that when an alarm is triggered for the first time, second time, fourth time, eighth time, ..., or 2 to the power of Nth time, alarm notifications will be sent. In other words, the alarm notification will be sent less and less frequently with longer time interval in between, reducing the disturbance caused by repeated notifications.
![](https://main.qcloudimg.com/raw/ef09e9e9a90886e83d1ffd0f42f592e7.png)
7. Configure the alarm channel.
Configure the recipient group, valid time period, and receipt channel (email, object, and WeChat).
![](https://main.qcloudimg.com/raw/d7fffec2c8787955df96edfb221cc6ac.png)
>CVM alarms will be sent only if [Agent](/doc/product/248/6211) has been installed on CVM to report monitoring metric data. On the Cloud Monitor page, you can view CVM instances that do not have Agent installed and download the IP list.
8. You can set an existing policy as the default alarm policy, which will be automatically associated with newly purchased CVMs.
![](https://main.qcloudimg.com/raw/378c8513d9af42664934b1d830c6b34a.png)
>
>- Only one default policy in the same policy type is allowed for each project.
>- The default alarm policy cannot be deleted.
>- Cloud Monitor will automatically create a default CVM alarm policy (alarms will be triggered when disks become read-only or unreachable ping occurs) and a default TencentDB policy (alarms will be triggered if the used disk capacity is greater than 90 MB or disk utilization exceeds 80% for 5 minutes).
