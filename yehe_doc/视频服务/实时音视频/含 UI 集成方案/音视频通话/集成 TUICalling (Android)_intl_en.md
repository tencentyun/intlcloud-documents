## Component Overview

`TUICalling` is an open-source audio/video UI component. After integrating it into your project, you can make your application support scenarios such as one-to-one and group audio/video calls and offline call simply by writing a few lines of code. It also supports iOS, web, Flutter, and UniApp platforms. Its basic features are as shown below:

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/94bbec9961b0d569cc7068389dc41412.jpg" width="400"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/534089ed0be5c78fb63c65cde79ad866.jpg" width="400"></td>
</tr>
</tbody></table>



## Component Integration

### Step 1. Download and import the `TUICalling` component
Go to [GitHub](https://github.com/tencentyun/TUICalling), clone or download the code, copy the `tuicalling`, `tuicore`, and `debug` directories in the `Android` directory to your project at the same level as `app`, and complete the following import operations:
- Complete import in `setting.gradle` as shown below:
```java
include ':tuicalling'
include ':tuicore'
include ':debug'
```
- Add dependencies on `tuicalling` to the `build.gradle` file in `app`:
```java
api project(':tuicalling')
```
- Add dependencies on `TRTC SDK` and `IM SDK` to the `build.gradle` file in the root directory:
```java
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### Step 2. Configure permission requests and obfuscation rules

1. Configure permission requests for your application in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera, mic, and storage read permissions must be requested at runtime.)
```java
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // Use case: Floating window. This permission is required for the application in the background to display the call page
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // Use case: This permission is required when a Bluetooth headset is used
<uses-permission android:name="android.permission.READ_PHONE_STATE" />          // Use case: This permission is required to determine whether the current call is interrupted by an incoming phone call
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```
-keep class com.tencent.** { *;}
```

### Step 3. Create and initialize the component

```java
// 1. Log in to the component
TUILogin.init(this, "Your SDKAppID", config, new V2TIMSDKListener() {
    @Override
    public void onKickedOffline() {  // Callback for forced logout (for example, the account is logged in to on another device)

    }
    @Override
    public void onUserSigExpired() { // Callback for `userSig` expiration

    }
});

TUILogin.login("Your userId", "Your userSig", new V2TIMCallback() {
    @Override
    public void onError(int code, String msg) {
        Log.d(TAG, "code: " + code + " msg:" + msg);
    }
    @Override
    public void onSuccess() {

    }
});

// 2. Initialize the `TUICalling` instance
TUICalling callingImpl = TUICallingImpl.sharedInstance(context);
```
**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**, which corresponds to `SDKAppID`. On the [Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **userId**: Current user ID, which is a string and can contain up to 32 bytes of letters and digits (special symbols are not supported). You can customize it based on your actual account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online or calculate it on your own by referring to the [TUICalling demo project](https://github.com/tencentyun/TUICalling/blob/main/Android/app/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


### Step 4. Make an audio/video call
- **Make a one-to-one audio/video call through [TUICalling#call](https://intl.cloud.tencent.com/document/product/647/43140)**
```java
// Make a one-to-one video call. Suppose the `userId` is `1111`
callingImpl.call(["1111"], TUICalling.Type.VIDEO);
```
- **Make a group video call**:
```java
// Make a group video call. Suppose the `userId` values are `1111`, `2222`, and `3333`
callingImpl.call(["1111", "2222", "3333"], TUICalling.Type.VIDEO);
```

>? 
>- After the callee completes step 3, (i.e., after successful login) when receiving a call request again, the `TUICalling` component will automatically display the corresponding call answering UI.    
>- If you want to make an audio call, simply change the type to `TUICalling.Type.AUDIO`.

### Step 5. Add the offline push feature (optional)

After the above four steps are completed, audio/video calls can be made and answered. However, if your business scenarios require that audio/video call requests can be normally received even **after the application process is killed** or **runs in the background**, you need to add the offline push feature to the `TUICalling` component. For more information, see [**TUICalling for Android Offline Push Connection Guide.md**](https://github.com/tencentyun/TUICalling/blob/main/Android/Android%E7%A6%BB%E7%BA%BF%E6%8E%A8%E9%80%81%E6%8E%A5%E5%85%A5%E6%8C%87%E5%BC%95.md).

### Step 6. Add the status listening feature (optional)
If your business needs to [listen on the call status](https://intl.cloud.tencent.com/document/product/647/43140) such as call start and end, listen on the following events:
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
If your business needs to enable the floating window feature, you can call `callingImpl.enableFloatWindow(true)` during `TUICalling` component initialization.

Currently, the component supports the following two floating window types:
- System floating window (click **Home** to switch to the background): You need to grant the application the floating window permission.
- In-app floating window (minimize and return to the previous UI): You need to grant the application the floating window permission and set the previous UI to be returned to.
How to grant the floating window permission: Select **Settings** > **App Management**, find your app, click **Permissions**, and click **Floating Window** > **Allow** (the setting path may vary by phone brand and platform).

Set the previous UI to be returned to: Configure the redirect action `com.tencent.trtc.tuicalling` for the target page in `AndroidManifest.xml` as follows:
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

### Does the `TUICalling` component support customizing profile photos and nicknames?

Yes. You can implement this by calling `setUserNickname/setUserAvatar`.

### Does the `TUICalling` component support customizing ringtones?
Yes. You can implement this by calling [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140).

>? If you have any requirements or feedback, contact colleenyu@tencent.com.
