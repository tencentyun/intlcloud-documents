`TRTCMeeting` has the following features based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM):
- The host can create a meeting room, and the attendees can enter the room ID to join the meeting.
- The attendees can share their screens with each other.
- All users can send various text and custom messages.

`TRTCMeeting` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Conferencing (Android)](https://intl.cloud.tencent.com/document/product/647/37283).
- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency video conferencing component.
- IM SDK: the `MeetingRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms in meetings.


<h2 id="TRTCMeeting">TRTCMeeting API Overview</h2>

### Basic SDK APIs

| API | Description |
|-----|-----|
| [sharedInstance](#sharedinstance) | Gets a singleton object.           |
| [destroySharedInstance](#destroysharedinstance) | Terminates a singleton object. |
| [setDelegate](#setdelegate) | Sets event callback. |
| [setDelegateHandler](#setdelegatehandler) | Sets the thread where the event callback is. |
| [login](#login) | Logs in. |
| [logout](#logout) | Logs out. |
| [setSelfProfile](#setselfprofile) | Modifies personal information. |

### Meeting room APIs

| API | Description |
|-----|-----|
| [createMeeting](#createmeeting) | Creates meeting room (called by host). |
| [destroyMeeting](#destroymeeting) | Terminates meeting room (called by host). |
| [enterMeeting](#entermeeting) | Enters meeting room (called by attendee). |
| [leaveMeeting](#leavemeeting) | Leaves meeting room (called by attendee). |

### Remote user APIs
| API | Description |
|-----|-----|
| [getUserInfoList](#getuserinfolist) | Gets the list of all users in room. This API will take effect only if it is called after `enterMeeting()` succeeds. |
| [getUserInfo](#getuserinfo) | Gets the details of specified user in room. This API will take effect only if it is called after `enterMeeting()` succeeds. |
| [startRemoteView](#startremoteview) | Plays back the remote video image of specified member. |
| [stopRemoteView](#stopremoteview) | Stops playing back remote video image. |
| [setRemoteViewFillMode](#setremoteviewfillmode) | Sets the rendering mode of remote image based on user ID. |
| [setRemoteViewRotation](#setremoteviewrotation) | Sets the clockwise rotation angle of remote image. |
| [muteRemoteAudio](#muteremoteaudio) | Mutes specified member. |
| [muteRemoteVideoStream](#muteremotevideostream) | Blocks the video stream of specified member. |

### Local video operation APIs

| API | Description |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | Enables the preview image of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [switchCamera](#switchcamera) | Switches between front and rear cameras. |
| [setVideoResolution](#setvideoresolution) | Sets resolution. |
| [setVideoFps](#setvideofps) | Sets frame rate. |
| [setVideoBitrate](#setvideobitrate) | Sets bitrate. |
| [setLocalViewMirror](#setlocalviewmirror) | Sets the mirroring preview mode of local image. |

### Local audio APIs

| API | Description |
|-----|-----|
| [startMicrophone](#startmicrophone) | Enables mic capturing. |
| [stopMicrophone](#stopmicrophone)  | Stops mic capturing. |
| [setAudioQuality](#setaudioquality) | Sets audio quality. |
| [muteLocalAudio](#mutelocalaudio) | Mutes local audio. |
| [setSpeaker](#setspeaker) | Enables speaker. |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume. |
| [startFileDumping](#startfiledumping) | Starts audio recording. |
| [stopFileDumping](#stopfiledumping) | Stops audio recording. |
| [enableAudioEvaluation](#enableaudioevaluation) | Enables volume reminder. |

### Screen sharing APIs

| API | Description |
|-----|-----|
| [startScreenCapture](#startscreencapture) | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture) | Stops screen sharing. |
| [pauseScreenCapture](#pausescreencapture) | Pauses screen sharing. |
| [resumeScreenCapture](#resumescreencapture) | Resumes screen sharing. |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager). |

### Sharing APIs

| API | Description |
|-----|-----|
| [getLiveBroadcastingURL](#getlivebroadcastingurl) | Gets CDN sharing link. |

### Message sending APIs

| API | Description |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | Broadcasts text message in room. This API is generally used for chat. |
| [sendRoomCustomMsg](#sendroomcustommsg) | Sends custom (signaling) message. |


<h2 id="TRTCMeetingDelegate">TRTCMeetingDelegate API Overview</h2>

### Common event callback APIs

| API | Description |
|-----|-----|
| [onError](#onerror) | Callback for error. |

### Meeting room event callbacks

| API | Description |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | Callback for meeting room termination. |
| [onNetworkQuality](#onnetworkquality)     | Callback for network status. |
| [onUserVolumeUpdate](#onuservolumeupdate) | Callback for user call volume. |

### Member entry/exit event callbacks

| API | Description |
|-----|-----|
| [onUserEnterRoom](#onuserenterroom) | Notification of new member's room entry. |
| [onUserLeaveRoom](#onuserleaveroom) | Notification of member's room exit. |

### Member audio/video event callbacks

| API | Description |
|-----|-----|
| [onUserVideoAvailable](#onuservideoavailable) | Notification of member enabling/disabling camera. |
| [onUserAudioAvailable](#onuseraudioavailable) | Notification of member enabling/disabling mic. |


### Message event callback APIs

| API | Description |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | Receipt of text message. |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of custom message. |

### Screen sharing event callbacks

| API | Description |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | Notification of screen sharing start. |
| [onScreenCapturePaused](#onscreencapturepaused)   | Callback for screen sharing pause. |
| [onScreenCaptureResumed](#onscreencaptureresumed) | Callback for screen sharing resumption. |
| [onScreenCaptureStoped](#onscreencapturestoped)   | Callback for screen sharing stop. |

## Basic SDK APIs

[](id:sharedInstance)
### sharedInstance

This API is used to get the [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283) singleton object.
```java
 public static synchronized TRTCMeeting sharedInstance(Context context);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| context | Context | Android context, which will be converted to `ApplicationContext` for the calling of system APIs |



### destroySharedInstance

This API is used to terminate the [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283) singleton object.
>?After the instance is terminated, the externally cached `TRTCMeeting` instance cannot be used, and you need to call [sharedInstance](#sharedInstance) again to get a new instance.

```java
public static void destroySharedInstance();
```

### setDelegate

This API is used to get the event callback of [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283). You can use `TRTCMeetingDelegate` to get various status notifications of [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37283).
```java
public abstract void setDelegate(TRTCMeetingDelegate delegate);
```

>?`setDelegate` is the delegation callback of `TRTCMeeting`.   

### setDelegateHandler

This API is used to set the thread where the event callback is.
```java
public abstract void setDelegateHandler(Handler handler);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| handler | Handler | Notifies various status notification callbacks in `TRTCMeeting` through this handler. Please do not use this parameter together with `setDelegate`. |

### login

This API is used to log in.
```java
public abstract void login(int sdkAppId,
	 String userId, String userSig,
	 TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppId | int | You can view the `SDKAppID` in the TRTC console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| userId | String | ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (\_). |
| userSig | String | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | ActionCallback | Callback for login. The `code` will be 0 if login succeeds. |


### logout

This API is used to log out.
```java
public abstract void logout(TRTCMeetingCallback.ActionCallback callback);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for logout. The code is 0 if logout succeeds. |

   

### setSelfProfile

This API is used to set profile.
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userName | String | Nickname |
| avatarURL | String | Profile photo address |
| callback | ActionCallback | Callback for personal information setting. The `code` will be 0 if the operation succeeds. |

   


## Meeting Room APIs
### createMeeting

This API is used to create a meeting (called by the host).
```java
public abstract void createMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Meeting room ID. You need to assign and manage the IDs in a centralized manner. |
| callback | ActionCallback | Callback for room creation result. The `code` will be 0 if the operation succeeds.  |

Generally, the host calls the APIs in the following steps: 
1. The **host** calls `createMeeting()` to create a meeting. No matter whether the room is successfully created, the result will be notified to the host through `ActionCallback`.
2. The **host** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted. 
3. The **host** calls `startMicrophone()` to enable mic capturing.

   

### destroyMeeting

This API is used to terminate a meeting room (called by the host). After creating a meeting, the host can call this API to terminate it.
```java
public abstract void destroyMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Meeting room ID. You need to assign and manage the IDs in a centralized manner. |
| callback | ActionCallback | Callback for room termination result. The `code` is 0 if the operation succeeds. |


### enterMeeting

This API is used to enter a meeting (called by the attendee).
```java
public abstract void enterMeeting(int roomId, TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | int | Meeting room ID. |
| callback | ActionCallback | Callback for room entry result. The `code` is 0 if the operation succeeds. |


Generally, the attendee joins a meeting in the following steps: 
1. The **attendee** calls `enterMeeting` and passes in `roomId` to enter the meeting room.
2. The **attendee** calls `startCameraPreview()` to enable camera preview and calls `startMicrophone()` to enable mic capturing.
3. The **attendee** receives the `onUserVideoAvailable` event and calls `startRemoteView(userId)` and passes in the `userId` of the target member to start playback.
   

### leaveMeeting

This API is used to leave a meeting (called by the attendee).
```java
public abstract void leaveMeeting(TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| callback | ActionCallback | Callback for room exit result. The code is 0 if the operation succeeds. |


## Remote User APIs

### getUserInfoList

This API is used to get the list of all users in the room. It will take effect only if it is called after `enterMeeting()` succeeds.


```java
public abstract void getUserInfoList(TRTCMeetingCallback.UserListCallback userListCallback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userListCallback | UserListCallback | Callback for user details. |


### getUserInfo

This API is used to get the details of a specified user in the room. It will take effect only if it is called after `enterMeeting()` succeeds.
```java
public abstract void getUserInfo(String userId, TRTCMeetingCallback.UserListCallback userListCallback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID |
| userListCallback | UserListCallback | Callback for user details. |


### startRemoteView

This API is used to play back the remote video image of a specified member. It can be called when the callback of `onUserVideoAvailable()` is `true`.
```java
public abstract void startRemoteView(String userId, TXCloudVideoView view, final TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user whose video image is to be played back. |
| view | TXCloudVideoView | `view` control that carries the video image. |
| callback | ActionCallback | Callback for operation. |

### stopRemoteView

This API is used to stop playing back the remote video image. It can be called when the callback of `onUserVideoAvailable()` is `false`.
```java
public abstract void stopRemoteView(String userId, final TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of the user whose video image is to be stopped. |
| callback | ActionCallback | Callback for operation. |

### setRemoteViewFillMode

This API is used to set the rendering mode of the remote video image based on user ID.
```java
public abstract void setRemoteViewFillMode(String userId, int fillMode);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID |
| fillMode | int  | Fill or fit mode. Default value: fill (FILL). For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f). |



### setRemoteViewRotation

This API is used to set the clockwise rotation angle of the remote image.
```java
public abstract void setRemoteViewRotation(String userId, int rotation);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| rotation | int  | Clockwise rotation angle. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69). |



### muteRemoteAudio

This API is used to mute or unmute a remote user.
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| mute | boolean | true: mutes; false: unmutes. |

   

### muteRemoteVideoStream

This API is used to block the remote video stream of a specified member.
```java
public abstract void muteRemoteVideoStream(String userId, boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| mute | boolean | true: blocks; false: unblocks. |


​      

## Local Video Operation APIs
### startCameraPreview

This API is used to enable local video preview.
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isFront | boolean | true: front camera; false: rear camera. |
| view | TXCloudVideoView | Control that carries the video image. |

   

### stopCameraPreview

This API is used to stop local video capturing and preview.
```java
public abstract void stopCameraPreview();
```

   

### switchCamera

This API is used to switch between front and rear cameras.
```java
public abstract void switchCamera(boolean isFront);
```
The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| isFront | boolean | Switches between front and rear cameras. true: front camera; false: rear camera. |


### setVideoResolution

Set the resolution

```java
public abstract void setVideoResolution(int resolution);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| resolution | int | Video resolution. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87). |



### setVideoFps

This API is used to set the frame rate.
```java
public abstract void setVideoFps(int fps);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| fps | int | Video capturing frame rate. |

>?**Recommended value:** 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lagging; if lower than 10 fps but higher than 5 fps, there will be slight lagging; if higher than 20 fps, too many resources will be wasted (the frame rate of movies is generally 24 fps).


### setVideoBitrate

This API is used to set the bitrate.
```java
public abstract void setVideoBitrate(int bitrate);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| bitrate | int  | Bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html). |

>? **Recommended value:** please see the optimal bitrate for each tier in `TRTCVideoResolution`. You can also slightly increase the optimal bitrate. For example, `TRTC_VIDEO_RESOLUTION_1280_720` corresponds to the target bitrate of 1,200 Kbps, and you can also set the bitrate to 1,500 Kbps for higher definition.



### setLocalViewMirror

This API is used to set the mirroring preview mode of local video image.
```java
public abstract void setLocalViewMirror(int type);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| type | int | Mirroring mode. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1). |

## Local Audio APIs

### startMicrophone

This API is used to enable mic capturing.
```java
public abstract void startMicrophone();
```

### stopMicrophone

This API is used to stop mic capturing.
```java
public abstract void stopMicrophone();
```

### setAudioQuality

This API is used to set audio quality.
```java
public abstract void setAudioQuality(int quality);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| quality | int | Audio quality. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55). |


### muteLocalAudio

This API is used to mute/unmute local audio.
```java
public abstract void muteLocalAudio(boolean mute);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | Mutes/Unmutes. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86). |



### setSpeaker

This API is used to enable the speaker.
```java
public abstract void setSpeaker(boolean useSpeaker);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| useSpeaker | boolean | true: speaker; false: receiver. |



### setAudioCaptureVolume

This API is used to set the mic capturing volume.
```java
public abstract void setAudioCaptureVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Capture volume. Value range: 0–100. Default value: 100. |


### setAudioPlayoutVolume

This API is used to set the playback volume.
```java
public abstract void setAudioPlayoutVolume(int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Playback volume. Value range: 0–100. Default value: 100. |


### startFileDumping

This API is used to start audio recording.
```java
public abstract void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | Audio recording parameters. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams). |

>? After this API is called, the SDK will record all audios (such as local audio, remote audio, and background music) in the current call to a file. No matter whether room entry is performed, this API will take effect once called. If audio recording is still ongoing when `exitMeeting` is called, it will stop automatically.

### stopFileDumping

This API is used to stop audio recording.
```java
public abstract void stopFileDumping();
```

### enableAudioEvaluation

This API is used to enable the volume reminder.
```java
public abstract void enableAudioEvaluation(boolean enable);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| enable | boolean | true: enables; false: disables. |

>? After this feature is enabled, the result of volume evaluation by the SDK will be obtained in `onUserVolumeUpdate`.

## Screen Sharing APIs
### startScreenCapture

This API is used to start screen sharing.
```java
public abstract void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | Screen sharing encoding parameters. We recommend you use the above configuration. If you set `encParams` to `null`, the encoding parameter settings before `startScreenCapture` is called will be used. |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | Special screen sharing configuration. We recommend you set `floatingView` which can prevent the application from being killed by the system and help protect user privacy. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).

### stopScreenCapture

This API is used to stop screen capture.
```java
public abstract void stopScreenCapture();
```

### pauseScreenCapture

This API is used to pause screen sharing.
```java
public abstract void pauseScreenCapture();
```

### resumeScreenCapture

This API is used to resume screen sharing.
```java
public abstract void resumeScreenCapture();
```

## Sharing APIs
### getLiveBroadcastingURL

This API is used to get the CDN sharing link.
```java
public abstract String getLiveBroadcastingURL();
```

The returned values are as detailed below:

| Returned Value | Type | Description |
|-----|-----|-----|
| url  | String  | CDN sharing link. |

## Beauty Filter APIs
### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager).
```java
public abstract TXBeautyManager getBeautyManager();
```

You can do the following using `TXBeautyManager`:
- Set the beauty filter style and apply effects including skin brightening, rosy skin, eye enlarging, face slimming, chin slimming, chin lengthening/shortening, face shortening, nose narrowing, eye brightening, teeth whitening, eye bag removal, wrinkle removal, and smile line removal.
- Adjust the hairline, eye spacing, eye corners, lip shape, nose wings, nose position, lip thickness, and face shape.
- Apply animated effects such as face widgets (materials).
- Add makeup effects.
- Recognize gestures.


## Message Sending APIs
### sendRoomTextMsg

This API is used to broadcast a text message in the room.
```java
public abstract void sendRoomTextMsg(String message, TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message. |
| callback | ActionCallback | Callback for operation |

   

### sendRoomCustomMsg

This API is used to send a custom text message.
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCMeetingCallback.ActionCallback callback);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| callback | ActionCallback | Callback for operation |

   

## `TRTCMeetingDelegate` Event Callback APIs

## Common Event Callback APIs
### onError

Callback for error.
This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```java
void onError(int code, String message);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| code | int | Error code |
| message | String | Error message |



## Room Event Callback APIs
### onRoomDestroy

Callback for room termination. When the host leaves the room, all users in the room will receive this callback.
```java
void onRoomDestroy(String roomId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| roomId | String | Room ID |

### onNetworkQuality

Callback for network status.
```java
 void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | Upstream network quality. |
| remoteQuality | List&lt;TRTCCloudDef.TRTCQuality&gt; | Downstream network quality. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b).


### onUserVolumeUpdate

Notification to all members of the volume after the volume reminder is enabled.
```java
void onUserVolumeUpdate(String userId, int volume);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID |
| volume | int | Volume. Value range: 0–100 |



## Member Entry/Exit Event Callbacks
### onUserEnterRoom

Notification of new member's room entry.
```java
void onUserEnterRoom(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID of the new member who enters the room |


### onUserLeaveRoom

Notification of member's room exit.
```java
void onUserLeaveRoom(String userId);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID of the member who leaves the room |


## Member Audio/Video Event Callbacks
### onUserVideoAvailable

Notification of member enabling/disabling camera.
```java
void onUserVideoAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| available | boolean | true: the camera is enabled; false: the camera is disabled. |

   

### onUserAudioAvailable

Notification of member enabling/disabling mic.
```java
void onUserAudioAvailable(String userId, boolean available);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID |
| available | boolean | true: the mic is enabled; false: the mic is disabled; |

   

## Message Event Callback APIs
### onRecvRoomTextMsg

A text message was received.
```java
void onRecvRoomTextMsg(String message, TRTCMeetingDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| message | String | Text message |
| userInfo | TRTCMeetingDef.UserInfo | Information of sender |

   

### onRecvRoomCustomMsg

A custom message was received.
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCMeetingDef.UserInfo userInfo);
```

The parameters are as detailed below:

| Parameter | Type | Description |
|-----|-----|-----|
| cmd | String | Custom command word used to distinguish between different message types |
| message | String | Text message |
| userInfo | TRTCMeetingDef.UserInfo | Information of sender |


## Screen Sharing Event Callbacks

### onScreenCaptureStarted

Screen sharing start notification.

```java
void onScreenCaptureStarted();
```

### onScreenCapturePaused

Screen sharing pause notification.

```java
void onScreenCapturePaused();
```

### onScreenCaptureResumed

Screen sharing resumption notification.

```java
void onScreenCaptureResumed();
```

### onScreenCaptureStoped

Screen sharing stop notification.

```java
void onScreenCaptureStopped(int reason);
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | Reason for stop. 0: the user stopped proactively; 1: stopped due to preemption by another application. |





