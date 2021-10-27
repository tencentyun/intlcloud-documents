`TRTCVoiceRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a chat salon and become a speaker, or enter a salon as a listener.
- The room owner can invite a listener to speak as well as remove a speaker.
- The room owner can also block a seat. Listeners cannot request to take a blocked seat.
- A listener can request to speak and become a speaker. A speaker can also become a listener.
- All users can send text and custom messages. Custom messages can be used to send on-screen comments, give likes, and send gifts.

`TRTCVoiceRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Audio Chat Room (iOS)](https://intl.cloud.tencent.com/document/product/647/37287).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio chat component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the seat list, and invitation signaling is used to send requests to speak or invite others to speak.


<h2 id="TRTCVoiceRoom">TRTCVoiceRoom API Overview</h2>

### Basic SDK APIs

| API | Description |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets a singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callback. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where the event callback is. |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets profile. |

### Room APIs

| API | Description |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom) | Creates a room (called by room owner). If the room does not exist, the system will automatically create a room. |
| [destroyRoom](#destroyroom) | Terminates a room (called by room owner). |
| [enterRoom](#enterroom) | Enters a room (called by listener). |
| [exitRoom](#exitroom) | Exits a room (called by listener). |
| [getRoomInfoList](#getroominfolist) | Gets room list details.                                     |
| [getUserInfoList](#getuserinfolist) | Gets the user information of the specified `userId`. If the value is `nil`, the information of all users in the room is obtained. |

### Seat management APIs

| API | Description |
| ----------------------- | ----------------------------------- |
| [enterSeat](#enterseat) | Becomes a speaker (called by room owner or listener). |
| [leaveSeat](#leaveseat) | Becomes a listener (called by speaker).    |
| [pickSeat](#pickseat)   | Invites a listener to speak (called by room owner).                  |
| [kickSeat](#kickseat)   | Removes a speaker (called by room owner).                  |
| [muteSeat](#muteseat)   | Mutes/Unmutes a seat (called by room owner). |
| [closeSeat](#closeseat) | Blocks/Unblocks a seat (called by room owner).          |

### Local audio APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Enables mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [setAudioQuality](#setaudioquality)             | Sets audio quality.           |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker)                       | Turns the speaker on.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume.       |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | Enables/Disables in-ear monitoring.       |


### Remote audio APIs

| API | Description |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | Mutes/Unmutes a specified member. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all members. |

### Background music and audio effect APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager). |

### Message sending APIs

| API                                     | Description                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

### Invitation signaling APIs

| API                                             | Description                                                         |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | Sends an invitation. |
| [acceptInvitation](#acceptinvitation) | Accepts an invitation.       |
| [rejectInvitation](#rejectinvitation) | Declines an invitation.       |
| [cancelInvitation](#cancelinvitation) | Cancels an invitation.       |

<h2 id="TRTCVoiceRoomDelegate">TRTCVoiceRoomDelegate API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------- |
| [onError](#onerror) | Error |
| [onWarning](#onwarning) | Warning |
| [onDebugLog](#ondebuglog) | Log |

### Room event callback APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy) | Room termination |
| [onRoomInfoChange](#onroominfochange)     | Room information change |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Seat list change callback APIs

| API                                     | Description                                  |
| --------------------------------------- | ------------------------------------- |
| [onSeatListChange](#onseatlistchange)   | All seat changes                |
| [onAnchorEnterSeat](#onanchorenterseat) | Someone became a speaker after requesting or being invited by the room owner. |
| [onAnchorLeaveSeat](#onanchorleaveseat) | Someone became a listener or was moved to listeners by the room owner. |
| [onSeatMute](#onseatmute) | The room owner muted a speaker. |
| [onUserMicrophoneMute](#onusermicrophonemute)               | Whether a user's mic is muted                          |
| [onSeatClose](#onseatclose)             | The room owner blocked a seat.                          |

### Callback APIs for room entry/exit by listeners

| API                                             | Description                                                         |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | A listener entered the room. |
| [onAudienceExit](#onaudienceexit) | A listener exited the room. |

### Message event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | Receipt of a text message  |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of a custom message |

### Signaling event callback APIs

| API | Description |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | Receipt of an invitation |
| [onInviteeAccepted](#oninviteeaccepted)           | Invitation accepted by invitee   |
| [onInviteeRejected](#oninviteerejected)           |  Invitation declined by invitee   |
| [onInvitationCancelled](#oninvitationcancelled)   | Invitation canceled by inviter |

## Basic SDK APIs

[](id:sharedInstance)

### sharedInstance

This API is used to get a [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) singleton object.

```Objective-C
/**
* Get a `TRTCVoiceRoom` singleton object
*
* - returns: `TRTCVoiceRoom` instance
* - note: to terminate a singleton object, call {@link TRTCVoiceRoom#destroySharedInstance()}.
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

This API is used to terminate a [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) singleton object.

>?After the instance is terminated, the externally cached `TRTCVoiceRoom` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```Objective-C
/**
* Terminate a `TRTCVoiceRoom` singleton object
*
* - note: after the instance is terminated, the externally cached `TRTCVoiceRoom` instance can no longer be used. You need to call {@link TRTCVoiceRoom#sharedInstance()} again to get a new instance.
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

This API is used to set the event callback of [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287). You can use `TRTCVoiceRoomDelegate` to get different status notifications of [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286).

```Objective-C
/**
* Set the component callback
* 
* You can use `TRTCVoiceRoomDelegate` to get different status notifications of `TRTCVoiceRoom`
*
* - parameter delegate Callback API
* - note: callback events in `TRTCVoiceRoom` are called back to you in the main queue by default. If you need to specify a queue for event callback, please use {@link TRTCVoiceRoom#setDelegateQueue(queue)}.
*/
- (void)setDelegate:(id<TRTCVoiceRoomDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?`setDelegate` is the delegate callback of `TRTCVoiceRoom`.   

### setDelegateQueue

This API is used to set the thread queue for event callback. The main thread (MainQueue) is used by default.

```Objective-C
/**
* Set the queue for event callback
*
* - parameter queue Queue. Various status callback notifications in `TRTCVoiceRoom` will be sent to the queue you specify.
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | The status notifications of `TRTCVoiceRoom` are sent to the thread queue you specify. |

   

### login

This API is used to log in.

```Objective-C
- (void)login:(int)sdkAppID
       userId:(NSString *)userId
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int | You can view the `SDKAppID` via **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC console. |
| userId | String | ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For more information on how to get it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The `code` will be 0 if login succeeds. |

   

### logout

This API is used to log out.

```Objective-C
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | Callback for logout. The code is 0 if logout succeeds. |

   

### setSelfProfile

This API is used to set profile.

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | -------------- | ----------------------------------- |
| userName | String | Nickname |
| avatar | String | Profile photo address |
| callback | ActionCallback | Callback for profile setting. The code is 0 if the operation succeeds. |

   


## Room APIs

### createRoom

This API is used to create a room (called by room owner).

```Objective-C
- (void)createRoom:(int)roomID roomParam:(VoiceRoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into an audio chat room list. Currently, Tencent Cloud does not provide management services for room lists. Please manage the list on your own. |
| roomParam | TRTCCreateRoomParam | Room information, such as room name, seat list information, and cover information. To manage seats, you must enter the number of seats in the room. |
| callback | ActionCallback | Callback for room creation result. The code is 0 if the operation succeeds.  |

The process of creating an audio chat room and becoming a speaker is as follows: 
1. A user calls `createRoom` to create an audio chat room, passing in room attributes (e.g. room ID, whether listeners require room owner's consent to speak, number of seats).
2. After creating the room, the user calls `enterSeat` to become a speaker.
3. The user will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
4. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

   

### destroyRoom

This API is used to terminate a room (called by room owner).

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room termination result. The code is 0 if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by listener).

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| roomId | int | Room ID |
| callback | ActionCallback | Callback for room entry result. The `code` is 0 if the operation succeeds. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest audio chat room list from your server. The list may contain the `roomId` and room information of multiple audio chat rooms.
2. The user selects a room, and calls `enterRoom` with the room ID passed in to enter the room.
3. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner's consent is required for listeners to speak, etc.
4. The user will receive an `onSeatListChange` notification about the change of the seat list and can update the change to the UI.
5. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker.

### exitRoom

This API is used to exit a room.

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room exit result. The code is 0 if the operation succeeds. |

   

### getRoomInfoList

This API is used to get room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?You don't need this API if both the room list and room information are managed on your server.


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(VoiceRoomInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | Room ID list |
| callback | RoomInfoCallback | Callback for room details |


### getUserInfoList

This API is used to get the user information of a specified `userId`.

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(VoiceRoomUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt; | List of user IDs to obtain. If this parameter is `null`, the information of all users in the room is obtained. |
| userlistcallback | UserListCallback   | Callback for user details                                           |


## Seat Management APIs

### enterSeat

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```Objective-C
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | -------------------- |
| seatIndex | int            | The number of the seat to take |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the seat list. In cases where listeners need the room owner's consent to speak, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `enterSeat`.

### leaveSeat

This API is used to remove a speaker (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for operation |

### pickSeat

This API is used to invite a listener to speak (called by room owner).

>? After a listener becomes a speaker following the room owner's invitation, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```Objective-C
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat that the listener is invited to take |
| userId | String | User ID |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the seat list. In cases where the room owner needs listeners' consent to make them speakers, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `pickSeat`.


### kickSeat

This API is used to remove a speaker (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```Objective-C
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat from which the speaker is to be removed |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the speaker list.

### muteSeat

This API is used to mute/unmute a seat (called by room owner).

>? After a seat is muted/unmuted, all members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.

```Objective-C
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | int            | The number of the seat to mute/unmute                          |
| isMute    | boolean        | `true`: mute; `false`: unmute |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will call `muteAudio` to mute/unmute his or her audio.

### closeSeat

This API is used to block/unblock a seat (called by room owner).

>? After a seat is blocked/unblocked, all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.

```Objective-C
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | int            | The number of the seat to block/unblock                          |
| isClose   | boolean        | `true`: block; `false`: unblock |
| callback | ActionCallback | Callback for operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will leave the seat.


## Local Audio APIs

### startMicrophone

This API is used to enable mic capturing.

```Objective-C
- (void)startMicrophone;
```

### stopMicrophone

This API is used to stop mic capturing.

```Objective-C
- (void)stopMicrophone;
```

### setAudioQuality

This API is used to set audio quality.

```Objective-C
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int | Audio quality. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute local audio.

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | Mutes/Unmutes. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to turn the speaker on.

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | `true`: speaker; `false`: receiver |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```Objective-C
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---- | ----------------------------- |
| volume | int | Capturing volume. Value range: 0-100 (default: 100) |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ---- | ----------------------------- |
| volume | int | Playback volume. Value range: 0-100 (default: 100) |

### muteRemoteAudio

This API is used to mute/unmute a specified user.

```Objective-C
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | --------------------------------- |
| userId | String | Specified user ID |
| mute | boolean | `true`: mute; `false`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all users.

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | --------------------------------- |
| mute | boolean | `true`: mute; `false`: unmute |

### setVoiceEarMonitorEnable

This API is used to enable/disable in-ear monitoring.

```Objective-C
- (void)setVoiceEarMonitorEnable:(BOOL)enable NS_SWIFT_NAME(setVoiceEarMonitor(enable:));
```
The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | --------------------------------- |
| enable | boolean | `true`: enable; `false`: disable |


## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).

```Objective-C
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in a room, which is generally used for on-screen comments.

```Objective-C
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| message | String | Text message |
| callback | ActionCallback | Callback for operation |

   

### sendRoomCustomMsg

This API is used to send a custom text message.

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------------------------------------------- |
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| callback | ActionCallback | Callback for operation |

   

## Invitation Signaling APIs

### sendInvitation

This API is used to send an invitation.

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userId
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ---------------- |
| cmd      | String         | Custom command of business |
| userId   | String         | Invitee's user ID  |
| content  | String         | Invitation content     |
| callback | ActionCallback | Callback for operation |

Returned value:

| Returned Value | Type | Description |
| -------- | ------ | --------------------- |
| inviteId | String | Invitation ID |

### acceptInvitation

This API is used to accept an invitation.

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(id:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for operation |

### rejectInvitation

This API is used to decline an invitation.

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(id:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for operation |


### cancelInvitation

This API is used to cancel an invitation.

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(id:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for operation |

[](id:TRTCVoiceRoomDelegate)
## TRTCVoiceRoomDelegate Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```Objective-C
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Error message |


### onWarning

Callback for warning.

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Warning message |

   

### onDebugLog

Callback for log.

```Objective-C
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Log information |

   


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the owner terminates the room, all users in the room will receive this callback.

```Objective-C
- (void)onRoomDestroy:(NSString *)roomId
NS_SWIFT_NAME(onRoomDestroy(roomId:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | --------- |
| roomId | String | Room ID |


### onRoomInfoChange

Callback for successful room entry. The information in `roomInfo` is passed in by the room owner during room creation.

```Objective-C
- (void)onRoomInfoChange:(VoiceRoomInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | Room information |


### onUserMicrophoneMute

Callback of whether a user's mic is muted. When a user calls `muteLocalAudio`, all members in the room will receive this callback.

```Objective-C
- (void)onUserMicrophoneMute:(NSString *)userId mute:(BOOL)mute
NS_SWIFT_NAME(onUserMicrophoneMute(userId:mute:));

```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------------------------- |
| userId | String | User ID |
| mute | boolean    | Volume. Value range: 0-100 |


### onUserVolumeUpdate

Callback of the volume of each member in the room after the volume reminder is enabled.

```Objective-C
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------ | ------------------------- |
| userVolumes | List | List of user IDs                 |
| totalVolume | int    | Volume. Value range: 0-100 |


## Seat Callback APIs

### onSeatListChange

Callback for all seat changes.

```Objective-C
- (void)onSeatInfoChange:(NSArray<VoiceRoomSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | -------------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | Full seat list |

### onAnchorEnterSeat

Someone became a speaker after requesting or being invited by the room owner.

```Objective-C
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | -------- | -------------------- |
| index | int      | The seat taken     |
| user  | UserInfo | Details of the user who took the seat |

### onAnchorLeaveSeat

A speaker became a listener or was moved to listeners by the room owner.

```Objective-C
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | -------- | -------------------- |
| index | int      | The seat previously occupied by the speaker         |
| user  | UserInfo | Details of the user who took the seat |

### onSeatMute

The room owner muted a seat.

```Objective-C
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------ | ------- | ---------------------------------- |
| index  | int     | The seat muted                       |
| isMute | boolean | `true`: muted; `false`: unmuted |

### onSeatClose

The room owner blocked a seat.

```Objective-C
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------- | ----------------------------------- |
| index   | int     | The seat blocked                        |
| isClose | boolean | `true`: blocked; `false`: unblocked |

## Callback APIs for Room Entry/Exit by Listener

### onAudienceEnter

A listener entered the room.

```Objective-C
- (void)onAudienceEnter:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the user who entered the room |

### onAudienceExit

A listener exited the room.

```Objective-C
- (void)onAudienceExit:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who exited the room |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | ---------------- |
| message | String | Text message |
| userInfo | UserInfo | Information of sender |

   

### onRecvRoomCustomMsg

A custom message was received.

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)command
                    message:(NSString *)message
                   userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(command:message:userInfo:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------- | -------------------------------------------------- |
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| userInfo | UserInfo | Information of sender                                   |

## Invitation Signaling Event Callbacks

### onReceiveNewInvitation

An invitation was received.

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(id:inviter:cmd:content:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | -------- | ---------------------------------- |
| id      | String   | Invitation ID                          |
| inviter | String   | Inviter's user ID                  |
| cmd     | String   | Custom command word specified by business |
| content | UserInfo | Content specified by business                   |

### onInviteeAccepted

The invitee accepted the invitation.

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(id:invitee:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id      | String | Invitation ID           |
| invitee | String | Invitee's user ID |

### onInviteeRejected

The invitee declined the invitation.

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(id:invitee:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id      | String | Invitation ID           |
| invitee | String | Invitee's user ID |

### onInvitationCancelled

The inviter canceled the invitation.

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(id:invitee:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ----------------- |
| id      | String | Invitation ID         |
| inviter | String | Inviter's user ID |
