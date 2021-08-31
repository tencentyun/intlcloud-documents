
Pushing messages to iOS devices involves client application (Client App), APNs (Apple Push Notification service), and TPNS server (TPNS Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a push message delivery failure.


## SDK Description

### File composition

- `XGPush.h`, `XGPushPrivate.h` (header files where the SDK provides APIs)
- `libXG-SDK-Cloud.a` (main SDK file)
- `libXGExtension.a`, `XGExtension.h` ("arrival and rich media" extension library and API header file)
- `XGMTACloud.framework` ("click report" component)
-  `TPNSInAppMessage.framework`, `TPNSInAppMessageResource.bundle` ("in-app message" component and "in-app message" template resource package)



### Release notes

- iOS 8.0+ is supported;
- For iOS 10.0+:
  - You also need to import `UserNotification.framework`.
  - We recommend you use Xcode 8.0+.
  - If you use the Xcode 7 version or below, you need to configure the SDK for iOS on your own to support the compilation of the `UserNotification` framework.



### Feature description
The SDK for iOS provided by TPNS contains APIs for clients to implement message pushing. It is mainly used to:
- Automatically get and register device tokens to facilitate integration;
- Bind accounts, tags, and devices, so you can push messages to specific user groups and have more varied push methods;
- Report the number of clicks, i.e., how many times a message is clicked by users.


### Push channel

Message delivery channels used by TPNS:
- TPNS channel: the channel built by TPNS. It can deliver messages only when the TPNS service is online (maintaining a persistent connection with the TPNS backend server). It requires the SDK 1.2.8.0 or above.
- APNs channel: Apple's official message push service. For more information, please see [APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1).

## Flow Description

### Device registration flow

The device registration flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/dbfa16df52e31f095e0dd9161656f5b7.png)



### Device unregistration flow

The device unregistration flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/e099201705deb2642dfc9252356bc3c7.png) 


### Account flow

The account flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/7e50fb47d21c45eb96459a0e317991e5.png)


### Tag flow

The tag flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/f00a948750d2f3ac85648e78f480673a.png)

### User attribute flow

The user attribute flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30727).
![](https://main.qcloudimg.com/raw/8941cba3ed40b4ff02d957e6c2332d64.png)
