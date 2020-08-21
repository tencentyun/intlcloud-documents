## Use Cases

TRTC supports four room entry modes, among which video call (VideoCall) and audio call (VoiceCall) are classified as call mode, while interactive video live streaming (Live) and interactive audio live streaming (VoiceChatRoom) are classified as [live streaming mode](https://intl.cloud.tencent.com/document/product/647/36070).
In call mode, there can be a maximum of 300 members in a single TRTC room, and up to 50 of them can speak at the same time. This service is suitable for various scenarios such as one-to-one video call, video conferencing with up to 300 attendees, online medical diagnosis, video interview, video customer service, and online werewolf.

## How It Works

The TRTC service consists of two types of server nodes: access servers and proxy servers:

-   **Access server**
    Backed by the highest-quality lines and high-performance servers, this type of nodes is ideal for processing end-to-end low-latency co-anchoring calls, but the fees per unit time are relatively high.
-   **Proxy server**
    With general lines and average-performance servers, this type of nodes is suitable for processing high-concurrence playback of pulled streams, and the fees per unit time are low.

In call mode, all users in the TRTC room will be assigned to access servers, which means that each user is an "anchor" and can speak at any time (up to 50 concurrent upstreams are supported), so it is suitable for scenarios such as online conferencing, but the number of members in a single room is limited to 300.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## Sample Code

You can log in to [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Electron) to get the sample code related to this document.

## Directions

<span id="step1"></span>
### Step 1. Try to run the official SimpleDemo

You are recommended to read [Run SimpleDemo (Electron)](https://intl.cloud.tencent.com/document/product/647/35089) first and then follow the instructions to run the official SimpleDemo.

If the SimpleDemo can run properly, it means that you have mastered the method of installing Electron in your project.

If the SimpleDemo cannot run, the problem is likely to be related to Electron download and installation. In this case, you can refer to the [Electron FAQs](https://cloud.tencent.com/developer/article/1616668) or Electron's official [installation guide](https://www.electronjs.org/docs/tutorial/installation) for assistance.

<span id="step2"></span>
### Step 2. Integrate trtc-electron-sdk into your project

If [step 1](#step1) is executed normally and the result is as expected, it means that you have mastered the method of installing the Electron environment.

You can conduct secondary development on the official demo, and the initial stage of your project will go smoothly.

You can also run the following command to install `trtc-electron-sdk` into your existing project:

```bash
npm install trtc-electron-sdk --save
```

<span id="step3"></span>
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
};
trtcCloud.on('onError',onError);
```

<span id="step4"></span>
### Step 4. Assemble the room entry parameter `TRTCParams`

When calling the [enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) API, you need to enter a key parameter [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html), which includes the following required fields:

| Parameter | Type | Description | Example |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | Numeric | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app). | 1400000123             |
| userId | String | It can contain only letters (a–z and A–Z), digits (0–9), underscores, and hyphens. | test_user_001 |
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
```

>! In TRTC, users with the same `userId` cannot be in the same room at the same time; otherwise, there will be a conflict.

<span id="step5"></span>
### Step 5. Create and enter a room

1. Call [enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) to enter the audio/video room specified by `roomId` in the `TRTCParams` parameter. If the room does not exist, the SDK will automatically create it with the `roomId` value as the room number.

2. Please set the appropriate `appScene` parameter according to the actual application scenario. An incorrect selection may lead to higher lagging rate or lower video definition than expected.

   - For video calls, please set `TRTCAppScene.TRTCAppSceneVideoCall`.
   - For audio calls, please set `TRTCAppScene.TRTCAppSceneAudioCall`.

   For more information on `TRTCAppScene`, please see [TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene).

3. After successful room entry, the SDK will call back the [onEnterRoom(result)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) event. If `result` is greater than 0, the room entry succeeds, and the specific value indicates the time in milliseconds (ms) used for entering the room; if `result` is less than 0, the room entry fails, and the specific value indicates the error code of the failure.

```javascript
import TRTCCloud from 'trtc-electron-sdk';
import { TRTCParams, TRTCAppScene } from "trtc-electron-sdk/liteav/trtc_define";
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();

let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
  } else {
    console.warn(`onEnterRoom: failed to enter the room ${result}`);
  }
};

// Subscribe to the event of successful room entry
trtcCloud.on('onEnterRoom', onEnterRoom);

// Enter room. If the room does not exist, the TRTC backend will automatically create a room
let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneVideoCall);
```

<span id="step6"></span>
### Step 6. Subscribe to remote audio/video streams

The SDK supports two subscription modes: automatic subscription and manual subscription. The former focuses on speeding up instant broadcasting and is suitable for call scenarios with a small number of participants, while the latter focuses on reducing traffic usage and is suitable for conference scenarios with a large number of participants.

#### Automatic subscription (recommended)

After room entry, the SDK will automatically receive audio streams from other users in the room to achieve the best "instant broadcasting" effect:

1. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) event notification, and the SDK will automatically play back the audio of the remote user.

2. You can block the audio data of a specified `userId` through [muteRemoteAudio(userId,  true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio) or all remote users through [muteAllRemoteAudio(true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteAudio). After that, the SDK will no longer pull the audio data of the corresponding remote users.

3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) event notification; however, since the SDK has not received instructions on how to display the video data at this time, video data will not be processed automatically. You need to associate the video data of the remote user with the display `view` by calling the [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) method.

4. You can specify the display mode of the local video image through [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode):
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
  
5. You can block the video data of a specified `userId` through [stopRemoteView(userId)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteView) or all remote users through [stopAllRemoteView()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllRemoteView). After that, the SDK will no longer pull the video data of the corresponding remote users.

```html
<div id="video-container"></div>

<script>
  import TRTCCloud from 'trtc-electron-sdk';
  const trtcCloud = new TRTCCloud();
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;

  /**
   * Whether camera is enabled for video
   * @param {number} uid - user ID
   * @param {boolean} available - Whether image is enabled
   **/
  let onUserVideoAvailable = function (uid, available) {
    console.log(`onUserVideoAvailable: uid: ${uid}, available: ${available}`);
    if (available === 1) {
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (!view) {
        view = document.createElement('div');
        view.id = id;
        videoContainer.appendChild(view);
      }
      trtcCloud.startRemoteView(uid, view);
      trtcCloud.setRemoteViewFillMode(uid, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    } else {
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (view) {
        videoContainer.removeChild(view);
      }
    }
  };

  // Sample code: subscribe to (or unsubscribe from) the video image of the remote user based on the notification
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

</script>
```

>? If you do not call `startRemoteView()` to subscribe to the video stream immediately after receiving the `onUserVideoAvailable()` event callback, the SDK will stop receiving remote video data within 5 seconds.

#### Manual subscription

You can specify the SDK to enter the manual subscription mode through the [setDefaultStreamRecvMode(autoRecvAudio, autoRecvVideo)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setDefaultStreamRecvMode) API. In this mode, the SDK will not automatically receive audio/video data of other users in the room; instead, you need to manually trigger the receipt through API functions.

1. **Before room entry**, call the [setDefaultStreamRecvMode(false, false)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setDefaultStreamRecvMode) API to set the SDK to manual subscription mode.
2. When another user in the room is upstreaming audio data, you will receive the [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) event notification. At this time, you need to manually subscribe to the user's audio data by calling [muteRemoteAudio(userId, false)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio), and the SDK will decode and play back it after receiving it.
3. When another user in the room is upstreaming video data, you will receive the [onUserVideoAvailable(userId, available)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) event notification. At this time, you need to manually subscribe to the user's video data by calling [startRemoteView(userId,  view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView), and the SDK will decode and play back it after receiving it.


<span id="step7"></span>
### Step 7. Publish the local audio/video stream

1. Call [startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) to enable local mic capturing and encode and send the captured audio.
2. Call [startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) to enable local camera capturing and encode and send the captured video.
3. Call [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode) to set the display mode of the local video image:
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fill` indicates the fill mode where the image may be scaled up proportionally or cropped, but no black bars will exist.
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fit` indicates the fit mode where the image may be scaled down proportionally to fit the screen, but black bars may exist.
4. Call [setVideoEncoderParam()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) to set the encoding parameter of the local video, which determines the [image quality](https://intl.cloud.tencent.com/document/product/647/35153) of the video watched by other users in the room.

```javascript
// Sample code: send local audio/video streams
trtcCloud.startLocalPreview(view);
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);
trtcCloud.startLocalAudio();
// Set local video encoding parameter
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
```

>! The SDK will use the system-default camera and mic by default. You can call [setCurrentCameraDevice()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentCameraDevice) and [setCurrentMicDevice()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDevice) to select another camera and mic.


<span id="step8"></span>
### Step 8. Exit the current room

Call the [exitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) method to exit the room. The SDK needs to disable and release hardware devices such as the camera and mic during room exit. Therefore, room exit is not completed as soon as the method is called. Only after the [onExitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) callback is received can the room exit be considered completed.

```javascript
// Please wait for the `onExitRoom` event callback after calling the room exit method
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
```

>! If multiple audio/video SDKs are integrated into your Electron program, please enable other SDKs only after receiving the `onExitRoom` callback; otherwise, hardware occupancy issues may occur.
