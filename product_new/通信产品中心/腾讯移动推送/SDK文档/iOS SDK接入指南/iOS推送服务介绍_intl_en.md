# Push service overview

Pushing messages to iOS devices involves client app, APNs (Apple Push Notification service), and TPNS server (XG Provider). They need to collaborate throughout the entire process to successfully push messages to the client. An exception from any of them can lead to a push message delivery failure.

To push messages to iOS devices, TPNS only uses the APNs channel. We currently do not support message delivery via specific in-app channels.



## SDK Description

### File Composition

```XGPush.h```, header file where the SDK provides APIs;

***```libXG-SDK-Cloud.a```, static library file;



### Version Notes

- iOS 6.0+ supported;
- For iOS 10.0+:
  1. You also need to refer to UserNotification.framework;
  2. We recommend you use Xcode 8.0+;
  3. If you use the Xcode 7 version or below, you need to configure the iOS SDK on your own to support the compilation of the UserNotification framework;



### Overview of main features

iOS SDK provided by TPNS includes APIs for developers to implement client-side message push services. It is mainly used for:

- Automatically obtaining and registering the device token to facilitate integration;
- Binding account, tag, and device, so developers can push messages to specific user groups and have more push methods;
- Reporting the number of clicks, i.e., how many times users click a message;



## Channel Overview

For more information on the APNs channel used by TPNS, see <a href="https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1">APNs </a>.

