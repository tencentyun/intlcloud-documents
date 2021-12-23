## Overview

This document introduces how to manage notification groups.

## Directions

### Adding notification groups

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. In the left sidebar, choose **Monitoring Alarm*** > **Notification Group** to go to the notification group management page.
3. Click **Create** and set the following parameters as required on the notification group creation page:
 - Name: custom notification group name.
 - Notification Type:
    - Alarm triggered: when the monitoring result meets the alarm trigger expression, an alarm triggered notification will be sent.
    - Alarm cleared: when the trigger condition is met in the previous monitoring period but not met in the current period and the alarm triggered notification has been sent, an alarm cleared notification will be sent.
4. Configure user notification and enter the receipt information:
 - Recipient: specified users or user groups (a user group contains multiple users).
 - Notification Period: time period for receiving alarm notifications.
 - Notify By: email, SMS, WeChat, or phone calls.
5. Configure the webhook and enter the webhook address information:
>! Up to 10 custom and WeCom webhooks are supported.
>
 - Webhook - WeCom bot
After creating a WeCom bot, just enter the URL of the webhook. For more information, please see [Receiving Alarm Notification Through a WeCom Group](https://intl.cloud.tencent.com/document/product/614/39581).

 - Webhook - custom
Enter a custom webhook address to further process and forward alarm notifications received. You can customize the request content. CLS alarm-related information can be referenced by variables, and when the alarm callback is triggered, it will be replaced with the corresponding content in the current alarm policy. For more information, please see [Custom Callback APIs](https://intl.cloud.tencent.com/document/product/614/41986).



### Copying a notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. In the left sidebar, choose **Monitoring Alarm*** > **Notification Group** to go to the notification group management page.
3. Select the notification group to copy and click **Copy**.

### Modifying a notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. In the left sidebar, choose **Monitoring Alarm*** > **Notification Group** to go to the notification group management page.
3. Select the notification group to modify and click **Edit**.


### Deleting a notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. In the left sidebar, choose **Monitoring Alarm*** > **Notification Group** to go to the notification group management page.
3. Select the notification group to delete and click **Delete**.

