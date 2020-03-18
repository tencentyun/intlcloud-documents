
TRTCCloud @ TXLiteAVSDK.

Main API class for the TRTC video call feature.


## Basic Methods
### sharedInstance

This API is used to create [TRTCCloud](#trtccloud) singleton.
```
TRTCCloud sharedInstance(Context context)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| context | Context | Android context, which will be converted to `ApplicationContext` for the system APIs to call. |

__Return__

[TRTCCloud](#trtccloud) instance.

>`destroySharedInstance` can be called to terminate a singleton object.


### destroySharedInstance

This API is used to terminate [TRTCCloud](#trtccloud) singleton.
```
void destroySharedInstance()
```


### setListener

This API is used to set the `TRTCCloudListener` callback API, through which users can get various status notifications from `[TRTCCloud](#trtccloud)`.
```
abstract void setListener(TRTCCloudListener listener)
```

__Overview__

You can use [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) to get various status notifications from the SDK. For more information, please see the definitions in [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener).


### setListenerHandler

This API is used to set the queue that drives the [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) callback.
```
abstract void setListenerHandler(Handler listenerHandler)
```

__Overview__

The SDK uses the main thread as the driver of `TRTCCloudListener` by default, which means, if you do not specify `listenerHandler`, the [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) callback of the SDK will be called by the main thread. Your operation on UI in the callback function of [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) is thread-safe now.



## Room API Functions
### enterRoom

This API is used to enter room.
```
abstract void enterRoom(TRTCCloudDef.TRTCParams param, int scene)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCCloudDef.TRTCParams](https://intl.cloud.tencent.com/document/product/647/35129#trtcparams) | Room entry parameters. For more information, please see `TRTCParams`. |
| scene | int | Application scenario. Currently, only video call (`VideoCall`) and LVB (`Live) scenarios are supported. |

__Overview__

After this API is called, the `onEnterRoom(result)` callback from [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) will be received: if room entry succeeded, `result` will be a positive number (`result` > 0), indicating the time in milliseconds (ms) used for entering the room; otherwise, `result` will be a negative number (`result` < 0), indicating the error code for room entry failure. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/647/35124).

>No matter whether room entry is successful, `enterRoom` must be used together with `exitRoom`. If `enterRoom` is called again before `exitRoom` is called, an unexpected error will occur.



### exitRoom

This API is used to exit room.
```
abstract void exitRoom()
```

__Overview__

