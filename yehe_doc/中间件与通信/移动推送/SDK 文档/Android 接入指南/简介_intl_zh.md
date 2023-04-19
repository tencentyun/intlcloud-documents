移动推送（Tencent Push Notification Service）是一款专业的移动 App 推送平台，支持百亿级的通知和消息推送，秒级触达移动用户，现已全面支持 Android 和 iOS 两大主流平台，开发者可以方便地通过嵌入 SDK，通过 API 调用或 Web 端可视化操作，实现对特定用户推送，大幅提升用户活跃度，有效唤醒沉睡用户，并实时查看推送效果。



## 功能说明

Android SDK 是移动推送服务为客户端实现消息推送而提供给开发者的接口，主要负责完成以下功能：

- 提供通知和消息二种推送形式，方便用户使用。
- 账号、标签与设备的绑定接口，以便开发者实现特定群组的消息推送，丰富推送方式。
- 点击量上报，统计消息被用户点击的次数。
- 提供多厂商通道集成功能，方便用户集成多厂商推送。


## SDK 说明

从官网上下载下来的包，解压后内容如下：
![](https://main.qcloudimg.com/raw/591f29cd6788b791c5e599707d0a4602.png)

#### 解压后根目录五个文件夹内容：

- Demo 文件夹：移动推送官方 Demo 程序，用户可以参考相关配置。
- flyme-notification-res 文件夹：魅族推送通道的资源文件，用于低版本魅族手机兼容，Flyme 6.0 及以下版本的魅族手机用户需要将对应的文件复制到 App 的 res 目录下。
- libs 文件夹：包含移动推送的 jar 和 so 文件。
- Other-Platform-SO 文件夹：包含其它不常用 CPU 架构的 so 文件。
- Other-Push-jar 文件夹：移动推送封装的华为、魅族、小米、OPPO、VIVO、FCM 的 jar 包。

#### libs 目录详细介绍
![](https://main.qcloudimg.com/raw/11b427ff202da51706d87e78a2cc6258.png)
- android-support-v4.jar： 谷歌推出的兼容包，兼容 Android1.6 以上的系统。
- jg-filter-sdk-1.1.jar：金刚扫描的 jar 包，使用腾讯 SDK 的产品必须带上。
- tpns-baseapi-sdk-x.x.x.x.jar：移动推送提供的部分底层公共 API。
- tpns-core-sdk-x.x.x.x.jar：移动推送 SDK 核心模块代码，存放所有对外的类、API 和组件。
- tpns-mqttchannel-sdk-x.x.x.x.jar：移动推送上层实现基于 MQTT 协议的通信功能，长连接独立在一个进程中。
- tpns-mqttv3-sdk-x.x.x.x.jar：移动推送改造后的 MQTT 协议包，提供多厂商通道集成功能，方便用户集成多厂商推送。


## 常用场景流程说明

### 设备注册流程

下图为设备注册相关流程，具体接口方法请查看 [启动与注册](https://intl.cloud.tencent.com/document/product/1024/30715)。
![](https://main.qcloudimg.com/raw/e795ce8ea14a01e064ba69a98cf43c5a.png)



### 设备反注册流程

下图为设备反注册相关流程，具体接口方法请查看 [反注册](https://intl.cloud.tencent.com/document/product/1024/30715)。
![](https://main.qcloudimg.com/raw/55ffc2d38b879f247ec7980d4ee44ef1.png)


### 账号相关流程

下图为账号相关流程，具体接口方法请查看 [账号管理](https://intl.cloud.tencent.com/document/product/1024/30715)。
![](https://main.qcloudimg.com/raw/3034b127932ecaa57ac1bb3adb91a9ec.png)



### 标签相关流程

下图为标签相关流程，具体接口方法请查看 [标签管理](https://intl.cloud.tencent.com/document/product/1024/30715)。
![](https://main.qcloudimg.com/raw/1dfe940d69878cc1c22a1466b8954d23.png)

### 用户属性相关流程

下图为用户属性相关流程，具体接口方法请查看 [用户属性管理](https://intl.cloud.tencent.com/document/product/1024/30715)。
![](https://main.qcloudimg.com/raw/8941cba3ed40b4ff02d957e6c2332d64.png)
