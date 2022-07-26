This document describes how to enter a TRTC room. Only after entering an audio/video room can a user subscribe to the audio/video streams of other users in the room or publish his or her own audio/video streams.
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

## Call Guide

[](id:step1)

### Step 1. Import the SDK
Import the SDK as instructed in [Electron](https://intl.cloud.tencent.com/document/product/647/35097).

[](id:step2)
### Step 2. Create an SDK instance

```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
```

[](id:step3)
### Step 3. Listen for SDK events
You can use callback APIs to listen for errors, warnings, traffic statistics, network quality, as well as various audio/video events of the SDK.

```javascript
function onError(errCode, errMsg) {
  // For information on the error codes, see https://intl.cloud.tencent.com/document/product/647/35124#error-codes
  console.log(errCode, errMsg);
}

function onWarning(warningCode, warningMsg) {
  // For information on the warning codes, see https://intl.cloud.tencent.com/document/product/647/35124#warning-codes
  console.log(warningCode, warningMsg);
}

rtcCloud.on('onError', onError);
rtcCloud.on('onWarning', onWarning);
```

[](id:step4)
### Step 4. Assemble the room entry parameter `TRTCParams`
When calling the `enterRoom` API, you need to enter two key parameters: `TRTCParams` and `TRTCAppScene`.

#### Parameter 1: TRTCAppScene
This parameter is used to specify whether your application scenario is **live streaming** or **real-time call**.
- For **real-time calls**, set the parameter to `TRTCAppSceneVideoCall` (video call) or `TRTCAppSceneAudioCall` (audio call). This mode is suitable for one-to-one audio/video calls or online meetings for up to 300 attendees.
- For **live streaming**, set the parameter to `TRTCAppSceneLIVE` (video live streaming) or `TRTCAppSceneVoiceChatRoom` (audio live streaming). This mode is suitable for live streaming to up to 100,000 users. Make sure you specify the **role** field (valid values: **anchor**, **audience**) in `TRTCParams` if you use this mode.

#### Parameter 2: TRTCParams
`TRTCParams` consists of many fields; however, you usually only need to pay attention to how to set the following fields:

| Parameter | Description | Remarks | Data Type | Sample Value |
|---------|---------|---------|---------|---------|
| SDKAppID | Application ID | You can view your application ID in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>. If you don’t have an application yet, click **Create application** to create one.| Number |1400000123 |
| userId | User ID | It can contain only letters, digits, underscores, and hyphens. In TRTC, a user cannot use the same user ID to enter the same room on two different devices at the same time. | String | `denny` or `123321`|
| userSig | The authentication ticket needed to enter a room | `userSig` is calculated based on `userId` and `SDKAppID`. For the calculation method, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). | String |eJyrVareCeYrSy1SslI... |
| roomId | Room ID | Numeric room ID. If you want to use string-type room IDs, specify **strRoomId**. Do not use `strRoomId` and `roomId` at the same time. | Number | 29834 |
| strRoomId | Room ID | String-type room ID. Do not use `strRoomId` and `roomId` at the same time. `"123"` and `123` are considered different rooms by the TRTC backend. | String | 29834 |
| role | Role | There are two roles: anchor and audience. This field is required only when `TRTCAppScene` is set to the `TRTCAppSceneLIVE` or `TRTCAppSceneVoiceChatRoom` live streaming scenarios. | Enumeration | `TRTCRoleAnchor` or `TRTCRoleAudience`   |

>!
>- In TRTC, a user cannot use the same `userId` to enter the same room on two different devices at the same time; otherwise, there will be a conflict.
>- The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.

[](id:step5)
### Step 5. Enter the room (`enterRoom`)
After preparing `TRTCAppScene` and `TRTCParams` as described in [step 4](#step4), you can call the `enterRoom` API to enter the room.

```javascript
import { TRTCParams, TRTCRoleType, TRTCAppScene } from 'trtc-electron-sdk';

const param = new TRTCParams();
param.sdkAppId = 1400000123;
param.userId = "denny";  
param.roomId = 123321;
param.userSig = "xxx";
param.role = TRTCRoleType.TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
rtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```

**Callbacks:**
- If room entry succeeds, the SDK will call back the `onEnterRoom(result)` event, and the value of `result` will be greater than 0, indicating the time in milliseconds taken to enter the room.
- If room entry fails, the SDK will also call back the `onEnterRoom(result)` event, but the value of `result` will be a negative number, indicating the error code for the room entry failure.

```javascript
function onEnterRoom(result) {
  // For details about `onEnterRoom`, see https://web.sdk.qcloud.com/trtc/electron/doc/en/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom
  if (result > 0) {
    console.log('Enter room succeed');
  } else {
    // For room entry error codes, see https://intl.cloud.tencent.com/document/product/647/35124
    console.log('Enter room failed');
  }
  
}

rtcCloud.on('onEnterRoom', onEnterRoom);
```
