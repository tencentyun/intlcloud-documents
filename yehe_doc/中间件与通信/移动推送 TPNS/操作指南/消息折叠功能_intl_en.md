## Overview
If a mobile phone receives multiple messages from the same application, these messages will be collapsed in the notification center according to the corresponding rule to avoid disturbing the user. However, this mechanism will reduce the exposure of a push and thus lower the operating profits.
Both the native Android and iOS systems provide the corresponding settings. You can use the message collapse feature to collapse messages of the same type based on your operation needs so that the pushed messages can be read more easily.

## Application Scope

| Mobile Phone OS | OS Version | SDK Version | Push Channel |
| -----------  | ------------|----------- -|------------ |
| Android | Android 7.0 or above | TPNS SDK v1.2.0.1 or above | TPNS channel |
| iOS | iOS 10 or above | TPNS SDK v1.2.0.1 or above | APNs channel |

## Directions
### Using the console
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns). In the left sidebar, click **Message Management** > **Task List**. Then, click **Create Push** > **Advanced Settings**.
![](https://main.qcloudimg.com/raw/ef1d3676fe5171a205cada9d189fcf63.png)
2. Set a message collapse rule, as shown in the following figure:
![](https://main.qcloudimg.com/raw/e43c9d985852396e65f420762d2eb641.png)
The following three options are provided for you to set whether and how to collapse messages in the notification center:
 - System Default: uses the default collapse rule of the system.
The following are system default rules of some vendors:
	- Native Android: If there are 5 or more messages of the same application, these messages will be collapsed into a group. The number on the right of the collapsed messages is the number of unread messages. When they are expanded, up to 8 messages can be displayed.
	- Huawei: If there are 2 or more messages of the same application, these messages will be collapsed into one group. The number on the right of the collapsed messages is the number of unread messages. When they are expanded, up to 8 messages can be displayed.
	- Mi: If there are 4 or more messages of the same application, these messages will be collapsed into one group. The number on the right of the collapsed messages is the number of unread messages (up to 7). When they are expanded, up to 10 messages can be displayed.
	- Meizu: If there are 4 or more messages of the same application, these messages will be collapsed into one group. The number at the top of the collapsed messages is the total number of messages. When they are expanded, up to 35 messages can be displayed.
>?Meizu phones provide the unimportant notification feature, which allows users to place excessive notifications in the notification drawer in the upper-right corner, where the notifications will not be collapsed. You can enable "Priority display" in the application notification settings to disable this feature.
	-  OPPO: If there are 4 or more messages of the same application, these messages will be collapsed into one group. The number on the right of the collapsed messages is the number of unread messages. When they are expanded, up to 8 notifications can be displayed.
	-  Vivo: If there are 2 or more messages of the same application, these messages will be collapsed into one group. The number of collapsed messages will not be displayed. When they are expanded, up to 8 notifications can be displayed.
 - Uncollapsed: The message will not be collapsed with other messages of the same application.
 - Custom: Messages with the same `thread_id` will be collapsed.
>?You can set this parameter for low-priority messages to collapse them. On the contrary, you can set **Uncollapsed** for important messages.

### Using RESTful APIs
If you want to implement the "Uncollapsed" and "Custom" effects of the console, you need to customize `thread_id` in the `message` field of the `Push` API. For more information, please see [Push API - Optional Parameters](https://intl.cloud.tencent.com/document/product/1024/33764).
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
        "Title": "Push title",
        "content": "Push content",
        "android": {
             "custom_content":"{\"key\":\"value\"}"
        },
	    "thread_id":"Activity_id",
	    "thread_sumtext":"Operation activity"
				
    }
}
```
