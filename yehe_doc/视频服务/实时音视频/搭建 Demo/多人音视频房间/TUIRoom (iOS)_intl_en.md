`TUIRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). `TUIRoom` includes the following features:
- The anchor can create a room, and members can enter the room ID to join the room.
- Room members can share their screens with each other.
- All users can send various text and custom messages.

`TUIRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Group Audio/Video Room (for iOS)](https://intl.cloud.tencent.com/document/product/647/37284).
- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video room component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) for **iOS** is used to implement the chat room feature.


## `TUIRoom` API Overview

### Basic functions of `TUIRoomCore`

| API | Description |
| ----------------------------------- | -------------- |
| [shareInstance](#shareinstance)     | Gets a singleton object. |
| [destroyInstance](#destroyinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |

### Room APIs

| API                                             | Description                                                         |
| ----------------------------------------- | ---------------------------------- |
| [createRoom](#createroom)                 | Creates a room (called by anchor).           |
| [destroyRoom](#destroyroom)               | Terminates a room (called by anchor).           |
| [enterRoom](#enterroom) | Enters a room (called by room member). |
| [leaveRoom](#leaveroom)                   | Exits a room (called by other room members). |
| [getRoomInfo](#getroominfo)               | Gets the room information.                     |
| [getRoomUsers](#getroomusers)             | Gets the information of all users in the room.           |
| [getUserInfo](#getuserinfo)               | Gets the information of a user.               |
| [transferRoomMaster](#transferroommaster) | Transfers the anchor permission (called by anchor).     |

### Local audio/video operation APIs

| API | Description |
| ----------------------------------------- | -------------------------- |
| [startCameraPreview](#startcamerapreview) | Enables the preview image of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [startLocalAudio](#startlocalaudio)       | Enables mic capturing.            |
| [stopLocalAudio](#stoplocalaudio)         | Stops mic capturing.           |
| [setVideoMirror](#setvideomirror)         | Sets the mirroring preview mode of the local image. |
| [setSpeaker](#setspeaker)                 | Sets whether to use the speaker or receiver.     |

### Remote user APIs

| API                                             | Description                                                         |
| ----------------------------------- | ---------------------------------- |
| [startRemoteView](#startremoteview) | Subscribes to and plays back the remote video image of a specified member. |
| [stopRemoteView](#stopremoteview)   | Unsubscribes from and stops the playback of a remote video image.   |

### Chat message sending APIs

| API | Description |
| ----------------------------------- | -------------- |
| [sendChatMessage](#sendchatmessage)     | Sends a chat message.   |
| [sendCustomMessage](#sendcustommessage) | Sends a custom message. |

### Room control APIs

| API          | Description         |
| --------------------------------------------------- | ------------------------------------------------------- |
| [muteUserMicrophone](#muteusermicrophone)           | Enables/Disables the mic of a specified user.                               |
| [muteAllUsersMicrophone](#muteallusersmicrophone)   | Enables/Disables the mic of all users and syncs the status to room information. |
| [muteUserCamera](#muteusercamera)                   | Enables/Disables the camera of a specified user.                               |
| [muteAllUsersCamera](#mutealluserscamera)           | Enables/Disables the camera of all users and syncs the status to room information. |
| [muteChatRoom](#mutechatroom)                       | Mutes/Unmutes the chat room (called by anchor).                     |
| [kickOffUser](#kickoffuser)                         | Removes a specified user in the room (called by anchor).                        |
| [startCallingRoll](#startcallingroll)               | Starts calling roll by the anchor.                                        |
| [stopCallingRoll](#stopcallingroll)                 | Stops calling roll by the anchor.                                        |
| [replyCallingRoll](#replycallingroll)               | Replies to roll call by a member.                                    |
| [sendSpeechInvitation](#sendspeechinvitation)       | Invites a member to speak by the anchor.                                    |
| [cancelSpeechInvitation](#cancelspeechinvitation)   | Cancels invitation to a member for speech by the anchor.                                |
| [replySpeechInvitation](#replyspeechinvitation)     | Accepts/Rejects the speech invitation from the anchor by a member.                         |
| [sendSpeechApplication](#sendspeechapplication)     | Applies for speech by a member.                                          |
| [replySpeechApplication](#replyspeechapplication)   | Approves/Rejects the speech application of a member by the anchor.                         |
| [forbidSpeechApplication](#forbidspeechapplication) | Forbids speech application by the anchor.                                    |
| [sendOffSpeaker](#sendoffspeaker)                   | Stops the speech of a member by the anchor.                                  |
| [sendOffAllSpeakers](#sendoffallspeakers)           | Stops the speech of all members by the anchor.                                  |
| [exitSpeechState](#exitspeechstate)                 | Stops speaking by a member and changes their role to audience.                              |

### Screen sharing APIs

| API          | Description         |
|-----|-----|
| [startScreenCapture](#startscreencapture)   | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture)     | Stops screen sharing. |

### Beauty filter APIs

| API          | Description         |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__ios.html). |


### Settings APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | Sets network bandwidth limit parameters. |

### SDK version acquisition APIs

| API | Description |
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | Gets the SDK version. |

## `TUIRoomCoreDelegate` API Overview

### Callbacks for error events

| API  | Description       |
| ------------------- | ---------- |
| [onError](#onerror) | Error|

### Basic event callbacks

| API | Description |
| ------------------------------------------- | ------------------ |
| [onDestroyRoom](#ondestroyroom)             | Room dismissal.     |
| [onUserVoiceVolume](#onuservoicevolume)     | Volume level. |
| [onRoomMasterChanged](#onroommasterchanged) | Anchor change.    |

### Remote user event callbacks

| API                          | Description  |
| ------------------------------------------------------------ | -------------------------------- |
| [onRemoteUserEnter](#onremoteuserenter)                      | A remote user entered the room.           |
| [onRemoteUserLeave](#onremoteuserleave)                      | A remote user exited the room.            |
| [onRemoteUserCameraAvailable](#onremoteusercameraavailable)  | Whether a remote user enabled the camera. |
| [onRemoteUserScreenVideoAvailable](#onremoteuserscreenvideoavailable) | Whether a remote user enabled screen sharing.   |
| [onRemoteUserAudioAvailable](#onremoteuseraudioavailable)    | Whether a remote user enabled sending audio.   |
| [onRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | A remote user started speaking.           |
| [onRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | A remote user stopped speaking.          |

### Message event callback APIs

| API | Description |
| ------------------------------------------------- | ------------------ |
| [onReceiveChatMessage](#onreceivechatmessage) | A text message was received. |

### Room control event callbacks

| API          | Description         |
| ------------------------------------------------------------ | ---------------------------------- |
| [onReceiveSpeechInvitation](#onreceivespeechinvitation)      | A member received a speech invitation from the anchor.       |
| [onReceiveInvitationCancelled](#onreceiveinvitationcancelled) | A member received a speech invitation cancellation from the anchor.    |
| [onReceiveSpeechApplication](#onreceivespeechapplication)    | The anchor received a speech application from a member.     |
| [onSpeechApplicationCancelled](#onspeechapplicationcancelled) | A member canceled a speech application.             |
| [onSpeechApplicationForbidden](#onspeechapplicationforbidden) | The anchor rejected a speech application.           |
| [onOrderedToExitSpeechState](#onorderedtoexitspeechstate)    | A member was asked to stop speaking.         |
| [onCallingRollStarted](#oncallingrollstarted)                | The anchor started a roll call.   |
| [onCallingRollStopped](#oncallingrollstopped)                | The anchor stopped a roll call.   |
| [onMemberReplyCallingRoll](#onmemberreplycallingroll)        | A member replied to roll call.   |
| [onChatRoomMuted](#onchatroommuted)                          | The anchor muted/unmuted the room.     |
| [onMicrophoneMuted](#onmicrophonemuted)                      | The anchor disabled the mic.         |
| [onCameraMuted](#oncameramuted)                              | The anchor disabled the camera.         |
| [onReceiveKickedOff](#onreceivekickedoff)                    | The anchor removed a member.         |


### Callback APIs for statistics on network quality and technical metrics

| API | Description |
| ------------------------------------- | ------------------ |
| [onStatistics](#onstatistics)         | Statistics on technical metrics. |
| [onNetworkQuality](#onnetworkquality) | Network quality.     |

### Screen sharing event callbacks

| API | Description |
| ------------------------------------------------- | ------------------ |
| [onScreenCaptureStarted](#onscreencapturestarted) | Screen sharing started. |
| [onScreenCaptureStopped](#onscreencapturestopped) | Screen sharing stopped. |

## Basic Functions of `TUIRoomCore`

### getInstance

This API is used to get a [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284) singleton object.
```objectivec
+ (instancetype)shareInstance;
```
### destroyInstance

```objectivec
+ (void)destroyInstance;
```

### setDelegate

This API is used to set the event callback of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284). You can use `TUIRoomCoreDelegate` to get different status notifications of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284).

```objectivec
- (void)setDelegate:(id<TUIRoomCoreDelegate>)delegate;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| delegate | TUIRoomCoreDelegate | Event callback class. |

### createRoom

This API is used to create a room (called by the anchor).
```objectivec
- (void)createRoom:(NSString *)roomId
        speechMode:(TUIRoomSpeechMode)speechMode
        callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----------| ------------- | -------------------------------------- |
| roomId  | NSString  | Room ID. You need to assign and manage the IDs in a centralized manner. |
| speechMode| TUIRoomSpeechMode | Speech mode. |
| callback | TUIRoomActionCallback | Room creation result. |

Generally, the anchor calls the APIs in the following steps:
1. The **anchor** calls `createRoom()` to create a room, the result of which is returned via `TUIRoomActionCallback`.
2. The **anchor** calls `startCameraPreview()` to enable camera capturing and preview.
3. The **anchor** calls `startLocalAudio()` to enable the local mic.

### destroyRoom

This API is used to terminate a room (called by the anchor).
```objectivec
- (void)destroyRoom:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | TUIRoomActionCallback | Room termination result. |

### enterRoom

This API is used to enter a room (called by a member).
```objectivec
- (void)enterRoom:(NSString *)roomId
        callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| roomId | NSString | Room ID. |
| callback | TUIRoomActionCallback| Result. |


Generally, a member enters a room in the following steps:
1. The **member** calls `enterRoom` and passes in `roomId` to enter the room.
2. The **member** calls `startCameraPreview()` to enable camera preview and calls startLocalAudio()` to enable mic capturing.
3. The **member** receives the `onRemoteUserCameraAvailable` event and calls `startRemoteView()` to start playback.

### leaveRoom

This API is used to exit a room (called by a member).
```objectivec
 - (void)leaveRoom:(TUIRoomActionCallback)callback;
```

  The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | TUIRoomActionCallback | Result. |

### getRoomInfo

This API is used to get the room information.
```objectivec
- (nullable TUIRoomInfo *)getRoomInfo;
```

### getRoomUsers

This API is used to get the information of all users in the room.
```objectivec
 - (nullable NSArray<TUIRoomUserInfo *> *)getRoomUsers;
```

### getUserInfo

This API is used to get the information of a user in the room.
```objectivec
- (void)getUserInfo:(NSString *)userId
           callback:(TUIRoomUserInfoCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId | NSString | User ID. |
| callback | TUIRoomUserInfoCallback | Room member details. |


### setSelfProfile

Set User Info
```objectivec
- (void)setSelfProfile:(NSString *)userName
        avatarURL:(NSString *)avatarURL
        callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------ | -------------- |
| userName  | NSString | User name. |
| avatarURL | NSString | User profile photo URL.  |
| callback | TUIRoomActionCallback | Whether the setting succeeded. |


### transferRoomMaster

This API is used to transfer a group to another user.
```objectivec
 - (void)transferRoomMaster:(NSString *)userId
                  callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId | NSString | User ID. |
| callback | TUIRoomActionCallback| Result. |


## Local Push APIs

### startCameraPreview

This API is used to start the preview of the local camera.
```objectivec
- (void)startCameraPreview:(BOOL)isFront
                      view:(UIView *)view;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| isFront | BOOL | YES: front camera; NO: rear camera. |
| view    | UIView | Control that carries the video image.                  |


### stopCameraPreview

This API is used to stop the preview of the local camera.
```objectivec
- (void)stopCameraPreview;
```

### startLocalAudio

This API is used to start mic capturing.
```objectivec
- (void)startLocalAudio:(TRTCAudioQuality)quality;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| quality | TRTCAudioQuality | Captured sound quality. |

### stopLocalAudio

This API is used to stop mic capturing.
```objectivec
- (void)stopLocalAudio;
```
### setVideoMirror

This API is used to set the mirroring preview mode of local video image.
```objectivec
 - (void)setVideoMirror:(TRTCVideoMirrorType)type;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| type | TRTCVideoMirrorType | Mirroring type. |

### setSpeaker

This API is used to set whether to use the speaker or receiver.
```objectivec
 - (void)setSpeaker:(BOOL)isUseSpeaker;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| isUseSpeaker | BOOL | YES: speaker; NO: receiver. |

## Remote User APIs

### startRemoteView
This API is used to subscribe to a remote user's video stream.

```objectivec
- (void)startRemoteView:(NSString *)userId
                   view:(UIView *)view
             streamType:(TUIRoomStreamType)streamType
               callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------------- | -------------------------- |
| userId   | NSString            | ID of the user whose video image is to be played back. |
| view     | UIView                                    | The control that loads video images. |
| streamType  | TUIRoomStreamType | Stream type. |
| callback  | TUIRoomActionCallback | Result. |


### stopRemoteView

This API is used to unsubscribe from and stop the playback of a remote video image.
```objectivec
- (void)stopRemoteView:(NSString *)userId
            streamType:(TUIRoomStreamType)streamType
              callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| userId   | NSString            | ID of the user whose video image is to be stopped. |
| streamType | TUIRoomStreamType  | Stream type. |
| callback  | TUIRoomActionCallback | Result. |

### switchCamera

This API is used to switch between the front and rear cameras.
```objectivec
- (void)switchCamera:(BOOL)isFront;

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| isFront | BOOL | YES: front camera; NO: rear camera. |

## Message Sending APIs

### sendChatMessage

This API is used to broadcast a text message in a room, which is generally used for text chat.
```objectivec
- (void)sendChatMessage:(NSString *)message
               callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | NSString | Message content. |
| callback  | TUIRoomActionCallback | Sending result. |

## Room Control APIs

### muteUserMicrophone

This API is used to enable/disable the mic of the specified user.
```objectivec
- (void)muteUserMicrophone:(NSString *)userId
                      mute:(BOOL)mute
                  callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| User ID.  |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback | Result. |

### muteAllUsersMicrophone

This API is used to enable/disable the mic of all users.
```objectivec
- (void)muteAllUsersMicrophone:(BOOL)mute
                      callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---- | ---------- |
| mute | BOOL | Whether to disable. |
| callback | TUIRoomActionCallback | Result. |


### muteUserCamera

This API is used to enable/disable the camera of the specified user.
```objectivec
- (void)muteUserCamera:(NSString *)userId
                  mute:(BOOL)mute
              callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| User ID.  |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback | Result. |

### muteAllUsersCamera

This API is used to enable/disable the camera of all users.
```objectivec
- (void)muteAllUsersCamera:(BOOL)mute
                  callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---- | ---------- |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback | Result. |

### muteChatRoom

This API is used to forbid/allow text chat.
```objectivec
- (void)muteChatRoom:(BOOL)mute
            callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---- | ---------- |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback | Result. |


### kickOffUser

This API is used by the anchor to remove a member.
```objectivec
- (void)kickOffUser:(NSString *)userId
           callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| User ID.  |
| callback | TUIRoomActionCallback | Result. |

### startCallingRoll

This API is used by the anchor to start roll call.
```objectivec
 - (void)startCallingRoll:(TUIRoomActionCallback)callback;
```
The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | Result. |

### stopCallingRoll

This API is used by the anchor to stop roll call.
```objectivec
- (void)stopCallingRoll:(TUIRoomActionCallback)callback;
```
The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | Result. |

### replyCallingRoll

This API is used by a member to reply to roll call.
```objectivec
- (void)replyCallingRoll:(TUIRoomActionCallback)callback;
```
The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | Result. |

### sendSpeechInvitation

This API is used by the anchor to invite a member to speak.
```objectivec
- (void)sendSpeechInvitation:(NSString *)userId
                    callback:(TUIRoomInviteeCallback)callback
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| User ID.  |
| callback | TUIRoomInviteeCallback | Result. |

### cancelSpeechInvitation

This API is used by the anchor to cancel the speech invitation to a member.
```objectivec
- (void)cancelSpeechInvitation:(NSString *)userId
                      callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| User ID.  |
| callback | TUIRoomActionCallback | Result. |

### replySpeechInvitation

This API is used by a member to accept/reject the speech invitation from the anchor.
```objectivec
- (void)replySpeechInvitation:(BOOL)agree
                     callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree | BOOL  | Whether to approve. |
| callback | TUIRoomActionCallback | Result. |

### sendSpeechApplication

This API is used by a member to apply to speak.
```objectivec
- (void)sendSpeechApplication:(TUIRoomInviteeCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomInviteeCallback | Result. |

### cancelSpeechApplication

This API is used by a member to cancel the speech application.
```objectivec
- (void)cancelSpeechApplication:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| Result. |

### replySpeechApplication

This API is used by the anchor to approve/reject the speech application of a member.
```objectivec
- (void)replySpeechApplication:(BOOL)agree
                        userId:(NSString *)userId
                      callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree  | BOOL| Whether to approve. |
| userId  | NSString| User ID.  |
| callback | TUIRoomActionCallback | Result. |

### forbidSpeechApplication

This API is used by the anchor to forbid speech application.
```objectivec
- (void)forbidSpeechApplication:(BOOL)forbid
                       callback:(TUIRoomActionCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ---------- |
| forbid | BOOL | Whether to forbid. |
| callback | TUIRoomActionCallback | Result. |


### sendOffSpeaker

This API is used by the anchor to stop the speech of the specified member.
```objectivec
- (void)sendOffSpeaker:(NSString *)userId
              callback:(TUIRoomInviteeCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| User ID.  |
| callback | TUIRoomInviteeCallback | Result. |

### sendOffAllSpeakers

This API is used by the anchor to stop the speech of all members.
```objectivec
- (void)sendOffAllSpeakers:(TUIRoomInviteeCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomInviteeCallback| Result. |

### exitSpeechState

This API is used for a member to stop speaking and change their role to audience.
```objectivec
- (void)exitSpeechState:(TUIRoomActionCallback)callback;
```
The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback | Result. |


## Screen Sharing APIs
### startScreenCapture

This API is used to start screen sharing.
```objectivec
- (void)startScreenCapture:(TRTCVideoEncParam *)encParam API_AVAILABLE(ios(11.0));
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| encParams | TRTCVideoEncParam | Sets encoding parameters for screen sharing. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff).

### stopScreenCapture

This API is used to stop screen capturing.
```objectivec
- (void)stopScreenCapture API_AVAILABLE(ios(11.0));
```

## Beauty Filter APIs
### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__ios.html).
```objectivec
- (TXBeautyManager *)getBeautyManager;
```

You can do the following using `TXBeautyManager`:
- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.

## Settings APIs

### setVideoQosPreference

set QoS parameters
```objectivec
- (void)setVideoQosPreference:(TRTCNetworkQosParam *)preference;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | --------------------- | -------------- |
| preference | TRTCNetworkQosParam | Network bandwidth limit policy. |

### setAudioQuality

This API is used to set audio quality.
```objectivec
- (void)setAudioQuality:(TRTCAudioQuality)quality;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| quality | TRTCAudioQuality | Audio quality. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53). |

### setVideoResolution

This API is used to set the resolution.

```objectivec
- (void)setVideoResolution:(TRTCVideoResolution)resolution;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| resolution | TRTCVideoResolution | Video resolution. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5). |


### setVideoFps

This API is used to set the frame rate.
```objectivec
- (void)setVideoFps:(int)fps;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| fps | int | Video capturing frame rate. |

>?**Recommended value:** 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lag; if lower than 10 fps but higher than 5 fps, there will be slight lag; if higher than 20 fps, excessive resources will be wasted (the frame rate of movies is generally 24 fps).


### setVideoBitrate

This API is used to set the bitrate.
```objectivec
- (void)setVideoBitrate:(int)bitrate;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| bitrate | int  | Bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454). |

>? **Recommended value:** see the optimal bitrate for each tier in `TRTCVideoResolution`. You can also slightly increase the bitrate. For example, `TRTC_VIDEO_RESOLUTION_1280_720` corresponds to the target bitrate of 1,200 Kbps, and you can also set the bitrate to 1,500 Kbps for higher definition.

### enableAudioEvaluation

This API is used to enable the volume reminder.
```objectivec
- (void)enableAudioEvaluation:(BOOL)enable;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | BOOL | YES: enable; NO: disable |

>? After this feature is enabled, the result of volume evaluation by the SDK will be obtained in `onUserVolumeUpdate`.

### setAudioPlayVolume

This API is used to set the playback volume.
```objectivec
- (void)setAudioPlayVolume:(NSInteger)volume;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| volume | int | Playback volume. Value range: 0–100. Default value: 100. |

### setAudioCaptureVolume

This API is used to set the mic capturing volume.
```objectivec
- (void)setAudioCaptureVolume:(NSInteger)volume;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| volume | int | Capture volume. Value range: 0–100. Default value: 100. |

### startFileDumping

This API is used to start audio recording.
```objectivec
- (void)startFileDumping:(TRTCAudioRecordingParams *)params;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| params | TRTCAudioRecordingParams | Audio recording parameters. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams). |

>? After this API is called, the SDK will record all audio of a call, including local audio, remote audio, and background music, into a file. This API works regardless of whether a user is in the room. When `leaveRoom` is called, audio recording will stop automatically.

### stopFileDumping

This API is used to stop audio recording.
```objectivec
- (void)stopFileDumping;
```

## SDK Version Acquisition APIs

### getSdkVersion

This API is used to get SDK version information.
```objectivec
- (NSInteger)getSdkVersion;
```

## Error Event Callbacks
### onError

```objectivec
- (void)onError:(NSInteger)code message:(NSString *)message;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | NSInteger | Error code.   |
| message | NSString  | Error message |

## Basic Event Callbacks

### onDestroyRoom

Room dismissal.
```objectivec
- (void)onDestroyRoom;
```

### onUserVoiceVolume

User volume level.
```objectivec
- (void)onUserVoiceVolume:(NSString *)userId volume:(NSInteger)volume;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------------------------------- |
| userId | NSString | User ID.  |
| volume  | NSInteger | User volume level. Value range: 0–100. |

### onRoomMasterChanged

Anchor change.
```objectivec
- (void)onRoomMasterChanged:(NSString *)previousUserId
              currentUserId:(NSString *)currentUserId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| previousUserId | NSString | Anchor's user ID before change. |
| currentUserId | NSString | Anchor's user ID after change. |


## Remote User Callbacks

### onRemoteUserEnter

A remote user entered the room.
```objectivec
- (void)onRemoteUserEnter:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |

### onRemoteUserLeave

A remote user exited the room.
```objectivec
- (void)onRemoteUserLeave:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |

### onRemoteUserCameraAvailable

Whether a remote user enabled the camera.
```objectivec
- (void)onRemoteUserCameraAvailable:(NSString *)userId
                          available:(BOOL)available;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | User ID. |
| available | BOOL| YES: enabled; NO: disabled. |

### onRemoteUserScreenVideoAvailable

A member **enabled/disabled** video sharing.
```objectivec
- (void)onRemoteUserScreenVideoAvailable:(NSString *)userId
                               available:(BOOL)available;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | User ID. |
| available | BOOL| Whether screen sharing stream data is available. |

### onRemoteUserAudioAvailable

Whether a remote user is sending audio.
```objectivec
- (void)onRemoteUserAudioAvailable:(NSString *)userId
                         available:(BOOL)available;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | User ID. |
| available | BOOL| Whether audio data is available. |

### onRemoteUserEnterSpeechState

A remote user started speaking.
```objectivec
- (void)onRemoteUserEnterSpeechState:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |

### onRemoteUserExitSpeechState

A remote user stopped speaking.
```objectivec
- (void)onRemoteUserExitSpeechState:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |


## Chat Room Message Event Callbacks

### onReceiveChatMessage

Callback for receiving a text message.
```objectivec
- (void)onReceiveChatMessage:(NSString *)userId message:(NSString *)message;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId | NSString | User ID.  |
| message  | NSString            | Text message     |


## Room Control Message Callbacks

### onReceiveSpeechInvitation

A user received a speech invitation from the anchor.
```objectivec
- (void)onReceiveSpeechInvitation:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | Anchor's user ID. |

### onReceiveInvitationCancelled

A user received a speech invitation cancellation from the anchor.
```objectivec
- (void)onReceiveInvitationCancelled:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | Anchor's user ID. |

### OnReceiveSpeechApplication

The anchor received a speech application from a member.
```objectivec
void onReceiveSpeechApplication(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |

### onSpeechApplicationCancelled

A user canceled a speech application.
```objectivec
- (void)onSpeechApplicationCancelled:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |

### onSpeechApplicationForbidden

The anchor forbidden a speech application.
```objectivec
- (void)onSpeechApplicationForbidden:(BOOL)isForbidden userId:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ---- | ---------- |
| isForbidden | BOOL | Whether to forbid. |
| userId | NSString  | User ID            |

### onOrderedToExitSpeechState

A member was asked to stop speaking.
```objectivec
- (void)onOrderedToExitSpeechState:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | Anchor's user ID. |


### onCallingRollStarted

The anchor started a roll call.
```objectivec
- (void)onCallingRollStarted:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | Anchor's user ID. |

### onCallingRollStopped

The anchor stopped a roll call.
```objectivec
- (void)onCallingRollStopped:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | Anchor's user ID. |

### onMemberReplyCallingRoll

A member replied to roll call.
```objectivec
- (void)onMemberReplyCallingRoll:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID            |

### onChatRoomMuted

The anchor muted/unmuted the room.
```objectivec
- (void)onChatRoomMuted:(BOOL)muted userId:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | BOOL | Whether to disable. |
| userId | NSString | Anchor's user ID. |

### onMicrophoneMuted

The anchor disabled the mic.
```objectivec
- (void)onMicrophoneMuted:(BOOL)muted userId:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | BOOL | Whether to disable. |
| userId | NSString | Anchor's user ID. |

### onCameraMuted

The anchor disabled the camera.
```objectivec
- (void)onCameraMuted:(BOOL)muted userId:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | BOOL | Whether to disable. |
| userId | NSString | Anchor's user ID. |

### onReceiveKickedOff

The anchor removed a member.
```objectivec
- (void)onReceiveKickedOff:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| userId | NSString | Anchor/Admin's user ID. |

## Statistics Collection and Quality Callbacks

### onStatistics

Callback of technical metric statistics.
```objectivec
- (void)onStatistics:(TRTCStatistics *)statistics;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | Statistics. |

### onNetworkQuality

Network quality.
```objectivec
- (void)onNetworkQuality:(TRTCQualityInfo *)localQuality remoteQuality:(NSArray<TRTCQualityInfo *> *)remoteQuality;

```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| localQuality  | TRTCQualityInfo            | Upstream network quality. |
| remoteQuality |NSArray&lt;TRTCQualityInfo *&gt; | Downstream network quality. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28).


## Screen Sharing Event Callbacks

### onScreenCaptureStarted

Screen sharing started.

```objectivec
 - (void)onScreenCaptureStarted;
```

### onScreenCaptureStopped

Screen sharing stopped.

```objectivec
- (void)onScreenCaptureStopped:(NSInteger)reason;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------------------------ |
| reason | NSInteger  | Reason for stop. 0: the user stopped proactively; 1: stopped due to preemption by another application. |
