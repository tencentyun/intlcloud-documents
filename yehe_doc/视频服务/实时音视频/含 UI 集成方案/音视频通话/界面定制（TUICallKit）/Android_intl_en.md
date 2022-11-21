This document describes how to customize the UI of `TUICallKit` and provides two schemes for customization: **slight UI adjustment** and **custom UI implementation**.

## Scheme 1. Slight UI Adjustment

You can adjust the UI of `TUICallKit` by directly modifying the UI source code in the `Android/tuicallkit` folder in [tencentyun/TUICallKit](https://github.com/tencentyun/TUICalling).

### Replacing icons

You can directly replace the icons in the `res\drawable-xxhdpi` folder to customize the color tone and style of all the icons in your application. When you replace an icon, make sure the filename is the same as the original icon.

![img](https://qcloudimg.tencent-cloud.cn/image/document/f2c76a093afce40a97a8d1d5ff281fef.png)

### Replacing ringtones

You can replace ringtones by replacing the three audio files in the `res\raw` folder.

| Filename |  Description |
| ----------------- | ---------------- |
| phone_dialing.mp3 | The sound of making a call |
| phone_hangup.mp3  | The sound of being hung up     |
| phone_ringing.mp3 | The ringtone for incoming calls |

### Replacing text

You can modify the strings on the video call UI by modifying the `strings.xml` file in `values-zh` and `values-e`.

## Scheme 2. Custom UI Implementation

The entire call feature of `TUICallKit` is implemented based on the UI-less component `TUICallEngine`. You can delete the `tuicallkit` folder and implement your own UIs based entirely on `TUICallEngine`.

### TUICallEngine

`TUICallEngine` is the underlying API of the entire `TUICallKit` component. It provides key APIs such as APIs for making, answering, declining, and hanging up one-to-one audio/video and group calls and device operations.

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51006#createinstance) | Creates a `TUICallEngine` instance (singleton).                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51006#destroyinstance) | Terminates a `TUICallEngine` instance (singleton).                         |
| [init](https://www.tencentcloud.com/document/product/647/51006#init) | Completes the authentication of basic audio/video call capabilities.                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51006#addobserver) | Registers an event listener.                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51006#removeobserver) | Unregisters an event listener.                                                |
| [call](https://www.tencentcloud.com/document/product/647/51006#call) | Makes a one-to-one call.                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51006#groupcall) | Makes a group call.                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51006#accept) | Answers a call.                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51006#reject) | Declines a call.                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51006#hangup) | Hangs up a call.                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51006#ignore) | Ignores a call.                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51006#inviteuser) | Invites a user during a group call.                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51006#joiningroupcall) | Joins the current group call actively.                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51006#switchcallmediatype) | Switches the call media type, such as from video call to audio call.                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51006#startremoteview) | Subscribes to the video stream of a remote user.                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51006#stopremoteview) | Unsubscribes from the video stream of a remote user.                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51006#opencamera) | Enables the camera.                                                  |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51006#closecamera) | Disables the camera.                                                  |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51006#switchcamera) | Switches between the front and rear cameras.                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51006#openmicrophone) | Enables the mic.                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51006#closemicrophone) | Disables the mic.                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51006#selectaudioplaybackdevice) | Selects the audio playback device (receiver/speaker on the device).                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51006#setselfinfo) | Sets the user nickname and profile photo.                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51006#enablemultideviceability) | Enables/Disables the multi-device login mode of `TUICallEngine` (supported by the premium plan). |

### TUICallObserver

`TUICallObserver` is the callback even class of `TUICallEngine`. You can use it to listen on the desired callback events.

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51007#onerror) | An error occurred during the call.           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51007#oncallreceived) | A call was received.               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51007#oncallcancelled) | The call was canceled.               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51007#oncallbegin) | The call was connected.               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51007#oncallend) | The call ended.               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51007#oncallmediatypechanged) | The call media type changed. |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51007#onuserreject) | A user declined the call.      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51007#onusernoresponse) | A user didn't respond.        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51007#onuserlinebusy) | A user was busy.          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51007#onuserjoin) | A user joined the call.      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51007#onuserleave) | A user left the call.      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51007#onuservideoavailable) | Whether a user had a video stream.   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51007#onuseraudioavailable) | Whether a user had an audio stream.   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51007#onuservoicevolumechanged) | The volume levels of all users.   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51007#onusernetworkqualitychanged) | The network quality of all users.   |

## Definitions of Key Types

| API | Description |
| ----------------------------------- | -------------------------------------------- |
| TUICallDefine.MediaType             | The call media type. Enumeration: Video call and audio call. |
| TUICallDefine.Role                  | The call role. Enumeration: Caller and callee.             |
| TUICallDefine.Status                | The call status. Enumeration: Idle, waiting, and answering.   |
| TUICommonDefine.RoomId              | The audio/video room ID, which can be a number or string.      |
| TUICommonDefine.Camera              | The camera type. Enumeration: Front camera and rear camera.         |
| TUICommonDefine.AudioPlaybackDevice | The audio playback device type. Enumeration: Speaker and receiver.       |
| TUICommonDefine.NetworkQualityInfo  | The information of the current network quality.                           |