`TRTCMeeting` has the following features based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM):
- The host can create a meeting room, and participants can enter the room ID to join the meeting.
- The participants can share their screens with each other.
- All users can send various text and custom messages.

>?The TUIKit series of components are based on two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, the IM SDK Trial Edition will be activated by default, which will support up to 100 DAUs. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

`TRTCMeeting` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, see [Group Audio/Video Room (Flutter)](https://intl.cloud.tencent.com/document/product/647/41945).
- TRTC SDK: The [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency video conferencing component.
- IM SDK: The `MeetingRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms in meetings.

[](id:TRTCMeeting)

## TRTCMeeting API Overview
### Basic SDK APIs

| API      | Description                         |
|-----|-----|
| [sharedInstance](#sharedinstance) | Gets a singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [registerListener](#registerlistener) | Sets an event listener. |
| [unRegisterListener](#unregisterlistener)       | Terminates an event listener. |
| [login](#login) | Logs in. |
| [logout](#logout) | Logs out. |
| [setSelfProfile](#setselfprofile) | Sets the profile. |

### Meeting room APIs

| API      | Description                         |
|-----|-----|
| [createMeeting](#createmeeting) | Creates meeting room (called by host). |
| [destroyMeeting](#destroymeeting) | Closes the meeting room (called by host). |
| [enterMeeting](#entermeeting) | Enters meeting room (called by participant). |
| [leaveMeeting](#leavemeeting) | Leaves meeting room (called by participant). |
| [getUserInfoList](#getuserinfolist)             | Gets the list of all users in the room. It takes effect only if it is called after `enterMeeting()`.  |
| [getUserInfo](#getuserinfo) | Gets the details of a specified user in the room. It takes effect only if it is called after `enterMeeting()`. |

### Remote user APIs

| API      | Description                         |
|-----|-----|
| [startRemoteView](#startremoteview) | Plays back the video of a specified remote member. |
| [stopRemoteView](#stopremoteview) | Stops playing back the video of a specified remote member. |
| [setRemoteViewParam](#setremoteviewparam) | Sets the rendering parameters of a remote video. |
| [muteRemoteAudio](#muteremoteaudio) | Mutes/Unmutes a specified remote member's audio. |
| [muteAllRemoteAudio](#muteallremoteaudio) | Mutes/Unmutes all remote users. |
| [muteRemoteVideoStream](#muteremotevideostream) | Pauses/Resumes a specified remote member's video stream. |
| [muteAllRemoteVideoStream](#muteallremotevideostream) | Pauses/Resumes receiving all remote video streams. |

### Local video operation APIs

| API      | Description                         |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | Enables preview of the local video. |
| [stopCameraPreview](#stopcamerapreview) | Stops local video capturing and preview.|
| [switchCamera](#switchcamera) | Switches between the front and rear cameras.|
| [setVideoEncoderParam](#setvideoencoderparam) | Sets video encoder parameters. |
| [setLocalViewMirror](#setlocalviewmirror) | Sets the mirror mode for local preview. |

### Local audio APIs

| API      | Description                         |
|-----|-----|
| [startMicrophone](#startmicrophone)             | Starts mic capturing.     |
| [stopMicrophone](#stopmicrophone)  | Stops mic capturing. |
| [muteLocalAudio](#mutelocalaudio)               | Mutes/Unmutes local audio.       |
| [setSpeaker](#setspeaker) | Sets whether to play sound from the device’s speaker or receiver. |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume. |
| [startAudioRecording](#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](#stopaudiorecording) | Stops audio recording. |
| [enableAudioVolumeEvaluation](#enableaudiovolumeevaluation) | Enables volume reminder. |

### Screen sharing APIs

| API      | Description                         |
|-----|-----|
| [startScreenCapture](#startscreencapture)   | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture) | Stops screen sharing. |
| [pauseScreenCapture](#pausescreencapture) | Pauses screen sharing. |
| [resumeScreenCapture](#resumescreencapture) | Resumes screen sharing. |

### Management object acquisition APIs

| API      | Description                         |
|-----|-----|
| [getDeviceManager](#getdevicemanager) | Gets the device management object [TXDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html). |
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html). |

### Message sending APIs

| API      | Description                         |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts a text chat message in a meeting, which is generally used for chat. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends a custom text chat message. |

[](id:TRTCLiveRoomDelegate)
## TRTCLiveRoomDelegate API Overview
### Common event callbacks

| API      | Description                         |
|-----|-----|
| [onError](#onerror) | Callback for error.|
| [onWarning](#onwarning) | Callback for warning.|
| [onKickedOffline](#onkickedoffline) | You were kicked offline because another user logged in with the same account. |

### Meeting room event callbacks

| API      | Description                         |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | The meeting room was closed. |
| [onNetworkQuality](#onnetworkquality) | Network status. |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume.     |

### Member entry/exit event callbacks

| API      | Description                         |
|-----|-----|
| [onEnterRoom](#onenterroom) | You entered the meeting. |
| [onLeaveRoom](#onleaveroom) | You left the meeting. |
| [onUserEnterRoom](#onuserenterroom) | A new member joined the meeting. |
| [onUserLeaveRoom](#onuserleaveroom) | A member left the meeting. |

### Member audio/video event callbacks

| API      | Description                         |
|-----|-----|
| [onUserAudioAvailable](#onuseraudioavailable) | A member turned their mic on/off. |
| [onUserVideoAvailable](#onuservideoavailable) | A member turned their camera on/off. |
| [onUserSubStreamAvailable](#onusersubstreamavailable) | A member enabled/disabled the substream image. |

### Message event callback APIs

| API      | Description                         |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | A text chat message was received.|
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | A custom message was received.|

### Screen sharing event callbacks

| API      | Description                         |
|-----|-----|
| [onScreenCaptureStarted](#onscreencapturestarted) | Screen sharing started. |
| [onScreenCapturePaused](#onscreencapturepaused) | Screen sharing paused. |
| [onScreenCaptureResumed](#onscreencaptureresumed) | Screen sharing resumed. |
| [onScreenCaptureStoped](#onscreencapturestoped) | Screen sharing stopped. |

## Basic SDK APIs
### sharedInstance

This API is used to get the [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945) singleton object.
```dart
static Future<TRTCMeeting> sharedInstance();
```

### destroySharedInstance

This API is used to terminate the [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945) singleton object.
```dart
static void destroySharedInstance();
```
>?After the instance is terminated, the externally cached `TRTCMeeting` instance can no longer be used. You need to call [sharedInstance](#sharedinstance) again to get a new instance.

### registerListener

This API is used to set an event listener. You can use `TRTCMeetingDelegate` to get various status notifications of [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/41945).
```dart
void registerListener(MeetingListenerFunc func);
```
>?`func` is the delegation callback of `TRTCMeeting`.

### unRegisterListener

This API is used to terminate an event listener.
```dart
void unRegisterListener(MeetingListenerFunc func);
```

### login

Login
```dart
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| sdkAppId | int | You can view the `SDKAppID` via **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Application Info** in the TRTC console. |
| userId | String | The ID of current user, which is a string that can contain only letters (a-z and A-Z), digits (0–9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security signature. For how to calculate and use it, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |

### logout

Log out
```dart
Future<ActionCallback> logout();
```

### setSelfProfile

This API is used to set the profile.
```dart
Future<ActionCallback> setSelfProfile(String userName, String avatarURL);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userName | String | Username |
| avatarURL | String | User profile photo URL. |

## Meeting Room APIs
### createMeeting

This API is used to create a meeting (called by the host).
```dart
Future<ActionCallback> createMeeting(int roomId);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| roomId | int | The meeting room ID. You need to assign and manage the IDs in a centralized manner. |

Generally, the host calls the APIs in the following steps: 
1. The **host** calls `createMeeting()` and passes in `roomId` to create a meeting, the result of which is returned via `ActionCallback`. 
2. The **host** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted.
3. The **host** calls `startMicrophone()` to enable mic capturing.

### destroyMeeting

This API is used to close a meeting room (called by the host). After creating a meeting, the host can call this API to terminate it.
```dart
Future<ActionCallback> destroyMeeting(int roomId);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| roomId | int | The meeting room ID. You need to assign and manage the IDs in a centralized manner. |

### enterMeeting

This API is used to enter a meeting room (called by a member).
```dart
Future<ActionCallback> enterMeeting(int roomId);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| roomId | int | The meeting room ID. |

Generally, a participant joins a meeting in the following steps: 
1. The **participant** calls `enterMeeting()` and passes in `roomId` to enter the meeting room.
2. The **participant** calls `startCameraPreview()` to enable camera preview and calls `startMicrophone()` to enable mic capturing.
3. The **participant** receives the `onUserVideoAvailable` event and calls `startRemoteView()` and passes in the `userId` of the target member to start playback.

### leaveMeeting

This API is used to leave a meeting room (called by participant).
```dart
Future<ActionCallback> leaveMeeting();
```

### getUserInfoList

This API is used to get the list of all users in the room. It takes effect only if it is called after `enterMeeting()`.
```dart
Future<UserListCallback> getUserInfoList(List<String> userIdList);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userIdList | List&lt;String&gt; | List of `userId` values to obtain. |

### getUserInfo

This API is used to get the details of a specified user in the room. It takes effect only if it is called after `enterMeeting()`.
```dart
Future<UserListCallback> getUserInfo(String userId);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |

## Remote User APIs
### startRemoteView

This API is used to play back the video of a specified remote member.
```dart
Future<void> startRemoteView(String userId, int streamType, int viewId);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| streamType | int | The type of the video stream to watch. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19). |
| viewId | int | `viewId` generated by `TRTCCloudVideoView` |

### stopRemoteView

This API is used to stop playing back the video of a specified remote member.
```dart
Future<void> stopRemoteView(String userId, int streamType);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| streamType | int | The type of the video stream to watch. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19). |

### setRemoteViewParam

This API is used to set the rendering parameters of a specified remote member’s video.
```dart
Future<void> setRemoteViewParam(String userId, int streamType,
  {int fillMode, int rotation, int mirrorType});
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| streamType | int | The type of the video stream to watch. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9a2aaa1d287b6a2169088c5ecbd25f19). |
| fillMode | int | The video image rendering mode. Valid values: Fill (default) or Fit. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ae697c0f66077568d33d0996064776b50). |
| rotation | int | Clockwise video image rotation angle. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ab3d380890a5e0b7b6a29bc5d0e58f8e8). |
| type | int | The mirroring mode of the video. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ae5d847e0006bf2cd689b1116721109ca). |

### muteRemoteAudio

This API is used to mute/unmute a specified remote member.
```dart
Future<void> muteRemoteAudio(String userId, bool mute);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| mute | boolean | `true`: Mute; `false`: Unmute |

### muteAllRemoteAudio

This API is used to mute/unmute all remote members.
```dart
Future<void> muteAllRemoteAudio(bool mute);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| mute | boolean | `true`: Mute; `false`: Unmute |

### muteRemoteVideoStream

This API is used to pause/resume a specified remote member's video stream.
```dart
Future<void> muteRemoteVideoStream(String userId, bool mute);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| mute | boolean | true: Pause; false: Resume |

### muteAllRemoteVideoStream

This API is used to pause/resume all remote video streams.
```dart
Future<void> muteAllRemoteVideoStream(bool mute);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| mute | boolean | true: Pause; false: Resume |

## Local Video Operation APIs
### startCameraPreview

This API is used to enable local video preview.
```dart
Future<void> startCameraPreview(bool isFront, int viewId);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| isFront | boolean | true: Front camera; false: Rear camera. |
| viewId | int | `viewId` generated by `TRTCCloudVideoView` |

### stopCameraPreview

This API is used to stop local video capturing and preview.
```dart
Future<void> stopCameraPreview();
```

### switchCamera

This API is used to switch between the front and rear cameras.
```dart
Future<void> switchCamera(bool isFront);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| isFront | boolean | true: Front camera; false: Rear camera. |

### setVideoEncoderParam

This API is used to set video encoder parameters.
```dart
Future<void> setVideoEncoderParam({
  int videoFps,
  int videoBitrate,
  int videoResolution,
  int videoResolutionMode,
});
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| videoFps | int | Video capturing frame rate. |
| videoBitrate | int | The video bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. |
| videoResolution | int | Resolution. |
| videoResolutionMode | int | The resolution mode. |
>? For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam).

### setLocalViewMirror

This API is used to set the mirror mode for local preview.
```dart
Future<void> setLocalViewMirror(bool isMirror);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| isMirror | boolean | Whether to enable mirroring preview mode. `true`: Yes; `false`: No. |

## Local Audio APIs
### startMicrophone

This API is used to start mic capturing.
```dart
Future<void> startMicrophone({int quality});
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| quality | int | The audio quality mode. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a4451651bf7fc810efc4400964c3c0408). |

