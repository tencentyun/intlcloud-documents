## TUICallEvent API

TUICallEvent API는 음성/영상 통화 컴포넌트의 **콜백 API**입니다.

## 이벤트 목록

| EVENT                                                 | 설명                                                         |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | SDK 내부 오류 발생                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | SDK가 ready 상태                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | 반복되는 로그인으로 인해 현재 사용자가 방에서 제거되었음                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | 사용자가 통화를 수락                     |
| [TUICallEvent.USER_ENTER](#user_enter) | 사용자가 통화에 참여             |
| [TUICallEvent.USER_LEAVE](#user_leave) | 사용자가 통화를 종료             |
| [TUICallEvent.REJECT](#reject) | 사용자가 통화를 거절                                         |
| [TUICallEvent.NO_RESP](#no_resp) | 초대된 사용자가 응답하지 않았음                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | 초대된 사용자가 통화 중                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | 통화 시간 초과(초대 대상자가 수신) |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | 원격 사용자가 카메라를 켜거나 끔              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | 원격 사용자가 마이크를 켜거나 끔              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | 원격 사용자가 통화 볼륨을 조정                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | 그룹 통화 초대 목록이 업데이트되었음                           |
| [TUICallEvent.INVITED](#invited) | 통화에 초대되었음                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | 통화가 취소되었음(초대 대상자가 수신함)   |
| [TUICallEvent.CALLING_END](#calling_end) | 통화가 종료되었음                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | 장치 목록이 업데이트되었음                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | 통화 유형이 변경되었음                               |

### ERROR

SDK 내부에서 오류가 발생했습니다.

```javascript
let onError = function(error) {
  console.log(error)
};
tuiCallEngine.on(TUICallEvent.ERROR, onError);
```

### SDK_READY

SDK ready 상태 진입 시, 이 콜백을 수신합니다.

```javascript
let onSDKReady = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.SDK_READY, onSDKReady);
```

### KICKED_OUT

반복 로그인으로 인해 방에서 퇴장되었습니다.


```javascript
let handleOnKickedOut = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.KICKED_OUT, handleOnKickedOut);
```

### USER_ACCEPT

사용자가 전화를 받았습니다.

```javascript
let handleUserAccept = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_ACCEPT, handleUserAccept);
```

### USER_ENTER

사용자가 통화 참여에 동의했습니다.

```javascript
let handleUserEnter = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_ENTER, handleUserEnter);
```

### USER_LEAVE

사용자가 통화를 종료하는 데 동의했습니다.

```javascript
let handleUserLeave = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_LEAVE, handleUserLeave);
```

### REJECT

사용자가 통화를 거절했습니다.

```javascript
let handleInviteeReject = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.REJECT, handleInviteeReject);
```

### NO_RESP

초대 받은 사람이 응답하지 않았습니다.

C2C 통화에서 초대받은 사람이 응답하지 않으면 초대한 사람이 이 콜백을 받게 됩니다.

그룹 통화에서 모든 초대 대상자는 이 콜백을 받을 수 있습니다. 예를 들어 사용자 A가 사용자 B와 사용자 C를 그룹 통화에 초대했지만 B가 응답하지 않으면 A와 C 모두 이 콜백을 받습니다.

```javascript
let handleNoResponse = function(event) {
console.log(event)
};
tuiCallEngine.on(TUICallEvent.NO_RESP, handleNoResponse);
```

### LINE_BUSY

초대받은 사람이 통화 중입니다.

```javascript
let handleLineBusy = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.LINE_BUSY, handleLineBusy);
```

### CALLING_TIMEOUT

통화 시간이 초과되었습니다. 이 콜백은 초대받은 사람이 받았습니다.

```javascript
let handleCallingTimeout = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_TIMEOUT, handleCallingTimeout);
```

### USER_VIDEO_AVAILABLE

원격 사용자가 카메라를 켜거나 끕니다.

```javascript
let handleUserVideoChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_VIDEO_AVAILABLE, handleUserVideoChange);
```

### USER_AUDIO_AVAILABLE

원격 사용자가 마이크를 켜거나 끕니다.

```javascript
let handleUserAudioChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_AUDIO_AVAILABLE, handleUserAudioChange);
```

### USER_VOICE_VOLUME

원격 사용자가 통화 볼륨을 조정했습니다.

```javascript
let handleUserVoiceVolumeChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_VOICE_VOLUME, handleUserVoiceVolumeChange);
```

### GROUP_CALL_INVITEE_LIST_UPDATE

그룹 통화의 초대 대상자 목록이 업데이트되었습니다.

```javascript
let handleGroupInviteeListUpdate = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE, handleGroupInviteeListUpdate);
```

### INVITED

통화에 초대되었습니다.

```javascript
let handleNewInvitationReceived = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.INVITED, handleNewInvitationReceived);
```

### CALLING_CANCEL

통화가 취소되었습니다. 이 콜백은 초대받은 사람이 받았습니다.

```javascript
let handleCallingCancel = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_CANCEL, handleCallingCancel);
```

### CALLING_END

통화가 종료되었습니다.

```javascript
let handleCallingEnd = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_END, handleCallingEnd);
```

### DEVICED_UPDATED

장치 목록이 업데이트되었습니다.

```javascript
let handleDeviceUpdated = function({ microphoneList, cameraList, currentMicrophoneID, currentCameraID }) {
  console.log(microphoneList, cameraList, currentMicrophoneID, currentCameraID)
};
tuiCallEngine.on(TUICallEvent.DEVICED_UPDATED, handleDeviceUpdated);
```

### CALL_TYPE_CHANGED

통화 유형이 변경되었습니다.

```javascript
let handleCallTypeChanged = function({ oldCallType, newCallType }) {
  console.log(oldCallType, newCallType)
};
tuiCallEngine.on(TUICallEvent.CALL_TYPE_CHANGED, handleDeviceUpdated);
```