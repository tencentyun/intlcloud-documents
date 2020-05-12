## Trial/Testing Application Limit
- A trial application supports up to 1,000 devices in a test. If the limit is exceeded, the trial may be terminated. Therefore, do not use it for commercial purpose to avoid potential losses.
- A testing application supports up to 1,000 devices in a test. If the limit is exceeded, the use of application may be terminated. Therefore, do not use it for commercial purpose to avoid potential losses.

## Android/iOS Message Content Limit
- On Android and iOS, the size of a push message body cannot exceed 4 KB, and this limit applies to the `message` field in the Push API.

### Limit on using Android vendor-specific channels 
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
>If the length limit is exceeded, message push through the corresponding vendor-specific channel will fail. In this case, the message will be pushed through the TPNS channel.


## API Use Limits
- When calling the API for batch push, you can specify up to 1,000 device tokens or accounts.
- When calling the API for push by tag, the list of tags can contain up to 512 characters.
- In full push, the same message can be pushed only once per hour, but there are no limits on the frequency and number of pushes for other push objects.
- The call frequency limit for a statistics-related API is 200 calls/hour.

## Limits on Number of Pushes and Push Rate

- The number of pushes through the TPNS channel is unlimited. For more information on the limit on the number of pushes through Android vendor-specific channels, please see [Limits on Number of Pushes for Vendor-Specific Channels](https://cloud.tencent.com/document/product/548/36675#.E5.90.84.E9.80.9A.E9.81.93.E6.B6.88.E6.81.AF.E5.8F.91.E9.80.81.E6.9C.89.E9.99.90.E5.88.B6.E5.90.97.EF.BC.9F).
- The push rate for the TPNS channel is not limited by default. If you need to limit the rate, you can use the relevant API for customization. For more information, please see [Optional Parameter Description](https://intl.cloud.tencent.com/document/product/1024/33764).
- For more information on the limit on the push rate for Android vendor-specific channels, please see [Limits on QPS for Vendor-Specific Channels](https://cloud.tencent.com/document/product/548/41407).
