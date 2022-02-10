
`TRTCMeeting` has the following features based on Tencent Real-Time Communication (TRTC) and Instant Messaging (IM):
- The host can create a meeting room, and the attendees can enter the room ID to join the meeting.
- The attendees can share their screens with each other.
- All users can send various text and custom messages.

`TRTCMeeting` is an open-source class depending on two closed-source Tencent Cloud SDKs. For the specific implementation process, please see [Video Conferencing (iOS)](https://intl.cloud.tencent.com/document/product/647/37284).

- TRTC SDK: the [TRTC SDK](https://intl.cloud.tencent.com/document/product/647) is used as the low-latency video conferencing component.
- IM SDK: the `MeetingRoom` feature of the [IM SDK](https://intl.cloud.tencent.com/document/product/1047) is used to implement chat rooms in meetings.

## `TRTCMeeting` API Overview

### Basic SDK APIs

| API | Description |
| ----------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance) | Gets singleton object.           |
| [delegateQueue](#delegatequeue)   | Sets the thread where the event callback is. |
| [delegate](#delegate)             | Sets event callback.           |
| [login](#login)                   | Logs in.                   |
| [logout](#logout)                 | Logs out.                   |
| [setSelfProfile](#setselfprofile) | Sets user information.           |

### Meeting room APIs

| API | Description |
| ----------------------------------- | ------------------------------ |
| [createMeeting](#createmeeting)   | Creates meeting room (called by host).   |
| [destroyMeeting](#destroymeeting) | Terminates meeting room (called by host).   |
| [enterMeeting](#entermeeting)     | Enters meeting room (called by attendee). |
| [leaveMeeting](#leavemeeting)     | Leaves meeting room (called by attendee). |

### Remote user APIs

| API | Description |
| ------------------------------------------------- | ------------------------------------------------------------ |
| [getUserInfoList](#getuserinfolist)             | Gets the list of all users in room. This API will take effect only if it is called after `enterMeeting()` succeeds.  |
| [getUserInfo](#getuserinfo)                     | Gets the details of specified user in room. This API will take effect only if it is called after `enterMeeting()` succeeds. |
| [startRemoteView](#startremoteview)             | Plays back the remote video image of specified member.                                 |
| [stopRemoteView](#stopremoteview)               | Stops playing back remote video image.                                       |
| [setRemoteViewFillMode](#setremoteviewfillmode) | Sets the rendering mode of remote image based on user ID. |
| [setRemoteViewRotation](#setremoteviewrotation) | Sets the clockwise rotation angle of remote image.                               |
| [muteRemoteAudio](#muteremoteaudio)             | Mutes specified remote member.                                      |
| [muteRemoteVideoStream](#muteremotevideostream) | Blocks the video stream of specified remote member.                                   |

### Local video operation APIs

| API | Description |
| ------------------------------------------- | -------------------------- |
| [startCameraPreview](#startcamerapreview) | Enables the preview image of local video.   |
| [stopCameraPreview](#stopcamerapreview)   | Stops local video capturing and preview.   |
| [switchCamera](#switchcamera)   | Switches between front and rear cameras.           |
| [setVideoResolution](#setvideoresolution) | Sets resolution.               |
| [setVideoFps](#setvideofps)               | Sets frame rate.                 |
| [setVideoBitrate](#setvideobitrate)       | Sets bitrate.                 |
| [setLocalViewMirror](#setlocalviewmirror) | Sets the mirroring preview mode of local image. |

### Local audio APIs

| API | Description |
| ------------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | Enables mic capturing.     |
| [stopMicrophone](#stopmicrophone)               | Stops mic capturing.     |
| [setAudioQuality](#setaudioquality)             | Sets audio quality.           |
| [muteLocalAudio](#mutelocalaudio)               | Mutes local audio.       |
| [setSpeaker](#setspeaker)                       | Turns the speaker on.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | Sets mic capturing volume. |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | Sets playback volume.       |
| [startFileDumping](#startfiledumping)           | Starts audio recording.           |
| [stopFileDumping](#stopfiledumping)             | Stops audio recording.           |
| [enableAudioEvaluation](#enableaudioevaluation) | Enables volume reminder.   |

### Screen sharing APIs

| API | Description |
| --------------------------------------------- | -------------- |
| [startScreenCapture](#startscreencapture)   | Starts screen sharing. |
| [stopScreenCapture](#stopscreencapture)     | Stops screen sharing. |
| [pauseScreenCapture](#pausescreencapture)   | Pauses screen sharing. |
| [resumeScreenCapture](#resumescreencapture) | Resumes screen sharing. |

### Beauty filter APIs

| API | Description |
| --------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | Gets the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html). |

### Sharing APIs

| API | Description |
| --------------------------------------------------- | ----------------- |
| [getLiveBroadcastingURL](#getlivebroadcastingurl) | Gets CDN sharing link. |

### Message sending APIs

| API | Description |
| ----------------------------------------- | ---------------------------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     |  Broadcasts text message in room. This API is generally used for text chat.                     |
| [sendRoomCustomMsg](#sendroomcustommsg) | Broadcasts custom (signaling) message in room. |

## TRTCMeetingDelegate API Overview

### Common event callback APIs

| API | Description |
| --------------------- | ---------- |
| [onError](#onerror) | Callback for error. |

### Meeting room event callbacks

| API | Description |
| ------------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | Callback for meeting room termination. |
| [onNetworkQuality](#onnetworkquality)     | Callback for network status.         |
| [onUserVolumeUpdate](#onuservolumeupdate) | User volume     |

### Member entry/exit event callbacks

| API | Description |
| ------------------------------------- | -------------------- |
| [onUserEnterRoom](#onuserenterroom) | Notification of new member's room entry. |
| [onUserLeaveRoom](#onuserleaveroom) | Notification of member's room exit.   |

### Member audio/video event callbacks

| API | Description |
| ----------------------------------------------- | --------------------------- |
| [onUserVideoAvailable](#onuservideoavailable) | Notification of member enabling/disabling camera.  |
| [onUserAudioAvailable](#onuseraudioavailable) | Notification of member enabling/disabling mic. |

### Screen sharing event callbacks

| API | Description |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | Notification of screen sharing start. |
| [onScreenCapturePaused](#onscreencapturepaused)   | Callback for screen sharing pause. |
| [onScreenCaptureResumed](#onscreencaptureresumed) | Callback for screen sharing resumption. |
| [onScreenCaptureStoped](#onscreencapturestoped)   | Callback for screen sharing stop. |

### Message event callback APIs

| API | Description |
| --------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | Receipt of a text message  |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | Receipt of a custom message |

### Screen sharing event callbacks

| API | Description |
| --------------------------------------------------- | -------------- |
| [onScreenCaptureStarted](#onscreencapturestarted) | Notification of screen sharing start. |
| [onScreenCapturePaused](#onscreencapturepaused)   | Callback for screen sharing pause. |
| [onScreenCaptureResumed](#onscreencaptureresumed) | Callback for screen sharing resumption. |
| [onScreenCaptureStoped](#onscreencapturestoped)   | Callback for screen sharing stop. |

## TRTCMeetingDef API Overview

### TRTCMeetingUserInfo (meeting user information)

| Attribute | Description |
| --------------------------------------- | -------------------------------------- |
| [userId](#userid)       | User ID.           |
| [userName](#username)   | Username (nickname). |
| [avatarURL](#avatarurl) | URL of user profile photo.      |
| [isVideoAvailable](#isvideoavailable) | Whether the user has enabled video.                   |
| [isAudioAvailable](#isaudioavailable) | Whether the user has enabled audio.                     |
| [isMuteVideo](#ismutevideo)           | Whether the video image of the user is frozen (the user's video is not played back). |
| [isMuteAudio](#ismuteaudio)           | Whether the audio of the user is muted (the user's audio is not played back). |


## Basic SDK APIs

### sharedInstance

This API is used to get the [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37284) singleton object.

```objective-c
+ (instancetype)sharedInstance;
```

### delegateQueue

This API is used to set the thread where the event callback is.

```objective-c
- (void)setDelegateQueue:(dispatch_queue_t)delegateQueue
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------- | ---------------- | ------------------------------------------------------------ |
| delegateQueue | dispatch_queue_t | Notifies various status notification callbacks in `TRTCMeeting` through this queue. Please do not use this parameter together with `setDelegate` |

### delegate

This API is used to get the event callback of [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37284). You can use `TRTCMeetingDelegate` to get various status notifications of [TRTCMeeting](https://intl.cloud.tencent.com/document/product/647/37284).

### login

This API is used to log in.

```objective-c
- (void)login:(UInt32)sdkAppId userId:(NSString *)userId userSig:(NSString *)userSig callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | ------------------------------------------------------------ |
| sdkAppId | UInt32              | You can view the `SDKAppID` in the TRTC console > **[Application Management](https://console.cloud.tencent.com/trtc/app)** > "Application Info". |
| userId   | NSString            | ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.|
| userSig  | NSString            | Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166). |
| callback | TRTCMeetingCallback | Callback for login. The `code` will be 0 if the operation succeeds.                                  |

### logout

This API is used to log out.

```objective-c
- (void)logout:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | --------------------------- |
| callback | TRTCMeetingCallback | Callback for logout. The `code` will be 0 if the operation succeeds. |

### setSelfProfile

This API is used to set profile.

```objective-c
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(TRTCMeetingCallback)callback;
```

| Parameter | Type | Description |
| --------- | ------------------- | ----------------------------------------- |
| userName  | NSString            | User nickname.                                |
| avatarURL | NSString            | User profile photo.                                |
| callback  | TRTCMeetingCallback | Callback for user information setting result. The `code` will be 0 if the operation succeeds. |



## Meeting Room APIs

### createMeeting

This API is used to create a meeting (called by the host).

```objective-c
- (void)createMeeting:(UInt32)roomId callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------------------------------- |
| roomId   | UInt32              | Room ID. You need to assign and manage the IDs in a centralized manner. |
| callback | TRTCMeetingCallback | Callback for room creation result. The `code` will be 0 if the operation succeeds.  |

Generally, the host calls the APIs in the following steps: 

1. The **host** calls `createMeeting()` to create a meeting. No matter whether the room is successfully created, the result will be notified to the host through `TRTCMeetingCallback`.
2. The **host** calls `startCameraPreview()` to enable camera preview. At this time, the beauty filter parameters can be adjusted. 
3. The **host** calls `startMicrophone()` to enable mic capturing.

### destroyMeeting

This API is used to terminate a meeting room (called by the host). After creating a meeting, the host can call this API to terminate it.

```objective-c
- (void)destroyMeeting:(UInt32)roomId callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------------------------------- |
| roomId   | UInt32              | Room ID. You need to assign and manage the IDs in a centralized manner. |
| callback | TRTCMeetingCallback | Callback for room creation result. The `code` will be 0 if the operation succeeds.  |

### enterMeeting

This API is used to enter a meeting (called by the attendee).

```objective-c
- (void)enterMeeting:(UInt32)roomId callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------------------------------- |
| roomId   | UInt32              | Room ID. You need to assign and manage the IDs in a centralized manner. |
| callback | TRTCMeetingCallback | Callback for room entry result. The `code` will be 0 if the operation succeeds.  |

Generally, the attendee joins a meeting in the following steps: 
1. The **attendee** calls `enterMeeting` and passes in `roomId` to enter the meeting room.
2. The **attendee** calls `startCameraPreview()` to enable camera preview and calls `startMicrophone()` to enable mic capturing.
3. The **attendee** receives the `onUserVideoAvailable` event and calls `startRemoteView(userId)` and passes in the `userId` of the target member to start playback.
   
### leaveMeeting

This API is used to leave a meeting (called by the attendee).

```objective-c
- (void)leaveMeeting:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | ------------------------------------- |
| callback | TRTCMeetingCallback | Callback for room exit result. The `code` will be 0 if the operation succeeds. |



## Remote User APIs

### getUserInfoList

This API is used to get the list of all users in the room. It will take effect only if it is called after `enterMeeting()` succeeds.

```objective-c
- (void)getUserInfoList:(TRTCMeetingUserListCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------------------------- | ------------------ |
| callback | TRTCMeetingUserListCallback | Callback for user details. |

### getUserInfo

This API is used to get the details of a specified user in the room. It will take effect only if it is called after `enterMeeting()` succeeds.

```objective-c
- (void)getUserInfo:(NSString *)userId callback:(TRTCMeetingUserListCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------------------------- | ----------- |
| userId | NSString | Remote user ID.                   |
| callback | TRTCMeetingUserListCallback | Callback for user details. |

### startRemoteView

This API is used to play back the remote video image of a specified member. It can be called when the callback of `onUserVideoAvailable()` is `true`.

```objective-c
- (void)startRemoteView:(NSString *)userId view:(UIView *)view callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------------------- |
| userId   | NSString            | ID of the user whose video image is to be played back.         |
| view     | UIView              | `view` control that carries the video image. |
| callback | TRTCMeetingCallback | Callback for operation.                 |

### stopRemoteView

This API is used to stop rendering the remote video image. It can be called when the callback of `onUserVideoAvailable()` is `false`.

```objective-c
- (void)stopRemoteView:(NSString *)userId callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | ---------------- |
| userId   | NSString            | ID of the user whose video image is to be stopped. |
| callback | TRTCMeetingCallback | Callback for operation.       |

### setRemoteViewFillMode

This API is used to set the rendering mode of the remote video image based on user ID.

```objective-c
- (void)setRemoteViewFillMode:(NSString *)userId fillMode:(TRTCVideoFillMode)fillMode;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ----------------- | ------------------------------------------------------------ |
| userId   | NSString          | User ID                                                    |
| fillMode | TRTCVideoFillMode | Fill or fit mode. Default value: fill (TRTCVideoFillMode_Fill). For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff). |

### setRemoteViewRotation

Set the clockwise rotation angle of remote image

```objective-c
- (void)setRemoteViewRotation:(NSString *)userId rotation:(NSInteger)rotation;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | --------- | ------------------------------------------------------------ |
| userId   | NSString  | Remote user ID. |
| rotation | NSInteger | Clockwise rotation angle. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90). |

### muteRemoteAudio

This API is used to mute or unmute a remote user.

```objective-c
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | -------- | --------------------------------- |
| userId | NSString | Remote user ID.                   |
| mute   | BOOL   | `true`: mutes; `false`: unmutes. |

### muteRemoteVideoStream

This API is used to block the remote video stream of a specified member.

```objective-c
- (void)muteRemoteVideoStream:(NSString *)userId mute:(BOOL)mute;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | -------- | ----------------------------- |
| userId | NSString | Remote user ID.               |
| mute   | BOOL     | true: blocks; false: unblocks. |



## Local Video Operation APIs

### startCameraPreview

This API is used to enable local video preview.

```objective-c
- (void)startCameraPreview:(BOOL)isFront view:(UIView *)view;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------ | ------------------------------------- |
| isFront | BOOL | `true`: turns the front camera on; `false`: turns the rear camera on. |
| view    | UIView | Control that carries the video image.                  |

### stopCameraPreview

This API is used to stop local video capturing and preview.

```objective-c
- (void)stopCameraPreview;
```

### switchCamera

This API is used to switch between the front and rear cameras.

```objective-c
- (void)switchCamera:(BOOL)isFront;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ----------------------------------------------------- |
| isFront | BOOL | Switches between front and rear cameras. true: front camera; false: rear camera. |

### setVideoResolution

This API is used to set the resolution.

```objective-c
- (void)setVideoResolution:(TRTCVideoResolution)resolution;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ------------------- | ------------------------------------------------------------ |
| resolution | TRTCVideoResolution | Video resolution. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5). |

### setVideoFps

This API is used to set the frame rate.

```objective-c
- (void)setVideoFps:(int)fps;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ---- | -------------- |
| fps  | int  | Video capturing frame rate. |

>? **Recommended value:** 15 or 20 fps. If the frame rate is lower than 5 fps, there will be obvious lagging; if lower than 10 fps but higher than 5 fps, there will be slight lagging; if higher than 20 fps, too many resources will be wasted (the frame rate of movies is generally 24 fps).

### setVideoBitrate

This API is used to set the bitrate.

```objective-c
- (void)setVideoBitrate:(int)bitrate;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---- | ------------------------------------------------------------ |
| bitrate | int  | Bitrate. The SDK encodes streams at the target video bitrate and will actively reduce the bitrate only if the network conditions are poor. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454). |

>?**Recommended value:** please see the optimal bitrate for each tier in `TRTCVideoResolution`. You can also slightly increase the optimal bitrate. For example, `TRTC_VIDEO_RESOLUTION_1280_720` corresponds to the target bitrate of 1,200 Kbps, and you can also set the bitrate to 1,500 Kbps for higher definition.

### setLocalViewMirror

This API is used to set the mirroring preview mode of local video image.

```objective-c
- (void)setLocalViewMirror:(TRTCLocalVideoMirrorType)type;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ------------------------ | ------------------------------------------------------------ |
| type | TRTCLocalVideoMirrorType | Mirroring mode. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#a21a93f89a608f4642ecc9d81ef25a454). |



## Local Audio APIs

### startMicrophone

This API is used to enable mic capturing.

```objective-c
- (void)startMicrophone;
```

### stopMicrophone

This API is used to stop mic capturing.

```objective-c
- (void)stopMicrophone;
```

### setAudioQuality

This API is used to set the audio quality.

```objective-c
- (void)setAudioQuality:(TRTCAudioQuality)quality;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ---------------- | ------------------------------------------------------------ |
| quality | TRTCAudioQuality | Audio quality. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53). |

### muteLocalAudio

This API is used to mute/unmute the local audio.

```objective-c
- (void)muteLocalAudio:(BOOL)mute;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---- | ---- | ------------------------------------------------------------ |
| mute | BOOL | Mutes/Unmutes. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9). |

### setSpeaker

This API is used to turn the speaker on.

```objective-c
- (void)setSpeaker:(BOOL)useSpeaker;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ---------- | ---- | ---------------------------- |
| useSpeaker | BOOL | `true`: speaker; `false`: receiver |

### setAudioCaptureVolume

This API is used to set the mic capturing volume.

```objective-c
- (void)setAudioCaptureVolume:(NSInteger)volume;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | --------- | --------------------------- |
| volume | NSInteger | Capture volume. Value range: 0–100. Default value: 100. |

### setAudioPlayoutVolume

This API is used to set the playback volume.

```objective-c
- (void)setAudioPlayoutVolume:(NSInteger)volume;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | --------- | --------------------------- |
| volume | NSInteger | Playback volume. Value range: 0–100. Default value: 100. |

### startFileDumping

This API is used to start audio recording.

```objective-c
- (void)startFileDumping:(TRTCAudioRecordingParams *)params;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ------------------------ | ------------------------------------------------------------ |
| params | TRTCAudioRecordingParams | Audio recording parameters. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams). |

>? After this API is called, the SDK will record all audios (such as local audio, remote audio, and background music) in the current call to a file. No matter whether room entry is performed, this API will take effect once called. If audio recording is still ongoing when `exitMeeting` is called, it will stop automatically.

### stopFileDumping

This API is used to stop audio recording.

```objective-c
- (void)stopFileDumping;
```

### enableAudioEvaluation

This API is used to enable volume reminder.

```objective-c
- (void)enableAudioEvaluation:(BOOL)enable;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ------------------------- |
| enable | BOOL | true: enables; false: disables. |

>? After this feature is enabled, the result of volume evaluation by the SDK will be obtained in `onUserVolumeUpdate`.



## Screen Sharing APIs

### startScreenCapture

This API is used to start screen sharing.

```objective-c
- (void)startScreenCapture:(TRTCVideoEncParam *)params;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ----------------- | ------------------------------------------------------------ |
| params | TRTCVideoEncParam | Screen sharing encoding parameters. We recommend you use the above configuration. If you set `encParams` to `nil`, the encoding parameter settings before `startScreenCapture` is called will be used. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff).

### stopScreenCapture

This API is used to stop screen capture.

```objective-c
- (int)stopScreenCapture
```

### pauseScreenCapture

This API is used to pause screen sharing.

```objective-c
- (int)pauseScreenCapture
```

### resumeScreenCapture

This API is used to resume screen sharing.

```objective-c
- (int)resumeScreenCapture
```



## Sharing APIs

### getLiveBroadcastingURL

This API is used to get the CDN sharing link.

```objective-c
- (NSString *)getLiveBroadcastingURL;
```

The returned values are as detailed below:

| Returned Value | Type | Description |
| ------ | -------- | ------------- |
| url    | NSString | CDN sharing link. |



## Beauty Filter APIs

### getBeautyManager

This API is used to get the beauty filter management object [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html).

```objective-c
- (TXBeautyManager *)getBeautyManager;
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

```objective-c
- (void)sendRoomTextMsg:(NSString *)message callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------- |
| message  | NSString            | Text message.     |
| callback | TRTCMeetingCallback | Callback for sending result. |

### sendRoomCustomMsg

This API is used to send a custom text message.

```objective-c
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(TRTCMeetingCallback)callback;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------------------------------------------- |
| cmd      | NSString            | Custom command word used to distinguish between different message types. |
| message  | NSString            | Text message.                                         |
| callback | TRTCMeetingCallback | Callback for sending result.                                     |



## `TRTCMeetingDelegate` Event Callback APIs

## Common Event Callback APIs

### onError

This callback indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.

```objective-c
- (void)onError:(NSInteger)code message:(NSString* _Nullable)message;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | --------- | ---------- |
| code    | NSInteger | Error code   |
| message | NSString  | Error message |



## Room Event Callback APIs

### onRoomDestroy

Callback for room termination. When the host leaves the room, all users in the room will receive this callback.

```objective-c
- (void)onRoomDestroy:(NSString *)roomId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | -------- | --------- |
| roomId | NSString | Room ID. |

### onNetworkQuality

Callback for network status.

```objective-c
- (void)onNetworkQuality:(TRTCQualityInfo *)localQuality
           remoteQuality:(NSArray<TRTCQualityInfo*> *)remoteQuality;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------------- | -------------------------- | -------------- |
| localQuality  | TRTCQualityInfo            | Upstream network quality. |
| remoteQuality | NSArray&lt;TRTCQualityInfo *&gt; | Downstream network quality. |

>? For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28).

### onUserVolumeUpdate

Callback of the volume of each member in the room after the volume reminder is enabled.

```objective-c
- (void)onUserVolumeUpdate:(NSString *)userId volume:(NSInteger)volume;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | --------- | --------------------- |
| userId | NSString  | User ID            |
| volume | NSInteger | Volume. Value range: 0–100 |



## Member Entry/Exit Event Callbacks

### onUserEnterRoom

Notification of new member's room entry.

```objective-c
- (void)onUserEnterRoom:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | -------- | --------------- |
| userId | NSString | ID of the user who entered the room. |


### onUserLeaveRoom

Notification of member's room exit.

```objective-c
- (void)onUserLeaveRoom:(NSString *)userId;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | -------- | ------------- |
| userId | NSString | ID of the user who left the room. |



## Member Audio/Video Event Callbacks

### onUserVideoAvailable

Notification of member enabling/disabling camera.

```objective-c
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------- | --------------------------------------------- |
| userId    | NSString | User ID. |
| available | BOOL     | true: the camera is enabled; false: the camera is disabled. |

### onUserAudioAvailable

Notification of member enabling/disabling mic.

```objective-c
- (void)onUserAudioAvailable:(NSString *)userId available:(BOOL)available;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| --------- | -------- | --------------------------------------------- |
| userId    | NSString | User ID. |
| available | BOOL     | true: the mic is enabled; false: the mic is disabled; |

   

## Message Event Callback APIs

### onRecvRoomTextMsg

A text message was received.

```objective-c
- (void)onRecvRoomTextMsg:(NSString* _Nullable)message userInfo:(TRTCMeetingUserInfo *)userInfo;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------- | ------------------- | ---------------- |
| message | NSString            | Text message.       |
| userInfo | TRTCMeetingUserInfo | Information of sender |

### onRecvRoomCustomMsg

A custom message was received.

```objective-c
- (void)onRecvRoomCustomMsg:(NSString* _Nullable)cmd message:(NSString* _Nullable)message userInfo:(TRTCMeetingUserInfo *)userInfo;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| -------- | ------------------- | -------------------------------------------------- |
| cmd      | NSString            | Custom command word used to distinguish between different message types. |
| message  | NSString            | Text message.                                         |
| userInfo | TRTCMeetingUserInfo | Information of sender |



## Screen Sharing Event Callbacks

### onScreenCaptureStarted

Screen sharing start notification.

```objective-c
- (void)onScreenCaptureStarted;
```

### onScreenCapturePaused

Screen sharing pause notification.

```objective-c
- (void)onScreenCapturePaused:(int)reason;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | -------------------------------------------------- |
| reason | int  | Reason for pause. 0: the user paused proactively; 1: screen sharing was paused as the screen window became invisible. |

### onScreenCaptureResumed

Screen sharing resumption notification.

```objective-c
- (void)onScreenCaptureResumed:(int)reason;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ---------------------------------------------------------- |
| reason | int  | Reason for resumption, 0: the user resumed proactively; 1: screen sharing was resumed as the screen window became visible. |

### onScreenCaptureStoped

Screen sharing stop notification.

```objective-c
- (void)onScreenCaptureStoped:(int)reason;
```

The parameters are as detailed below:

| Parameter | Type | Description |
| ------ | ---- | ---------------------------------------------------- |
| reason | int | Reason for stop. 0: the user stopped proactively; 1: screen sharing stopped as the shared window was closed |



## `TRTCMeetingDef` Attributes

## TRTCMeetingUserInfo

### userId

User ID.

```objective-c
@property (nonatomic, strong) NSString *userId;
```

### userName

Username (nickname).

```objective-c
@property (nonatomic, strong) NSString *userName;
```

### avatarURL

URL of user profile photo.

```objective-c
@property (nonatomic, strong) NSString *avatarURL;
```

### roomId

Room ID.

```objective-c
@property (nonatomic, assign) UInt32 roomId;
```

### isVideoAvailable

Whether the user has enabled video.

```objective-c
@property (nonatomic, assign) BOOL isVideoAvailable;
```

### isAudioAvailable

Whether the user has enabled audio.

```objective-c
@property (nonatomic, assign) BOOL isAudioAvailable;
```

### isMuteVideo

Whether the video image of the user is frozen (the user's video is not played back).

```objective-c
@property (nonatomic, assign) BOOL isMuteVideo;
```

### isMuteAudio

Whether the audio of the user is muted (the user's audio is not played back).

```objective-c
@property (nonatomic, assign) BOOL isMuteAudio;
```

