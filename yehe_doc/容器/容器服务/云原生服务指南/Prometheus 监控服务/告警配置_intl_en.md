
## Overview
This document describes how to configure alarm policies in cloud native monitoring.  

## Prerequisites

Before configuring alarm policies, you need to perform the following operations:
- Create a TMP instance.
- Associate the desired clusters with the TMP instance.
- Configure the information to be collected.

## Directions

### Configuring alarm policies

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar.
2. On the instance list page, select an instance name that needs to configure alarm policies to go to its details page.
3. On the **Alarm configurations** page, click **Create alarm policy**.
![](https://qcloudimg.tencent-cloud.cn/raw/a77281e19dde819b6ff47d1db0ee816b.png)
4. On the **Create alarm policy** page, add the details of the alarm policy.
  * **Name**: Name of the alarm policy.
  * **Policy template**: Select a policy template as needed.
  * **Rule**:
    - **Rule name**: Name of alarm rule (up to 63 characters).
    - **Rule description**: The description of the alarm rule.
    - **PromQL**: The statement of the alarm rule. You can use the default value or customize it. It indicates an alert trigger condition based on a PromQL expression, which is used to calculate whether there is time series data meeting the condition.
    - **Label**: Prometheus labels of each rule.
    - **Annotation**: It indicates that users are allowed to define additional message for the alarm.
    - **Alarm content**: The alarm notifications to be sent to recipients through email and SMS when an alarm is triggered.
    - **Duration**: When the condition described in the above statement reaches the duration specified here, an alarm will be triggered.
  * **Convergence time**: In this specified period, if the alarm condition is met multiple times, only one notification is sent.
  * **Delivery method**: The delivery channel of alarm notifications.
  * **Alarm notification**: You can customize the alarm notification template, including template name, notification type, target audience and delivery method. For details, see [Notification Template](https://intl.cloud.tencent.com/document/product/1116/43196).
  * **Save the current alarm policy as the template**: The default template name is the alarm policy name. You can edit the template name and template content in the template settings after saving.
5. Click **Complete**.

>! The alarm policy will take effect by default once created.

### Pausing alarming
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **TMP** in the left sidebar.
2. On the instance list page, select an instance name that needs to pause alarming to go to its details page.
3. On the **Alarm configurations** page, click **Pause alarming** on the right side of the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/cffd3de9e2fd861f9474f874a30a7af0.png)
4. In the **Disable alarm policy** pop-up window, click **OK**.

