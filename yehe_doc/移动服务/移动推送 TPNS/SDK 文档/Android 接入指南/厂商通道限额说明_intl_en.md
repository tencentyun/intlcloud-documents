## Vivo Push Channel
### Quota description
- The daily message delivery limit is calculated based on the number of SDK subscriptions. If the actual number of SDK subscriptions is below 10,000, it will be calculated as 10,000; otherwise, the actual number will be used. Currently, the ratio between single pushes and group pushes is not limited. The number of users to whom single-push and group-push messages can be sent cannot exceed the daily message delivery limit.
- Public message: push messages include full-push, group-push, and tag-push messages. A user can receive up to 5 public messages per day. The number of arrived messages is counted in the quota. Once a message arrives at a user phone, no matter whether notification is enabled on the phone, the quota will decrease by one.
  - Full push: one full push can be sent to all application users subscribing to Vpush (`turnOPush` succeeds on the client) per day by default. If the number of messages arrived at user phones reaches the quota, excessive messages will not be sent.
 - Group push: a group push can be used to send a message to multiple users. The number of user phones at which a message arrives is counted in the quota; for example, if a message arrives at the clients of 500 valid users, 500 will be deducted from the quota. "Group push message body" refers to the group push message body saved by calling an API, whose quantity limit is 1,000 by default and increases with the number of SDK subscriptions.
 - Tag push: the rule is the same as that of group push.
- Personalized information message: it refers to single push, for which only the daily total number of pushes is limited, while the number of pushes that can be received by one user is not limited. One message can be sent to only one user, and the quota will decrease by one once a message arrives at a valid `regId`.
 
### Quota query guide

- You can view the number of SDK subscriptions and total number of deliverable messages in **[Vivo Push Platform](https://dev.vivo.com.cn/openAbility/pushNews)** > **Push Statistics** > **Push Data**. For more information, please see [Vivo Push Platform User Guide](https://dev.vivo.com.cn/documentCenter/doc/151#w2-36381313).

## OPPO Platform Limits
### Quota description
 - For a public message channel (suitable for pushing universal messages to multiple users by default), if the total number of users is smaller than 50,000, the number of allowed pushes will be 100,000; otherwise, the number of allowed pushes will be the total number of users multiplying by 2.
 - For a private message channel (suitable for pushing private messages to individual users), the number of pushes is not limited. For more information, please see [OPPO Private Message Channel](https://intl.cloud.tencent.com/document/product/1024/35719).
 
### Quota query guide
 - Query in console: you can query the cumulative number of users in [Opush](https://push.oppo.com), which is refreshed once every day.
 - Query through API: please see [OPPO Push Server API](https://open.oppomobile.com/wiki/doc/#id=10696).

## Mi Platform Limits
### Quota description
 - The number of general messages (default universal messages delivered to multiple users) that can be pushed per day is 5 times the number of daily connected MIUI devices of the application. If the number of such devices is below 10,000, 50,000 messages can be pushed per day.
 - The number of notification messages (private messages to single users) that can be pushed is not limited. For more information, please see [Mi Push Message Limit Description](https://dev.mi.com/console/doc/detail?pId=2086).
 >If the number of pushes through the vendor channel exceeds the daily limit, excessive push tasks will be delivered through the TPNS channel.
 
### Quota query guide 
  - Query in console: you can query the number of daily connected MIUI devices in [Mi Open Platform](https://dev.mi.com/console/appservice/push.html) > Push Operation Platform > Push Statistics > User Data > Detailed Data.
  - Query through API: for more information on how to query the total number of deliverable messages and number of arrived messages for a day, please see [Mi Push Message Limit Description](https://dev.mi.com/console/doc/detail?pId=2086#_0_1).

## Meizu Platform Limits
### Quota description
 - The push rate of one business is limited, which is 500 pushes per second per application by default.
 - The daily number of pushes of one business is limited, which is 1000 pushes per day by default.
 - The number of subscribed tags of one business cannot exceed 100.
 - If the number of pushed messages of one business to a device reaches 4, the messages will be collapsed. If they are not clicked after a prolonged time, they may be moved to the message inbox in the top-right corner.
 - If a device is inactive for a month, its subscription will be canceled.
 - The number of API requests that can be initiated at one IP address per hour is limited, and the specific limit is not disclosed by Meizu.
 - The total number of API requests that can be initiated by one business per day is limited, and the specific limit is not disclosed by Meizu.
 - The total number of pushed messages by one business per day is limited, and the specific limit is not disclosed by Meizu.

## Huawei Platform Limits
### Quota description
 - Limit on number of delivered messages: up to 3,000 messages can be sent to one single device per day, and if the limit is exceeded, the push feature will be restricted for 24 hours. If the number of messages sent to one single device exceeds 100,000 per day, the push permission will be banned directly, and you need to rectify your application and submit your rectification plan to apply for push permission again to Huawei.
 - Limit on push rate: Huawei Push Kit calculates and assigns the push rate mainly based on the application's monthly active users (MAUs) and category of the application in Huawei AppGallery.


