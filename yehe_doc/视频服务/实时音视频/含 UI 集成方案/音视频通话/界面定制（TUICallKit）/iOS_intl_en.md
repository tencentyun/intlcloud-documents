This document describes how to customize the UI of `TUICallKit` and provides two schemes for customization: **slight UI adjustment** and **custom UI implementation**.

## Scheme 1. Slight UI Adjustment

You can adjust the UI of `TUICallKit` by directly modifying the UI source code in the `iOS/TUICallKit` folder in [tencentyun/TUICallKit](https://github.com/tencentyun/TUICalling).

**Replacing icons:** You can directly replace the icons in the `Resources\Calling.xcassets` folder to customize the color tone and style of all the icons in your application. When you replace an icon, make sure the filename is the same as the original icon.

![img](https://qcloudimg.tencent-cloud.cn/image/document/f2c76a093afce40a97a8d1d5ff281fef.png)


**Replacing ringtones:** You can replace ringtones by replacing the three audio files in the `Resources\AudioFile` folder.

| Filename |  Description |
| ------------------ | ---------------- |
| phone_dialing.m4a  | The sound of making a call. |
| phone_hangup.mp3   | The sound of being hung up.     |
| phone_ringing.flac | The ringtone for incoming calls. |

**Replacing text:** You can modify the strings on the video call UI by modifying the `CallingLocalized.strings` file in `zh-Hans.lproj ` and `en.lproj`.

## Scheme 2. Custom UI Implementation

The entire call feature of `TUICallKit` is implemented based on the UI-less component `TUICallEngine`. You can delete the `tuicallkit` folder and implement your own UIs based entirely on `TUICallEngine`.

### TUICallEngine

`TUICallEngine` is the underlying API of the entire `TUICallKit` component. It provides key APIs such as APIs for making, answering, declining, and hanging up one-to-one audio/video and group calls and device operations.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51012#createinstance) | Creates a `TUICallEngine` instance (singleton).                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51012#destroyinstance) | Terminates a `TUICallEngine` instance (singleton).                         |
| [init](https://www.tencentcloud.com/document/product/647/51012#init) | Completes the authentication of basic audio/video call capabilities.                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51012#addobserver) | Registers an event listener.                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51012#removeobserver) | Unregisters an event listener.                                                |
| [call](https://www.tencentcloud.com/document/product/647/51012#call) | Makes a one-to-one call.                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51012#groupcall) | Makes a group call.                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51012#accept) | Answers a call.                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51012#reject) | Declines a call.                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51012#hangup) | Hangs up a call.                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51012#ignore) | Ignores a call.                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51012#inviteuser) | Invites a user during a group call.                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51012#joiningroupcall) | Joins the current group call actively.                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51012#switchcallmediatype) | Switches the call media type, such as from video call to audio call.                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51012#startremoteview) | Subscribes to the video stream of a remote user.                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51012#stopremotereview) | Unsubscribes from the video stream of a remote user.                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51012#opencamera) | Enables the camera.                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51012#closecamera) | Disables the camera.                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51012#switchcamera) | Switches between the front and rear cameras.                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51012#openmicrophone) | Enables the mic.                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51012#closemicrophone) | Disables the mic.                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51012#selectaudioplaybackdevice) | Selects the audio playback device (receiver/speaker).                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51012#setselfinfo) | Sets the user nickname and profile photo.                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51012#enablemultideviceability) | Enables/Disables the multi-device login mode of `TUICallEngine` (supported by the premium plan). |

### TUICallObserver

`TUICallObserver` is the callback even class of `TUICallEngine`. You can use it to listen on the desired callback events.

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51013#onerror) | An error occurred during the call.           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51013#oncallreceived) | A call was received.               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51013#oncallcancelled) | The call was canceled.               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51013#oncallbegin) | The call was connected.               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51013#oncallend) | The call ended.               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51013#oncallmediatypechanged) | The call media type changed. |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51013#onuserreject) | A user declined the call.      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51013#onusernoresponse) | A user didn't respond.        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51013#onuserlinebusy) | A user was busy.           |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51013#onuserjoin) | A user joined the call.      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51013#onuserleave) | A user left the call.      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51013#onuservideoavailable) | Whether a user had a video stream.   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51013#onuseraudioavailable) | Whether a user had an audio stream.   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51013#onuservoicevolumechanged) | The volume levels of all users.   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51013#onusernetworkqualitychanged) | The network quality of all users.   |

### Definitions of key classes

| API | Description |
| ---------------------- | -------------------------------------------- |
| TUICallMediaType       | The call media type. Enumeration: Video call and audio call. |
| TUICallRole            | The call role. Enumeration: Caller and callee.             |
| TUICallStatus          | The call status. Enumeration: Idle, waiting, and answering.   |
| TUIRoomId              | The audio/video room ID, which can be a number or string.      |
| TUICallCamera          | The camera type. Enumeration: Front camera and rear camera.         |
| TUIAudioPlaybackDevice | The audio playback device type. Enumeration: Speaker and receiver.       |
| TUINetworkQualityInfo  | The information of the current network quality.                           |