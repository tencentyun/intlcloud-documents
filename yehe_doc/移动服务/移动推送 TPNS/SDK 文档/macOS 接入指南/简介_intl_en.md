Pushing messages to macOS devices involves client application (Client App), APNs (Apple Push Notification service), and TPNS server (TPNS Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a push message delivery failure.

>?To push messages to macOS devices, TPNS only uses the APNs channel. It currently does not support message delivery through specific in-app channels.



## SDK Description

### File composition
-  XG_SDK_Cloud_macOS.framework.
-  XGMTACloud_macOS.framework.

### Notes
- macOS 10.8+ is supported.
- For macOS 10.14+:
 - You also need to import `UserNotification.framework`;
 - We recommend you use Xcode 10.0+.



### Key features
The SDK for macOS provided by TPNS contains APIs for clients to implement message pushing. It is mainly used to:
- Automatically get and register device tokens to facilitate integration;
- Bind accounts, tags, and devices, so you can push messages to specific user groups and have more varied push methods;
- Report the number of clicks, i.e., how many times a message is clicked by users.




For more information on the APNs channel used by TPNS, please see [APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).
