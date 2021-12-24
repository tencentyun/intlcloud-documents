`TRTCKaraokeRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:

- A user can create a karaoke room and become a speaker, or enter a karaoke room as a listener.
- The room owner can manage song requests as well as remove a speaker.
- The room owner can also block a seat. Listeners cannot request to take a blocked seat.
- A listener can become a speaker to request songs and sing. A speaker can also become a listener.
- All users can send gifts and text and custom messages. Custom messages can be used to send on-screen comments and give likes.

`TRTCKaraokeRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Karaoke (iOS)](https://intl.cloud.tencent.com/document/product/647/41940).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio chat component.
- IM SDK: the `AVChatRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms. The attribute APIs of IM are used to store room information such as the seat list, and invitation signaling is used to send requests to speak or invite others to speak.

[](id:TRTCKaraokeRoom)
## `TRTCKaraokeRoom` API Overview

### Basic SDK APIs

| API | Description |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets a singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |
| [delegateQueue](#delegatequeue)   | Sets the thread where event callbacks are. |
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

### Music playback APIs

| API                                             | Description                                                         |
| ----------------------------------- | --------------- |
| [startPlayMusic](#startplaymusic)   | Starts music.     |
| [stopPlayMusic](#stopplaymusic)     | Stops music.     |
| [pausePlayMusic](#pauseplaymusic)   | Pauses music.     |
| [resumePlayMusic](#resumeplaymusic) | Resumes music.     |

### Seat management APIs

| API                                             | Description                                                         |
| ----------------------- | ----------------------------------- |
| [enterSeat](#enterseat) | Becomes a speaker (called by room owner or listener). |
| [leaveSeat](#leaveseat) | Becomes a listener (called by speaker).    |
| [pickSeat](#pickseat)   | Places a user in a seat (called by room owner).                  |
| [kickSeat](#kickseat)   | Removes a speaker (called by room owner).                  |
| [muteSeat](#muteseat)   | Mutes/Unmutes a seat (called by room owner). |
| [closeSeat](#closeseat) | Blocks/Unblocks a seat (called by room owner).          |

### Local audio APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Starts mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [setAudioQuality](#setaudioquality)             | Sets audio quality.           |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker)                       | Sets whether to use the speaker or receiver.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume.       |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | Enables/Disables in-ear monitoring.       |


### Remote audio APIs

| API                                             | Description                                                         |
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

[](id:TRTCKaraokeRoomDelegate)
## `TRTCKaraokeRoomDelegate` API Overview

### Common event callback APIs

| API                                             | Description                                                         |
| ------------------------- | ---------- |
| [onError](#onerror) | Error |
| [onWarning](#onwarning) | Warning |
| [onDebugLog](#ondebuglog) | Log|

### Room event callback APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)     | The room was terminated.       |
| [onRoomInfoChange](#onroominfochange)     | The room information changed. |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Seat list change callback APIs

| API                                     | Description                                  |
| --------------------------------------- | ------------------------------------- |
| [onSeatListChange](#onseatlistchange)   | All seat changes                |
| [onAnchorEnterSeat](#onanchorenterseat) | Someone became a speaker or was made a speaker by the room owner. |
| [onAnchorLeaveSeat](#onanchorleaveseat) | Someone became a listener or was moved to listeners by the room owner. |
| [onSeatMute](#onseatmute) | The room owner muted a seat. |
| [onUserMicrophoneMute](#onusermicrophonemute)               | Whether a user’s mic is muted                          |
| [onSeatClose](#onseatclose)             | The room owner blocked a seat.                          |

### Callback APIs for room entry/exit by listener

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

| API                                             | Description                                                         |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | Receipt of an invitation |
| [onInviteeAccepted](#oninviteeaccepted)           | Invitation accepted by invitee   |
| [onInviteeRejected](#oninviteerejected)           |  Invitation declined by invitee   |
| [onInvitationCancelled](#oninvitationcancelled)   | Invitation canceled by inviter |

### Song event callback APIs

| API                                             | Description                                                         |
| ------------------------------------------------- | ----------------- |
| [onMusicProgressUpdate](#onmusicprogressupdate)   | Music playback progress |
| [onMusicPrepareToPlay](#onmusicpreparetoplay)     | Music playback is ready. |
| [onMusicCompletePlaying](#onmusiccompleteplaying) | Music playback was completed. |

## Basic SDK APIs

[](id:sharedInstance)

### sharedInstance

This API is used to get a [TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41940) singleton object.

```Objective-C
/**
* Get a `TRTCKaraokeRoom` singleton object
*
* - returns: `TRTCKaraokeRoom` instance
* - note: To terminate a singleton object, call {@link TRTCKaraokeRoom#destroySharedInstance()}.
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

This API is used to terminate a [TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41940) singleton object.

>?After the instance is terminated, the externally cached `TRTCKaraokeRoom` instance can no longer be used. You need to call [sharedInstance](#sharedInstance) again to get a new instance.

```Objective-C
/**
* Terminate the `TRTCKaraokeRoom` singleton object
*
* - note: After the instance is terminated, the externally cached `TRTCKaraokeRoom` instance can no longer be used. You need to call {@link TRTCKaraokeRoom#sharedInstance()} again to get a new instance.
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

This API is used to set the event callbacks of [TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41940). You can use `TRTCKaraokeRoomDelegate` to get different status notifications of [TRTCKaraokeRoom](https://intl.cloud.tencent.com/document/product/647/41940).

```Objective-C
/**
* Set the event callbacks of the component
* 
* You can use `TRTCKaraokeRoomDelegate` to get different status notifications of `TRTCKaraokeRoom`.
*
* - parameter delegate Callback API
* - note: Callbacks in `TRTCKaraokeRoom` are sent to you in the main queue by default. If you need to specify a queue for event callbacks, please use {@link TRTCKaraokeRoom#setDelegateQueue(queue)}.
*/
- (void)setDelegate:(id<TRTCKaraokeRoomDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?`setDelegate` is the delegate callback of `TRTCKaraokeRoom`.   

### setDelegateQueue

This API is used to set the thread queue for event callbacks. The main thread (MainQueue) is used by default.

```Objective-C
/**
* Set the queue for event callbacks
*
* - parameter queue. The status notifications of `TRTCKaraokeRoom` will be sent to the queue you specify.
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | The status notifications of `TRTCKaraokeRoom` are sent to the thread queue you specify. |

   

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
| userId | String | ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For more information on how to get it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The code is 0 if login succeeds. |

   

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

This API is used to set the profile.

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ----------------------------------- |
| userName | String | Username|
| avatar | String | Profile photo address |
| callback | ActionCallback | Callback for profile setting. The code is 0 if the operation succeeds. |

   


## Room APIs

### createRoom

This API is used to create a room (called by room owner).

```Objective-C
- (void)createRoom:(int)roomID roomParam:(RoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId | int | Room ID. You need to assign and manage the IDs in a centralized manner. Multiple `roomID` values can be aggregated into a karaoke room list. Currently, Tencent Cloud does not provide management services for room lists. Please manage the list on your own. |
| roomParam | TRTCCreateRoomParam | Room information, such as room name, seat list information, and cover information. To manage seats, you must enter the number of seats in the room. |
| callback | ActionCallback | Callback for room creation result. The code is 0 if the operation succeeds.  |

The process of creating a karaoke room and becoming a speaker is as follows: 
1. A user calls `createRoom` to create a karaoke room, passing in room attributes (e.g., room ID, whether listeners need room owner’s consent to speak, number of seats).
2. After creating the room, the user calls `enterSeat` to become a speaker.
3. The user will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
4. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

   

### destroyRoom

This API is used to terminate a room (called by room owner).

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room termination. The code is `0` if the operation succeeds. |


### enterRoom

This API is used to enter a room (called by listener).

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ------------------------------------- |
| roomId | int | Room ID |
| callback | ActionCallback | Callback for room entry. The code is `0` if the operation succeeds. |


The process of entering a room as a listener is as follows: 

1. A user gets the latest karaoke room list from your server. The list may contain the `roomId` and room information of multiple karaoke rooms.
2. The user selects a room, and calls `enterRoom` with the room ID passed in to enter.
3. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner’s consent is required for listeners to speak, etc.
4. The user will receive an `onSeatListChange` notification about the change of the seat list and can update the change to the UI.
5. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker.

### exitRoom

This API is used to exit a room.

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | Callback for room exit. The code is `0` if the operation succeeds. |

   

### getRoomInfoList

This API is used to get room list details. The room name and cover are set by the room owner via `roomInfo` when calling `createRoom()`.

>?You don’t need this API if both the room list and room information are managed on your server.


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(KaraokeInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | Room ID list |
| callback | RoomInfoCallback | Callback of room details |


### getUserInfoList

This API is used to get the user information of a specified `userId`.

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(KaraokeUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List | IDs of the users to query. If this parameter is `null`, the information of all users in the room is obtained. |
| userlistcallback | UserListCallback   | Callback of user details                                           |


## Music Playback APIs

### startPlayMusic

This API is used to play music (called after mic-on).
>?
>- After music playback starts, you will receive an `onMusicPrepareToPlay` notification.
>- During music playback, all members in the room will keep receiving an `onMusicProgressUpdate` notification.
>- After music playback stops, you will receive an `onMusicCompletePlaying` notification.

```Objective-C
- (void)startPlayMusic:(int32_t)musicID originalUrl:(NSString *)originalUrl accompanyUrl:(NSString *)backingUrl NS_SWIFT_NAME(startPlayMusic(musicID:originalUrl:accompanyUrl:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | -------------------- |
| musicID | int32_t        | Music ID |
|originalUrl  | String | Absolute path of the vocal track   |
|accompanyUrl |  String | Absolute path of the instrumental track  |

After this API is called, the song being played will stop.

### stopPlayMusic

This API is used to stop music (called during music playback).
>?After music playback stops, you will receive an `onMusicCompletePlaying` notification.

```Objective-C
- (void)stopPlayMusic NS_SWIFT_NAME(stopPlayMusic());
```

### pausePlayMusic

This API is used to pause music (called during music playback).
>?
>- The `onMusicProgressUpdate` notification will be paused.
>- No `onMusicCompletePlaying` notification will be received.

```Objective-C
- (void)pausePlayMusic NS_SWIFT_NAME(pausePlayMusic());
```

### resumePlayMusic

This API is used to resume music (called after pause).
>?No `onMusicPrepareToPlay` notification will be received.

```Objective-C
- (void)resumePlayMusic NS_SWIFT_NAME(resumePlayMusic());
```

## Seat Management APIs

### enterSeat

This API is used to become a speaker (called by room owner or listener).

>?After a user becomes a speaker, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```Objective-C
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | -------------------- |
| seatIndex | int            | The number of the seat to take |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. In cases where listeners need the room owner’s consent to speak, you can call `sendInvitation` first to send a request and, after receiving `onInvitationAccept`, call `enterSeat`.

### leaveSeat

This API is used to become a listener (called by speaker).

>? After a speaker becomes a listener, all members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | ---------- |
| callback | ActionCallback | Callback for the operation |

### pickSeat

This API is used to place a user in a seat (called by room owner).

>? After the room owner places a user in a seat, all members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.

```Objective-C
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

```Objective-C
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

```Objective-C
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | int            | The number of the seat to mute/unmute                          |
| isMute    | boolean        | `true`: mute; `false`: unmute |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will call `muteAudio` to mute/unmute his or her audio.

### closeSeat

This API is used to block/unblock a seat (called by room owner).

>? After a seat is blocked/unblocked, all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.

```Objective-C
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | int            | The number of the seat to block/unblock                          |
| isClose   | boolean        | `true`: block; `false`: unblock |
| callback | ActionCallback | Callback for the operation |

Calling this API will immediately modify the seat list. The speaker on the seat specified by `seatIndex` will leave the seat.


## Local Audio APIs

### startMicrophone

This API is used to start mic capturing.

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
| quality | int | Audio quality. For more information, please see [setAudioQuality()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute local audio.

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | Whether to mute or unmute audio. For more information, please see [muteLocalAudio()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to set whether to use the speaker or receiver.

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
- (void)setAudioCaptureVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ----------------------------- |
| volume | int | Capturing volume. Value range: 0-100 (default: 100) |


### setAudioPlayoutVolume

This API is used to set the playback volume.

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
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
| userId | String | User ID |
| mute | boolean | `true`: mute; `false`: unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all users.

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------- | --------------------------------- |
| isMute | boolean | `true`: mute; `false`: unmute |

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

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| message | String | Text message |
| callback | ActionCallback | Callback for the operation |

   

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
| callback | ActionCallback | Callback for the operation |

   

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

| Parameter | Type | Description |
| -------- | -------------- | ---------------- |
| cmd      | String         | Custom command of business |
| userId   | String         | Invitee’s user ID  |
| content  | String         | Invitation content     |
| callback | ActionCallback | Callback for the operation |

Returned value:

| Returned Value | Type | Description |
| -------- | ------ | --------------------- |
| inviteId | String | Invitation ID |

### acceptInvitation

This API is used to accept an invitation.

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(identifier:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for the operation |

### rejectInvitation

This API is used to decline an invitation.

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(identifier:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for the operation |


### cancelInvitation

This API is used to cancel an invitation.

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(identifier:callback:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------------- | -------------- |
| id       | String         | Invitation ID      |
| callback | ActionCallback | Callback for the operation |

[](id:TRTCKaraokeRoomDelegate)
## `TRTCKaraokeRoomDelegate` Event Callback APIs

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

| Parameter        | Type    | Description                                                                                                      |
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

| Parameter        | Type    | Description                                                                                                      |
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

| Parameter        | Type    | Description                                                                                                      |
| ------- | ------ | ---------- |
| message | String | Log information |

   


## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the owner terminates the room, all users in the room will receive this callback.

```Objective-C
- (void)onRoomDestroy:(NSString *)message
NS_SWIFT_NAME(onRoomDestroy(message:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------ | ------ | --------- |
| message | String | Callback information |


### onRoomInfoChange

Callback for change of room information. This callback is sent after successful room entry. The information in `roomInfo` is passed in by the room owner during room creation.

```Objective-C
- (void)onRoomInfoChange:(KaraokeInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | Room information |


### onUserMicrophoneMute

Callback of whether a user’s mic is muted. When a user calls `muteLocalAudio`, all members in the room will receive this callback.

```Objective-C
- (void)onUserMicrophoneMute:(NSString *)userId mute:(BOOL)mute
NS_SWIFT_NAME(onUserMicrophoneMute(userId:mute:));

```

The parameters are as detailed below:

| Parameter | Type | Description |
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

| Parameter | Type | Description |
| ------ | ------ | ------------------------- |
| userVolumes | List | List of user volumes                 |
| totalVolume | int    | Total volume. Value range: 0-100 |


## Seat Callback APIs

### onSeatListChange

Callback for all seat changes.

```Objective-C
- (void)onSeatInfoChange:(NSArray<KaraokeSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------ | -------------------- | ---------------- |
| seatInfoList | List&lt;SeatInfo&gt; | Full seat list |

### onAnchorEnterSeat

Someone became a speaker or was made a speaker by the owner.

```Objective-C
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(KaraokeUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | -------- | -------------------- |
| index | int      | The seat taken     |
| user | UserInfo | Details of the user who took the seat |

### onAnchorLeaveSeat

A speaker became a listener or was moved to listeners by the room owner.

```Objective-C
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(KaraokeUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ----- | -------- | -------------------- |
| index | int      | The seat previously occupied by the speaker         |
| user | UserInfo | Details of the user who became a listener |

### onSeatMute

The room owner muted/unmuted a seat.

```Objective-C
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------- | ---------------------------------- |
| index  | int     | The seat muted/unmuted                       |
| isMute | boolean | `true`: muted; `false`: unmuted |

### onSeatClose

The room owner blocked/unblocked a seat.

```Objective-C
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| ------- | ------- | ----------------------------------- |
| index   | int     | The seat blocked/unblocked                        |
| isClose | boolean | `true`: blocked; `false`: unblocked |

## Callback APIs for Room Entry/Exit by Listener

### onAudienceEnter

A listener entered the room.

```Objective-C
- (void)onAudienceEnter:(KaraokeUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the user who entered the room |

### onAudienceExit

A listener exited the room.

```Objective-C
- (void)onAudienceExit:(KaraokeUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | -------------- |
| userInfo | UserInfo | Information of the listener who exited the room |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(KaraokeUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------------- |
| message | String | Text message |
| userInfo | UserInfo | Information of the sender |

   

### onRecvRoomCustomMsg

A custom message was received.

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)cmd
                    message:(NSString *)message
                   userInfo:(KaraokeUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(cmd:message:userInfo:));
```

The parameters are as detailed below:

| Parameter    | Type   | Description                                                                                                                    |
| -------- | -------- | -------------------------------------------------- |
| command | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| userInfo | UserInfo | Information of the sender                                   |

## Invitation Signaling Callback APIs

### onReceiveNewInvitation

An invitation was received.

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(identifier:inviter:cmd:content:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | -------- | ---------------------------------- |
| id      | String   | Invitation ID                          |
| inviter | String   | Inviter’s user ID                  |
| cmd     | String   | Custom command word specified by business |
| content | UserInfo | Content specified by business                   |

### onInviteeAccepted

The invitee accepted the invitation.

```Objective-C
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

The invitee declined the invitation.

```Objective-C
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

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(identifier:invitee:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ----------------- |
| id      | String | Invitation ID         |
| inviter | String | Inviter’s user ID |

## Music Playback Status Callback APIs

### onMusicPrepareToPlay

Music playback is ready.

```Objective-C
- (void)onMusicPrepareToPlay:(int32_t)musicID
NS_SWIFT_NAME(onMusicPrepareToPlay(musicID:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------- | -------------------- |
| musicID | int32_t | `musicID` passed in for playback  |

### onMusicProgressUpdate

Music playback progress.

```Objective-C
- (void)onMusicProgressUpdate:(int32_t)musicID
                     progress:(NSInteger)progress total:(NSInteger)total
NS_SWIFT_NAME(onMusicProgressUpdate(musicID:progress:total:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------- | -------------------- |
| musicID | int32_t | `musicID` passed in for playback  |
| progress | NSInteger | Current playback progress in ms |
| total    | NSInteger | Total duration in ms      |

### onMusicCompletePlaying

Music playback was completed.

```Objective-C
- (void)onMusicCompletePlaying:(int32_t)musicID
NS_SWIFT_NAME(onMusicCompletePlaying(musicID:));
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------- | -------------------- |
| musicID | int32_t | `musicID` passed in for playback  |
