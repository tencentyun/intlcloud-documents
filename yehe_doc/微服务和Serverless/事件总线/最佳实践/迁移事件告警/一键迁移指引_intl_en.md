## Feature Description
If you are currently using Cloud Monitor (CM) Event Center, EventBridge had automatically migrated your existing CM **alarm policies** and **push targets** at the end of April 2022 to ensure smooth user experience.

## Limits
1. This migration involves only **event alarm** policies. For metric alarms, you can still configure and manage them in the CM console.
![](https://qcloudimg.tencent-cloud.cn/raw/c847311f108601a2f0c406c4b58a706f.png)
2. Policies will be migrated by service. The conversion logic for a single alarm rule is as shown below. After migration, alarms will be configured for all resources of the specific service under your account. The number of alarm policies remains the same before and after the migration. If you want to configure alarms for specified resources, you can manually adjust the alarm rules. For more information, see [Alarm Policy Configuration](https://intl.cloud.tencent.com/document/product/1108/45206).
![](https://qcloudimg.tencent-cloud.cn/raw/157790efa462957756733e39600e0b29.png)
3. **Alarm policies**, **push targets**, and **platform events** will all be migrated together, and the corresponding event rules and targets will be created for your **Tencent Cloud service event bus** in the **Guangzhou** region.
