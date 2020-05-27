
Pushing messages to iOS devices involves client application (Client App), APNs (Apple Push Notification service), and TPNS server (XG Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a push message delivery failure.


## SDK Description

### File composition
- `XGPush.h`: header file where the SDK provides APIs.
- `libXG-SDK-Cloud.a`: static library file.



### Release notes

- iOS 8.0+ is supported;
- For iOS 10.0+:
 - You also need to import `UserNotification.framework`.
 - You are recommended to use Xcode 8.0+.
 - If you use the Xcode 7 version or below, you need to configure the SDK for iOS on your own to support the compilation of the `UserNotification` framework.



### Feature description
The SDK for iOS provided by TPNS contains APIs for clients to implement message pushing. It carries out the following features:
- Automated getting and registration of the device token to lower access threshold.
- Binds accounts, tags, and devices, so you can push messages to specific user groups and have more varied push methods.
- Reports the number of clicks, i.e., how many times users click a message.




For more information on the APNs channel used by TPNS, please see [APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

