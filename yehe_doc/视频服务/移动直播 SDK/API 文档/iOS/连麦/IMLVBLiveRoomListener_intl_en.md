__Feature__

[MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41673) event callback APIs

__Introduction__

APIs for the callback of room exit, debugging events, errors, and more.



## Common Event Callback APIs

### onError

Error callback.

```
void onError(int errCode, String errMsg, Bundle extraInfo)
```

__Parameters__

| Parameter | Type | Description |
| --------- | ------ | ------------------------------------------------------------ |
| errCode   | int            | Error code                                                     |
| errMsg    | String | Error message                                                   |
| extraInfo | Bundle | Additional information, such as the user for which the error is generated. It generally does not require attention and is displayed for local errors by default. |

__Introduction__

This callback indicates that the SDK encounters an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending on the situation.

***

### onWarning

Warning callback.

```
void onWarning(int warningCode, String warningMsg, Bundle extraInfo)
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ----------- | ------ | ------------------------------------------------------------ |
| warningCode | int            | Warning code                                     |
| warningMsg  | String     | Warning information                                                   |
| extraInfo | Bundle | Additional information, such as the user for which the warning is generated. It generally does not require attention and is displayed for local errors by default. |

***

### onDebugLog

```
void onDebugLog(String log)
```

***


## Room Event Callback APIs

### onRoomDestroy

Callback of room termination.

```
void onRoomDestroy(String roomID)
```

__Parameters__

| Parameter | Type | Description |
| ------ | ------ | --------- |
| roomID | String | Room ID |

__Introduction__

When a host exits a room, all users in the room will receive this callback notification.

***

### onAnchorEnter

Notification of the room entry of a new host.

```
void onAnchorEnter(AnchorInfo anchorInfo)
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | ---------------- |
| anchorInfo | AnchorInfo | ID of the new host who enters the room |

__Introduction__

When a new host enters a room, the host already in the room and mic connect viewers will receive the notification of the new host's room entry, and they can call [MLVBLiveRoom#startRemoteView(AnchorInfo, TXCloudVideoView, PlayCallback)](https://intl.cloud.tencent.com/document/product/1071/41673#startremoteview) to display the video image of the new host.

>?Common viewers in the live room will not receive notifications of host entry and exit.

***

### onAnchorExit

Notification of the room exit of a host.

```
void onAnchorExit(AnchorInfo anchorInfo)
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | -------------- |
| anchorInfo | AnchorInfo | ID of the user who exits the room |

__Introduction__

When a host exits a room, the host in the room and mic connect viewers will receive the notification of the host's room exit, and they can call [MLVBLiveRoom#stopRemoteView(AnchorInfo)](https://intl.cloud.tencent.com/document/product/1071/41673#stopremoteview) to close the video image of the host.

>?Common viewers in the live room will not receive notifications of host entry and exit.

***

### onAudienceEnter

Notification of the room entry of a viewer.

```
void onAudienceEnter(AudienceInfo audienceInfo)
```

__Parameters__

| Parameter | Type | Description |
| ------------ | ------------ | -------------- |
| audienceInfo | AudienceInfo | Information of the viewer who enters the room |

***

### onAudienceExit

Notification of the room exit of a viewer.

```
void onAudienceExit(AudienceInfo audienceInfo)
```

__Parameters__

| Parameter | Type | Description |
| ------------ | ------------ | -------------- |
| audienceInfo | AudienceInfo | Information of the viewer who exits the room |

***

### onRequestJoinAnchor

Callback of host receiving a mic connect request from a viewer.

```
void onRequestJoinAnchor(AnchorInfo anchorInfo, String reason)

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | -------------- |
| anchorInfo | AnchorInfo | Information of the viewer     |
| reason     | String     | Reason for mic connect |

***

### onKickoutJoinAnchor

Notification of being kicked out of mic connect received by mic connect viewer.

```
void onKickoutJoinAnchor()

```

__Introduction__

