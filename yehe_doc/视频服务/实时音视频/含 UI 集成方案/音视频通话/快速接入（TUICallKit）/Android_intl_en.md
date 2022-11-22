This document describes how to quickly integrate the `TUICallKit` component. Performing the following key steps generally takes about an hour, after which you can implement the video call feature with complete UIs.

## Environment Preparations

Android 4.1 (SDK API level 16) or later (Android 5.0 (SDK API level 21) or later is recommended).

Android Studio 3.5 or later (Gradle 3.5.4 or later).

Mobile phone on Android 4.1 or later.

[](id:step1)
## Step 1. Activate the service

`TUICallKit` is an audio/video call component developed based on two paid PaaS services: [IM](https://www.tencentcloud.com/document/product/1047) and [TRTC](https://www.tencentcloud.com/document/product/647). You can activate the services and enjoy a 60-day free trial as follows:

1. Log in to the [IM console](https://console.tencentcloud.com/im) and click **Create Application**. In the pop-up window, enter your application name and click **OK**.
![img](https://qcloudimg.tencent-cloud.cn/raw/571d5bed98a46752933169fbf4136271.png)

2. Click the application just created to enter the **Basic Configuration** page. In the Activate free trial of audio/video call feature pop-up window, click Activate Now to activate the 60-day free trial of TUICallKit.
![img](https://qcloudimg.tencent-cloud.cn/raw/0860fe4f282d2d918d3911127d85120a.png)

>! Different paid editions of the IM audio/video call capability are available for different business needs. You can learn more about the available features and purchase an the edition you want on the IM purchase page.

3. On the same page, find and record the **SDKAppID** and **Key**, which will be used in [step 4](#step4).
![img](https://qcloudimg.tencent-cloud.cn/raw/5c1b56dc1972d836c85579dd16b0634d.png)


>? **Note:** After you click **Free trial**, the following message will be displayed for some users who have used [TRTC](https://www.tencentcloud.com/document/product/647/35078) before:

```java
[-100013]:TRTC service is suspended. Please check if the package balance is 0 or the Tencent Cloud account is in arrears
```
This is because the new IM audio/video call capability is based on two basic PaaS services: [TRTC](https://www.tencentcloud.com/document/product/647/35078) and [IM](https://www.tencentcloud.com/document/product/1047). If you have used up your free monthly quota (10,000 minutes) for TRTC, you will fail to activate the capability. You can log in to the [TRTC console](https://console.tencentcloud.com/trtc/app), go to the **Application Management** page of the corresponding `SDKAppID`, and activate the pay-as-you-go feature. Then, next time when you **start the application**, you can experience the new audio/video call capability properly.

[](id:step2)
## Step 2. Download and import the component

Go to [GitHub](https://github.com/tencentyun/TUICalling), clone or download the code, and copy the `tuicallkit` subdirectory in the `Android` directory to the directory at the same level as `app` in your current project, as shown below:

![img](https://qcloudimg.tencent-cloud.cn/raw/4b6a74f2ee2f5d8eab00061b9fc1f112.png)

[](id:step3)
## Step 3. Configure the project
1. Find the `setting.gradle` file in the project root directory and add the following code to import the `TUICallKit` component downloaded in [step 2](#step2) to your current project:

```java
include ':tuicallkit'
```

2. Find the `build.gradle` file in the `app` directory and add the following code to declare the dependencies of the current application on the `TUICallKit` component just added:
```java
api project(':tuicallkit')
```
>? The `TUICallKit` project depends on `TRTC SDK`, `IM SDK`, `tuicallengine`, and the `tuicore` public library internally by default with no need of additional configuration. To upgrade the version, modify the `tuicallkit/build.gradle` file.

3. As the SDK uses Java's reflection feature internally, you need to add certain classes in the SDK to the obfuscation allowlist by adding the following code to the `proguard-rules.pro` file:
```bash
-keep class com.tencent.** { *;}
```
>! `TUICallKit` helps you apply for camera, mic, and storage read/write permissions internally. If you need more or fewer permissions based on your actual business conditions, you can modify `tuicallkit/src/main/AndroidManifest.xml`.

[](id:step4)
## Step 4. Log in to the `TUICallKit` component

Add the following code to your project to call the relevant APIs in `TUICore` to log in to the `TUICallKit` component. This step is very important, as the user can use the component features properly only after a successful login. Carefully check whether the relevant parameters are correctly configured:
```java
// Set the listener for the login result
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

// Log in
TUILogin.login(context, 
    1400000001,     // Replace it with the `SDKAppID` obtained in step 1.
    "denny",        // Replace it with your `UserID`.
    "xxxxxxxxxxx",  // You can calculate a `UserSig` in the console and enter it here.
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

**Parameter description:** The key parameters used by the `login` function are as detailed below:

- **SDKAppID**: Obtained in the last step in step 1 and not detailed here.
- **UserID**: The ID of the current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), or underscores (_).
- **UserSig**: The authentication credential used by Tencent Cloud to verify whether the current user is allowed to use the TRTC service. You can get it by using the `SecretKey` obtained in the third step in [step 1](#step1) to encrypt the information such as `SDKAppID` and `UserID`. You can generate a temporary `UserSig` by using the [**auxiliary tool**](https://console.cloud.tencent.com/im/tool-usersig) in the console.

For more information, see [UserSig](https://www.tencentcloud.com/document/product/647/35166).

>- **Many developers have contacted us with questions regarding this step. Below are some of the frequently encountered problems:**
- `SDKAppID` is invalid. It is generally a 10-digit integer starting with `140`.
- `userSig` is set to the value of `Secretkey` mistakenly. The `userSig` is generated by using the `SecretKey` for the purpose of encrypting information such as `sdkAppId`, `userId`, and the expiration time. But the value of the `userSig` that is required cannot be directly substituted with the value of the `SecretKey`.
- `userId` is set to a simple string such as `1`, `123`, or `111`, and your colleague may be using the same `userId` while working on a project simultaneously. In this case, login will fail as **TRTC doesn't support login on multiple terminals with the same `UserID`**. Therefore, we recommend you use some distinguishable `userId` values during debugging.

>! The sample code on GitHub uses the `genTestUserSig` function to calculate `UserSig` locally, so as to help you complete the current integration process more quickly. However, this scheme exposes your `SecretKey` in the application code, which makes it difficult for you to upgrade and protect your `SecretKey` subsequently. Therefore, we strongly recommend you run the `UserSig` calculation logic on the server and make the application request the `UserSig` calculated in real time every time the application uses the `TUICallKit` component from the server.

[](id:step5)
## Step 5. Make a call

### One-to-one video call

You can call the `call` function of `TUICallKit` and specify the call type and the callee's `userId` to make an audio/video call.
```java
// Make a one-to-one video call. Suppose the `UserID` is `mike`.
TUICallKit.createInstance(context).call("mike", TUICallDefine.MediaType.Video); 
```

| Parameter | Type | Description |
| ------------- | ----------------------- | ----------------------------------------------------- |
| userId        | String                  | The ID of the target user, such as `"mike"`.                           |
| callMediaType | TUICallDefine.MediaType | The call media type, such as `TUICallDefine.MediaType.Video`. |

### Group video call

You can call the `groupCall` function of `TUICallKit` and specify the call type and the list of callees' `UserID` values to make a group audio/video call.
```java
TUICallKit.createInstance(context).groupCall("12345678", Arrays.asList("jane", "mike", "tommy"),TUICallDefine.MediaType.Video);
```

| Parameter | Type | Description |
| ------------- | ----------------------- | --------------------------------------------------------- |
| groupId       | String                  | The group ID, such as `"12345678"`.                               |
| userIdList    | List                    | The list of `UserID` values of the target users, such as `{"jane", "mike", "tommy"}`. |
| callMediaType | TUICallDefine.MediaType | The call media type, such as `TUICallDefine.MediaType.Video`.     |

>? You can create a group as instructed in [Android, iOS, and macOS](https://www.tencentcloud.com/document/product/1047/48466). You can also use [IM TUIKit](https://intl.cloud.tencent.com/document/product/1047/34286) to integrate chat and call scenarios at one stop.

`TUICallKit` currently doesn't support making a multi-person video call among users not in a group. If you have such a need, contact colleenyu@tencent.com.

[](id:step6)
## Step 6. Answer a call

After receiving an incoming call, the `TUICallKit` component will automatically wake up the call answering UI. However, the wake effect varies by Android system permissions as follows:

- If your application is in the foreground, it will pop up the call UI and play back the incoming call ringtone automatically when receiving an incoming call.
- If your application is in the background and is granted the `Display over other apps` or `Display pop-up windows while running in the background` permission, it will still pop up the call UI and play back the incoming call ringtone automatically when receiving an incoming call.
- If your application is in the background but isn't granted with the `Display over other apps` or `Display pop-up windows while running in the background` permission, `TUICallKit` will play back the incoming call ringtone to prompt the user to answer or decline the call.
- If the application process has been terminated, you can use the offline push feature as described in [Offline Call Push (Android)](https://www.tencentcloud.com/document/product/647/50991) to prompt the user to answer or decline the call through the status bar notification.

[](id:step7)
## Step 7. Implement more features

### 1. Nickname and profile photo settings

To customize the nickname or profile photo, use the following API for update:
```java
TUICallKit.createInstance(context).setSelfInfo("jack", "https:/****/user_avatar.png", callback);
```

>! The update of the callee's nickname and profile photo may be delayed during a call between non-friend users due to the user privacy settings. After a call is made successfully, the information will also be updated properly in subsequent calls.

### 2. Offline call push

You can make/answer audio or video calls after completing the above steps. However, if you want your users to be able to receive call invitations even when your application is in the background or after it is closed, then you need to also implement the offline call push feature. For more information, see [Offline Call Push (Android)](https://www.tencentcloud.com/document/product/647/50991).

### 3. Floating window

To implement the floating window feature in your application, call the following API when initializing the `TUICallKit` component:
```java
TUICallKit.createInstance(context).enableFloatWindow(true);
```

### 4. Call status listening

To **listen on the call status** (for example, the start or end of a call or the call quality during a call), listen on the following events:
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

### 5. Custom ringtone

You can use the following API to customize the ringtone:

```java
TUICallKit.createInstance(context).setCallingBell(filePath);
```

## FAQs

### 1. What should I do if I receive the error message "The package you purchased does not support this ability"?

The error message indicates that your application's audio/video call capability package has expired or is not activated. You can claim or activate the audio/video call capability as instructed in [step 1](#step1) to continue using `TUICallKit`.

### 2. How do I purchase a plan?

For more information, see [Billing Overview](https://www.tencentcloud.com/document/product/647/50553). If you have any questions, please contact us.

### 3. What should I do if `TUICallKit` crashes and outputs the log "No implementation found for xxxx"?

Below is the stack information:

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

**`TUICallkit` is not supported on VMs and must be run on a real device.** If the above exception occurs on a real device, it is because some APIs of SDKs such as the TRTC SDK depended on by `TUICallKit` are implemented through JNI, but Android Studio may not package native .so libraries when compiling the APK under some conditions. In this case, just clean the project again.

>? For more information, see [FAQs (Android)](https://www.tencentcloud.com/document/product/647/51022).

## Exchange and Feedback

If you have any requirements or feedback, contact colleenyu@tencent.com.
