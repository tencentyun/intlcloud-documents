## Overview

`TUILiveRoom` is an open-source video live streaming scenario UI component. After integrating it into your project, you can enable your application to support interactive video live streaming simply by writing a few lines of code. It provides source code for Android, iOS, and mini program platforms. Its basic features are as shown below:

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<table>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a1b4b04662bb342de1e7b713cb3f59ce.png"></td>
</tr>
</table>

[](id:model)
## Integration
[](id:model.step1)
### Step 1. Download and import the `TUILiveRoom` component
Go to [GitHub](https://github.com/tencentyun/TUILiveRoom), clone or download the code, copy the `Android/debug`, `Android/tuiaudioeffect`, `Android/tuibarrage`, `Android/tuibeauty`, `Android/tuigift`, and `Android/tuiliveroom` directories to your project, and complete the following import operations:

- Add the code below in `setting.gradle`:
```
include ':debug'
include ':tuibeauty'
include ':tuibarrage'
include ':tuiaudioeffect'
include ':tuigift'
include ':tuiliveroom'
```
- Add dependencies on `tuiliveroom` to the `build.gradle` file in `app`:
```
api project(":tuiliveroom")
```
- Add the `TRTC SDK` and `IM SDK` dependencies in `build.gradle` in the root directory:
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules
1. Configure permission requests for your application in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and later, the camera and storage read permissions must be requested at runtime.)
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```
2. In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```java
-keep class com.tencent.** { *;}
```

[](id:model.step3)
### Step 3. Initialize and log in to the component
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
});

// 2. Initialize the `TUILiveRoom` component
TUILiveRoom mLiveRoom = TUILiveRoom.sharedInstance(mContext);
```

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated TRTC, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, click **Application Info**, and select the **Quick Start** tab to view its `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**. Each secret key corresponds to a `SDKAppID`. You can view your application’s secret key on the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **UserSig**: Security signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to quickly generate a `UserSig` for testing or calculate it on your own by referring to our [demo project](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).


[](id:model.step4)
### Step 4. Implement an interactive video live room
1. **The anchor starts streaming**.
```java
mLiveRoom.createRoom(int roomId, String roomName, String coverUrl);
```
2. **The audience member watches**.
```java
mLiveRoom.enterRoom(roomId);
```
3. **Audience member and the anchor co-anchor together through [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37333)**.
```java
// 1. The audience member sends a co-anchoring request
// `LINK_MIC_TIMEOUT` is the timeout period
TRTCLiveRoom mTRTCLiveRoom=TRTCLiveRoom.sharedInstance(mContext);
mTRTCLiveRoom.requestJoinAnchor(mSelfUserId + "requested to co-anchor", LINK_MIC_TIMEOUT
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // The request is accepted by the anchor
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // The audience member turns on the camera and starts pushing streams
            mTRTCLiveRoom.startCameraPreview(true, view, null);
            mTRTCLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2. The anchor receives the co-anchoring request
mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // The anchor accepts the co-anchoring request
        mTRTCLiveRoom.responseJoinAnchor(userInfo.userId, true, "agreed to co-anchor");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // The anchor receives a notification that the co-anchoring audience member has turned on the mic
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // The anchor plays the audience member's video
        mTRTCLiveRoom.startPlay(userId, view, null);
    }
});
```
4. **Anchors from different rooms communicate with each other by calling [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37333#requestroompk)**.
```java
// Create room 12345
mLiveRoom.createRoom(12345, "roomA", "Your coverUrl");
// Create room 54321
mLiveRoom.createRoom(54321, "roomB", "Your coverUrl");

// Anchor A:
TRTCLiveRoom mTRTCLiveRoom=TRTCLiveRoom.sharedInstance(mContext);

// 1. Send a cross-room communication request to anchor B
mTRTCLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5. Receive a callback of whether the request is accepted by anchor B
        if (code == 0) {
            // Accepted
        } else {
            // Declined
        }
    }
});

mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6. Receive a notification about anchor B’s entry
        mTRTCLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// Anchor B:
// 2. Receive anchor A’s request
mTRTCLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3. Accept anchor A's request
        mTRTCLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4. Receive a notification about anchor A’s entry and play anchor A's video
        mTRTCLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
