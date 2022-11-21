### TUICallKit 是否可以不引入 IM SDK，只使用 TRTC？

**不可以**，TUIKit 全系组件都使用了腾讯云 IM SDK 做为通信的基础服务，比如通话拨打信令、通话忙线信令等核心逻辑，如果您已经购买有其他 IM 产品，也可以参照 TUICallKit 逻辑进行适配。

### 错误提示“The package you purchased does not support this ability”？

如遇以上错误提示，是由于您当前应用的音视频通话能力包过期或未开通，请参见 [步骤一：开通服务](https://www.tencentcloud.com/document/product/647/50991#step1)，领取或者开通音视频通话能力，进而继续使用 TUICallKit 组件。

### 如何购买音视频通话套餐？

请参考购买链接 [音视频通话 SDK 价格总览](https://www.tencentcloud.com/document/product/647/50553)，如有其他问题，请点击页面右侧，进行售前套餐咨询；或者加入 QQ 群：**592465424**，进行咨询和反馈。

### TUICallKit 崩溃，崩溃日志："No implementation found for xxxx"？

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

>! **TUICallkit 不支持虚拟机，请用真机进行体验**；如在真机上遇到上述异常，是因为 TUICallKit 依赖的 TRTC 等 SDK 部分接口使用了 JNI 实现，Android Studio 在某些条件进行编译 APK 的时候可能并不会把 Native 的 .so 库打包进去，导致出现这类报错，重新 Clean 一下即可。

### allowBackup 异常？

**报错信息**：`Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml`

**问题原因**：TUICallKit 依赖的 IM SDK 中默认 allowBackup 的值为 false ，表示关闭应用的备份和恢复功能。

**解决方法**：您可以在您工程的 `AndroidManifest.xml` 文件中删除 allowBackup 属性或将该属性改为 false，表示关闭备份和恢复功能；也可以在 `AndroidManifest.xml` 文件的 application 节点中添加 `tools:replace="android:allowBackup";` 表示覆盖 IM SDK 的设置，使用您自己的设置。

### TUICallKit 是否支持离线推送呢？

**支持**，Android 离线推送采用腾讯云的 TUIOfflinePush 组件，详情请参见 [TUIOfflinePush](https://www.tencentcloud.com/document/product/1047/39156)，在 [TUICallKit](https://github.com/tencentyun/TUICalling/tree/main/Android) 组件中，我们也接入了该组件。

### 在通话邀请超时时间内，被邀请者如果离线再上线，能否弹出通话界面？

根据 App 的启动类型，分别有不同的情况：

![img](https://qcloudimg.tencent-cloud.cn/image/document/f4b8ab415785fb5274e2f6cc709254fc.png)

如果离线再上线后没有弹出通话界面，请过滤`onReceiveNewInvitation`日志，检查是否拉取到历史消息，如果没有该日志的打印，请[联系我们](https://intl.cloud.tencent.com/contact-us)协助处理。

### 应用在后台时，不能自动将通话界面拉取到前台

**将应用从后台自动拉取到前台，需要检查 App 是否开启了”后台自启动“或”悬浮窗“权限。**

值得注意的是，不同厂商、甚至同一厂商不同 Android 版本，其对于应用开放的权限以及权限名称也会存在不一致。例如，小米6只需要开启后台弹出界面权限，而红米需要同时打开后台弹出界面和显示悬浮窗权限。

>? 如果您在测试中手动开启了所有权限，依然无法自动拉起通话界面到前台，可能需要做厂商兼容。