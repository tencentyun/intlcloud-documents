## Use Cases

TRTC supports four room entry modes, among which video call (VideoCall) and audio call (VoiceCall) are classified as [call mode](https://intl.cloud.tencent.com/document/product/647/36069), while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as live streaming mode.
TRTC in live streaming mode supports a maximum of 100,000 online users in one single room with a co-anchoring latency of below 300 ms and a watch latency of below 1,000 ms and enables users to mic on/off smoothly. This mode is suitable for such application scenarios as low-latency interactive live streaming, interactive classroom for up to 100,000 participants, video dating, online education, remote training, and large-scale conferencing.

## How It Works

The TRTC service consists of two types of server nodes: access servers and proxy servers:

-   **Access server**
    Backed by the highest-quality lines and high-performance servers, this type of nodes is ideal for processing end-to-end low-latency co-anchoring calls, but the fees per unit time are relatively high.
-   **Proxy server**
    With general lines and average-performance servers, this type of nodes is suitable for processing high-concurrence playback of pulled streams, and the fees per unit time are low.

In call mode, all users in the TRTC room will be assigned to access servers, which means that each user is an "anchor" and can speak at any time (up to 30 concurrent upstreams are supported), so it is suitable for scenarios such as online conferencing, but the number of members in a single room is limited to 300.

![](https://main.qcloudimg.com/raw/afd9cefdfe72a2914fd55f8586f2c7e0.jpg)

## Sample Code

You can log in to [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron) to get the sample code related to this document.

## Directions

<span id="step1"> </span>
### Step 1. Try to run the official SimpleDemo

You are recommended to read [Run SimpleDemo (Electron)](https://intl.cloud.tencent.com/document/product/647/35089) first and then follow the instructions to run the official SimpleDemo.

If the SimpleDemo can run properly, it means that you have mastered the method of installing Electron in your project.

If the SimpleDemo cannot run, the problem is likely to be related to Electron download and installation. In this case, you can refer to Electron's official [installation guide](https://www.electronjs.org/docs/tutorial/installation) for assistance.

<span id="step2"> </span>
### Step 2. Integrate trtc-electron-sdk into your project

If [step 1](#step1) is executed normally and the result is as expected, it means that you have mastered the method of installing the Electron environment.

You can conduct secondary development on the official demo, and the initial stage of your project will go smoothly.

You can also run the following command to install `trtc-electron-sdk` into your existing project:

```bash
npm install trtc-electron-sdk --save
```

<span id="step3"> </span>
### Step 3. Initialize an SDK instance and listen on the event callback

Create a `trtc-electron-sdk` instance:

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

Listen on the `onError` event:

```javascript
// Error notifications should be listened on, captured, and sent to the user
let onError = function(err) {
  console.error(err);
}
trtcCloud.on('onError',onError);
```

<span id="step4"> </span>
### Step 4. Assemble the room entry parameter `TRTCParams`

When calling the [enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) API, you need to enter a key parameter [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html), which includes the following required fields:

| Parameter | Type | Description | Example |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | Numeric | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app). | 1400000123             |
| userId | String | It can contain only letters (a–z and A–Z), digits (0–9), underscores, and hyphens. | test_user_001|
| userSig | String | `userSig` can be calculated based on `userId`. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166) . | eJyrVareCeYrSy1SslI... |
| roomId | Numeric | Room IDs in string type are not supported by default, as they will lower the room entry speed. If you need to used string-type room IDs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. | 29834 |

```javascript
import {
  TRTCParams,
  TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
param.role = TRTCRoleType.TRTCRoleAnchor; // Set the role to "anchor"
```

> In TRTC, users with the same `userId` cannot be in the same room at the same time; otherwise, there will be a conflict.

### Step 5. The anchor enables camera preview and mic capture

1. The anchor can call [startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) to enable the preview of local camera, and the SDK will request the system camera access.
2. The anchor can call `setLocalViewFillMode()` to set the display mode of the local video image:
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
3. The anchor can call [setVideoEncoderParam()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.
4. The anchor can call [startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) to enable the mic, and the SDK will request the system mic access.

```javascript
// Sample code: send local audio/video streams
trtcCloud.startLocalPreview(view);
trtcCloud.startLocalAudio();
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);

// Set local video encoding parameter
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
```

### Step 6. The anchor sets beauty filters

1. The anchor can call [setBeautyStyle(style, beauty, white, ruddiness)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle) to enable beauty filters.
2. Parameter description:
    -   style: beauty filter style: smooth or natural. The smooth style has more obvious skin smoothing effect and is suitable for entertaining scenarios.
        -   `TRTCBeautyStyle.TRTCBeautyStyleSmooth`: smooth, which is suitable for shows since it has more obvious effect.
        -   `TRTCBeautyStyle.TRTCBeautyStyleNature`: natural style, which retains more facial details and seems more natural subjectively.
    -   beauty: effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
    -   white: effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect.
    -   ruddiness: effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. This parameter does not take effect on Windows currently.

```javascript
// Enable beauty filters 
trtcCloud.setBeautyStyle(TRTCBeautyStyle.TRTCBeautyStyleNature, 5, 5, 5);
```



### Step 7. The anchor creates a room and starts push

1. The anchor sets the `role` field in [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) to **`TRTCRoleType.TRTCRoleAnchor`**, which indicates that the current user role is anchor.
2. The anchor can call `enterRoom( )` to create an audio/video room whose ID is the `roomId` field value in the `TRTCParams` parameter and specify the `appScene` parameter:

    -   `TRTCAppScene.TRTCAppSceneLIVE`: interactive video live streaming. Mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms. Live streaming to hundreds of thousands of concurrent viewers is supported with the playback latency down to 1,000 ms. This document uses this mode as an example.
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: interactive audio live streaming. Mic can be turned on/off smoothly without waiting for switchover, and the anchor latency is as low as less than 300 ms. Live streaming to hundreds of thousands of concurrent viewers is supported with the playback latency down to 1,000 ms.
    
    For more information on `TRTCAppScene`, please see [TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene).
3. After a room is successfully created, the anchor starts encoding and transferring audio/video data. At the same time, the SDK will call back the [onEnterRoom(result)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) event. If `result` is greater than 0, the room entry succeeds, and the specific value indicates the time in milliseconds (ms) used for entering the room; if `result` is less than 0, the room entry fails, and the specific value indicates the error code of the failure.


```javascript
let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
  } else {
    console.warn(`onEnterRoom: failed to enter the room ${result}`);
  }
};

trtcCloud.on('onEnterRoom', onEnterRoom);

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
param.role = TRTCRoleType.TRTCRoleAnchor;
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```



### Step 8. The viewer enters the room to watch the live stream

1. The viewer sets the field `role` in [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) to **`TRTCRoleType.TRTCRoleAudience`**, which indicates that the current user role is viewer.

1. The viewer can call `enterRoom()` to enter the audio/video room whose ID is the `roomId` field value in the `TRTCParams` parameter and specify the `appScene` parameter:

    -   `TRTCAppScene.TRTCAppSceneLIVE`: interactive video live streaming.
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: interactive audio live streaming.

2. View the anchor's video image:

    - If the viewer knows the anchor's `userId` in advance, the viewer can use it to call [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) after successfully entering the room so as to display the anchor's video image.
    - If the viewer does not know the anchor's `userId`, the viewer will receive the [onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) event notification after successfully entering the room. The viewer can use the anchor's `userId` obtained from the callback to call [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) so as to display the anchor's video image.


```html
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // Room entry callback, which will be triggered upon successful room entry
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
    } else {
      console.warn(`onEnterRoom: failed to enter the room ${result}`);
    }
  };
  // This callback will be triggered when the anchor enables/disables camera push
  let onUserVideoAvailable = function(userId, available) {
    if (available === 1) {
        let id = `${userId}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
        let view = document.getElementById(id);
        if (!view) {
          view = document.createElement('div');
          view.id = id;
          videoContainer.appendChild(view);
        }
        trtcCloud.startRemoteView(userId, view);
        trtcCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    } else {
        let id = `${userId}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
        let view = document.getElementById(id);
        if (view) {
          videoContainer.removeChild(view);
        }
    }
  };

  trtcCloud.on('onEnterRoom', onEnterRoom);
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

  let param = new TRTCParams();
  param.sdkAppId = 1400000123;
  param.roomId = roomId;
  param.userId = 'test_user_001';
  param.userSig = 'eJyrVareCeYrSy1SslI...';
  param.role = TRTCRoleType.TRTCRoleAudience; // Set the role to "viewer"
  trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
</script>
```

### Step 9. The viewer co-anchors with the anchor

1. The viewer can call [switchRole(TRTCRoleType.TRTCRoleAnchor)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole) to switch the role to anchor (`TRTCRoleType.TRTCRoleAnchor`).
2. The viewer can call [startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) to enable the local image.
3. The viewer can call [startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) to enable mic capture:


```javascript
// Sample code: the viewer mics on
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

// Sample code: the viewer mics off
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview();
```



### Step 10. Anchors compete across rooms (cross-room co-anchoring)

In TRTC, two anchors in different rooms can use the "cross-room call" feature to engage in "cross-room co-anchoring" without the need to exit their current rooms.

1. Anchor A calls the [connectOtherRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom) API. Currently, the API parameters are in JSON format, and `roomId` and `userId` of anchor B need to be spliced into a parameter in the format of `{"roomId": 978,"userId": "userB"}` and then passed in to the API function.
2. After the cross-room call is successfully made, anchor A will receive the [onConnectOtherRoom(userId, errCode, errMsg)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom) event callback. At the same time, all users in both rooms will receive the [onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) and [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) event callbacks.
    For example, when anchor A in room "001" uses `connectOtherRoom()` to successfully call anchor B in room "002", all users in room "001" will receive the `onUserVideoAvailable(B, true)` and `onUserAudioAvailable(B, true)` callbacks of anchor B, and all users in room "002" will receive the `onUserVideoAvailable(A,  true)` and `onUserAudioAvailable(A, true)` callbacks of anchor A.
3. Users in both rooms can call [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) to display the video image of the anchor in the other room, and audio will be automatically played back.

![](https://main.qcloudimg.com/raw/292309441c681909c6a98a715f29fe77.jpg)

```javascript
// Sample code: cross-room co-anchoring

let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`Successfully connected to the room of anchor ${userId}`);
  } else {
    console.warn(`Failed to connect to another anchor's room: ${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
```

### Step 11. Exit the current room  

Call the [exitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) method to exit the room. The SDK needs to disable and release hardware devices such as the camera and mic during room exit. Therefore, room exit is not completed as soon as the method is called. Only after the [onExitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) callback is received can the room exit be considered completed.

```javascript
// Please wait for the `onExitRoom` event callback after calling the room exit method
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);

```

> If multiple audio/video SDKs are integrated into your Electron program, please enable other SDKs only after receiving the `onExitRoom` callback; otherwise, hardware occupancy issues may occur.
