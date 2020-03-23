
TRTCCloud @ TXLiteAVSDK.

Main API class for the TRTC video call feature.


## Creation and Termination
### delegate

This API is used to set the `TRTCCloudDelegate` callback API.
```
@property (nonatomic, weak) id< TRTCCloudDelegate > delegate;
```

__Overview__

You can use `TRTCCloudDelegate` to get various status notifications from the SDK. For more information, please see the definitions in `TRTCCloudDelegate.h`.

### delegateQueue

This API is used to set the queue that drives the `TRTCCloudDelegate` callback.
```
@property (nonatomic, strong) dispatch_queue_t delegateQueue;
```

__Overview__

The SDK uses the main queue as the driver of `TRTCCloudDelegate` by default. If you do not specify `delegateQueue`, the `TRTCCloudDelegate` callback of the SDK will be called by the main queue. Your operation on UI in the callback function of `TRTCCloudDelegate` is thread-safe now.

### sharedInstance

This API is used to create [TRTCCloud](#trtccloud) singleton.
```
+ (instancetype)sharedInstance
```


### destroySharedIntance

This API is used to terminate [TRTCCloud](#trtccloud) singleton.
```
+ (void)destroySharedIntance
```



## Room API Functions
### enterRoom

This API is used to enter room.
```
- (void)enterRoom:(TRTCParams *)param appScene:(TRTCAppScene)scene 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcparams) * | Room entry parameters. For more information, please see [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcparams). |
| scene | [TRTCAppScene](https://intl.cloud.tencent.com/document/product/647/35123#trtcappscene) | Application scenario. Currently, only video call (`VideoCall`) and LVB (`Live) scenarios are supported. |

__Overview__

If room entry succeeded, the `onEnterRoom(result)` callback from [TRTCCloudDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcclouddelegate) will be received:

- If room entry succeeded, `result` will be a positive number (`result` > 0), indicating the time in milliseconds (ms) used for entering the room.
- If room entry failed, `result` will be a negative number (`result` < 0), indicating the error code for room entry failure. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/647/35124).



>No matter whether room entry is successful, `enterRoom` must be used together with `exitRoom`. If `enterRoom` is called again before `exitRoom` is called, an unexpected error will occur.



### exitRoom

This API is used to exit room.
```
- (void)exitRoom
```

__Overview__

When the [exitRoom](#exitroom) API is called, the logic related to room exit will be executed, such as releasing resources of audio/video devices and codecs. After resources are released, the SDK will use the `onExitRoom()` callback in `TRTCCloudDelegate` to notify you.
If you need to call `enterRoom()` again or switch to another audio/video SDK, please wait until you receive the `onExitRoom()` callback; otherwise, exceptions such as occupied camera or mic (e.g., `AudioSession` in iOS) may occur.


### switchRole

This API is used to switch roles and applies only to the LVB scenario (`TRTCAppSceneLIVE`).
```
- (void)switchRole:(TRTCRoleType)role 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| role | [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35123#trtcroletype) | Target role, which is anchor by default. |

__Overview__

In the LVB scenario, a user may need to switch between "viewer" and "anchor" roles. You can use the `role` field in [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcparams) before room entry to determine the role or use the `switchRole` API to switch roles after room entry.


### connectOtherRoom

This API is used to request cross-room call (anchor competition).
```
- (void)connectOtherRoom:(NSString *)param 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | NSString * | Co-anchoring parameters in the format of JSON string. `roomId` indicates the target room number, and `userId` indicates the target user ID. |

__Overview__

In TRTC, two anchors in different rooms can use the "cross-room call" feature to co-anchor across the rooms. They can engage in "co-anchoring competition" without the need to exit their own rooms.
For example, when anchor A in room "001" uses `connectOtherRoom()` to successfully call anchor B in room "002", all users in room "001" will receive the `onUserEnter(B)` and `onUserVideoAvailable(B,YES)` callbacks of anchor B, and all users in room "002" will receive the `onUserEnter(A)` and `onUserVideoAvailable(A,YES)` callbacks of anchor A.
In short, cross-room call is to share between two anchors in different rooms, so that users in either room can see both of them.


<pre>
               Room 001                    Room 002
            --------------              -------------
 Before cross-room call: | Anchor A      |             | Anchor B     |
            | Viewers U, V, and W  |             | Viewers X, Y, and Z |
            --------------              -------------</pre>



<pre>              Room 001                     Room 002
            --------------              -------------
 After cross-room call: | Anchors A and B    |             | Anchors B and A   |
            | Viewers U, V, and W  |             | Viewers X, Y, and Z |
            --------------              -------------
</pre>

For the sake of compatibility of subsequent extended fields for cross-room call, parameters in JSON format are used currently and must contain at least two fields:
- `roomId`: If anchor A in room "001" wants to co-anchor with anchor B in room "002", the `roomId` must be set to `002` when anchor A calls `connectOtherRoom()`.
- `userId`: If anchor A in room "001" wants to co-anchor with anchor B in room "002", the `userId` must be set to the `userId` of anchor B when anchor A calls `connectOtherRoom()`.


The result of requesting cross-room call will be returned through the `onConnectOtherRoom()` callback in [TRTCCloudDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcclouddelegate).


<pre>
  NSMutableDictionary * jsonDict = [[NSMutableDictionary alloc] init];
  [jsonDict setObject:@(002) forKey:"roomId"];
  [jsonDict setObject:@"userB" forKey:@"userId"];
  NSData* jsonData = [NSJSONSerialization dataWithJSONObject:jsonDict options:NSJSONWritingPrettyPrinted error:nil];
  NSString* jsonString = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
  [trtc connectOtherRoom:jsonString];
</pre>



### disconnectOtherRoom

This API is used to exit cross-room call.
```
- (void)disconnectOtherRoom
```

__Overview__

The result of exiting cross-room call will be returned through the `onDisconnectOtherRoom()` callback in [TRTCCloudDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcclouddelegate).


### setDefaultStreamRecvMode

This API is used to set audio/video data reception mode, which must be set before room entry for it to take effect.
```
- (void)setDefaultStreamRecvMode:(BOOL)autoRecvAudio video:(BOOL)autoRecvVideo
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| autoRecvAudio | BOOL | YES: audio data will be automatically received; NO: `muteRemoteAudio` needs to be called to send or cancel a request. Default value: YES. |
| autoRecvVideo | BOOL | YES: video data will be automatically received; NO: `startRemoteView/stopRemoteView` needs to be called to send or cancel a request. Default value: YES. |

__Overview__

To deliver an excellent instant broadcasting experience, the SDK automatically receives audio/video upon successful room entry by default, that is, you will immediately receive audio/video data from all remote users. If you do not call `startRemoteView`, video data will be automatically canceled due to timeout. If you use this API mainly in scenarios where automatic video data reception is not required, such as audio chat, you can select the reception mode based on your actual needs.

>This API takes effect only if it is set before room entry.




## Video API Functions
### startLocalPreview

This API is used to enable preview image of local video (for iOS).
```
- (void)startLocalPreview:(BOOL)frontCamera view:(TXView *)view 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frontCamera | BOOL | YES: front camera; NO: rear camera. |
| view | TXView * | Control that carries the video image. |

__Overview__

When the first video frame starts to be rendered, you will receive the `onFirstVideoFrame(nil)` callback in [TRTCCloudDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcclouddelegate).


### startLocalPreview

This API is used to enable preview image of local video (for macOS).
```
- (void)startLocalPreview:(TXView *)view 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| view | TXView * | Control that carries the video image. |

__Overview__

Before this method is called, `setCurrentCameraDevice` can be called first to select whether to use the macOS device's built-in camera or an external camera. When the first video frame starts to be rendered, you will receive the `onFirstVideoFrame(nil)` callback in [TRTCCloudDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcclouddelegate).


### stopLocalPreview

This API is used to stop local video capture and preview.
```
- (void)stopLocalPreview
```


### muteLocalVideo

This API is used to specify whether to block local video image.
```
- (void)muteLocalVideo:(BOOL)mute 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | BOOL | YES: blocks; NO: enables. Default value: NO. |

__Overview__

After the local video is blocked, other members in the room will receive the `onUserVideoAvailable` callback notification.


### startRemoteView

This API is used to start displaying remote video image.
```
- (void)startRemoteView:(NSString *)userId view:(TXView *)view 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | ID of remote user. |
| view | TXView * | Control that carries the video image. |

__Overview__

If you receive the `onUserVideoAvailable(userid, YES)` notification from the SDK, you can know that the remote user has enabled the video image. Later, when you use the `startRemoteView(userid)` API to load the remote image of this user, you can use a loading animation to optimize the experience for awaiting video loading. When the first video frame of this user starts to be displayed, you will receive the `onFirstVideoFrame(userId)` event callback.

### stopRemoteView

This API is used to stop displaying remote video image.
```
- (void)stopRemoteView:(NSString *)userId 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | ID of remote user. |

__Overview__

After this API is called, the SDK will stop receiving the remote video stream of the specified user and clear relevant video displaying resources.


### stopAllRemoteView

This API is used to stop displaying all remote video images.
```
- (void)stopAllRemoteView
```

>If there is a screen sharing image, it will be stopped together with other remote video images.



### muteRemoteVideoStream

This API is used to pause receiving the specified remote video stream.
```
- (void)muteRemoteVideoStream:(NSString *)userId mute:(BOOL)mute 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | ID of remote user. |
| mute | BOOL | Whether to stop reception. |

__Overview__

This API only stops receiving remote user's video stream but does not release displaying resources; therefore, the video image will freeze at the last frame before the muting operation.


### muteAllRemoteVideoStreams

This API is used to stop receiving all remote video streams.
```
- (void)muteAllRemoteVideoStreams:(BOOL)mute 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | BOOL | Whether to stop reception. |


### setVideoEncoderParam

This API is used to set video encoder parameters.
```
- (void)setVideoEncoderParam:(TRTCVideoEncParam *)param 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) * | Video encoding parameters. For more information, please see the definition of [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) in `TRTCCloudDef.h`. |

__Overview__

These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.


### setNetworkQosParam

This API is used to set network bandwidth limit parameters.
```
- (void)setNetworkQosParam:(TRTCNetworkQosParam *)param 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcnetworkqosparam) * | Network bandwidth limit parameters. For more information, please see the definition of [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcnetworkqosparam) in `TRTCCloudDef.h`. |

