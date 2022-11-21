## TUICallEvent APIの概要

TUICallEvent APIはオーディオビデオ通話コンポーネントの**イベントインターフェース**です。

## イベントリスト

| EVENT                                                        | 説明                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | SDKの内部でエラーが発生しました                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | SDKがready状態に入ったときにこのコールバックを受信します                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | 重複ログインです。このコールバックを受信した場合は、ルームからの強制退出を意味します                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | 応答したユーザーがいる場合に、このコールバックを受信します                     |
| [TUICallEvent.USER_ENTER](#user_enter) | 通話への参加に同意したユーザーがいる場合に、このコールバックを受信します             |
| [TUICallEvent.USER_LEAVE](#user_leave) | 通話からの退出に同意したユーザーがいる場合に、このコールバックを受信します             |
| [TUICallEvent.REJECT](#reject) | ユーザーが通話を拒否                                         |
| [TUICallEvent.NO_RESP](#no_resp) | 招待したユーザーからの応答なし                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | 招待者が通話中                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | 被招待者が受信します。このコールバックを受信した場合は、今回の通話に応答せずタイムアウトしたことを意味します |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | リモートユーザーによるカメラのオン/オフがあった場合に、このコールバックを受信します              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | リモートユーザーによるマイクのオン/オフがあった場合に、このコールバックを受信します              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | リモートユーザーがスピーカーの音量調整を行った場合に、このコールバックを受信します                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | グループチャットの招待リストが更新された場合にこのコールバックを受信します                           |
| [TUICallEvent.INVITED](#invited) | 通話に招待されました                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | 被招待者が受信します。このコールバックを受信した場合は、今回の通話がキャンセルされたことを意味します   |
| [TUICallEvent.CALLING_END](#calling_end) | このコールバックを受信した場合は、今回の通話が終了したことを意味します                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | デバイスリストが更新された場合にこのコールバックを受信します                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | 通話タイプが切り替わった場合にこのコールバックを受信します                               |

### ERROR

SDK内部にエラーが発生しました。

```javascript
let onError = function(error) {
  console.log(error)
};
tuiCallEngine.on(TUICallEvent.ERROR, onError);
```

### SDK_READY

SDKがready状態に入るとこのコールバックを受信します

```javascript
let onSDKReady = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.SDK_READY, onSDKReady);
```

### KICKED_OUT

重複ログインです。このコールバックを受信した場合は、ルームからの強制退出を意味します。


```javascript
let handleOnKickedOut = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.KICKED_OUT, handleOnKickedOut);
```

### USER_ACCEPT

応答したユーザーがいる場合に、このコールバックを受信します。

```javascript
let handleUserAccept = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_ACCEPT, handleUserAccept);
```

### USER_ENTER

通話への参加に同意したユーザーがいる場合に、このコールバックを受信します。

```javascript
let handleUserEnter = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_ENTER, handleUserEnter);
```

### USER_LEAVE

通話からの退出に同意したユーザーがいる場合に、このコールバックを受信します。

```javascript
let handleUserLeave = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_LEAVE, handleUserLeave);
```

### REJECT

ユーザーが通話を拒否しました。

```javascript
let handleInviteeReject = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.REJECT, handleInviteeReject);
```

### NO_RESP

招待されたユーザーは応答しませんでした。

C2C通話では、発信者のみが応答なしのコールバックを受信します。例えばA がB、C を通話に招待し、Bが応答しなかった場合、Aはこのコールバックを受信できますが、Cは受信できません。

IMグループ通話では、すべての被招待者がこのコールバックを受信できます。例えばA がB、C を通話に招待し、Bが応答しなかった場合、A、Cのどちらもこのコールバックを受信できます。

```javascript
let handleNoResponse = function(event) {
console.log(event)
};
tuiCallEngine.on(TUICallEvent.NO_RESP, handleNoResponse);
```

### LINE_BUSY

招待者が通話中です。

```javascript
let handleLineBusy = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.LINE_BUSY, handleLineBusy);
```

### CALLING_TIMEOUT

被招待者が受信します。このコールバックを受信した場合は、今回の通話に応答せずタイムアウトしたことを意味します。

```javascript
let handleCallingTimeout = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_TIMEOUT, handleCallingTimeout);
```

### USER_VIDEO_AVAILABLE

リモートユーザーによるカメラのオン/オフがあった場合に、このコールバックを受信します。

```javascript
let handleUserVideoChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_VIDEO_AVAILABLE, handleUserVideoChange);
```

### USER_AUDIO_AVAILABLE

リモートユーザーによるマイクのオン/オフがあった場合に、このコールバックを受信します。

```javascript
let handleUserAudioChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_AUDIO_AVAILABLE, handleUserAudioChange);
```

### USER_VOICE_VOLUME

リモートユーザーがスピーカーの音量調整を行った場合に、このコールバックを受信します。

```javascript
let handleUserVoiceVolumeChange = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.USER_VOICE_VOLUME, handleUserVoiceVolumeChange);
```

### GROUP_CALL_INVITEE_LIST_UPDATE

グループチャットで招待リストを更新するとこのコールバックを受信します

```javascript
let handleGroupInviteeListUpdate = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE, handleGroupInviteeListUpdate);
```

### INVITED

通話に招待されました。

```javascript
let handleNewInvitationReceived = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.INVITED, handleNewInvitationReceived);
```

### CALLING_CANCEL

被招待者が受信します。このコールバックを受信した場合は、今回の通話がキャンセルされたことを意味します。

```javascript
let handleCallingCancel = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_CANCEL, handleCallingCancel);
```

### CALLING_END

このコールバックを受信した場合は、今回の通話が終了したことを意味します。

```javascript
let handleCallingEnd = function(event) {
  console.log(event)
};
tuiCallEngine.on(TUICallEvent.CALLING_END, handleCallingEnd);
```

### DEVICED_UPDATED

デバイスリストが更新された場合にこのコールバックを受信します。

```javascript
let handleDeviceUpdated = function({ microphoneList, cameraList, currentMicrophoneID, currentCameraID }) {
  console.log(microphoneList, cameraList, currentMicrophoneID, currentCameraID)
};
tuiCallEngine.on(TUICallEvent.DEVICED_UPDATED, handleDeviceUpdated);
```

### CALL_TYPE_CHANGED

通話タイプが切り替わった場合にこのコールバックを受信します。

```javascript
let handleCallTypeChanged = function({ oldCallType, newCallType }) {
  console.log(oldCallType, newCallType)
};
tuiCallEngine.on(TUICallEvent.CALL_TYPE_CHANGED, handleDeviceUpdated);
```