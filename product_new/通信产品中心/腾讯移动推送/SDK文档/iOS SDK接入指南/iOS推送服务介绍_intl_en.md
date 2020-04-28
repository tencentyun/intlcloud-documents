# Push Service Overview

Pushing messages to iOS devices involves client application, APNs (Apple Push Notification service), and TPNS server (XG Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a push message delivery failure.

To push messages to iOS devices, TPNS only uses the APNs channel. It currently does not support message delivery through specific in-app channels.



## SDK Description

### File composition

```XGPush.h```, header file where the SDK provides APIs;

***```libXG-SDK-Cloud.a```, static library file;



### Release notes

- iOS 6.0+ supported;
- For iOS 10.0+:
  1. You also need to import `UserNotification.framework`;
  2. You are recommended to use Xcode 8.0+;
  3. If you use the Xcode 7 version or below, you need to configure the SDK for iOS on your own to support the compilation of the `UserNotification` framework;



### Overview of main features

The SDK for iOS provided by TPNS includes APIs for you to implement client-side message push services. It is mainly used for:

- Automatically obtaining and registering the device token to facilitate integration;
- Binding account, tag, and device, so you can push messages to specific user groups and have more push methods;
- Reporting the number of clicks, i.e., how many times users click a message;



## Channel Overview

For more information on the APNs channel used by TPNS, please see <a href="https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1">APNs </a>.

