## TUICallKit (UI Included)

TUICallKit is an audio/video call component that **includes UI elements**. You can use its APIs to quickly implement an audio/video call application similar to WeChat.

| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51011#createinstance) | Creates a `TUICallKit` instance (singleton mode). |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51011#setselfinfo) | Sets the user nickname and profile photo.             |
| [call](https://www.tencentcloud.com/document/product/647/51011#call) | Makes a one-to-one call.                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51011#groupcall) | Makes a group call.                                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51011#joiningroupcall) | Joins a group call.         |
| [setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell) | Sets the ringtone.               |
| [enableMuteMode](https://www.tencentcloud.com/document/product/647/51011#enablemutemode) | Sets whether to turn on the mute mode.               |
| [enableFloatWindow](https://www.tencentcloud.com/document/product/647/51011#enablefloatwindow) | Sets whether to enable floating windows.              |

## TUICallEngine (No UI)

`TUICallEngine` is an audio/video call component that **does not include UI elements**. If `TUICallKit` does not meet your requirements, you can use the APIs of `TUICallEngine` to customize your project.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51012#createinstance) | Creates a `TUICallEngine` instance (singleton).                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51012#destroyinstance) | Terminates a `TUICallEngine` instance (singleton).                         |
| [init](https://www.tencentcloud.com/document/product/647/51012#init) | Authenticates the basic audio/video call capabilities.                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51012#addobserver) | Registers an event listener.                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51012#removeobserver) | Unregisters an event listener.                                                |
| [call](https://www.tencentcloud.com/document/product/647/51012#call) | Makes a one-to-one call.                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51012#groupcall) | Makes a group call.                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51012#accept) | Answers a call.                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51012#reject) | Declines a call.                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51012#hangup) | Ends a call.                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51012#ignore) | Ignores a call.                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51012#inviteuser) | Invites users to the current group call.                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51012#joiningroupcall) | Joins a group call.                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51012#switchcallmediatype) | Changes the call type, such as from video call to audio call.                    |
| [setRenderView](https://www.tencentcloud.com/document/product/647/51012#setrenderview) | Sets the view object to display a video.                                |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51012#startremoteview) | Sets the view object to display a video.                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51012#stopremoteview) | Unsubscribes from the video stream of a remote user.                                |
| [openCamera](https://www.tencentcloud.com/document/product/647/51012#opencamera) | Turns the camera on.                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51012#closecamera) | Turns the camera off.                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51012#switchcamera) || Switches between the front and rear cameras.                   |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51012#openmicrophone) | Enables the mic.                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51012#closemicrophone) | Disables the mic.                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51012#selectaudioplaybackdevice) | Selects the audio playback device (receiver/speaker).                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51012#setselfinfo) | Sets the alias and profile photo.                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51012#enablemultideviceability) | Sets whether to enable multi-device login for `TUICallEngine` (supported by the premium package). |

### TUICallObserver

`TUICallObserver` is the callback class of `TUICallEngine`. You can use it to listen for events.

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51013#onerror) | An error occurred during the call.           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51013#oncallreceived) | A call was received.               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51013#oncallcancelled) | The call was canceled.               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51013#oncallbegin) | The call was connected.               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51013#oncallend) | The call ended.               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51013#oncallmediatypechanged) | The call type changed. |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51013#onuserreject) | A user declined the call.      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51013#onusernoresponse) | A user didn't respond.        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51013#onuserlinebusy) | A user was busy.           |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51013#onuserjoin) | A user joined the call.      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51013#onuserleave) | A user left the call.      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51013#onuservideoavailable) | Whether a user had a video stream.   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51013#onuseraudioavailable) | Whether a user had an audio stream.   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51013#onuservoicevolumechanged) | The volume levels of all users.   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51013#onusernetworkqualitychanged) | The network quality of all users.   |

## Definitions of Key Types

| API                                                                                                            | Description                                                                                                                                                                                     |
| ---------------------- | -------------------------------------------- |
| TUICallMediaType       | The call type. Enumeration: Video call and audio call. |
| TUICallRole            | The call role. Enumeration: Caller and callee.             |
| TUICallStatus          | The call status. Enumeration: Idle, waiting, and answering.   |
| TUIRoomId              | The room ID, which can be a number or string.      |
| TUICallCamera          | The camera type. Enumeration: Front camera and rear camera.         |
| TUIAudioPlaybackDevice | The audio playback device type. Enumeration: Speaker and receiver.       |
| TUINetworkQualityInfo  | The current network quality.                           |