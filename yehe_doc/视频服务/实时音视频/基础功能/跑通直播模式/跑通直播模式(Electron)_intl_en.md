## Application Scenarios

TRTC supports four room entry modes. Video call (`VideoCall`) and audio call (`VoiceCall`) are the [call modes](https://intl.cloud.tencent.com/document/product/647/36069), and interactive video streaming (`Live`) and interactive audio streaming (`VoiceChatRoom`) are the live streaming modes.
The live streaming modes allow a maximum of 100,000 concurrent users in each room with smooth mic on/off. Co-anchoring latency is kept below 300 ms and watch latency below 1,000 ms. The live streaming modes are suitable for use cases such as low-latency interactive live streaming, interactive classrooms for up to 100,000 participants, video dating, online education, remote training, and mega-scale conferencing.

## How It Works

TRTC services use two types of server nodes: access servers and proxy servers.

- **Access server**
    This type of nodes use high-quality lines and high-performance servers and are better suited to drive low-latency end-to-end calls.
- **Proxy server**
    This type of servers use mediocre lines and average-performance servers and are better suited to power high-concurrency stream pulling and playback.

In the call modes, all users in a TRTC room are assigned to access servers and are in the role of “anchor”. This means the users can speak to each other at any point during the call (up to 50 users can send data at the same time). This makes the call modes suitable for use cases such as online conferencing, but the number of users in each room is capped at 300.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code

You can obtain the sample code used in this document at [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron).

## Directions

[](id:step1)
### Step 1. Run the official `SimpleDemo`

We recommend that you read [Demo Quick Start > Electron](https://intl.cloud.tencent.com/document/product/647/35089) first and follow the instructions to run the official `SimpleDemo`.
- If you run `SimpleDemo` successfully, then you know how to install Electron in your project.
- If not, there may be a problem in the download or installation process. Try troubleshooting the problem by following the instructions in Electron's [installation document](https://www.electronjs.org/docs/tutorial/installation).

[](id:step2)
### Step 2. Integrate `trtc-electron-sdk` into your project

If you can [run SimpleDemo](#step1) successfully, then you know how to set up the Electron environment.

- You can develop your project based on the demo we provide to get started quickly.
- You can also run the following command to install `trtc-electron-sdk` in your project.
```bash
npm install trtc-electron-sdk --save
```

[](id:step3)
### Step 3. Initialize an SDK instance and configure event callbacks

Create a `trtc-electron-sdk` instance:

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

Listen for the `onError` event:

```javascript
// Error events must be listened for and captured, and error messages should be sent to users.
let onError = function(err) {
  console.error(err);
}
trtcCloud.on('onError',onError);
```

[](id:step4)
### Step 4. Assemble the room entry parameter `TRTCParams`

When calling the [enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) API, you need to pass in a key parameter [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html), which includes the following required fields:

| Parameter     | Field Type   | Description                                                         | Example                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | Number | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app) | 1400000123             |
| userId | String | Can contain only letters (a-z and A-Z), digits (0-9), underscores, and hyphens. We recommend you set it based on your business account system. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Number | Numeric room ID. For string-type room ID, use `strRoomId` in `TRTCParams`. | 29834 |

<dx-codeblock>
::: javascript javascript
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
:::
</dx-codeblock>

>! 
>-In TRTC, users with the same `userId` cannot be in the same room at the same time as it will cause a conflict.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

[](id:step5)
### Step 5. Enable camera preview and mic capturing
1.  Call [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) to enable preview of the local camera. The SDK will ask for camera permission.
2. Call `setLocalViewFillMode()` to set the display mode of the local video image.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
3. Call [setVideoEncoderParam()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) to set the encoding parameters of the local video, which determine the [quality of your video](https://intl.cloud.tencent.com/document/product/647/35153) seen by other users in the room.
4.  Call [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) to turn the mic on. The SDK will ask for mic permission.


<dx-codeblock>
::: javascript javascript
// Sample code: publish the local audio/video stream
trtcCloud.startLocalPreview(view);
trtcCloud.startLocalAudio();
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);

// Set local video encoding parameters
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
:::
</dx-codeblock>

[](id:step6)
### Step 6. Sets beauty filters

1. Call [setBeautyStyle(style, beauty, white, ruddiness)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle) to enable filters.
2. Parameter description:
    -   `style`: style, which may be smooth or natural. The smooth style features more obvious skin smoothing effect and is suitable for entertainment scenarios.
        -   `TRTCBeautyStyle.TRTCBeautyStyleSmooth`: smooth, which features more obvious skin smoothing effect and is suitable for shows
        -   `TRTCBeautyStyle.TRTCBeautyStyleNature`: natural, which retains more facial details and is more natural
    -   `beauty`: strength of the beauty filter. Value range: 0-9. `0` indicates that the filter is disabled. The larger the value, the more obvious the effect.
    -   `white`: strength of the skin brightening filter. Value range: 0-9. `0` indicates that the filter is disabled. The larger the value, the more obvious the effect.
    -   `ruddiness`: strength of the rosy skin filter. Value range: 0-9. `0` indicates that the filter is disabled. The larger the value, the more obvious the effect. This parameter is unavailable on Windows currently.

```javascript
// Enable beauty filters 
trtcCloud.setBeautyStyle(TRTCBeautyStyle.TRTCBeautyStyleNature, 5, 5, 5);
```


[](id:step7)
### Step 7. Create a room and push streams

1. If `role` in [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html) is set to **`TRTCRoleType.TRTCRoleAnchor`**, the current user is in the role of an anchor.
2. Call `enterRoom( )`, specifying the `appScene` parameter, and a room whose ID is the value of the `roomId` field in `TRTCParams` will be created.
    -   `TRTCAppScene.TRTCAppSceneLIVE`: the interactive video streaming mode, which features smooth mic on/off and anchor latency below 300 ms. Up to 100,000 users can play the anchor’s video at the same time, with playback latency as low as 1,000 ms. The example in this document uses this mode.
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: the interactive audio streaming mode, which features smooth mic on/off and anchor latency below 300 ms. Up to 100,000 users can play the anchor’s audio at the same time, with playback latency as low as 1,000 ms. 
    -   For more information about `TRTCAppScene`, see [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene).
3. After the room is created, start encoding and transferring audio/video data. The SDK will return the [onEnterRoom(result)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) callback. If `result` is greater than 0, room entry succeeds, and the value indicates the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.

<dx-codeblock>
::: javascript javascript
let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
  } else {
    console.warn(`onEnterRoom: failed to enter room ${result}`);
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
:::
</dx-codeblock>

[](id:step8)
### Step 8. Enter the room as audience

1. Set the `role` field in [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html) to **`TRTCRoleType.TRTCRoleAudience`** to take the role of “audience”.
2. Call `enterRoom()` to enter the room whose ID is the value of the `roomId` field in `TRTCParams`, specifying `appScene`:
    -   `TRTCAppScene.TRTCAppSceneLIVE`: interactive video streaming
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: interactive audio streaming
3. Watch the anchor's video:
    - If you know the anchor’s `userId`, call [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) with the anchor’s `userId` passed in to play the anchor's video.
    - If you do not know the anchor’s `userId`, find the anchor’s `userId` in the [onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) callback, which you will receive after room entry, and call [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) with the anchor’s `userId` passed in to play the anchor’s video.

<dx-codeblock>
::: html html
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // Callback for room entry
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
    } else {
      console.warn(`onEnterRoom: failed to enter room ${result}`);
    }
  };
  // This callback is triggered when the anchor publishes/unpublishes streams from the camera.
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
  param.role = TRTCRoleType.TRTCRoleAudience; // Set the role to "audience"
  trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
