`TRTCChorusRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a room and start streaming as the room owner, or enter a room as audience to listen or sing together with the room owner.
- The room owner can manage song requests, invite a listener to speak, remove a speaker, and start a duet.
- The room owner can also block a seat. Listeners cannot request to take a blocked seat.
- A listener can request to sing and become the co-singer, and the co-singer can become a listener after a duet ends.
- All users can send gifts and text and custom messages. Custom messages can be used to send on-screen comments and give likes.

`TRTCChorusRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Duet (Android)](https://intl.cloud.tencent.com/document/product/647/42688).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio chat component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the seat list, and invitation signaling is used to send requests to speak or invite others to speak.

[](id:TRTCChorusRoom)
## `TRTCChorusRoom` API Overview

### Basic SDK APIs

| API       | Description       |
| ------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets a singleton object. |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |
| [delegateQueue](#delegatequeue) | Sets the thread where event callbacks are. |
| [login](#login) | Logs in. |
| [logout](#logout) | Logs out. |
| [setSelfProfile](#setselfprofile) | Sets the profile. |

### Room APIs

| API | Description |
| -------------- | ----------- |
| [createRoom](#createroom) | Creates a room (called by room owner). If the room does not exist, the system will automatically create a room. |
| [destroyRoom](#destroyroom) | Terminates a room (called by room owner). |
| [enterRoom](#enterroom) | Enters a room (called by listener). |
| [exitRoom](#exitroom) | Exits a room (called by listener). |
| [getRoomInfoList](#getroominfolist) | Gets room list details.|
| [getUserInfoList](#getuserinfolist) | Gets the user information of the specified `userId`. If the value is `nil`, the information of all users in the room is obtained. |

### Music playback APIs

| API                                             | Description                                                         |
| -------------- | --------------- |
| [startPlayMusic](#startPlayMusic)   | Starts music playback. |
| [stopPlayMusic](#stopPlayMusic)     | Stops music playback. |
| [pausePlayMusic](#pausePlayMusic)   | Pauses music playback.|
| [resumePlayMusic](#resumePlayMusic) | Resumes music playback.|

### Seat management APIs

| API                                             | Description                                                         |
| ----------------------- | -------------- |
| [enterSeat](#enterseat) | Becomes a speaker (called by room owner or listener). |
| [leaveSeat](#leaveseat) | Becomes a listener (called by speaker).|
| [pickSeat](#pickseat)   | Places a user in a seat (called by room owner).                  |
| [kickSeat](#kickseat)   | Removes a speaker (called by room owner).                  |
| [closeSeat](#closeseat) | Blocks/Unblocks a seat (called by room owner).          |

### Local audio APIs

| API                                             | Description                                                         |
| ------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Starts mic capturing.     |
| [stopMicrophone](#stopmicrophone)  | Stops mic capturing. |
| [setAudioQuality](#setaudioquality) | Sets audio quality. |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker) | Sets whether to use the speaker or receiver.|
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume. |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | Enables/Disables in-ear monitoring.       |


### Background music and audio effect APIs

| API     | Description |
| ------------------- | ----------- |
| [getAudioEffectManager](#getaudioeffectmanager) | Gets the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager). |

### Message sending APIs

| API     | Description |
| ------------------ | ------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text message in a room. This API is generally used for on-screen comments. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text message. |

### Invitation signaling APIs

| API                                             | Description                                                         |
| ---------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | Sends an invitation. |
| [acceptInvitation](#acceptinvitation) | Accepts an invitation.       |
| [rejectInvitation](#rejectinvitation) | Declines an invitation.       |
| [cancelInvitation](#cancelinvitation) | Cancels an invitation.       |

<h2 id="TRTCChorusRoomDelegate">`TRTCChorusRoomDelegate` API Overview</h2>

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------- |
| [onError](#onerror) | Error |
| [onWarning](#onwarning) | Warning |
| [onDebugLog](#ondebuglog) | Log|

### Room event callback APIs

| API                                             | Description                                                         |
| -------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy) | The room was terminated.|
| [onRoomInfoChange](#onroominfochange)     | The room information changed. |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Seat list change callback APIs

| API                                             | Description                                                         |
| ------------------ | ---------------- |
| [onSeatListChange](#onseatlistchange)   | All seat changes                |
| [onAnchorEnterSeat](#onanchorenterseat) | Someone became a speaker or was made a speaker by the room owner. |
| [onAnchorLeaveSeat](#onanchorleaveseat) | Someone became a listener or was moved to listeners by the room owner. |
| [onUserMicrophoneMute](#onusermicrophonemute)               | Whether a user’s mic is muted                          |
| [onSeatClose](#onseatclose)             | The room owner blocked a seat.|

### Callback APIs for room entry/exit by listener

| API                                             | Description                                                         |
| -------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | A listener entered the room. |
| [onAudienceExit](#onaudienceexit) | A listener exited the room. |

### Message event callback APIs

| API                                             | Description                                                         |
| ---------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | A text message was received.|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | A custom message was received.|

### Signaling event callback APIs

| API                                             | Description                                                         |
| --------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | A new invitation was received.   |
| [onInviteeAccepted](#oninviteeaccepted)           | The invitee accepted the invitation.   |
| [onInviteeRejected](#oninviteerejected)           |  The invitee declined the invitation.   |
| [onInvitationCancelled](#oninvitationcancelled)   | The inviter canceled the invitation. |

### Song event callback APIs

| API                                             | Description                                                         |
| --------------------- | ----------------- |
| [onMusicProgressUpdate](#onMusicProgressUpdate)   | Music playback progress |
| [onMusicPrepareToPlay](#onMusicPrepareToPlay)     | Music playback is ready. |
| [onMusicCompletePlaying](#onMusicCompletePlaying) | Music playback was completed. |
| [onReceiveAnchorSendChorusMsg](#onReceiveAnchorSendChorusMsg) | The room owner sent a duet message. |

## Basic SDK APIs

[](id:sharedInstance)

### sharedInstance

This API is used to get a [TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940) singleton object.

```ObjectiveC
/**
* Get a `TRTCChorus` singleton object
*
* - returns: `TRTCChorus` instance
* - note: You can call {@link TRTCChorus#destroySharedInstance()} to terminate a singleton object.
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

This API is used to terminate a [TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940) singleton object.

>?After the instance is terminated, the externally cached `TRTCChorus` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

```ObjectiveC
/**
* Terminate a `TRTCChorus` singleton object
*
* - note: After the instance is terminated, the externally cached `TRTCChorus` instance can no longer be used. You need to call {@link TRTCChorus#sharedInstance()} again to get a new instance.
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

This API is used to set the event callbacks of [TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940). You can use `TRTCChorusDelegate` to get different status notifications of [TRTCChorus](https://intl.cloud.tencent.com/document/product/647/41940).

```ObjectiveC
/**
* Set the event callbacks of the component
* 
* You can use `TRTCChorusDelegate` to get different status notifications of `TRTCChorus`.
*
* - parameter delegate Callback API
* - note: Event callbacks in `TRTCChorus` are sent to you in the main queue by default. If you need to specify a queue for event callbacks, please use {@link TRTCChorus#setDelegateQueue(queue)}.
*/
- (void)setDelegate:(id<TRTCChorusDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?`setDelegate` is the delegate callback of `TRTCChorus`.   

### setDelegateQueue

This API is used to set the thread queue for event callbacks. The main thread (MainQueue) is used by default.

```ObjectiveC
/**
* Set the queue for event callbacks
*
* - parameter queue. The status notifications of `TRTCChorus` will be sent to the queue you specify.
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | ---------------- | ----------- |
| queue | dispatch_queue_t | The status notifications of `TRTCChorus` will be sent to the thread queue you specify. |

   

### login

This API is used to log in.

```ObjectiveC
- (void)login:(int)sdkAppID
       userId:(NSString *)userId
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ----------- |
| sdkAppId | int | You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For more information on how to get it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The code is `0` if login succeeds. |

   

### logout

This API is used to log out.

```ObjectiveC
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | Callback for logout. The code is `0` if logout succeeds. |

   

### setSelfProfile

This API is used to set the profile.

```ObjectiveC
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | -------------- |
| userName | String | Username|
| avatarURL | String | Profile photo URL|
| callback | ActionCallback | Callback for profile setting. The code is `0` if the operation succeeds. |

   


## Room APIs

### createRoom

This API is used to create a room (called by room owner).

```ObjectiveC
- (void)createRoom:(int)roomID roomParam:(RoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | ------------------- | ----------- |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a room list. Currently, Tencent Cloud does not provide management services for room lists. Please manage the list on your own. |
| roomParam | TRTCCreateRoomParam | Room information, such as room name, seat list information, and cover information. To manage seats, you must enter the number of seats in the room. |
| callback | ActionCallback | Callback for room creation. The code is `0` if the operation succeeds.  |

The process of creating a room and becoming a speaker is as follows: 
1. A user calls `createRoom` to create a room, passing in room attributes (e.g., room ID, whether listeners need room owner’s consent to speak, number of seats).
2. After creating the room, the user calls `enterSeat` to become a speaker.
3. The user will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
4. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

   

### destroyRoom

This API is used to terminate a room (called by room owner).

```ObjectiveC
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

The parameters are as detailed below:

| Parameter     | Type   | Description                     |
| -------- | -------------- | ---------------- |
| callback | ActionCallback | Callback for room termination. The code is `0` if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by listener).

```ObjectiveC
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

The parameters are as detailed below:

| Parameter     | Type   | Description                     |
| -------- | -------------- | ---------------- |
| roomId | int | Room ID |
| callback | ActionCallback | Callback for room entry. The code is `0` if the operation succeeds. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest room list from your server. The list may contain the `roomId` and room information of multiple rooms.
2. The user selects a room, and calls `enterRoom` with the room ID passed in to enter.
3. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner’s consent is required for listeners to speak, etc.
4. The user will receive an `onSeatListChange` notification about the change of the seat list and can update the change to the UI.
5. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker.

### exitRoom

This API is used to exit a room.

```ObjectiveC
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

The parameters are as detailed below:

| Parameter     | Type   | Description                     |
| -------- | -------------- | ---------------- |
| callback | ActionCallback | Callback for room exit. The code is `0` if the operation succeeds. |

   

### getRoomInfoList

This API is used to get room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?You don’t need this API if both the room list and room information are managed on your server.


```ObjectiveC
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(ChorusInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | Room ID list |
| callback | RoomInfoCallback | Callback of room details |


### getUserInfoList

This API is used to get the user information of a specified `userId`.

```ObjectiveC
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(ChorusUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------------- | ------------------ | ----------- |
| userIdList       | List&lt;String&gt; | IDs of the users to query. If this parameter is `null`, the information of all users in the room is queried. |
| userlistcallback | UserListCallback   | Callback of user details                                           |


## Music Playback APIs

### startPlayMusic

This API is used to play music (called after mic-on).
>?
>- After music playback starts, you will receive an `onMusicPrepareToPlay` notification.
>- During music playback, all members in the room will keep receiving an `onMusicProgressUpdate` notification.
>- After music playback stops, you will receive an `onMusicCompletePlaying` notification.

```ObjectiveC
- (void)startPlayMusic:(int32_t)musicID url:(NSString *)url NS_SWIFT_NAME(startPlayMusic(musicID:url:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | -------------------- |
| musicID | int32_t        | Music ID |
| url     | String  | Absolute path of the music track |

After this API is called, the song being played will stop.

### stopPlayMusic

This API is used to stop music (called during music playback).
>?After music playback stops, you will receive an `onMusicCompletePlaying` notification.

```ObjectiveC
- (void)stopPlayMusic NS_SWIFT_NAME(stopPlayMusic());
```

### pausePlayMusic

This API is used to pause music (called during music playback).
>? 
>- The `onMusicProgressUpdate` notification will be paused.
>- No `onMusicCompletePlaying` notification will be received.

```ObjectiveC
- (void)pausePlayMusic NS_SWIFT_NAME(pausePlayMusic());
```

### resumePlayMusic

This API is used to resume music (called after pause).
>?No `onMusicPrepareToPlay` notification will be received.

```ObjectiveC
- (void)resumePlayMusic NS_SWIFT_NAME(resumePlayMusic());
```

## Seat Management APIs

### enterSeat

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```ObjectiveC
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

The parameters are as detailed below:

| Parameter       | Type   | Description                     |
| --------- | -------------- | -------------------- |
| seatIndex | int            | The number of the seat to take |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where listeners need the room owner’s consent to speak, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `enterSeat`.

### leaveSeat

This API is used to become a listener (called by speaker).

>? After a speaker becomes a listener, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```ObjectiveC
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for the operation |

### pickSeat

This API is used to place a user in a seat (called by room owner).

>? After the room owner places a user in a seat, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```ObjectiveC
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat to place the listener in |
| userId | String | User ID |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where the room owner needs listeners’ consent to make them speakers, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `pickSeat`.


### kickSeat

This API is used to remove a speaker (called by room owner).

>? After a speaker is removed, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```ObjectiveC
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ---------------------- |
| seatIndex | int            | The number of the seat to remove the speaker from |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list.

### muteSeat

This API is used to mute/unmute a seat (called by room owner).

>? After a seat is muted/unmuted, all members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.

```ObjectiveC
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

The parameters are as detailed below:

| Parameter       | Type   | Description                     |
| --------- | -------------- | ------------------------ |
| seatIndex | int            | The number of the seat to mute/unmute                          |
| isMute    | boolean        | `true`: mute; `false`: unmute |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will call `muteAudio` to mute/unmute his or her audio.

### closeSeat

This API is used to block/unblock a seat (called by room owner).

>? After a seat is blocked/unblocked, all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.

```ObjectiveC
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | --------------------- |
| seatIndex | int            | The number of the seat to block/unblock                          |
| isClose   | boolean        | `true`: block; `false`: unblock |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will leave the seat.


## Local Audio APIs

### startMicrophone

This API is used to start mic capturing.

```ObjectiveC
- (void)startMicrophone;
```

### stopMicrophone

This API is used to stop mic capturing.

```ObjectiveC
- (void)stopMicrophone;
```

### setAudioQuality

This API is used to set audio quality.

```ObjectiveC
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ----------- |
| quality | int | Audio quality. For more information, please see [setAudioQuality()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute local audio.

```ObjectiveC
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ----------- |
| mute | boolean | Whether to mute or unmute audio. For more information, please see [muteLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to set whether to use the speaker or receiver.

```ObjectiveC
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | `true`: speaker; `false`: receiver |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```ObjectiveC
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------- |
| volume | int | Capturing volume. Value range: 0-100 (default: 100) |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```ObjectiveC
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------- |
| volume | int | Playback volume. Value range: 0-100 (default: 100) |

### muteRemoteAudio

This API is used to mute/unmute a specified user.

```ObjectiveC
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | ------------ |
| userId | String | User ID |
| mute | boolean | `true`: mute; `false`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all users.

```ObjectiveC
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------- | ------------ |
| mute | boolean | `true`: mute; `false`: unmute |

### setVoiceEarMonitorEnable

This API is used to enable/disable in-ear monitoring.

```ObjectiveC
- (void)setVoiceEarMonitorEnable:(BOOL)enable NS_SWIFT_NAME(setVoiceEarMonitor(enable:));
```
The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---- | ------- | ------------ |
| enable | boolean | `true`: enable; `false`: disable |


## Background Music and Audio Effect APIs

### getAudioEffectManager

This API is used to get the background music and audio effect management object [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa).

```ObjectiveC
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## Message Sending APIs

### sendRoomTextMsg

This API is used to broadcast a text message in a room, which is generally used for on-screen comments.

```ObjectiveC
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| message | String | Text message |
| callback | ActionCallback | Callback for the operation |

   

### sendRoomCustomMsg

This API is used to send a custom text message.

```ObjectiveC
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ---------------------- |
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| callback | ActionCallback | Callback for the operation |

   

## Invitation Signaling APIs

### sendInvitation

This API is used to send an invitation.

```ObjectiveC
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userId
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

The parameters are as detailed below:

| Parameter       | Type   | Description                     |
| -------- | -------------- | ---------------- |
| cmd      | String         | Custom command of business |
| userId   | String         | Invitee’s user ID  |
| content  | String         | Invitation content     |
| callback | ActionCallback | Callback for the operation |

Response parameters:

| Returned Value | Type | Description |
| -------- | ------ | --------------------- |
| inviteId | String | Invitation ID |

### acceptInvitation

This API is used to accept an invitation.

```ObjectiveC
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(identifier:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for the operation |

### rejectInvitation

This API is used to decline an invitation.

```ObjectiveC
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(identifier:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for the operation |


### cancelInvitation

This API is used to cancel an invitation.

```ObjectiveC
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(identifier:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for the operation |

[](id:TRTCChorusDelegate)
## `TRTCChorusDelegate` Event Callback APIs

## Common Event Callback APIs

### onError

Callback for error.

>? This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```ObjectiveC
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Error message |


### onWarning

Callback for warning.

```ObjectiveC
- (void)onWarning:(int)code
                  message:(NSString *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Warning message |

   

### onDebugLog

Callback for log.

```ObjectiveC
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| message | String | Log information |

   


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the owner terminates the room, all users in the room will receive this callback.

```ObjectiveC
- (void)onRoomDestroy:(NSString *)message
NS_SWIFT_NAME(onRoomDestroy(message:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------ | --------- |
| roomId | String | Room ID |


### onRoomInfoChange

Callback for change of room information. This callback is sent after successful room entry. The information in `roomInfo` is passed in by the room owner during room creation.

```ObjectiveC
- (void)onRoomInfoChange:(ChorusInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | Room information |


### onUserVolumeUpdate

Callback of the volume of each member in the room after the volume reminder is enabled.

```ObjectiveC
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | ------------------------- |
| userVolumes | List | List of user volumes                 |
| totalVolume | int    | Total volume. Value range: 0-100 |


## Seat Callback APIs

### onSeatListChange

Callback for all seat changes.

```ObjectiveC
- (void)onSeatInfoChange:(NSArray<ChorusSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | -------------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | Full seat list |

### onAnchorEnterSeat

Someone became a speaker or was made a speaker by the owner.

```ObjectiveC
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(ChorusUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | -------- | -------------------- |
| index | int      | The seat taken     |
| user | UserInfo | Details of the user who took the seat |

### onAnchorLeaveSeat

A speaker became a listener or was moved to listeners by the room owner.

```ObjectiveC
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(ChorusUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | -------- | -------------------- |
| index | int      | The seat previously occupied by the speaker         |
| user | UserInfo | Details of the user who took the seat |

### onSeatMute

The room owner muted/unmuted a seat.

```ObjectiveC
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | ------------- |
| index  | int     | The seat muted/unmuted                       |
| isMute | boolean | `true`: muted; `false`: unmuted |

### onSeatClose

The room owner blocked/unblocked a seat.

```ObjectiveC
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------- | -------------- |
| index   | int     | The seat blocked/unblocked                        |
| isClose | boolean | `true`: blocked; `false`: unblocked |

## Callback APIs for Room Entry/Exit by Listener

### onAudienceEnter

A listener entered the room.

```ObjectiveC
- (void)onAudienceEnter:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description  |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who entered the room |

### onAudienceExit

A listener exited the room.

```ObjectiveC
- (void)onAudienceExit:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description  |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who exited the room |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.

```ObjectiveC
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------------- |
| message | String | Text message |
| userInfo | UserInfo | Information of the sender |

   

### onRecvRoomCustomMsg

A custom message was received.

```ObjectiveC
- (void)onRecvRoomCustomMsg:(NSString *)cmd
                    message:(NSString *)message
                   userInfo:(ChorusUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(cmd:message:userInfo:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------------------- |
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| userInfo | UserInfo | Information of the sender |

## Invitation Signaling Callback APIs

### onReceiveNewInvitation

An invitation was received.

```ObjectiveC
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(identifier:inviter:cmd:content:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | -------- | ------------- |
| id      | String   | Invitation ID                          |
| inviter | String   | Inviter’s user ID                  |
| cmd     | String   | Custom command word specified by business |
| content | UserInfo | Content specified by business                   |

### onInviteeAccepted

The invitee accepted the invitation

```ObjectiveC
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(identifier:invitee:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id      | String | Invitation ID           |
| invitee | String | Invitee’s user ID |

### onInviteeRejected

The invitee declined the invitation

```ObjectiveC
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(identifier:invitee:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------- |
| id      | String | Invitation ID           |
| invitee | String | Invitee’s user ID |

### onInvitationCancelled

The inviter canceled the invitation.

```ObjectiveC
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(identifier:invitee:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ----------------- |
| id      | String | Invitation ID           |
| inviter | String | Inviter’s user ID |

## Music Playback Status Callback APIs

### onMusicPrepareToPlay

Music playback is ready.

```ObjectiveC
- (void)onMusicPrepareToPlay:(int32_t)musicID
NS_SWIFT_NAME(onMusicPrepareToPlay(musicID:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------- | -------------------- |
| musicID | int32_t | `musicID` passed in for playback  |

### onMusicProgressUpdate

Music playback progress.

```ObjectiveC
- (void)onMusicProgressUpdate:(int32_t)musicID
                     progress:(NSInteger)progress total:(NSInteger)total
NS_SWIFT_NAME(onMusicProgressUpdate(musicID:progress:total:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | --------- | -------------------- |
| musicID | int32_t | `musicID` passed in for playback  |
| progress | NSInteger | Current playback progress in ms |
| total    | NSInteger | Total duration in ms      |

### onMusicCompletePlaying

Music playback was completed.

```ObjectiveC
- (void)onMusicCompletePlaying:(int32_t)musicID
NS_SWIFT_NAME(onMusicCompletePlaying(musicID:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | --------- | -------------------- |
| musicID | int32_t | `musicID` passed in for playback  |

### onReceiveAnchorSendChorusMsg

The room owner sent a duet message.

```ObjectiveC
- (void)onReceiveAnchorSendChorusMsg:(NSString *)musicId startDelay:(NSInteger)startDelay
NS_SWIFT_NAME(onReceiveAnchorSendChorusMsg(musicId:startDelay:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | --------- | -------------------- |
| musicId  | NSString   | `musicID` of the song to sing |
| startDelay  | NSInteger   | Time (s) to wait before the song is played |
