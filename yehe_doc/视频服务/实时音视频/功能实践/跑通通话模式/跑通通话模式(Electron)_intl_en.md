## Use Cases

TRTC supports four room entry modes. Video call (`VideoCall`) and audio call (`VoiceCall`) are the call modes, and interactive video streaming (`Live`) and interactive audio streaming (`VoiceChatRoom`) are the [live streaming modes](https://intl.cloud.tencent.com/document/product/647/36070).
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

1. Create a `trtc-electron-sdk` instance:
```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```
2. Listen for the `onError` event:
<dx-codeblock>
::: javascript javascript
// Error events must be listened for and captured, and error messages should be sent to users.
let onError = function(err) {
    console.error(err);
};
trtcCloud.on('onError',onError);
:::
</dx-codeblock>

[](id:step4)
### Step 4. Assemble the room entry parameter `TRTCParams`

When calling the [enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) API, you need to pass in a key parameter [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html), which includes the following required fields:

| Parameter     | Type   | Description                                                         | Example                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | Number | Application ID, which can be found in **Application Management** > **Application Info** in the [console](https://console.cloud.tencent.com/trtc/app) | 1400000123             |
| userId | String | Only letters (a-z and A-Z), digits (0-9), underscores, and hyphens are allowed. | test_user_001 |
| userSig | String | `userSig` is calculated based on `userId`. For the calculation method, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | eJyrVareCeYrSy1SslI... |
| roomId | Number | String-type room IDs tend to slow down the room entry process and are therefore not supported by the SDK by default. If you need to use string-type room IDs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category). | 29834 |

<dx-codeblock>
::: javascript javascript
import {
  ## TRTCParams
  ## TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
:::
</dx-codeblock>


>! 
>- In TRTC, users with the same `userId` cannot be in the same room at the same time as it will cause a conflict.
>
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

[](id:step5)
### Step 5. Create and enter a room

1. Call [enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) to enter the room specified by the `roomId` field in `TRTCParams`. If the room does not exist, the SDK will create a room whose number is the value of `roomId`.
2. Set the `appScene` parameter according to your actual application scenario. Inappropriate `appScene` values may increase stutter or reduce video clarity.
   - For video calls, set it to `TRTCAppScene.TRTCAppSceneVideoCall`.
   - For audio calls, set it to `TRTCAppScene.TRTCAppSceneAudioCall`.
>? For more information about `TRTCAppScene`, see [TRTCAppScene ](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene).
3. You will receive the [onEnterRoom(result)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) callback. If `result` is greater than 0, room entry succeeds, and the value of `result` indicates the time (ms) room entry takes; if `result` is less than 0, room entry fails, and the value is the error code for the failure.

<dx-codeblock>
::: javascript javascript
import TRTCCloud from 'trtc-electron-sdk';
import { TRTCParams, TRTCAppScene } from "trtc-electron-sdk/liteav/trtc_define";
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();

let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, room entry succeeded and took ${result} seconds`);
  } else {
    console.warn(`onEnterRoom: failed to enter room ${result}`);
  }
};

// Subscribe to the room entry event
trtcCloud.on('onEnterRoom', onEnterRoom);

// Enter room. If the room does not exist, the TRTC will create one.
let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneVideoCall);
:::
</dx-codeblock>


[](id:step6)
### Step 6. Subscribe to remote audio/video streams

The SDK supports two subscription modes: automatic subscription and manual subscription. The former allows instant streaming and is suitable for calls with a small number of participants, while the latter reduces bandwidth usage and is suitable for conferences with a large number of participants.

#### Automatic subscription (recommended)

After room entry, the SDK will automatically pull audio streams from other users in the room. This enables instant streaming.

1. If other users in the room are sending audio data, you will receive the [onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) notification, and the SDK will play their audio automatically.
2. You can call [muteRemoteAudio(userId, true)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio) to mute a specified user (`userId`), or [muteAllRemoteAudio(true)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio) to mute all remote users. The SDK will stop pulling the audio data of the user(s).
3. If a remote user in the room is sending video data, you will receive the [onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) notification, but since the SDK has not received instructions on how to display the video, it will not process the video data. You need to call [startRemoteView(userId, view, streamType)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) to associate the remote user’s video data with `view`.
4. You can call [setRemoteViewFillMode(userId, mode)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewFillMode) to set the display mode of a remote video.
    -`TRTCVideoFillMode.TRTCVideoFillMode_Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
    -`TRTCVideoFillMode.TRTCVideoFillMode_Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
5. You can call [stopRemoteView(userId)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView) to block the video of a specified `userId` or [stopAllRemoteView()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView) to block the video of all remote users. The SDK will stop pulling the video data of the user(s).

<dx-codeblock>
::: html html
<div id="video-container"></div>

<script>
  import TRTCCloud from 'trtc-electron-sdk';
  const trtcCloud = new TRTCCloud();
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;

  /**
   * Whether camera video is enabled
   * @param {number} uid - user ID
   * @param {boolean} available - Whether video is enabled
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

  // Sample code: subscribe to or unsubscribe from the video image of a remote user based on the notification received
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

</script>
:::
</dx-codeblock>

>? If you do not call `startRemoteView()` to subscribe to the video stream immediately after receiving the `onUserVideoAvailable()` callback, the SDK will stop pulling the remote video within 5 seconds.

#### Manual subscription

You can call [setDefaultStreamRecvMode(autoRecvAudio, autoRecvVideo)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode) to switch the SDK to the manual subscription mode. In this mode, the SDK will not pull the audio/video data of other users in the room automatically. You have to start the process manually via APIs.

1. **Before you enter a room**, call the [setDefaultStreamRecvMode(false, false)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode) API to switch the SDK to the manual subscription mode.
2. If other users in the room are sending audio data, you will receive the [onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) notification, and you need to call [muteRemoteAudio(userId, false)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio) to manually subscribe to the users’ audio. The SDK will decode and play the audio data received.
3. If a remote user in the room is sending video data, you will receive the [onUserVideoAvailable(userId, available)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) notification, and you need to call [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) to manually subscribe to the user's video data. The SDK will decode and play the video data received.


[](id:step7)
### Step 7. Publish the local stream

1. Call [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) to enable mic capturing and encode and publish the audio captured.
2. Call [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) to enable camera capturing and encode and publish the video captured.
3. Call [setLocalViewFillMode()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode) to set the display mode of the local video:
   -`TRTCVideoFillMode.TRTCVideoFillMode_Fill`: aspect fill. The image may be scaled up and cropped, but there are no black bars.
   -`TRTCVideoFillMode.TRTCVideoFillMode_Fit`: aspect fit. The image may be scaled down to ensure that it’s displayed in its entirety, and there may be black bars.
4. Call [setVideoEncoderParam()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) to set the encoding parameters for the local video, which determine the [quality of your video](https://intl.cloud.tencent.com/document/product/647/35153) seen by other users in the room.

<dx-codeblock>
::: javascript javascript
// Sample code: publish the local audio/video stream
trtcCloud.startLocalPreview(view);
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);
trtcCloud.startLocalAudio();
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


>! The SDK uses the default camera and mic. You can call [setCurrentCameraDevice()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice) and [setCurrentMicDevice()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDevice) to switch to a different camera and mic.


[](id:step8)
### Step 8. Exit the room

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
