## Use Cases
TRTC supports four room entry modes, among which video call (VideoCall) and audio call (VoiceCall) are classified as call mode, while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as live streaming mode.
TRTC in live streaming mode supports a maximum of 100,000 online users in one single room with a co-anchoring latency of below 300 ms and a watch latency of below 1,000 ms and enables users to mic on/off smoothly. This mode is suitable for such application scenarios as low-latency interactive live streaming, interactive classroom for up to 100,000 participants, video dating, online education, remote training, and large-scale conferencing.

## How It Works
The TRTC service consists of two types of server nodes: access servers and proxy servers:
- **Access server**
Backed by the highest-quality lines and high-performance servers, this type of nodes is ideal for processing end-to-end low-latency co-anchoring calls, but the fees per unit time are relatively high.
- **Proxy server**
With general lines and average-performance servers, this type of nodes is suitable for processing high-concurrence playback of pulled streams, and the fees per unit time are low.

In live streaming mode, TRTC uses the concept of "role". Specifically, users are divided into two roles, namely, "anchors" and "viewers". "Anchors" will be allocated to access servers, while "viewers" to proxy servers. A room can accommodate up to 100,000 viewers.
If a "user" wants to mic on, the role needs to be switched (switchRole) to "anchor" for the user to speak. During role switch, the user is also migrated from a proxy server to an access server. Thanks to its proprietary low-latency watch and smooth mic-on/off technologies, TRTC can get the whole switch done in a very short time.

## Sample Code
You can log in to [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCSimpleDemo) to get the sample code related to this document.

>If your access to GitHub is slow, you can directly download [TXLiteAVSDK_TRTC_Android_latest.zip](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip).

## Directions
<span id="step1"> </span>
### Step 1. Integrate the SDK
You can integrate the **TRTC SDK** into your project in the following ways:
#### Method 1. Automatically load the SDK (aar)
The TRTC SDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
You only need to use Android Studio to open the project to be integrated with the SDK (integration with `TRTCSimpleDemo` has already been completed, and the sample code is for your reference) and modify the `app/build.gradle` file in simple steps to complete SDK integration:

1. Add the TRTC SDK dependencies to `dependencies`.
```
dependencies {
      compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by the application.
>Currently, the TRTC SDK supports armeabi, armeabi-v7a, and arm64-v8a.
>
```
 defaultConfig {
      ndk {
          abiFilters "armeabi", "armeabi-v7a", "arm64-v8a"
      }
  }
```
3. Click **Sync Now** to sync the SDK.
 If JCenter can be connected to, the SDK will be automatically downloaded and integrated into the project.

#### Method 2. Download the ZIP package for manual integration
You can directly download the [ZIP package](https://intl.cloud.tencent.com/document/product/647/34615) and integrate the SDK into your project as instructed in [Quick Integration (Android)](https://intl.cloud.tencent.com/document/product/647/35093#.E6.96.B9.E6.B3.95.E4.BA.8C.EF.BC.9A.E6.89.8B.E5.8A.A8.E4.B8.8B.E8.BD.BD.EF.BC.88aar.EF.BC.89).


<span id="step2"> </span>
### Step 2. Configure application permissions
Add the permissions to request camera, mic, and network access in the `AndroidManifest.xml` file.

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


<span id="step3"> </span>
### Step 3. Initialize an SDK instance and listen on the event callback

1. Call the [sharedInstance()](https://intl.cloud.tencent.com/document/product/647/35125) API to create a `TRTCCloud` instance.
 ```java
// Create a `trtcCloud` instance
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
 ```
2. Set the `setListener` attribute to register the event callback and listen on relevant events and error notifications.
```java
// Listen on error notifications, which indicate that the SDK cannot continue to run
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

<span id="step4"> </span>
### Step 4. Assemble the room entry parameter `TRTCParams`
When calling the [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) API, you need to enter a key parameter [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59), which includes the following required fields:

| Parameter | Field Type | Description | Example |
|---------|---------|---------|---------|
| sdkAppId | Numeric | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app). | 1400000123 |
| userId | String | It can contain only letters (a–z and A–Z), digits (0–9), underscores, and hyphens. | test_user_001 |
| userSig | String | `userSig` can be calculated based on `userId`. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Numeric | Room IDs in string type are not supported by default, as they will lower the room entry speed. If you need to use string-type room IDs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. | 29834 |

>In TRTC, users with the same `userId` cannot be in the same room at the same time; otherwise, there will be a conflict.

<span id="step5"> </span>
### Step 5. The anchor enables camera preview and mic capture
1. The anchor can call [startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) to enable the preview of local camera, and the SDK will request the system camera access.
2. The anchor can call [setLocalViewFillMode()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) to set the display mode of the local video image:
 - `Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
 - `Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
