This document describes how to actively exit the current TRTC room and in which cases will a user be forced to exit a room.
![](https://qcloudimg.tencent-cloud.cn/raw/ea39f08a98dc41195ae63a6ecae803b8.png)

## Call Guide

[](id:step1)
### Step 1. Perform prerequisite steps

1. Import the SDK and configure the application permissions as instructed in [Electron](https://intl.cloud.tencent.com/document/product/647/35097).
2. Implement the room entry process as instructed in [Electron](https://cloud.tencent.com/document/product/647/74635).

[](id:step2)
### Step 2. Actively exit the current room
Call the [exitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#exitRoom) API to exit the current room. The SDK uses the `onExitRoom(int reason)` callback event to notify you of the reason the room was exited.
```javascript
import TRTCCloud from 'trtc-electron-sdk';
const trtcCloud = new TRTCCloud();

// Exit the current room
trtcCloud.exitRoom();
```

After the `exitRoom` API is called, the SDK will enter the room exit process, where two key tasks need to be completed:
- **1. Notify the exit of the current user**
Notify other users in the room of the upcoming room exit, and they will receive the **onRemoteUserLeaveRoom** callback from the current user; otherwise, other users may think the current user's video image is simply frozen.
- **2. Revoke device permissions**
If the current user is publishing an audio/video stream before exiting the room, the user needs to turn off the camera and mic and release the device permissions during the room exit process.

Therefore, we recommend you release the `TRTCCloud` instance after receiving the `onExitRoom` callback.

[](id:step3)
### Step 3. Be forced to exit the current room
The [onExitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) callback will also be received in other two cases in addition to active room exit:
- **Case 1. A user is kicked out of the room**
You can use the [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) or [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630) API to kick a user out of a TRTC room. After being kicked out, the user will receive the `onExitRoom(1)` callback.

- **Case 2. The current room is closed**
You can call the [DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) or [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631) API to close a TRTC room. After the room is closed, all users in the room will receive the `onExitRoom(2)` callback.

```javascript
// Listen for the `onExitRoom` callback to get the reason for room exit
function onExitRoom(reason) {
  console.log(`onExitRoom reason: ${reason}`);
}
trtcCloud.on('onExitRoom', onExitRoom);
```