### stopMicrophone

This API is used to stop mic capturing.
```dart
Future<void> stopMicrophone();
```

### muteLocalAudio

This API is used to mute/unmute local audio.
```dart
Future<void> muteLocalAudio(bool mute);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| mute | boolean | `true`: Mute; `false`: Unmute |

### setSpeaker

This API is used to set whether to play sound from the device’s speaker or receiver.
```dart
Future<void> setSpeaker(bool useSpeaker);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| useSpeaker | boolean | `true`: Speaker; `false`: Receiver |

### setAudioCaptureVolume

This API is used to set the mic capturing volume.
```dart
Future<void> setAudioCaptureVolume(int volume);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| volume | int | The capture volume. Value range: 0–100. Default value: 100. |

### setAudioPlayoutVolume

This API is used to set the playback volume.
```dart
Future<void> setAudioPlayoutVolume(int volume);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| volume | int | The playback volume. Value range: 0–100. Default value: 100. |

### startAudioRecording

This API is used to start audio recording.
```dart
Future<int?> startAudioRecording(String filePath);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| filePath | String | The storage path of the audio recording file. Specify the path according to your specific needs and ensure that the specified path exists and is writable. This path must be accurate to the file name and extension. The extension determines the format of the audio recording file. Currently, supported formats include PCM, WAV, and AAC. |

### stopAudioRecording

This API is used to stop audio recording.
```dart
Future<void> stopAudioRecording();
```

### enableAudioVolumeEvaluation

This API is used to enable the volume reminder.
```dart
Future<void> enableAudioVolumeEvaluation(int intervalMs);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| intervalMs | int | Sets the interval in ms for triggering the `onUserVoiceVolume` callback. The minimum interval is 100 ms. If the value is smaller than 0, the callback will be disabled. We recommend you set this parameter to 300 ms. |

