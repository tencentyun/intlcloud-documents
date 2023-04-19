With tightening restrictions over the push limit and frequency of vendor channels, the push reach rate and delivery speed are also affected. For specific restrictions, see:

- [Vendor Channel Limit Description](https://www.tencentcloud.com/document/product/1024/35829)
- [Vendor Channel QPS Limit Description](https://www.tencentcloud.com/document/product/1024/35247)

Tencent Push Notification Service provides two channel assignment policies: smart assignment and custom. These policies can help improve the overall push reach rate and delivery speed against the restrictions of the vendor channels.

## Channel Overview

| Channel Type | Applicable Condition | Supported Mobile Brand |
|---------|---------|---------|
|Tencent Push Notification Service channel | The application process is online | All brands |
| <nobr>Android vendor channels</br>(Huawei, Mi, Meizu, vivo, OPPO, and FCM)</nobr> | <nobr>Application process online or offline</nobr> | Huawei, Mi, Meizu, vivo, OPPO, OnePlus, Black Shark, realme, iQOO, Honor, and other mobile phones with Google Services Framework |
| iOS vendor channel (APNs) | <nobr>The application process is online or offline</nobr> | Apple |

## Channel Policy Overview

### Smart assignment[](id:zhineng)

Tencent Push Notification Service will, based on the device status, segment active status, and push channel status, intelligently assign the optimal delivery channel for each device to achieve the following effects:

1. Improve the overall push reach rate.
2. Speed up the message arrival overall.
3. Save the resources of the vendor channels.

### Custom channel policy[](id:zidingyi)

Currently, vendor channels limit the daily number of pushes. You can choose the channels through which this push can be delivered according to business needs and personalize the push channel delivery policy to save vendor channel resources and maximize the value of pushes.
The table below specifies the delivery rules of a custom policy.

| Channel                                                  | Enabled                                                        | Disabled                   | Supported Messages                                               |
| ----------------------------------------------------- | ------------------------------------------------------------ | ---------------------- | ------------------------------------------------------------ |
| Android vendor channels </br>(Huawei, Mi, Meizu, vivo, OPPO, and FCM)| Both the vendor channel and the Tencent Push Notification Service channel are available for this push.<br>Note: <li>If the **Tencent Push Notification Service preference** is enabled, this push is preferentially delivered through the Tencent Push Notification Service channel when the device is online.<li>Otherwise, the vendor channel will be preferred.<li>If the vendor channel push fails, the Tencent Push Notification Service channel will be used to retry the push.<li>If Tencent Push Notification Service channel is disabled, the push can only be delivered with the vendor channel.| You can disable the Tencent Push Notification Service channel or the vendor channel.| Notification bar messages                                              |
|  iOS vendor channels (APNs) | Both the APNs and Tencent Push Notification Service channels are available for the push.<br>Note: <li>If the **Tencent Push Notification Service preference** feature is enabled, this push is preferentially delivered through the Tencent Push Notification Service channel when the device is online.<li>Otherwise, the APNs channel is preferred.<li>If the APNs channel push fails, the Tencent Push Notification Service channel will be used to retry the push.<li>If Tencent Push Notification Service channel is disabled, the push can only be delivered with the vendor channel.</li> |You can disable the Tencent Push Notification Service channel or the vendor channel. | Notification bar messages and silent messages. <br/>**Note**: The APNs channel supports delivering up to 3 silent messages to a device per hour.  |
| Tencent Push Notification Service                                                  | The Tencent Push Notification Service channel is available for the push.                                       | The Tencent Push Notification Service channel can be disabled.            | Notification bar messages, in-app messages, and silent messages.<br/>**Note**: The Tencent Push Notification Service channel for iOS only takes effect in iOS SDK 1.2.8.0 or later. |


## Directions

### Setting the policy in the console

You can select a channel policy for a push in the following path when creating it in the console:
**[Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns) > Message Management > Task List> Create Push > Advanced settings> Channel Policy**

#### Smart assignment

Select **Smart assignment**. The system will intelligently assign the delivery channel for each device. For more information, see the rules given in [Smart assignment](#zhineng).
![](https://main.qcloudimg.com/raw/b53a8b8e21b37aefea81fe7c8c7553c4.png)

#### Custom policy for Android channels

Select **Custom**. Click **View details** to check vendor-specific quota information.
![](https://main.qcloudimg.com/raw/a28f612612f856e05bd8e0758805500b.png)
You can choose the channel used for push according to the remaining quota of the current vendor channels and the priority of the push task. For more information, see the rules given in [Custom channel policy](#zidingyi). We recommend selecting **It is preferentially delivered through Tencent Push Notification Service channel when the device is online** to save vendor channel resources.
![](https://main.qcloudimg.com/raw/a86a6ccee99087fe9507de555eed8542.png)

>! The Tencent Push Notification Service channel can be disabled.
>

#### Custom policy for iOS channels

You can choose the channel used for push based on the priority of the push task. For more information, see the rules given in [Custom channel policy](#zidingyi). We recommend selecting **It is preferentially delivered through Tencent Push Notification Service channel when the device is online** to ensure the fastest notification delivery to the device.
![](https://main.qcloudimg.com/raw/9f79ff7b6dddbf1d03a06327fda20507.png)

### Setting the policy with RESTful APIs

Set the optional `channel_rules` parameter for the RESTful API. For more information, please see [channel_rules parameter description](https://www.tencentcloud.com/document/product/1024/33764#channel_rules-parameter-description) in the Push API documentation.
Below is a sample push on Android:
```json
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae*************8d884aada5bb2"
    ],
    "message_type": "notify",
    "channel_rules": [
        {
            "channel": "mz",
            "disable": true  //Disable the Meizu channel
        },
        {
            "channel": "xm",
            "disable": false  //Enable the Mi channel
        }
    ],
    "tpns_online_push_type":0, //The push will be delivered through the Tencent Push Notification Service channel by default when the device is online
    "message": {
        "title": "The push will be delivered through the Mi channel, and the Meizu channel is not needed",
        "content": "Push content",
        "android": {
             "custom_content":"{\"key\":\"value\"}"
        }
    }
}
```

Below is a sample push on iOS:
```
{
		"audience_type": "token",
		"environment": "dev",
		"token_list": ["05da87c0ae********fa9e08d884aada5bb2"],
		"message_type": "notify",
		"channel_rules": [{
			"channel": "apns",
			"disable": true
		}],
		"tpns_online_push_type": 0,
		"message": {
			"title": "The push will be delivered through the Tencent Push Notification Service channel only",
			"content": "Push content",
			"ios": {
				"aps": {
					"alert": {
						"subtitle": "Push subtitle"
					},
					"badge_type": -2,
					"sound": "Tassel.wav"
				},
				"custom_content": "{\"key\":\"value\"}"
			}
		}
}
```

