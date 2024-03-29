离线唤醒功能，能够让您的 应用在`后台运行`或者`离线状态`下依然能够收到音视频通话的响铃呼叫，TUICallKit 集成了 TUIOfflinePush 组件实现离线唤醒功能，本文将介绍如何在音视频通话项目中集成`TUIOfflinePush`组件。

## 前期准备

1. **注册应用到厂商推送平台** 离线推送功能依赖厂商原始通道，您需要将自己的应用注册到各个厂商的推送平台，得到 APPID 和 APPKEY 等参数。

>! **下述两个文件在后续步骤会用到：**
>- 注册华为平台的时候，下载 `agconnect-services.json` 文件，并保存。
>- 注册 Google 平台的时候，下载 `google-services.json` 文件，并保存。
> |Google FCM                                                   |
   > | ------------------------------------------------------------ |
   > | ![img](https://qcloudimg.tencent-cloud.cn/raw/aa734c4d4a8c1c2580b964360ad66304.png) |


2. **在 IM 控制台进行配置** 

注册厂商通道需要传入自己的包名，各厂商填入的包名需保持一致，用于消息互通。记录生成的 ID，APPID 以及 APPKEY，他们会在后续步骤中用到。 



## 步骤一：下载并导入组件

1. 在 [Github](https://github.com/tencentyun/TUICalling) 中克隆/下载代码，然后拷贝 Android 目录下的 tuiofflinepush 子目录到您当前工程中的 app 同级目录中，如下图：

![img](https://qcloudimg.tencent-cloud.cn/raw/8ce4eb830c8880f523e3aa833150c864.png)﻿﻿

2. 在工程根目录下找到 `setting.gradle` 文件，并在其中增加如下代码：

```java
include ':tuiofflinepush'
```

3. 在 app 目录下找到 `build.gradle` 文件，并在其中增加如下代码，它的作用是声明当前 app 对新加入的 tuiofflinepush 组件的依赖：

```java
api project(':tuiofflinepush')
```

## 步骤二：完成工程配置

1. 在 app 目录下，找到 `build.gradle` 文件，修改应用包名为自己的包名。

```java
applicationId 'com.****.trtc'
```

2. 在 app 目录下，找到 `build.gradle` 文件，设置 `ViVo` 接入参数 `VIVO_APPKEY`、`VIVO_APPID`以及`HONOR_APPID`，避免编译或运行报错。

```java
manifestPlaceholders = [
    "VIVO_APPKEY": "PLACEHOLDER", 
    "VIVO_APPID" : "PLACEHOLDER",
    "HONOR_APPID": "PLACEHOLDER"
]
```

3. 配置 **华为** 和 **谷歌** 文件： 在 app 目录下，替换  `google-services.json` 文件，该文件为您在 [前期准备](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87) 注册 Google 平台的时候保存的文件。 在 app 目录下，增加 `agconnect-services.json`文件，该文件为您在 [前期准备](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87) 注册华为平台的时候下保存的文件。

4. 将 [前期准备](https://www.tencentcloud.com/document/product/647/50999#.E5.89.8D.E6.9C.9F.E5.87.86.E5.A4.87) 记录的 ID、APPID 和 APPKEY 填入 `PrivateConstants`文件中，并检查参数是否配置正确。**填充的参数如下：**

```java
public class PrivateConstants {
    /****** 小米离线推送参数start ******/
    // 在腾讯云控制台上传第三方推送证书后分配的证书 ID
    public static final long XM_PUSH_BUZID = 您应用分配的证书 ID;
    // 小米开放平台分配的应用APPID及APPKEY
    public static final String XM_PUSH_APPID = "您应用分配的 APPID";
    public static final String XM_PUSH_APPKEY = "您应用分配的 APPKEY";
    /****** 小米离线推送参数end ******/
}
```

>! 这一步非常重要，请认真检查参数是否配置正确。

 完成以上步骤，您的工程就具备了 `TUICallKit` 的离线唤醒功能。

## 步骤三：自定义离线通知内容

TUICallKit 提供了默认的通知样式，但是如果您需要自定义通知内容，请修改 [OfflinePushInfoConfig.java](https://github.com/tencentyun/TUICallKit/blob/main/Android/tuicallkit/src/main/java/com/tencent/qcloud/tuikit/tuicallkit/config/OfflinePushInfoConfig.java)  文件 。

```java
public static TUIOfflinePushInfo createOfflinePushInfo(Context context) {    
    TUIOfflinePushInfo pushInfo = new TUIOfflinePushInfo();    
    pushInfo.setTitle("mike");    
    pushInfo.setDesc("You have receive a new call");    
    // OPPO必须设置ChannelID才可以收到推送消息，这个channelID需要和控制台一致    
    // OPPO must set a ChannelID to receive push messages. This channelID needs to be the same as the console.    
    pushInfo.setAndroidOPPOChannelID("tuikit");    
    pushInfo.setIgnoreIOSBadge(false);    
    pushInfo.setIOSSound("phone_ringing.mp3");  
    return pushInfo;
}
```

## 常见问题

收不到离线推送通知，请 [联系我们](https://intl.cloud.tencent.com/contact-us) 进行排查。

### 1、收不到通知

用厂商控制台进行推送测试，能成功说明厂商通道没有问题。再检查 TUIOfflinePush 控制台厂商参数配置是否正确，按要求进行填写。（经测试：vivo x9必须在控制台配置消息类别）。

部分手机收到通知会放到`不重要的通知`中，请下拉状态栏，检查是否归纳到 `不重要的通知` 中。

检查 TUIOfflinePush 注册是否成功，过滤以下日志：

```java
TUIOfflinePush
```

### 2、锁屏时无法点亮屏幕

Android 手机由于厂商和平台的限制，在锁屏情况下需要不同的权限。请按以下情况进行排查。

**确认打开厂商锁屏下通知权限** 部分厂商统一做了约束，例如小米锁屏下离线通知到达时未亮屏：在**设置** > **锁屏**里，单击开关**锁屏来通知时亮屏**，打开开关。

**确认打开应用锁屏通知权限** 例如：小米 需要锁屏显示权限。

>? 如遇到该问题，需要做兼容处理，您可以加入我们的 QQ 群（592465424）进行咨询与反馈。

### 3、单击离线推送通知，拉不起通话界面

需要检查下是否查到了通话请求，可以过滤以下日志：

```java
onReceiveNewInvitation
```

### 4、应用在后台时，不能自动将通话界面拉取到前台

**将应用从后台自动拉取到前台，需要检查 App 是否开启了”后台自启动“或”悬浮窗“权限。**

值得注意的是，不同厂商、甚至同一厂商不同 Android 版本，其对于应用开放的权限以及权限名称也会存在不一致。例如，小米6只需要开启**后台弹出界面**权限，而红米需要同时打开**后台弹出界面**和**显示悬浮窗**权限。

>? 如果您在测试过程中发现手动开启了所有权限，依然无法自动拉起通话界面到前台，需要做兼容处理。
