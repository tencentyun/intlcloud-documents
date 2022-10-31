TUIRoom is based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM). Its features include:
- The host can create a room, and participants can enter the room ID to join the room.
- The participants can share their screens with each other.
- All members can send text chat messages and custom messages.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports up to 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

TUIRoom is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, see [Integrating TUIRoom (Windows and macOS)](https://intl.cloud.tencent.com/document/product/647/44071).
- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as a low-latency video conference component.
- IM SDK: The [IM SDK](https://intl.cloud.tencent.com/document/product/1047) (**C++ edition**) is used to implement chat messages.


## TUIRoom API Overview[](id:TUIRoom)

### TUIRoomCore basic APIs

| API                                     | Description                                  |
|-----|-----|
| [GetInstance](#getinstance)         | Gets a singleton object. |
| [DestroyInstance](#destroyinstance) | Terminates a singleton object. |
| [SetCallback](#setcallback)         | Sets event callbacks. |

### Room APIs

| API | Description |
|-----|-----|
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [CreateRoom](#createroom)                 | Creates a room (called by host).           |
| [DestroyRoom](#destroyroom)               | Closes the room (called by host).           |
| [EnterRoom](#enterroom) | Enters a room (called by participant). |
| [LeaveRoom](#leaveroom)             | Leaves a room (called by participant).           |
| [GetRoomInfo](#getroominfo)               | Gets the room information.                     |
| [GetRoomUsers](#getroomusers)             | Gets the information of all members in the room.           |
| [GetUserInfo](#getuserinfo)               | Gets the information of a user.               |
| [TransferRoomMaster](#transferroommaster) | Transfers the host permissions (called by host).     |

### Local audio/video operation APIs

| API | Description |
|-----|-----|
| [StartCameraPreview](#startcamerapreview) | Enables preview of the local video.   |
| [StopCameraPreview](#stopcamerapreview) | Stops local video capturing and preview.|
| [UpdateCameraPreview](#updatecamerapreview)           | Updates the local video rendering window.     |
| [StartLocalAudio](#startlocalaudio)                   | Enables mic capturing.           |
| [StopLocalAudio](#stoplocalaudio)                     | Stops mic capturing.           |
| [StartSystemAudioLoopback](#startsystemaudioloopback) | Enables system audio capturing.  |
| [StopSystemAudioLoopback](#stopsystemaudioloopback)   | Disables system audio capturing.  |
| [SetVideoMirror](#setvideomirror)                     | Sets the mirror mode for local video preview. |

### Remote user APIs

| API | Description |
|-----|-----|
| [StartRemoteView](#startremoteview) | Subscribes to and plays back the remote video image of a specified member. |
| [StopRemoteView](#stopremoteview)   | Unsubscribes from and stops the playback of a remote video image.   |
| [UpdateRemoteView](#updateremoteview) | Updates the video rendering window of a remote user.      |

### Chat message sending APIs

| API | Description |
|-----|-----|
| [SendChatMessage](#sendchatmessage)     | Sends a chat message.   |
| [SendCustomMessage](#sendcustommessage) | Sends a custom message. |

### Room control APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
|-----|-----|
| [MuteUserMicrophone](#muteusermicrophone)           | Enables/Disables the mic of a specified user.                               |
| [MuteAllUsersMicrophone](#muteallusersmicrophone)   | Enables/Disables the mics of all users and syncs the status to room information. |
| [MuteUserCamera](#muteusercamera)                   | Enables/Disables the camera of a specified user.                               |
| [MuteAllUsersCamera](#mutealluserscamera)           | Enables/Disables the cameras of all users and syncs the status to room information. |
| [MuteChatRoom](#mutechatroom)                       | Enables/Disables chat messages (called by host).                     |
| [KickOffUser](#kickoffuser)                         | Removes a specified user from the room (called by host).                        |
| [StartCallingRoll](#startcallingroll)               | Starts a roll call (called by host).                                        |
| [StopCallingRoll](#stopcallingroll)                 | Stops a roll call (called by host).                                        |
| [ReplyCallingRoll](#replycallingroll)               | Replies to a roll call (called by participant).                                    |
| [SendSpeechInvitation](#sendspeechinvitation)       | Sends a speech invitation to a participant (called by host).                                    |
| [CancelSpeechInvitation](#cancelspeechinvitation)   | Cancels a speech invitation sent to a participant (called by host).                                 |
| [ReplySpeechInvitation](#replyspeechinvitation)     | Accepts/Rejects the speech invitation of the host (called by participant).                         |
| [SendSpeechApplication](#sendspeechapplication)     | Sends a speech request (called by participant).                                         |
| [CancelSpeechApplication](#cancelspeechapplication) | Cancels a speech request (called by participant).                                      |
| [ReplySpeechApplication](#replyspeechapplication)   | Approves/Rejects the speech request of a participant (called by host).                         |
| [ForbidSpeechApplication](#forbidspeechapplication) | Disables requests to speak (called by host).                                    |
| [SendOffSpeaker](#sendoffspeaker)                   | Stops the speech of a participant (called by host).                                |
| [SendOffAllSpeakers](#sendoffallspeakers)           | Stops the speech of all members (called by host).                                  |
| [ExitSpeechState](#exitspeechstate)                 | Exits the speaker mode (called by participant).                               |

### Basic component APIs

| API                                                 | Description                                                                                                                   |
|-----|-----|
| [GetDeviceManager](#getdevicemanager)           | Gets the local device management object `ITXDeviceManager`.    |
| [GetScreenShareManager](#getscreensharemanager) | Gets the screen sharing management object `IScreenShareManager`. |

### On-cloud recording APIs

| API                                     | Description                                  |
|-----|-----|
| [StartCloudRecord](#startcloudrecord) | Starts on-cloud recording. |
| [StopCloudRecord](#stopcloudrecord)   | Stops on-cloud recording. |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [SetBeautyStyle](#setbeautystyle) | Sets beauty filters. |

### Settings APIs

| API | Description |
|-----|-----|
| [SetVideoQosPreference](#setvideoqospreference) | Sets network QoS control parameters. |

### SDK version APIs

| API | Description |
|-----|-----|
| [GetSDKVersion](#getsdkversion) | Gets the SDK version. |

## `TUIRoomCoreCallback` API Overview[](id:TUIRoomCoreCallback)

### Callbacks for error events

| API | Description |
|-----|-----|
| [OnError](#onerror) | Callback for error.|

### Basic event callbacks

| API | Description |
|-----|-----|
| [OnLogin](#onlogin)                         | The local user logged in.         |
| [OnLogout](#onlogout)                       | The local user logged out.         |
| [OnCreateRoom](#oncreateroom)               | The room was created.     |
| [OnDestroyRoom](#ondestroyroom)             | The room was closed.     |
| [OnEnterRoom](#onenterroom)                   | The local user entered the room.   |
| [OnExitRoom](#onexitroom)                   | The local user left the room.     |
| [OnFirstVideoFrame](#onfirstvideoframe)     | Started rendering the first video frame.     |
| [onUserVoiceVolume](#onuservoicevolume)     | The audio volume of a user. |
| [OnRoomMasterChanged](#onroommasterchanged) | The host changed.   |

### Remote user event callbacks

| API                                                          | Description                            |
|-----|-----|
| [OnRemoteUserEnter](#onremoteuserenter)                      | A remote user entered the room.           |
| [OnRemoteUserLeave](#onremoteuserleave)                      | A remote user exited the room.            |
| [OnRemoteUserCameraAvailable](#onremoteusercameraavailable)  | A remote user enabled/disabled their camera. |
| [OnRemoteUserScreenAvailable](#onremoteuserscreenavailable) | A remote user started/stopped screen sharing.   |
| [OnRemoteUserAudioAvailable](#onremoteuseraudioavailable)    |  A remote user turned on/off their mic.   |
| [OnRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | A remote user started speaking.           |
| [OnRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | A remote user stopped speaking.          |

### Message event callbacks

| API | Description |
|-----|-----|
| [OnReceiveChatMessage](#onreceivechatmessage)     | A text chat message was received. |
| [OnReceiveCustomMessage](#onreceivecustommessage) | A custom message was received. |

### Room control event callbacks

| API                                                          | Description                               |
|-----|-----|
| [OnReceiveSpeechInvitation](#onreceivespeechinvitation)      | A participant received a speech invitation from the host.       |
| [OnReceiveInvitationCancelled](#onreceiveinvitationcancelled) | The speech invitation sent to a participant was canceled by the host.    |
| [OnReceiveReplyToSpeechInvitation](#onreceivereplytospeechinvitation) | A participant accepted the speech invitation sent by the host. |
| [OnReceiveSpeechApplication](#onreceivespeechapplication)    | The host received a speech request from a participant.     |
| [OnSpeechApplicationCancelled](#onspeechapplicationcancelled) | A participant canceled a speech request.             |
| [OnReceiveReplyToSpeechApplication](#onreceivereplytospeechapplication) | The host approved a request to speak.           |
| [OnSpeechApplicationForbidden](#onspeechapplicationforbidden) | The host disabled requests to speak.           |
| [OnOrderedToExitSpeechState](#onorderedtoexitspeechstate)  | A participant was asked to stop speaking.         |
| [OnCallingRollStarted](#oncallingrollstarted)                | The host started a roll call (received by participants)   |
| [OnCallingRollStopped](#oncallingrollstopped)                | The host stopped a roll call (received by participants).   |
| [OnMemberReplyCallingRoll](#onmemberreplycallingroll)        | A participant replied to the roll call (received by the host).   |
| [OnChatRoomMuted](#onchatroommuted)                          | The host disabled/enabled chat messages.     |
| [OnMicrophoneMuted](#onmicrophonemuted)                      | The host disabled mic use.         |
| [OnCameraMuted](#oncameramuted)                              | The host disabled camera use.         |

### Callbacks for statistics on network quality and technical metrics

| API | Description |
|-----|-----|
| [OnStatistics](#onstatistics)         | Statistics on technical metrics. |
| [OnNetworkQuality](#onnetworkquality) | Network quality.     |

### Screen sharing event callbacks

| API | Description |
|-----|-----|
| [OnScreenCaptureStarted](#onscreencapturestarted) | Screen sharing started. |
| [OnScreenCaptureStopped](#onscreencapturestopped) | Screen sharing stopped. |

### Video recording callbacks

| API                                     | Description                                  |
|-----|-----|
| [OnRecordError](#onrecorderror)       | Recording error. |
| [OnRecordComplete](#onrecordcomplete) | Recording completed. |
| [OnRecordProgress](#onrecordprogress) | The recording progress. |


### Local device test callbacks

| API                                                          | Description                  |
|-----|-----|
| [OnTestSpeakerVolume](#ontestspeakervolume)                  | The speaker volume.       |
| [OnTestMicrophoneVolume](#ontestmicrophonevolume)            | The mic volume.       |
| [OnAudioDeviceCaptureVolumeChanged](#onaudiodevicecapturevolumechanged) | The system capturing volume changed. |
| [OnAudioDevicePlayoutVolumeChanged](#onaudiodeviceplayoutvolumechanged) | The system audio playback volume changed. |

## TUIRoomCore Basic APIs

### GetInstance

This API is used to get a [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/44071) singleton object.
```C++
 static TUIRoomCore* GetInstance();
```

### DestroyInstance

```C++
static void DestroyInstance();
```

### SetCallback

This API is used to set the event callbacks of [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/44071). You can use `TRTCChorusRoomDelegate` to get the callbacks.

```C++
virtual void SetCallback(const TUIRoomCoreCallback* callback) = 0;
```

### Login

Login
```C++
virtual int Login(int sdk_appid, const std::string& user_id, const std::string& user_sig) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdk_appid | int | You can view `SDKAppID` in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** of the TRTC console. |
| user_id | string | The ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your own account system. |
| user_sig | string | Tencent Cloud's proprietary security signature. For how to calculate and use it, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

### Logout

Log out
```C++
virtual int Logout() = 0;
```

### CreateRoom

This API is used to create a room (called by the host).
```C++
virtual int CreateRoom(const std::string& room_id, TUISpeechMode speech_mode) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| room_id | string | The room ID. You need to assign and manage the IDs in a centralized manner. |
| speech_mode | TUISpeechMode | The speech mode. |

Generally, a host may need to call the following APIs:
1. The **host** calls `CreateRoom()` to create a room, the result of which is returned via `OnCreateRoom`.
2. The **host** calls `EnterRoom()` to enter the room.
3. The **host** calls `StartCameraPreview()` to enable camera capturing and preview.
4. The **host** calls `StartLocalAudio()` to enable the local mic.

### DestroyRoom

This API is used to close a room (called by the host).
```C++
virtual int DestroyRoom() = 0;
```

### EnterRoom

This API is used to enter a room (called by a participant).
```C++
virtual int EnterRoom(const std::string& room_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| room_id | string | The room ID. |

Generally, a participant joins a meeting in the following steps:
1. The **participant** calls `EnterRoom` (passing in `room_id`) to enter the room.
2. The **participant** calls `startCameraPreview()` to enable camera preview and calls `StartLocalAudio()` to enable mic capturing.
3. The **participant** receives the `OnRemoteUserCameraAvailable` callback and calls `StartRemoteView()` to start playback.

### LeaveRoom

This API is used to leave a room (called by a participant).
```C++
virtual int LeaveRoom() = 0;
```

### GetRoomInfo

This API is used to get the room information.
```C++
virtual TUIRoomInfo GetRoomInfo() = 0;
```

### GetRoomUsers

This API is used to get the information of all members in the room.
```C++
virtual std::vector<TUIUserInfo> GetRoomUsers() = 0;
```

### GetUserInfo

This API is used to get the information of a specified member.
```C++
virtual const TUIUserInfo* GetUserInfo(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### SetSelfProfile

This API is used to set the user profile.
```C++
virtual int SetSelfProfile(const std::string& user_name, const std::string& avatar_url) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_name | string | The username. |
| avatar_url | string | The URL of the user profile photo. |

### TransferRoomMaster

This API is used to transfer host permissions to another user.
```C++
virtual int TransferRoomMaster(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

## Local Push APIs

### StartCameraPreview

This API is used to start the preview of the local camera.
```C++
virtual int StartCameraPreview(const liteav::TXView& view) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| view | liteav::TXView | The window handle. |

### StopCameraPreview

This API is used to stop the preview of the local camera.
```C++
virtual int StopCameraPreview() = 0;
```

### UpdateCameraPreview

This API is used to update the local preview window.
```C++
virtual int UpdateCameraPreview(const liteav::TXView& view) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| view | liteav::TXView | The window handle. |

### StartLocalAudio

This API is used to enable the local audio device.
```C++
virtual int StartLocalAudio(const liteav::TRTCAudioQuality& quality) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| view | liteav::TXView | The window handle. |

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

This API is used to set the mirror mode.
```C++
virtual int SetVideoMirror(bool mirror) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | bool | Whether to mirror the video. |

## Remote User APIs

### StartRemoteView
This API is used to subscribe to a remote user's video stream.

```C++
virtual int StartRemoteView(const std::string& user_id, const liteav::TXView& view,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The ID of the user whose video image is to be played back. |
| liteav::TXView | TXView | The view that loads the video. |
| type | TUIStreamType | The stream type. |

### StopRemoteView

This API is used to unsubscribe from and stop the playback of a remote video image.
```C++
virtual int StopRemoteView(const std::string& user_id,
        TUIStreamType type = TUIStreamType::kStreamTypeCamera) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The ID of the user whose video image is to be stopped. |
| type | TUIStreamType | The stream type. |

### UpdateRemoteView

This API is used to update the rendering window of a remote video.
```C++
virtual int UpdateRemoteView(const std::string& user_id, TUIStreamType type, liteav::TXView& view) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| type | TUIStreamType | The stream type. |
| view | liteav::TXView | The rendering window handle. |

## Message Sending APIs

### SendChatMessage

This API is used to send a text message.
```C++
virtual int SendChatMessage(const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | string | The message content. |

### SendCustomMessage

This API is used to send a custom message.
```C++
virtual int SendCustomMessage(const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | string | The message content. |

## Room Control APIs

### MuteUserMicrophone

This API is used to enable/disable the mic of the specified user.
```C++
virtual int MuteUserMicrophone(const std::string& user_id, bool mute, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| mute | bool | Whether to disable. |
| callback | Callback | API callback. |

### MuteAllUsersMicrophone

This API is used to enable/disable the mics of all users.
```C++
virtual int MuteAllUsersMicrophone(bool mute) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | Whether to disable. |

### MuteUserCamera

This API is used to enable/disable the camera of the specified user.
```C++
virtual int MuteUserCamera(const std::string& user_id, bool mute, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| mute | bool | Whether to disable. |
| callback | Callback | API callback. |

### MuteAllUsersCamera

This API is used to enable/disable the cameras of all users.
```C++
virtual int MuteAllUsersCamera(bool mute) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | Whether to disable. |

### MuteChatRoom

This API is used to disable/enable chat messages.
```C++
virtual int MuteChatRoom(bool mute) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | Whether to disable. |

### KickOffUser

This API is used by the host to remove a member from the room.
```C++
virtual int KickOffUser(const std::string& user_id, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| callback | Callback | API callback. |

### StartCallingRoll

This API is used by the host to start a roll call.
```C++
virtual int StartCallingRoll() = 0;
```

### StopCallingRoll

This API is used by the host to stop a roll call.
```C++
virtual int StopCallingRoll() = 0;
```

### ReplyCallingRoll

This API is used by a participant to reply to a roll call.
```C++
virtual int ReplyCallingRoll(Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | Callback | API callback. |

### SendSpeechInvitation

This API is used by the host to invite a participant to speak.
```C++
virtual int SendSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| callback | Callback | API callback. |

### CancelSpeechInvitation

This API is used by the host to cancel a speech invitation.
```C++
virtual int CancelSpeechInvitation(const std::string& user_id, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| callback | Callback | API callback. |

### ReplySpeechInvitation

This API is used by a participant to accept/reject the host’s invitation to speak.
```C++
virtual int ReplySpeechInvitation(bool agree, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| agree | bool | Whether to approve. |
| callback | Callback | API callback. |

### SendSpeechApplication

This API is used by a participant to send a request to speak.
```C++
virtual int SendSpeechApplication(Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | Callback | API callback. |

### CancelSpeechApplication

This API is used by a participant to cancel the request to speak.
```C++
virtual int CancelSpeechApplication(Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | Callback | API callback. |

### ReplySpeechApplication

This API is used by the host to approve/reject a participant’s speech request.
```C++
virtual int ReplySpeechApplication(const std::string& user_id, bool agree, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| callback | Callback | API callback. |

### ForbidSpeechApplication

This API is used by the host to disable requests to speak.
```C++
virtual int ForbidSpeechApplication(bool forbid) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| forbid | bool | Whether to disable. |

### SendOffSpeaker

This API is used by the host to stop the speech of a participant.
```C++
virtual int SendOffSpeaker(const std::string& user_id, Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| callback | Callback | API callback. |

### SendOffAllSpeakers

This API is used by the host to stop the speech of all members.
```C++
virtual int SendOffAllSpeakers(Callback callback) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | Callback | API callback. |

### ExitSpeechState

This API is used by a participant to exit the speaker mode.
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

This API is used to set the strength of the beauty, skin brightening, and rosy skin effects
```C++
virtual int SetBeautyStyle(liteav::TRTCBeautyStyle style, uint32_t beauty_level,
        uint32_t whiteness_level, uint32_t ruddiness_level) = 0;
```

You can do the following using the beauty filter manger:
- Set the beauty style to smooth or natural. The smooth style features more obvious skin smoothing effect.
- Set the strength of the beauty effect. Value range: 0-9. 0 indicates to disable the effect. The larger the value, the more obvious the effect.
- Set the skin brightening strength. Value range: 0-9. 0 indicates to disable the effect. The larger the value, the more obvious the effect.

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| style | liteav::TRTCBeautyStyle | The beauty style. |
| beauty_level | uint32_t | The strength of the beauty effect. |
| whiteness_level | uint32_t | The strength of the skin brightening effect. |
| ruddiness_level | uint32_t | The strength of the rosy skin effect. |

## Settings APIs

### SetVideoQosPreference

This API is used to set network QoS control parameters.
```C++
virtual int SetVideoQosPreference(TUIVideoQosPreference preference) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| preference | TUIVideoQosPreference | The network QoS policy. |

## SDK Version APIs

### GetSDKVersion

This API is used to get the SDK version.
```C++
virtual const char* GetSDKVersion() = 0;
```

## Error Event Callbacks
### OnError

```C++
void OnError(int code, const std::string& message);
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| code    | int    | The error code.   |
| message | string | The error message. |

## Basic Event Callbacks
### OnLogin

```C++
virtual void OnLogin(int code, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| code    | int    | The error code.   |
| message | string | The login information or error message for login failure. |

### OnLogout

```C++
virtual void OnLogout(int code, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| code    | int    | The error code.   |
| message | string | The error message. |

### OnCreateRoom

A room was created.
```C++
virtual void OnCreateRoom(int code, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| code    | int    | The error code.   |
| message | string | The error message. |

### OnDestroyRoom

The room was closed.
```C++
virtual void OnDestroyRoom(int code, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| code    | int    | The error code.   |
| message | string | The error message. |

### OnEnterRoom

The local user entered the room.
```C++
virtual void OnEnterRoom(int code, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| code    | int    | The error code.   |
| message | string | The error message. |

### OnExitRoom

The local user left the room.
```C++
virtual void OnExitRoom(TUIExitRoomType type, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| type | TUIExitRoomType | The room exit type. |
| message | string | The error message. |

### OnFirstVideoFrame

The first video frame of the local user or a remote user was rendered.
```C++
virtual void OnFirstVideoFrame(const std::string& user_id, const TUIStreamType stream_type) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| stream_type | TUIStreamType | The stream type. |

### OnUserVoiceVolume

The audio volume of a user.
```C++
virtual void OnUserVoiceVolume(const std::string& user_id, int volume)
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| volume | int | The volume level. Value range: 0-100. |

### OnRoomMasterChanged

The host changed.
```C++
virtual void OnRoomMasterChanged(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

## Remote User Callbacks

### OnRemoteUserEnter

A remote user entered the room.
```C++
virtual void OnRemoteUserEnter(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### OnRemoteUserLeave

A remote user exited the room.
```C++
virtual void OnRemoteUserLeave(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### OnRemoteUserCameraAvailable

A remote user enabled/disabled their camera.
```C++
virtual void OnRemoteUserCameraAvailable(const std::string& user_id, bool available) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| available | bool | true: Enabled; false: Disabled. |

### OnRemoteUserScreenAvailable

A remote user started/stopped screen sharing.
```C++
virtual void OnRemoteUserScreenAvailable(const std::string& user_id, bool available) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| available | bool | true: Enabled; false: Disabled. |

### OnRemoteUserAudioAvailable

 A remote user enabled/disabled their mic.
```C++
virtual void OnRemoteUserAudioAvailable(const std::string& user_id, bool available) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| available | bool | true: Enabled; false: Disabled. |

### OnRemoteUserEnterSpeechState

A remote user started speaking.
```C++
virtual void OnRemoteUserEnterSpeechState(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### OnRemoteUserExitSpeechState

A remote user stopped speaking.
```C++
virtual void OnRemoteUserExitSpeechState(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |


## Chat Message Event Callbacks

### OnReceiveChatMessage

A text chat message was received.
```C++
virtual void OnReceiveChatMessage(const std::string& user_id, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| message | string | The message content. |

### OnReceiveCustomMessage

A custom message was received.
```C++
virtual void OnReceiveCustomMessage(const std::string& user_id, const std::string& message) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| message    | string | The custom message content. |

## Room Control Message Callbacks

### OnReceiveSpeechInvitation

The host sent a speech invitation (received by a participant).
```C++
virtual void OnReceiveSpeechInvitation() = 0;
```

### OnReceiveInvitationCancelled

The host canceled the speech invitation (received by a participant).
```C++
virtual void OnReceiveInvitationCancelled() = 0;
```

### OnReceiveReplyToSpeechInvitation

A participant accepted/rejected a speech invitation (received by the host).
```C++
virtual void OnReceiveReplyToSpeechInvitation(const std::string& user_id, bool agree) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |
| agree | bool | Whether the invitation was accepted. |

### OnReceiveSpeechApplication

A participant sent a request to speak (received by the host).
```C++
virtual void OnReceiveSpeechApplication(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### OnSpeechApplicationCancelled

A participant canceled a speech request.
```C++
virtual void OnSpeechApplicationCancelled(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### OnReceiveReplyToSpeechApplication

The host approved/rejected a request to speak.
```C++
virtual void OnReceiveReplyToSpeechApplication(bool agree) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| agree | bool | Whether the request was approved. |

### OnSpeechApplicationForbidden

The host disabled/enabled requests to speak.
```C++
virtual void OnSpeechApplicationForbidden(bool forbidden) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| forbidden | bool | Whether requests to speak were disabled. |

### OnOrderedToExitSpeechState

A participant was asked to stop speaking.
```C++
virtual void OnOrderedToExitSpeechState() = 0;
```

### OnCallingRollStarted

The host started a roll call (received by participants).
```C++
virtual void OnCallingRollStarted() = 0;
```

### OnCallingRollStopped

The host stopped a roll call (received by participants).
```C++
virtual void OnCallingRollStopped() = 0;
```

### OnMemberReplyCallingRoll

A participant replied to the roll call (received by the host).
```C++
virtual void OnMemberReplyCallingRoll(const std::string& user_id) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| user_id | string | The user ID. |

### OnChatRoomMuted

The host disabled/enabled chat messages.
```C++
virtual void OnChatRoomMuted(bool muted) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| muted | bool | Disabled or not. |

### OnMicrophoneMuted

The host disabled mic use.
```C++
virtual void OnMicrophoneMuted(bool muted) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| muted | bool | Disabled or not. |

### OnCameraMuted

The host disabled camera use.
```C++
virtual void OnCameraMuted(bool muted) = 0;
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| muted | bool | Disabled or not. |

## Statistics Collection and Quality Callbacks

### OnStatistics

Callback of technical metric statistics.
```C++
virtual void OnStatistics(const liteav::TRTCStatistics& statis) {}
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| statis | liteav::TRTCStatistics | Statistics. |

### OnNetworkQuality

Network quality.
```C++
virtual void OnNetworkQuality(const liteav::TRTCQualityInfo& local_quality, liteav::TRTCQualityInfo* remote_quality,
        uint32_t remote_quality_count) {}
```

The parameters are described below:

| Parameter | Type | Description |
|-----|-----|-----|
| local_quality | liteav::TRTCQualityInfo | The network quality of the local user. |
| remote_quality | liteav::TRTCQualityInfo* | The network quality of remote users. |
| remote_quality_count | uint32_t | The number of remote users. |

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

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | The reason screen sharing stopped. 0: The user stopped screen sharing; 1: Screen sharing was interrupted by another application. |

## Video Recording Callbacks

### OnRecordError

Recording error.

```C++
virtual void OnRecordError(TXLiteAVLocalRecordError error, const std::string& messgae) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| error | TXLiteAVLocalRecordError  | The error. |
| messgae | string  | The error message. |

### OnRecordComplete

Recording completed.

```C++
virtual void OnRecordComplete(const std::string& path) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| path | string  | The error description. |

### OnRecordProgress

The recording progress.

```C++
virtual void OnRecordProgress(int duration, int file_size) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| duration | int  | The file duration. |
| file_size | int  | The file size. |

## Local Device Test Callbacks

### OnTestSpeakerVolume

The speaker volume.

```C++
virtual void OnTestSpeakerVolume(uint32_t volume) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | The volume level. |

### OnTestMicrophoneVolume

The mic volume.

```C++
virtual void OnTestMicrophoneVolume(uint32_t volume) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | The volume level. |

### OnAudioDeviceCaptureVolumeChanged

The system capturing volume changed.

```C++
virtual void OnAudioDeviceCaptureVolumeChanged(uint32_t volume, bool muted) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | The volume level. |
| muted | bool  | Whether capturing was disabled. |

### OnAudioDevicePlayoutVolumeChanged

The system playback volume level changed.

```C++
virtual void OnAudioDevicePlayoutVolumeChanged(uint32_t volume, bool muted) {}
```

The parameters are described below:

| Parameter       | Type                            | Description  |
| ------ | ---- | -------------------------------------------------- |
| volume | uint32_t  | The volume level. |
| muted | bool  | Whether playback was disabled. |