__Overview__

The settings determine the bandwidth limit practices of the SDK in various network conditions (e.g., whether to "ensure definition" or "ensure smoothness" on a weak network).


### setLocalViewFillMode

This API is used to set rendering mode of local image.
```
- (void)setLocalViewFillMode:(TRTCVideoFillMode)mode 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mode | [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideofillmode) | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). |


### setRemoteViewFillMode

This API is used to set rendering mode of remote image.
```
- (void)setRemoteViewFillMode:(NSString *)userId mode:(TRTCVideoFillMode)mode 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID. |
| mode | [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideofillmode) | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). |


### setLocalViewRotation

This API is used to set clockwise rotation angle of local image.
```
- (void)setLocalViewRotation:(TRTCVideoRotation)rotation 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | [TRTCVideoRotation](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideorotation) | Rotation angles of 90, 180, and 270 degrees are supported. Default value: TRTCVideoRotation_0. |


### setRemoteViewRotation

This API is used to set clockwise rotation angle of remote image.
```
- (void)setRemoteViewRotation:(NSString *)userId rotation:(TRTCVideoRotation)rotation 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID. |
| rotation | [TRTCVideoRotation](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideorotation) | Rotation angles of 90, 180, and 270 degrees are supported. Default value: TRTCVideoRotation_0. |


### setVideoEncoderRotation

This API is used to set direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server).
```
- (void)setVideoEncoderRotation:(TRTCVideoRotation)rotation 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | [TRTCVideoRotation](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideorotation) | Currently, rotation angles of 0 and 180 degrees are supported. Default value: TRTCVideoRotation_0. |

__Overview__

When an iPad or iPhone is rotated 180 degrees, as the capture direction of the camera does not change, the video image viewed by remote users will be upside-down. In this case, you can call this API to rotate the image output by the SDK to remote users 180 degrees, so that remote users can view the normal image.


### setLocalViewMirror

This API is used to set mirror mode of local camera's preview image (for iOS).
```
- (void)setLocalViewMirror:(TRTCLocalVideoMirrorType)mirror 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | [TRTCLocalVideoMirrorType](https://intl.cloud.tencent.com/document/product/647/35123#trtclocalvideomirrortype) | Mirror mode. Default value: TRTCLocalVideoMirrorType_Auto. |


### setLocalViewMirror

This API is used to set mirror mode of local camera's preview image (for macOS).
```
- (void)setLocalViewMirror:(BOOL)mirror 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | BOOL | Mirror mode. Default value: YES. |


### setVideoEncoderMirror

This API is used to set mirror mode of image output by encoder.
```
- (void)setVideoEncoderMirror:(BOOL)mirror 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | BOOL | Whether to enable remote mirror mode. YES: yes; NO: no. Default value: NO. |

__Overview__

This API does not change the preview image of the local camera; instead, it changes the video image viewed by the remote user (and recorded by the server).


### setGSensorMode

This API is used to set adaptation mode of the g-sensor.
```
- (void)setGSensorMode:(TRTCGSensorMode)mode 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mode | [TRTCGSensorMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcgsensormode) | G-sensor mode. For more information, please see the definition of `TRTCGSensorMode`. Default value: TRTCGSensorMode_UIAutoLayout. |


### enableEncSmallVideoStream

This API is used to enable dual-channel encoding mode with big and small images.
```
- (int)enableEncSmallVideoStream:(BOOL)enable withQuality:(TRTCVideoEncParam *)smallVideoEncParam 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | Whether to enable small image encoding. Default value: NO. |
| smallVideoEncParam | [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) * | Video parameters of small image stream. |

__Return__

0: success; -1: the big image is already of the lowest image quality.

__Overview__

If the current user is a major role (such as anchor, teacher, or host) in the room and uses PC or Mac, this mode can be enabled. In this mode, the current user will output two channels of video streams, i.e., **HD** and **LD**, at the same time (only one channel of audio stream will be output though). This mode will consume more network bandwidth and CPU computing resources.
As for remote viewers in the same room:
- If the downstream network is good, they can select the **HD** image.
- If the downstream network is poor, they can select the **LD** image.

>Dual-channel encoding will consume more CPU resources and network bandwidth; therefore, this feature can be enabled on macOS, Windows, or high-spec tablets, but should not be enabled on phones.


### setRemoteVideoStreamType

This API is used to select whether to view the big or small image of the specified `uid`.
```
- (void)setRemoteVideoStreamType:(NSString *)userId type:(TRTCVideoStreamType)type 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID. |
| type | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideostreamtype) | Video stream type, i.e., big image or small image. Default value: big image. |

__Overview__

To implement this feature, the dual-channel encoding mode must be enabled by the `uid` through `enableEncSmallVideoStream`; otherwise, this operation will not take effect.


### setPriorRemoteVideoStreamType

This API is used to set the video quality preferred by viewers.
```
- (void)setPriorRemoteVideoStreamType:(TRTCVideoStreamType)type 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| type | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideostreamtype) | Selects whether to watch big image or small image by default. Default value: big image. |

