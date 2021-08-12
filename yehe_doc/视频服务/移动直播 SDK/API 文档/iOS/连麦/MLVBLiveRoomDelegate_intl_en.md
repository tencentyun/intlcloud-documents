__Feature__

[MLVBLiveRoom](https://intl.cloud.tencent.com/document/product/1071/41668) event callbacks

__Introduction__

Callbacks for room exit, debugging events, errors, and more



## Common Event Callbacks

### onError

Error callback.

```
- (void)onError:(int)errCode errMsg:(NSString *)errMsg extraInfo:(NSDictionary *)extraInfo 
```

__Parameters__

| Parameter | Type | Description |
| --------- | -------------- | ------------------------------------------------------------ |
| errCode   | int            | Error code                                                     |
| errMsg    | NSString *     | Error message                                                   |
| extraInfo | NSDictionary * | Additional information, such as the user for which the error is generated. It generally does not require attention. |

__Introduction__

This callback indicates that the SDK encounters an irrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending on the situation.

***

### onWarning

Warning callback.

```
- (void)onWarning:(int)warningCode warningMsg:(NSString *)warningMsg extraInfo:(NSDictionary *)extraInfo 
```

__Parameters__

| Parameter        | Type    | Description                                                                                                      |
| ----------- | -------------- | ------------------------------------------------------------ |
| warningCode | int            | Error code                                     |
| warningMsg  | NSString *     | Warning information                                                   |
| extraInfo | NSDictionary * | Additional information, such as the user for which the warning is generated. It generally does not require attention. |

***

### onDebugLog

Log callback.

```
- (void)onDebugLog:(NSString *)log 
```

__Parameters__

| Parameter | Type | Description |
| ---- | ---------- | ---------- |
| log  | NSString * | Log information |

***


## Room Event Callbacks

### onRoomDestroy

Callback of room termination.

```
- (void)onRoomDestroy:(NSString *)roomID 
```

__Parameters__

| Parameter | Type | Description |
| ------ | ---------- | --------- |
| roomID | NSString * | Room ID |

__Introduction__

When a host exits a room, all users in the room will receive this callback notification.

***


## Host/Viewer Room Entry/Exit Event Callbacks

### onAnchorEnter

Notification of the room entry of a new host.

```
- (void)onAnchorEnter:(MLVBAnchorInfo *)anchorInfo 
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------------- | ---------------- |
| anchorInfo | MLVBAnchorInfo * | Information of the new host who enters the room |

__Introduction__

When a new host enters a room, the host already in the room and mic connect viewers will receive the notification of the new host's room entry, and they can call [MLVBLiveRoom startRemoteView](https://intl.cloud.tencent.com/document/product/1071/41668#startremoteview) to display the video image of the new host.

>?Common viewers in the live room will not receive notifications of host entry and exit.

***

### onAnchorExit

Notification of the room exit of a host.

```
- (void)onAnchorExit:(MLVBAnchorInfo *)anchorInfo 
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------------- | -------------- |
| anchorInfo | MLVBAnchorInfo * | Information of the user who exits the room |

__Introduction__

When a host exits a room, the host in the room and mic connect viewers will receive the notification of the host's room exit, and they can call [MLVBLiveRoom stopRemoteView](https://intl.cloud.tencent.com/document/product/1071/41668#stopremoteview) to close the video image of the host.

>?Common viewers in the live room will not receive notifications of host entry and exit.

***

### onAudienceEnter

Notification of the room entry of a viewer.

```
- (void)onAudienceEnter:(MLVBAudienceInfo *)audienceInfo 
```

__Parameters__

| Parameter | Type | Description |
| ------------ | ------------------ | -------------- |
| audienceInfo | MLVBAudienceInfo * | Information of the viewer who enters the room |

***

### onAudienceExit

Notification of the room exit of a viewer.

```
- (void)onAudienceExit:(MLVBAudienceInfo *)audienceInfo 
```

__Parameters__

| Parameter | Type | Description |
| ------------ | ------------------ | -------------- |
| audienceInfo | MLVBAudienceInfo * | Information of the viewer who exits the room |

***


## Host/Viewer Mic Connect Event Callbacks

### onRequestJoinAnchor

Callback when the host receives a mic connect request from a viewer.

```
- (void)onRequestJoinAnchor:(MLVBAnchorInfo *)anchorInfo reason:(NSString *)reason 
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------------- | -------------- |
| anchorInfo | MLVBAnchorInfo * | Information of the viewer     |
| reason     | NSString *       | Reason for requesting mic connect |

***

### onKickoutJoinAnchor

Notification of being kicked out of mic connect received by a mic connect viewer.

```
- (void)onKickoutJoinAnchor
```

__Introduction__

If a mic connect viewer receives a message of being kicked out of mic connect by the host, the viewer needs to call [MLVBLiveRoom kickoutJoinAnchor](https://intl.cloud.tencent.com/document/product/1071/41668#kickoutjoinanchor) to exit mic connect.

***


## Host Competition Event Callbacks

### onRequestRoomPK

Notification of a cross-room competition request.

```
- (void)onRequestRoomPK:(MLVBAnchorInfo *)anchorInfo 
```

__Parameters__

| Parameter       | Type             | Description                     |
| ---------- | ---------------- | ------------------------ |
| anchorInfo | MLVBAnchorInfo * | Information of the host who initiates cross-room mic connect |

__Introduction__

If a host receives a competition request from the host of another room and accepts the competition, the invited host needs to call [MLVBLiveRoom startRemoteView](https://intl.cloud.tencent.com/document/product/1071/41668#startremoteview) to display the video image of the inviting host.

***

### onQuitRoomPK

Notification of the stop of cross-room competition.

```
- (void)onQuitRoomPK
```

***


## Message Event Callbacks

### onRecvRoomTextMsg

Receipt of a text message.

```
- (void)onRecvRoomTextMsg:(NSString *)roomID userID:(NSString *)userID userName:(NSString *)userName userAvatar:(NSString *)userAvatar message:(NSString *)message 
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | ------------ |
| roomID | NSString * | Room ID |
| userID     | NSString * | Sender ID  |
| userName   | NSString * | Sender nickname |
| userAvatar | NSString * | Sender profile photo |
| message    | NSString * | Text message   |

***

### onRecvRoomCustomMsg

Receipt of a custom message.

```
- (void)onRecvRoomCustomMsg:(NSString *)roomID userID:(NSString *)userID userName:(NSString *)userName userAvatar:(NSString *)userAvatar cmd:(NSString *)cmd message:(NSString *)message 
```

__Parameters__

| Parameter | Type | Description |
| ---------- | ---------- | ---------------- |
| roomID     | NSString * | Room ID |
| userID     | NSString * | Sender ID  |
| userName   | NSString * | Sender nickname |
| userAvatar | NSString * | Sender profile photo |
| cmd        | NSString * | Custom CMD     |
| message    | NSString * | Custom message content |