When the [exitRoom()](#exitroom) API is called, the logic related to room exit will be executed, such as releasing resources of audio/video devices and codecs. After resources are released, the SDK will use the `onExitRoom()` callback in [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener) to notify you.
If you need to call [enterRoom()](#enterroom) again or switch to another audio/video SDK, please wait until you receive the `onExitRoom()` callback; otherwise, exceptions such as occupied camera or mic may occur; for example, the common issue with switching between media volume and call volume on Android is caused by this problem.


### switchRole

This API is used to switch roles and applies only to the LVB scenario (`TRTCAppSceneLIVE`).
```
abstract void switchRole(int role)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| role | int | Target role, which is anchor by default. |

__Overview__

In the LVB scenario, a user may need to switch between "viewer" and "anchor" roles. You can use the `role` field in `TRTCParams` before room entry to determine the role or use the `switchRole` API to switch roles after room entry.


### ConnectOtherRoom

This API is used to request cross-room call (anchor competition).
```
abstract void ConnectOtherRoom(String param)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | String | Co-anchoring parameters in the format of JSON string. `roomId` indicates the target room number, and `userId` indicates the target user ID. |

__Overview__

In TRTC, two anchors in different rooms can use the "cross-room call" feature to co-anchor across the rooms. They can engage in "co-anchoring competition" without the need to exit their own rooms.
For example, when anchor A in room "001" uses `connectOtherRoom()` to successfully call anchor B in room "002", all users in room "001" will receive the `onUserEnter(B)` and `onUserVideoAvailable(B,true)` callbacks of anchor B, and all users in room "002" will receive the `onUserEnter(A)` and `onUserVideoAvailable(A,true)` callbacks of anchor A.
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
- `roomId`: If anchor A in room "001" wants to co-anchor with anchor B in room "002", the `roomId` must be set to `002` when anchor A calls [ConnectOtherRoom()](#connectotherroom).
- `userId`: If anchor A in room "001" wants to co-anchor with anchor B in room "002", the `userId` must be set to the `userId` of anchor B when anchor A calls [ConnectOtherRoom()](#connectotherroom).


The result of requesting cross-room call will be returned through the `onConnectOtherRoom()` callback in [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener).


<pre>
  JSONObject jsonObj = new JSONObject();
  jsonObj.put("roomId"， 002);
  jsonObj.put("userId"， "userB");
  trtc.ConnectOtherRoom(jsonObj.toString());
</pre>


### DisconnectOtherRoom

This API is used to exit cross-room call.
```
abstract void DisconnectOtherRoom()
```

__Overview__

The result of exiting cross-room call will be returned through the `onDisconnectOtherRoom` callback in `TRTCCloudListener.java`.


### setDefaultStreamRecvMode

This API is used to set audio/video data reception mode, which must be set before room entry for it to take effect.
```
abstract void setDefaultStreamRecvMode(boolean autoRecvAudio, boolean autoRecvVideo)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| autoRecvAudio | boolean | true: audio data will be automatically received; false: `muteRemoteAudio` needs to be called to send or cancel a request. Default value: true. |
| autoRecvVideo | boolean | true: video data will be automatically received; false: `startRemoteView/stopRemoteView` needs to be called to send or cancel a request. Default value: true. |

__Overview__

To deliver an excellent instant broadcasting experience, the SDK automatically receives audio/video upon successful room entry by default, that is, you will immediately receive audio/video data from all remote users. If you do not call `startRemoteView`, video data will be automatically canceled due to timeout. If you use this API mainly in scenarios where automatic video data reception is not required, such as audio chat, you can select the reception mode based on your actual needs.

>This API takes effect only if it is set before room entry.




## Video API Functions
### startLocalPreview

This API is used to enable preview image of local video.
```
abstract void startLocalPreview(boolean frontCamera, TXCloudVideoView view)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frontCamera | boolean | true: front camera; false: rear camera. |
| view | TXCloudVideoView | Control that carries the video image. |

__Overview__

When the first video frame starts to be rendered, you will receive the `onFirstVideoFrame(null)` callback in [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/35127#trtccloudlistener).


### stopLocalPreview

This API is used to stop local video capture and preview.
```
abstract void stopLocalPreview()
```


### muteLocalVideo

This API is used to specify whether to block local video image.
```
abstract void muteLocalVideo(boolean mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | true: blocks; false: enables. Default value: false. |

__Overview__

After the local video is blocked, other members in the room will receive the `onUserVideoAvailable` callback notification.


### startRemoteView

This API is used to start displaying remote video image.
```
abstract void startRemoteView(String userId, TXCloudVideoView view)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |
| view | TXCloudVideoView | Control that carries the video image. |

__Overview__

If you receive the `onUserVideoAvailable(userId, true)` notification from the SDK, you can know that the remote user has enabled the video image. Later, when you use the `startRemoteView(userId)` API to load the remote image of this user, you can use a loading animation to optimize the experience for awaiting video loading. When the first video frame of this user starts to be displayed, you will receive the `onFirstVideoFrame(userId)` event callback.


### stopRemoteView

This API is used to stop displaying remote video image.
```
abstract void stopRemoteView(String userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |

__Overview__

After this API is called, the SDK will stop receiving the remote video stream of the specified user and clear relevant video displaying resources.


### stopAllRemoteView

This API is used to stop displaying all remote video images.
```
abstract void stopAllRemoteView()
```

>If there is a screen sharing image, it will be stopped together with other remote video images.



### muteRemoteVideoStream

This API is used to pause receiving the specified remote video stream.
```
abstract void muteRemoteVideoStream(String userId, boolean mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |
| mute | boolean | Whether to stop reception. |

__Overview__

This API only stops receiving remote user's video stream but does not release displaying resources; therefore, the video image will freeze at the last frame before the muting operation.


### muteAllRemoteVideoStreams

This API is used to stop receiving all remote video streams.
```
abstract void muteAllRemoteVideoStreams(boolean mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | Whether to stop reception. |


### setVideoEncoderParam

This API is used to set video encoder parameters.
```
abstract void setVideoEncoderParam(TRTCCloudDef.TRTCVideoEncParam param)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCCloudDef.TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoencparam) | Video encoding parameters. For more information, please see the definition of `TRTCVideoEncParam` in `TRTCCloudDef.java`. |

__Overview__

These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.


### setNetworkQosParam

This API is used to set network bandwidth limit parameters.
```
abstract void setNetworkQosParam(TRTCCloudDef.TRTCNetworkQosParam param)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCCloudDef.TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcnetworkqosparam) | Network bandwidth limit parameters. For more information, please see the definition of `TRTCNetworkQosParam` in `TRTCCloudDef.java`. |

__Overview__

The settings determine the bandwidth limit practices of the SDK in various network conditions (e.g., whether to "ensure definition" or "ensure smoothness" on a weak network).


### setLocalViewFillMode

This API is used to set rendering mode of local image.
```
abstract void setLocalViewFillMode(int mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mode | int | Fill (the image may be stretched or cropped) or fit (there may be black bars in unmatched areas). Default value: TRTC_VIDEO_RENDER_MODE_FILL. |


### setRemoteViewFillMode

This API is used to set rendering mode of remote image.
```
abstract void setRemoteViewFillMode(String userId, int mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| mode | int | Fill (the image may be stretched or cropped) or fit (there may be black bars in unmatched areas). Default value: TRTC_VIDEO_RENDER_MODE_FILL. |


### setLocalViewRotation

This API is used to set clockwise rotation angle of local image.
```
abstract void setLocalViewRotation(int rotation)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | int | Rotation angles of `TRTC_VIDEO_ROTATION_90`, `TRTC_VIDEO_ROTATION_180`, and `TRTC_VIDEO_ROTATION_270` are supported. Default value: TRTC_VIDEO_ROTATION_0. |


### setRemoteViewRotation

This API is used to set clockwise rotation angle of remote image.
```
abstract void setRemoteViewRotation(String userId, int rotation)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| rotation | int | Rotation angles of `TRTC_VIDEO_ROTATION_90`, `TRTC_VIDEO_ROTATION_180`, and `TRTC_VIDEO_ROTATION_270` are supported. Default value: TRTC_VIDEO_ROTATION_0. |


### setVideoEncoderRotation

This API is used to set direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server).
```
abstract void setVideoEncoderRotation(int rotation)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | int | Rotation angles of `TRTC_VIDEO_ROTATION_0` and `TRTC_VIDEO_ROTATION_180` are supported. Default value: TRTC_VIDEO_ROTATION_0. |

__Overview__

When a phone or Android tablet is rotated 180 degrees, as the capture direction of the camera does not change, the video image viewed by remote users will be upside-down. In this case, you can call this API to rotate the image output by the SDK to remote users 180 degrees, so that remote users can view the normal image.


### setLocalViewMirror

This API is used to set mirror mode of local camera's preview image.
```
abstract void setLocalViewMirror(int mirrorType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirrorType | int | mirrorType. TRTC_VIDEO_MIRROR_TYPE_AUTO: the SDK determines the mirror mode: mirrors the front camera's image but does not mirror the rear camera's image. TRTC_VIDEO_MIRROR_TYPE_ENABLE: mirrors the images of both the front and rear cameras. TRTC_VIDEO_MIRROR_TYPE_DISABLE: does not mirror the images of both the front and rear cameras. Default value: TRTC_VIDEO_MIRROR_TYPE_AUTO. |


### setVideoEncoderMirror

This API is used to set mirror mode of image output by encoder.
```
abstract void setVideoEncoderMirror(boolean mirror)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | boolean | true: mirrors; false: does not mirror. Default value: false. |

__Overview__

This API does not change the preview image of the local camera; instead, it changes the video image viewed by the remote user (and recorded by the server).


### setGSensorMode

This API is used to set adaptation mode of the g-sensor.
```
abstract void setGSensorMode(int mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mode | int | G-sensor mode. For more information, please see the definition of `TRTC_GSENSOR_MODE`. Default value: TRTC_GSENSOR_MODE_UIFIXLAYOUT. |


### enableEncSmallVideoStream

This API is used to enable dual-channel encoding mode with big and small images.
```
abstract int enableEncSmallVideoStream(boolean enable, TRTCCloudDef.TRTCVideoEncParam smallVideoEncParam)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | boolean | Whether to enable small image encoding. Default value: `false`. |
| smallVideoEncParam | [TRTCCloudDef.TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoencparam) | Video parameters of small image stream. |

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
abstract int setRemoteVideoStreamType(String userId, int streamType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| streamType | int | Video stream type, i.e., big image or small image. Default value: big image. |

__Overview__

To implement this feature, the dual-channel encoding mode must be enabled by the `uid` through `enableEncSmallVideoStream`; otherwise, this operation will not take effect.


### setPriorRemoteVideoStreamType

This API is used to set the video quality preferred by viewers.
```
abstract int setPriorRemoteVideoStreamType(int streamType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| streamType | int | Selects whether to watch big image or small image. Default value: big image. |

__Overview__

It is recommended to select the LD small image for low-spec devices first. If the dual-channel encoding mode is not enabled, this operation will not take effect.



## Audio API Functions
### startLocalAudio

This API is used to enable local audio capture and upstreaming.
```
abstract void startLocalAudio()
```

__Overview__

This function will start mic capture and transmit audio data to other users in the room.
The SDK does not enable local audio capture and upstreaming by default, and you need to call this function to enable it; otherwise, other users in the room cannot hear you.

>This function will check the mic permission. If the current application does not have permission to use the mic, the SDK will ask the user to grant the permission.



### stopLocalAudio

This API is used to disable local audio capture and upstreaming.
```
abstract void stopLocalAudio()
```

__Overview__

When local audio capture and upstreaming is disabled, other members in the room will receive the `onUserAudioAvailable(false)` callback notification.


### muteLocalAudio

This API is used to mute local audio.
```
abstract void muteLocalAudio(boolean mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | true: blocks; false: enables. Default value: false. |

__Overview__

After local audio is muted, other members in the room will receive the `onUserAudioAvailable(false)` callback notification.
Different from `stopLocalAudio`, `muteLocalAudio` will not stop sending audio/video data; instead, it continues to send mute packets of an extremely low bitrate. Since some video file formats such as MP4 have a high requirement for audio continuity, an MP4 recording file cannot be played back smoothly if `stopLocalAudio` is used. Therefore, `muteLocalAudio` is recommended in scenarios where the requirement for recording quality is high, so as to record MP4 files with better compatibility.

### setAudioRoute

This API is used to set audio routing.
```
abstract void setAudioRoute(int route)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| route | int | Audio routing, i.e., whether the audio is output by speaker or receiver. For more information, please see [TRTCCloudDef.TRTC_AUDIO_ROUTE_SPEAKER](https://intl.cloud.tencent.com/document/product/647/35129#TRTC_AUDIO_ROUTE). Default value: TRTC_AUDIO_ROUTE_SPEAKER. |

__Overview__

The hands-free mode of video call features in WeChat and Mobile QQ is implemented based on audio routing. Generally, a mobile phone has two speakers, one is the receiver at the top with low volume, and the other is the stereo speaker at the bottom with high volume. The purpose of setting audio routing is to determine which speaker will be used.


### muteRemoteAudio

This API is used to mute the specified user's audio.
```
abstract void muteRemoteAudio(String userId, boolean mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |
| mute | boolean | true: muted; false: not muted. |


### muteAllRemoteAudio

This API is used to mute all users' audio.
```
abstract void muteAllRemoteAudio(boolean mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | boolean | true: muted; false: not muted. |


### enableAudioVolumeEvaluation

This API is used to enable volume reminder.
```
abstract void enableAudioVolumeEvaluation(int intervalMs)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| intervalMs | int | Determines the interval in ms for triggering the `onUserVoiceVolume` callback. The minimum interval is 100 ms. If the value is smaller than 0, the callback will be disabled. It is recommended to set this parameter to 300 ms. For detailed callback rules, please see the description of `onUserVoiceVolume`. |

__Overview__

After this feature is enabled, the evaluation result of the volume level will be obtained in `onUserVoiceVolume`. To enable this feature, call this API before calling [startLocalAudio()](#startlocalaudio).

>The volume bar in the demo is implemented based on this API.

### startAudioRecording

This API is used to start audio recording.
```
abstract int startAudioRecording(TRTCCloudDef.TRTCAudioRecordingParams TRTCAudioRecordingParams)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| TRTCAudioRecordingParams | [TRTCCloudDef.TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudiorecordingparams) | Audio recording parameters. For more information, please see `TRTCAudioRecordingParams`. |

__Return__

0: success; -1: audio recording has been started; -2: failed to create file or directory; -3: the audio format of the specified file extension is not supported.

__Overview__

After this API is called, the SDK will record all audios (such as local audio, remote audio, and background music) in the current call to a file. No matter whether room entry is performed, this API will take effect once called. If audio recording is still ongoing when `exitRoom` is called, it will stop automatically.


### stopAudioRecording

This API is used to stop audio recording.
```
abstract void stopAudioRecording()
```

__Overview__

If audio recording is still ongoing when `exitRoom` is called, it will stop automatically.


### setSystemVolumeType

This API is used to set the system volume type used in call.
```
abstract void setSystemVolumeType(int type)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| type | int | System volume type. For more information, please see [TRTCSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35129#TRTCSystemVolumeType). Default value: TRTCSystemVolumeTypeAuto. |

>This API must be called before [startLocalAudio()](#startlocalaudio) is called.



### enableAudioEarMonitoring

This API is used to enable in-ear monitoring.
```
abstract void enableAudioEarMonitoring(boolean enable)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | boolean | true: enables; false: disables. |

__Overview__

After in-ear monitoring is enabled, the local user can hear their own voice.

>This API takes effect only if the user wears headphones.



## Camera API Functions
### switchCamera

This API is used to switch cameras.

```
abstract void switchCamera()
```


### isCameraZoomSupported

This API is used to query whether the current camera supports zoom.
```
abstract boolean isCameraZoomSupported()
```


### setZoom

This API is used to set zoom factor (focal length) of camera.
```
abstract void setZoom(int distance)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| distance | int | Value range: 1–5. The greater the value, the further the focal length. |

__Overview__

The value range is 1–5. 1 indicates the furthest view (normal lens), and 5 indicates the nearest view (enlarging lens).
It is recommended to set the maximum value to 5. If the maximum value is greater than 5, the video will become blurry.


### isCameraTorchSupported

This API is used to query whether the device supports flash (flash mode).
```
abstract boolean isCameraTorchSupported()
```


### enableTorch

This API is used to enable or disable flash.
```
abstract boolean enableTorch(boolean enable)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | boolean | true: enables; false: disables. Default value: false. |


### isCameraFocusPositionInPreviewSupported

This API is used to query whether the device supports setting focus.
```
abstract boolean isCameraFocusPositionInPreviewSupported()
```


### setFocusPosition

This API is used to set camera focus.
```
abstract void setFocusPosition(int x, int y)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| x | int | X coordinate of the focus position. |
| y | int | Y coordinate of the focus position. |


### isCameraAutoFocusFaceModeSupported

This API is used to query whether the device supports automatic recognition of face position.
```
abstract boolean isCameraAutoFocusFaceModeSupported()
```



## Beauty Filter API Functions
### getBeautyManager

This API is used to get the beauty filter management object.
```
abstract TXBeautyManager getBeautyManager()
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
abstract void setBeautyStyle(int beautyStyle, int beautyLevel, int whitenessLevel, int ruddinessLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| beautyStyle | int | Beauty filter style: smooth or natural. The smooth style has more obvious skin smoothing effect and is suitable for entertaining scenarios. |
| beautyLevel | int | Effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |
| whitenessLevel | int | Effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |
| ruddinessLevel | int | Effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |

__Overview__

The SDK is integrated with two skin smoothing algorithms of different styles. One is called "smooth" and is suitable for shows as its effect is more obvious. The other is called "natural", which retains more facial details and seems more natural subjectively.


### setFilter

This API is used to specify material filter effect.
```
abstract void setFilter(Bitmap image)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| image | Bitmap | Specified material, i.e., color lookup table. **The material must be in PNG format.** |


### setFilterConcentration

This API is used to set effect level of a filter.
```
abstract void setFilterConcentration(float concentration)
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
abstract void setWatermark(Bitmap image, int streamType, float x, float y, float width)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| image | Bitmap | Watermark image, **which must be a PNG image with transparent background.** |
| streamType | int | `setWatermark` needs to be called twice if the screen sharing channel also requires a watermark. |
| x | float | Unified X coordinate of the watermark position. Value range: [0,1]. |
| y | float | Unified Y coordinate of the watermark position. Value range: [0,1]. |
| width | float | Unified width of the watermark. Value range: [0,1]. |

__Overview__

The watermark position is determined by the `x`, `y`, and `width` parameters.
- x: X coordinate of watermark, which is a floating point number between 0 and 1.
- y: Y coordinate of watermark, which is a floating point number between 0 and 1.
- width: width of watermark, which is a floating point number between 0 and 1.


For example, if the current encoding resolution is 540 * 960 and `(x, y, width)` is set to (0.1, 0.1, 0.2), then the coordinates of the top-left point of the watermark will be (540 * 0.1, 960 * 0.1), i.e., (54, 96), the watermark width will be 540 * 0.2 = 108 px, and the height will be calculated automatically.


### setEyeScaleLevel

This API is used to set effect level of the eye enlarging filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setEyeScaleLevel(int eyeScaleLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| eyeScaleLevel | int | Effect level of the eye enlarging filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setFaceSlimLevel

This API is used to set effect level of the face slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setFaceSlimLevel(int faceScaleLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceScaleLevel | int | Effect level of the face slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setFaceVLevel

This API is used to set effect level of the chin slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setFaceVLevel(int faceVLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceVLevel | int | Effect level of the chin slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setFaceShortLevel

This API is used to set effect level of the face shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setFaceShortLevel(int faceShortlevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| faceShortlevel | int | Effect level of the face shortening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setChinLevel

This API is used to set effect level of the chin lengthening/shortening or shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setChinLevel(int chinLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| chinLevel | int | Effect level of the chin lengthening/shortening filter. Value range: -9–9; 0 indicates that the filter is disabled, a value smaller than 0 indicates that the chin is shortened, while a value greater than 0 indicates that the chin is lengthened. |


### setNoseSlimLevel

This API is used to set effect level of the nose slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setNoseSlimLevel(int noseSlimLevel)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| noseSlimLevel | int | Effect level of the nose slimming filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |


### setGreenScreenFile

This API is used to set green screen video (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract boolean setGreenScreenFile(String file)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| file | String | Path to the video file, which can be in MP4 format. null: disables the effect. |

__Overview__

The green screen feature here is not intelligent keying. It requires that there be a green screen behind the videoed person or object for further chroma keying.


### selectMotionTmpl

This API is used to select AI animated effect pendant (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void selectMotionTmpl(String motionPath)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionPath | String | Full path to the animated effect. |


### setMotionMute

This API is used to mute animated effect (it takes effect only in TRTC Commercial edition and is invalid in other editions).
```
abstract void setMotionMute(boolean motionMute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| motionMute | boolean | true: muted; false: unmuted. |

__Overview__

Some animated effects have audio effects, which can be disabled through this API when they are played back.



## Secondary Stream API Functions
### startRemoteSubStreamView

This API is used to start displaying screen sharing image of a remote user.
```
abstract void startRemoteSubStreamView(String userId, TXCloudVideoView view)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |
| view | TXCloudVideoView | Rendering control. |

__Overview__

Different from [startRemoteView()](#startremoteview) that is used to display the primary image, this API can only be used to display the image of the secondary channel (e.g., screen sharing and remote video playback).

>This API must be called after `onUserSubStreamAvailable` is called back.



### stopRemoteSubStreamView

This API is used to stop displaying screen sharing image of a remote user.
```
abstract void stopRemoteSubStreamView(String userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |


### setRemoteSubStreamViewFillMode

This API is used to set display mode of screen sharing image.
```
abstract void setRemoteSubStreamViewFillMode(String userId, int mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| mode | int | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). Default value: TRTC_VIDEO_RENDER_MODE_FIT. |

__Overview__

Different from [setRemoteViewFillMode()](#setremoteviewfillmode) that is used to set the display mode of primary image, this API can be used to set the remote image of the secondary channel (e.g., screen sharing and remote video playback).



## Custom Capture and Rendering API Functions
### enableCustomVideoCapture

This API is used to enable custom video capture mode.
```
abstract void enableCustomVideoCapture(boolean enable)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | boolean | Whether to enable. true: yes; false: no. Default value: false. |

__Overview__

After the custom mode is enabled, the SDK will not run the original video capture process and retain only the encoding and sending capabilities. You need to use [sendCustomVideoData()](#sendcustomvideodata) to continuously insert the captured video image into the SDK.


### sendCustomVideoData

This API is used to deliver the captured video data to the SDK.
```
abstract void sendCustomVideoData(TRTCCloudDef.TRTCVideoFrame frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | [TRTCCloudDef.TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35129#trtcvideoframe) | Video data. If the `buffer` scheme is used, please set the `data` field; if the `texture` scheme is used, please set the `TRTCTexture` object. |

__Overview__

Android supports two schemes:
- `buffer` scheme: its connection is easy but its performance is poor, so it is not suitable for scenarios with high resolution.
- `texture` scheme: its connection requires certain knowledge in OpenGL but its performance is well. For resolution higher than 640 * 360, please use this scheme.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35123/35158).

>
>- The SDK has an internal frame rate control logic, and the target frame rate set in `setVideoEncoderParam` shall prevail. If the frame rate is too high, automatic frame discarding may occur; if too low, automatic frame interpolation will be implemented.
>- It is recommended to set `timestamp` in `frame` to 0, so that the SDK will set the timestamp by itself. However, please "evenly" set the calling interval of `sendCustomVideoData`; otherwise, the video frame rate will be unstable.


### setLocalVideoRenderListener

This API is used to set callback of custom rendering for local video.
```
abstract int setLocalVideoRenderListener(int pixelFormat, int bufferType, TRTCCloudListener.TRTCVideoRenderListener listener)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| pixelFormat | int | Specifies the pixel format of video frame, such as TRTC_VIDEO_PIXEL_FORMAT_I420 or TRTC_VIDEO_PIXEL_FORMAT_Texture_2D. |
| bufferType | int | Specifies the data structure of video frame. `TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER` or `TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY` corresponds to `pixelFormat` of `TRTC_VIDEO_PIXEL_FORMAT_I420`; `TRTC_VIDEO_BUFFER_TYPE_TEXTURE` corresponds to `pixelFormat` of `TRTC_VIDEO_PIXEL_FORMAT_Texture_2D`. |
| listener | [TRTCCloudListener.TRTCVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcvideorenderlistener) | Callback of custom video rendering. The callback is returned once for each video frame. |

__Return__

0: success; values smaller than 0: error.

__Overview__

After this method is set, the SDK will skip its own rendering process and call back the captured data. Therefore, you need to complete image rendering on your own.
- `pixelFormat` specifies the format of the called back data. Currently, Texture2D and I420 are supported.
- `bufferType` specifies the buffer type. `BYTE_BUFFER` is suitable for the JNI layer, while `BYTE_ARRAY` can be used in direct operations at the Java layer.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35123/35158).


### setRemoteVideoRenderListener

This API is used to set callback of custom rendering for remote video.
```
abstract int setRemoteVideoRenderListener(String userId, int pixelFormat, int bufferType, TRTCCloudListener.TRTCVideoRenderListener listener)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | ID of remote user. |
| pixelFormat | int | Specifies the pixel format of video frame. Currently, only `TRTC_VIDEO_PIXEL_FORMAT_I420` is supported. |
| bufferType | int | Specifies the data structure of video frame, such as `TRTC_VIDEO_BUFFER_TYPE_BYTE_BUFFER` or `TRTC_VIDEO_BUFFER_TYPE_BYTE_ARRAY`. |
| listener | [TRTCCloudListener.TRTCVideoRenderListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcvideorenderlistener) | Callback of custom video rendering. The callback is returned once for each video frame. |

__Return__

0: success; values smaller than 0: error.

__Overview__

This method is similar to `setLocalVideoRenderListener`. The difference is that one is callback of rendering the local image, while the other is callback of rendering the remote image.
For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35123/35158).

>In practice, `startRemoteView(userid, null)` needs to be called first to initiate pull of the remote video stream, and `view` needs to be set to `null`; otherwise, the SDK will not start the custom rendering process, and the callback function of `listener` will not be triggered.



### enableCustomAudioCapture

This API is used to enable custom audio capture mode.
```
abstract void enableCustomAudioCapture(boolean enable)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | boolean | Whether to enable. true: yes; false: no. Default value: false. |

__Overview__

After the custom mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](#sendcustomaudiodata) to continuously insert the captured audio data into the SDK.


### sendCustomAudioData

This API is used to deliver the captured audio data to the SDK.
```
abstract void sendCustomAudioData(TRTCCloudDef.TRTCAudioFrame frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | [TRTCCloudDef.TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudioframe) | Audio frame. Currently, only mono channel and 48 kHz sample rate are supported. |

__Overview__

It is recommended to enter the following information for `TRTCAudioFrame`:
- data: audio frame buffer. Audio frame data must be in PCM format, and it is recommended to set sampling time to 20 ms for each frame. **For example, if the sample rate is 48000, then the frame length for mono channel will be `48000 * 0.02s * 1 * 16 bit = 15360 bit = 1920 bytes`.**
- sampleRate: sample rate. Currently, only 48000 is supported.
- channel: number of channels (if stereo is used, data is interwoven). Valid values: 1: mono channel; 2: dual channel.
- timestamp: if the intervals for `timestamp` are uneven, the audio/video sync and quality of MP4 recording will be seriously affected.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35123/35158).

>You can set `timestamp` in `frame` to `0`, so that the SDK will set the timestamp by itself. However, please "evenly" set the calling interval of `sendCustomAudioData`; otherwise, the audio will be unstable.



### setAudioFrameListener

This API is used to set audio data callback.
```
abstract void setAudioFrameListener(TRTCCloudListener.TRTCAudioFrameListener listener)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| listener | [TRTCCloudListener.TRTCAudioFrameListener](https://intl.cloud.tencent.com/document/product/647/35127#trtcaudioframelistener) | Audio data callback. If `listener = null`, data callback will be stopped. |

__Overview__

After this method is set, the SDK will internally call back the audio data (in PCM format), including:
- onCapturedAudioFrame: audio data captured by current mic
- onPlayAudioFrame: audio data from each remote user before audio mixing
- onMixedPlayAudioFrame: audio data to be played back by speaker after audio data from each channel is mixed



## Custom Message Sending API Functions
### sendCustomCmdMsg

This API is used to send custom message to all users in the room.
```
abstract boolean sendCustomCmdMsg(int cmdID, byte[] data, boolean reliable, boolean ordered)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| cmdID | int | Message ID. Value range: 1–10. |
| data | byte[] | Message to be sent, which can contain up to 1 KB (1,000 bytes) of data. |
| reliable | boolean | Whether reliable sending is enabled; if yes, the recipient needs to temporarily store the data of a certain period to wait for re-sending, which will cause certain delay. |
| ordered | boolean | Whether orderly sending is enabled, i.e., whether the data should be received in the same order in which it is sent; if yes, the recipient needs to temporarily store and sort messages, which will cause certain delay. |

__Return__

true: message has been sent successful; false: failed to send message.

__Overview__

This API can be used to broadcast your custom data to other users in the room though the audio/video data channel. Due to reuse of this channel, please strictly control the frequency of sending custom messages and message size; otherwise, the quality control logic of the audio/video data will be affected, causing uncertain issues.

>This API has the following restrictions:
>- Up to 30 messages can be sent per second to all users in the room.
>- A packet can contain up to 1 KB of data; if the threshold is exceeded, the packet is very likely to be discarded by the intermediate router or server.
>- A client can send up to 8 KB of data in total per second.
>- `reliable` and `ordered` must be set to the same value (`true` or `false`) and cannot be set to different values currently.
>- You are strongly recommended to use different `cmdIDs` for messages of different types. This can reduce message delay when orderly sending is required.


### sendSEIMsg

This API is used to embed custom data of a small size in video frames.
```
abstract boolean sendSEIMsg(byte[] data, int repeatCount)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| data | byte[] | Data to be sent, which can be up to 1 KB (1,000 bytes). |
| repeatCount | int | Data sending count. |

__Return__

true: the message is allowed and will be sent to subsequent video frames; false: the message is not allowed to be sent.

__Overview__

Different from how `sendCustomCmdMsg` works, `sendSEIMsg` directly inserts data into the video data header. Therefore, even if the video frames are relayed to LVB CDN, the data will always exist. As the data needs to be embedded in the video frames, it is recommended to keep the data size under several bytes.
The most common use is to embed the custom timestamp into video frames through `sendSEIMsg`. The biggest benefit of this scheme is that it can implement a perfect alignment between messages and video image.

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
abstract void playBGM(String path, BGMNotify notify)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | String | Path to music file. |
| notify | [BGMNotify](#.E6.92.AD.E6.94.BE.E8.83.8C.E6.99.AF.E9.9F.B3.E4.B9.90.E7.9A.84.E5.9B.9E.E8.B0.83.E6.8E.A5.E5.8F.A3) | Callback of background music playback. |


### stopBGM

This API is used to stop background music.
```
abstract void stopBGM()
```


### pauseBGM

This API is used to pause background music.
```
abstract void pauseBGM()
```


### resumeBGM

This API is used to resume background music.
```
abstract void resumeBGM()
```


### getBGMDuration

This API is used to get the total length of the music file in milliseconds.
```
abstract int getBGMDuration(String path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | String | Path to music file. If `path` is left empty, the length of the music file being played back will be returned. |

__Return__

The length will be returned if this API is successfully called; otherwise, `-1` will be returned.

### setBGMPosition

This API is used to set playback progress of background music.

```
abstract int setBGMPosition(int pos)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| pos | int | In milliseconds. |

__Return__

0: success; -1: failure.


### setMicVolumeOnMixing

This API is used to set mic volume level. This API is used to adjust the mic volume level when background music is played back.
```
abstract void setMicVolumeOnMixing(int volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. 100 indicates normal volume level. Value range: 0–100. |


### setBGMVolume

This API is used to set background music volume level. This API is used to control the background music volume level during playback.
```
abstract void setBGMVolume(int volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. 100 indicates normal volume level. Value range: 0–100. |


### setReverbType

This API is used to set reverb effect.
```
abstract void setReverbType(int reverbType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| reverbType | int | Reverb type. For more information, please see `TRTC_REVERB_TYPE`. Default value: TRTC_REVERB_TYPE_0. |


### setVoiceChangerType

This API is used to set voice changer type.
```
abstract boolean setVoiceChangerType(int voiceChangerType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| voiceChangerType | int | Voice changer type. For more information, please see `TRTC_VOICE_CHANGER_TYPE`. Default value: TRTC_VOICE_CHANGER_TYPE_0. |



## Sound Effect API Functions
### playAudioEffect

This API is used to play back sound effect.
```
abstract void playAudioEffect(TRTCCloudDef.TRTCAudioEffectParam effect)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effect | [TRTCCloudDef.TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcaudioeffectparam) | Sound effect. |

__Overview__

You need to assign an ID to each sound effect, through which you can start, stop, or set the volume level of a sound effect.

>If you want to play back multiple sound effects at the same time, please assign different IDs to them. If you use the same ID for different sound effects, the SDK cannot play them back at the same time; instead, it will stop playing back the old sound effect and then start playing back the new one.


### setAudioEffectVolume

This API is used to set sound effect volume level.
```
abstract void setAudioEffectVolume(int effectId, int volume)
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
abstract void stopAudioEffect(int effectId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |


### stopAllAudioEffects

This API is used to stop all sound effects.
```
abstract void stopAllAudioEffects()
```


### setAllAudioEffectsVolume

This API is used to set volume level of all sound effects.
```
abstract void setAllAudioEffectsVolume(int volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

>The volume level set by this operation will take precedence over that of an individual sound effect specified in `setAudioEffectVolume`.

## Network Test
### startSpeedTest

This API is used to start network speed test (do not test during a video call so as to avoid affecting the call quality).
```
abstract void startSpeedTest(int sdkAppId, String userId, String userSig)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppId | int | Application ID. |
| userId | String | User ID. |
| userSig | String | User signature. |

__Overview__

The speed test result will be used to optimize the SDK's subsequent selection policy. It is recommended to perform the speed test before users place the first call, which will help select the optimal server. If the test result is not satisfactory, you can use a noticeable UI prompt to remind the user to select a better network. The test result will be called back through [TRTCCloudListener.onSpeedTest](https://intl.cloud.tencent.com/document/product/647/35127#onspeedtest).

>The speed test will consume a certain amount of traffic and generate a small amount of extra traffic fees as a result.



### stopSpeedTest

This API is used to stop server speed test.
```
abstract void stopSpeedTest()
```



## MixTranscoding and Release to CDN
### setMixTranscodingConfig

This API is used to set On-Cloud MixTranscoding parameters.
```
abstract void setMixTranscodingConfig(TRTCCloudDef.TRTCTranscodingConfig config)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| config | [TRTCCloudDef.TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35129#trtctranscodingconfig) | For more information, please see the description of `TRTCTranscodingConfig` in `TRTCCloudDef.java`. If `null` is passed in, On-Cloud MixTranscoding will be canceled. |

__Overview__

This API will send a command to the Tencent Cloud transcoding server to combine multiple image channels in the room into one channel.
If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each image channel in the room will have a corresponding LVB [CDN address](https://intl.cloud.tencent.com/document/product/647/35123/34617), and you can use On-Cloud MixTranscoding to mix multiple image channels from the LVB addresses to one channel and view the mixed image on LVB CDN.
You can use the transcoding parameters to set the position of each channel of image and quality of the final output image.
Reference document: [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/35123/34618). Sample code: the demo provides the entry for trying out this feature. You can experience it in "On-Cloud Image Mix" and "Share Playback Address" in the "More Features" panel.


<pre>
**Image 1**=> decoding => =>
                        \
**Image 2**=> decoding =>  image mixing => encoding => **mixed image**
                        /
**Image 3**=> decoding => =>
</pre>

>Notes on On-Cloud MixTranscoding:
>- On-cloud transcoding will cause a delay of 1–2 seconds in video playback with CDN.
>- If you call this function, the multiple channels of images will be mixed to the [CDN address](https://intl.cloud.tencent.com/document/product/647/35123/34617) of your own channel.


### startPublishCDNStream

This API is used to relay stream to the specified push address.
```
abstract void startPublishCDNStream(TRTCCloudDef.TRTCPublishCDNParam param)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | [TRTCCloudDef.TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35129#trtcpublishcdnparam) | For more information, please see the description of `TRTCPublishCDNParam` in `TRTCCloudDef.java`. |

__Overview__

This API will push a command to Tencent Cloud's relay server, and Tencent Cloud will push the current channel of audio/video to your specified RTMP push address.
If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each channel of image in the room will have a default CDN address. Therefore, this feature is not commonly used and required only if you need to configure multiple CDN providers.
As relaying an individual channel of image to LVB CDN is generally meaningless, this feature is usually used with On-Cloud MixTranscoding, i.e., `setMixTranscodingConfig` is used to mix multiple image channels to one channel and then relay it.

>Notes on relayed push:
>- By default, audio/video streams can be relayed only to the Tencent Cloud RTMP [push address](https://intl.cloud.tencent.com/document/product/267/32720). To relay streams to other cloud services, please submit a ticket to contact us.
>- If you call this function, only your own channel of image will be relayed to the specified RTMP push address. Therefore, this API usually needs to be used together with `setMixTranscodingConfig`.
>- In TRTC, each channel of image in the room will have a default CDN address (which needs to be enabled). Therefore, this feature is not commonly used and required only if you need to configure multiple CDN providers.


### stopPublishCDNStream

This API is used to stop relayed push.
```
abstract void stopPublishCDNStream()
```



## Log API Functions
### getSDKVersion

This API is used to get SDK version information.
```
String getSDKVersion()
```


### setLogLevel

This API is used to set log output level.
```
void setLogLevel(int level)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | int | For more information, please see [TRTC_LOG_LEVEL](https://intl.cloud.tencent.com/document/product/647/35129#4.2-log-.E7.BA.A7.E5.88.AB). Default value: TRTC_LOG_LEVEL_NULL. |


### setConsoleEnabled

This API is used to disable or enable console log printing.
```
void setConsoleEnabled(boolean enabled)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enabled | boolean | Specifies whether to enable it, which is disabled by default. |


### setLogCompressEnabled

This API is used to enable or disable local log compression.
```
void setLogCompressEnabled(boolean enabled)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enabled | boolean | Specifies whether to enable it, which is enabled by default. |

__Overview__

If compression is enabled, the log size will significantly reduce, but logs can be read only after being decompressed by the Python script provided by Tencent Cloud. If compression is disabled, logs will be stored in plaintext and can be read directly in Notepad, but will take up more storage capacity.


### setLogDirPath

This API is used to modify log storage path.
```
void setLogDirPath(String path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | String | Log storage path. |

>The log files are stored in `/sdcard/Android/data/application package name/files/log/tencent/liteav/` by default. To change the path, call this API before calling other methods and make sure that the directory exists and the application has read/write access to the directory.



### setLogListener

This API is used to set log callback.
```
void setLogListener(final TRTCCloudListener.TRTCLogListener logListener)
```


### showDebugView

This API is used to display dashboard.
```
abstract void showDebugView(int showType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| showType | int | 0: does not display; 1: displays lite edition; 2: displays full edition. Default value: 0. |

__Overview__

The dashboard is a floating view for status statistics and event notifications to facilitate debugging.


### setDebugViewMargin

This API is used to set dashboard margin.
```
abstract void setDebugViewMargin(String userId, TRTCViewMargin margin)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | String | User ID. |
| margin | [TRTCViewMargin](#.E8.A7.86.E5.9B.BE.E8.BE.B9.E8.B7.9D) | Inner margin of the dashboard, which is based on the percentage of `parentView`. Value range: 0–1. |

__Overview__

The settings can only take effect if set before `showDebugView` is called.


### callExperimentalAPI

This API is used to call experimental APIs.
```
abstract void callExperimentalAPI(String jsonStr)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| jsonStr | String | JSON string of API and parameter descriptions. |

>This API is used to call some experimental APIs.



## Callback APIs of Background Music Playback

__Relevant class__

`TRTCCloud.BGMNotify`



### onBGMStart

Callback notification of music playback start.
```
void onBGMStart(int errCode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| errCode | int | 0: success; -1: failure. |


### onBGMProgress

Callback notification of music playback progress.
```
void onBGMProgress(long progress, long duration)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| progress | long | Elapsed time of the current background music playback in ms. |
| duration | long | Total time of background music in ms. |


### onBGMComplete

Callback notification of music playback end.
```
void onBGMComplete(int err)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| err | int | 0: ended normally; -1: ended exceptionally. |



## View Margin

__Relevant class__

`TRTCCloud.TRTCViewMargin`



### Attribute list

__Attribute list__

| Attribute | Type | Description |
|-----|-----|-----|
| leftMargin | float | Percentage of the margin to the left. Value range: 0–1. |
| topMargin | float | Percentage of the margin to the top. Value range: 0–1. |
| rightMargin | float | Percentage of the margin to the right. Value range: 0–1. |
| bottomMargin | float | Percentage of the margin to the bottom. Value range: 0–1. |




