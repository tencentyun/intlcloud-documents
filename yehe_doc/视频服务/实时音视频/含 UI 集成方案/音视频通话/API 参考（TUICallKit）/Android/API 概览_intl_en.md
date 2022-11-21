## TUICallKit (UI Included)

TUICallKit is an audio/video call component that **includes UI elements**. You can use its APIs to quickly implement an audio/video call application similar to WeChat.

| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51005#createinstance) | Creates a TUICallKit instance (singleton mode). |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51005#setselfinfo) | Sets the user nickname and profile photo.             |
| [call](https://www.tencentcloud.com/document/product/647/51005#call) | Makes a one-to-one call.                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51005#groupcall) | Makes a group call.                                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51005#joiningroupcall) | Joins a group call.         |
| [setCallingBell](https://www.tencentcloud.com/document/product/647/51005#setcallingbell) | Sets the ringtone.               |
| [enableMuteMode](https://www.tencentcloud.com/document/product/647/51005#enablemutemode) | Sets whether to turn on the mute mode.               |
| [enableFloatWindow](https://www.tencentcloud.com/document/product/647/51005#enablefloatwindow) | Sets whether to enable floating windows.              |

## TUICallEngine (No UI)

`TUICallEngine` is an audio/video call component that **does not include UI elements**. If `TUICallKit` does not meet your requirements, you can use the APIs of `TUICallEngine` to customize your project.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51006#createinstance) | Creates a `TUICallEngine` instance (singleton).                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51006#destroyinstance) | Terminates a `TUICallEngine` instance (singleton).                         |
| [init](https://www.tencentcloud.com/document/product/647/51006#init) | Authenticates the basic audio/video call capabilities.                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51006#addobserver) | Registers an event listener.                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51006#removeobserver) | Unregisters an event listener.                                                |
| [call](https://www.tencentcloud.com/document/product/647/51006#call) | Makes a one-to-one call.                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51006#groupcall) | Makes a group call.                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51006#accept) | Answers a call.                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51006#reject) | Declines a call.                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51006#hangup) | Ends a call.                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51006#ignore) | Ignores a call.                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51006#inviteuser) | Invites users to the current group call.                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51006#joiningroupcall) | Joins a group call.                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51006#switchcallmediatype) | Switches the call media type, such as from video call to audio call.                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51006#startremoteview) | Subscribes to the video stream of a remote user.                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51006#stopremoteview) | Unsubscribes from the video stream of a remote user.                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51006#opencamera) | Turns the camera on.                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51006#closecamera) | Turns the camera off.                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51006#switchcamera) || Switches between the front and rear cameras.                   |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51006#openmicrophone) | Enables the mic.                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51006#closemicrophone) | Disables the mic.                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51006#selectaudioplaybackdevice) | Selects the audio playback device (receiver/speaker).                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51006#setselfinfo) | Sets the user nickname and profile photo.                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51006#enablemultideviceability) | Sets whether to enable multi-device login for `TUICallEngine` (supported by the premium package). |

## TUICallObserver

`TUICallObserver` is the callback class of `TUICallEngine`. You can use it to listen for events.

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51007#onerror) | An error occurred during the call.           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51007#oncallreceived) | A call was received.               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51007#oncallcancelled) | The call was canceled.               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51007#oncallbegin) | The call was connected.               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51007#oncallend) | The call ended.               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51007#oncallmediatypechanged) | The call type changed. |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51007#onuserreject) | A user declined the call.      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51007#onusernoresponse) | A user didn't respond.        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51007#onuserlinebusy) | A user was busy.          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51007#onuserjoin) | A user joined the call.      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51007#onuserleave) | A user left the call.      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51007#onuservideoavailable) | Whether a user has a video stream.   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51007#onuseraudioavailable) | Whether a user has an audio stream.   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51007#onuservoicevolumechanged) | The volume levels of all users.   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51007#onusernetworkqualitychanged) | The network quality of all users.   |

## Definitions of Key Types

| API                                                                                                            | Description                                                                                                                                                                                     |
| ----------------------------------- | -------------------------------------------- |
| TUICallDefine.MediaType             | The call type. Enumeration: Video call and audio call. |
| TUICallDefine.Role                  | The call role. Enumeration: Caller and callee.             |
| TUICallDefine.Status                | The call status. Enumeration: Idle, waiting, and answering.   |
| TUICommonDefine.RoomId              | The room ID, which can be a number or string.      |
| TUICommonDefine.Camera              | The camera type. Enumeration: Front camera and rear camera.         |
| TUICommonDefine.AudioPlaybackDevice | The audio playback device type. Enumeration: Speaker and receiver.       |
| TUICommonDefine.NetworkQualityInfo  | The current network quality.                           |