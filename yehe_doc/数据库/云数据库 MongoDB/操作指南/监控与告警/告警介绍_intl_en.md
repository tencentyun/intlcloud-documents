## Operation Scenarios
TencentDB for MongoDB monitoring provides multi-dimensional custom alarm features that will send alarm messages through SMS when metric data exceeds certain thresholds.

## Directions
### Creating alarm policy
1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and select **Alarm Configuration** > **Alarm Policy** on the left sidebar.
2. In the alarm policy list, click **Add**.
3. Set the policy name, policy type, target project, alarm object, and trigger condition.
![](https://main.qcloudimg.com/raw/2c00a4d8c828e4df98ceb29ffb6beb3a.png)
4. After confirming that everything is correct, click **Complete**.

### Associating objects
After the alarm policy is created, you can associate some alarm objects with it. When an alarm object satisfies an alarm trigger condition, an alarm notification will be sent.
1. In the alarm policy list, click the name of an alarm policy to enter the alarm policy management page.
2. Click **Add Object** on the alarm policy management page.
![](https://main.qcloudimg.com/raw/40d54cb03240c507ac1461978246b6f5.png)
3. Select a desired Tencent Cloud product and click **Apply** to associate it with the alarm policy.

### Setting alarm recipient
Alarm recipients are those who will receive alarm messages.
1. In the alarm policy list, click the name of an alarm policy.
2. On the alarm policy management page, select **Alarm Recipient Object** and click **Edit**.
3. Select the user group to be notified, set relevant options, and click **Save**.