3. The anchor can call [setVideoEncoderParam()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.
4. The anchor can call [startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) to enable the mic, and the SDK will request the system mic access.

```java
// Sample code: publish local audio/video streams
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, localView);
// Set local video encoding parameter
TRTCCloudDef.TRTCVideoEncParam encParam = new TRTCCloudDef.TRTCVideoEncParam();
encParam.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_960_540;
encParam.videoFps = 15;
encParam.videoBitrate = 1200;
encParam.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
mTRTCCloud.setVideoEncoderParam(encParam);
mTRTCCloud.startLocalAudio();
```

<span id="step6"> </span>
### Step 6. The anchor sets beauty filters

1. The anchor can call [getBeautyManager()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) to get the beauty filter setting API [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).
2. The anchor can call [setBeautyStyle()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) to set the beauty filter style.
 - Smooth: smooth style, which has more obvious skin smoothing effect, similar to the selfie style of internet influencers.
 - Nature: natural style, which retains more facial details and seems more natural subjectively.
 - Pitu: it is supported only for the [Enterprise Edition](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise).
3. The anchor can call [setBeautyLevel()](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#a7f388122cf319218b629fb8e192a2730) to set the skin smoothing level (level 5 is generally okay).
4. The anchor can call [setWhitenessLevel()](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html#aa4e57d02a4605984f4dc6d3508987746) to set the skin brightening level (level 5 is generally okay).


<span id="step7"> </span>
### Step 7. The anchor creates a room and starts push
1. The anchor sets the `role` field in [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) to **`TRTCCloudDef.TRTCRoleAnchor`**, which indicates that the current user role is anchor.
2. The anchor can call [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) to create an audio/video room whose ID is the `roomId` field value in the `TRTCParams` parameter and specify the **`appScene`** parameter:
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE: interactive live video streaming mode, which is used as an example in this document.
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM: interactive live audio streaming mode.
3. After a room is successfully created, the anchor starts encoding and transferring audio/video data. At the same time, the SDK will call back the [onEnterRoom(result)](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) event. If `result` is greater than 0, the room entry succeeds, and the specific value indicates the time in milliseconds (ms) used for entering the room; if `result` is less than 0, the room entry fails, and the specific value indicates the error code of the failure.

```java
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = usersig;
    trtcParams.userSig = 908;
    mTRTCCloud.enterRoom(trtcParams, TRTC_APP_SCENE_VIDEOCALL);
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

<span id="step8"> </span>
### Step 8. The viewer enters the room to watch the live stream
1. The viewer sets the field `role` in [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59) to **`TRTCCloudDef.TRTCRoleAudience`**, which indicates that the current user role is viewer.
2. The viewer can call [enterRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) to enter the audio/video room whose ID is the `roomId` field value in the `TRTCParams` parameter and specify the **`appScene`** parameter:
 - TRTCCloudDef.TRTC_APP_SCENE_LIVE: interactive live video streaming mode, which is used as an example in this document.
 - TRTCCloudDef.TRTC_APP_SCENE_VOICE_CHATROOM: interactive live audio streaming mode.
3. View the anchor's video image:
 - If the viewer knows the anchor's `userId` in advance, the viewer can use it to call [startRemoteView(userId, view)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) after successfully entering the room so as to display the anchor's video image.
 - If the viewer does not know the anchor's `userId`, the viewer will receive the [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) event notification after successfully entering the room. The viewer can use the anchor's `userId` obtained from the callback to call [startRemoteView(userId, view)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) so as to display the anchor's video image.

<span id="step9"> </span>
### Step 9. The viewer co-anchors with the anchor
1. The viewer can call [switchRole(TRTCCloudDef.TRTCRoleAnchor)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) to switch the role to anchor (TRTCCloudDef.TRTCRoleAnchor).
2. The viewer can call [startLocalPreview()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) to enable the local image.
3. The viewer can call [startLocalAudio()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) to enable mic capture:

```java
// Sample code: the viewer mics on
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mTrtcCloud.startLocalAudio();
mTrtcCloud.startLocalPreview(mIsFrontCamera, localView);

// Sample code: the viewer mics off
mTrtcCloud.switchRole(TRTCCloudDef.TRTCRoleAudience);
mTrtcCloud.stopLocalAudio();
mTrtcCloud.stopLocalPreview();
```


<span id="step10"> </span>
### Step 10. Anchors compete across rooms (cross-room co-anchoring)

In TRTC, two anchors in different rooms can use the "cross-room call" feature to engage in "cross-room co-anchoring" without the need to exit their current rooms.

1. Anchor A calls the [connectOtherRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) API. Currently, the API parameters are in JSON format, and `roomId` and `userId` of anchor B need to be spliced into a parameter in the format of `{"roomId": "978","userId": "userB"}` and then passed in to the API function.
2. After the cross-room call is successfully made, anchor A will receive the [onConnectOtherRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) event callback. At the same time, all users in both rooms will receive the [onUserVideoAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) and [onUserAudioAvailable()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) event callbacks.
 For example, when anchor A in room "001" uses `connectOtherRoom()` to successfully call anchor B in room "002", all users in room "001" will receive the `onUserVideoAvailable(B, true)` and `onUserAudioAvailable(B, true)` callbacks of anchor B, and all users in room "002" will receive the `onUserVideoAvailable(A, true)` and `onUserAudioAvailable(A, true)` callbacks of anchor A.
3. Users in both rooms can call [startRemoteView(userId, view)](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) to display the video image of the anchor in the other room, and audio will be automatically played back.

```java
// Sample code: cross-room co-anchoring
mTRTCCloud.ConnectOtherRoom(String.format("{\"roomId\":%s,\"userId\":\"%s\"}", roomId, username));
```

<span id="step11"> </span>
### Step 11. Exit the current room

Call the [exitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) method to exit the room. The SDK needs to disable and release hardware devices such as the camera and mic during room exit. Therefore, room exit is not completed as soon as the method is called. Only after the [onExitRoom()](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) callback is received can the room exit be considered completed.

```java
// Please wait for the `onExitRoom` event callback after calling the room exit method
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

> If multiple audio/video SDKs are integrated into your application, please enable other SDKs only after receiving the `onExitRoom` callback; otherwise, hardware occupancy issues may occur.