</script>
:::
</dx-codeblock>

[](id:step9)
### Step 9. Co-anchor

1. Call [switchRole(TRTCRoleType.TRTCRoleAnchor)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole) to switch the role to “anchor” (`TRTCRoleType.TRTCRoleAnchor`).
2.  Call [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) to enable local camera preview.
3.  Call [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) to enable mic capturing.

<dx-codeblock>
::: javascript javascript
// Sample code: start co-anchoring
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

// Sample code: end co-anchoring
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview()
:::
</dx-codeblock>


[](id:step10)
### Step 10. Compete across rooms

Anchors from two rooms can compete with each other without exiting their current rooms.

1. Anchor A calls the [connectOtherRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom) API. The API uses parameters in JSON strings, so anchor A needs to pass the `roomId` and `userId` of anchor B in the format of `{"roomId": 978,"userId": "userB"}` to the API.
2. After the cross-room call is set up, anchor A will receive the [onConnectOtherRoom(userId, errCode, errMsg)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom) callback, and all users in both rooms will receive the [onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) and [onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) callbacks.
    For example, after anchor A in room "001" uses `connectOtherRoom()` to call anchor B in room “002” successfully, all users in room "001" will receive the `onUserVideoAvailable(B, true)` and `onUserAudioAvailable(B, true)` callbacks, and all users in room "002" will receive the `onUserVideoAvailable(A, true)` and `onUserAudioAvailable(A, true)` callbacks.
3. Users in both rooms can call [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) to play the video of the anchor in the other room. Audio will be played automatically.

![](https://main.qcloudimg.com/raw/bffa420102bb31dee6f76d7f08a16e4f.png)

<dx-codeblock>
::: javascript javascript
// Sample code: cross-room competition
let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`Connected to the room of anchor ${userId}`);
  } else {
    console.warn(`Failed to connect to the anchor's room: ${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
:::
</dx-codeblock>

[](id:step11)
### Step 11. Exit the room  

Call [exitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom) to exit the room. The SDK disables and releases devices such as cameras and mics during room exit. Therefore, room exit is not an instant process. It completes only after the [onExitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) callback is received.

<dx-codeblock>
::: javascript javascript
// Please wait for the `onExitRoom` callback after calling the room exit API.
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
:::
</dx-codeblock>

>! If your Electron application integrates multiple audio/video SDKs, please wait after you receive the `onExitRoom` callback to start other SDKs; otherwise the device busy error may occur.
