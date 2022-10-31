TUIRoom is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:
- A host can create a room, and users can enter the room ID to join the room.
- Room members can share their screens with each other.
- All members can send text chat messages and custom messages.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports up to 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

TUIRoom is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, see [Integrating TUIRoom (iOS)](https://intl.cloud.tencent.com/document/product/647/37284).
- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video room component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) (**iOS edition**) is used to implement chat messages.


## TUIRoom API Overview

### TUIRoomCore basic APIs

| API | Description |
| ----------------------------------- | -------------- |
| [shareInstance](#shareinstance)     | Gets a singleton object. |
| [destroyInstance](#destroyinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callbacks. |

### Room APIs

| API | Description |
| ----------------------------------------- | ---------------------------------- |
| [createRoom](#createroom)                 | Creates a room (called by host).           |
| [destroyRoom](#destroyroom)               | Closes the room (called by host).           |
| [enterRoom](#enterroom)                   | Enters a room (called by participant)|
| [leaveRoom](#leaveroom)             | Leaves a room (called by participant).           |
| [getRoomInfo](#getroominfo)               | Gets the room information.                     |
| [getRoomUsers](#getroomusers)             | Gets the information of all users in the room.           |
| [getUserInfo](#getuserinfo)               | Gets the information of a user.               |
| [transferRoomMaster](#transferroommaster) | Transfers the host permissions to another user (called by host).     |

### Local audio/video operation APIs

| API | Description |
| ----------------------------------------- | -------------------------- |
| [startCameraPreview](#startcamerapreview) | Enables the preview image of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [startLocalAudio](#startlocalaudio)       | Enables mic capturing.           |
| [stopLocalAudio](#stoplocalaudio)         | Stops mic capturing.           |
| [setVideoMirror](#setvideomirror)                     | Sets the mirror mode for local video preview. |
| [setSpeaker](#setspeaker)                 | Sets whether to play sound from the device’s speaker or receiver.     |

### Remote user APIs

| API | Description |
| ----------------------------------- | ---------------------------------- |
| [startRemoteView](#startremoteview) | Subscribes to and plays back the remote video image of a specified room member. |
| [stopRemoteView](#stopremoteview)   | Unsubscribes from and stops the playback of a remote video image.   |

### Chat message sending APIs

| API | Description |
| ----------------------------------- | -------------- |
| [sendChatMessage](#sendchatmessage)     | Sends a chat message.   |
| [sendCustomMessage](#sendcustommessage) | Sends a custom message. |

### Room control APIs

| API | Description |
| --------------------------------------------------- | ------------------------------------------------------- |
| [muteUserMicrophone](#muteusermicrophone)           | Enables/Disables the mic of a specified user.                               |
| [muteAllUsersMicrophone](#muteallusersmicrophone)   | Enables/Disables the mics of all users and syncs the status to room information. |
| [muteUserCamera](#muteusercamera)                   | Enables/Disables the camera of a specified user.                               |
| [muteAllUsersCamera](#mutealluserscamera)           | Enables/Disables the cameras of all users and syncs the status to room information. |
| [muteChatRoom](#mutechatroom)                       | Disables/Enables chat messages (called by host).                     |
| [kickOffUser](#kickoffuser)                         | Removes a specified user from the room (called by host).                        |
| [startCallingRoll](#startcallingroll)               | Starts a roll call (called by host).                                        |
| [stopCallingRoll](#stopcallingroll)                 | Stops a roll call (called by host).                                        |
| [replyCallingRoll](#replycallingroll)               | Replies to a roll call (called by participant).                                    |
| [sendSpeechInvitation](#sendspeechinvitation)       | Sends a speech invitation to a participant (called by host).                                    |
| [cancelSpeechInvitation](#cancelspeechinvitation)   | Cancels a speech invitation sent to a participant (called by host).                                 |
| [replySpeechInvitation](#replyspeechinvitation)     | Accepts/Rejects the speech invitation of the host (called by participant).                         |
| [SendSpeechApplication](#sendspeechapplication)     | Sends a speech request (called by participant).                                         |
| [replySpeechApplication](#replyspeechapplication)   | Approves/Rejects the speech request of a participant (called by host).                         |
| [forbidSpeechApplication](#forbidspeechapplication) | Disables requests to speak (called by host).                                    |
| [sendOffSpeaker](#sendoffspeaker)                   | Stops the speech of a participant (called by host).                                |
| [sendOffAllSpeakers](#sendoffallspeakers)           | Stops the speech of all room members (called by host).                                  |
| [ExitSpeechState](#exitspeechstate)                 | Exits the speaker mode (called by participant).                               |

### Screen sharing APIs

| API | Description |
|-----|-----|
| [startScreenCapture](#startscreencapture)   | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture)   | Stops screen sharing. |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__ios.html). |


### Settings APIs

| API | Description |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | Sets network QoS control parameters. |

### SDK version APIs

| API | Description |
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | Gets the SDK version. |

## TUIRoomCoreDelegate API Overview

### Callbacks for error events

| API | Description |
| ------------------- | ---------- |
| [onError](#onerror) | Callback for error.|

### Basic event callbacks

| API | Description |
| ------------------------------------------- | ------------------ |
| [OnDestroyRoom](#ondestroyroom)             | The room was closed.     |
| [onUserVoiceVolume](#onuservoicevolume)     | The audio volume of a user. |
| [onRoomMasterChanged](#onroommasterchanged) | The host changed.   |

### Remote user event callbacks

| API                          | Description  |
| ------------------------------------------------------------ | -------------------------------- |
| [onRemoteUserEnter](#onremoteuserenter)                      | A remote user entered the room.           |
| [onRemoteUserLeave](#onremoteuserleave)                      | A remote user exited the room.            |
| [onRemoteUserCameraAvailable](#onremoteusercameraavailable)  | A remote user enabled/disabled their camera. |
| [onRemoteUserScreenVideoAvailable](#onremoteuserscreenvideoavailable) | A remote user started/stopped screen sharing.   |
| [onRemoteUserAudioAvailable](#onremoteuseraudioavailable)    |  A remote user turned on/off their mic.   |
| [onRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | A remote user started speaking.           |
| [onRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | A remote user stopped speaking.          |

### Message event callbacks

| API | Description |
| ------------------------------------------------- | ------------------ |
| [onReceiveChatMessage](#onreceivechatmessage)     | A text chat message was received. |

### Room control event callbacks

| API | Description |
| ------------------------------------------------------------ | ---------------------------------- |
| [onReceiveSpeechInvitation](#onreceivespeechinvitation)      | A participant received a speech invitation from the host.       |
| [onReceiveInvitationCancelled](#onreceiveinvitationcancelled) | The speech invitation sent to a participant was canceled by the host.    |
| [onReceiveSpeechApplication](#onreceivespeechapplication)    | The host received a speech request from a participant.     |
| [onSpeechApplicationCancelled](#onspeechapplicationcancelled) | A participant canceled a speech request.             |
| [onSpeechApplicationForbidden](#onspeechapplicationforbidden) | The host disabled requests to speak.           |
| [onOrderedToExitSpeechState](#onorderedtoexitspeechstate)  | A participant was asked to stop speaking.         |
| [onCallingRollStarted](#oncallingrollstarted)                | The host started a roll call (received by participants)   |
| [onCallingRollStopped](#oncallingrollstopped)                | The host stopped a roll call (received by participants).   |
| [onMemberReplyCallingRoll](#onmemberreplycallingroll)        | A participant replied to the roll call (received by the host).   |
| [onChatRoomMuted](#onchatroommuted)                          | The host disabled/enabled chat messages.     |
| [onMicrophoneMuted](#onmicrophonemuted)                      | The host disabled mic use.         |
| [onCameraMuted](#oncameramuted)                              | The host disabled camera use.         |
| [onReceiveKickedOff](#onreceivekickedoff)                    | The host removed a participant from the room (received by the participant).         |


### Callback of statistics on network quality and technical metrics

| API | Description |
| ------------------------------------- | ------------------ |
| [onStatistics](#onstatistics)         | Statistics on technical metrics. |
| [onNetworkQuality](#onnetworkquality) | Network quality.     |

### Screen sharing event callbacks

| API | Description |
| ------------------------------------------------- | ------------------ |
| [onScreenCaptureStarted](#onscreencapturestarted) | Screen sharing started. |
| [onScreenCaptureStopped](#onscreencapturestopped) | Screen sharing stopped. |

## TUIRoomCore Basic APIs

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

This API is used to set the event callbacks of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37284). You can use `TUIRoomCoreDelegate` to get the callbacks.

```objectivec
- (void)setDelegate:(id<TUIRoomCoreDelegate>)delegate;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| delegate | TUIRoomCoreDelegate | The event callback class. |

### createRoom

This API is used to create a room (called by the host).
```objectivec
- (void)createRoom:(NSString *)roomId
        speechMode:(TUIRoomSpeechMode)speechMode
        callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
|-----------| ------------- | -------------------------------------- |
| roomId  | NSString  | The room ID. You need to assign and manage the IDs in a centralized manner. |
| speechMode| TUIRoomSpeechMode | The speech mode. |
| callback | TUIRoomActionCallback | The room creation result. |

Generally, a host may need to call the following APIs:
1. The **host** calls `createRoom()` to create a room, the result of which is returned via `TUIRoomActionCallback`.
2. The **host** calls `startCameraPreview()` to enable camera capturing and preview.
3. The **host** calls `startLocalAudio()` to enable the local mic.

### destroyRoom

This API is used to close a room (called by the host).
```objectivec
- (void)destroyRoom:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | TUIRoomActionCallback | The room closing result. |

### enterRoom

This API is used to enter a room (called by a participant).
```objectivec
- (void)enterRoom:(NSString *)roomId
        callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| roomId | NSString | The room ID. |
| callback | TUIRoomActionCallback| The result. |


Generally, a participant joins a room in the following steps:
1. The **participant** calls `enterRoom` (passing in `roomId`) to enter the room.
2. The **participant** calls `startCameraPreview()` to enable camera preview and calls `startLocalAudio()` to enable mic capturing.
3. The **participant** receives the `onRemoteUserCameraAvailable` callback and calls `startRemoteView()` to start playback.

### leaveRoom

This API is used to leave a room (called by a participant).
```objectivec
 - (void)leaveRoom:(TUIRoomActionCallback)callback;
```

  The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | TUIRoomActionCallback| The result. |

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

This API is used to get the information of a specified room member.
```objectivec
- (void)getUserInfo:(NSString *)userId
           callback:(TUIRoomUserInfoCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId | NSString | The user ID. |
| callback | TUIRoomUserInfoCallback | Room member details. |


### setSelfProfile

This API is used to set the user profile.
```objectivec
- (void)setSelfProfile:(NSString *)userName
        avatarURL:(NSString *)avatarURL
        callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ---------- | ------ | -------------- |
| userName  | NSString | The username.  |
| avatarURL | NSString | The URL of the user profile photo. |
| callback | TUIRoomActionCallback | Whether the setting succeeded. |


### transferRoomMaster

This API is used to transfer host permissions to another user.
```objectivec
 - (void)transferRoomMaster:(NSString *)userId
                  callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId | NSString | The user ID. |
| callback | TUIRoomActionCallback| The result. |


## Local Push APIs

### startCameraPreview

This API is used to start the preview of the local camera.
```objectivec
- (void)startCameraPreview:(BOOL)isFront
                      view:(UIView *)view;
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| isFront | BOOL | YES: Front camera; NO: Rear camera. |
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

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| quality | TRTCAudioQuality | The sound quality. |

### stopLocalAudio

This API is used to stop mic capturing.
```objectivec
- (void)stopLocalAudio;
```
### setVideoMirror

This API is used to set the mirror mode for local video preview.
```objectivec
 - (void)setVideoMirror:(TRTCVideoMirrorType)type;
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| type | TRTCVideoMirrorType | The mirror mode. |

### setSpeaker

This API is used to set whether to play sound from the device’s speaker or receiver.
```objectivec
 - (void)setSpeaker:(BOOL)isUseSpeaker;
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| isUseSpeaker | BOOL | YES: Speaker; NO: Receiver. |

## Remote User APIs

### startRemoteView
This API is used to subscribe to a remote user's video stream.

```objectivec
- (void)startRemoteView:(NSString *)userId
                   view:(UIView *)view
             streamType:(TUIRoomStreamType)streamType
               callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------------- | ------------- | -------------------------- |
| userId  | NSString  | The ID of the user whose video image is to be played back. |
| view     | UIView                                    | The view that loads video images. |
| streamType  | TUIRoomStreamType | The stream type. |
| callback | TUIRoomActionCallback| The result. |


### stopRemoteView

This API is used to unsubscribe from and stop the playback of a remote video image.
```objectivec
- (void)stopRemoteView:(NSString *)userId
            streamType:(TUIRoomStreamType)streamType
              callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| userId | NSString | The ID of the user whose video image is to be stopped. |
| streamType | TUIRoomStreamType  | The stream type. |
| callback | TUIRoomActionCallback| The result. |

### switchCamera

This API is used to switch between the front and rear cameras.
```objectivec
- (void)switchCamera:(BOOL)isFront;

```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| isFront | BOOL | YES: Front camera; NO: Rear camera. |

## Message Sending APIs

### sendChatMessage

This API is used to broadcast a text chat message in the room.
```objectivec
- (void)sendChatMessage:(NSString *)message
               callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | NSString | The message content. |
| callback | TUIRoomActionCallback| The result. |

## Room Control APIs

### muteUserMicrophone

This API is used to enable/disable the mic of the specified user.
```objectivec
- (void)muteUserMicrophone:(NSString *)userId
                      mute:(BOOL)mute
                  callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| The user ID.  |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback| The result. |

### muteAllUsersMicrophone

This API is used to enable/disable the mics of all users.
```objectivec
- (void)muteAllUsersMicrophone:(BOOL)mute
                      callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ---- | ---- | ---------- |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback| The result. |


### muteUserCamera

This API is used to enable/disable the camera of the specified user.
```objectivec
- (void)muteUserCamera:(NSString *)userId
                  mute:(BOOL)mute
              callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| The user ID.  |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback| The result. |

### muteAllUsersCamera

This API is used to enable/disable the cameras of all users.
```objectivec
- (void)muteAllUsersCamera:(BOOL)mute
                  callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ---- | ---- | ---------- |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback| The result. |

### muteChatRoom

This API is used to disable/enable chat messages.
```objectivec
- (void)muteChatRoom:(BOOL)mute
            callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ---- | ---- | ---------- |
| mute  | BOOL  | Whether to disable. |
| callback | TUIRoomActionCallback| The result. |


### kickOffUser

This API is used by the host to remove a member from the room.
```objectivec
- (void)kickOffUser:(NSString *)userId
           callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| The user ID.  |
| callback | TUIRoomActionCallback| The result. |

### startCallingRoll

This API is used by the host to start a roll call.
```objectivec
 - (void)startCallingRoll:(TUIRoomActionCallback)callback;
```
The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| The result. |

### stopCallingRoll

This API is used by the host to stop a roll call.
```objectivec
- (void)stopCallingRoll:(TUIRoomActionCallback)callback;
```
The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| The result. |

### replyCallingRoll

This API is used by a participant to reply to a roll call.
```objectivec
- (void)replyCallingRoll:(TUIRoomActionCallback)callback;
```
The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| The result. |

### sendSpeechInvitation

This API is used by the host to invite a participant to speak.
```objectivec
- (void)sendSpeechInvitation:(NSString *)userId
                    callback:(TUIRoomInviteeCallback)callback
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| The user ID.  |
| callback | TUIRoomInviteeCallback | The result. |

### cancelSpeechInvitation

This API is used by the host to cancel a speech invitation.
```objectivec
- (void)cancelSpeechInvitation:(NSString *)userId
                      callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| The user ID.  |
| callback | TUIRoomActionCallback| The result. |

### replySpeechInvitation

This API is used by a participant to accept/reject the host’s invitation to speak.
```objectivec
- (void)replySpeechInvitation:(BOOL)agree
                     callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree | bool | Whether to approve. |
| callback | TUIRoomActionCallback| The result. |

### sendSpeechApplication

This API is used by a participant to send a request to speak.
```objectivec
- (void)sendSpeechApplication:(TUIRoomInviteeCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomInviteeCallback | The result. |

### cancelSpeechApplication

This API is used by a participant to cancel the request to speak.
```objectivec
- (void)cancelSpeechApplication:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| The result. |

### replySpeechApplication

This API is used by the host to approve/reject a participant’s speech request.
```objectivec
- (void)replySpeechApplication:(BOOL)agree
                        userId:(NSString *)userId
                      callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree | BOOL | Whether to approve. |
| userId  | NSString| The user ID.  |
| callback | TUIRoomActionCallback| The result. |

### forbidSpeechApplication

This API is used by the host to disable requests to speak.
```objectivec
- (void)forbidSpeechApplication:(BOOL)forbid
                       callback:(TUIRoomActionCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---- | ---------- |
| forbid | BOOL | Whether to disable. |
| callback | TUIRoomActionCallback| The result. |


### sendOffSpeaker

This API is used by the host to stop the speech of a participant.
```objectivec
- (void)sendOffSpeaker:(NSString *)userId
              callback:(TUIRoomInviteeCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | NSString| The user ID.  |
| callback | TUIRoomInviteeCallback | The result. |

### sendOffAllSpeakers

This API is used by the host to stop the speech of all room members.
```objectivec
- (void)sendOffAllSpeakers:(TUIRoomInviteeCallback)callback;
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomInviteeCallback | The result. |

### exitSpeechState

This API is used by a participant to exit the speaker mode.
```objectivec
- (void)exitSpeechState:(TUIRoomActionCallback)callback;
```
The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomActionCallback| The result. |


## Screen Sharing APIs
### startScreenCapture

This API is used to start screen sharing.
```objectivec
- (void)startScreenCapture:(TRTCVideoEncParam *)encParam API_AVAILABLE(ios(11.0));
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| encParams | TRTCVideoEncParam | Sets encoding parameters for screen sharing. |

>? For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff).

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

You can do the following using the beauty filter manger:
- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.

## Settings APIs

### setVideoQosPreference

This API is used to set network QoS control parameters.
```objectivec
- (void)setVideoQosPreference:(TRTCNetworkQosParam *)preference;
```

The parameters are described below:

| Parameter | Type | Description |
| ---------- | --------------------- | -------------- |
| preference | TRTCNetworkQosParam | The network QoS policy. |

### setAudioQuality

This API is used to set audio quality.
```objectivec
- (void)setAudioQuality:(TRTCAudioQuality)quality;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| quality | TRTCAudioQuality | The audio quality. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53). |

### setVideoResolution

This API is used to set the resolution.

```objectivec
- (void)setVideoResolution:(TRTCVideoResolution)resolution;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| resolution | TRTCVideoResolution | The resolution. For details, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5). |


### setVideoFps

This API is used to set the frame rate.
```objectivec
- (void)setVideoFps:(int)fps;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| fps | int | The video capturing frame rate. |

>? **Recommended value:** 15 or 20 fps. Video will stutter severely if the frame rate is lower than 5 fps and slightly if it is lower than 10 fps. Setting the frame rate to higher than 20 fps would be a waste of resources (the frame rate of films is 24 fps).


### setVideoBitrate

This API is used to set the bitrate.
```objectivec
- (void)setVideoBitrate:(int)bitrate;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| bitrate | int  | The bitrate. The SDK encodes streams at the target video bitrate. However, it may reduce the bitrate if network conditions are poor. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454). |

>? **Recommended value:** See the recommended bitrate for each `TRTCVideoResolution` value. For a better viewing experience, you can slightly increase the bitrate. For example, the recommended bitrate for `TRTC_VIDEO_RESOLUTION_1280_720` is 1,200 Kbps. You can set the bitrate to 1,500 Kbps.

### enableAudioEvaluation

This API is used to enable the volume reminder.
```objectivec
- (void)enableAudioEvaluation:(BOOL)enable;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| bEnable | BOOL | YES: Enable. NO: Disable. |

>? After the volume reminder is enabled, the volumes measured by the SDK will be returned via the `onUserVolumeUpdate` callback.

### setAudioPlayVolume

This API is used to set the playback volume.
```objectivec
- (void)setAudioPlayVolume:(NSInteger)volume;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | The playback volume. Value range: 0-100. Default value: 100. |

### setAudioCaptureVolume

This API is used to set the mic capturing volume.
```objectivec
- (void)setAudioCaptureVolume:(NSInteger)volume;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | The capturing volume. Value range: 0-100. Default value: 100. |

### startFileDumping

This API is used to start audio recording.
```objectivec
- (void)startFileDumping:(TRTCAudioRecordingParams *)params;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| params | TRTCAudioRecordingParams | The recording parameters. For details, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams). |

>? After this API is called, the SDK will record all audios of a call, including the local audio, remote audios, and background music, into a single file. This API works regardless of whether you are in the room or not. When `leaveRoom` is called, audio recording will stop automatically.

### stopFileDumping

This API is used to stop audio recording.
```objectivec
- (void)stopFileDumping;
```

## SDK Version APIs

### getSdkVersion

This API is used to get the SDK version.
```objectivec
- (NSInteger)getSdkVersion;
```

## Error Event Callbacks
### onError

```objectivec
- (void)onError:(NSInteger)code message:(NSString *)message;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | NSInteger | The error code.   |
| message | NSString  | The error message. |

## Basic Event Callbacks

### onDestroyRoom

The room was closed.
```objectivec
- (void)onDestroyRoom;
```

### onUserVoiceVolume

The audio volume of a user.
```objectivec
- (void)onUserVoiceVolume:(NSString *)userId volume:(NSInteger)volume;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------------------------------- |
| userId  | NSString| The user ID.  |
| volume | NSInteger| The volume. Value range: 0-100. |

### onRoomMasterChanged

The host changed.
```objectivec
- (void)onRoomMasterChanged:(NSString *)previousUserId
              currentUserId:(NSString *)currentUserId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| previousUserId | NSString | The host’s user ID before the change. |
| currentUserId | NSString | The host's user ID after the change. |


## Remote User Callbacks

### onRemoteUserEnter

A remote user entered the room.
```objectivec
- (void)onRemoteUserEnter:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId  | NSString| The user ID.  |

### onRemoteUserLeave

A remote user exited the room.
```objectivec
- (void)onRemoteUserLeave:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId  | NSString| The user ID.  |

### onRemoteUserCameraAvailable

A remote user enabled/disabled their camera.
```objectivec
- (void)onRemoteUserCameraAvailable:(NSString *)userId
                          available:(BOOL)available;
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId  | NSString| The user ID.  |
| available | BOOL| YES: Enabled; NO: Disabled. |

### onRemoteUserScreenVideoAvailable

A member **enabled/disabled** video sharing.
```objectivec
- (void)onRemoteUserScreenVideoAvailable:(NSString *)userId
                               available:(BOOL)available;
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId  | NSString| The user ID.  |
| available | BOOL| Whether the user enabled/disabled screen sharing. |

### onRemoteUserAudioAvailable

A remote user enabled/disabled their mic.
```objectivec
- (void)onRemoteUserAudioAvailable:(NSString *)userId
                         available:(BOOL)available;
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| NSString | User ID. |
| available | BOOL| Whether the user enabled/disabled their mic. |

### onRemoteUserEnterSpeechState

A remote user started speaking.
```objectivec
- (void)onRemoteUserEnterSpeechState:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId  | NSString| The user ID.  |

### onRemoteUserExitSpeechState

A remote user stopped speaking.
```objectivec
- (void)onRemoteUserExitSpeechState:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId  | NSString| The user ID.  |


## Chat Message Event Callbacks

### onReceiveChatMessage

A text chat message was received.
```objectivec
- (void)onReceiveChatMessage:(NSString *)userId message:(NSString *)message;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId  | NSString| The user ID.  |
| message | NSString | The message content. |


## Room Control Message Callbacks

### onReceiveSpeechInvitation

The host sent a speech invitation (received by a participant).
```objectivec
- (void)onReceiveSpeechInvitation:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | The host's user ID. |

### onReceiveInvitationCancelled

The host canceled the speech invitation (received by a participant).
```objectivec
- (void)onReceiveInvitationCancelled:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | The host's user ID. |

### OnReceiveSpeechApplication

A participant sent a request to speak (received by the host).
```objectivec
void onReceiveSpeechApplication(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | NSString  | User ID.            |

### onSpeechApplicationCancelled

A participant canceled a speech request.
```objectivec
- (void)onSpeechApplicationCancelled:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId  | NSString| The user ID.  |

### onSpeechApplicationForbidden

The host disabled requests to speak.
```objectivec
- (void)onSpeechApplicationForbidden:(BOOL)isForbidden userId:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ---- | ---------- |
| isForbidden | BOOL | Disabled or not. |
| userId | NSString  | User ID.            |

### onOrderedToExitSpeechState

A participant was asked to stop speaking.
```objectivec
- (void)onOrderedToExitSpeechState:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | The host's user ID. |


### onCallingRollStarted

The host started a roll call (received by participants).
```objectivec
- (void)onCallingRollStarted:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | The host's user ID. |

### onCallingRollStopped

The host stopped a roll call (received by participants).
```objectivec
- (void)onCallingRollStopped:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | NSString | The host's user ID. |

### onMemberReplyCallingRoll

A participant replied to the roll call (received by the host).
```objectivec
- (void)onMemberReplyCallingRoll:(NSString *)userId;
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId  | NSString| The user ID.  |

### onChatRoomMuted

The host disabled/enabled chat messages.
```objectivec
- (void)onChatRoomMuted:(BOOL)muted userId:(NSString *)userId;
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | BOOL | Disabled or not. |
| userId | NSString | The host's user ID. |

### onMicrophoneMuted

The host disabled mic use.
```objectivec
- (void)onMicrophoneMuted:(BOOL)muted userId:(NSString *)userId;
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | BOOL | Disabled or not. |
| userId | NSString | The host's user ID. |

### onCameraMuted

The host disabled camera use.
```objectivec
- (void)onCameraMuted:(BOOL)muted userId:(NSString *)userId;
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | BOOL | Disabled or not. |
| userId | NSString | The host's user ID. |

### onReceiveKickedOff

The host removed a member from the room.
```objectivec
- (void)onReceiveKickedOff:(NSString *)userId;
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| userId | NSString | The user ID of the host/admin. |

### Callbacks of statistics on network quality and technical metrics

### onStatistics

Callback of technical metric statistics.
```objectivec
- (void)onStatistics:(TRTCStatistics *)statistics;
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | Statistics. |

### onNetworkQuality

Network quality.
```objectivec
- (void)onNetworkQuality:(TRTCQualityInfo *)localQuality remoteQuality:(NSArray<TRTCQualityInfo *> *)remoteQuality;

```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| localQuality  | TRTCQualityInfo            | The upstream network quality. |
| remoteQuality |NSArray&lt;TRTCQualityInfo *&gt; | The downstream network quality. |

>? For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28).


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

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------------------------ |
| reason | NSInteger  | The reason. 0: The user stopped screen sharing; 1: Screen sharing was interrupted by another application. |
