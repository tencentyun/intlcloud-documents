## Application Scenarios
TRTC supports four room entry modes. Video call (`VideoCall`) and audio call (`AudioCall`) are the call modes, and interactive video streaming (`Live`) and interactive audio streaming (`VoiceChatRoom`) are the [live streaming modes](https://intl.cloud.tencent.com/document/product/647/35108).
The call modes allow a maximum of 300 users in each TRTC room, and up to 50 of them can speak at the same time. The call modes are suitable for scenarios such as one-to-one video calls, video conferencing with up to 300 participants, online medical consultation, remote interviews, video customer service, and online Werewolf playing.

## How It Works
TRTC services use two types of server nodes: access servers and proxy servers.
- **Access server**
This type of nodes use high-quality lines and high-performance servers and are better suited to drive low-latency end-to-end calls, but the unit cost is relatively high.
- **Proxy server**
This type of servers use mediocre lines and average-performance servers and are better suited to power high-concurrency stream pulling and playback. The unit cost is relatively low.

In the call modes, all users in a TRTC room are assigned to access servers and are in the role of “anchor”. This means the users can speak to each other at any point during the call (up to 50 users can send data at the same time). This makes the call modes suitable for use cases such as online conferencing, but the number of users in each room is capped at 300.
![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code
You can visit [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTC-API-Example) to obtain the sample code used in this document.
![](https://main.qcloudimg.com/raw/cdef573133900a8dce22dcca5242fcfc.png)

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
You can directly download the [ZIP package](https://intl.cloud.tencent.com/document/product/647/34615) and integrate the SDK into your project as instructed in [Quick Integration (Android)](https://intl.cloud.tencent.com/document/product/647/35093).


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
```
// Create a `TRTCCloud` instance
mTRTCCloud = TRTCCloud.sharedInstance(getApplicationContext());
mTRTCCloud.setListener(new TRTCCloudListener(){
    // Processing callbacks
    ...
});
```
2. Set the attributes of `setListener` to subscribe to event callbacks and listen for event and error notifications.
```
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
| userId | String | Can contain only letters (a-z and A-Z), digits (0-9), underscores, and hyphens. We recommend you set it based on your business account system. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Number | Numeric room ID. For string-type room ID, use `strRoomId` in `TRTCParams`. | 29834 |

>!In TRTC, users with the same `userID` cannot be in the same room at the same time as it will cause a conflict.

[](id:step5)
### Step 5. Create and enter a room
1. Call [enterRoom()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) to enter the audio/video room specified by `roomId` in the `TRTCParams` parameter. If the room does not exist, the SDK will automatically create it with the `roomId` value as the room number.
2. Set the **`appScene`** parameter according to your actual application scenario. Inappropriate `appScene` values may lead to increased lag or decreased clarity.
 - For video calls, please set `TRTC_APP_SCENE_VIDEOCALL`.
 - For audio calls, please set `TRTC_APP_SCENE_AUDIOCALL`.
3. You will receive the `onEnterRoom(result)` callback. If `result` is greater than 0, room entry succeeds, and the value of `result` indicates the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.

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
>! 
>- If the room entry fails, the SDK will also call back the `onError` event and return the parameters `errCode` ([error code](https://intl.cloud.tencent.com/document/product/647/35130)), `errMsg` (error message), and `extraInfo` (reserved parameter).
>- If you are already in a room, you must call `exitRoom` to exit the room before entering another room.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

[](id:step6)
### Step 6. Subscribe to remote audio/video streams
The SDK supports automatic subscription and manual subscription.

#### Automatic subscription (default)
In automatic subscription mode, after room entry, the SDK will automatically receive audio streams from other users in the room to achieve the best "instant broadcasting" effect:
1. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) event notification, and the SDK will automatically play back the audio of the remote user.
2. You can call [muteRemoteAudio(userId, true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) to mute a specified user (`userId`), or [muteAllRemoteAudio(true)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) to mute all remote users. The SDK will stop pulling the audio data of the user(s).
3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) event notification; however, since the SDK has not received instructions on how to display the video data at this time, video data will not be processed automatically. You need to associate the video data of the remote user with the display `view` by calling the [startRemoteView(userId, view)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) method.
4. Call [setRemoteViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) to specify the display mode of a remote video.
 - `Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
 - `Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
5. Call [stopRemoteView(userId)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a) to block the video data of a specified user (`userId`) or [stopAllRemoteView()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) to block the video data of all remote users. The SDK will stop pulling the video data of the user(s).

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

>? If you do not call `startRemoteView()` to subscribe to the video stream immediately after receiving the `onUserVideoAvailable()` event callback, the SDK will stop pulling the remote video within 5 seconds.

#### Manual subscription
You can call [setDefaultStreamRecvMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) to switch the SDK to the manual subscription mode. In this mode, the SDK will not pull the data of other users in the room automatically. You have to start the process manually via APIs.

1. **Before room entry**, call the [setDefaultStreamRecvMode(false, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) API to set the SDK to manual subscription mode.
2. If other users in the room are sending audio data, you will receive the [onUserAudioAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) notification, and you need to call [muteRemoteAudio(userId, false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) to manually subscribe to the users’ audio. The SDK will decode and play the audio data received.
3. If a remote user in the room is sending video data, you will receive the [onUserVideoAvailable()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) notification, and you need to call [startRemoteView(userId, remoteView)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) to manually subscribe to the user's video data. The SDK will decode and play the video data received.


[](id:step7)
### Step 7. Publish the local stream
1. Call [startLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) to enable local mic capturing and encode and send the audio captured.
2. Call [startLocalPreview()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) to enable local camera capturing and encode and send the video captured.
3. Call [setLocalViewFillMode()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) to set the display mode of the local video:
 - `Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
 - `Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
4. Call [setVideoEncoderParam()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.
```java
// Sample code: publish the local audio/video stream
mTRTCCloud.setLocalViewFillMode(TRTC_VIDEO_RENDER_MODE_FIT);
mTRTCCloud.startLocalPreview(mIsFrontCamera, mLocalView);
mTRTCCloud.startLocalAudio();
```

[](id:step8)
### Step 8. Exit the room

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