## Screen Sharing APIs
### startScreenCapture

This API is used to start screen sharing.
```dart
Future<void> startScreenCapture({
  int videoFps,
  int videoBitrate,
  int videoResolution,
  int videoResolutionMode,
  String appGroup,
});
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| videoFps | int | The frame rate for video capturing. |
| videoBitrate | int | The video bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. |
| videoResolution | int | The video resolution. |
| videoResolutionMode | int | The resolution mode. |
| appGroup | String | This parameter takes effect only for iOS and can be ignored for Android. It is the `Application Group Identifier` shared by the primary app and broadcast process. |
>? For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam).

### stopScreenCapture

This API is used to stop screen capturing.
```dart
Future<void> stopScreenCapture();
```

### pauseScreenCapture

This API is used to pause screen capturing.
```dart
Future<void> pauseScreenCapture();
```

### resumeScreenCapture

This API is used to resume screen capturing.
```dart
Future<void> resumeScreenCapture();
```

## Management Object Acquisition APIs
### getDeviceManager

This API is used to get the device management object [TXDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html).
```dart
getDeviceManager();
```

### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html).
```dart
getBeautyManager();
```

You can do the following using `TXBeautyManager`:
- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.

## Message Sending APIs
### sendRoomTextMsg

This API is used to broadcast a text chat message in a meeting, which is generally used for chat.
```dart
Future<ActionCallback> sendRoomTextMsg(String message);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| message | String | A text chat message. |

