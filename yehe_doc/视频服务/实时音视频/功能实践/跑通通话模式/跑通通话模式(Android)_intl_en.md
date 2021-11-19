## Use Cases
TRTC supports four room entry modes, among which video call (VideoCall) and audio call (AudioCall) are classified as call mode, while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as [live streaming mode](https://cloud.tencent.com/document/product/647/35428).
In call mode, there can be a maximum of 300 members in a single TRTC room, and up to 30 of them can speak at the same time. This service is suitable for various scenarios such as one-to-one video call, video conferencing with up to 300 attendees, online medical diagnosis, video interview, video customer service, and online werewolf.

## How It Works
The TRTC service consists of two types of server nodes: access servers and proxy servers:
- **Access server**
Backed by the highest-quality lines and high-performance servers, this type of nodes is ideal for processing end-to-end low-latency co-anchoring calls, but the fees per unit time are relatively high.
- **Proxy server**
With general lines and average-performance servers, this type of nodes is suitable for processing high-concurrence playback of pulled streams, and the fees per unit time are low.

In call mode, all users in the TRTC room will be assigned to access servers, which means that each user is an "anchor" and can speak at any time (up to 30 concurrent upstreams are supported), so it is suitable for scenarios such as online conferencing, but the number of members in a single room is limited to 300.

## Sample Code
You can log in to [GitHub] to get the sample code related to this document.

>?If your access to GitHub is slow, you can directly download [TXLiteAVSDK_TRTC_Android_latest.zip](https://lliteav.sdk.qcloud.com/download/latest/TXLiteAVSDK_TRTC_Android_latest.zip).

## Directions
[](id:step1)
### Step 1. Integrate the SDK
You can integrate the **TRTC SDK** into your project in the following ways:
#### Method 1. Automatically load the SDK (aar)
The TRTC SDK has been released to the JCenter repository, and you can configure Gradle to download updates automatically.
You only need to use Android Studio to open the project to be integrated with the SDK (integration with `TRTC-API-Example` has already been completed, and the sample code is for your reference) and modify the `app/build.gradle` file in simple steps to complete SDK integration:

1. Add the TRTC SDK dependencies to `dependencies`.
```
dependencies {
      compile 'com.tencent.liteav:LiteAVSDK_TRTC:latest.release'
}
```
2. In `defaultConfig`, specify the CPU architecture to be used by the application.
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
 If JCenter can be connected to, the SDK will be automatically downloaded and integrated into the project.

#### Method 2. Download the ZIP package for manual integration
You can directly download the [ZIP package](https://intl.cloud.tencent.com/document/product/647/34615) and integrate the SDK into your project as instructed in [Quick Integration (Android)](https://intl.cloud.tencent.com/document/product/647/35093).


[](id:step2)
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


[](id:step3)
### Step 3. Initialize an SDK instance and listen on the event callback

1. Call the [sharedInstance()](https://cloud.tencent.com/document/product/647/32267) API to create a `TRTCCloud` instance.
```
// Create a `trtcCloud` instance
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener());
```
2. Set the `setListener` attribute to register the event callback and listen on relevant events and error notifications.
```
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

[](id:step4)
### Step 4. Assemble the room entry parameter `TRTCParams`
When calling the [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) API, you need to enter a key parameter [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a674b3c744a0522802d68dfd208763b59), which includes the following required fields:

| Parameter | Field Type | Description | Example | 
|---------|---------|---------|---------|
| sdkAppId | Numeric | Application ID. You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>. |1400000123 | 
| userId | String | It can contain only letters (a–z and A–Z), digits (0–9), underscores, and hyphens. | test_user_001 | 
| userSig | String | `userSig` can be calculated based on `userId`. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Numeric | Numeric room ID. For string-type room ID, use `strRoomId` in `TRTCParams`. | 29834 |

>!In TRTC, users with the same `userId` cannot be in the same room at the same time; otherwise, there will be a conflict.

[](id:step5)
### Step 5. Create and enter a room
1. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) to enter the audio/video room specified by `roomId` in the `TRTCParams` parameter. If the room does not exist, the SDK will automatically create it with the `roomId` value as the room number.
2. Please set the appropriate **`appScene`** parameter according to the actual application scenario. An incorrect selection may lead to higher lagging rate or lower video definition than expected.
 - For video calls, please set `TRTC_APP_SCENE_VIDEOCALL`.
 - For audio calls, please set `TRTC_APP_SCENE_AUDIOCALL`.
3. After successful room entry, the SDK will call back the `onEnterRoom(result)` event. If `result` is greater than 0, the room entry succeeds, and the specific value indicates the time in milliseconds (ms) used for entering the room; if `result` is less than 0, the room entry fails, and the specific value indicates the error code of the failure.

```
public void enterRoom() {
    TRTCCloudDef.TRTCParams trtcParams = new TRTCCloudDef.TRTCParams();
    trtcParams.sdkAppId = sdkappid;
    trtcParams.userId = userid;
    trtcParams.roomId = 908;
    trtcParams.userSig = usersig;
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

> !
>- If the room entry fails, the SDK will also call back the `onError` event and return the parameters `errCode` ([error code](https://intl.cloud.tencent.com/document/product/647/35130)), `errMsg` (error message), and `extraInfo` (reserved parameter).
>- If you are already in a room, you must call `exitRoom()` to exit the current room first before entering the next room.

To avoid unexpected events, make sure that the same `appScene` value is used by different clients.

[](id:step6)
### Step 6. Subscribe to remote audio/video streams
The SDK supports both automatic subscription and manual subscription.

#### Automatic subscription mode (default)
In automatic subscription mode, after room entry, the SDK will automatically receive audio streams from other users in the room to achieve the best "instant broadcasting" effect:
1. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) event notification, and the SDK will automatically play back the audio of the remote user.
2. You can block the audio data of a specified `userId` through [muteRemoteAudio(userId, true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) or all remote users through [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba). After that, the SDK will no longer pull the audio data of the corresponding remote users.
3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) event notification; however, since the SDK has not received instructions on how to display the video data at this time, video data will not be processed automatically. You need to associate the video data of the remote user with the display `view` by calling the [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) method.
4. You can specify the display mode of the local video image through [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f):
 - `Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
 - `Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
5. You can block the video data of a specified `userId` through [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a) or all remote users through [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127). After that, the SDK will no longer pull the video data of the corresponding remote users.

```
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    TXCloudVideoView remoteView = remoteViewDic[userId];
    if (available) {
        mTRTCCloud.startRemoteView(userId, remoteView);
        mTRTCCloud.setRemoteViewFillMode(userId, TRTC_VIDEO_RENDER_MODE_FIT);
    } else {
        mTRTCCloud.stopRemoteView(userId);
    }
}
```

>? If you do not call `startRemoteView()` to subscribe to the video stream immediately after receiving the `onUserVideoAvailable()` event callback, the SDK will stop receiving remote video data within 5 seconds.

#### Manual subscription mode
You can specify the SDK to enter the manual subscription mode through the [setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) API. In this mode, the SDK will not automatically receive audio/video data of other users in the room; instead, you need to manually trigger the receipt through API functions.

1. **Before room entry**, call the [setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) API to set the SDK to manual subscription mode.
2. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) event notification. At this time, you need to manually subscribe to the user's audio data by calling [muteRemoteAudio(userId, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f), and the SDK will decode and play back it after receiving it.
3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) event notification. At this time, you need to manually subscribe to the user's video data by calling [startRemoteView(userId, remoteView)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c), and the SDK will decode and play back it after receiving it.


[](id:step7)
### Step 7. Publish the local audio/video stream
1. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) to enable local mic capture and encode and send the captured audio.
2. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) to enable local camera capture and encode and send the captured video.
3. Call [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) to set the display mode of the local video image:
 - `Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
 - `Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
4. Call [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.
```java
// Sample code: send local audio/video streams
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
mTRTCCloud.startLocalAudio();
```

[](id:step8)
### Step 8. Exit the current room

Call the [exitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) method to exit the room. The SDK needs to disable and release hardware devices such as the camera and mic during room exit. Therefore, room exit is not completed as soon as the method is called. Only after the [onExitRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) callback is received can the room exit be considered completed.

```java
// Please wait for the `onExitRoom` event callback after calling the room exit method
mTRTCCloud.exitRoom()

@Override
public void onExitRoom(int reason) {
    Log.i(TAG, "onExitRoom: reason = " + reason);
}
```

> !If multiple audio/video SDKs are integrated into your application, please enable other SDKs only after receiving the `onExitRoom` callback; otherwise, hardware occupancy issues may occur.
