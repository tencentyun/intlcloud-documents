1. `TUIRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). `TUIRoom` includes the following features:
- The anchor can create a room, and members can enter the room ID to join the room.
- Room members can share their screens with each other.
- All users can send various text and custom messages.

2. `TUIRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Group Audio/Video Room (for Android)](https://intl.cloud.tencent.com/document/product/647/37283).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video room component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) for **Android** is used to implement the chat room feature.


## `TUIRoom` API Overview

### Basic functions of `TUIRoomCore`

| API | Description |
| ----------------------------------- | -------------- |
| [getInstance](#getinstance)         | Gets a singleton object. |
| [destroyInstance](#destroyinstance) | Terminates a singleton object. |
| [setListener](#setlistener)         | Sets event callbacks. |

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
| [exitSpeechState](#exitspeechstate)                 | Stops speech by a member and changes their role to audience.                              |

### Screen sharing APIs

| API          | Description         |
|-----|-----|
| [startScreenCapture](#startscreencapture)   | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture)     | Stops screen sharing. |

### Beauty filter APIs

| API          | Description         |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager). |


### Settings APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | Sets network bandwidth limit parameters. |

### SDK version acquisition APIs

| API | Description |
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | Gets the SDK version. |

## `TUIRoomCoreListener` API Overview[](id:TUIRoomCoreListener)

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
| [onReceiveChatMessage](#onreceivechatmessage)     | A text message was received. |
| [onReceiveRoomCustomMsg](#onreceiveroomcustommsg) | A custom message was received. |

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

This API is used to get a [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) singleton object.
```java
public static TUIRoomCore getInstance(Context context);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| context | Context | Android context, which will be converted to `ApplicationContext` for the system APIs to call. |


### destroyInstance

```java
void destroyInstance();
```

### setListener

This API is used to set the event callback of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283). You can use `TUIRoomCoreListener` to get different status notifications of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283).

```java
void setListener(TUIRoomCoreListener listener);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| listener | TUIRoomCoreListener | Event callback class. |

### createRoom

This API is used to create a room (called by the anchor).
```java
void createRoom(String roomId, TUIRoomCoreDef.SpeechMode speechMode, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----------| ------------- | -------------------------------------- |
| roomId  | String  | Room ID. You need to assign and manage the IDs in a centralized manner. |
| speechMode| TUIRoomCoreDef.SpeechMode | Speech mode. |
| callback | TUIRoomCoreCallback.ActionCallback | Room creation result. |

Generally, the anchor calls the APIs in the following steps:
1. The **anchor** calls `createRoom()` to create a room, the result of which is returned via `TUIRoomCoreCallback.ActionCallback`.
2. The **anchor** calls `startCameraPreview()` to enable camera capturing and preview.
3. The **anchor** calls `startLocalAudio()` to enable the local mic.

### destroyRoom

This API is used to terminate a room (called by the anchor).
```java
void destroyRoom(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | Room termination result. |

### enterRoom

This API is used to enter a room (called by a member).
```java
void enterRoom(String roomId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| roomId | String | Room ID. |
| callback | UIRoomCoreCallback.ActionCallback | Result. |


Generally, a member enters a room in the following steps:
1. The **member** calls `enterRoom` and passes in `roomId` to enter the room.
2. The **member** calls `startCameraPreview()` to enable camera preview and calls startLocalAudio()` to enable mic capturing.
3. The **member** receives the `onRemoteUserCameraAvailable` event and calls `startRemoteView()` to start playback.

### leaveRoom

This API is used to exit a room (called by a member).
```java
 void leaveRoom(TUIRoomCoreCallback.ActionCallback callback);
```

  The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | Result.|

### getRoomInfo

This API is used to get the room information.
```java
TUIRoomCoreDef.RoomInfo getRoomInfo();
```

### getRoomUsers

This API is used to get the information of all users in the room.
```java
 List<TUIRoomCoreDef.UserInfo> getRoomUsers();
```

### getUserInfo

This API is used to get the information of a user in the room.
```java
void getUserInfo(String userId, TUIRoomCoreCallback.UserInfoCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId    | String | User ID |
| callback | UIRoomCoreCallback.UserInfoCallback | Room member details. |


### setSelfProfile

Set User Info
```java
void setSelfProfile(String userName, String avatarURL, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are listed below:

| Parameter | Type | Description |
| ---------- | ------ | -------------- |
| userName  | String | User name. |
| avatarURL | String | User profile photo URL.  |
| callback | TUIRoomCoreCallback.ActionCallback | Whether the setting succeeded. |


### transferRoomMaster

This API is used to transfer a group to another user.
```java
 void transferRoomMaster(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId    | String | User ID |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


## Local Push APIs

### startCameraPreview

This API is used to start the preview of the local camera.
```java
void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| isFront | Boolean | `true`: front camera; `false`: rear camera |
| view | TXCloudVideoView | The control that loads video images |


### stopCameraPreview

This API is used to stop the preview of the local camera.
```java
 void stopCameraPreview();
```

### startLocalAudio

This API is used to start mic capturing.
```java
 void startLocalAudio(int quality);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| quality | int | Captured sound quality: <li/>TRTC_AUDIO_QUALITY_MUSIC<li/>TRTC_AUDIO_QUALITY_DEFAULT<li/>TRTC_AUDIO_QUALITY_SPEECH |

### stopLocalAudio

This API is used to stop mic capturing.
```java
void stopLocalAudio();
```

### setVideoMirror

This API is used to set the mirroring preview mode of local video image.
```java
 void setVideoMirror(int type);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| type | int | Mirroring type. |

### setSpeaker

This API is used to set whether to use the speaker or receiver.
```java
 void setSpeaker(boolean isUseSpeaker);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | -------------- | ---------- |
| isUseSpeaker | boolean | true: device speaker; false: device receiver. |

## Remote User APIs

### startRemoteView
This API is used to subscribe to a remote user's video stream.

```java
void startRemoteView(String userId, TXCloudVideoView view, TUIRoomCoreDef.SteamType streamType, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------------- | ------------- | -------------------------- |
| userId | String | ID of the user whose video image is to be played back. |
| view | TXCloudVideoView | The control that loads video images. |
| streamType  | TUIRoomCoreDef.SteamType | Stream type. |
| callback  | TUIRoomCoreCallback.ActionCallback | Result. |


### stopRemoteView

This API is used to unsubscribe from and stop the playback of a remote video image.
```java
void stopRemoteView(String userId, TUIRoomCoreCallback.ActionCallback callback);

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| userId | String | ID of the user whose video image is to be stopped. |
| callback  | TUIRoomCoreCallback.ActionCallback | Result. |

### switchCamera

This API is used to switch between the front and rear cameras.
```java
void switchCamera(boolean isFront);

```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| isFront | Boolean | true: front camera; false: rear camera. |

## Message Sending APIs

### sendChatMessage

This API is used to broadcast a text message in a room, which is generally used for text chat.
```java
void sendChatMessage(String message, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Message content. |
| callback  | TUIRoomCoreCallback.ActionCallback | Callback of the operation. |


### sendCustomMessage

Sending Custom Messages
```java
void sendCustomMessage(String data, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| data | String | Message content. |
| callback  | TUIRoomCoreCallback.ActionCallback | Callback of the operation. |

## Room Control APIs

### muteUserMicrophone

This API is used to enable/disable the mic of the specified user.
```java
void muteUserMicrophone(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| User ID.  |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### muteAllUsersMicrophone

This API is used to enable/disable the mic of all users.
```java
void muteAllUsersMicrophone(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---- | ---------- |
| mute | boolean | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### muteUserCamera

This API is used to enable/disable the camera of the specified user.
```java
void muteUserCamera(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| User ID.  |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### muteAllUsersCamera

This API is used to enable/disable the camera of all users.
```java
void muteAllUsersCamera(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---- | ---------- |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### muteChatRoom

This API is used to forbid/allow text chat.
```java
void muteChatRoom(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ---- | ---- | ---------- |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### kickOffUser

This API is used by the anchor to remove a member.
```java
void kickOffUser(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### startCallingRoll

This API is used by the anchor to start roll call.
```java
 void startCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### stopCallingRoll

This API is used by the anchor to stop roll call.
```java
 void stopCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
 
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### replyCallingRoll

This API is used by a member to reply to roll call.
```java
void replyCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### sendSpeechInvitation

This API is used by the anchor to invite a member to speak.
```java
void sendSpeechInvitation(String userId, TUIRoomCoreCallback.InvitationCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| User ID.  |
| callback | TUIRoomCoreCallback.InvitationCallback | Result. |

### cancelSpeechInvitation

This API is used by the anchor to cancel the speech invitation to a member.
```java
 void cancelSpeechInvitation(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### replySpeechInvitation

This API is used by a member to accept/reject the speech invitation from the anchor.
```java
void replySpeechInvitation(boolean agree, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree | boolean  | Whether the invitation was accepted. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### sendSpeechApplication

This API is used by a member to apply to speak.
```java
void sendSpeechApplication(TUIRoomCoreCallback.InvitationCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.InvitationCallback | Result. |

### cancelSpeechApplication

This API is used by a member to cancel the speech application.
```java
void cancelSpeechApplication(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### replySpeechApplication

This API is used by the anchor to approve/reject the speech application of a member.
```java
void replySpeechApplication(boolean agree, String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree  | Boolean| Whether the invitation was accepted. |
| userId  | String| User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### forbidSpeechApplication

This API is used by the anchor to forbid speech application.
```java
 void forbidSpeechApplication(boolean forbid, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ---------- |
| forbid | boolean | Whether speech application is forbidden. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### sendOffSpeaker

This API is used by the anchor to stop the speech of the specified member.
```java
void sendOffSpeaker(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### sendOffAllSpeakers

This API is used by the anchor to stop the speech of all members.
```java
void sendOffAllSpeakers(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### exitSpeechState

This API is used for a member to stop speaking and change their role to audience.
```java
void exitSpeechState(TUIRoomCoreCallback.ActionCallback callback);
```
The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


## Screen Sharing APIs
### startScreenCapture

This API is used to start screen sharing.
```java
void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | Screen sharing encoding parameters. We recommend you use the above configuration. If you set `encParams` to `null`, the encoding parameter settings before `startScreenCapture` is called will be used. |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | Special screen sharing configuration. We recommend you set `floatingView` which can prevent the application from being killed by the system and help protect user privacy. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).

### stopScreenCapture

This API is used to stop screen capturing.
```java
void stopScreenCapture();
```

## Beauty Filter APIs
### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).
```java
TXBeautyManager getBeautyManager();
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
```java
 void setVideoQosPreference(TRTCCloudDef.TRTCNetworkQosParam preference);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | --------------------- | -------------- |
| preference | TRTCCloudDef.TRTCNetworkQosParam | Network bandwidth limit policy. |

### setAudioQuality

This API is used to set audio quality.
```java
void setAudioQuality(int quality);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| quality | int | Audio quality. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |

### setVideoResolution

This API is used to set the resolution.

```java
void setVideoResolution(int resolution);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| resolution | int | Video resolution. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87). |


### setVideoFps

This API is used to set the frame rate.
```java
void setVideoFps(int fps);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| fps | int | Video capturing frame rate. |

>?**Recommended value:** 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lagging; if lower than 10 fps but higher than 5 fps, there will be slight lagging; if higher than 20 fps, too many resources will be wasted (the frame rate of movies is generally 24 fps).


### setVideoBitrate

This API is used to set the bitrate.
```java
void setVideoBitrate(int bitrate);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| bitrate | int  | Bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html). |

>? **Recommended value:** please see the optimal bitrate for each tier in `TRTCVideoResolution`. You can also slightly increase the optimal bitrate. For example, `TRTC_VIDEO_RESOLUTION_1280_720` corresponds to the target bitrate of 1,200 Kbps, and you can also set the bitrate to 1,500 Kbps for higher definition.

### enableAudioEvaluation

This API is used to enable the volume reminder.
```java
void enableAudioEvaluation(boolean enable);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| enable | boolean  | true: enable; false: disable. |

>? After this feature is enabled, the result of volume evaluation by the SDK will be obtained in `onUserVolumeUpdate`.

### setAudioPlayVolume

This API is used to set the playback volume.
```java
void setAudioPlayVolume(int volume);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| volume | int | Playback volume. Value range: 0–100. Default value: 100. |

### setAudioCaptureVolume

This API is used to set the mic capturing volume.
```java
void setAudioCaptureVolume(int volume);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| volume | int | Capture volume. Value range: 0–100. Default value: 100. |

### startFileDumping

This API is used to start audio recording.
```java
void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | Audio recording parameters. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams). |

>? After this API is called, the SDK will record all audio of a call, including local audio, remote audio, and background music, into a file. This API works regardless of whether a user is in the room. When `leaveRoom` is called, audio recording will stop automatically.

### stopFileDumping

This API is used to stop audio recording.
```java
void stopFileDumping();
```

## SDK Version Acquisition APIs

### getSdkVersion

This API is used to get SDK version information.
```java
int getSdkVersion();
```

## Error Event Callbacks
### onError

```java
void onError(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Error message |

## Basic Event Callbacks

### onDestroyRoom

Room dismissal.
```java
void onDestroyRoom();
```

### onUserVoiceVolume

User volume level.
```java
void onUserVoiceVolume(String userId, int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------------------------------- |
| userID | String | User ID |
| volume | int | User volume level. Value range: 0–100. |

### onRoomMasterChanged

Anchor change.
```java
void onRoomMasterChanged(String previousUserId, String currentUserId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| previousUserId | String | Anchor's user ID before change. |
| currentUserId | String | Anchor's user ID after change. |


## Remote User Callbacks

### onRemoteUserEnter

A remote user entered the room.
```java
void onRemoteUserEnter(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |

### onRemoteUserLeave

A remote user exited the room.
```java
void onRemoteUserLeave(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |

### onRemoteUserCameraAvailable

Whether a remote user enabled the camera.
```java
void onRemoteUserCameraAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| String | User ID. |
| available | boolean| true: enabled; false: disabled. |

### onRemoteUserScreenVideoAvailable

A member **enabled/disabled** video sharing.
```java
void onRemoteUserScreenVideoAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| String | User ID. |
| available | boolean| Whether screen sharing stream data is available. |

### onRemoteUserAudioAvailable

Whether a remote user is sending audio.
```java
void onRemoteUserAudioAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| String | User ID. |
| available | boolean| Whether audio data is available. |

### onRemoteUserEnterSpeechState

A remote user started speaking.
```java
void onRemoteUserEnterSpeechState(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |

### onRemoteUserExitSpeechState

A remote user stopped speaking.
```java
void onRemoteUserExitSpeechState(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |


## Chat Room Message Event Callbacks

### onReceiveChatMessage

Callback for receiving a text message.
```java
void onReceiveChatMessage(String userId, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userID | String | User ID |
| message | String | Text message |

### onReceiveRoomCustomMsg

Callback for receiving a custom message.
```java
void onReceiveRoomCustomMsg(String userId, String data);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | User ID |
| message | String | Custom message content. |

## Room Control Message Callbacks

### onReceiveSpeechInvitation

A user received a speech invitation from the anchor.
```java
void onReceiveSpeechInvitation(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | Anchor's user ID. |

### onReceiveInvitationCancelled

A user received a speech invitation cancellation from the anchor.
```java
void onReceiveInvitationCancelled(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | Anchor's user ID. |


### onReceiveSpeechApplication

The anchor received a speech application from a member.
```java
void onReceiveSpeechApplication(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |

### onSpeechApplicationCancelled

A user canceled a speech application.
```java
void onSpeechApplicationCancelled(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |

### onSpeechApplicationForbidden

The anchor forbidden a speech application.
```java
void onSpeechApplicationForbidden(boolean isForbidden);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | ---- | ---------- |
| isForbidden | boolean | Whether to forbid. |

### onOrderedToExitSpeechState

A member was asked to stop speaking.
```java
void onOrderedToExitSpeechState(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | Anchor's user ID. |


### onCallingRollStarted

The anchor started a roll call.
```java
void onCallingRollStarted(String userId);
```

### onCallingRollStopped

The anchor stopped a roll call.
```java
void onCallingRollStopped(String userId);
```

### onMemberReplyCallingRoll

A member replied to roll call.
```java
void onMemberReplyCallingRoll(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | User ID |

### onChatRoomMuted

The anchor muted/unmuted the room.
```java
void onChatRoomMuted(boolean muted);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | boolean | Whether to disable. |

### onMicrophoneMuted

The anchor disabled the mic.
```java
void onMicrophoneMuted(boolean muted);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | boolean | Whether to disable. |

### onCameraMuted

The anchor disabled the camera.
```java
void onCameraMuted(boolean muted);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | boolean | Whether to disable. |

### onReceiveKickedOff

The anchor removed a member.
```java
void onReceiveKickedOff(String userId);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| userId | String | Anchor/Admin's user ID. |

## Statistics Collection and Quality Callbacks

### onStatistics

Callback of technical metric statistics.
```java
void onStatistics(TRTCStatistics statistics);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | Statistics. |

### onNetworkQuality

Network quality.
```java
void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);

```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | Upstream network quality. |
| remoteQuality | List&amp;lt;TRTCCloudDef.TRTCQuality&amp;gt; | Downstream network quality. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b).


## Screen Sharing Event Callbacks

### onScreenCaptureStarted

Screen sharing started.

```java
 void onScreenCaptureStarted();
```

### onScreenCaptureStopped

Screen sharing stopped.

```java
void onScreenCaptureStopped(int reason);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------------------------ |
| reason | int  | Reason for stop. 0: the user stopped proactively; 1: stopped due to preemption by another application. |
