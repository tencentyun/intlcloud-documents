
iOS 端实现推送消息的服务涉及到三个角色：终端应用（Client App），APNs（Apple Push Notification service），腾讯移动推送服务器（XG Provider）。在使用腾讯移动推送服务实现给客户端推送消息，需要这三个角色在整个流程中相互配合，任何一个角色出现异常，都可能会导致消息推送无法收到。


## SDK 说明

### 文件组成
- `XGPush.h`，SDK 提供接口的头文件。
- `libXG-SDK-Cloud.a`，静态库文件。



### 版本说明

- 支持 iOS 8.0+。
- 针对 iOS 10.0+ 以上版本。
 - 需要额外引入 UserNotification.framework。
 - 建议使用 Xcode 8.0 +。
 - 如果使用 Xcode7 及其以下的版本，需要自行配置 iOS SDK 来支持 UserNotification 框架的编译。



### 功能说明
iOS SDK 是腾讯移动推送服务为客户端实现消息推送而提供给开发者的接口，主要负责完成：
- 设备 Token 的自动化获取和注册，降低接入门槛。
- 账号、标签与设备的绑定接口，以便开发者实现特定群组的消息推送，丰富推送方式。
- 点击量上报，统计消息被用户点击的次数。




关于腾讯移动推送使用的消息下发通道 APNs 介绍，请参见  [APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)。

