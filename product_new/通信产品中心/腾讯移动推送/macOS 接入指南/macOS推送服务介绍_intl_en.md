# macOS Push Service Introduction

Pushing messages on macOS involves three roles: client app, APNs (Apple Push Notification service), and TPNS server (XG Provider). All three roles needs to work together to successfully push messages to the client. If an issue occurs with any one of the roles, the push process could fail. 

TPNS platform currently only supports APNs for push messages targeting macOS devices. It does not currently support in-app message delivery.



## SDK Description

### Document Group

 * XG_SDK_Cloud_macOS.framework
 * XGMTACloud_macOS.framework

### Version Description

- Supports macOS 10.8 and above;
- Designed for macOS10.14 and above;
  1. Introduction of UserNotification.framework is required.
  2. Xcode 10.0 or above is recommended.



### Key Features Description

macOS SDK is an API provided for developers to push messages to clients. It is primarily responsible for the following operations:

- Automatic acquisition and registration of device tokens, reducing the access threshold.
- Binding APIs for accounts, tags, and devices makes it easier for developers to push notifications to specific groups and provides a variety of push methods.
- Click volume report, the number of times the message is clicked by a user.



## Channel Description

For an introduction on the message delivery channel APNs used by TPNS, see: <a href="https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1">APNs </a>

