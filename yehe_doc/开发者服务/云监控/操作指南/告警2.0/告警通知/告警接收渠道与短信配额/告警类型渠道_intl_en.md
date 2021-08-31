## Alarm Type

Cloud Monitor alarms divide into two types: basic monitoring alarms and custom notification alarms.

| Alarm Type | Description |
| ------- | ---------------------------------------- |
| Basic alarm | Alarms triggered by monitoring items (metrics and events) provided by Tencent Cloud service resources |
| Custom notification | Business alarms triggered by the custom notification service of Cloud Monitor |

## Alarm Channel

Cloud Monitor provides three alarm channels: SMS, email, and phone (in beta test).

Both the SMS and email channels are enabled for all alarm policies by default. To receive alarm messages, you need to enter and verify the contact information (including mobile number and email address) of the recipient in the [CAM Console](https://console.cloud.tencent.com/cam).

Currently, the SMS channel has a quota limit. After the quota of a channel is used up, alarm notifications will no longer be sent through this channel.

## Alarm Channel Coverage


| Alarm Type | SMS | Email | Phone |
| ------- | ---- | ---- |---- |
| Basic alarm | Supported | Supported | Supported (in beta test) |
| Custom notification | Supported | Supported | Supported (in beta test) |
