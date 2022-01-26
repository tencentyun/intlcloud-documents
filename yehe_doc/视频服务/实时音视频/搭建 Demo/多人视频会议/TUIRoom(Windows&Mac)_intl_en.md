`TUIRoom` is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:
- The anchor can create a room, and the member can enter the room ID to join the room.
- The participants can share their screens with each other.
- All users can send various text and custom messages.

`TUIRoom` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Group Audio/Video Room (for Windows and macOS)](https://intl.cloud.tencent.com/document/product/647/44071).
- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency video conferencing component.
- IM SDK: the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) for **C++** is used to implement the chat room feature.


## `TUIRoom` API Overview[](id:TUIRoom)

### Basic functions of `TUIRoomCore`

| API                                 | Description           |
|-----|-----|
| [GetInstance](#getinstance)         | Gets a singleton object. |
| [DestroyInstance](#destroyinstance) | Terminates a singleton object. |
| [SetCallback](#setcallback)         | Sets event callback. |

### Room APIs

| API                                             | Description                                                         |
|-----|-----|
| [login](#login)                           | Logs in.                             |
| [logout](#logout)                         | Logs out.                             |
| [CreateRoom](#createroom)                 | Creates a room (called by anchor).           |
| [DestroyRoom](#destroyroom)               | Terminates a room (called by anchor).           |
| [EnterRoom](#enterroom)                   | Enters a room (called by member).         |
| [LeaveRoom](#leaveroom)                   | Exits a room (called by member or anchor). |
| [GetRoomInfo](#getroominfo)               | Gets the room information.                     |
| [GetRoomUsers](#getroomusers)             | Gets the information of all users in the room.           |
| [GetUserInfo](#getuserinfo)               | Gets the information of a user.               |
| [TransferRoomMaster](#transferroommaster) | Transfers the anchor permission (called by anchor).     |

### Local audio/video operation APIs

| API                                                   | Description                       |
|-----|-----|
| [StartCameraPreview](#startcamerapreview)             | Enables the preview of the local video.   |
| [StopCameraPreview](#stopcamerapreview)               | Stops local video capturing and preview.   |
| [UpdateCameraPreview](#updatecamerapreview)           | Updates the local video rendering window.     |
| [StartLocalAudio](#startlocalaudio)                   | Enables mic capturing.           |
| [StopLocalAudio](#stoplocalaudio)                     | Stops mic capturing.           |
| [StartSystemAudioLoopback](#startsystemaudioloopback) | Enables system audio capturing.  |
| [StopSystemAudioLoopback](#stopsystemaudioloopback)   | Disables system audio capturing.  |
| [SetVideoMirror](#setvideomirror)                     | Sets the mirroring preview mode of the local image. |

### Remote user APIs

| API                                   | Description                               |
|-----|-----|
| [StartRemoteView](#startremoteview)   | Subscribes to and plays back the remote video image of a specified member. |
| [StopRemoteView](#stopremoteview)     | Unsubscribes from and stops the playback of a remote video image.   |
| [UpdateRemoteView](#updateremoteview) | Updates the video rendering window of a remote user.      |

### Chat message sending APIs

| API                                     | Description             |
|-----|-----|
| [SendChatMessage](#sendchatmessage)     | Sends a chat message.   |
| [SendCustomMessage](#sendcustommessage) | Sends a custom message. |

### Room control APIs

| API                                                 | Description                                                    |
|-----|-----|
| [MuteUserMicrophone](#muteusermicrophone)           | Enables/Disables the mic of a specified user.                               |
| [MuteAllUsersMicrophone](#muteallusersmicrophone)   | Enables/Disables the mic of all users and syncs the status to room information. |
| [MuteUserCamera](#muteusercamera)                   | Enables/Disables the camera of a specified user.                               |
| [MuteAllUsersCamera](#mutealluserscamera)           | Enables/Disables the camera of all users and syncs the status to room information. |
| [MuteChatRoom](#mutechatroom)                       | Mutes/Unmutes the chat room (called by anchor).                     |
| [KickOffUser](#kickoffuser)                         | Removes a specified user in the room (called by anchor).                        |
| [StartCallingRoll](#startcallingroll)               | Starts calling roll by the anchor.                                        |
| [StopCallingRoll](#stopcallingroll)                 | Stops calling roll by the anchor.                                        |
| [ReplyCallingRoll](#replycallingroll)               | Replies to roll call by a member.                                    |
| [SendSpeechInvitation](#sendspeechinvitation)       | Invites a member to speak by the anchor.                                    |
| [CancelSpeechInvitation](#cancelspeechinvitation)   | Cancels invitation to a member for speech by the anchor.                                |
| [ReplySpeechInvitation](#replyspeechinvitation)     | Accepts/Rejects the speech invitation from the anchor by a member.                         |
| [SendSpeechApplication](#sendspeechapplication)     | Applies for speech by a member.                                          |
| [CancelSpeechApplication](#cancelspeechapplication) | Cancels speech application by a member.                                      |
| [ReplySpeechApplication](#replyspeechapplication)   | Approves/Rejects the speech application of a member by the anchor.                         |
| [ForbidSpeechApplication](#forbidspeechapplication) | Forbids speech application by the anchor.                                    |
| [SendOffSpeaker](#sendoffspeaker)                   | Stops the speech of a member by the anchor.                                  |
| [SendOffAllSpeakers](#sendoffallspeakers)           | Stops the speech of all members by the anchor.                                  |
| [ExitSpeechState](#exitspeechstate)                 | Stops speaking by a member and changes their role to audience.                               |

### Basic component API functions

| API                                             | Description                                       |
|-----|-----|
| [GetDeviceManager](#getdevicemanager)           | Gets the local settings management object `ITXDeviceManager`.    |
| [GetScreenShareManager](#getscreensharemanager) | Gets the screen sharing management object `IScreenShareManager`. |

### On-cloud recording API functions

| API                                   | Description          |
|-----|-----|
| [StartCloudRecord](#startcloudrecord) | Starts on-cloud recording. |
| [StopCloudRecord](#stopcloudrecord)   | Stops on-cloud recording. |

### Beauty filter APIs

| API                                             | Description                                                         |
|-----|-----|
| [SetBeautyStyle](#setbeautystyle) | Sets a beauty filter. |

### Settings APIs

| API                                             | Description                                                         |
|-----|-----|
| [SetVideoQosPreference](#setvideoqospreference) | Sets network bandwidth limit parameters. |

### SDK version acquisition APIs

| API                                             | Description                                                         |
|-----|-----|
| [GetSDKVersion](#getsdkversion) | Gets the SDK version. |

## `TUIRoomCoreCallback` API Overview[](id:TUIRoomCoreCallback)

### Callbacks for error events

| API                                             | Description                                                         |
|-----|-----|
| [OnError](#onerror) | Callback for error. |

### Basic event callbacks

| API                                         | Description               |
|-----|-----|
| [OnLogin](#onlogin)                         | Login.         |
| [OnLogout](#onlogout)                       | Logout.         |
| [OnCreateRoom](#oncreateroom)               | Room creation.     |
| [OnDestroyRoom](#ondestroyroom)             | Room dismissal.     |
| [OnEnterRoom](#onenterroom)                 | Room entry.     |
| [OnExitRoom](#onexitroom)                   | Room exit.     |
| [OnFirstVideoFrame](#onfirstvideoframe)     | The first video frame.     |
| [OnUserVoiceVolume](#onuservoicevolume)     | Volume level. |
| [OnRoomMasterChanged](#onroommasterchanged) | Anchor change.   |

### Remote user event callbacks

| API                                                          | Description                            |
|-----|-----|
| [OnRemoteUserEnter](#onremoteuserenter)                      | A remote user entered the room.           |
| [OnRemoteUserLeave](#onremoteuserleave)                      | A remote user exited the room.            |
| [OnRemoteUserCameraAvailable](#onremoteusercameraavailable)  | Whether a remote user enabled the camera. |
| [OnRemoteUserScreenVideoAvailable](#onremoteuserscreenvideoavailable) | Whether a remote user enabled screen sharing.   |
| [OnRemoteUserAudioAvailable](#onremoteuseraudioavailable)    | Whether a remote user enabled sending audio.   |
| [OnRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | A remote user started speaking.           |
| [OnRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | A remote user stopped speaking.          |

### Message event callback APIs

| API                                               | Description               |
|-----|-----|
| [OnReceiveChatMessage](#onreceivechatmessage)     | A text message was received. |
| [OnReceiveCustomMessage](#onreceivecustommessage) | A custom message was received. |

### Room control event callbacks

| API                                                          | Description                               |
|-----|-----|
| [OnReceiveSpeechInvitation](#onreceivespeechinvitation)      | A member received a speech invitation from the anchor.       |
| [OnReceiveInvitationCancelled](#onreceiveinvitationcancelled) | A member received a speech invitation cancellation from the anchor.    |
| [OnReceiveReplyToSpeechInvitation](#onreceivereplytospeechinvitation) | The anchor received the acceptance to a speech invitation by a member. |
| [OnReceiveSpeechApplication](#onreceivespeechapplication)    | The anchor received a speech application from a member.     |
| [OnSpeechApplicationCancelled](#onspeechapplicationcancelled) | A member canceled a speech application.             |
| [OnReceiveReplyToSpeechApplication](#onreceivereplytospeechapplication) | The anchor approved a speech application.           |
| [OnSpeechApplicationForbidden](#onspeechapplicationforbidden) | The anchor rejected a speech application.           |
| [OnOrderedToExitSpeechState](#onorderedtoexitspeechstate)  | A member was asked to stop speaking.         |
| [OnCallingRollStarted](#oncallingrollstarted)                | The anchor started a roll call.   |
| [OnCallingRollStopped](#oncallingrollstopped)                | The anchor stopped a roll call.   |
| [OnMemberReplyCallingRoll](#onmemberreplycallingroll)        | A member replied to roll call.   |
| [OnChatRoomMuted](#onchatroommuted)                          | The anchor muted/unmuted the room.     |
| [OnMicrophoneMuted](#onmicrophonemuted)                      | The anchor disabled the mic.         |
| [OnCameraMuted](#oncameramuted)                              | The anchor disabled the camera.         |

### Callback APIs for statistics on network quality and technical metrics

| API                                             | Description                                                         |
|-----|-----|
| [OnStatistics](#onstatistics)         | Statistics on technical metrics. |
| [OnNetworkQuality](#onnetworkquality) | Network quality.     |

### Screen sharing event callbacks

| API                                               | Description               |
|-----|-----|
| [OnScreenCaptureStarted](#onscreencapturestarted) | Screen sharing started. |
| [OnScreenCaptureStopped](#onscreencapturestopped) | Screen sharing stopped. |

### Video recording callbacks

| API                                               | Description               |
|-----|-----|
| [OnRecordError](#onrecorderror)       | Recording error. |
| [OnRecordComplete](#onrecordcomplete) | Recording completion. |
| [OnRecordProgress](#onrecordprogress) | Recording progress. |


### Local device test callbacks

| API                                                          | Description                  |
|-----|-----|
| [OnTestSpeakerVolume](#ontestspeakervolume)                  | Speaker volume level.       |
| [OnTestMicrophoneVolume](#ontestmicrophonevolume)            | Mic volume level.       |
| [OnAudioDeviceCaptureVolumeChanged](#onaudiodevicecapturevolumechanged) | System capturing volume level adjustment. |
| [OnAudioDevicePlayoutVolumeChanged](#onaudiodeviceplayoutvolumechanged) | System playback volume level adjustment. |

## Basic Functions of `TUIRoomCore`

### GetInstance

This API is used to get a [TUIRoomCore](https://cloud.tencent.com/document/product/647/63494) singleton object.
```C++
 static TUIRoomCore* GetInstance();
```

### DestroyInstance

```C++
static void DestroyInstance();
```

### SetCallback

This API is used to set the event callback of [TUIRoomCore](https://cloud.tencent.com/document/product/647/63494). You can use `TUIRoomCoreCallback` to get different status notifications of [TUIRoomCore](https://cloud.tencent.com/document/product/647/63494).

```C++
virtual void SetCallback(const TUIRoomCoreCallback* callback) = 0;
```

### Login

This API is used to log in to the Tencent backend server.
```C++
virtual int Login(int sdk_appid, const std::string& user_id, const std::string& user_sig) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| sdk_appid | int |  You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| user_id | string | ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system. |
| user_sig | string | Tencent Cloud's proprietary security signature. For more information on how to get it, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

### Logout

This API is used to log out of the Tencent backend server.
```C++
virtual int Logout() = 0;
```

### CreateRoom

This API is used to create a room (called by the anchor).
```C++
virtual int CreateRoom(const std::string& room_id, TUISpeechMode speech_mode) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| room_id | string | Room ID. You need to assign and manage the IDs in a centralized manner. |
| speech_mode | TUISpeechMode | Speech mode. |

Generally, the chairperson calls the APIs in the following steps:
1. The **anchor** calls `CreateRoom()` to create a room, the result of which is returned via `OnCreateRoom`.
2. The **anchor** calls `EnterRoom()` to enter the room.
3. The **anchor** calls `StartCameraPreview()` to enable camera capturing and preview.
4. The **anchor** calls `StartLocalAudio()` to enable the local mic.

### DestroyRoom

This API is used to terminate a room (called by the anchor).
```C++
virtual int DestroyRoom() = 0;
```

### EnterRoom

This API is used to enter a room (called by a member).
```C++
virtual int EnterRoom(const std::string& room_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| room_id | string | Room ID. |

Generally, a member enters a room in the following steps:
1. The **member** calls `EnterRoom` and passes in `room_id` to enter the room.
2. The **member** calls `startCameraPreview()` to enable camera preview and calls `StartLocalAudio()` to enable mic capturing.
3. The **member** receives the `OnRemoteUserCameraAvailable` event and calls `StartRemoteView()` to start playback.

### LeaveRoom

This API is used to exit a room (called by a member).
```C++
virtual int LeaveRoom() = 0;
```

### GetRoomInfo

This API is used to get the room information.
```C++
virtual TUIRoomInfo GetRoomInfo() = 0;
```

### GetRoomUsers

This API is used to get the information of all users in the room.
```C++
virtual std::vector<TUIUserInfo> GetRoomUsers() = 0;
```

### GetUserInfo

This API is used to get the information of a user in the room.
```C++
virtual const TUIUserInfo* GetUserInfo(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### SetSelfProfile

This API is used to set the user attributes.
```C++
virtual int SetSelfProfile(const std::string& user_name, const std::string& avatar_url) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_name | string | User name. |
| avatar_url | string | User profile photo URL. |

### TransferRoomMaster

This API is used to transfer a group to another user.
```C++
virtual int TransferRoomMaster(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

## Local Push APIs

### StartCameraPreview

This API is used to start the preview of the local camera.
```C++
virtual int StartCameraPreview(const liteav::TXView& view) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | liteav::TXView | Window handle. |

### StopCameraPreview

This API is used to stop the preview of the local camera.
```C++
virtual int StopCameraPreview() = 0;
```

### UpdateCameraPreview

This API is used to update the preview image of the local video.
```C++
virtual int UpdateCameraPreview(const liteav::TXView& view) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | liteav::TXView | Window handle. |

### StartLocalAudio

This API is used to enable the local audio device.
```C++
virtual int StartLocalAudio(const liteav::TRTCAudioQuality& quality) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| view | liteav::TXView | Window handle. |

### StopLocalAudio

This API is used to disable the local audio device.
```C++
virtual int StopLocalAudio() = 0;
```

### StartSystemAudioLoopback

This API is used to enable system audio capturing.
```C++
virtual int StartSystemAudioLoopback() = 0;
```

### StopSystemAudioLoopback

This API is used to disable system audio capturing.
```C++
virtual int StopSystemAudioLoopback() = 0;
```

### SetVideoMirror

This API is used to set mirroring mode.
```C++
virtual int SetVideoMirror(bool mirror) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mirror | bool | Whether to enable the mirroring mode. |

## Remote User APIs

### StartRemoteView
This API is used to subscribe to a remote user's video stream.

```C++
virtual int StartRemoteView(const std::string& user_id, const liteav::TXView& view,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | ID of the user whose video image is to be played back. |
| liteav::TXView | TXView | `view` control that carries the video image. |
| type | TUIStreamType | Stream type. |

### StopRemoteView

This API is used to unsubscribe from and stop the playback of a remote video image.
```C++
virtual int StopRemoteView(const std::string& user_id,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | ID of the user whose video image is to be stopped. |
| type | TUIStreamType | Stream type. |

### UpdateRemoteView

This API is used to updates the rendering window of a remote video.
```C++
virtual int UpdateRemoteView(const std::string& user_id, TUIStreamType type, liteav::TXView& view) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| type | TUIStreamType | Stream type. |
| view | liteav::TXView | Rendering window handle. |

## Message Sending APIs

### SendChatMessage

This API is used to send text messages.
```C++
virtual int SendChatMessage(const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| message | string | Message content. |

### SendCustomMessage

Sending Custom Messages
```C++
virtual int SendCustomMessage(const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| message | string | Message content. |

## Room Control APIs

### MuteUserMicrophone

This API is used to enable/disable the mic of the specified user.
```C++
virtual int MuteUserMicrophone(const std::string& user_id, bool mute, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| mute | bool | Whether to disable. |
| callback | Callback | API callback. |

### MuteAllUsersMicrophone

This API is used to enable/disable the mic of all users.
```C++
virtual int MuteAllUsersMicrophone(bool mute) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mute | bool | Whether to disable. |

### MuteUserCamera

This API is used to enable/disable the camera of the specified user.
```C++
virtual int MuteUserCamera(const std::string& user_id, bool mute, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| mute | bool | Whether to disable. |
| callback | Callback | API callback. |

### MuteAllUsersCamera

This API is used to enable/disable the camera of all users.
```C++
virtual int MuteAllUsersCamera(bool mute) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mute | bool | Whether to disable. |

### MuteChatRoom

This API is used to mute/unmute the chat room.
```C++
virtual int MuteChatRoom(bool mute) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| mute | bool | Whether to disable. |

### KickOffUser

This API is used by the anchor to remove a member.
```C++
virtual int KickOffUser(const std::string& user_id, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| callback | Callback | API callback. |

### StartCallingRoll

This API is used by the anchor to start roll call.
```C++
virtual int StartCallingRoll() = 0;
```

### StopCallingRoll

This API is used by the anchor to stop roll call.
```C++
virtual int StopCallingRoll() = 0;
```

### ReplyCallingRoll

This API is used by a member to reply to roll call.
```C++
virtual int ReplyCallingRoll(Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| callback | Callback | API callback. |

### SendSpeechInvitation

This API is used by the anchor to invite a member to speak.
```C++
virtual int SendSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| callback | Callback | API callback. |

### CancelSpeechInvitation

This API is used by the anchor to cancel the speech invitation to a member.
```C++
virtual int CancelSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| callback | Callback | API callback. |

### ReplySpeechInvitation

This API is used by a member to accept/reject the speech invitation from the anchor.
```C++
virtual int ReplySpeechInvitation(bool agree, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| agree | bool | Whether to approve. |
| callback | Callback | API callback. |

### SendSpeechApplication

This API is used by a member to apply to speak.
```C++
virtual int SendSpeechApplication(Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| callback | Callback | API callback. |

### CancelSpeechApplication

This API is used by a member to cancel the speech application.
```C++
virtual int CancelSpeechApplication(Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| callback | Callback | API callback. |

### ReplySpeechApplication

This API is used by the anchor to approve/reject the speech application of a member.
```C++
virtual int ReplySpeechApplication(const std::string& user_id, bool agree, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| callback | Callback | API callback. |

### ForbidSpeechApplication

This API is used by the anchor to forbid speech application.
```C++
virtual int ForbidSpeechApplication(bool forbid) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| forbid | bool | Whether to forbid. |

### SendOffSpeaker

This API is used by the anchor to stop the speech of the specified member.
```C++
virtual int SendOffSpeaker(const std::string& user_id, Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| callback | Callback | API callback. |

### SendOffAllSpeakers

This API is used by the anchor to stop the speech of all members.
```C++
virtual int SendOffAllSpeakers(Callback callback) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| callback | Callback | API callback. |

### ExitSpeechState

This API is used for a member to stop speaking and change their role to audience.
```C++
virtual int ExitSpeechState() = 0;
```

## Basic Component APIs

### GetDeviceManager

This API is used to get the device management object pointer.
```C++
virtual liteav::ITXDeviceManager* GetDeviceManager() = 0;
```

### GetScreenShareManager

This API is used to get the screen sharing management object pointer.
```C++
virtual IScreenShareManager* GetScreenShareManager() = 0;
```

## On-Cloud Recording APIs

### StartCloudRecord

This API is used to start on-cloud recording.
```C++
virtual int StartCloudRecord() = 0;
```

### StopCloudRecord

This API is used to stop on-cloud recording.
```C++
virtual int StopCloudRecord() = 0;
```

## Beauty Filter APIs

### SetBeautyStyle

This API is used to set effect levels of beauty, brightening, and rosy skin filters.
```C++
virtual int SetBeautyStyle(liteav::TRTCBeautyStyle style, uint32_t beauty_level,
        uint32_t whiteness_level, uint32_t ruddiness_level) = 0;
```

You can do the following using `TXBeautyManager`:
- Set the beauty filter style to smooth or natural. The smooth style features more obvious skin smoothing effect.
- Set the strength of the beauty filter. Value range: 0-9. `0` indicates that the filter is disabled. The larger the value, the more obvious the effect.
- Set the strength of the skin brightening filter. Value range: 0-9. `0` indicates that the filter is disabled. The larger the value, the more obvious the effect.

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| style | liteav::TRTCBeautyStyle | Beauty filter style. |
| beauty_level | uint32_t | strength of the beauty filter. |
| whiteness_level | uint32_t | Strength of the skin brightening filter. |
| ruddiness_level | uint32_t | Strength of the rosy skin filter. |

## Settings APIs

### SetVideoQosPreference

set QoS parameters
```C++
virtual int SetVideoQosPreference(TUIVideoQosPreference preference) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| preference | TUIVideoQosPreference | Network bandwidth limit policy. |

## SDK Version Acquisition APIs

### GetSDKVersion

This API is used to get SDK version information.
```C++
virtual const char* GetSDKVersion() = 0;
```

## Error Event Callbacks
### OnError

```C++
void OnError(int code, const std::string& message);
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code    | int    | Error code   |
| message | string | Error message. |

## Basic Event Callbacks
### OnLogin

```C++
virtual void OnLogin(int code, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code    | int    | Error code   |
| message | string | Login message or error message of login failure. |

### OnLogout

```C++
virtual void OnLogout(int code, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code    | int    | Error code   |
| message | string | Error message. |

### OnCreateRoom

Room creation.
```C++
virtual void OnCreateRoom(int code, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code    | int    | Error code   |
| message | string | Error message. |

### OnDestroyRoom

Room dismissal.
```C++
virtual void OnDestroyRoom(int code, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code    | int    | Error code   |
| message | string | Error message. |

### OnEnterRoom

Room entry.
```C++
virtual void OnEnterRoom(int code, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| code    | int    | Error code   |
| message | string | Error message. |

### OnExitRoom

Room exit.
```C++
virtual void OnExitRoom(TUIExitRoomType type, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| type | TUIExitRoomType | Room exit type. |
| message | string | Error message. |

### OnFirstVideoFrame

Rendering the first frame of the local video or a remote user started.
```C++
virtual void OnFirstVideoFrame(const std::string& user_id, const TUIStreamType stream_type) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| stream_type | TUIStreamType | Stream type. |

### OnUserVoiceVolume

User volume level.
```C++
virtual void OnUserVoiceVolume(const std::string& user_id, int volume)
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| volume | int | User volume level. Value range: 0–100. |

### OnRoomMasterChanged

Anchor change.
```C++
virtual void OnRoomMasterChanged(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

## Remote User Callbacks

### OnRemoteUserEnter

A remote user entered the room.
```C++
virtual void OnRemoteUserEnter(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### OnRemoteUserLeave

A remote user exited the room.
```C++
virtual void OnRemoteUserLeave(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### OnRemoteUserCameraAvailable

Whether a remote user enabled the camera.
```C++
virtual void OnRemoteUserCameraAvailable(const std::string& user_id, bool available) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| available | bool | true: enabled; false: disabled. |

### OnRemoteUserScreenVideoAvailable

Whether a remote user enabled the camera.
```C++
virtual void OnRemoteUserScreenVideoAvailable(const std::string& user_id, bool available) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| available | bool | true: enabled; false: disabled. |

### OnRemoteUserAudioAvailable

Whether a remote user enabled the camera.
```C++
virtual void OnRemoteUserAudioAvailable(const std::string& user_id, bool available) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| available | bool | true: enabled; false: disabled. |

### OnRemoteUserEnterSpeechState

A remote user started speaking.
```C++
virtual void OnRemoteUserEnterSpeechState(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### OnRemoteUserExitSpeechState

A remote user stopped speaking.
```C++
virtual void OnRemoteUserExitSpeechState(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |


## Chat Room Message Event Callbacks

### OnReceiveChatMessage

A text message was received.
```C++
virtual void OnReceiveChatMessage(const std::string& user_id, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| message | string | Text message. |

### OnReceiveCustomMessage

A custom message was received.
```C++
virtual void OnReceiveCustomMessage(const std::string& user_id, const std::string& message) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| message | string | Custom message. |

## Room Control Message Callbacks

### OnReceiveSpeechInvitation

A user received a speech invitation from the anchor.
```C++
virtual void OnReceiveSpeechInvitation() = 0;
```

### OnReceiveInvitationCancelled

A user received a speech invitation cancellation from the anchor.
```C++
virtual void OnReceiveInvitationCancelled() = 0;
```

### OnReceiveReplyToSpeechInvitation

The anchor received the acceptance to a speech invitation by a member.
```C++
virtual void OnReceiveReplyToSpeechInvitation(const std::string& user_id, bool agree) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |
| agree | bool | Whether the invitation was accepted. |

### OnReceiveSpeechApplication

The anchor received a speech application from a member.
```C++
virtual void OnReceiveSpeechApplication(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### OnSpeechApplicationCancelled

A user canceled a speech application.
```C++
virtual void OnSpeechApplicationCancelled(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### OnReceiveReplyToSpeechApplication

The anchor approved a speech application.
```C++
virtual void OnReceiveReplyToSpeechApplication(bool agree) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| agree | bool | Whether to approve. |

### OnSpeechApplicationForbidden

The anchor forbidden a speech application.
```C++
virtual void OnSpeechApplicationForbidden(bool forbidden) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| forbidden | bool | Whether to forbid. |

### OnOrderedToExitSpeechState

A member was asked to stop speaking.
```C++
virtual void OnOrderedToExitSpeechState() = 0;
```

### OnCallingRollStarted

The anchor started a roll call.
```C++
virtual void OnCallingRollStarted() = 0;
```

### OnCallingRollStopped

The anchor stopped a roll call.
```C++
virtual void OnCallingRollStopped() = 0;
```

### OnMemberReplyCallingRoll

A member replied to roll call.
```C++
virtual void OnMemberReplyCallingRoll(const std::string& user_id) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| user_id | string | User ID. |

### OnChatRoomMuted

The anchor muted/unmuted the room.
```C++
virtual void OnChatRoomMuted(bool muted) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| muted | bool | Whether to disable. |

### OnMicrophoneMuted

The anchor disabled the mic.
```C++
virtual void OnMicrophoneMuted(bool muted) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| muted | bool | Whether to disable. |

### OnCameraMuted

The anchor disabled the camera.
```C++
virtual void OnCameraMuted(bool muted) = 0;
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| muted | bool | Whether to disable. |

## Statistics Collection and Quality Callbacks

### OnStatistics

Callback of technical metric statistics.
```C++
virtual void OnStatistics(const liteav::TRTCStatistics& statis) {}
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| statis | liteav::TRTCStatistics | Statistics. |

### OnNetworkQuality

Network quality.
```C++
virtual void OnNetworkQuality(const liteav::TRTCQualityInfo& local_quality, liteav::TRTCQualityInfo* remote_quality,
        uint32_t remote_quality_count) {}
```

The parameters are as detailed below:

| Parameter        | Type    | Description                                                                                                      |
|-----|-----|-----|
| local_quality | liteav::TRTCQualityInfo | Local user quality information. |
| remote_quality | liteav::TRTCQualityInfo* | Pointer to the remote user quality information. |
| remote_quality_count | uint32_t | Number of remote users. |

## Screen Sharing Event Callbacks

### OnScreenCaptureStarted

Screen sharing started.

```C++
virtual void OnScreenCaptureStarted() {}
```

### OnScreenCaptureStopped

Screen sharing stopped.

```C++
void OnScreenCaptureStopped(int reason) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | Reason for stop. 0: the user stopped proactively; 1: stopped due to preemption by another application. |

## Video Recording Callbacks

### OnRecordError

Recording error.

```C++
virtual void OnRecordError(TXLiteAVLocalRecordError error, const std::string& messgae) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| error | TXLiteAVLocalRecordError  | Error message. |
| messgae | string  | Error description. |

### OnRecordComplete

Recording completion.

```C++
virtual void OnRecordComplete(const std::string& path) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| path | string  | Error description. |

### OnRecordProgress

Recording progress.

```C++
virtual void OnRecordProgress(int duration, int file_size) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| duration | int  | File duration. |
| file_size | int  | File size. |

## Local Device Test Callbacks

### OnTestSpeakerVolume

Speaker volume level.

```C++
virtual void OnTestSpeakerVolume(uint32_t volume) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | Volume level. |

### OnTestMicrophoneVolume

Mic volume level.

```C++
virtual void OnTestMicrophoneVolume(uint32_t volume) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | Volume level. |

### OnAudioDeviceCaptureVolumeChanged

System capturing volume level adjustment.

```C++
virtual void OnAudioDeviceCaptureVolumeChanged(uint32_t volume, bool muted) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | Volume level. |
| muted | bool  | Whether to disable. |

### OnAudioDevicePlayoutVolumeChanged

System playback volume level adjustment.

```C++
virtual void OnAudioDevicePlayoutVolumeChanged(uint32_t volume, bool muted) {}
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | Volume level. |
| muted | bool  | Whether to disable. |
