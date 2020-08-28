## Trial Application Limits
- A trial application supports up to 1,000 devices in a test. It may be terminated if the testing devices are more than 1,000. Therefore, do not use it for commercial purpose to avoid potential losses.

## Android/iOS Message Content Limit
- On Android and iOS, the size of a push message body cannot exceed 4 KB, and this limit applies to the `message` field in the Push API.

### Limit on using Android vendor channels
#### Android message title
Mi: up to 50 characters.
Huawei: up to 40 characters.
Meizu: up to 32 characters.
OPPO: up to 32 characters.
Vivo: up to 20 Chinese characters or 40 English characters.


#### Android message content
Mi: up to 128 characters.
Huawei: up to 80 characters.
Meizu: up to 100 characters.
OPPO: up to 200 characters.
Vivo: up to 50 Chinese characters or 100 English characters.
>If the length limit is exceeded, message push through the corresponding vendor channel will fail. In this case, the message will be pushed through the TPNS channel.


## API Use Limits
- When calling the API for batch push, you can specify up to 1,000 device tokens or accounts.
- When calling the API for tag push, the list of tags can contain up to 512 characters.
- In full push, the same message can be pushed only once per hour, but there are no limits on the frequency and number of pushes for other push objects.
- The call frequency limit for a statistics-related API is 200 calls/hour.
- One application can have up to 10,000 custom tags, and each device token can be bound to up to 100 custom tags. To increase this limit, please submit a ticket for application. One custom tag can be bound to an unlimited number of device tokens.

## Limits on Number of Pushes and Push Rate

- The number of pushes through the TPNS channel is unlimited. For more information on the limit on the number of pushes through Android vendor channels, please see [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829).
- The push rate for the TPNS channel is not limited by default. If you need to limit the rate, you can use the relevant API for customization. For more information, please see [Optional Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764).
- For more information on the limit on the push rate for Android vendor channels, please see [Vendor Channel QPS Limit Description](https://intl.cloud.tencent.com/document/product/1024/35247).
