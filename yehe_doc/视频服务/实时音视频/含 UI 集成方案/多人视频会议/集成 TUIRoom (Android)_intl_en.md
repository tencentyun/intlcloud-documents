## Overview
`TUIRoom` is an open-source UI component for audio/video communication. With just a few lines of code changes, you can integrate it into your project to implement screen sharing, beauty filters, low-latency video calls, and other features. In addition to the Android component, we also offer components for [iOS](https://intl.cloud.tencent.com/document/product/647/37284), [Windows](https://intl.cloud.tencent.com/document/product/647/44071), [macOS](https://intl.cloud.tencent.com/document/product/647/44071), and more.

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/2944bac3c5d348b06d2a11c439783b48.png"></td>
</tr>
</tbody></table>

## Integration
### Step 1. Download and import the `TUIRoom` component
Go to the component's [GitHub page](https://github.com/tencentyun/TUIRoom), clone or download the code, and copy the `tuiroom` and `debug`, and `tuibeauty` folders in the `Android` directory to your project. Then, do the following to import the component:
1. Add the code below in `setting.gradle`:

```
include ':tuiroom'
include ':debug'
include ':tuibeauty'
```
2. Add dependencies on `tuiroom`, `debug`, and `tuibeauty` to the `build.gradle` file in `app`:

```
api project(':tuiroom')
api project(':debug')
api project(':tuibeauty')
```
3. Add the `TRTC SDK` and `IM SDK` dependencies in `build.gradle` in the root directory:
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### Step 2. Configure permission requests and obfuscation rules
1. Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and later, the mic permission must be requested at runtime.)
```
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
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
// 1. Log in to the component
TUILogin.addLoginListener(new TUILoginListener() {
    @Override
    public void onKickedOffline() {  // Callback for forced logout (for example, due to login from another device)
    }

    @Override
    public void onUserSigExpired() { // Callback for `userSig` expiration
    }
});

TUILogin.login(context, "Your SDKAppId", "Your userId", "Your userSig", null);


// 2. Initialize the `TUIRoom` instance
TUIRoom tuiRoom = TUIRoom.sharedInstance(this);
```

#### Parameter description
- **SDKAppID**: **TRTC application ID**. If you haven't activated TRTC, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, click **Application Info**, and select the **Quick Start** tab to view its `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**. Each secret key corresponds to a `SDKAppID`. You can view your application’s secret key on the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **UserSig**: Security signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to quickly generate a `UserSig` for testing. For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


### Step 4. Implement group audio/video communication
1. **Create a room**
```java
tuiRoom.createRoom(12345, TUIRoomCoreDef.SpeechMode.FREE_SPEECH, true, true);
```
2. **Join a room**
```java
tuiRoom.enterRoom(12345, true, true);
```

### Step 5. Implement room management (optional)
1. **The room owner calls [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37281) to close the room**.
```java
// 1. The room owner calls the API below to close the room.
mTUIRoomCore.destroyRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

Other users in the room will receive the `onDestroyRoom` callback.
@Override
public void onDestroyRoom() {
    // The room owner closes and exits the room.
}
```
2. **A user in the room calls [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37281) to leave the room**.
```java
// 1. A user (not the room owner) calls the API below to leave the room.
mTUIRoomCore.leaveRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

Other users in the room will receive the `onRemoteUserLeave` callback.
@Override
public void onRemoteUserLeave(String userId) {
        Log.d(TAG, "onRemoteUserLeave userId: " + userId);
}
```

### Step 6. Implement screen sharing (optional)
Call [TUIRoomCore#startScreenCapture](https://www.tencentcloud.com/document/product/647/45483) to implement screen sharing.
```java
// 1. Add the SDK’s screen sharing activity and permission in `AndroidManifest.xml`
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>

// 2. Request the floating window permission in your UI
if (Build.VERSION.SDK_INT >= 23) {
    if (!Settings.canDrawOverlays(getApplicationContext())) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, 100);
    } else {
        startScreenCapture();
    }
} else {
    startScreenCapture();
}

// 3. System callback result
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == 100) {
        if (Build.VERSION.SDK_INT >= 23) {
            if (Settings.canDrawOverlays(this)) {
                // The user grants the permission.
                startScreenCapture();
            } else {
            }
        }
    }
}

// 4. Start screen sharing
private void startScreenCapture() {
        TRTCCloudDef.TRTCVideoEncParam encParams = new TRTCCloudDef.TRTCVideoEncParam();
        encParams.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720;
        encParams.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
        encParams.videoFps = 10;
        encParams.enableAdjustRes = false;
        encParams.videoBitrate = 1200;

        TRTCCloudDef.TRTCScreenShareParams params = new TRTCCloudDef.TRTCScreenShareParams();
        mTUIRoom.stopCameraPreview();
        mTUIRoom.startScreenCapture(encParams, params);
}
```

## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
