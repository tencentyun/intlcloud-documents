## Component Overview
`TUIRoom` is an open-source audio/video UI component. After integrating it into your project, you can add features such as screen sharing, beauty filter, and low-latency video call to your application simply by writing a few lines of code. It also supports the [iOS](https://intl.cloud.tencent.com/document/product/647/37284), [Windows](https://intl.cloud.tencent.com/document/product/647/44071), and [macOS](https://intl.cloud.tencent.com/document/product/647/44071) platforms. Its basic features are as shown below:

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/0f07b6d570174f6fdc999eb67864f1f3.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/9bdc61aa798c2c3926949d00a97302dc.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/37ef82ac97172967c037a523c5d09af3.png" width="250"></td>
</tr>
</tbody></table>


## Component Integration
### Step 1. Download and import the `TUIRoom` component
Go to [GitHub](https://github.com/tencentyun/TUIRoom), clone or download the code, copy the `Source` and `TUICore`, and `Beauty` directories from the `Android` directory to your project, and complete the following import operations:
- Complete import in `setting.gradle` as shown below:
```
include ':Source'
include ':TUICore'
include ':Beauty'
```
- Add dependencies on `Source`, `TUICore`, and `Beauty` to the `build.gradle` file in `app`:
```
api project(':Source')
```
- Add dependencies on `TRTC SDK` and `IM SDK` to the `build.gradle` file in the root directory:
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### Step 2. Configure permission requests and obfuscation rules
1. Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and later, the mic access must be requested at runtime):
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

### Step 3. Create and initialize the TUI component
```java
  // 1. Log in to the component
  TUILogin.init(this, your SDKAppId, config, new V2TIMSDKListener() {
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
  
  // 2. Initialize the `TUIRoomCore` instance
  TUIRoomCore mTUIRoomCore = TUIRoomCore.getInstance(context);
  mTUIRoomCore.setListener(listener);

```

#### Parameter description
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**, which corresponds to `SDKAppID`. On the *[Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online, or you can calculate it on your own by referring to the [demo project](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


### Step 4. Implement group audio/video interaction
1. **The room owner creates a group audio/video interaction room through [TUIRoomCore#createRoom](https://intl.cloud.tencent.com/document/product/647/37281)**.
```java
// 1. The room owner calls an API to create a room
int roomId = 12345; // Room ID
mTUIRoomCore.createRoom(roomId, TUIRoomCoreDef.SpeechMode.FREE_SPEECH,
        new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // Room created successfully
            }
        }
    }
});
```

2. **Other users enter the audio/video room through [TUIRoomCore#enterRoom](https://intl.cloud.tencent.com/document/product/647/37281)**.
```java
// 1. Another user calls an API to enter the room
mTUIRoomCore.enterRoom(roomId, new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // Room entered successfully
            }
        }
    }
});

// 2. The callback of whether a remote user is sending audio is received. At this time, the room user list can be refreshed
@Override
public void onRemoteUserEnterSpeechState(final String userId) {
}
```

3. **The room owner dismisses the room through [TUIRoomCore#destroyRoom](https://intl.cloud.tencent.com/document/product/647/37281)**.
```java
// 1. The room owner calls an API to dismiss the room
mTUIRoomCore.destroyRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

Room members receive the `onDestroyRoom` callback message that notifies them of room dismissal.
@Override
public void onDestroyRoom() {
    // The room owner dismisses and exits the room
}
```

4. **Other members exit the room through [TUIRoomCore#leaveRoom](https://intl.cloud.tencent.com/document/product/647/37281)**.
```java
// 1. A room member calls an API to exit the room
mTUIRoomCore.leaveRoom(new TUIRoomCoreCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
                    
    }
});

Room members receive the `onRemoteUserLeave` callback message that notifies them of member exit.
@Override
public void onRemoteUserLeave(String userId) {
        Log.d(TAG, "onRemoteUserLeave userId: " + userId);
}
```

5. **Implement screen sharing through [TUIRoomCore#startScreenCapture](https://intl.cloud.tencent.com/document/product/647/37281)**.
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

// 4. Enable screen sharing
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
