This document describes how to subscribe to the audio/video streams of another user (remote user) in the room, i.e., how to play a remote user’s audio/video.
![](https://qcloudimg.tencent-cloud.cn/raw/c8ae41656c97fe546b9c4b0b857b0746.png)

## Call Guide

[](id:step1)
### Step 1. Perform prerequisite steps
Import the SDK as instructed in [Electron](https://intl.cloud.tencent.com/document/product/647/35097).

[](id:step2)
### Step 2. Set the subscription mode (optional)
You can call the **setDefaultStreamRecvMode** API in `TRTCCloud` to set the subscription mode. TRTC provides two subscription modes:
- Automatic subscription: The SDK automatically plays remote users' audios. This is the default subscription mode.
- Manual subscription: The SDK doesn't automatically pull or play remote users' audios. You need to call **muteRemoteAudio(userId, false)** manually to play the audio of a remote user.
>! If you don't call `setDefaultStreamRecvMode`, the automatic subscription mode will apply. If you want to use the manual subscription mode, **make sure you call `setDefaultStreamRecvMode` before `enterRoom`**.

[](id:step3)
### Step 3. Enter a TRTC room
Make the current user enter a TRTC room as instructed in [Entering a Room](https://intl.cloud.tencent.com/document/product/647/48049). A user can subscribe to the audio/video streams of a remote user only after a successful room entry.

[](id:step4)
### Step 4. Play the audio of a remote user
You can call `muteRemoteAudio("denny", true)` to mute the remote user `denny` and then call `muteRemoteAudio("denny", false)` to unmute `denny`.

```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();

// For details, see https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio
// Mute the user “denny”
rtcCloud.muteRemoteAudio('denny', true);
// Unmute the user with ID denny
rtcCloud.muteRemoteAudio('denny', false);
```

[](id:step5)
### Step 5. Play the video of a remote user

#### 1. Start and stop playback (startRemoteView + stopRemoteView)
You can call `startRemoteView` to play the video of a remote user, but only after you pass in a view object to the SDK as the rendering control for the user's video.

The first parameter of `startRemoteView` is `userId` of the remote user, the second is the stream type of the user, and the third is the view object to be passed in. Here, the second parameter `streamType` has three valid values:
- **TRTCVideoStreamTypeBig**: The primary stream, which is usually a user's camera video.
- **TRTCVideoStreamTypeSub**: The substream, which is usually a user's screen sharing image.
- **TRTCVideoStreamTypeSmall**: A lower quality video of a user's primary stream. You can play the lower quality video of a remote user only after the user enables dual-stream mode (`enableEncSmallVideoStream`). The original and lower quality streams cannot be played at the same time.

You can call the `stopRemoteView` API to stop playing back the video of one remote user or call the `stopAllRemoteView` API to stop playing back videos of all remote users.

```javascript
// For details, see https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView

import TRTCCloud, { TRTCVideoStreamType } from 'trtc-electron-sdk';

const cameraView = document.querySelector('.user-dom');
const screenView = document.querySelector('.screen-dom');
const rtcCloud = new TRTCCloud();
// Play back the camera (primary stream) image of `denny`
rtcCloud.startRemoteView('denny', cameraView, TRTCVideoStreamType.TRTCVideoStreamTypeBig);
// Play back the screen sharing (substream) image of `denny`
rtcCloud.startRemoteView('denny', screenView, TRTCVideoStreamType.TRTCVideoStreamTypeSub);
// Play back the lower quality video of `denny` (The original and lower quality streams cannot be played back at the same time)
rtcCloud.startRemoteView('denny', cameraView, TRTCVideoStreamType.TRTCVideoStreamTypeSmall);
// Stop playing back the camera image of `denny`
rtcCloud.stopRemoteView('denny', TRTCVideoStreamType.TRTCVideoStreamTypeBig);
// Stop playing back the videos of all remote users
rtcCloud.stopAllRemoteView();
```

#### 2. Set playback parameters (`setRemoteRenderParams`)

You can use `setRemoteRenderParams` to set the video image fill mode, rotation angle, and mirror mode.
- Fill mode: You can use the fill mode or fit mode. In both modes, the original image aspect ratio is not changed. The difference is whether black bars are displayed.
- Rotation angle: You can set the rotation angle to 0, 90, 180, or 270 degrees.
- Mirror mode: Indicates whether to flip the image horizontally.

```javascript
// For details, see https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams
// Set the fill mode for the primary stream of the remote user `denny` to fill, and flip the image horizontally
import TRTCCloud, { 
  TRTCRenderParams, TRTCVideoStreamType, TRTCVideoRotation,
  TRTCVideoFillMode, TRTCVideoMirrorType
} from 'trtc-electron-sdk';

const param = new TTRTCRenderParams(
  TRTCVideoRotation.TRTCVideoRotation0,
  TRTCVideoFillMode.TRTCVideoFillMode_Fill,
  TRTCVideoMirrorType.TRTCVideoMirrorType_Enable
);
const rtcCloud = new TRTCCloud();
rtcCloud.setRemoteRenderParams('denny', TRTCVideoStreamType.TRTCVideoStreamTypeBig, param);
```

[](id:step6)
### Step 6. Get the audio/video status of a remote user in the room

[Step 4](#step4) and [step 5](#step4) showed how to use APIs to control the playback of the audio and video of a remote user. However, without the following information, you may not know what user ID to pass in when calling the APIs.
- What users are in the current room
- The camera and mic status of users in the room

To solve this problem, you need to listen for the following event callbacks from the SDK:
- **Audio status change notification (onUserAudioAvailable)**
You can listen for `onUserAudioAvailable(userId,boolean)` to be notified when a remote user turns their mic on/off.

- **Video status change notification (onUserVideoAvailable)**
You can listen for `onUserVideoAvailable(userId,boolean)` to be notified when a remote user turns their camera on/off.
You can listen for `onUserSubStreamAvailable(userId,boolean)` to be notified when a remote user enables/disables screen sharing.

- **User room entry/exit notification (onRemoteUserEnter/LeaveRoom)**
When a remote user enters the current room, you can get the user’s ID from `onRemoteUserEnterRoom(userId)`. When a remote user exits the current room, you can get the user’s ID and the reason for their exit from `onRemoteUserLeaveRoom(userId, reason)`.
>! More accurately, `onRemoteUserEnter/LeaveRoom` only notifies you about the room entry/exit of anchors. This prevents frequent notifications when there are a large audience in the room.

With the event callbacks above, you can know the users in the room and whether they have turned on their cameras and mics. In the sample code below, `mCameraUserList`, `mMicrophoneUserList`, and `mUserList` are used to maintain the following information:
- What users (anchors) are in the room
- Which users have turned on their cameras
- Which users have turned on their mics

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let openCameraUserList = [];
let openMicUserList = [];
let roomUserList = [];

function onUserVideoAvailable(userId, available) {
  if (available === 1) {
    openCameraUserList.push(userId);
  } else {
    openCameraUserList = openCameraUserList.filter((item) => item !== userId);
  }
}

function onUserAudioAvailable(userId, available) {
  if (available === 1) {
    openMicUserList.push(userId);
  } else {
    openMicUserList = openMicUserList.filter((item) => item !== userId);
  }
}

function onRemoteUserEnterRoom(userId) {
  roomUserList.push(userId);
}

function onRemoteUserLeaveRoom(userId, reason) {
  roomUserList = roomUserList.filter((item) => item !== userId);
}

const rtcCloud = new TRTCCloud();
rtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);
rtcCloud.on('onUserAudioAvailable', onUserAudioAvailable);
rtcCloud.on('onRemoteUserEnterRoom', onRemoteUserEnterRoom);
rtcCloud.on('onRemoteUserLeaveRoom', onRemoteUserLeaveRoom);
```

## Advanced Guide

### What are the differences between different muting methods?
There are three muting methods which work in completely different ways:
- **Method 1. The player stops subscribing to the audio stream**
To stop playing back the audio of the remote user `denny`, you can call `muteRemoteAudio("denny", true)`, and the SDK will stop pulling the audio data of `denny`. In this mode, less traffic is used. However, it will be slow to resume audio playback because the SDK needs to restart the audio data pull process.

- **Method 2. Adjust the playback volume level to zero**
If you want to mute a user more quickly, you can call `setRemoteAudioVolume("denny", 0)`, which sets the playback volume of the remote user `denny` to zero. Because this API doesn't involve network operations, it takes effect very quickly.

- **Method 3. The remote user turns off the mic**
All operations described in this document are performed in the player and take effect only for the local user. For example, if you call `muteRemoteAudio("denny", true)` to mute the remote user `denny`, other users in the room can still hear `denny`.
To completely disable the audio of `denny`, you need to change the way their audio is published. For more information, see [Publishing Audio/Video Streams](https://intl.cloud.tencent.com/document/product/647/48050).
