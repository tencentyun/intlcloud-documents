## Overview

This document introduces how to manage notification groups.

## Directions

### Adding notification groups

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, click **Monitoring Alarm** > **Notification Group** to enter the notification group management page.
3. Click **Create** and set the following parameters as required on the notification group creation page:
 - Basic information
    - Name: custom notification group name.
    - Notification Type:
      - Alarm triggered: when the monitoring result meets the alarm trigger expression, an alarm triggered notification will be sent.
      - Alarm cleared: when the trigger condition is met in the previous monitoring period but not met in the current period and the alarm triggered notification has been sent, an alarm cleared notification will be sent.
 - Method: Configure user notification and enter the receipt information.
    - Type: Select a type as needed.
    - Recipient: specified users or user groups (a user group contains multiple users).
    - Notification Period: Define the time period for receiving alarms.
    - Notify By: email, SMS, Weixin, or phone calls.
    - Webhook URL: Configure the API callback and enter the callback address.
>! Up to 10 custom and WeCom webhooks are supported.
>
>    - Webhook - WeCom robot
>
>After creating a WeCom bot, just enter the URL of the webhook.

      - Webhook - custom
Enter a custom webhook address to further process and forward alarm notifications received. You can customize the request content. CLS alarm-related information can be referenced by variables, and when the alarm callback is triggered, it will be replaced with the corresponding content in the current alarm policy. For more information, please see [Custom Callback APIs](https://intl.cloud.tencent.com/document/product/614/41986).



### Copying a notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, click **Monitoring Alarm** > **Notification Group** to enter the notification group management page.
3. Select the target notification group and click **Copy**.

### Modifying a notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, click **Monitoring Alarm** > **Notification Group** to enter the notification group management page.
3. Select the target notification group and click **Edit**.


### Deleting a notification group

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, click **Monitoring Alarm** > **Notification Group** to enter the notification group management page.
3. Select the target notification group and click **Delete**.

