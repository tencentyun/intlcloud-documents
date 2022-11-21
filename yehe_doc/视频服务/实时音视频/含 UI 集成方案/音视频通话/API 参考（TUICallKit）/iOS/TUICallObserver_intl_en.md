## TUICallObserver APIs

`TUICallObserver` is the callback class of `TUICallEngine`. You can use it to listen for events.

## Overview

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| [onError](#onerror) | A call occurred during the call.         |
| [onCallReceived](#oncallreceived) | A call invitation was received.             |
| [onCallCancelled](#oncallcancelled) | The call was canceled.             |
| [onCallBegin](#oncallbegin) | The call was connected.             |
| [onCallEnd](#oncallend) | The call ended.             |
| [onCallMediaTypeChanged](#oncallmediatypechanged) | The call type changed. |
| [onUserReject](#onuserreject) | A user declined the call.    |
| [onUserNoResponse](#onusernoresponse) | A user didn't respond.      |
| [onUserLineBusy](#onuserlinebusy) | A user was busy.        |
| [onUserJoin](#onuserjoin) |  A user joined the call.    |
| [onUserLeave](#onuserleave) | A user left the call.         |
| [onUserVideoAvailable](#onuservideoavailable) | Whether a user had a video stream. |
| [onUserAudioAvailable](#onuseraudioavailable) | Whether a user had an audio stream. |
| [onUserVoiceVolumeChanged](#onuservoicevolumechanged) | The volume levels of all users. |
| [onUserNetworkQualityChanged](#onusernetworkqualitychanged) | The network quality of all users. |

## Details

### onError

An error occurred.

>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```objc
- (void)onError:(int)code message:(NSString * _Nullable)message;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | -------- | -------- |
| code    | int    | The error code.   |
| message | NSString  | The error message. |

### onCallReceived

A call invitation was received. This callback is received by an invitee. You can listen for this event to determine whether to display the incoming call view.

```objc
- (void)onCallReceived:(NSString *)callerId calleeIdList:(NSArray<NSString *> *)calleeIdList groupId:(NSString * _Nullable)groupId callMediaType:(TUICallMediaType)callMediaType
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ---------------- | -------------------------------------- |
| callerId      | NSString                  | The user ID of the inviter.                      |
| calleeIdList  | NSArray          | The invitee list.               |
| groupId       | NSString         | The group ID.                            |
| callMediaType | TUICallMediaType | The call type, which can be video or audio.                       |

### onCallCancelled

The call was canceled by the inviter or timed out. This callback is received by an invitee. You can listen for this event to determine whether to show a missed call message.

```objc
- (void)onCallCancelled:(NSString *)callerId;
```

The parameters are described below:

| Parameter     |  Type  | Description                                    |
| -------- | -------- | ------------- |
| callerId | NSString | The user ID of the inviter. |

### onCallBegin

The call was connected. This callback is received by both the inviter and invitees. You can listen for this event to determine whether to start on-cloud recording, content moderation, or other tasks.

```swift
- (void)onCallBegin:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole;
```

The parameters are described below:

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |
| callRole      | TUICallRole      | The role, which can be caller or callee.                                   |

### onCallEnd

The call ended. This callback is received by both the inviter and invitees. You can listen for this event to determine when to display call information such as call duration and call type, or stop on-cloud recording.

```swift
- (void)onCallEnd:(TUIRoomId *)roomId callMediaType:(TUICallMediaType)callMediaType callRole:(TUICallRole)callRole totalTime:(float)totalTime;
```

The parameters are described below:

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| roomId        | TUIRoomId        | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |
| callRole      | TUICallRole      | The role, which can be caller or callee.                                   |
| totalTime     | float            | The call duration.                                               |

>! Client-side callbacks are often lost when errors occur, for example, when the process is closed. If you need to measure the duration of a call for billing or other purposes, we recommend you use the RESTful API.

### onCallMediaTypeChanged

The call type changed.

```swift
- (void)onCallMediaTypeChanged:(TUICallMediaType)oldCallMediaType newCallMediaType:(TUICallMediaType)newCallMediaType;
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------------- | ---------------- | ------------ |
| oldCallMediaType | TUICallMediaType | The call type before the change. |
| newCallMediaType | TUICallMediaType | The call type after the change. |

### onUserReject

The call was rejected. In a one-to-one call, only the inviter will receive this callback. In a group call, all invitees will receive this callback.

```swift
- (void)onUserReject:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | -------- | ------------- |
| userId | NSString | The ID of the user who rejected the call. |

### onUserNoResponse

A user did not respond.

```swift
- (void)onUserNoResponse:(NSString *)userId;
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | -------- | --------------- |
| userId | NSString | The ID of the user who did not respond. |

### onUserLineBusy

The line is busy.

```swift
- (void)onUserLineBusy:(NSString *)userId;
```

### onUserJoin

A user joined the call.

```swift
- (void)onUserJoin:(NSString *)userId;
```

### onUserLeave

A user left the call.

```swift
- (void)onUserLeave:(NSString *)userId;
```

### onUserAudioAvailable

Whether a user is sending audio.

```swift
- (void)onUserAudioAvailable:(NSString *)userId isAudioAvailable:(BOOL)isAudioAvailable;
```

The parameters are described below:

| Parameter     |    Type     | Description                                                         |
| ---------------- | -------- | ---------------- |
| userId | NSString  | The user ID.            |
| isAudioAvailable | BOOL     | Whether the user has audio. |

### onUserVideoAvailable

Whether a user is sending video.

```swift
- (void)onUserVideoAvailable:(NSString *)userId isVideoAvailable:(BOOL)isVideoAvailable;
```

The parameters are described below:

| Parameter     |    Type     | Description                                                         |
| ---------------- | -------- | ---------------- |
| userId           | NSString | The user ID.      |
| isVideoAvailable | BOOL     | Whether the user has video. |

### onUserVoiceVolumeChanged

The volumes of all users.

```swift
- (void)onUserVoiceVolumeChanged:(NSDictionary <NSString *, NSNumber *> *)volumeMap;
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------------------------------------- | ------------------------------------------------------------ |
| volumeMap | NSDictionary <NSString *, NSNumber *> | The volume table, which includes the volume of each user (`userId`). Value range: 0-100. |
| volumeMap | NSDictionary                          | The volume table, which includes the volume of each user (`userId`). Value range: 0-100. |

### onUserNetworkQualityChanged

The network quality of all users.

```swift
- (void)onUserNetworkQualityChanged:(NSArray<TUINetworkQualityInfo *> *)networkQualityList;
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------------------ | ------- | -------------------------------------------------------- |
| networkQualityList | NSArray | The current network conditions for all users (`userId`). |