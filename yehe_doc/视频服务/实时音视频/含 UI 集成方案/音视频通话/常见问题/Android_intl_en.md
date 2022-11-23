### Can I not integrate the IM SDK if I use only TRTC features?

**No, you can’t.** All components of `TUIKit` rely on the IM SDK for underlying logic such as outgoing call signaling and busy line signaling. If you have already purchased IM’s services, you can use them according to `TUICallKit` logic.

### What should I do if I receive the error message "The package you purchased does not support this ability"?

If the above error occurs, it indicates that you haven’t activated TRTC or your TRTC package has expired. For directions on how to activate TRTC, see [Step 1. Activate services](https://www.tencentcloud.com/document/product/647/50991#step1). You can get a free trial package after activation.

### `TUICallKit` crashed, and the error message was "No implementation found for xxxx". What should I do?

Below is the stack trace:

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

>! **`TUICallkit` does not support emulators. Please test it on an a real device.** If the above error occurs on a real device, it is because some APIs the `TUICallKit` component relies on are based on JNI, and in some cases, Android Studio may not package native SO libraries when building the APK. In this case, just clean your project.

### What should I do if an `allowBackup` error occurs?

**Error message**: `Manifest merger failed : Attribute application@allowBackup value=(true) from AndroidManifest.xml`

**Cause**: In the IM SDK, the default value of `allowBackup` is `false`, which means backup and recovery are disabled for the application.

**Solution**: Delete the `allowBackup` property from the `AndroidManifest.xml` file or change its value to `false`. Alternatively, add `tools:replace="android:allowBackup"` to `application` in the `AndroidManifest.xml` file to replace the IM SDK configuration with your own configuration.

### Does `TUICallKit` support offline call push?

**Yes, it does.** For Android, we use the `TUIOfflinePush` component to implement offline call push. For detailed directions, see [Android](https://www.tencentcloud.com/document/product/1047/39156). This component is also built into [TUICallKit](https://github.com/tencentyun/TUICalling/tree/main/Android).

### If a call is within the timeout period, and an offline invitee goes online, will `TUICallKit` display the incoming call view?

There are several cases depending on what status the application is in when the invitee goes online:

![img](https://qcloudimg.tencent-cloud.cn/raw/1b82ef1bcc5dbc5b0a2d7bf6e4c9d772.jpg)

If the incoming call view is not displayed after an invitee goes back online, search for `onReceiveNewInvitation` in your logs and check if historical messages are obtained. If you cannot find the log data, please [contact us](https://intl.cloud.tencent.com/contact-us) for help.

### Why can’t my application be automatically switched to the foreground to display the incoming call view?

**Check whether your application is granted the autostart-from-background or floating window permission.**

Note that different vendors or even different Android versions require different permissions to implement this. The naming of the permissions may also vary. For example, for Mi 6, only the pop-up-from-background permission is needed, while for Redmi, both the pop-up-from-background and floating window permissions are required.

>? If you have manually granted all the necessary permissions and still cannot move your application to the foreground, it may be a vendor compatibility issue.
