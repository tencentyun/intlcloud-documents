## Operation Scenarios
In a mobile phone's notification center, if multiple notifications from the same application are received, the system will collapse them according to the corresponding rule to avoid disturbing the user. However, this mechanism will reduce the exposure of a push and thus lower its operational profits.
Both Android and iOS provide corresponding native settings for you to set notification collapse categories based on the operational needs of your business. This feature can collapse notifications in the same type together to improve the readability of notifications.

## Scope of Application
| Mobile Phone OS | OS Version | SDK Version | Push Channel |
| -----------  | ------------|----------- -|------------ |
|Android| Android 7.0 or above |TPNS SDK v1.2.0.1 or above | TPNS channel |
|iOS| iOS 10 or above |TPNS SDK v1.2.0.1 or above | APNs channel |

## Directions
### Console	
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns), select **Message Push** on the left sidebar, and click **Create Push** > **Advanced Settings**.
![](https://main.qcloudimg.com/raw/ef1d3676fe5171a205cada9d189fcf63.png)
2. Set a message collapse rule as shown below:
![](https://main.qcloudimg.com/raw/e43c9d985852396e65f420762d2eb641.png)
You can use the following three options to set whether and how to collapse notifications in the device notification center:
 - System default: the system's default collapse rule will be used.
The following are system rules of certain vendors:
	- Native Android: if there are 5 or more notifications from the same application, they will be collapsed into one group. When they are collapsed, the number on the right will be the total number of collapsed unread notifications; when they are expanded, the contents of up to 8 notifications can be displayed.
	- Huawei: if there are 2 or more notifications from the same application, they will be collapsed into one group. When they are collapsed, the number on the right will be the total number of collapsed unread notifications; when they are expanded, the contents of up to 8 notifications can be displayed.
	- Mi: if there are 4 or more notifications from the same application, they will be collapsed into one group. When they are collapsed, the number on the right will be the number of collapsed notifications (up to 7); when they are expanded, the contents of up to 10 notifications can be displayed.
	- Meizu: if there are 4 or more notifications from the same application, they will be collapsed into one group. When they are collapsed, the number at the top will be the total number of notifications; when they are expanded, the contents of many notifications (above 35 currently) can be displayed.
>?Meizu phones provide an unimportant notification feature, which can place excessive notifications in the notification drawer in the top-right corner, where the notifications will not be collapsed. You can enable "Priority display" in the application notification settings to disable this feature.
	- OPPO: if there are 4 or more notifications from the same application, they will be collapsed into one group. When they are collapsed, the number on the right will be the total number of collapsed unread notifications; when they are expanded, the contents of up to 8 notifications can be displayed.
	- Vivo: if there are 2 or more notifications from the same application, they will be collapsed into one group. When they are collapsed, the total number of collapsed notifications will not be displayed; when they are expanded, the contents of up to 8 notifications can be displayed.
 - Do not collapse: a notification will not be collapsed together with other notifications from the same application.
 - Custom: notifications with the same `thread_id` will be collapsed.
>?If the priority of a notification type is low, you can set this parameter to collapse such notifications so as to avoid disturbing users. If a notification type is important and you want users to see such notifications first, you can set "Do not collapse".

### RESTful API
If you want to implement the "Do not collapse" and "Custom" options of the console, you need to customize `thread_id` in the `message` field of the `Push` API. For more information, please see [Push API - Optional Parameters](https://intl.cloud.tencent.com/document/product/1024/33764).
Below is a sample push:
```
{
    "audience_type": "token",
    "token_list": [
        "05da87c0ae******2dfa9e08d884aada5bb2"
    ],
    "message_type": "notify",
    "multi_pkg":true,
    "message": {
        "title": "Push title",
        "content": "Push content",
        "android": {
             "custom_content":"{\"key\":\"value\"}"
        }
				"thread_id":"Event_id",
				"thread_sumtext":"Marketing event"
				
    }
}
```