### sendRoomCustomMsg

This API is used to send a custom text message.
```dart
Future<ActionCallback> sendRoomCustomMsg(String cmd, String message);
```

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| cmd | String | A custom command word used to distinguish between different message types.|
| message | String | A text chat message. |

## `TRTCMeetingDelegate` Event Callback APIs
## Common Event Callback APIs
### onError

Callback for error.
This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending if necessary.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| errCode | int    | The error code.   |
| errMsg | String | The error message.|
| extraInfo | String | Extended field. Certain error codes may carry extra information for troubleshooting. |

### onWarning

Callback for warning.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| warningCode | int | The warning code. |
| warningMsg  | String     | The warning message. |
| extraInfo | String | Extended field. Certain error codes may carry extra information for troubleshooting. |

### onKickedOffline

Callback for being kicked offline because another user logged in to the same account.

## Meeting Room Event Callback APIs
### onRoomDestroy

Callback for meeting room termination. When the host leaves the room, all users in the room will receive this callback.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| roomId | String | The meeting room ID. |

### onNetworkQuality

Callback for network status.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | The upstream network quality. |
| remoteQuality | List&lt;TRTCCloudDef.TRTCQuality&gt; | The downstream network quality. |

### onUserVolumeUpdate

Call volume of a user.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userVolumes | List | Volume of every currently speaking user in the room. Value range: 0-100. |
| totalVolume | int | Total volume level of all remote members. Value range: 0–100. |

