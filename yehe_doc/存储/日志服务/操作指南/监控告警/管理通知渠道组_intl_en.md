## Overview

This document describes how to manage notification groups.

## Directions

### Adding notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, select **Monitoring and Alarms** > **Notification Group** to enter the notification group management page.
3. Click **Create** and set the following parameters as required on the notification group creation page:
 - Basic Info
    - Name: Custom notification group name.
    - Notification Type:
      - Triggered: When the monitoring result meets the alarm trigger expression, an alarm triggered notification will be sent.
      - Resolved: When the trigger condition is met in the previous monitoring period but not met in the current period and the alarm triggered notification has been sent, an alarm resolved notification will be sent.
 - Method: Configure user notification and enter the receipt information.
    - Type: Select a type as needed.
    - Recipient: Specified users or user groups (a user group contains multiple users).
    - Notification Period: Define the time period for receiving alarms.
    - Notify By: Email, SMS, or phone.
    - Webhook URL: Configure the API callback and enter the callback address.
>! Up to ten custom webhooks can be configured for API callback.
>      - Webhook - Custom
Enter a custom webhook address to further process and forward alarm notifications received. You can customize the request content. CLS alarm-related information can be referenced by variables, and when the alarm callback is triggered, it will be replaced with the corresponding content in the current alarm policy. For more information, see [Custom Callback APIs](https://intl.cloud.tencent.com/document/product/614/41986).



### Copying notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, select **Monitoring and Alarms** > **Notification Group** to enter the notification group management page.
3. Select the notification group to copy and click **Copy**.

### Modifying notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, select **Monitoring and Alarms** > **Notification Group** to enter the notification group management page.
3. Select the notification group to modify and click **Edit**.


### Deleting notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, select **Monitoring and Alarms** > **Notification Group** to enter the notification group management page.
3. Select the notification group to delete and click **Delete**.

