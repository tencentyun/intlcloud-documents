
iOS 端实现推送消息的服务涉及到三个角色：终端应用（Client App），APNs（Apple Push Notification service），移动推送 服务器（移动推送Provider）。在使用移动推送 服务实现给客户端推送消息，需要这三个角色在整个流程中相互配合，任何一个角色出现异常，都可能会导致消息推送无法收到。


## SDK 说明

### 文件组成

- `XGPush.h`，`XGPushPrivate.h` （SDK 提供接口的头文件）
- `libXG-SDK-Cloud.a` （主 SDK 文件）
- `libXGExtension.a` 、`XGExtension.h`（“抵达和富媒体”扩展插件库及接口头文件）
- `XGMTACloud.framework`（“点击上报”组件）
- `XGInAppMessage.framework`（应用内消息）



### 版本说明

- 支持 iOS 8.0+。
- 针对 iOS 10.0+ 以上版本。
   - 需要额外引入 UserNotification.framework。
   - 建议使用 Xcode 8.0 +。
   - 如果使用 Xcode7 及其以下的版本，需要自行配置 iOS SDK 来支持 UserNotification 框架的编译。



### 功能说明
iOS SDK 是移动推送 服务为客户端实现消息推送而提供给开发者的接口，主要负责完成：
- 设备 Token 的自动化获取和注册，降低接入门槛。
- 账号、标签与设备的绑定接口，以便开发者实现特定群组的消息推送，丰富推送方式。
- 点击量上报，统计消息被用户点击的次数。


### 推送通道

移动推送 使用的消息下发通道：
- 移动推送在线通道：移动推送在线通道是移动推送 的自建通道，依赖移动推送 Service 在线（与移动推送 后台服务器保持长连接）才能下发消息；需要 SDK 1.2.8.0 及以上版本支持。
- APNs 通道：苹果官方提供的消息推送服务，详情请参见  [APNs](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1)。

## 常用场景流程说明

### 设备注册流程

下图为设备注册相关流程，具体接口方法请查看 [启动腾讯移动推送服务](https://intl.cloud.tencent.com/document/product/1024/30727)。
![](https://main.qcloudimg.com/raw/dbfa16df52e31f095e0dd9161656f5b7.png)



### 设备反注册流程

下图为设备反注册相关流程，具体接口方法请查看 [终止腾讯移动推送服务](https://intl.cloud.tencent.com/document/product/1024/30727)。
![](https://main.qcloudimg.com/raw/e099201705deb2642dfc9252356bc3c7.png) 


### 账号相关流程

下图为账号相关流程，具体接口方法请查看 [账号管理](https://intl.cloud.tencent.com/document/product/1024/30727)。
![](https://main.qcloudimg.com/raw/7e50fb47d21c45eb96459a0e317991e5.png)


### 标签相关流程

下图为标签相关流程，具体接口方法请查看 [标签管理](https://intl.cloud.tencent.com/document/product/1024/30727)。
![](https://main.qcloudimg.com/raw/f00a948750d2f3ac85648e78f480673a.png)

### 用户属性相关流程

下图为用户属性相关流程，具体接口方法请查看 [用户属性管理](https://intl.cloud.tencent.com/document/product/1024/30727)。
![](https://main.qcloudimg.com/raw/8941cba3ed40b4ff02d957e6c2332d64.png)
