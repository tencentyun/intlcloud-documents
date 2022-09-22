
Pushing messages to iOS devices involves client application (Client App), APNs (Apple Push Notification service), and Tencent Push Notification Service server (Tencent Push Notification Service Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a push message delivery failure.


## SDK Description

### File Composition

- `XGPush.h`, `XGPushPrivate.h` (header files where the SDK provides APIs)
- `libXG-SDK-Cloud.a` (main SDK file)
- `libXGExtension.a`, `XGExtension.h` ("arrival and rich media" extension library and API header file)
- `XGMTACloud.framework` ("click report" component)
- `XGInAppMessage.framework` (in-app messages)



### Release Notes

- Supports iOS 8.0 and later
- For iOS 10.0 and later
   - You need to introduce `UserNotification.framework`.
   - We recommend you use Xcode 8.0 and later
   - If you use Xcode 7 or an earlier version , you need to configure the SDK for iOS on your own to support the compilation of the `UserNotification` framework.



### Description
The SDK for iOS provided by Tencent Push Notification Service contains APIs for clients to implement message pushing. It is mainly used to:
- Get and register device tokens automatically to facilitate integration.
- Bind accounts, tags, and devices, so you can push messages to specific user groups and have more push methods.
- Report the number of clicks, i.e., how many times a message is clicked by users.


### Push channel

Message delivery channels used by Tencent Push Notification Service:
- Tencent Push Notification Service channel: the channel built by Tencent Push Notification Service. It can deliver messages only when the Tencent Push Notification Service is online (maintaining a persistent connection with the Tencent Push Notification Service backend server). It requires the SDK 1.2.8.0 or later.
- APNs channel: Apple's official message push service. For more information, please see [APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

## Flow Description

### Device registration flow

The device registration flow is as shown below. For specific API methods, see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/dbfa16df52e31f095e0dd9161656f5b7.png)



### Device unregistration flow

The device unregistration flow is as shown below. For specific API methods, see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/e099201705deb2642dfc9252356bc3c7.png) 


### Account flow

The account flow is as shown below. For specific API methods, see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/7e50fb47d21c45eb96459a0e317991e5.png)


### Tag flow

The tag flow is as shown below. For specific API methods, see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/f00a948750d2f3ac85648e78f480673a.png)

### User attribute flow

The user attribute flow is as shown below. For specific API methods, see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/8941cba3ed40b4ff02d957e6c2332d64.png)
