## Overview

You can set an alarm rule for a specific Tencent Cloud product through a trigger template and then reuse the alarm rule to set alarm policies for other products, eliminating the need to set the same alarm rule repeatedly. When using a trigger template to set triggers for an alarm policy, you can edit the template and then apply it to the corresponding alarm policy group. This allows you to quickly modify alarm policies and rules in a unified manner, improving OPS efficiency. This document describes how to configure a trigger template.

## Notes

An alarm trigger is a semantic condition consisting of metric, comparison, threshold, statistical period, and duration. For example, if the metric is CPU utilization, the comparison is `>`, the threshold is `80%`, the statistical period is `5 minutes`, and the duration is `2 periods`, then data on CPU utilization of a CVM will be collected once every 5 minutes, and an alarm will be triggered if the CPU utilization exceeds 80% for three consecutive periods.

You can set a repeated notification policy for each alarm rule, so an alarm notification will be sent repeatedly at specified frequency when an alarm is triggered.
Frequency options: never repeat, every 5 minutes, every 10 minutes, and other frequencies that increase exponentially.
Exponential increase means that when an alarm is triggered for the first time, second time, fourth time, eighth time, ..., or 2 to the power of Nth time, alarm notifications will be sent. In other words, the alarm notification will be sent less and less frequently with longer time interval in between, reducing the disturbance caused by repeated notifications.

The default logic for repeated alarm notifications is as follows:

- The alarm notification will be sent to you at the configured frequency for 24 hours after an alarm is triggered.
- Then, the alarm notification will be sent once every day by default.
- The alarm notification will be sent for the last time 72 hours after the alarm is triggered and then will no longer be sent.

>
> - A trigger template is used to set triggers for one specific Tencent Cloud product.
> - After a trigger template is modified, the corresponding alarm policy that has already been applied will be synced to the latest trigger.

## Directions

### Creating a trigger condition template

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the trigger template list page.
3. Click **Create**. In the pop-up window, configure the following items:
 - Template Name: enter a template name.
 - Remarks: enter template remarks.
 - Policy Type: select a monitored service, such as CVM.
 - Use preset trigger conditions: select this option to enable preset trigger conditions for the corresponding monitored product.
 - Trigger condition: this includes indicator alarm and event alarm. You can click "Add" to set multiple alarms.
![](https://main.qcloudimg.com/raw/9282a92a9440514dbc4f6609a69e848d.png)
4. Click **Save**.

### Editing a trigger condition template

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the trigger template list page.
3. Click the name of the template to be edited to enter the details page.
4. Click **Edit** to modify alarm trigger conditions.
   ![](https://main.qcloudimg.com/raw/e36f133304ca0062f95137cb3bd3c8a6.png)
5. Modify trigger conditions as needed.
   ![](https://main.qcloudimg.com/raw/cb616a9c452abb8fa440338d6a0d980e.png)

>After a trigger template associated with alarm policies is edited, the modification will apply to all associated alarm policies.

### Deleting a trigger condition template

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the trigger template list page.
3. Find the template to be deleted and click **Delete** in the column on the right.
   ![](https://main.qcloudimg.com/raw/56bc0d60357f3185ce93d949694532eb.png)
4. Click **Delete** in the pop-up dialog box.

>After a trigger template associated with alarm policies is deleted, all alarm policies associated with the template will become invalid.

### Copying a trigger condition template

1. Log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Trigger Condition Template** to enter the trigger template list page.
3. Find the template to be copied and click **Copy** in the column on the right.
   ![](https://main.qcloudimg.com/raw/6638d17b77829c02873a865d5644e70a.png)
4. Click **Copy** in the pop-up dialog box.

>When a trigger template is copied, only its trigger conditions and rules will be copied. If the trigger template is associated with alarm policies, the relationship will not be copied.