## Member Entry/Exit Event Callbacks
### onEnterRoom

You joined the meeting.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| result | int | A value greater than 0 indicates the time (in ms) at which the meeting was joined. A value smaller than 0 indicates the error code thrown while joining the meeting. |

### onLeaveRoom

You left the meeting.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| reason | int | The reason for leaving the meeting. 0: The user actively called `leaveMeeting` to leave the meeting; 1: The user was kicked out of the meeting by the server; 2: The meeting was closed. |

### onUserEnterRoom

A new member joined the meeting.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID of the new member who enters the room. |

### onUserLeaveRoom

A member left the meeting.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID of the member who leaves the room. |

## Member Audio/Video Event Callbacks
### onUserAudioAvailable

A member turned their mic on/off.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| available | boolean | true: The mic is enabled; false: The mic is disabled. |

### onUserVideoAvailable

A member turned their camera on/off.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| available | boolean | true: The camera is enabled; false: The camera is disabled. |

### onUserSubStreamAvailable

A member enabled/disabled the substream image.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| userId | String | The user ID. |
| available | boolean | true: The substream is enabled; false: The substream is disabled. |

## Message Event Callback APIs
### onRecvRoomTextMsg

A text chat message was received.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| message | String | A text chat message. |
| sendId     | String | The message sender's user ID.   |
| userAvatar | String | The sender's profile photo. |
| userName | String | The sender's username. |

### onRecvRoomCustomMsg

A custom message was received.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| command | String | A custom command word used to distinguish between different message types. |
| message | String | A text chat message. |
| sendId     | String | The sender's user ID.   |
| userAvatar | String | The sender's profile photo. |
| userName | String | The sender's username. |

## Screen Sharing Event Callbacks
### onScreenCaptureStarted

Screen sharing started.

### onScreenCapturePaused

Screen sharing paused.

### onScreenCaptureResumed

Screen sharing resumed.

### onScreenCaptureStoped

Screen sharing stopped.

The parameters are described below:

| Parameter   |  Type  | Description         |
|-----|-----|-----|
| reason | int | The reason screen sharing stopped. 0: The user actively stopped; 1: Screen sharing stopped as the shared window was closed. |
