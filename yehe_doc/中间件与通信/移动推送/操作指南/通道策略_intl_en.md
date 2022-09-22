With tightening restrictions over the push limit and frequency of vendor channels, the push reach rate and delivery speed are also affected. For specific restrictions, please see:

- [Vendor Channel Limit Description](https://intl.cloud.tencent.com/document/product/1024/35829)
- [Vendor Channel QPS Limit Description](https://intl.cloud.tencent.com/document/product/1024/35247)

TPNS provides two channel assignment policies: smart assignment and custom. These policies will improve the overall push reach rate and delivery speed against the restrictions of the vendor channels.

## Channel Overview

| Channel Type | Applicable Condition | Supported Mobile Brand |
|---------|---------|---------|
| TPNS channel | Application process online | All |
| <nobr>Android vendor channels</br>(Huawei, Mi, Meizu, vivo, OPPO, and FCM)</nobr> | <nobr>Application process online or offline</nobr> | Huawei, Mi, Meizu, vivo, OPPO, OnePlus, Black Shark, realme, iQOO, Honor, and other mobile phones with Google Services Framework |
| iOS vendor channel (APNs) | <nobr>Application process online or offline</nobr> | Apple |

## Channel Policy Overview

### Smart assignment[](id:zhineng)

TPNS will take into account the device status, segment active status, and push channel status to intelligently assign the optimal delivery channel for each device to achieve the following effects:

1. Improve the overall push reach rate.
2. Speed up the overall message arrival.
3. Save the resources of the vendor channels.

### Custom channel policy[](id:zidingyi)

Currently, the Mi, OPPO, and vivo channels limit the daily number of pushes. You can choose the channels through which this push can be delivered according to business needs and personalize the push channel delivery policy to save vendor channel resources and maximize the value of pushes.
The table below specifies the delivery rules of a custom policy.

| Channel                                                  | Enabled                                                        | Disabled                   | Supported Messages                                               |
| ----------------------------------------------------- | ------------------------------------------------------------ | ---------------------- | ------------------------------------------------------------ |
| Android vendor channels</br>(Huawei, Mi, Meizu, vivo, OPPO, and FCM) | Both vendor channels and the TPNS channel are available for the push. <br>Note: <li>If the TPNS preference feature is enabled, this push is preferentially delivered through the TPNS channel when the device is online. <li>If the TPNS preference feature is disabled, this push is preferentially delivered through an available vendor channel. <li>If the vendor channel push fails, the TPNS channel will be used to retry the push. | Only the TPNS channel is available for the push. | Notification bar message |
| iOS vendor channel (APNs) | Both the APNs and TPNS channels are available for the push. <br>Note: <li>If the TPNS preference feature is enabled, this push is preferentially delivered through the TPNS channel when the device is online. <li>If the TPNS preference feature is disabled, this push is preferentially delivered through the APNs channel. <li>If the APNs channel push fails, the TPNS channel will be used to retry the push.</li> | Only the TPNS channel is available for the push. | Notification bar message and silent message <br/>**Note**: the APNs channel supports delivering up to three silent messages to a device per hour. |
| TPNS                                                  | The TPNS channel is available to the push.                                       | The TPNS channel cannot be disabled.            | Notification bar message, in-app message, and silent message<br/>**Note**: the TPNS channel for iOS only takes effect in iOS SDK 1.2.8.0 or later. |


## Getting Started

### Console

When creating a push in the console, you can select a channel policy for it in the following path:
[**TPNS Console**](https://console.cloud.tencent.com/tpns)  -> **Message Management**-> **Task List** -> **Create Push** -> **Advanced Settings** -> **Channel Policy**

#### Smart assignment

Select **Smart assignment**. The system will intelligently assign the delivery channel for each device. For more information, please see the rules of [smart assignment](#zhineng).
![](https://main.qcloudimg.com/raw/b53a8b8e21b37aefea81fe7c8c7553c4.png)

#### Custom policy for Android channels

Select **Custom**. You can click **View Details** to see the vendor quota details.
![](https://main.qcloudimg.com/raw/a28f612612f856e05bd8e0758805500b.png)
You can choose the channel used for push according to the remaining quota of the current vendor channels and the priority of the push task. For more information, please see the rules of the [custom policy](#zidingyi). We recommend selecting **It is preferentially delivered through TPNS channel when the device is online** to save vendor channel resources.
![](https://main.qcloudimg.com/raw/a86a6ccee99087fe9507de555eed8542.png)

>! The TPNS channel cannot be disabled.
>

#### Custom policy for iOS channels

You can choose the channel used for push based on the priority of the push task. For more information, please see the rules of the [custom policy](#zidingyi). We recommend selecting **It is preferentially delivered through TPNS channel when the device is online** to ensure the fastest notification delivery to the device.
![](https://main.qcloudimg.com/raw/9f79ff7b6dddbf1d03a06327fda20507.png)

### RESTful API

Set the optional `channel_rules` parameter for the RESTful API. For more information, please see [channel_rules parameter description](https://intl.cloud.tencent.com/document/product/1024/33764#channel_rules-parameter-description) in the Push API documentation.
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
    "tpns_online_push_type":0, //The push will be delivered through the TPNS channel by default when the device is online
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
			"title": "The push can only be delivered through the TPNS channel",
			"content": "Push content",
			"ios": {
				"aps": {
					"alert": {
						"subtitle": "Push subtitle"
					},
					"badge_type": -2,
					"sound": "Tassel.wav"
				},
				"custom_content":"{\"key\":\"value\"}",
			}
		}
}
```

