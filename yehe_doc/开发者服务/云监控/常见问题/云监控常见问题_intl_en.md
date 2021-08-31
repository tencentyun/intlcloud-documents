### No monitoring data available for a CVM
The possible causes are as follows:
- The Agent is not installed or launched.
- The reporting domains cannot be resolved.
- The Agent failed to obtain the UUID.
- The CVM instance is shut down or being restarted.
- The CVM instance is under high load.

To troubleshoot, please see [CVM Has No Monitoring Data](https://intl.cloud.tencent.com/document/product/248/36208).

### How do I create Cloud Monitor (CM) alarm policies?
1. Log in to the [CM console](https://console.cloud.tencent.com/monitor).
2. Click **Alarm Configuration** > **Alarm Policy** to access the alarm policy configuration page.
3. Click **Create** to configure alarm policies.

For more information, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

### How does CM pull monitoring data?
You can obtain the monitoring data of Tencent Cloud services through the API [GetMonitorData](https://intl.cloud.tencent.com/document/product/248/39306).
For more information, see [Using API to Pull Tencent Cloud Service Monitoring Data](https://intl.cloud.tencent.com/document/product/248/39917).

### How do I quickly create a CM dashboard?
See [Quickly Creating a Dashboard](https://intl.cloud.tencent.com/document/product/248/35282)



### No alarm is received
The possible causes are as follows:
- The alarm policy has not been enabled.
- The alarm SMS quota is insufficient.
- The alarm notification channel has not been configured or verified.
- No user has been added to the recipient group.
- The alarm trigger conditions have not been met.

To troubleshoot, please see [No Alarm Is Received](https://intl.cloud.tencent.com/document/product/248/38297).

### How do I create a recipient (group)?

Alarm recipients/ recipient groups determine who can receive alarm notifications. You can put people who pay attention to the same alarm in the same group. When the alarm is triggered, people in the group will receive the corresponding alarm notification. For more information, see [Creating Recipient (Group)](https://intl.cloud.tencent.com/document/product/248/38921).
### CVM is unreachable when pinged
If you receive a an alarm notification from CVM indicating that CVM is unreachable when pinged, you can refer to [CVM Is Unreachable When Pinged](https://intl.cloud.tencent.com/document/product/248/36205) to troubleshoot. If the alarm notification disturbs you, disable it as instructed in the “Disabling the alarm policy” section in the aforementioned documentation.

For more troubleshooting information, see [CVM Is Unreachable When Pinged](https://intl.cloud.tencent.com/document/product/248/36205).
