## Overview

You can set an alarm rule for a specific cloud product according to a trigger template, and then reuse the alarm rule with one click to set alarm policies, avoiding the need to set the same alarm rule repeatedly. When using a trigger template to set triggers for an alarm policy, you can edit the template and then apply it to the corresponding alarm policy group. This allows you to quickly modify the alarm policy and rules in a unified manner, improving OPS efficiency. The following describes in detail how to configure a trigger template.

## Notes

An alarm trigger is a semantic condition that consists of metric, comparison, threshold, statistical period, and duration. For example, if the metric is the disk utilization, the comparison is `>`, the threshold is 80%, the statistical period is five minutes, and the duration is two periods, CPU disk utilization data is collected every five minutes. If the CPU utilization of a Cloud Virtual Machine (CVM) is greater than 80% for three consecutive periods, an alarm is triggered.

You can set a repeated notification policy for each alarm rule. When an alarm is generated, you can define the frequency to send an alarm notification repeatedly.
Frequency options: not repeated, every five minutes, every 10 minutes, frequency increases exponentially, and other frequencies.
Frequency increases exponentially means that when an alarm is triggered for the first time, second time, fourth time, eighth time, ..., or 2 to the Nth time, alarm information will be sent to you. This means the alarm will be sent less and less frequently with longer time interval in between.

The default logic for repeated alarms is as follows:

- After an alarm is generated, alarm information is sent to you according to the configured notification frequency for 24 hours.
- After an alarm is generated for 24 hours or more but less than 72 hours, alarm notifications are sent repeatedly once every day by default.
- Alarm information is sent for the last time when the alarm has been generated for 72 hours, after which this alarm information will no longer be sent.

> ?
> - A trigger template is used to set triggers for one specific cloud product.
> - After a trigger template is modified, the corresponding alarm policy that has been applied will synchronize the latest trigger conditions.

## Steps

### Creating a trigger template

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Trigger Condition Template** to access the trigger template page.
3. Click **Create**. In the pop-up window, configure the following trigger conditions:
 - **Template Name**: Enter a template name.
 - **Remarks**: Enter template remarks.
 - **Policy Type**: Select a monitoring service, such as CVM.
 - **Use preset trigger conditions**: Select this option to enable preset CVM trigger conditions for a given monitoring item.
 - **Trigger Condition**: This includes **Indicator Alarm** and **Event Alarm**. You can click **Add** to set multiple alarm items.
![](https://main.qcloudimg.com/raw/9282a92a9440514dbc4f6609a69e848d.png)
4. Click **Save** to create a trigger template.

### Editing a trigger template

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Trigger Condition Template** to access the trigger template page.
3. Click the name of a template to be edited to access the template details page.
4. Click **Edit** to modify alarm triggers.
   ![](https://main.qcloudimg.com/raw/e36f133304ca0062f95137cb3bd3c8a6.png)
5. Modify triggers as needed.
   ![](https://main.qcloudimg.com/raw/cb616a9c452abb8fa440338d6a0d980e.png)

> ?After a trigger template associated with alarm policies is edited, the modification applies to all associated alarm policies.

### Deleting a trigger template

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Trigger Condition Template** to access the trigger template page.
3. Find the template to be deleted and click **Delete** in the column on the right.
   ![](https://main.qcloudimg.com/raw/56bc0d60357f3185ce93d949694532eb.png)
4. In the pop-up dialog boxs, click **Delete**.

> ?After a trigger template associated with alarm policies is deleted, all alarm policies associated with the template become invalid.

### Copying a trigger template

1. Log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. In the left sidebar, click **Trigger Condition Template** to access the trigger template page.
3. Find the template to be copied and click **Replication** in the column on the right.
   ![](https://main.qcloudimg.com/raw/6638d17b77829c02873a865d5644e70a.png)
4. In the pop-up dialog box, click **Copy**.

> ?When a trigger template is copied, only the triggers and rules of the template are copied. If the copied template is associated with an alarm policy, the association relationship is not copied.



