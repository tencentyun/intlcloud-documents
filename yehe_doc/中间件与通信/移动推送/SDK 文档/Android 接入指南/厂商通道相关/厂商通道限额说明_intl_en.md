
## Vivo Channel Limits

### Quota description
#### Message push quota description
- Official messages include system messages and operation messages. The quota depends on the number of SDK subscriptions. A subscription number smaller than 10,000 will be counted as 10,000. If the number exceeds 10,000, the actual number of subscriptions will be counted. If you need to upgrade the system message volume, please see [How to Apply for Vivo System Message](https://intl.cloud.tencent.com/document/product/1024/36250).
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
- For a private message channel (suitable for pushing private messages to individual users), the number of pushes is not limited. For more information, see [OPPO notification channel overview](https://intl.cloud.tencent.com/document/product/1024/36250).
- For the OPPO channel (including public and private message channels), the maximum number of messages that can be received by a single user is 2000 per day.

### Quota query guide

- Query in the console: you can query the cumulative number of users on the [OPPO PUSH Operation Platform](https://push.oppo.com), which is refreshed once every day.
- Query through API: see [OPPO PUSH Platform Server-side API](https://developers.oppomobile.com/wiki/doc/index#id=71).

## Mi Channel Limits

### Quota description

- The number of general messages (default universal messages to multiple users) that can be pushed per day is 5 times the number of daily connected MIUI devices of the application. If the number of such devices is below 10,000, 50,000 messages can be pushed per day.
- The number of notification messages (private messages to single users) that can be pushed is not limited. For more information, see [Mi notification channel overview](https://intl.cloud.tencent.com/document/product/1024/36250).

> ?If the number of pushes through the vendor channel exceeds the daily limit, excessive push tasks will be delivered through the TPNS channel.

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

- Limit on the number of delivered messages: up to 3,000 messages can be sent to one single device per day, and if the limit is exceeded, the push feature will be restricted for 24 hours. If the number of messages sent to one single device exceeds 100,000 per day, the push permission will be banned directly, and you need to rectify your application and submit your rectification plan to apply for push permission again to Huawei.
- Limit on the push rate: Huawei Push Kit calculates and assigns the push rate mainly based on the application's monthly active users (MAUs) and category of the application in Huawei AppGallery.

