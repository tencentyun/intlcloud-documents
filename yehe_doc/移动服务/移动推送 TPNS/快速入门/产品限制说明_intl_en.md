## Trial-Edition Application Limit
For applications of the trial edition, up to 1,000 devices can be used for testing. If the limit is exceeded, the trial may be terminated. To avoid loss, do not use applications of the trial edition for commercial purposes.


## Notification Title and Content Length Limits


###  Android push channel limits

| Channel       |        Notification Title Length Limit           |    Notification Content Length Limit                  |
| --------------- | ------| -------------------------------------------- |
| TPNS | 20 characters (Excess parts will be displayed as an ellipsis.) | Unlimited |
| Mi | 50 characters | 128 characters |
| Huawei | 40 characters | 80 characters |
| Meizu | 32 characters | 100 characters |
| OPPO | 32 characters | 200 characters |
| vivo | 40 characters | 128 characters |

>?
> - Pushes through vendor channels will fail if corresponding length limits are exceeded, and they will be retried through the TPNS channel.
> - Pushes through vendor channels will fail if the notification title or content is empty, and they will be retried through the TPNS channel.
> - For Android, the size of the pushed message body cannot exceed 4 KB, and this limit applies to the `message` field in the Push API.
> 



### iOS push channel limits

| Channel       |        Notification Title Length Limit           |    Notification Content Length Limit                  |
| --------------- | ------| -------------------------------------------- |
| APNs | 40 characters (Excess parts will be displayed as an ellipsis.) | <li>Up to 110 characters will be displayed in the notification center, and excess parts will be displayed as an ellipsis.<li>Up to 110 characters will be displayed when the phone screen is locked, and excess parts will be displayed as an ellipsis.<li>Up to 62 characters will be displayed in the top pop-up window, and excess parts will be displayed as an ellipsis. |
| TPNS | Same as that of APNs | Same as that of APNs |


>? For iOS, the size of the pushed message body cannot exceed 4 KB, and this limit applies to the `message` field in the Push API.


## API Use Limits
- For batch pushes through APIs, you can specify up to 1,000 device tokens or accounts at a time.
- For pushes to devices with specified tags, the tag list cannot exceed 512 characters.
- For pushes to all devices, the same message can only be sent once per hour, and there is no limit on the frequency and number of sending times for other push targets.
- The call frequency limit for statistics APIs is 200 times per hour.
- One application can have up to 10,000 custom tags. One device token can be bound to a maximum of 100 custom tags (if you want to increase this limit, please [submit a ticket](https://console.cloud.tencent.com/workorder/category)). One custom tag can be bound to an unlimited number of device tokens.

## Push Volume and Push Rate Limits

- For the TPNS channel, the push volume is unlimited. For Android vendor channels, see their push volume limits in [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829).
- For the TPNS channel, the push rate is unlimited by default. If necessary, you can call the relevant API to customize a push rate. For relevant parameter descriptions, see [Optional Parameters](https://intl.cloud.tencent.com/document/product/1024/33764#optional-parameters).
- For Android vendor channels, see their push rate limits in [Vendor Channel QPS Limit Description](https://intl.cloud.tencent.com/document/product/1024/35247).