__Overview__

It is recommended to select the LD small image for low-spec devices first. If the dual-channel encoding mode is not enabled, this operation will not take effect.



## Audio API Functions
### startLocalAudio

This API is used to enable local audio capture and upstreaming.
```
- (void)startLocalAudio
```

__Overview__

This function will start mic capture and transmit audio data to other users in the room.
The SDK does not enable local audio capture and upstreaming by default, and you need to call this function to enable it; otherwise, other users in the room cannot hear you.

>This function will check the mic permission. If the current application does not have permission to use the mic, the SDK will ask the user to grant the permission.



### stopLocalAudio

This API is used to disable local audio capture and upstreaming.
```
- (void)stopLocalAudio
```

__Overview__

When local audio capture and upstreaming is disabled, other members in the room will receive the `onUserAudioAvailable(NO)` callback notification.


### muteLocalAudio

This API is used to mute local audio.
```
- (void)muteLocalAudio:(BOOL)mute 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | BOOL | YES: blocks; NO: enables. Default value: NO. |

__Overview__

After local audio is muted, other members in the room will receive the `onUserAudioAvailable(NO)` callback notification.
Different from `stopLocalAudio`, `muteLocalAudio` will not stop sending audio/video data; instead, it continues to send mute packets of an extremely low bitrate. Since some video file formats such as MP4 have a high requirement for audio continuity, an MP4 recording file cannot be played back smoothly if `stopLocalAudio` is used. Therefore, `muteLocalAudio` is recommended in scenarios where the requirement for recording quality is high, so as to record MP4 files with better compatibility.

### setAudioRoute

This API is used to set audio routing.
```
- (void)setAudioRoute:(TRTCAudioRoute)route 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| route | [TRTCAudioRoute](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioroute) | Audio routing, i.e., whether the audio is output by speaker or receiver. Default value: TRTCAudioModeSpeakerphone. |

__Overview__

The hands-free mode of video call features in WeChat and Mobile QQ is implemented based on audio routing. Generally, a mobile phone has two speakers, one is the receiver at the top with low volume, and the other is the stereo speaker at the bottom with high volume. The purpose of setting audio routing is to determine which speaker will be used.


### muteRemoteAudio

This API is used to mute the specified user's audio.
```
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | ID of remote user. |
| mute | BOOL | YES: mutes; NO: does not mute. |


### muteAllRemoteAudio

This API is used to mute all users' audio.
```
- (void)muteAllRemoteAudio:(BOOL)mute 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | BOOL | YES: mutes; NO: does not mute. |


### enableAudioVolumeEvaluation

