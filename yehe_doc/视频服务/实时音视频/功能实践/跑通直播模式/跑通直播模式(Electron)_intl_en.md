## Use Cases

TRTC supports four room entry modes, among which video call (`VideoCall`) and audio call (`VoiceCall`) are the [call modes](https://intl.cloud.tencent.com/document/product/647/36069), and interactive video live streaming (`Live`) and interactive audio live streaming (`VoiceChatRoom`) are the live streaming modes.
The live streaming modes allow a maximum of 100,000 concurrent users in each room with smooth mic connection/disconnection. Co-anchoring latency is kept below 300 ms and watch latency below 1,000 ms. The live streaming modes are suitable for use cases such as low-latency interactive live streaming, interactive classrooms for up to 100,000 participants, video dating, online education, remote training, and mega conferences.

## How It Works

TRTC services use two types of server nodes: access servers and proxy servers.

- **Access server**
    This type of nodes use high-quality lines and high-performance servers and are good at processing end-to-end low-latency co-anchoring calls, but the unit cost is relatively high.
- **Proxy server**
    This type of servers use mediocre lines and average-performance servers and are good at processing high-concurrency stream pulling and playback. The unit cost is relatively low.

In the call modes, all users in a TRTC room are assigned to access servers and are in the role of an anchor. This means the users can speak to each other at any point in the call (up to 30 users can send upstream data at the same time). The modes are suitable for use cases such as online conferencing, but the number of users in each room is capped at 300.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code

You can obtain the sample code used in this document at [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron).

## Directions

<span id="step1"></span>

### Step 1. Run the official SimpleDemo.

We recommend that you read [Demo Quick Start > Electron](https://intl.cloud.tencent.com/document/product/647/35089) first and follow the instructions to run the official SimpleDemo.
If you run SimpleDemo successfully, it means that you have mastered the method of installing Electron in your project.
If not, there may be a problem in the download or installation process. Try troubleshooting the problem by following the instructions in Electron's [installation document](https://www.electronjs.org/docs/tutorial/installation).

<span id="step2"></span>

### Step 2. Integrate `trtc-electron-sdk` into your project.

If you can [run SimpleDemo](#step1) successfully, it means that you have mastered the method of preparing the Electron environment.

- You can develop your project based on the demo we provide to get started quickly.
- You can also run the following command to install `trtc-electron-sdk` in your project.
```bash
npm install trtc-electron-sdk --save
```

<span id="step3"></span>
### Step 3. Initialize an SDK instance and configure event callbacks.

Create a `trtc-electron-sdk` instance:

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

Subscribe to the `onError` event:

```javascript
// Error events must be listened for and captured, and error messages should be sent to users.
let onError = function(err) {
  console.error(err);
}
trtcCloud.on('onError',onError);
```

<span id="step4"></span>
### Step 4. Set the room entry parameter `TRTCParams`.

When calling the [enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) API, you need to set a key parameter [`TRTCParams`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html), which includes the following required fields:

| Parameter     | Type   | Description                                                         | Example                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | Numeric | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app) | 1400000123             |
| userId | String | Only letters (a-z and A-Z), digits (0-9), underscores, and hyphens are allowed. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Numeric | By default, TRTC does not support `roomId` in strings as it will slow down the room entry process. If you need to use string-type `roomId`, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). | 29834  |

```
import(
  ## TRTCParams
  ## TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
param.role = TRTCRoleType.TRTCRoleAnchor; // Set the role to "anchor".
```

>! In TRTC, users with the same `userId` cannot be in the same room at the same time as it will cause a conflict.

<span id="step5"></span>

### Step 5. Enables camera preview and mic capture as an anchor.
1.  Call [`startLocalPreview()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) as an anchor to enable local camera preview. The SDK will ask for camera access from the system.
2. Call `setLocalViewFillMode()` as an anchor to set the display mode of the local video image.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` is the fill mode. The image may be scaled up proportionally or cropped, but there are no black bars.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` is the fit mode. The image may be scaled down proportionally to fit the screen, but there may be black bars.
3. Call [`setVideoEncoderParam()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) as an anchor to set the encoding parameters of the local video, which determine the [quality of the anchor’s video image](https://intl.cloud.tencent.com/document/product/647/35153) seen by other users in the room.
4.  Call [`startLocalAudio()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) as an anchor to enable the mic. The SDK will ask for mic access from the system.


```
// Sample code: send local audio/video streams
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
```

<span id="step6"></span>

### Step 6. Sets beauty filters as an anchor.

1. Call [`setBeautyStyle(style, beauty, white, ruddiness)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle) as an anchor to enable beauty filters.
2. Parameter description:
    -   `style`: beauty filter style, which may be smooth or natural. The smooth style features more obvious skin smoothing effect and is suitable for entertainment scenarios.
        -   `TRTCBeautyStyle.TRTCBeautyStyleSmooth`: smooth, which features more obvious skin smoothing effect and is suitable for shows
        -   `TRTCBeautyStyle.TRTCBeautyStyleNature`: natural, which retains more facial details and is more natural
    -   beauty: intensity of the skin smoothing filter; valid value range: 0-9; 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
    -   white: intensity of the skin brightening filter; valid value range: 0-9; 0 indicates that the filter is disabled. The larger the value, the higher the intensity.
    -   ruddiness: intensity of the rosy complexion filter; valid value range: 0-9; 0 indicates that the filter is disabled. The larger the value, the higher the intensity. This parameter is not enabled for Windows for the time being.

```javascript
// Enable beauty filters. 
trtcCloud.setBeautyStyle(TRTCBeautyStyle.TRTCBeautyStyleNature, 5, 5, 5);
```


<span id="step7"></span>
### Step 7. Create a room and start pushing streams as an anchor.

1. If `role` in [`TRTCParams`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) is set to **`TRTCRoleType.TRTCRoleAnchor`**, the current user role is an anchor.
2. Call `enterRoom( )` as an anchor to create an audio/video room whose ID is the value of `roomId` in `TRTCParams` and set the `appScene` parameter:
    -   `TRTCAppScene.TRTCAppSceneLIVE`: interactive video live streaming, with smooth mic connection/disconnection and anchor latency below 300 ms. Up to 100,000 users can play the video of the anchor at the same time with playback latency as low as 1,000 ms. The example in this document uses this mode.
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: interactive audio live streaming, with smooth mic connection/disconnection and anchor latency below 300 ms. Up to 100,000 users can play the video of the anchor at the same time with playback latency as low as 1,000 ms. 
    -   For more information about `TRTCAppScene`, see [TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene).
3. After an anchor creates a room successfully, the SDK will start encoding and uploading the video and audio data of the anchor and call back the [`onEnterRoom(result)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) event. If `result` is greater than 0, the room entry is successful, and the value indicates the time (in milliseconds) the room entry takes; if `result` is less than 0, the room entry fails, and the value is the error code of the failure.

```
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

<span id="step8"></span>
### Step 8. Enter a room as a viewer to watch live streams.

1. If `role` in [`TRTCParams`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) is set to **`TRTCRoleType.TRTCRoleAudience`**, the current user role is a viewer.
2. Call `enterRoom()` as a viewer to enter an audio/video room whose ID is the value of `roomId` in `TRTCParams` and set the `appScene` parameter:
    -   `TRTCAppScene.TRTCAppSceneLIVE`: interactive video live streaming
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: interactive audio live streaming
3. Watch the anchor's video:
    - If a viewer knows the `userId` of the anchor of a room, after entering the room, the viewer can call [`startRemoteView(userId, view)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) to display the anchor's video image.
    - Viewers receive the [`onUserVideoAvailable()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) callback after room entry. A viewer not knowing the `userId` of the anchor can obtain the information from the callback and then call [`startRemoteView(userId, view)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) to display the anchor's video image.

```
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // Room entry callback, which is triggered upon successful room entry
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
    } else {
      console.warn(`onEnterRoom: failed to enter the room ${result}`);
    }
  };
  // This callback is triggered when the anchor enables/disables stream pushing by the camera.
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
  param.role = TRTCRoleType.TRTCRoleAudience; // Set the role to "viewer".
  trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
</script>
```

<span id="step9"></span>
### Step 9. Co-anchor.

1. Call [`switchRole(TRTCRoleType.TRTCRoleAnchor)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole) to switch from a viewer to an anchor (`TRTCRoleType.TRTCRoleAnchor`).
2.  Call [`startLocalPreview()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) to enable local camera preview.
3.  Call [`startLocalAudio()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) to enable audio capture by the mic.

```
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

// Sample code: the viewer disables the mic.
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview()
```


<span id="step10"></span>
### Step 10. Co-anchor across rooms.

In TRTC, anchors from two rooms can use the "cross-room call" feature to compete with each other without exiting their current rooms.

1. Anchor A calls the [`connectOtherRoom()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom) API. The API uses parameters in JSON strings, so anchor A needs to pass the `roomId` and `userId` of anchor B in the format of `{"roomId": 978,"userId": "userB"}` to the API function.
2. After co-anchoring is enabled successfully, anchor A will receive the [`onConnectOtherRoom(userId, errCode, errMsg)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom) callback, and all users in both rooms will receive the [`onUserVideoAvailable()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) and [`onUserAudioAvailable()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) callbacks.
    For example, after anchor A in room "001" uses `connectOtherRoom()` to call anchor B in room “002” successfully all users in room "001" will receive the `onUserVideoAvailable(B, true)` and `onUserAudioAvailable(B, true)` callbacks of anchor B, and all users in room "002" will receive the `onUserVideoAvailable(A, true)` and `onUserAudioAvailable(A, true)` callbacks of anchor A.
3. Users in both rooms can call [`startRemoteView(userId, view)`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) to display the video image of the anchor in the other room. Audio will be played automatically.

```
// Sample code: cross-room co-anchoring
let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`Successfully connected to the room of anchor ${userId}`);
  } else {
    console.warn(`Failed to connect to the anchor's room: ${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
```

<span id="step11"></span>
### Step 11. Exit the room.  

Call the [`exitRoom()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) method to exit the room. The SDK needs to disable and release hardware such as the camera and mic during room exit, so the process may take a while. Room exit is completed only after the [`onExitRoom()`](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) callback is received.

```
// Please wait for the `onExitRoom` callback after calling the room exit method.
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
```

>! If your Electron application integrates multiple audio/video SDKs, please wait till you receive the `onExitRoom` callback to start other SDKs; otherwise the “device busy” error may occur.