If a mic connect viewer receives a message of being kicked out of mic connect by the host, the viewer needs to call [MLVBLiveRoom#kickoutJoinAnchor(String)](https://intl.cloud.tencent.com/document/product/1071/41673#kickoutjoinanchor) to exit mic connect.

***

### onRequestRoomPK

Notification of a cross-room competition request.

```
void onRequestRoomPK(AnchorInfo anchorInfo)

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | ------------------------ |
| anchorInfo | AnchorInfo | Information of the host who initiates cross-room mic connect |

__Introduction__

If a host receives a competition request from the host of another room and accepts the competition, the invited host needs to call [MLVBLiveRoom#startRemoteView(AnchorInfo， TXCloudVideoView， PlayCallback)](https://intl.cloud.tencent.com/document/product/1071/41673#startremoteview) to display the video image of the inviting host.

***

### onQuitRoomPK

Notification of the stop of cross-room competition.

```
void onQuitRoomPK(AnchorInfo anchorInfo)

```

***


## Message Event Callback APIs

### onRecvRoomTextMsg

Callback of the receipt of a text message.

```
void onRecvRoomTextMsg(String roomID, String userID, String userName, String userAvatar, String message)

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ------ | ------------ |
| roomID | String | Room ID |
| userID | String | Sender ID |
| userName | String | Sender nickname |
| userAvatar | String | Sender profile photo |
| message | String | Text message |

***

### onRecvRoomCustomMsg

Callback of the receipt of a custom message.

```
void onRecvRoomCustomMsg(String roomID, String userID, String userName, String userAvatar, String cmd, String message)

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ------ | ---------------- |
| roomID     | String | Room ID        |
| userID | String | Sender ID |
| userName | String | Sender nickname |
| userAvatar | String | Sender profile photo |
| cmd        | String | Custom CMD     |
| message    | String | Custom message content |

***


## LoginCallback

__Feature__

Login result callback APIs



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## GetRoomListCallback

__Feature__

Viewer list getting result callback APIs



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***

### onSuccess

Success callback.

```
void onSuccess(ArrayList< RoomInfo > roomInfoList)

```

__Parameters__

| Parameter | Type | Description |
| ------------ | --------------------- | ---------- |
| roomInfoList | ArrayList< RoomInfo > | Room list |

***


## GetAudienceListCallback

__Feature__

Viewer list getting result callback APIs

__Introduction__

When viewers enter a room, the backend adds their information to the viewer list of the room. A viewer list can contain up to 30 viewers.



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***

### onSuccess

Success callback.

```
void onSuccess(ArrayList< AudienceInfo > audienceInfoList)

```

__Parameters__

| Parameter | Type | Description |
| ---------------- | ------------------------- | ---------- |
| audienceInfoList | ArrayList< AudienceInfo > | Viewer list |

***


## CreateRoomCallback

__Feature__

Room creation result callback APIs



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***

### onSuccess

Success callback.

```
void onSuccess(String RoomID)

```

__Parameters__

| Parameter | Type | Description |
| ------ | ------ | ------------ |
| RoomID | String | Room ID |

***


## EnterRoomCallback

__Feature__

Room entry result callback APIs



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## ExitRoomCallback

__Feature__

Room exit result callback APIs



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## RequestJoinAnchorCallback

__Feature__

APIs for the callback of viewer's mic connect request results



### onAccept

Callback of host accepting mic connect.

```
void onAccept()

```

***

### onReject

Callback of host rejecting mic connect.

```
void onReject(String reason)

```

__Parameters__

| Parameter | Type | Description |
| ------ | ------ | ---------- |
| reason | String | Reason for rejection |

***

### onTimeOut

Callback of request timeout.

```
void onTimeOut()

```

***

### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information |

***


## JoinAnchorCallback

__Feature__

APIs for the callback of mic connect status entering results



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ------------------------------ |
| errCode | int    | Error code |
| errInfo | String | Error information                     |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## QuitAnchorCallback

__Feature__

APIs for the callback of mic connect status exiting results



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## RequestRoomPKCallback

__Feature__

APIs for the callback of cross-room competition request results



### onAccept

Callback of host accepting cross-room competition.

```
void onAccept(AnchorInfo anchorInfo)

```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | ---------------------- |
| anchorInfo | AnchorInfo | Information of the invited host |

***

### onReject

Callback of host rejecting cross-room competition.

```
void onReject(String reason)

```

__Parameters__

| Parameter | Type | Description |
| ------ | ------ | ---------- |
| reason | String | Reason for rejection |

***

### onTimeOut

Callback of request timeout.

```
void onTimeOut()

```

***

### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***


## QuitRoomPKCallback

__Feature__

APIs for the callback of cross-room competition exiting results



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## PlayCallback

__Feature__

Player callback APIs



### onBegin

Start callback.

```
void onBegin()

```

***

### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onEvent

Callback of other events.

```
void onEvent(int event, Bundle param)

```

__Parameters__

| Parameter | Type | Description |
| ----- | ------ | -------------- |
| event | int    | Event ID      |
| param | Bundle | Additional information of the event |

***


## SendRoomTextMsgCallback

__Feature__

APIs for the callback of text message sending results



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## SendRoomCustomMsgCallback

__Feature__

APIs for the callback of custom text message sending results



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onSuccess

Success callback.

```
void onSuccess()

```

***


## SetCustomInfoCallback

__Feature__

APIs for the callback of custom information setting results



### onError

Error callback.

```
void onError(int errCode, String errInfo)

```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onSuccess

Success callback.

```
void onSuccess()
```

***


## GetCustomInfoCallback

__Feature__

APIs for the callback of custom information getting results



### onError

Error callback.

```
void onError(int errCode, String errInfo)
```

__Parameters__

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| errCode | int    | Error code   |
| errInfo | String | Error information                     |

***

### onGetCustomInfo

APIs for the callback of custom text message getting results

```
void onGetCustomInfo(Map< String, Object > customInfo)
```

__Parameters__

| Parameter | Type | Description |
| ---------- | --------------------- | ------------ |
| customInfo | Map< String, Object > | Custom information |

***
