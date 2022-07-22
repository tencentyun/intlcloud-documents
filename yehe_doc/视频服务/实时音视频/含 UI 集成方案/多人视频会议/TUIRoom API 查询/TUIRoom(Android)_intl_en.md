1. `TUIRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:
- A host can create a room, and users can enter the room ID to join the room.
- Room members can share their screens with each other.
- All users can send various text and custom messages.

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

`TUIRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, see [Group Audio/Video Room (Android)](https://intl.cloud.tencent.com/document/product/647/37283).
- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency audio/video room component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) for **Android** is used to implement the chat room feature.


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
| [createRoom](#createroom)                 | Creates a room (called by host).           |
| [destroyRoom](#destroyroom)               | Closes the room (called by host).           |
| [enterRoom](#enterroom)                   | Enters a room (called by a member)|
| [leaveRoom](#leaveroom)                   | Exits a room (called by other room members). |
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
| [setVideoMirror](#setvideomirror)         | Sets the mirror mode for local preview. |
| [setSpeaker](#setspeaker)                 | Sets whether to play sound from the device’s speaker or receiver.     |

### Remote user APIs

| API                                             | Description                                                         |
| ----------------------------------- | ---------------------------------- |
| [startRemoteView](#startremoteview) | Subscribes to and plays back the video of a specified remote member. |
| [stopRemoteView](#stopremoteview)   | Unsubscribes from and stops the playback of a remote video image.   |

### Chat message sending APIs

| API | Description |
| ----------------------------------- | -------------- |
| [sendChatMessage](#sendchatmessage)     | Sends a chat message.   |
| [sendCustomMessage](#sendcustommessage) | Sends a custom message. |

### Room control APIs

| API      | Description                         |
| --------------------------------------------------- | ------------------------------------------------------- |
| [muteUserMicrophone](#muteusermicrophone)           | Enables/Disables the mic of a specified user.                               |
| [muteAllUsersMicrophone](#muteallusersmicrophone)   | Enables/Disables the mic of all users and syncs the status to room information. |
| [muteUserCamera](#muteusercamera)                   | Enables/Disables the camera of a specified user.                               |
| [muteAllUsersCamera](#mutealluserscamera)           | Enables/Disables the camera of all users and syncs the status to room information. |
| [muteChatRoom](#mutechatroom)                       | Turns on/off chat (called by host).                     |
| [kickOffUser](#kickoffuser)                         | Removes a specified user from the room (called by host).                        |
| [startCallingRoll](#startcallingroll)               | Starts a roll call (called by host).                                        |
| [stopCallingRoll](#stopcallingroll)                 | Stops a roll call (called by host).                                        |
| [replyCallingRoll](#replycallingroll)               | Replies to a roll call (called by a member).                                    |
| [sendSpeechInvitation](#sendspeechinvitation)       | Sends a speech invitation to a member (called by host).                                    |
| [cancelSpeechInvitation](#cancelspeechinvitation)   | Cancels a speech invitation sent to a member (called by host).                                |
| [replySpeechInvitation](#replyspeechinvitation)     | Accepts/Rejects the speech invitation of the host (called by a member).                         |
| [sendSpeechApplication](#sendspeechapplication)     | Sends a speech request (called by a member).                                          |
| [replySpeechApplication](#replyspeechapplication)   | Approves/Rejects the speech request of a member (called by host).                         |
| [forbidSpeechApplication](#forbidspeechapplication) | Disables requests to speak (called by host).                                    |
| [sendOffSpeaker](#sendoffspeaker)                   | Stops the speech of a member (called by host).                                  |
| [sendOffAllSpeakers](#sendoffallspeakers)           | Stops the speech of all members in the room (called by host).                                  |
| [exitSpeechState](#exitspeechstate)                 | Stops speaking and becomes an audience member.                               |

### Screen sharing APIs

| API      | Description                         |
|-----|-----|
| [startScreenCapture](#startscreencapture)   | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture)   | Stops screen sharing. |

### Beauty filter APIs

| API      | Description                         |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager). |


### Settings APIs

| API                                             | Description                                                         |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | Sets network QoS control parameters. |

### SDK version APIs

| API | Description |
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | Gets the SDK version. |

## `TUIRoomCoreListener` API Overview[](id:TUIRoomCoreListener)

### Callbacks for error events

| API                          | Description           |
| ------------------- | ---------- |
| [onError](#onerror) | Callback for error.|

### Basic event callbacks

| API | Description |
| ------------------------------------------- | ------------------ |
| [onDestroyRoom](#ondestroyroom)             | The room was closed.     |
| [onUserVoiceVolume](#onuservoicevolume)     | Volume level. |
| [onRoomMasterChanged](#onroommasterchanged) | The host changed.   |

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
| [onReceiveChatMessage](#onreceivechatmessage)     | A text chat message was received. |
| [onReceiveRoomCustomMsg](#onreceiveroomcustommsg) | A custom message was received. |

### Room control event callbacks

| API      | Description                         |
| ------------------------------------------------------------ | ---------------------------------- |
| [onReceiveSpeechInvitation](#onreceivespeechinvitation)      | A member received a speech invitation from the host.       |
| [onReceiveInvitationCancelled](#onreceiveinvitationcancelled) | The speech invitation sent to a member was canceled by the host.    |
| [onReceiveSpeechApplication](#onreceivespeechapplication)    | The host received a speech request from a member.     |
| [onSpeechApplicationCancelled](#onspeechapplicationcancelled) | A member canceled a speech request.             |
| [onSpeechApplicationForbidden](#onspeechapplicationforbidden) | The host disabled requests to speak.           |
| [onOrderedToExitSpeechState](#onorderedtoexitspeechstate)    | A member was asked to stop speaking.         |
| [onCallingRollStarted](#oncallingrollstarted)                | The host started a roll call.   |
| [onCallingRollStopped](#oncallingrollstopped)                | The host stopped a roll call.   |
| [onMemberReplyCallingRoll](#onmemberreplycallingroll)        | A member replied to the roll call.   |
| [onChatRoomMuted](#onchatroommuted)                          | The host turned on/off chat.     |
| [onMicrophoneMuted](#onmicrophonemuted)                      | The host disabled mic use.         |
| [onCameraMuted](#oncameramuted)                              | The host disabled camera use.         |
| [onReceiveKickedOff](#onreceivekickedoff)                    | The host removed a member from the room.         |


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

This API is used to get the [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) singleton object.
```java
public static TUIRoomCore getInstance(Context context);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| context | Context | Android context, which will be converted to `ApplicationContext` for the system APIs to call. |


### destroyInstance

```java
void destroyInstance();
```

### setListener

This API is used to get the event callback of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283). You can use `TRTCVoiceRoomDelegate` to get various status notifications of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283).

```java
void setListener(TUIRoomCoreListener listener);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| listener | TUIRoomCoreListener | Event callback class. |

### createRoom

This API is used to create a room (called by the host).
```java
void createRoom(String roomId, TUIRoomCoreDef.SpeechMode speechMode, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
|-----------| ------------- | -------------------------------------- |
| roomId  | String  | The room ID. You need to assign and manage the IDs in a centralized manner. |
| speechMode| TUIRoomCoreDef.SpeechMode | The speech mode. |
| callback | TUIRoomCoreCallback.ActionCallback | The result of room creation. |

Generally, the host calls the APIs in the following steps:
1. The **host** calls `createRoom()` to create a room, the result of which is returned via `TUIRoomCoreCallback.ActionCallback`.
2. The **host** calls `startCameraPreview()` to enable camera capturing and preview.
3. The **host** calls `startLocalAudio()` to enable the local mic.

### destroyRoom

This API is used to close a room (called by the host).
```java
void destroyRoom(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | Room termination result. |

### enterRoom

This API is used to enter a room (called by a member).
```java
void enterRoom(String roomId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| roomId | String | The room ID. |
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

  The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | Result. |

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

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId    | String | The user ID. |
| callback | UIRoomCoreCallback.UserInfoCallback | Room member details. |


### setSelfProfile

This API is used to set user profile.
```java
void setSelfProfile(String userName, String avatarURL, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| ---------- | ------ | -------------- |
| userName  | String | The username.  |
| avatarURL | String | The URL of the user profile photo. |
| callback | TUIRoomCoreCallback.ActionCallback | Whether the setting succeeded. |


### transferRoomMaster

This API is used to transfer a room to another user.
```java
 void transferRoomMaster(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userId    | String | The user ID. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


## Local Push APIs

### startCameraPreview

This API is used to start the preview of the local camera.
```java
void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| isFront | boolean | `true`: Front camera; `false`: Rear camera |
| view | TXCloudVideoView | The control that loads video images. |


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

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| quality | int | Captured sound quality: <li/>TRTC_AUDIO_QUALITY_MUSIC<li/>TRTC_AUDIO_QUALITY_DEFAULT<li/>TRTC_AUDIO_QUALITY_SPEECH |

### stopLocalAudio

This API is used to stop mic capturing.
```java
void stopLocalAudio();
```

### setVideoMirror

This API is used to set the mirror mode for local preview.
```java
 void setVideoMirror(int type);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| type | int | Mirroring type. |

### setSpeaker

This API is used to set whether to play sound from the device’s speaker or receiver.
```java
 void setSpeaker(boolean isUseSpeaker);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | -------------- | ---------- |
| isUseSpeaker | boolean | true: Speaker; false: Receiver. |

## Remote User APIs

### startRemoteView
This API is used to subscribe to a remote user's video stream.

```java
void startRemoteView(String userId, TXCloudVideoView view, TUIRoomCoreDef.SteamType streamType, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------------- | ------------- | -------------------------- |
| userId  | String  | The ID of the user whose video image is to be played back. |
| view | TXCloudVideoView  | The control that loads video images. |
| streamType  | TUIRoomCoreDef.SteamType | The stream type. |
| callback  | TUIRoomCoreCallback.ActionCallback | Result. |


### stopRemoteView

This API is used to unsubscribe from and stop the playback of a remote video image.
```java
void stopRemoteView(String userId, TUIRoomCoreCallback.ActionCallback callback);

```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| userId | String  | The ID of the user whose video image is to be stopped. |
| callback  | TUIRoomCoreCallback.ActionCallback | Result. |

### switchCamera

This API is used to switch between the front and rear cameras.
```java
void switchCamera(boolean isFront);

```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------------- | ----------------------- |
| isFront | boolean | true: Front camera; false: Rear camera. |

## Message Sending APIs

### sendChatMessage

Broadcast a text chat message in the room. This API is generally used for text chat.
```java
void sendChatMessage(String message, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| message | String | Message content. |
| callback  | TUIRoomCoreCallback.ActionCallback | Callback of the operation. |


### sendCustomMessage

This API is used to send a custom message.
```java
void sendCustomMessage(String data, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

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

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| The User ID.  |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### muteAllUsersMicrophone

This API is used to enable/disable the mics of all users.
```java
void muteAllUsersMicrophone(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | ---- | ---------- |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### muteUserCamera

This API is used to enable/disable the cameras of the specified user.
```java
void muteUserCamera(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| The User ID.  |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### muteAllUsersCamera

This API is used to enable/disable the cameras of all users.
```java
void muteAllUsersCamera(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | ---- | ---------- |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### muteChatRoom

This API is used to forbid/allow text chat.
```java
void muteChatRoom(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
| ---- | ---- | ---------- |
| mute  | boolean  | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### kickOffUser

This API is used by the host to remove a member from the room.
```java
void kickOffUser(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| The User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### startCallingRoll

This API is used by the host to start a roll call.
```java
 void startCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### stopCallingRoll

This API is used by the host to stop a roll call.
```java
 void stopCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
 
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### replyCallingRoll

This API is used by a member to reply to the roll call.
```java
void replyCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### sendSpeechInvitation

This API is used by the host to invite a member to speak.
```java
void sendSpeechInvitation(String userId, TUIRoomCoreCallback.InvitationCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| The User ID.  |
| callback | TUIRoomCoreCallback.InvitationCallback | Result. |

### cancelSpeechInvitation

This API is used by the host to cancel the speech invitation sent to a member.
```java
 void cancelSpeechInvitation(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| The User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### replySpeechInvitation

This API is used by a member to accept/reject an invitation to speak by the host.
```java
void replySpeechInvitation(boolean agree, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree | boolean  | Whether to approve. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### sendSpeechApplication

This API is used by a member to request to speak.
```java
void sendSpeechApplication(TUIRoomCoreCallback.InvitationCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.InvitationCallback | Result. |

### cancelSpeechApplication

This API is used by a member to cancel their request to speak.
```java
void cancelSpeechApplication(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### replySpeechApplication

This API is used by the host to approve/reject a speech request sent by a member.
```java
void replySpeechApplication(boolean agree, String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| agree  | boolean| Whether to approve. |
| userId  | String| The User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### forbidSpeechApplication

This API is used by the host to disable requests to speak.
```java
 void forbidSpeechApplication(boolean forbid, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---- | ---------- |
| forbid | boolean | Whether to disable. |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


### sendOffSpeaker

This API is used by the host to stop the speech of the specified member.
```java
void sendOffSpeaker(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| userId  | String| The User ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### sendOffAllSpeakers

This API is used by the host to stop the speech of all members.
```java
void sendOffAllSpeakers(TUIRoomCoreCallback.ActionCallback callback);
```

The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |

### exitSpeechState

This API is used to stop speaking and become an audience member.
```java
void exitSpeechState(TUIRoomCoreCallback.ActionCallback callback);
```
The parameters are described below:

| Parameter | Type | Description |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | Callback of the result. |


## Screen Sharing APIs
### startScreenCapture

This API is used to start screen sharing.
```java
void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | Screen sharing encoding parameters. We recommend you use the above configuration. If you set `encParams` to `null`, the encoding parameter settings before `startScreenCapture` is called will be used. |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | Special screen sharing configuration. We recommend you set `floatingView` which can prevent the application from being killed by the system and help protect user privacy. |

>? For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).

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

This API is used to set QoS parameters.
```java
 void setVideoQosPreference(TRTCCloudDef.TRTCNetworkQosParam preference);
```

The parameters are described below:

| Parameter | Type | Description |
| ---------- | --------------------- | -------------- |
| preference | TRTCCloudDef.TRTCNetworkQosParam | Network QoS control policy. |

### setAudioQuality

This API is used to set audio quality.
```java
void setAudioQuality(int quality);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| quality | int | Audio quality. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |

### setVideoResolution

This API is used to set the resolution.

```java
void setVideoResolution(int resolution);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| resolution | int | Video resolution. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87). |


### setVideoFps

This API is used to set the frame rate.
```java
void setVideoFps(int fps);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| fps | int | Video capturing frame rate. |

>?**Recommended value:** 15 or 20 fps. Video will stutter severely if the frame rate is lower than 5 fps and slightly if it is lower than 10 fps. Setting the frame rate to higher than 20 fps would be a waste of resources (the frame rate of films is 24 fps).


### setVideoBitrate

This API is used to set the bitrate.
```java
void setVideoBitrate(int bitrate);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| bitrate | int  | Bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html). |

>? **Recommended value:** See the optimal bitrate for each tier in `TRTCVideoResolution`. You can also slightly increase the optimal bitrate. For example, `TRTC_VIDEO_RESOLUTION_1280_720` corresponds to the target bitrate of 1,200 Kbps, and you can also set the bitrate to 1,500 Kbps for higher definition.

### enableAudioEvaluation

This API is used to enable the volume reminder.
```java
void enableAudioEvaluation(boolean enable);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| enable | boolean  | true: Enable; false: Disable. |

>? After this feature is enabled, the result of volume evaluation by the SDK will be obtained in `onUserVolumeUpdate`.

### setAudioPlayVolume

This API is used to set the playback volume.
```java
void setAudioPlayVolume(int volume);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| volume | int | Playback volume. Value range: 0–100. Default value: 100. |

### setAudioCaptureVolume

This API is used to set the mic capturing volume.
```java
void setAudioCaptureVolume(int volume);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| volume | int | Capture volume. Value range: 0–100. Default value: 100. |

### startFileDumping

This API is used to start audio recording.
```java
void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | Audio recording parameters. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams). |

>? After this API is called, the SDK will record all audios of a call, including the local audio, remote audios, and background music, into a single file. This API works regardless of whether you are in the room or not. When `leaveRoom` is called, audio recording will stop automatically.

### stopFileDumping

This API is used to stop audio recording.
```java
void stopFileDumping();
```

## SDK Version APIs

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

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| code    | int    | Error code   |
| message | String | Error message |

## Basic Event Callbacks

### onDestroyRoom

The room was closed.
```java
void onDestroyRoom();
```

### onUserVoiceVolume

User volume level.
```java
void onUserVoiceVolume(String userId, int volume);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------------------------------- |
| userID | String | The User ID. |
| volume | int | User volume level. Value range: 0–100. |

### onRoomMasterChanged

The host changed.
```java
void onRoomMasterChanged(String previousUserId, String currentUserId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| previousUserId | String | Host’s user ID before the change. |
| currentUserId | String | Host’s user ID after the change. |


## Remote User Callbacks

### onRemoteUserEnter

A remote user entered the room.
```java
void onRemoteUserEnter(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |

### onRemoteUserLeave

A remote user exited the room.
```java
void onRemoteUserLeave(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |

### onRemoteUserCameraAvailable

Whether a remote user enabled the camera.
```java
void onRemoteUserCameraAvailable(String userId, boolean available);
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| String | The User ID. |
| available | boolean| true: Enabled; false: Disabled. |

### onRemoteUserScreenVideoAvailable

A member **enabled/disabled** video sharing.
```java
void onRemoteUserScreenVideoAvailable(String userId, boolean available);
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| String | The User ID. |
| available | boolean| Whether screen sharing stream data is available. |

### onRemoteUserAudioAvailable

Whether a remote user is sending audio.
```java
void onRemoteUserAudioAvailable(String userId, boolean available);
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ------ | ----------------------------------------- |
| userId| String | The User ID. |
| available | boolean| Whether audio data is available. |

### onRemoteUserEnterSpeechState

A remote user started speaking.
```java
void onRemoteUserEnterSpeechState(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |

### onRemoteUserExitSpeechState

A remote user stopped speaking.
```java
void onRemoteUserExitSpeechState(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |


## Chat Room Message Event Callbacks

### onReceiveChatMessage

A text chat message was received.
```java
void onReceiveChatMessage(String userId, String message);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ---------- |
| userID | String | The User ID. |
| message | String | Text message |

### onReceiveRoomCustomMsg

A custom message was received.
```java
void onReceiveRoomCustomMsg(String userId, String data);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | The User ID. |
| message | String | Custom message. |

## Room Control Message Callbacks

### onReceiveSpeechInvitation

A member received a speech invitation from the host.
```java
void onReceiveSpeechInvitation(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | The host's user ID. |

### onReceiveInvitationCancelled

The speech invitation sent to a member was canceled by the host.
```java
void onReceiveInvitationCancelled(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | The host's user ID. |


### onReceiveSpeechApplication

The host received a speech request from a member.
```java
void onReceiveSpeechApplication(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |

### onSpeechApplicationCancelled

A user canceled a speech request.
```java
void onSpeechApplicationCancelled(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |

### onSpeechApplicationForbidden

The host disabled requests to speak.
```java
void onSpeechApplicationForbidden(boolean isForbidden);
```

The parameters are described below:

| Parameter | Type | Description |
| --------- | ---- | ---------- |
| isForbidden | boolean | Whether to disable. |

### onOrderedToExitSpeechState

A member was asked to stop speaking.
```java
void onOrderedToExitSpeechState(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | ------------ |
| userId | String | The host's user ID. |


### onCallingRollStarted

The host started a roll call.
```java
void onCallingRollStarted(String userId);
```

### onCallingRollStopped

The host stopped a roll call.
```java
void onCallingRollStopped(String userId);
```

### onMemberReplyCallingRoll

A member replied to the roll call.
```java
void onMemberReplyCallingRoll(String userId);
```

The parameters are described below:

| Parameter | Type | Description |
| ------- | ------ | --------- |
| userId | String | The User ID. |

### onChatRoomMuted

The host turned on/off chat.
```java
void onChatRoomMuted(boolean muted);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | boolean | Whether to disable. |

### onMicrophoneMuted

The host disabled mic use.
```java
void onMicrophoneMuted(boolean muted);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | boolean | Whether to disable. |

### onCameraMuted

The host disabled camera use.
```java
void onCameraMuted(boolean muted);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| muted | boolean | Whether to disable. |

### onReceiveKickedOff

The host removed a member from the room.
```java
void onReceiveKickedOff(String userId);
```

The parameters are described below:

| Parameter        | Type    | Description                                                                                                      |
| ----- | ---- | ---------- |
| userId | String | The user ID of the host/admin. |

## Statistics Collection and Quality Callbacks

### onStatistics

Callback of technical metric statistics.
```java
void onStatistics(TRTCStatistics statistics);
```

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | Statistics. |

### onNetworkQuality

Network quality.
```java
void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);

```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | Upstream network quality. |
| remoteQuality | List&amp;lt;TRTCCloudDef.TRTCQuality&amp;gt; | Downstream network quality. |

>? For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b).


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

The parameters are described below:

| Parameter | Type | Description |
| ------ | ---- | ------------------------------------------------------ |
| reason | int  | Reason for stop. 0: The user stopped screen sharing; 1: Interrupted by another application. |
