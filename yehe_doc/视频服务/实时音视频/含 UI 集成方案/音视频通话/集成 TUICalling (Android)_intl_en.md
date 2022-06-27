## Overview

`TUICalling` is an open-source UI component for audio/video communication. With just a few lines of code changes, you can integrate it into your project to implement one-to-one audio/video calls that support offline push notifications. In addition to the Android component, we also offer components for iOS, web, Flutter, UniApp, and more.

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/af697557d2746585a0d9f4b894dc42d5.png" </td>
</tr>
</tbody></table>


## Integration

### Step 1. Import the `TUICalling` component
Go to the component’s [GitHub page](https://github.com/tencentyun/TUICalling), clone or download the code, and copy the `tuicalling` and `debug` folders in the `Android` directory to the same directory as `app` in your project. Then, do the following to import the component:
- Add the code below in `setting.gradle`:
```java
include ':tuicalling'
include ':debug'
```
- Add the `tuicalling` dependency in `build.gradle` in the `app` directory:
```java
api project(':tuicalling')
```
- Add the `TRTC SDK` and `IM SDK` dependencies in `build.gradle` in the root directory:
```java
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### Step 2. Configure permission requests and obfuscation rules

1. Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and later, the camera, mic, and read storage permissions must be requested at runtime).
```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // Use cases: This permission is required to implement floating windows and display the call page when your app is in the background.
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // Use case: This permission is required when a Bluetooth headset is used.
<uses-permission android:name="android.permission.READ_PHONE_STATE" />          // Use case: This permission is required to determine whether the current call is interrupted by an incoming phone call.
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```
-keep class com.tencent.** { *;}
```

### Step 3. Create and initialize an instance of the component

```java
// 1. Add a listener and log in
TUILogin.addLoginListener(new TUILoginListener() {
    @Override
    public void onConnecting() {      // Connecting …
        super.onConnecting();
    }
    @Override
    public void onConnectSuccess() {  // Connected
        super.onConnectSuccess();
    }
    @Override
    public void onConnectFailed(int errorCode, String errorMsg) {  // Failed to connect
        super.onConnectFailed(errorCode, errorMsg);
    }
    @Override
    public void onKickedOffline() {  // Callback for forced logout (for example, due to login from another device)
        super.onKickedOffline();
    }
    @Override
    public void onUserSigExpired() { // Callback for `userSig` expiration
        super.onUserSigExpired();
    }
});
TUILogin.login(mContext, "Your SDKAppID", "Your userId", "Your userSig", new TUICallback() {
    @Override
    public void onSuccess() {
    }
    @Override
    public void onError(int errorCode, String errorMsg) {
        Log.d(TAG, "errorCode: " + errorCode + " errorMsg:" + errorMsg);
    }

// 2. Initialize the `TUICalling` instance
TUICalling callingImpl = TUICallingImpl.sharedInstance(context);
```
**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated TRTC, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, click **Application Info**, and select the **Quick Start** tab to view its `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **SecretKey**: **TRTC application key**. Each secret key corresponds to an `SDKAppID`. You can view your application’s secret key on the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- **userId**: Current user ID, which is a custom string that can contain up to 32 bytes of letters and digits (special characters are not supported).
- **UserSig**: Security signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to quickly generate a `UserSig` for testing or calculate it on your own by referring to our [TUICalling demo project](https://github.com/tencentyun/TUICalling/blob/main/Android/app/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


### Step 4. Make an audio/video call
**Make a one-to-one audio/video call using [TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43140)**:
```java
// Make a one-to-one video call. Suppose the `userId` is `1111`
callingImpl.call(["1111"], TUICalling.Type.VIDEO);
```


>? 
>- After the callee completes step 3, (that is, after successful login), the `TUICalling` component will display the call answering UI when the callee receives a call invitation.    
>- If you want to make an audio call, set the type to `TUICalling.Type.AUDIO`.

### Step 5. Implement offline push notifications (optional)

You can make audio/video calls after completing the above four steps. However, if you want your users to be able to receive call invitations even when your app is in the background or after it is killed, then you need to also implement the offline push notification feature. For details, see [Implementing Offline Push Notifications in TUICalling for Android](https://github.com/tencentyun/TUICalling/blob/main/Android/Android%E7%A6%BB%E7%BA%BF%E6%8E%A8%E9%80%81%E6%8E%A5%E5%85%A5%E6%8C%87%E5%BC%95.md).

### Step 6. Listen for call status (optional)
If you want to be notified of [call status](https://intl.cloud.tencent.com/document/product/647/43140) (for example, the start and end of a call), register the following listeners:
```
callingImpl.setCallingListener(new TUICalling.TUICallingListener() {
    @Override
    public boolean shouldShowOnCallView() {
        return true;
    }

    @Override
    public void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView) {

    }

    @Override
    public void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime) {

    }

    @Override
    public void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message) {
        Log.d(TAG, "onCallEvent: event = " + event + " ,message = " + message);
    }
});
```

### Step 7. Add the floating window feature (optional)
To implement the floating window feature in your app, call `callingImpl.enableFloatWindow(true)` when initializing the `TUICalling` component.

Currently, the component supports the following two floating window types:
- For system-wide floating windows (after your app is switched to the background when users press the Home button), you need to grant the app floating window permission.
- For in-app floating windows (after users tap the Back button to return to a previous page), you need to grant the app floating window permission and set the UI view to return to.
How to grant the floating window permission: Select **Settings** > **App Management**, find your app, click **Permissions**, and click **Floating Window** > **Allow** (the setting path may vary by phone brand and platform).

To set the UI view to return to, configure `com.tencent.trtc.tuicalling` for the target page in `AndroidManifest.xml`:
```
<activity
    android:name="{packageName}.MainActivity"
    android:launchMode="singleTop">
    <intent-filter>
        <action android:name="com.tencent.trtc.tuicalling" /> 
        <category android:name="android.intent.category.DEFAULT" />
    </intent-filter>
</activity>
```

## FAQs

### Does the `TUICalling` component support customizing profile photos and usernames?

Yes. You can implement this by calling `setUserNickname/setUserAvatar`.

### Does the `TUICalling` component support customizing ringtones?
Yes. You can implement this by calling [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140).

>? If you have any requirements or feedback, contact colleenyu@tencent.com.
