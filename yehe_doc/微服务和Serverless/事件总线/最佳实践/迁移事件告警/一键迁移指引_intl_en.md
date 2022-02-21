## Overview
If you are currently using Cloud Monitor Event Center, EventBridge offers a **quick migration** feature to support smooth migration while ensuring an optimal user experience. It can automatically and quickly migrate your existing **alarm policies** and **push targets** in CM.

## Notes
1. This migration involves only **event alarm** policies. For metric alarms, you can still configure and manage them in the CM console.
![](https://qcloudimg.tencent-cloud.cn/raw/c847311f108601a2f0c406c4b58a706f.png)
2. Policies will be migrated by service. The conversion logic for a single alarm rule is as shown below. After migration, alarms will be configured for all resources of the specific service under your account. The number of alarm policies stays the same before and after the migration. If you want to configure alarms for specified resources, you can manually adjust the alarm rules. For more information, see [Alarm Policy Configuration](https://intl.cloud.tencent.com/document/product/1108/45206).
![](https://qcloudimg.tencent-cloud.cn/raw/157790efa462957756733e39600e0b29.png)
3. You can perform migration repeatedly. Every time you click **Migrate**, the existing alarm policy configuration in CM will automatically **overwrite** the full rule configuration in EventBridge. Therefore, proceed with caution.
4. **Alarm policies**, **push targets**, and **platform events** will all be migrated together, and the corresponding event rules and CLS log set will be created for your **Tencent Cloud service event bus** in the **Guangzhou** region.

## Migration Directions

>? The quick migration feature is only available in the **Guangzhou** region. Before any sub-account uses it, make sure that the root account has granted the required basic console permissions to the sub-account.
>
1. Log in to the [EventBridge console](https://console.cloud.tencent.com/eb), enter the event bus list page, and click **More** > **Migrating existing policies** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/f23e00afcd1af810dbdc4b62c7383964.png)
2. Confirm the information in the pop-up window and click **OK** to start migration as shown below. As the number of the alarm policies in CM varies, the migration may take 3–6 minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/498840f65822cad9b9faab0c1c266bfc.png)
3. After migration is completed, go to the [Event Rule](https://console.cloud.tencent.com/eb/rule) page and select the **default event bus** to view and manage the migrated alarm rules as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/dfe1184e33221cb3362afb089f95bfcc.png)
 To avoid duplicate alarms, the migrated rules are **disabled** by default. After all policies in CM are removed, the corresponding alarm rules will be automatically enabled in a unified manner. You can also manually enable/disable rules in the EventBridge console.
