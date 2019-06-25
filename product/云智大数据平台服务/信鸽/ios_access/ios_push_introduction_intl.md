Pushing messages on iOS involves client app, APNs (Apple Push Notification service), and TPNS server (XG Provider). Their collaboration in the entire process is needed to successfully push messages to the client. An exception of any component can lead to push message failure.

For message pushes to iOS devices, TPNS currently only uses the APNs channel. We currently do not support message delivery via in-app specific channels.

## How Push Works

![How push works](https://main.qcloudimg.com/raw/9847d1ccfc81791799ccf41c096bb877.png)

Below are the steps for the iOS client to implement the push process:

- Step 1: Establish a TSL connection between the client device and the APNs. The APNs need to verify the validity of the device;
- Step 2: The client app requests the token used to push the message from the APNs at the appropriate time via the API provided by the system (internal implementation in the SDK);
- Step 3: The client app registers the token obtained from the APNs to the TPNS server at the appropriate time (internal implementation in the SDK);
- Step 4: Create a push message via the console (xg.qq.com) or REST API, and then the TPNS requests the APNs to deliver the message;
- Step 5: After receiving the push message request from the TPNS server, the APNs delivers the message to the specified device according to the token.

As you can see in the process above, the <font color=##FF0000>connected status</font> of the device is crucial.

## SDK Description

### File Composition

```XGPush.h```: The header file where the SDK provides APIs;

```libXG-SDK-Cloud.a```: Static library file;



### Release Notes

- iOS 6.0+ supported;
- For iOS 10.0+:
  1. You need to additionally reference UserNotification.framework;
  2. It is recommended to use Xcode 8.0+;
  3. If you are using Xcode 7 or below, you need to configure the iOS SDK on your own to support the compilation of the UserNotification framework.



### Overview of Main Features

The iOS SDK contains the APIs provided by TPNS for message push implementation and is mainly responsible for:

- Automated getting and registration of the device token to lower access threshold;
- The binding of account, tag, and device, so that you can implement message pushes to specific user groups for diversified push methods;
- Reporting taps, i.e., the number of times the messages are tapped by users.



## Channel Overview

For more information about the APNs channel used by TPNS, see <a href="https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1">APNs </a>.
