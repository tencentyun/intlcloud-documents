## TUICallEvent APIs

`TUICallEvent` APIs are the **callback APIs** of the audio/video call component.

## Event List

| Event                                                        | Description                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | An internal error occurred.                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | The SDK is ready.                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | The current user was removed from the room due to repeated login.                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | A user accepted the call.                     |
| [TUICallEvent.USER_ENTER](#user_enter) | A user joined the call.             |
| [TUICallEvent.USER_LEAVE](#user_leave) | A user left the call.             |
| [TUICallEvent.REJECT](#reject) | A user rejected the call.                                         |
| [TUICallEvent.NO_RESP](#no_resp) | The invitee user did not answer.                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | The line is busy.                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | The call timed out (received by an invitee). |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | A remote user turned on/off their camera.              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | A remote user turned on/off their mic.              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | A remote user adjusted their call volume.                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | The invitation list for a group call was updated.                           |
| [TUICallEvent.INVITED](#invited) | You were invited to a call.                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | The call was canceled (received by an invitee).   |
| [TUICallEvent.CALLING_END](#calling_end) | The call ended.                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | The device list was updated.                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | The call type changed.                               |

### ERROR

An error occurred inside the SDK.

```javascript
let onError = function(error) {
  console.log(error);
};
tuiCallEngine.on(TUICallEvent.ERROR, onError);
```

### SDK_READY

The SDK is ready.

```javascript
let onSDKReady = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.SDK_READY, onSDKReady);
```

### KICKED_OUT

You were removed from the room due to repeated login.


```javascript
let handleOnKickedOut = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.KICKED_OUT, handleOnKickedOut);
```

### USER_ACCEPT

A user answered the call.

```javascript
let handleUserAccept = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_ACCEPT, handleUserAccept);
```

### USER_ENTER

A user agreed to join the call.

```javascript
let handleUserEnter = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_ENTER, handleUserEnter);
```

### USER_LEAVE

A user agreed to leave the call.

```javascript
let handleUserLeave = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_LEAVE, handleUserLeave);
```

### REJECT

The user rejected the call.

```javascript
let handleInviteeReject = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.REJECT, handleInviteeReject);
```

### NO_RESP

The invitee did not answer.

In a one-to-one call, if the invitee does not answer, the inviter will receive this callback.

In a group call, all invitees can receive this callback. For example, if user A invited user B and user C to a group call, and B did not answer, both A and C would receive this callback.

```javascript
let handleNoResponse = function(event) {
console.log(event)
};
tuiCallEngine.on(TUICallEvent.NO_RESP, handleNoResponse);
```

### LINE_BUSY

The invitee is busy.

```javascript
let handleLineBusy = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.LINE_BUSY, handleLineBusy);
```

### CALLING_TIMEOUT

The call timed out. This callback is received by an invitee.

```javascript
let handleCallingTimeout = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_TIMEOUT, handleCallingTimeout);
```

### USER_VIDEO_AVAILABLE

A remote user turned on/off their camera.

```javascript
let handleUserVideoChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_VIDEO_AVAILABLE, handleUserVideoChange);
```

### USER_AUDIO_AVAILABLE

A remote user turned on/off their mic.

```javascript
let handleUserAudioChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_AUDIO_AVAILABLE, handleUserAudioChange);
```

### USER_VOICE_VOLUME

A remote user adjusted their call volume.

```javascript
let handleUserVoiceVolumeChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_VOICE_VOLUME, handleUserVoiceVolumeChange);
```

### GROUP_CALL_INVITEE_LIST_UPDATE

The invitee list for a group call was updated.

```javascript
let handleGroupInviteeListUpdate = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE, handleGroupInviteeListUpdate);
```

### INVITED

You were invited to a call.

```javascript
let handleNewInvitationReceived = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.INVITED, handleNewInvitationReceived);
```

### CALLING_CANCEL

The call was canceled. This callback is received by an invitee.

```javascript
let handleCallingCancel = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_CANCEL, handleCallingCancel);
```

### CALLING_END

The call ended.

```javascript
let handleCallingEnd = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_END, handleCallingEnd);
```

### DEVICED_UPDATED

The device list was updated.

```javascript
let handleDeviceUpdated = function({ microphoneList, cameraList, currentMicrophoneID, currentCameraID }) {
  console.log(microphoneList, cameraList, currentMicrophoneID, currentCameraID)
};
tuiCallEngine.on(TUICallEvent.DEVICED_UPDATED, handleDeviceUpdated);
```

### CALL_TYPE_CHANGED

The call type changed.

```javascript
let handleCallTypeChanged = function({ oldCallType, newCallType }) {
  console.log(oldCallType, newCallType)
};
tuiCallEngine.on(TUICallEvent.CALL_TYPE_CHANGED, handleDeviceUpdated);
```