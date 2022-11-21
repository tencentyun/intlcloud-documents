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

```java
void onError(int code, String msg);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------ | -------- |
| code    | int    | The error code.   |
| msg  | String | The error message. |

### onCallReceived

A call invitation was received. This callback is received by an invitee. You can listen for this event to determine whether to display the incoming call view.

```java
void onCallReceived(String callerId, List<String> calleeIdList, String groupId, 
                    TUICallDefine.MediaType callMediaType);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ------------- | ----------------------- | -------------------------------------- |
| callerId      | String                  | The user ID of the inviter.                      |
| calleeIdList  | List                    | The invitee list.               |
| groupId       | String                  | The group ID.                            |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |

### onCallCancelled

The call was canceled by the inviter or timed out. This callback is received by an invitee. You can listen for this event to determine whether to show a missed call message.

```java
void onCallCancelled(String callerId);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | ------ | ------------- |
| callerId | String | The user ID of the inviter. |

### onCallBegin

The call was connected. This callback is received by both the inviter and invitees. You can listen for this event to determine whether to start on-cloud recording, content moderation, or other tasks.

```java
void onCallBegin(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |
| callRole      | TUICallDefine.Role      | The role, which can be caller or callee.                                   |

### onCallEnd

The call ended. This callback is received by both the inviter and invitees. You can listen for this event to determine when to display call information such as call duration and call type, or stop on-cloud recording.

```java
void onCallEnd(TUICommonDefine.RoomId roomId, TUICallDefine.MediaType callMediaType, TUICallDefine.Role callRole, long totalTime);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------- | ----------------------- | ------------------------------------------------------------ |
| roomId        | TUICommonDefine.RoomId  | The room ID. Currently, you can only use numeric room IDs. String-type room IDs will be supported in the future. |
| callMediaType | TUICallDefine.MediaType | The call type, which can be video or audio.                       |
| callRole      | TUICallDefine.Role      | The role, which can be caller or callee.                                   |
| totalTime     | long                    | The call duration.                                               |

>! Client-side callbacks are often lost when errors occur, for example, when the process is closed. If you need to measure the duration of a call for billing or other purposes, we recommend you use the RESTful API.

### onCallMediaTypeChanged

The call type changed.

```java
void onCallMediaTypeChanged(TUICallDefine.MediaType oldCallMediaType,TUICallDefine.MediaType newCallMediaType);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------------- | ----------------------- | ------------ |
| oldCallMediaType | TUICallDefine.MediaType | The call type before the change. |
| newCallMediaType | TUICallDefine.MediaType | The call type after the change. |

### onUserReject

The call was rejected. In a one-to-one call, only the inviter will receive this callback. In a group call, all invitees will receive this callback.

```java
void onUserReject(String userId);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | ------------- |
| userId | String | The user ID of the invitee who rejected the call. |

### onUserNoResponse

A user did not respond.

```java
void onUserNoResponse(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ------ | --------------- |
| userId | String | The user ID of the invitee who did not answer. |

### onUserLineBusy

A user is busy.

```java
void onUserLineBusy(String userId);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | ------------- |
| userId | String | The user ID of the invitee who is busy. |

### onUserJoin

A user joined the call.

```java
void onUserJoin(String userId);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ------ | --------------------- |
| userId | String | The ID of the user who joined the call. |

### onUserLeave

A user left the call.

```java
void onUserLeave(String userId);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ------ | --------------------- |
| userId | String | The ID of the user who left the call. |

### onUserVideoAvailable

Whether a user is sending video.

```java
void onUserVideoAvailable(String userId, boolean isVideoAvailable);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------------- | ------- | ---------------- |
| userId | String | The user ID. |
| isVideoAvailable | boolean | Whether the user has video. |

### onUserAudioAvailable

Whether a user is sending audio.

```java
void onUserAudioAvailable(String userId, boolean isAudioAvailable);
```

The parameters are described below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------------- | ------- | ---------------- |
| userId           | String  | The user ID.          |
| isAudioAvailable | boolean | Whether the user has audio. |

### onUserVoiceVolumeChanged

The volumes of all users.

```java
void onUserVoiceVolumeChanged(Map<String, Integer> volumeMap);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| --------- | -------------------- | ------------------------------------------------------------ |
| volumeMap | Map<String, Integer> | The volume table, which includes the volume of each user (`userId`). Value range: 0-100. |

### onUserNetworkQualityChanged

The network quality of all users.

```java
void onUserNetworkQualityChanged(List<TUICallDefine.NetworkQualityInfo> networkQualityList);
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------------------ | ---- | -------------------------------------------------------- |
| networkQualityList | List | The current network conditions for all users (`userId`). |
