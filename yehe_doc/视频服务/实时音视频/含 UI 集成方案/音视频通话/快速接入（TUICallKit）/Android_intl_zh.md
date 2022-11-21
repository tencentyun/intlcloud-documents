本文将介绍如何用最短的时间完成 TUICallKit 组件的接入，跟随本文档，您将在一个小时的时间内完成如下几个关键步骤，并最终得到一个包含完备 UI 界面的视频通话功能。

## 环境准备

最低兼容 Android 4.1（SDK API Level 16），建议使用 Android 5.0 （SDK API Level 21）及以上版本。

Android Studio 3.5 及以上的版本（Gradle 3.5.4 及以上的版本）。

Android 4.1 及以上的手机设备。

[](id:step1)
## 步骤一：开通服务

TUICallKit 是基于腾讯云 [即时通信 IM](https://www.tencentcloud.com/document/product/1047) 和 [实时音视频 TRTC](https://www.tencentcloud.com/document/product/647) 两项付费 PaaS 服务构建出的音视频通信组件。您可以按照如下步骤开通相关的服务并体验 7 天的免费试用服务：

1. 登录到 [即时通信 IM 控制台](https://console.tencentcloud.com/im)，单击**创建新应用**，在弹出的对话框中输入您的应用名称，并单击**确定**。
![img](https://qcloudimg.tencent-cloud.cn/raw/571d5bed98a46752933169fbf4136271.png)

2. 单击刚刚创建出的应用，进入基本配置页面，并在页面的右下角找到开通腾讯实时音视频服务功能区，单击免费体验即可开通 TUICallKit 的 7 天免费试用服务。如果需要正式应用上线，可以单击 前往加购 即可进入购买页面。
![img](https://qcloudimg.tencent-cloud.cn/raw/0860fe4f282d2d918d3911127d85120a.png)

>! IM 音视频通话能力针对不同的业务需求提供了差异化的付费版本供您选择，您可以在 IM 购买页了解包含功能并选购您适合的版本。

3. 在同一页面找到 **SDKAppID** 和 **密钥(SecretKey)** 并记录下来，它们会在后续的 [步骤四：登录 TUI 组件](#step4) 中被用到。
![img](https://qcloudimg.tencent-cloud.cn/raw/5c1b56dc1972d836c85579dd16b0634d.png)


>? **友情提示：** 单击**免费体验**以后，部分之前使用过 [实时音视频 TRTC](https://www.tencentcloud.com/document/product/647/35078) 服务的用户会提示：

```java
[-100013]:TRTC service is  suspended. Please check if the package balance is 0 or the Tencent Cloud accountis in arrears
```
因为新的 IM 音视频通话能力是整合了腾讯云[实时音视频 TRTC](https://www.tencentcloud.com/document/product/647/35078) 和 [即时通信 IM](https://www.tencentcloud.com/document/product/1047) 两个基础的 PaaS 服务，所以当 [实时音视频 TRTC](https://www.tencentcloud.com/document/product/647/35078) 的免费额度（10000分钟）已经过期或者耗尽，就会导致开通此项服务失败，这里您可以单击 [TRTC 控制台](https://console.tencentcloud.com/trtc/app)，找到对应 SDKAppID 的应用管理页，开通后付费功能后，再次**启用应用**即可正常体验音视频通话能力。


[](id:step2)
## 步骤二：下载并导入组件

在 [Github](https://github.com/tencentyun/TUICalling) 中克隆/下载代码，然后拷贝 Android 目录下的 tuicallkit 子目录到您当前工程中的 app 同级目录中，如下图：

![img](https://qcloudimg.tencent-cloud.cn/raw/4b6a74f2ee2f5d8eab00061b9fc1f112.png)

[](id:step3)
## 步骤三：完成工程配置
1. 在工程根目录下找到 `setting.gradle` 文件，并在其中增加如下代码，它的作用是将 [步骤二](#step2) 中下载的 tuicallkit 组件导入到您当前的项目中：

```java
include ':tuicallkit'
```

2. 在 app 目录下找到 `build.gradle` 文件，并在其中增加如下代码，它的作用是声明当前 app 对新加入的 tuicallkit 组件的依赖：
```java
api project(':tuicallkit')
```
>? TUICallKit 工程内部已经默认依赖：`TRTC SDK`、`IM SDK`、`tuicallengine` 以及公共库 `tuicore`，不需要开发者单独配置。如需进行版本升级，则修改`tuicallkit/build.gradle`文件即可。

3. 由于我们在 SDK 内部使用了Java 的反射特性，需要将 SDK 中的部分类加入不混淆名单，因此需要您在 `proguard-rules.pro` 文件中添加如下代码：
```bash
-keep class com.tencent.** { *; }
```
>! TUICallKit 会在内部帮助您动态申请相机、麦克风、读取存储权限等，如果因为您的业务问题需要删减，可以请修改`tuicallkit/src/main/AndroidManifest.xml`。

[](id:step4)
## 步骤四：登录 TUI 组件

在您的项目中添加如下代码，它的作用是通过调用 TUICore 中的相关接口完成 TUI 组件的登录。这个步骤异常关键，因为只有在登录成功后才能正常使用 TUICallKit 的各项功能，故请您耐心检查相关参数是否配置正确：
```java
//设置对登录结果的监听器
private final TUILoginListener mLoginListener = new TUILoginListener() {    
    @Override    
    public void onKickedOffline() {        
        super.onKickedOffline();        
        Log.i(TAG, "You have been kicked off the line. Please login again!"); 
        //logout();
    }    
    @Override    
    public void onUserSigExpired() {        
        super.onUserSigExpired();       
        Log.i(TAG, "Your user signature information has expired");        
        //logout();    
    }
};
TUILogin.addLoginListener(mLoginListener);

//登录
TUILogin.login(context, 
    1400000001,     // 请替换为步骤一取到的 SDKAppID
    "denny",        // 请替换为您的 UserID
    "xxxxxxxxxxx",  // 您可以在控制台中计算一个 UserSig 并填在这个位置
    new TUICallback() {
    @Override
    public void onSuccess() {
        Log.i(TAG, "login success");
    }

    @Override
    public void onError(int errorCode, String errorMessage) {
        Log.e(TAG, "login failed, errorCode: " + errorCode + " msg:" + errorMessage);
    }
});
```

**参数说明** 这里详细介绍一下 login 函数中所需要用到的几个关键参数：

- **SDKAppID**：在步骤一中的最后一步中您已经获取到，这里不再赘述。
- **UserID**：当前用户的 ID，字符串类型，只允许包含英文字母（a-z 和 A-Z）、数字（0-9）、连词符（-）和下划线（_）。
- **UserSig**：使用 [步骤一](#step1) 的第3步中获取的 SecretKey 对 SDKAppID、UserID 等信息进行加密，就可以得到 UserSig，它是一个鉴权用的票据，用于腾讯云识别当前用户是否能够使用 TRTC 的服务。您可以通过控制台中的 [**辅助工具**](https://console.cloud.tencent.com/im/tool-usersig) 生成一个临时可用的 UserSig。

更多信息请参见 [如何计算及使用 UserSig](https://www.tencentcloud.com/document/product/647/35166)。

>? **这个步骤也是目前我们收到的开发者反馈最多的步骤，常见问题如下：**
- SDKAppID 设置错误，国内站的 SDKAppID 一般是以140开头的10位整数。
- UserSig 被错配成了加密密钥（SecretKey），UserSig 是用 SecretKey 把 SDKAppID、UserID 以及过期时间等信息加密得来的，而不是直接把 SecretKey 配置成 UserSig。
- UserID 被设置成“1”、“123”、“111”等简单字符串，由于 **TRTC 不支持同一个 UserID 多端登录**，所以在多人协作开发时，形如 “1”、“123”、“111” 这样的 UserID 很容易被您的同事占用，导致登录失败，因此我们建议您在调试的时候设置一些辨识度高的 UserID。

>! Github 中的示例代码使用了 genTestUserSig 函数在本地计算 UserSig 是为了更快地让您跑通当前的接入流程，但该方案会将您的 SecretKey 暴露在 App 的代码当中，这并不利于您后续升级和保护您的 SecretKey，所以我们强烈建议您将 UserSig 的计算逻辑放在服务端进行，并由 app 在每次使用 TUICallKit 组件时向您的服务器请求实时计算出的 UserSig。

[](id:step5)
## 步骤五：拨打通话

### 1对1视频通话

通过调用 TUICallKit 的 call 函数并指定通话类型和被叫方的 userId，就可以发起语音或者视频通话。
```java
// 发起1对1视频通话(假设 UserID 为 mike)
TUICallKit.createInstance(context).call("mike", TUICallDefine.MediaType.Video); 
```

| 参数          | 类型                    | 含义                                                  |
| ------------- | ----------------------- | ----------------------------------------------------- |
| userId        | String                  | 目标用户的 UserID：`"mike"`                           |
| callMediaType | TUICallDefine.MediaType | 通话的媒体类型，示例：`TUICallDefine.MediaType.Video` |

### 群内视频通话

通过调用 TUICallKit 的 groupCall 函数并指定通话类型和被叫方的 UserID 列表，就可以发起群内的语音或者视频通话。
```java
TUICallKit.createInstance(context).groupCall("12345678", Arrays.asList("jane", "mike", "tommy"),TUICallDefine.MediaType.Video);
```

| 参数          | 类型                    | 含义                                                      |
| ------------- | ----------------------- | --------------------------------------------------------- |
| groupId       | String                  | 群组 Id，示例：`"12345678"`                               |
| userIdList    | List                    | 目标用户的 UserID 列表，示例：`{"jane", "mike", "tommy"}` |
| callMediaType | TUICallDefine.MediaType | 通话的媒体类型，示例：`TUICallDefine.MediaType.Video`     |

>? 群组的创建详见：[ IM 群组管理](https://www.tencentcloud.com/document/product/1047/48466) ，或者您也可以直接使用 [IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286)，一站式集成聊天、通话等场景。

TUICallKit 目前还不支持发起非群组的多人视频通话，如果您有此类需求，您可以联系：colleenyu@tencent.com。

[](id:step6)
## 步骤六：接听通话

收到来电请求后，TUICallKit 组件会自动唤起来电提醒的接听界面，不过因为 Android 系统权限的原因，分为如下几种情况：

- 您的 App 在前台时，当收到邀请时会自动弹出呼叫界面并播放来电铃音。
- 您的 App 在后台，但是有授予`悬浮窗权限`或`后台弹出应用`等权限时，仍然会自动弹出呼叫界面并播放来电铃音。
- 您的 App 在后台，且没有授予`悬浮窗权限`或`后台弹出应用`等权限时，TUICallKit 会播放来电铃音，提示用户接听或挂断。
- 您的 App 进程已经被销毁，只能通过接入[离线唤醒（Android）](https://www.tencentcloud.com/document/product/647/50991)，通过通知栏消息提示用户接听或挂断。

[](id:step7)
## 步骤七：更多特性

### 一、设置昵称&头像

如果您需要自定义昵称或头像，可以使用如下接口进行更新：
```java
TUICallKit.createInstance(context).setSelfInfo("jack", "https:/****/user_avatar.png", callback);
```

>! 因为用户隐私限制，非好友之间的通话，被叫的昵称和头像更新可能会有延迟，一次通话成功后就会顺利更新。

### 二、离线唤醒

完成以上步骤，就可以实现音视频通话的拨打和接通，但如果您的业务场景需要在 `应用的进程被杀死后`或者`应用退到后台后`，还可以正常接收到音视频通话请求，就需要增加离线唤醒功能，详情见 [离线唤醒（Android）](https://www.tencentcloud.com/document/product/647/50991)。

### 三、悬浮窗功能

如果您的业务需要开启悬浮窗功能，您可以在 TUICallKit 组件初始化时调用以下接口开启该功能：
```java
TUICallKit.createInstance(context).enableFloatWindow(true);
```

### 四、通话状态监听

如果您的业务需要 **监听通话的状态**，例如通话开始、结束，以及通话过程中的网络质量等等，可以监听以下事件：
```java
TUICallEngine.createInstance(context).addObserver(new TUICallObserver() {
    @Override
    public void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole) {
    }
    public void onCallEnd(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType,TUICallDefine.Role callRole, long totalTime) {
    }
    public void onUserNetworkQualityChanged(List<TUICommonDefine.NetworkQualityInfo> networkQualityList) {
    }
});
```

### 五、自定义铃音

如果您需要自定义来电铃音，可以通过如下接口进行设置：

```java
TUICallKit.createInstance(context).setCallingBell(filePath);
```

## 常见问题

### 1、错误提示“The package you purchased does not support this ability”？

如遇以上错误提示，是由于您当前应用的音视频通话能力包过期或未开通，请参见 [步骤一：开通服务](#step1)，领取或者开通音视频通话能力，进而继续使用 TUICallKit 组件。

### 2、如何购买套餐？

请参考购买链接 [音视频通话 SDK 价格总览](https://www.tencentcloud.com/document/product/647/50553)，如有其他问题，请点击页面右侧，进行售前套餐咨询，或者加入 QQ 群：**592465424**，进行咨询和反馈。

### 3、TUICallKit 崩溃，崩溃日志："No implementation found for xxxx"？

堆栈信息如下：

```java
java.lang.UnsatisfiedLinkError: No implementation found for void com.tencent.liteav.base.Log.nativeWriteLogToNative(int, java.lang.String, java.lang.String) (tried Java_com_tencent_liteav_base_Log_nativeWriteLogToNative and Java_com_tencent_liteav_base_Log_nativeWriteLogToNative__ILjava_lang_String_2Ljava_lang_String_2)
       at com.tencent.liteav.base.Log.nativeWriteLogToNative(Native Method)
       at com.tencent.liteav.base.Log.i(SourceFile:177)
       at com.tencent.liteav.basic.log.TXCLog.i(SourceFile:36)
       at com.tencent.liteav.trtccalling.model.impl.base.TRTCLogger.i(TRTCLogger.java:15)
       at com.tencent.liteav.trtccalling.model.impl.ServiceInitializer.init(ServiceInitializer.java:36)
       at com.tencent.liteav.trtccalling.model.impl.ServiceInitializer.onCreate(ServiceInitializer.java:101)
       at android.content.ContentProvider.attachInfo(ContentProvider.java:2097)
       at android.content.ContentProvider.attachInfo(ContentProvider.java:2070)
       at android.app.ActivityThread.installProvider(ActivityThread.java:8168)
       at android.app.ActivityThread.installContentProviders(ActivityThread.java:7709)
       at android.app.ActivityThread.handleBindApplication(ActivityThread.java:7573)
       at android.app.ActivityThread.access$2600(ActivityThread.java:260)
       at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2435)
       at android.os.Handler.dispatchMessage(Handler.java:110)
       at android.os.Looper.loop(Looper.java:219)
       at android.app.ActivityThread.main(ActivityThread.java:8668)
       at java.lang.reflect.Method.invoke(Native Method)
       at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:513)
       at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:1109)
```

**TUICallkit不支持虚拟机，请用真机进行体验**；如在真机上遇到上述异常，是因为 TUICallKit 依赖的 TRTC 等 SDK 部分接口使用了 JNI 实现，Android Studio 在某些条件进行编译 APK 的时候可能并不会把 Native 的 .so 库打包进去，导致出现这类报错，重新 Clean 一下即可。

>? 更多帮助信息，详情请参见 [Android 常见问题](https://www.tencentcloud.com/document/product/647/51022)。

## 交流与反馈

如果有任何需要或者反馈，您可以联系：colleenyu@tencent.com。