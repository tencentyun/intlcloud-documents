This document describes how to create a notification template in the CLS console.
## Notes

| Category | Description |
| ----------------- | ------------------------------------------------------------ |
| Notification type - alarm triggered | When the monitoring result meets the alarm trigger expression, an alarm triggered notification will be triggered |
| Notification type - alarm cleared | When the trigger condition is met in the previous monitoring period but not met in the current period and the alarm notification has been sent, an alarm cleared notification will be triggered |
| User notification | Notifications can be sent to specified users |
| User group notification | A user group contains multiple users. Notifications can be sent to specified user groups |
| Receipt channel | Email, SMS, phone calls, and WeChat are supported |
| Webhook | Up to 10 custom and WeCom webhooks can be configured |



## Directions
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. Select **Monitoring Alarm** > **Notification Template** on the left sidebar and click **Create**.
3. Enter the basic information in **Create Notification Template**:
 - Template name: custom template name.
 - Notification type:
    - Alarm triggered: a notification will be sent when an alarm is triggered.
    - Alarm cleared: a notification will be sent when an alarm is resolved.
4. Configure user notification and enter the receipt information:
 - Recipient: user or user group (a collection of multiple users).
 - Notification time: time period for receiving alarm notifications.
 - Notify by: email, SMS, WeChat, or phone calls.
5. Configure webhook and enter the webhook address information:
### Webhook - WeCom robot
After creating a WeCom bot, just enter the URL of the webhook. For more information, please see [Receiving Alarm Notification Through a WeCom Group](https://intl.cloud.tencent.com/document/product/614/39581).
### Webhook - custom
You can enter a custom webhook address to further process and forward received alarm notifications. You can also customize the request content. CLS alarm-related information can be referenced by variables, and when the alarm callback is triggered, it will be replaced with the corresponding content in the current alarm policy.
In the custom webhook, **request content** supports the following alarm variables:
| Variable | Description |
| ---------------- | -------------------------------------------- |
| {{.UIN}} | Tencent Cloud account `UID` of the alarm policy |
| {{.User}} | Tencent Cloud account name of the alarm policy |
| {{.AlarmID}}  | Alarm policy ID |
| {{.AlarmName}} | Alarm policy name |
| {{.TopicName}} | The name of the log topic in the monitoring object. Multiple values will be returned if there are multiple topics |
| {{.Condition}} | Trigger condition expression |
| {{.TriggerTime}} | Alarm trigger time |
| {{.ConsecutiveAlertNums}} | The number of times the trigger condition is met |







