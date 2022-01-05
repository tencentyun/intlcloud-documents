## Use Cases
TRTC supports four room entry modes. Video call (`VideoCall`) and audio call (`VoiceCall`) are the [call modes](https://intl.cloud.tencent.com/document/product/647/35103), and interactive video streaming (`Live`) and interactive audio streaming (`VoiceChatRoom`) are the live streaming modes.
The live streaming modes allow a maximum of 100,000 concurrent users in each room with smooth mic on/off. Co-anchoring latency is kept below 300 ms and watch latency below 1,000 ms. The live streaming modes are suitable for use cases such as low-latency interactive live streaming, interactive classrooms for up to 100,000 participants, video dating, online education, remote training, and mega-scale conferencing.

## How It Works
TRTC services use two types of server nodes: access servers and proxy servers.
- **Access server**
This type of nodes use high-quality lines and high-performance servers and are better suited to drive low-latency end-to-end calls, but the unit cost is relatively high.
- **Proxy server**
This type of servers use mediocre lines and average-performance servers and are better suited to power high-concurrency stream pulling and playback. The unit cost is relatively low.

In the live streaming modes, TRTC has introduced the concept of "role". Users are either in the role of "anchor" or "audience". Anchors are assigned to access servers, and audience to proxy servers. Each room allows up to 100,000 users in the role of audience.
For audience to speak, they must switch the role (`switchRole`) to “anchor”. The switching process involves users being migrated from proxy servers to access servers. TRTC’s low-latency streaming and smooth mic on/off technologies help keep this process short.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code
You can visit [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example) to obtain the sample code used in this document.
![](https://main.qcloudimg.com/raw/959efe00790a0a2952f8837a48baec25.png)

>?If your access to GitHub is slow, download the ZIP file [here](https://liteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip).

## Directions
[](id:step1)
### Step 1. Integrate the SDKs
You can integrate the **TRTC SDK** into your project in the following ways:
#### Method 1: automatic loading (AAR)
The TRTC SDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
The TRTC SDK has integrated `TRTC-API-Example`, which offers sample code for your reference. Use Android Studio to open your project and follow the steps below to modify the `app/build.gradle` file.

1. Add the TRTC SDK dependency to `dependencies`.
```
dependencies {
      compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
>?Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
>
```
 defaultConfig {
      ndk {
          abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
      }
  }
```
3. Click **Sync Now** to sync the SDK.
 If you have no problem connecting to JCenter, the SDK will be downloaded and integrated into your project automatically.

#### Method 2: manual integration
You can download the [ZIP file](https://intl.cloud.tencent.com/document/product/647/34615) of the SDK and integrate it into your project as instructed in [SDK Quick Integration > Android](https://intl.cloud.tencent.com/document/product/647/35093).


[](id:step2)
### Step 2. Configure app permissions.
Add camera, mic, and network permission requests in `AndroidManifest.xml`.

```
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />

<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```


[](id:step3)
### Step 3. Initialize an SDK instance and configure event callbacks

1. Call the [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) API to create a `TRTCCloud` instance.
 ```java
// Create a `TRTCCloud` instance
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
 ```
2. Set the attributes of `setListener` to subscribe to event callbacks and listen for event and error notifications.
```java
// Error notifications indicate that the SDK has stopped working and therefore must be listened for
@Override
public void onError(int errCode, String errMsg, Bundle extraInfo) {
    Log.d(TAG, "sdk callback onError");
    if (activity != null) {
        Toast.makeText(activity, "onError: " + errMsg + "[" + errCode+ "]" , Toast.LENGTH_SHORT).show();
        if (errCode == TXLiteAVCode.ERR_ROOM_ENTER_FAIL) {
            activity.exitRoom();
        }
    }
}
```

[](id:step4)
### Step 4. Assemble the room entry parameter `TRTCParams`
When calling the [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) API, you need to pass in a key parameter [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59), which includes the following required fields:

| Parameter | Type | Description | Example |
|---------|---------|---------|---------|
| sdkAppId | Number | Application ID, which you can view in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>. |1400000123 |
| userId | String | Can contain only letters (a-z and A-Z), digits (0-9), underscores, and hyphens. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Number | Numeric room ID. For string-type room ID, use `strRoomId` in `TRTCParams`. | 29834 |

>!
>-In TRTC, users with the same `userId` cannot be in the same room at the same time as it will cause a conflict.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

[](id:step5)
### Step 5. Enables camera preview and mic capturing
1. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) to enable preview of the local camera. The SDK will ask for camera permission.
2. Call [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) to set the display mode of the local video image:
 - `Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
 - `Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
3. Call [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) to set the encoding parameters for the local video, which determine the [quality of your video](https://intl.cloud.tencent.com/document/product/647/35153) seen by other users in the room.
4. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) to turn the mic on. The SDK will ask for mic permission.

```java
// Sample code: publish the local audio/video stream
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, localView);
// Set local video encoding parameters
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_960_540;
encParam.videoFps = 15;
encParam.videoBitrate = 1200;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
mTRTCCloud.setVideoEncoderParam(encParam);
mTRTCCloud.startLocalAudio();
```

[](id:step6)
### Step 6. Sets beauty filters

1. Call [getBeautyManager()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) to get the beauty filter management class [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).
2. Call [setBeautyStyle()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) to set the beauty filter style.
 - `Smooth`: smooth. This style features more obvious skin smoothing effect and is typically used by influencers.
 - `Nature`: natural. This style retains more facial details and is more natural.
 - `Pitu`: This style is supported only in the [Enterprise Edition](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise).
3. Call [setBeautyLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#a3931ccd8fa54bb846783ab4d6ca2874b) to set the skin smoothing strength (`5` is recommended).
4. Call [setWhitenessLevel()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#ab08c07ce725dbb8769b61fe0c76b0e95) to set the skin brightening strength (`5` is recommended).


[](id:step7)
### Step 7. Create a room and push streams
1. Set the `role` field in [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) to **`TRTCCloudDef.TRTCRoleAnchor`** to take the role of “anchor”.
2. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c), specifying **`appScene`**, and a room whose ID is the value of the `roomId` field in `TRTCParams` will be created.
 - `TRTCCloudDef.TRTC_APP_SCENE_LIVE`: the interactive video streaming mode, which is used in the example of this document
 - `TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM`: the interactive audio streaming mode
3. After the room is created, start encoding and transferring audio/video data. The SDK will return the [onEnterRoom(result)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) callback. If `result` is greater than 0, room entry succeeds, and the value indicates the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.

```java
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = 908;
    trtcParams.userSig = usersig;
    mTRTCCloud.enterRoom(trtcParams, TRTCCloudDef.TRTC_APP_SCENE_LIVE);
}

@Override
public void onEnterRoom(long result) {
    if (result > 0) {
        toastTip("Entered room successfully; the total time used is [\(result)] ms")
    } else {
        toastTip("Failed to enter the room; the error code is [\(result)]")
    }
}
```

[](id:step8)
### Step 8. Enter the room as audience
1. Set the `role` field in [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) to **`TRTCCloudDef.TRTCRoleAudience`** to take the role of “audience”.
2. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) to enter the room whose ID is the value of the `roomId` field in `TRTCParams`, specifying **`appScene`**.
 - `TRTCCloudDef.TRTC_APP_SCENE_LIVE`: the interactive video streaming mode, which is used in the example of this document
 - `TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM`: the interactive audio streaming mode
3. Watch the anchor’s video:
 - If you know the anchor’s `userId`, call [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) with the anchor’s `userId` passed in to play the anchor's video.
 - If you do not know the anchor’s `userId`, find the anchor’s `userId` in the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) callback, which you will receive after room entry, and call [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) with the anchor’s `userId` passed in to play the anchor’s video.

[](id:step9)
### Step 9. Co-anchor
1. Call [switchRole(TRTCCloudDef.TRTCRoleAnchor)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) to switch the role to “anchor” (`TRTCCloudDef.TRTCRoleAnchor`).
2. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) to enable preview of the local image.
3. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) to enable mic capturing.

```java
// Sample code: start co-anchoring
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mTrtcCloud.startLocalAudio();
mTrtcCloud.startLocalPreview(mIsFrontCamera, localView);

// Sample code: end co-anchoring
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAudience);
mTrtcCloud.stopLocalAudio();
mTrtcCloud.stopLocalPreview();
```


[](id:step10)
### Step 10. Compete across rooms

Anchors from two rooms can compete with each other without exiting their current rooms.

1. Anchor A calls the [connectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) API. The API uses parameters in JSON strings, so anchor A needs to pass the `roomId` and `userId` of anchor B in the format of `{"roomId": 978,"userId": "userB"}` to the API.
2. After the cross-room call is set up, anchor A will receive the [onConnectOtherRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) callback, and all users in both rooms will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) and [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) callbacks.
 For example, after anchor A in room "001" uses `connectOtherRoom()` to call anchor B in room “002” successfully, all users in room "001" will receive the `onUserVideoAvailable(B, true)` and `onUserAudioAvailable(B, true)` callbacks, and all users in room "002" will receive the `onUserVideoAvailable(A, true)` and `onUserAudioAvailable(A, true)` callbacks.
3. Users in both rooms can call [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) to play the video of the anchor in the other room, and audio will be played automatically.

```java
// Sample code: cross-room competition
mTRTCCloud.ConnectOtherRoom(String.format("{\"roomId\":%s,\"userId\":\"%s\"}", roomId, username));
```

[](id:step11)
### Step 11. Exit the room

Call [exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) to exit the room. The SDK disables and releases devices such as cameras and mics during room exit. Therefore, room exit is not an instant process. It completes only after the [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) callback is received.

```java
// Please wait for the `onExitRoom` callback after calling the room exit API.
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

>! If your application integrates multiple audio/video SDKs, please wait after you receive the `onExitRoom` callback to start other SDKs; otherwise, the device busy error may occur.