This API is used to enable volume reminder.
```
- (void)enableAudioVolumeEvaluation:(NSUInteger)interval 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| interval | NSUInteger | Sets the interval in ms for triggering the `onUserVoiceVolume` callback. The minimum interval is 100 ms. If the value is smaller than 0, the callback will be disabled. It is recommended to set this parameter to 300 ms. |

__Overview__

After this feature is enabled, the SDK will return the evaluation of the voice volume level of each channel in `onUserVoiceVolume()`. To enable this feature, call this API before calling `[startLocalAudio](#startlocalaudio)`.

>The volume bar in the demo is implemented based on this API.

### startAudioRecording

This API is used to start audio recording.
```
- (int)startAudioRecording:(TRTCAudioRecordingParams *)param 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | TRTCAudioRecordingParams * | Audio recording parameters. For more information, please see [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudiorecordingparams). |

__Return__

0: success; -1: audio recording has been started; -2: failed to create file or directory; -3: the audio format of the specified file extension is not supported.

__Overview__

After this API is called, the SDK will record all audios (such as local audio, remote audio, and background music) in the current call to a file. No matter whether room entry is performed, this API will take effect once called. If audio recording is still ongoing when `exitRoom` is called, it will stop automatically.


### stopAudioRecording

This API is used to stop audio recording.
```
- (void)stopAudioRecording
```

__Overview__

If audio recording is still ongoing when `exitRoom` is called, it will stop automatically.

### setSystemVolumeType

This API is used to set the system volume type used in call.
```
- (void)setSystemVolumeType:(TRTCSystemVolumeType)type 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| type | TRTCSystemVolumeType | System volume type. For more information, please see [TRTCSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35123#trtcsystemvolumetype). |

>This API must be called before [startLocalAudio](#startlocalaudio) is called.



### enableAudioEarMonitoring

This API is used to enable in-ear monitoring.
```
- (void)enableAudioEarMonitoring:(BOOL)enable 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | YES: enables; NO: disables. Default value: NO. |

__Overview__

After in-ear monitoring is enabled, the local user can hear their own voice.

>This API takes effect only if the user wears headphones.



## Camera API Functions
### switchCamera

This API is used to switch cameras.
```
- (void)switchCamera
```


### isCameraZoomSupported

This API is used to query whether the current camera supports zoom.
```
- (BOOL)isCameraZoomSupported
```


### setZoom

This API is used to set zoom factor (focal length) of camera.
```
- (void)setZoom:(CGFloat)distance 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| distance | CGFloat | Value range: 1–5. The greater the value, the further the focal length. |

__Overview__

The value range is 1–5. 1 indicates the furthest view (normal lens), and 5 indicates the nearest view (enlarging lens).
It is recommended to set the maximum value to 5. If the maximum value is greater than 5, the video will become blurry.


### isCameraTorchSupported

This API is used to query whether the device supports flash (flash mode).
```
- (BOOL)isCameraTorchSupported
```


### enbaleTorch

This API is used to enable or disable flash.
```
- (BOOL)enbaleTorch:(BOOL)enable 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | YES: enables; NO: disables. Default value: NO. |


### isCameraFocusPositionInPreviewSupported

This API is used to query whether the device supports setting focus.
```
- (BOOL)isCameraFocusPositionInPreviewSupported
```


### setFocusPosition

This API is used to set camera focus.
```
- (void)setFocusPosition:(CGPoint)touchPoint 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| touchPoint | CGPoint | Focus position. |


### isCameraAutoFocusFaceModeSupported

This API is used to query whether the device supports automatic recognition of face position.
```
- (BOOL)isCameraAutoFocusFaceModeSupported
```


### enableAutoFaceFoucs

This API is used to enable automatic recognition of face position.
```
- (void)enableAutoFaceFoucs:(BOOL)enable 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | YES: enables; NO: disables. Default value: YES. |


### getCameraDevicesList

This API is used to gets list of cameras.
```
- (NSArray< TRTCMediaDeviceInfo * > *)getCameraDevicesList
```

__Return__

List of cameras, in which the first one is the current default device of the system.

__Overview__

A macOS device has a built-in camera and supports USB cameras. If you want users to be able to select their external cameras, you can provide a feature of selecting from multiple cameras.

### getCurrentCameraDevice

This API is used to get the currently used camera.
```
- (TRTCMediaDeviceInfo *)getCurrentCameraDevice
```


### setCurrentCameraDevice

This API is used to set the camera to be used.
```
- (int)setCurrentCameraDevice:(NSString *)deviceId 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| deviceId | NSString * | Device ID obtained from `getCameraDevicesList`. |

__Return__

0: success; -1: failure.



## Audio Device API Functions
### getMicDevicesList

This API is used to get list of mics.
```
- (NSArray< TRTCMediaDeviceInfo * > *)getMicDevicesList
```

__Return__

List of mics, in which the first one is the current default device of the system.

__Overview__

A macOS device has a built-in high-quality mic and supports external mics. In addition, many USB cameras have built-in mics. If you want users to be able to select their external mics, you can provide a feature of selecting from multiple mics.


### getCurrentMicDevice

This API is used to get the current mic device.
```
- (TRTCMediaDeviceInfo *)getCurrentMicDevice
```

__Return__

This API is used to get current mic device information.


### setCurrentMicDevice

This API is used to set the mic to be used.
```
- (int)setCurrentMicDevice:(NSString *)deviceId 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| deviceId | NSString * | Device ID obtained from `getMicDevicesList`. |

__Return__

0: success; \<0: failure.


### getCurrentMicDeviceVolume

This API is used to get current mic volume level.
```
- (float)getCurrentMicDeviceVolume
```

__Return__

Mic volume level.


### setCurrentMicDeviceVolume

This API is used to set mic volume level.
```
- (void)setCurrentMicDeviceVolume:(NSInteger)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | NSInteger | Mic volume level. Value range: 0–100. |


### getSpeakerDevicesList

This API is used to get list of speakers.
```
- (NSArray< TRTCMediaDeviceInfo * > *)getSpeakerDevicesList
```

__Return__

List of speakers, in which the first one is the current default device of the system.


### getCurrentSpeakerDevice

This API is used to get the currently used speaker.
```
- (TRTCMediaDeviceInfo *)getCurrentSpeakerDevice
```

__Return__

This API is used to get current speaker device information.


### setCurrentSpeakerDevice

This API is used to set the speaker to be used.
```
- (int)setCurrentSpeakerDevice:(NSString *)deviceId 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| deviceId | NSString * | Device ID obtained from `getSpeakerDevicesList`. |

__Return__

0: success; \<0: failure.


### getCurrentSpeakerDeviceVolume

This API is used to get current speaker volume level.
```
- (float)getCurrentSpeakerDeviceVolume
```

__Return__

Speaker volume level.


### setCurrentSpeakerDeviceVolume

This API is used to set current speaker volume level.
```
- (int)setCurrentSpeakerDeviceVolume:(NSInteger)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | NSInteger | Speaker volume to be set. Value range: 0–100. |

__Return__

0: success; \<0: failure.



## Beauty Filter API Functions
### getBeautyManager

This API is used to get the beauty filter management object.
```
- (TXBeautyManager *)getBeautyManager
```

__Overview__

You can use the following features with beauty filter management:
- Set beauty effects such as "beauty filter style", "brightening", "rosy skin", "eye enlarging", "face slimming", "chin slimming", "chin lengthening or shortening", "face shortening", "nose narrowing", "eye brightening", "teeth whitening", "eye bag removal", "wrinkle removal", and "smile line removal".
- Adjust the "hairline", "eye distance", "eye corners", "mouth shape", "nose wing", "nose position", "lip thickness", and "face shape".
- Set animated effects such as facial pendants (materials)
- Add makeup effects
- Recognize gestures


### setBeautyStyle

This API is used to set effect levels of beauty, brightening, and rosy skin filters.
```
- (void)setBeautyStyle:(TRTCBeautyStyle)beautyStyle beautyLevel:(NSInteger)beautyLevel whitenessLevel:(NSInteger)whitenessLevel ruddinessLevel:(NSInteger)ruddinessLevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| beautyStyle | [TRTCBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35123#trtcbeautystyle) | Beauty filter style: smooth or natural. The smooth style has more obvious skin smoothing effect and is suitable for entertaining scenarios. |
| beautyLevel | NSInteger | Effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |
| whitenessLevel | NSInteger | Effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |
| ruddinessLevel | NSInteger | Effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

__Overview__

The SDK is integrated with two skin smoothing algorithms of different styles. One is called "smooth" and is suitable for shows as its effect is more obvious. The other is called "natural", which retains more facial details and seems more natural subjectively.


### setFilter

This API is used to specify material filter effect.
```
- (void)setFilter:(TXImage *)image 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| image | TXImage * | Specified material, i.e., color lookup table. **The material must be in PNG format.** |


### setFilterConcentration

This API is used to set effect level of a filter.
```
- (void)setFilterConcentration:(float)concentration 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| concentration | float | Value range: 0–1. The greater the value, the more obvious the effect. Default value: 0.5. |

__Overview__

In application scenarios such as shows, a high effect level is required to highlight the characteristics of anchors. The default effect level is 0.5, and if it is not sufficient, it can be adjusted with the following APIs.


### setWatermark

This API is used to add watermark.
```
- (void)setWatermark:(TXImage *)image streamType:(TRTCVideoStreamType)streamType rect:(CGRect)rect 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| image | TXImage * | Watermark image, **which must be a PNG image with transparent background.** |
| streamType | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideostreamtype) | `setWatermark` needs to be called twice if the screen sharing channel also requires a watermark. |
| rect | CGRect | Unified coordinates of the watermark relative to the encoded resolution. Value range of `x`, `y`, `width`, and `height`: 0–1. |

__Overview__

The watermark position is determined by `rect`, which is in the format of (x, y, width, height).
- x: X coordinate of watermark, which is a floating point number between 0 and 1.
- y: Y coordinate of watermark, which is a floating point number between 0 and 1.
- width: width of watermark, which is a floating point number between 0 and 1.
- height: it does not need to be set. The SDK will automatically calculate the height according to the watermark image's aspect ratio.


For example, if the current encoding resolution is 540 * 960 and `rect` is set to (0.1, 0.1, 0.2, 0.0), then the coordinates of the top-left point of the watermark will be (540 * 0.1, 960 * 0.1), i.e., (54, 96), the watermark width will be 540 * 0.2 = 108 px, and the height will be calculated automatically.


### setEyeScaleLevel

This API is used to set effect level of the eye enlarging filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setEyeScaleLevel:(float)eyeScaleLevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| eyeScaleLevel | float | Effect level of the eye enlarging filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setFaceScaleLevel

This API is used to set effect level of the face slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceScaleLevel:(float)faceScaleLevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceScaleLevel | float | Effect level of the face slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setFaceVLevel

This API is used to set effect level of the chin slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceVLevel:(float)faceVLevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceVLevel | float | Effect level of the chin slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setChinLevel

This API is used to set effect level of the chin lengthening/shortening or shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setChinLevel:(float)chinLevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| chinLevel | float | Effect level of the chin lengthening/shortening filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates that the chin is shortened, while a value greater than 0 indicates that the chin is lengthened. |


### setFaceShortLevel

This API is used to set effect level of the face shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setFaceShortLevel:(float)faceShortlevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceShortlevel | float | Effect level of the face shortening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setNoseSlimLevel

This API is used to set effect level of the nose slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setNoseSlimLevel:(float)noseSlimLevel TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| noseSlimLevel | float | Effect level of the nose slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setGreenScreenFile

This API is used to set green screen video (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setGreenScreenFile:(NSURL *)file 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| file | NSURL * | Path to the video file, which can be in MP4 format. nil: disables the effect. |

__Overview__

The green screen feature here is not intelligent keying. It requires that there be a green screen behind the videoed person or object for further chroma keying.


### selectMotionTmpl

This API is used to select AI animated effect pendant (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)selectMotionTmpl:(NSString *)tmplPath TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | NSString * | Path to animated effect file. |


### setMotionMute

This API is used to mute animated effect (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
- (void)setMotionMute:(BOOL)motionMute TRTC_DEPRECAETD_BEAUTY_API
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionMute | BOOL | YES: mutes; NO: does not mute. |

__Overview__

Some animated effects have audio effects, which can be disabled through this API when they are played back.



## Secondary Stream API Functions (macOS)
### startRemoteSubStreamView

This API is used to start displaying screen sharing image of a remote user.
```
- (void)startRemoteSubStreamView:(NSString *)userId view:(TXView *)view 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | ID of remote user. |
| view | TXView * | Rendering control. |

__Overview__

Different from `startRemoteView()` that is used to display the primary image, this API can only be used to display the image of the secondary channel (e.g., screen sharing and remote video playback).

>This API must be called after `onUserSubStreamAvailable` is called back.



### stopRemoteSubStreamView

This API is used to stop displaying screen sharing image of a remote user.
```
- (void)stopRemoteSubStreamView:(NSString *)userId 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | ID of remote user. |


### setRemoteSubStreamViewFillMode

This API is used to set display mode of screen sharing image.
```
- (void)setRemoteSubStreamViewFillMode:(NSString *)userId mode:(TRTCVideoFillMode)mode 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID. |
| mode | [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideofillmode) | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). Default value: TRTCVideoFillMode_Fit. |

__Overview__

Different from `setRemoteViewFillMode()` that is used to set the display mode of primary image, this API can be used to set the remote image of the secondary channel (e.g., screen sharing and remote video playback).


### getScreenCaptureSourcesWithThumbnailSize

This API is used to enumerate shareable windows.
```
- (NSArray< TRTCScreenCaptureSourceInfo * > *)getScreenCaptureSourcesWithThumbnailSize:(CGSize)thumbnailSize iconSize:(CGSize)iconSize 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| thumbnailSize | CGSize | Specifies thumbnail size of the window to be obtained. The thumbnail can be drawn on the window selection UI. |
| iconSize | CGSize | Specifies icon size of the window to be obtained. |

__Return__

List of windows (including the screen).

__Overview__

If you want to add the screen sharing feature to your application, a window selection UI needs to be displayed first generally, so that the user can select the window to be shared. You can use the related functions to get the ID, type, name, and thumbnail of shareable windows and implement the window selection UI with the obtained information. Or, you can use the window selection UI implemented in the demo's source code.

>The returned list includes the screen and application windows. The screen will be in the first several elements in the list.



### selectScreenCaptureTarget

This API is used to set screen sharing parameters. This method can be called during screen sharing.
```
- (void)selectScreenCaptureTarget:(TRTCScreenCaptureSourceInfo *)screenSource rect:(CGRect)rect capturesCursor:(BOOL)capturesCursor highlight:(BOOL)highlight 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| screenSource | [TRTCScreenCaptureSourceInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcscreencapturesourceinfo) * | Specifies sharing source. |
| rect | CGRect | Specify the area to be captured (if `CGRectZero` is passed in, the full screen will be shared by default). |
| capturesCursor | BOOL | Whether to capture mouse cursor. |
| highlight | BOOL | Whether to highlight the window being shared. |

__Overview__

If you want to switch to another window to be shared during screen sharing, you can call this function again without starting screen sharing again.


### startScreenCapture

This API is used to start screen sharing.
```
- (void)startScreenCapture:(NSView *)view 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| view | NSView * | Parent control of the rendering control. |


### stopScreenCapture

This API is used to stop screen capture.
```
- (int)stopScreenCapture
```

__Return__

0: success; \<0: failure.


### pauseScreenCapture

This API is used to pause screen sharing.
```
- (int)pauseScreenCapture
```

__Return__

0: success; \<0: failure.


### resumeScreenCapture

This API is used to resume screen sharing.
```
- (int)resumeScreenCapture
```

__Return__

0: success; \<0: failure.


### setSubStreamEncoderParam

This API is used to set encoder parameters for screen sharing.
```
- (void)setSubStreamEncoderParam:(TRTCVideoEncParam *)param 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) * | Secondary stream encoding parameters. For more information, please see the definition of [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) in `TRTCCloudDef.h`. |

__Overview__

Different from `setVideoEncoderParam()` that is used to set the encoder of primary image, this function can only be used to set the encoder of the secondary channel (screen sharing and remote video playback). 
These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.


### setSubStreamMixVolume

This API is used to set audio mixing volume level of screen sharing.
```
- (void)setSubStreamMixVolume:(NSInteger)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | NSInteger | Volume level set. Value range: 0–100. |

__Overview__

The greater the value, the larger the ratio of the secondary stream volume level to the mic volume level. You are not recommended to set a high value for this parameter as a high volume level will cover the mic sound.


## Custom Capture and Rendering API Functions
### enableCustomVideoCapture

This API is used to enable custom video capture mode.
```
- (void)enableCustomVideoCapture:(BOOL)enable 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | Whether to enable. Default value: NO. |

__Overview__

After the custom mode is enabled, the SDK will not run the original video capture process and retain only the encoding and sending capabilities. You need to use `sendCustomVideoData()` to continuously insert the captured video image into the SDK.


### sendCustomVideoData

This API is used to deliver the captured video data to the SDK.
```
- (void)sendCustomVideoData:(TRTCVideoFrame *)frame 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | [TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoframe) * | Video data, which can be in PixelBuffer NV12, BGRA, or I420 format. |

__Overview__

It is recommended to enter the following information for [TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoframe) (other fields can be left empty):
- pixelFormat: `TRTCVideoPixelFormat_NV12` is recommended.
- bufferType: `TRTCVideoBufferType_PixelBuffer` is recommended.
- pixelBuffer: common video data format on iOS.
- data: raw video data format, which is used if `bufferType` is `NSData`.
- timestamp: if the intervals for `timestamp` are uneven, the audio/video sync and quality of MP4 recording will be seriously affected.
- width: video image length, which needs to be set if `bufferType` is `NSData`.
- height: video image width, which needs to be set if `bufferType` is `NSData`.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35123/35158).

>
>- The SDK has an internal frame rate control logic, and the target frame rate set in `setVideoEncoderParam` shall prevail. If the frame rate is too high, automatic frame discarding may occur; if too low, automatic frame interpolation will be implemented.
>- It is recommended to set `timestamp` in `frame` to 0, so that the SDK will set the timestamp by itself. However, please "evenly" set the calling interval of `sendCustomVideoData`; otherwise, the video frame rate will be unstable.


### setLocalVideoRenderDelegate

This API is used to set callback of custom rendering for local video.
```
- (int)setLocalVideoRenderDelegate:(id< TRTCVideoRenderDelegate >)delegate pixelFormat:(TRTCVideoPixelFormat)pixelFormat bufferType:(TRTCVideoBufferType)bufferType 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| delegate | id< [TRTCVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcvideorenderdelegate) > | Custom rendering callback. |
| pixelFormat | [TRTCVideoPixelFormat](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideopixelformat) | Specifies the called back pixel format. |
| bufferType | [TRTCVideoBufferType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideobuffertype) | PixelBuffer: this can be directly converted to `UIImage` by using `imageWithCVImageBuffer`; NSData: this is memory-mapped video data. |

__Return__

0: success; \<0: error.

__Overview__

After this method is set, the SDK will skip its own rendering process and call back the captured data. Therefore, you need to complete image rendering on your own.
- `pixelFormat` specifies the format of the called back data, such as NV12, i420, and 32BGRA.
- `bufferType` specifies the buffer type. `PixelBuffer` has the highest efficiency, while `NSData` makes the SDK to perform a memory conversion internally, which will result in extra performance loss.




### setRemoteVideoRenderDelegate

This API is used to set callback of custom rendering for remote video.
```
- (int)setRemoteVideoRenderDelegate:(NSString *)userId delegate:(id< TRTCVideoRenderDelegate >)delegate pixelFormat:(TRTCVideoPixelFormat)pixelFormat bufferType:(TRTCVideoBufferType)bufferType 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | Specifies target `userId`. |
| delegate | id< [TRTCVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcvideorenderdelegate) > | Custom rendering callback. |
| pixelFormat | [TRTCVideoPixelFormat](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideopixelformat) | Specifies the called back pixel format. |
| bufferType | [TRTCVideoBufferType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideobuffertype) | PixelBuffer: this can be directly converted to `UIImage` by using `imageWithCVImageBuffer`; NSData: this is memory-mapped video data. |

__Return__

0: success; \<0: error.

__Overview__

This method is similar to `setLocalVideoRenderDelegate`. The difference is that one is callback of rendering the local image, while the other is callback of rendering the remote image.

>Before this function is called, `startRemoteView` needs to be called to get the video stream of the remote user (`view` can be set to `nil` for this end); otherwise, there will be no data called back.



### enableCustomAudioCapture

This API is used to enable custom audio capture mode.
```
- (void)enableCustomAudioCapture:(BOOL)enable 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | BOOL | Whether to enable. true: yes; false: no. Default value: NO. |

__Overview__

After the custom mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use `sendCustomAudioData()` to continuously insert the captured audio data into the SDK.

>As acoustic echo cancellation (AEC) requires strict control on the audio capture and playback time, after custom audio capture is enabled, AEC may fail.



### sendCustomAudioData

This API is used to deliver the captured audio data to the SDK.
```
- (void)sendCustomAudioData:(TRTCAudioFrame *)frame 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | [TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioframe) * | Audio data. |

__Overview__

It is recommended to enter the following information for [TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioframe):

- data: audio frame buffer. Audio frame data must be in PCM format, and it is recommended to set sampling time to 20 ms for each frame. **For example, if the sample rate is 48000, then the frame length for mono channel will be `48000 * 0.02s * 1 * 16 bit = 15360 bit = 1920 bytes`.**
- sampleRate: sample rate. Currently, only 48000 is supported.
- channel: number of channels (if stereo is used, data is interwoven). Valid values: 1: mono channel; 2: dual channel.
- timestamp: if the intervals for `timestamp` are uneven, the audio/video sync and quality of MP4 recording will be seriously affected.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35123/35158).

>You can set `timestamp` in `frame` to `0`, so that the SDK will set the timestamp by itself. However, please "evenly" set the calling interval of `sendCustomAudioData`; otherwise, the audio will be unstable.



### setAudioFrameDelegate

This API is used to set audio data callback.
```
- (void)setAudioFrameDelegate:(id< TRTCAudioFrameDelegate >)delegate 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| delegate | id< [TRTCAudioFrameDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcaudioframedelegate) > | Audio data callback. If `delegate = nil`, data callback will be stopped. |

__Overview__

After this method is set, the SDK will internally call back the audio data (in PCM format), including:
- onCapturedAudioFrame: audio data captured by current mic
- onPlayAudioFrame: audio data from each remote user before audio mixing
- onMixedPlayAudioFrame: audio data to be played back by speaker after audio data from each channel is mixed



## Custom Message Sending API Functions
### sendCustomCmdMsg

This API is used to send custom message to all users in the room.
```
- (BOOL)sendCustomCmdMsg:(NSInteger)cmdID data:(NSData *)data reliable:(BOOL)reliable ordered:(BOOL)ordered 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| cmdID | NSInteger | Message ID. Value range: 1–10. |
| data | NSData * | Message to be sent, which can contain up to 1 KB (1,000 bytes) of data. |
| reliable | BOOL | Whether reliable sending is enabled; if yes, the recipient needs to temporarily store the data of a certain period to wait for re-sending, which will cause certain delay. |
| ordered | BOOL | Whether orderly sending is enabled, i.e., whether the data should be received in the same order in which it is sent; if yes, the recipient needs to temporarily store and sort messages, which will cause certain delay. |

__Return__

YES: message has been sent successful; NO: failed to send message.

__Overview__

This API can be used to broadcast your custom data to other users in the room though the audio/video data channel. Due to reuse of this channel, please strictly control the frequency of sending custom messages and message size; otherwise, the quality control logic of the audio/video data will be affected, causing uncertain issues.

>This API has the following restrictions:
>- Up to 30 messages can be sent per second to all users in the room.
>- A packet can contain up to 1 KB of data; if the threshold is exceeded, the packet is very likely to be discarded by the intermediate router or server.
>- A client can send up to 8 KB of data in total per second.
>- `reliable` and `ordered` must be set to the same value (`YES` or `NO`) and cannot be set to different values currently.
>- You are strongly recommended to use different `cmdIDs` for messages of different types. This can reduce message delay when orderly sending is required.


### sendSEIMsg

This API is used to embed custom data of a small size in video frames.
```
- (BOOL)sendSEIMsg:(NSData *)data repeatCount:(int)repeatCount 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| data | NSData * | Data to be sent, which can contain up to 1 KB (1,000 bytes) of data. |
| repeatCount | int | Data sending count. |

__Return__

YES: the message is allowed and will be sent to subsequent video frames; NO: the message is not allowed to be sent.

__Overview__

Different from how `sendCustomCmdMsg` works, `sendSEIMsg` directly inserts data into the video data header. Therefore, even if the video frames are relayed to LVB CDN, the data will always exist. As the data needs to be embedded in the video frames, it is recommended to keep the data size under several bytes.
The most common use is to embed the custom timestamp into video frames through `sendSEIMsg` so as to implement a perfect alignment between messages and video image.

>This API has the following restrictions:
>- The data will not be instantly sent after this API is called; instead, it will be inserted into the next video frame after the API call.
>- Up to 30 messages can be sent per second to all users in the room (this limit is shared with `sendCustomCmdMsg`).
>- Each packet can be up to 1 KB (this limit is shared with `sendCustomCmdMsg`). If a large amount of data is sent, the video bitrate will increase, which may reduce the video quality or even cause lagging.
>- Each client can send up to 8 KB of data in total per second (this limit is shared with `sendCustomCmdMsg`).
>- If multiple times of sending is required (i.e., `repeatCount` > 1), the data will be inserted into subsequent `repeatCount` video frames in a row for sending, which will increase the video bitrate.
>- If `repeatCount` is greater than 1, the data will be sent for multiple times, and the same message may be received multiple times in the `onRecvSEIMsg` callback; therefore, deduplication is required.



## Background Audio Mixing API Functions
### playBGM

This API is used to start background music.
```
- (void)playBGM:(NSString *)path withBeginNotify:(void(^)(NSInteger errCode))beginNotify withProgressNotify:(void(^)(NSInteger progressMS, NSInteger durationMS))progressNotify andCompleteNotify:(void(^)(NSInteger errCode))completeNotify 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | NSString * | Path to music file. |
| beginNotify | void(^)(NSInteger errCode) | Callback notification of the start of music playback. |
| progressNotify | void(^)(NSInteger progressMS, NSInteger durationMS) | Notification of music playback progress in milliseconds. |
| completeNotify | void(^)(NSInteger errCode) | Callback notification of the end of music playback. |


### stopBGM

This API is used to stop background music.
```
- (void)stopBGM
```


### pauseBGM

This API is used to pause background music.
```
- (void)pauseBGM
```


### resumeBGM

This API is used to resume background music.
```
- (void)resumeBGM
```


### getBGMDuration

This API is used to get the total length of the music file in milliseconds.
```
- (NSInteger)getBGMDuration:(NSString *)path 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | NSString * | Path to music file. If `path` is left empty, the length of the music file being played back will be returned. |

__Return__

The length will be returned if this API is successfully called; otherwise, `-1` will be returned.


### setBGMPosition

This API is used to set playback progress of background music.
```
- (int)setBGMPosition:(NSInteger)pos 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| pos | NSInteger | In milliseconds. |

__Return__

0: success; -1: failure.


### setMicVolumeOnMixing

This API is used to set mic volume level. This API is used to adjust the mic volume level when background music is played back.
```
- (void)setMicVolumeOnMixing:(NSInteger)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | NSInteger | Volume level. 100 indicates normal volume level. Value range: 0–100. |


### setBGMVolume

This API is used to set background music volume level. This API is used to control the background music volume level during playback.
```
- (void)setBGMVolume:(NSInteger)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | NSInteger | Volume level. 100 indicates normal volume level. Value range: 0–100. |


### setReverbType

This API is used to set reverb effect (currently, this is supported only for iOS).
```
- (void)setReverbType:(TRTCReverbType)reverbType 
```

__Parameters__


| Parameter | Type | Description |
|-----|-----|-----|
| reverbType | TXReverbType | Reverb type. For more information, please see [TRTCReverbType](https://intl.cloud.tencent.com/document/product/647/35123#trtcreverbtype). |


### setVoiceChangerType

This API is used to set voice changer type (currently, this is supported only for iOS).
```
- (void)setVoiceChangerType:(TRTCVoiceChangerType)voiceChangerType 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| voiceChangerType |TXVoiceChangerType | Voice changer type. For more information, please see [TRTCVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvoicechangertype). |

## Sound Effect API Functions
### playAudioEffect

This API is used to play back sound effect.
```
- (void)playAudioEffect:(TRTCAudioEffectParam *)effect 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effect | [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioeffectparam) * | Sound effect. |

__Overview__

You need to assign an ID to each sound effect, through which you can start, stop, or set the volume level of a sound effect. If you want to play back multiple sound effects at the same time, please assign different IDs to them. If you use the same ID for different sound effects, the SDK cannot play them back at the same time; instead, it will stop playing back the old sound effect and then start playing back the new one.


### setAudioEffectVolume

This API is used to set volume level of a single sound effect.
```
- (void)setAudioEffectVolume:(int)effectId volume:(int)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

>This operation will take precedence over the overall sound effect volume level specified in `setAllAudioEffectsVolume`.

### stopAudioEffect

This API is used to stop sound effect.
```
- (void)stopAudioEffect:(int)effectId 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |


### stopAllAudioEffects

This API is used to stop all sound effects.
```
- (void)stopAllAudioEffects
```


### setAllAudioEffectsVolume

This API is used to set volume level of all sound effects.
```
- (void)setAllAudioEffectsVolume:(int)volume 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

>The volume level set by this operation will take precedence over that of an individual sound effect specified in `setAudioEffectVolume`.

## Device and Network Test API Functions
### startSpeedTest

This API is used to start network speed test (do not test during a video call so as to avoid affecting the call quality).
```
- (void)startSpeedTest:(uint32_t)sdkAppId userId:(NSString *)userId userSig:(NSString *)userSig completion:(void(^)(TRTCSpeedTestResult *result, NSInteger completedCount, NSInteger totalCount))completion 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppId | uint32_t | Application ID. |
| userId | NSString * | User ID. |
| userSig | NSString * | User signature. |
| completion | void(^)([TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35123#trtcspeedtestresult) *result, NSInteger completedCount, NSInteger totalCount) | Test callback, which will be divided into multiple callbacks. |

__Overview__

The speed test result will be used to optimize the SDK's subsequent selection policy. It is recommended to perform the speed test before users place the first call, which will help select the optimal server. If the test result is not satisfactory, you can use a noticeable UI prompt to remind the user to select a better network.

>The speed test will consume a certain amount of traffic and generate a small amount of extra traffic fees as a result.



### stopSpeedTest

This API is used to stop server speed test.
```
- (void)stopSpeedTest
```


### startCameraDeviceTestInView

This API is used to start camera test.
```
- (void)startCameraDeviceTestInView:(NSView *)view 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| view | NSView * | Parent control of the preview control. |

>You can use the `setCurrentCameraDevice` API to switch cameras during the test.



### stopCameraDeviceTest

This API is used to stop video test preview.
```
- (void)stopCameraDeviceTest
```


### startMicDeviceTest

This API is used to start mic test.
```
- (void)startMicDeviceTest:(NSInteger)interval testEcho:(void(^)(NSInteger volume))testEcho 
```

__Overview__

This method is used to test whether the mic can function properly, and `volume` ranges from 0 to 100.


### stopMicDeviceTest

This API is used to stop mic test.
```
- (void)stopMicDeviceTest
```


### startSpeakerDeviceTest

This API is used to start speaker test.
```
- (void)startSpeakerDeviceTest:(NSString *)audioFilePath onVolumeChanged:(void(^)(NSInteger volume, BOOL isLastFrame))volumeBlock 
```

__Overview__

This method plays back the specified audio data to test whether the speaker can function properly. If sound can be heard, the speaker is normal.


### stopSpeakerDeviceTest

This API is used to stop speaker test.
```
- (void)stopSpeakerDeviceTest
```



## MixTranscoding and CDN Relayed Push
### setMixTranscodingConfig

This API is used to set On-Cloud MixTranscoding parameters.
```
- (void)setMixTranscodingConfig:(TRTCTranscodingConfig *)config 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| config | [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35123#trtctranscodingconfig) * | For more information, please see the description of [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35123#trtctranscodingconfig) in `TRTCCloudDef.h`. If `nil` is passed in, On-Cloud MixTranscoding will be canceled. |

__Overview__

This API will send a command to the Tencent Cloud transcoding server to combine multiple image channels in the room into one channel.
If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each image channel in the room will have a corresponding LVB [CDN address](https://intl.cloud.tencent.com/document/product/647/35242), and you can use On-Cloud MixTranscoding to mix multiple image channels from the LVB addresses to one channel and view the mixed image on LVB CDN.
You can use the transcoding parameters to set the position of each channel of image and quality of the final output image.
For more information, please see [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/35123/34618). 
Sample code: the demo provides the entry for trying out this feature. You can experience it in "On-Cloud Image Mix" and "Share Playback Address" in the "More Features" panel.


<pre>
**Image 1**=> decoding => =>
                        \
**Image 2**=> decoding =>  image mixing => encoding => **mixed image**
                        /
**Image 3**=> decoding => =>
</pre>


>Notes on On-Cloud MixTranscoding:
>- On-cloud transcoding will cause a delay of 1–2 seconds in video playback with CDN.
>- If you call this function, the multiple channels of images will be mixed to the [CDN address](https://intl.cloud.tencent.com/document/product/647/35242) of your own channel.


### startPublishCDNStream

This API is used to relay stream to the specified push address.
```
- (void)startPublishCDNStream:(TRTCPublishCDNParam *)param 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcpublishcdnparam) * | For more information, please see the description of [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcpublishcdnparam) in `TRTCCloudDef.h`. |

__Overview__

This API will push a command to Tencent Cloud's relay server, and Tencent Cloud will push the current channel of audio/video to your specified RTMP push address.
If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each channel of image in the room will have a default CDN address. Therefore, this feature is not commonly used and required only if you need to configure multiple CDN providers.
As relaying an individual channel of image to LVB CDN is generally meaningless, this feature is usually used with On-Cloud MixTranscoding, i.e., `setMixTranscodingConfig` is used to mix multiple image channels to one channel and then relay it.

>Notes on relayed push:
>- By default, audio/video streams can be relayed only to the Tencent Cloud RTMP [push address](https://intl.cloud.tencent.com/document/product/267/32480). To relay streams to other cloud services, please submit a ticket to contact us.
>- If you call this function, only your own channel of image will be relayed to the specified RTMP push address by default. Therefore, this API usually needs to be used together with `setMixTranscodingConfig`.
>- If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each channel of image in the room will have a default CDN address. Therefore, this feature is required only if you need to configure multiple CDN providers.

### stopPublishCDNStream

This API is used to stop relayed push.
```
- (void)stopPublishCDNStream
```



## Log API Functions
### getSDKVersion

This API is used to get SDK version information.
```
+ (NSString *)getSDKVersion
```


### setLogLevel

This API is used to set log output level.
```
+ (void)setLogLevel:(TRTCLogLevel)level 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35123#trtcloglevel) | For more information, please see `TRTCLogLevel`. Default value: TRTC_LOG_LEVEL_NULL. |


### setConsoleEnabled

This API is used to disable or enable console log printing.
```
+ (void)setConsoleEnabled:(BOOL)enabled 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enabled | BOOL | Specifies whether to enable it, which is disabled by default. |


### setLogCompressEnabled

This API is used to enable or disable local log compression.
```
+ (void)setLogCompressEnabled:(BOOL)enabled 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enabled | BOOL | Specifies whether to enable, which is enabled by default. |

__Overview__

If compression is enabled, the log size will significantly reduce, but logs can be read only after being decompressed by the Python script provided by Tencent Cloud. If compression is disabled, logs will be stored in plaintext and can be read directly in Notepad, but will take up more storage capacity.


### setLogDirPath

This API is used to modify log storage path.
```
+ (void)setLogDirPath:(NSString *)path 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | NSString * | Log storage path. |

>The log files are stored in `sandbox Documents/log` by default. To change the path, call this API before calling other methods.



### setLogDelegate

This API is used to set log callback.
```
+ (void)setLogDelegate:(id< TRTCLogDelegate >)logDelegate 
```


### showDebugView

This API is used to display dashboard.
```
- (void)showDebugView:(NSInteger)showType 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| showType | NSInteger | 0: does not display; 1: displays lite edition; 2: displays full edition. |

__Overview__

The dashboard is a floating view for status statistics and event notifications to facilitate debugging. 



### setDebugViewMargin

This API is used to set dashboard margin.
```
- (void)setDebugViewMargin:(NSString *)userId margin:(TXEdgeInsets)margin 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | NSString * | User ID. |
| margin | TXEdgeInsets | Inner margin of the dashboard. It should be noted that this is based on the percentage of `parentView`. Value range: 0–1. |

__Overview__

The settings can only take effect if set before `showDebugView` is called.


### callExperimentalAPI

This API is used to call experimental APIs.
```
- (void)callExperimentalAPI:(NSString *)jsonStr 
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| jsonStr | NSString * | JSON string of API and parameter descriptions. |

>This API is used to call some experimental APIs.
