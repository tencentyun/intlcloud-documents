This document describes how an anchor publishes audio/video streams. "Publishing" refers to turning on the mic and camera to make the audio heard and video seen by other users in the room.

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)
## Call Guide

[](id:step1)
### Step 1. Perform prerequisite steps
Import the SDK as instructed in [Electron](https://intl.cloud.tencent.com/document/product/647/35097).

[](id:step2)
### Step 2. Enable camera preview
You can call the **startLocalPreview** API to enable camera preview. The SDK will request camera permission from the system. Camera images can be captured only after the permission is granted.

You can call the **setLocalRenderParams** API to set the rendering parameters of local preview. Image jitters may occur if preview parameters are set after preview is enabled, so we recommend you call this API before enabling preview.

```javascript
// Set the rendering parameters of local preview: Flip the video horizontally and use the fill mode
import TRTCCloud, { 
	TRTCRenderParams, TRTCVideoRotation,
	TRTCVideoFillMode, TRTCVideoMirrorType
} from 'trtc-electron-sdk';

const param = new TRTCRenderParams(
	TRTCVideoRotation.TRTCVideoRotation0,
	TRTCVideoFillMode.TRTCVideoFillMode_Fill,
	TRTCVideoMirrorType.TRTCVideoMirrorType_Auto
);
const rtcCloud = new TRTCCloud();
rtcCloud.setLocalRenderParams(param);
const cameraVideoDom = document.querySelector('.camera-dom');
rtcCloud.startLocalPreview(cameraVideoDom);
```

[](id:step3)
### Step 3. Enable mic capture
You can call **startLocalAudio** to start mic capture. When calling this API, you need to specify `quality`. A higher quality isn't necessarily better. We recommend you set this parameter based on the application scenario.

- **SPEECH**
In this mode, the SDK audio module is dedicated to capturing audio signals and filtering environmental noise as much as possible. In addition, the audio data in this mode has the highest immunity to a poor network quality. Therefore, it is especially suitable for scenarios highlighting audio communication, such as video calls and online meetings.
- **MUSIC**
In this mode, the SDK uses a high bandwidth for audio processing and uses the stereo mode to maximize the capturing quality while minimizing the role of the DSP module. It guarantees audio quality and is therefore suitable for music streaming scenarios, especially when an anchor uses a high-end sound card.
- **DEFAULT**
In this mode, the SDK uses an algorithm to recognize the current environment and selects the processing mode accordingly. However, the recognition algorithm is not always accurate, so if your product has a clear positioning (for example, an audio chat app or a music streaming app), we recommend you set the parameter to `SPEECH` or `MUSIC`.

```javascript
import { TRTCAudioQuality } from 'trtc-electron-sdk';
// Enable mic capture and set `quality` to `SPEECH` (strong in noise suppression and adapts well to poor network conditions)
rtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualitySpeech);

// Enable mic capture and set `quality` to `MUSIC` (high fidelity, minimum audio quality loss, recommended if a high-end sound card is used)
rtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualityMusic);
```

[](id:step4)
### Step 4. Enter a TRTC room
Make the current user enter a TRTC room as instructed in [Entering a Room](https://intl.cloud.tencent.com/document/product/647/48049). The SDK will start publishing the audio of the local user to remote users upon successful room entry.

>! You can enable camera preview and mic capture after room entry (`enterRoom`), but in live streaming scenarios, you need to leave a certain amount of time for the anchor to test the mic and adjust the beauty filters; therefore, it is more common to turn on the camera and mic first and then enter a room.

```javascript
import { TRTCParams, TRTCRoleType, TRTCAppScene } from 'trtc-electron-sdk';

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
const param = new TRTCParams();
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.userId = "denny";       // Replace with your own user ID  
params.roomId = 123321;        // Replace with your own room number
params.userSig = "xxx";        // Replace with your own userSig
params.role = TRTCRoleType.TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
rtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```

