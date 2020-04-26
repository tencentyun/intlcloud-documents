You can create an alarm to trigger alarms and send alarm messages to a certain user group when a Tencent Cloud product meets the configured condition. The created alarm can periodically determine whether an alarm notification should be sent based on the difference between the monitored metric and the given threshold.

The specified users can take appropriate precautionary or remedial measures in a timely manner when the alarm is triggered. Therefore, properly created alarms can help you improve the robustness and reliability of your applications. For more information on alarms, please see [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215).

You can create an alarm policy in the following steps:
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Alarm Configuration** > **Alarm Policy** on the left sidebar to enter the [alarm policy configuration page](https://console.cloud.tencent.com/monitor/policylist).
3. Click **Add** to configure an alarm policy.
4. Configure the basic items as shown below:
 - Policy Name: enter a policy name.
 - Remarks: add remarks to the policy.
 - Policy Type: select monitoring metrics.
 - Project: select a project as needed.

5. Configure alarm objects.
 - If you select "All objects", the alarm policy will be associated with all instances under the current account.
 - If you select "Select some objects", the alarm policy will be associated with the selected instances.
 - If you select "Select instance group", the alarm policy will be associated with the selected instance group.

6. Set the alarm trigger. You can either choose a trigger condition template or configure trigger conditions.
 - Trigger condition template
  Enable "Trigger Condition Template" and select a configured template from the drop-down list. For detailed configurations, please see [Configuring trigger condition templates](https://intl.cloud.tencent.com/document/product/248/32817). If a newly created template is not displayed, click **Refresh** on the right.
 - Configure trigger conditions
An alarm trigger is a semantic condition consisting of metric, statistical period, comparison relationship, threshold, duration, and notification frequency.
For example, if the specified metric is `inbound packets`, the statistical period is `1 minute`, the comparison relationship is `>`, the threshold is `100 packets/sec`, the duration is `2 periods`, and the notification frequency is `once per day`, then the number of inbound packets will be collected once every minute, and an alarm will be triggered once per day if the number of inbound packets of a CLB listener is over 100 packets/sec for two consecutive times.

7. Configure the alarm channel. Configure the recipient group, valid period, and receiving channel (email and object) as needed.

8. You can set an existing policy as the default alarm policy, which will be automatically associated with new CLB instances purchased.

>
>- Only one default policy in the same policy type is allowed for each project.
>- The default alarm policy cannot be deleted.
