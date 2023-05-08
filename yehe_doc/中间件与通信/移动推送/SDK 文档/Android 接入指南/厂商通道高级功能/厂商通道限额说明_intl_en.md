
## Vivo Channel Limits

### Quota description
#### Message push quota description
- Official messages include system messages and operation messages. The quota depends on the number of SDK subscriptions. A subscription number smaller than 10,000 will be counted as 10,000. If the number exceeds 10,000, the actual number of subscriptions will be counted. If you need to upgrade the system message volume, please see [How to Apply for Vivo System Message](https://www.tencentcloud.com/document/product/1024/36250).
 - System message: includes emails, user-specified reminders, logistics messages, order messages, to-do/to-read, financial messages, feature reminders, and instant messages.
 - Operation message: includes but is not limited to operation-facilitating messages for advertisements, recommendations, promotions, as well as events, user-triggered messages, and unsubscribed video/audio messages, product promotions, advertisements, discounts, red pockets, and coupons.
- The number of testing system messages and testing operation messages that can be sent is limited to 10,000 per day and 100 per day, respectively. There can be up to 20 testing devices.
- Currently, the ratio of single push and group push is not limited. The number of users to whom the single/group push messages can be pushed should not exceed the total daily quota.

#### Message receive quota description

- A user can receive up to 5 operation messages a day from an application, while the number of system messages is not limited. This limit might be adjusted according to users’ feedback and experience. The specific quota is subject to the official announcement of Vivo.
- The number of messages a user can receive from an application is counted based on whether the number of messages **arrived** exceeds 5, which will be checked during message sending. If exceeded, Vivo will control and decide whether messages can still be sent to the device.

### Quota query guide

You can view the number of SDK subscriptions and the total number of deliverable messages in [vivo Push Platform](https://dev.vivo.com.cn/openAbility/pushNews) > **Push Statistics** > **Push Data**. For more information, see [vivo Push Platform User Guide](https://dev.vivo.com.cn/documentCenter/doc/151#w2-36381313).

## OPPO Channel Limits

### Quota description

- For a public message channel (suitable for pushing universal messages to multiple users by default), if the total number of users is smaller than 50,000, the number of allowed pushes will be 100,000; otherwise, the number of allowed pushes will be twice the total number of users.
- For a private message channel (suitable for pushing private messages to individual users), the number of pushes is not limited. For more information, see [OPPO notification channel overview](https://www.tencentcloud.com/document/product/1024/36250).
- For the OPPO channel (including public and private message channels), the maximum number of messages that can be received by a single user is 2000 per day.
For the maximum number of messages delivered per device, see [here](https://open.oppomobile.com/new/developmentDoc/info?id=11210).
<table>
<thead>
<tr>
<th colspan = "2" style="width:30%">Type</th>
<th style="width:50%">Public Message Channel</th>
<th style="width:20%">Private Message Channel</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = "2">Single user push limit (number of messages per day)</td>
<td>News (third-level category)</td>
<td>5</td>
<td>Unlimited</td>
</tr>
<tr>
<td>Other application types</td>
<td>2</td>
<td>Unlimited</td>
</tr>
<tr>
<td colspan = "2">Maximum number of pushes</td>
<td>All public message channels share a total number of pushes. If the daily limit is reached, they will stop pushing messages on the day. The current maximum number of daily pushes is twice the total number of all registered users.</td>
<td>Unlimited</td>
</tr>
</tbody></table>

### Quota query guide

- Query in the console: you can query the cumulative number of users on the [OPPO PUSH Operation Platform](https://push.oppo.com), which is refreshed once every day.
- Query through API: see [OPPO PUSH Platform Server-side API](https://developers.oppomobile.com/wiki/doc/index#id=71).

## Mi Channel Limits

### Quota description

- The total number of public messages (default universal messages to multiple users) that can be pushed per day is the number of MIUI devices with applications installed and the notification bar enabled multiplied by a factor. The multiplication factor is 2 by default and is 3 if the applications have the Internet News Information Service License, as shown in Table 1. If the number of devices with the notification bar enabled is less than 10,000, it will be calculated as 10,000.
- The number of private messages (private messages to single users) that can be pushed is not limited. For more information, see [Mi notification channel overview](https://intl.cloud.tencent.com/document/product/1024/36250).

The multiplication factor-based quota limit on public messages is effective from February 1, 2023. For more information, see [Mi Push Message Restrictions](https://dev.mi.com/distribute/doc/details?pId=1656).

| With the Internet News Information Service License | Multiplication Factor to Calculate the Maximum Number of Notifications Pushed Per Device Per Day Per Application | Maximum Number of Notifications Received Per Device Per Day Per Application |
|------------------------------|-------------------------------------------|--------------------------------|
|Yes        |3      |8     |
|No        |2      |5     |

> ?If the number of pushes through the vendor channel exceeds the daily limit, excessive push tasks will be delivered through the Tencent Push Notification Service channel.

### Quota query guide 

- Query in the console: you can query the number of daily connected MIUI devices in [Mi Open Platform](https://dev.mi.com/console/appservice/push.html) > **Push Operation Platform** > **Push Statistics** > **User Data** > **Detailed Data**.
- Query through API: for more information on how to query the total number of deliverable messages and number of arrived messages per day, see [Mi Push Message Limit Description](https://dev.mi.com/console/doc/detail?pId=2086#_0_1).

## Meizu Channel Limits

### Quota description

- There is a limit on the push rate for one application, which is 500 pushes per second per application by default.
- The daily number of pushes of one application is limited, which is 1,000 pushes per day by default.
- The number of subscribed tags of one application cannot exceed 100.
- If the number of pushed messages of one application to a device reaches 4, the messages will be collapsed. If they are not clicked after a prolonged time, they may be moved to the message box in the upper-right corner.
- If a device is inactive for a month, its subscription will be canceled.
- The number of API requests that can be initiated at one IP address per hour is limited, and the specific limit is not disclosed by Meizu.
- The total number of API requests that can be initiated by one application per day is limited, and the specific limit is not disclosed by Meizu.
- The total number of pushed messages by one application per day is limited, and the specific limit is not disclosed by Meizu.

## Huawei Channel Limits

### Quota description

- Limit on the number of messages sent: From January 5, 2023 on, the number of "information and marketing" messages pushed per day will be capped according to the type of application, while there will be no limit to the number of "service and communication" messages pushed per day. For more information, see [here](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-restriction-description-0000001361648361?ha_source=hms5).
- Limit on the push rate: Huawei Push Kit calculates and assigns the push rate mainly based on the application's monthly active users (MAUs) and category of the application in Huawei AppGallery.

## HONOR Channel Limits

### Quota description

Limit on the number of messages sent: According to message classification standards, HONOR Push classifies push messages into "information and marketing" messages and "service and communication" messages. The number of "information and marketing" messages pushed per day will be capped according to the type of application, while there will be no limit to the number of "service and communication" messages pushed per day. For more information, see [here](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-push-standards.md&token=).





