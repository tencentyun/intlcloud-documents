
ITRTCCloud @ TXLiteAVSDK

## Creating and Terminating an ITRTCCloud Singleton

### getTRTCShareInstance

This API is used to get [ITRTCCloud](https://intl.cloud.tencent.com/document/product/647/35132#itrtccloud) object pointer in dynamic DLL loading.
```
LITEAV_API ITRTCCloud * getTRTCShareInstance()
```

__Return__

The pointer of the [ITRTCCloud](https://intl.cloud.tencent.com/document/product/647/35132#itrtccloud) singleton object will be returned. Note: deleting `ITRTCCloud*` will cause a compilation error; therefore, `destroyTRTCCloud` needs to be called to release the singleton pointer object.


### destroyTRTCShareInstance

This API is used to release [ITRTCCloud](https://intl.cloud.tencent.com/document/product/647/35132#itrtccloud) singleton object.
```
LITEAV_API void destroyTRTCShareInstance()
```



## Setting the `ITRTCCloudCallback` Callback
### addCallback

This API is used to set the [ITRTCCloudCallback](https://intl.cloud.tencent.com/document/product/647/35133) callback API.
```
void addCallback(ITRTCCloudCallback * callback)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| callback | [ITRTCCloudCallback](https://intl.cloud.tencent.com/document/product/647/35133) * | Event callback pointer. |

__Overview__

You can use [ITRTCCloudCallback](https://intl.cloud.tencent.com/document/product/647/35133) to get various status notifications from the SDK. For more information, please see the definitions in `ITRTCCloudCallback.h`.


### removeCallback

This API is used to remove event callback.
```
void removeCallback(ITRTCCloudCallback * callback)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| callback | [ITRTCCloudCallback](https://intl.cloud.tencent.com/document/product/647/35133) * | Event callback pointer. |



## Room API Functions
### enterRoom

This API is used to enter room.
```
void enterRoom(const TRTCParams & params, TRTCAppScene scene)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| params | const [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35134#trtcparams) & | Room entry parameters. For more information, please see [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35134#trtcparams). |
| scene | [TRTCAppScene](https://intl.cloud.tencent.com/document/product/647/35134#trtcappscene) | Application scenario. Currently, only video call (`VideoCall`) and LVB (`Live) scenarios are supported. |

__Overview__

If the room is successfully entered, the `onEnterRoom()` callback will be received; otherwise, the `onEnterRoom(result)` callback will be received. For more information on error codes for room entry failures, please see [Error Codes](https://intl.cloud.tencent.com/document/product/647/35140).

>?No matter whether room entry is successful, `enterRoom` must be used together with `exitRoom`. If `enterRoom` is called again before `exitRoom` is called, an unexpected error will occur.



### exitRoom

This API is used to exit room.
```
void exitRoom()
```

__Overview__

When the [exitRoom()](https://intl.cloud.tencent.com/document/product/647/35132#exitroom) API is called, the logic related to room exit will be executed, such as releasing resources of audio/video devices and codecs. After resources are released, the SDK will use the `onExitRoom()` callback in `TRTCCloudCallback` to notify you.
If you need to call [enterRoom()](https://intl.cloud.tencent.com/document/product/647/35132#enterroom) again or switch to another audio/video SDK, please wait until you receive the `onExitRoom()` callback; otherwise, exceptions such as occupied camera or mic may occur.


### switchRole

This API is used to switch roles and applies only to the LVB scenario (`TRTCAppSceneLIVE`).
```
void switchRole(TRTCRoleType role)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| role | [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35134#trtcroletype) | Target role, which is anchor by default. |

__Overview__

In the LVB scenario, a user may need to switch between "viewer" and "anchor" roles. You can use the `role` field in [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35134#trtcparams) before room entry to determine the role or use the `switchRole` API to switch roles after room entry.


### connectOtherRoom

This API is used to request cross-room call (anchor competition).
```
void connectOtherRoom(const char * params)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| params | const char * | Co-anchoring parameters in the format of JSON string. `roomId` indicates the target room number, and `userId` indicates the target user ID. |

__Overview__

In TRTC, two anchors in different rooms can use the "cross-room call" feature to co-anchor across the rooms. They can engage in "co-anchoring competition" without the need to exit their own rooms.
For example, when anchor A in room "001" uses [connectOtherRoom()](https://intl.cloud.tencent.com/document/product/647/35132#connectotherroom) to successfully call anchor B in room "002", all users in room "001" will receive the `onUserEnter(B)` and `onUserVideoAvailable(B,true)` callbacks of anchor B, and all users in room "002" will receive the `onUserEnter(A)` and `onUserVideoAvailable(A,true)` callbacks of anchor A.
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
- `roomId`: If anchor A in room "001" wants to co-anchor with anchor B in room "002", the `roomId` must be set to `002` when anchor A calls [connectOtherRoom()](https://intl.cloud.tencent.com/document/product/647/35132#connectotherroom).
- `userId`: If anchor A in room "001" wants to co-anchor with anchor B in room "002", the `userId` must be set to the `userId` of anchor B when anchor A calls [connectOtherRoom()](https://intl.cloud.tencent.com/document/product/647/35132#connectotherroom).


The result of requesting cross-room call will be returned through the `onConnectOtherRoom()` callback in `TRTCCloudCallback`.


<pre>
  //Here, the JsonCpp library is used to format the JSON string
  Json::Value jsonObj;
  jsonObj["roomId"] = 002;
  jsonObj["userId"] = "userB";
  Json::FastWriter writer;
  std::string params = writer.write(jsonObj);
  trtc.ConnectOtherRoom(params.c_str());
</pre>


### disconnectOtherRoom

This API is used to exit cross-room co-anchoring.
```
void disconnectOtherRoom()
```

__Overview__

The result of exiting cross-room call will be returned through the `onDisconnectOtherRoom()` callback in `TRTCCloudCallback`.


### setDefaultStreamRecvMode

This API is used to set audio/video data reception mode, which must be set before room entry for it to take effect.
```
void setDefaultStreamRecvMode(bool autoRecvAudio, bool autoRecvVideo)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| autoRecvAudio | bool | true: audio data will be automatically received; false: `muteRemoteAudio` needs to be called to send or cancel a request. Default value: true. |
| autoRecvVideo | bool | true: video data will be automatically received; false: `startRemoteView/stopRemoteView` needs to be called to send or cancel a request. Default value: true. |

__Overview__

To deliver an excellent instant broadcasting experience, the SDK automatically receives audio/video upon successful room entry by default, that is, you will immediately receive audio/video data from all remote users. If you do not call `startRemoteView`, video data will be automatically canceled due to timeout. If you use this API mainly in scenarios where automatic video data reception is not required, such as audio chat, you can select the reception mode based on your actual needs.

>?This API takes effect only if it is set before room entry.




## Video API Functions
### startLocalPreview

This API is used to enable preview image of local video.
```
void startLocalPreview(HWND rendHwnd)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rendHwnd | HWND | `HWND` that carries the preview image. |

__Overview__

This API will enable the default camera. You can call the `setCurrentCameraDevice` API to select another camera. When the first video frame starts to be rendered, you will receive the `onFirstVideoFrame(null)` callback in `TRTCCloudCallback`.


### stopLocalPreview

This API is used to stop local video capture and preview.
```
void stopLocalPreview()
```


### muteLocalVideo

This API is used to specify whether to block local video image.
```
void muteLocalVideo(bool mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | true: blocks; false: enables. Default value: false. |

__Overview__

After the local video is blocked, other members in the room will receive the `onUserVideoAvailable` callback notification.


### startRemoteView

This API is used to start displaying remote video image.
```
void startRemoteView(const char * userId, HWND rendHwnd)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | ID of remote user. |
| rendHwnd | HWND | Window handler that carries the preview image. |

__Overview__

If you receive the `onUserVideoAvailable(userId, true)` notification from the SDK, you can know that the remote user has enabled the video image. Later, when you use the `startRemoteView(userId)` API to load the remote image of this user, you can use a loading animation to optimize the experience for awaiting video loading. When the first video frame of this user starts to be displayed, you will receive the `onFirstVideoFrame(userId)` event callback.


### stopRemoteView

This API is used to stop displaying remote video image.
```
void stopRemoteView(const char * userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | ID of remote user. |

__Overview__

After this API is called, the SDK will stop receiving the remote video stream of the specified user and clear relevant video displaying resources.


### stopAllRemoteView

This API is used to stop displaying all remote video images.
```
void stopAllRemoteView()
```

>?If there is a screen sharing image, it will be stopped together with other remote video images.



### muteRemoteVideoStream

This API is used to pause receiving the specified remote video stream.
```
void muteRemoteVideoStream(const char * userId, bool mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | ID of remote user. |
| mute | bool | Whether to stop reception. |

__Overview__

This API only stops receiving remote user's video stream but does not release displaying resources; therefore, the video image will freeze at the last frame before the muting operation.


### muteAllRemoteVideoStreams

This API is used to stop receiving all remote video streams.
```
void muteAllRemoteVideoStreams(bool mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | Whether to stop reception. |


### setVideoEncoderParam

This API is used to set video encoder parameters.
```
void setVideoEncoderParam(const TRTCVideoEncParam & params)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| params | const [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoencparam) & | Video encoding parameters. For more information, please see the definition of [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoencparam) in `TRTCCloudDef.h`. |

__Overview__

These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.


### setNetworkQosParam

This API is used to set network bandwidth limit parameters.
```
void setNetworkQosParam(const TRTCNetworkQosParam & params)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| params | const [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcnetworkqosparam) & | Network bandwidth limit parameters. For more information, please see the definition of [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcnetworkqosparam) in `TRTCCloudDef.h`. |

__Overview__

These settings determine the bandwidth limit policies of the SDK in various network conditions (e.g., whether to "ensure definition" or "ensure smoothness" on a weak network).


### setLocalViewFillMode

This API is used to set rendering mode of local image.
```
void setLocalViewFillMode(TRTCVideoFillMode mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mode | [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideofillmode) | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). Default value: TRTCVideoFillMode_Fit. |


### setRemoteViewFillMode

This API is used to set rendering mode of remote image.
```
void setRemoteViewFillMode(const char * userId, TRTCVideoFillMode mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| mode | [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideofillmode) | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). Default value: TRTCVideoFillMode_Fit. |


### setLocalViewRotation

This API is used to set clockwise rotation angle of local image.
```
void setLocalViewRotation(TRTCVideoRotation rotation)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | TRTCVideoRotation | Rotation angles of `TRTCVideoRotation90`, `TRTCVideoRotation180`, and `TRTCVideoRotation270` are supported. Default value: TRTCVideoRotation0. |


### setRemoteViewRotation

This API is used to set clockwise rotation angle of remote image.
```
void setRemoteViewRotation(const char * userId, TRTCVideoRotation rotation)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| rotation | TRTCVideoRotation | Rotation angles of `TRTCVideoRotation90`, `TRTCVideoRotation180`, and `TRTCVideoRotation270` are supported. Default value: TRTCVideoRotation0. |


### setVideoEncoderRotation

This API is used to set direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server).
```
void setVideoEncoderRotation(TRTCVideoRotation rotation)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rotation | TRTCVideoRotation | Currently, rotation angles of `TRTCVideoRotation0` and `TRTCVideoRotation180` are supported. Default value: TRTCVideoRotation0. |


### setLocalViewMirror

This API is used to set mirror mode of local camera's preview image.
```
void setLocalViewMirror(bool mirror)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | bool | Mirror mode. Default value: false (not mirrored). |


### setVideoEncoderMirror

This API is used to set mirror mode of image output by encoder.
```
void setVideoEncoderMirror(bool mirror)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mirror | bool | Whether to enable remote mirror mode. true: yes; false: no. Default value: false. |

__Overview__

This API does not change the preview image of the local camera; instead, it changes the video image viewed by the remote user (and recorded by the server).


### enableSmallVideoStream

This API is used to enable dual-channel encoding mode with big and small images.
```
void enableSmallVideoStream(bool enable, const TRTCVideoEncParam & smallVideoParam)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | bool | Whether to enable small image encoding. Default value: `false`. |
| smallVideoParam | const [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoencparam) & | Video parameters of small image stream. |

__Overview__

If the current user is a major role (such as anchor, teacher, or host) in the room and uses PC or Mac, this mode can be enabled. In this mode, the current user will output two channels of video streams, i.e., **HD** and **LD**, at the same time (only one channel of audio stream will be output though). This mode will consume more network bandwidth and CPU computing resources.
As for remote viewers in the same room:
- If the downstream network is good, they can select the **HD** image.
- If the downstream network is poor, they can select the **LD** image.


### setRemoteVideoStreamType

This API is used to specify whether to view the big or small image of the specified `userId`.
```
void setRemoteVideoStreamType(const char * userId, TRTCVideoStreamType type)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| type | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Video stream type, i.e., big image or small image. Default value: `TRTCVideoStreamTypeBig`. |

__Overview__

To implement this feature, the dual-channel encoding mode must be enabled by the `userId` through `enableEncSmallVideoStream`; otherwise, this operation will not take effect.


### setPriorRemoteVideoStreamType

This API is used to set the video quality preferred by viewers.
```
void setPriorRemoteVideoStreamType(TRTCVideoStreamType type)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| type | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Whether big or small image will be viewed by default. Default value: `TRTCVideoStreamTypeBig`. |

__Overview__

It is recommended to select the LD small image for low-spec devices first. If the dual-channel encoding mode is not enabled, this operation will not take effect.



## Audio API Functions
### startLocalAudio

This API is used to enable local audio capture and upstreaming.
```
void startLocalAudio()
```

__Overview__

This function will start mic capture and transmit audio data to other users in the room. The SDK does not enable local audio upstreaming by default, which means that if you do not call this function, other users in the room will not hear your voice.

>?The TRTC SDK does not enable local mic capture by default.



### stopLocalAudio

This API is used to disable local audio capture and upstreaming.
```
void stopLocalAudio()
```

__Overview__

When local audio capture and upstreaming is disabled, other members in the room will receive the `onUserAudioAvailable(false)` callback notification.


### muteLocalAudio

This API is used to mute local audio.
```
void muteLocalAudio(bool mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | true: blocks; false: enables. Default value: false. |

__Overview__

After local audio is muted, other members in the room will receive the `onUserAudioAvailable(false)` callback notification. Different from `stopLocalAudio`, `muteLocalAudio` will not stop sending audio/video data; instead, it continues to send mute packets of an extremely low bitrate. `muteLocalAudio` is ideal in scenarios where the requirement for recording quality is high, so as to record MP4 files with better compatibility. This is because that some video file formats such as MP4 have a high requirement for audio continuity, an MP4 recording file cannot be played back smoothly if `stopLocalAudio` is used.


### muteRemoteAudio

This API is used to mute the specified user's audio.
```
void muteRemoteAudio(const char * userId, bool mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| mute | bool | true: muted; false: not muted. |


### muteAllRemoteAudio

This API is used to mute all users' audio.
```
void muteAllRemoteAudio(bool mute)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| mute | bool | true: muted; false: not muted. |


### enableAudioVolumeEvaluation

This API is used to enable or disable volume reminder.
```
void enableAudioVolumeEvaluation(uint32_t interval)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| interval | uint32_t | Sets the interval in ms for triggering the `onUserVoiceVolume` callback. The minimum interval is 100 ms. If the value is smaller than 0, the callback will be disabled. It is recommended to set this parameter to 300 ms. |

__Overview__

After this feature is enabled, the SDK will return the evaluation of the voice volume level of each channel in `onUserVoiceVolume()`. The volume bar in the demo is implemented based on this API. To enable this feature, call this API before calling [startLocalAudio()](https://intl.cloud.tencent.com/document/product/647/35132#startlocalaudio).


### startAudioRecording

This API is used to start audio recording.
```
int startAudioRecording(const TRTCAudioRecordingParams & audioRecordingParams)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| audioRecordingParams | const [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35134#trtcaudiorecordingparams) & | Audio recording parameters. For more information, please see `TRTCAudioRecordingParams`. |

__Return__

0: success; -1: audio recording has been started; -2: failed to create file or directory; -3: the audio format of the specified file extension is not supported.

__Overview__

After this API is called, the SDK will record all audios (such as local audio, remote audio, and background music) in the current call to a file. No matter whether room entry is performed, this API will take effect once called. If audio recording is still ongoing when `exitRoom` is called, it will stop automatically.


### stopAudioRecording

This API is used to stop audio recording.
```
void stopAudioRecording()
```

__Overview__

If audio recording is still ongoing when `exitRoom` is called, it will stop automatically.



## Camera API Functions
### getCameraDevicesList

This API is used to gets list of cameras.
```
ITRTCDeviceCollection * getCameraDevicesList()
```

__Return__

Camera manager object pointer `ITRTCDeviceCollection*`.

__Overview__

Sample code: 

<pre>
 ITRTCDeviceCollection * pDevice = m_pCloud->getCameraDevicesList();
 for (int i = 0; i < pDevice->getCount(); i++)
 {
     std::wstring name = UTF82Wide(pDevice->getDeviceName(i));
 }
 pDevice->release();
 pDevice = null;
</pre>

>?If deleting the `ITRTCDeviceCollection*` pointer causes a compilation error, the SDK will maintain the lifecycle of the `ITRTCDeviceCollection` object.



### setCurrentCameraDevice

This API is used to set the camera to be used.
```
void setCurrentCameraDevice(const char * deviceId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| deviceId | const char * | Device ID obtained from `getCameraDevicesList`. |


### getCurrentCameraDevice

This API is used to get the currently used camera.
```
ITRTCDeviceInfo * getCurrentCameraDevice()
```

__Return__

`ITRTCDeviceInfo` device information, which contains the device ID and name.



## Audio Device API Functions
### getMicDevicesList

This API is used to get list of mics.
```
ITRTCDeviceCollection * getMicDevicesList()
```

__Return__

Mic manager object pointer `ITRTCDeviceCollection*`.

__Overview__

Sample code: 

<pre>
 ITRTCDeviceCollection * pDevice = m_pCloud->getMicDevicesList();
 for (int i = 0; i < pDevice->getCount(); i++)
 {
     std::wstring name = UTF82Wide(pDevice->getDeviceName(i));
 }
 pDevice->release();
 pDevice = null;
</pre>

>?If deleting the `ITRTCDeviceCollection*` pointer causes a compilation error, the SDK will maintain the lifecycle of the `ITRTCDeviceCollection` object.



### getCurrentMicDevice

This API is used to get the currently used mic.
```
ITRTCDeviceInfo * getCurrentMicDevice()
```

__Return__

`ITRTCDeviceInfo` device information, which contains the device ID and name.


### setCurrentMicDevice

This API is used to set the mic to be used.
```
void setCurrentMicDevice(const char * micId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| micId | const char * | Device ID obtained from `getMicDevicesList`. |

__Overview__

This API is used to select a mic as the audio recording device. If it is not called, the mic with index 0 will be selected by default.


### getCurrentMicDeviceVolume

This API is used to get current mic volume level of the system.
```
uint32_t getCurrentMicDeviceVolume()
```

__Return__

Volume level value between 0 and 100.


### setCurrentMicDeviceVolume

This API is used to set current mic volume level of the system.
```
void setCurrentMicDeviceVolume(uint32_t volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint32_t | Mic volume level. Value range: 0–100. |


### getSpeakerDevicesList

This API is used to get list of speakers.
```
ITRTCDeviceCollection * getSpeakerDevicesList()
```

__Return__

Speaker manager object pointer `ITRTCDeviceCollection*`.

__Overview__

Sample code: 

<pre>
 ITRTCDeviceCollection * pDevice = m_pCloud->getSpeakerDevicesList();
 for (int i = 0; i < pDevice->getCount(); i++)
 {
     std::wstring name = UTF82Wide(pDevice->getDeviceName(i));
 }
 pDevice->release();
 pDevice = null;
</pre>

>?If deleting the `ITRTCDeviceCollection*` pointer causes a compilation error, the SDK will maintain the lifecycle of the `ITRTCDeviceCollection` object.



### getCurrentSpeakerDevice

This API is used to get the currently used speaker.
```
ITRTCDeviceInfo * getCurrentSpeakerDevice()
```

__Return__

`ITRTCDeviceInfo` device information, which contains the device ID and name.


### setCurrentSpeakerDevice

This API is used to set the speaker to be used.
```
void setCurrentSpeakerDevice(const char * speakerId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| speakerId | const char * | Device ID obtained from `getSpeakerDevicesList`. |


### getCurrentSpeakerVolume

This API is used to get current speaker volume level.
```
uint32_t getCurrentSpeakerVolume()
```

__Return__

Speaker volume level between 0 and 100.

>?The volume level to be queried is that of the system's speaker.



### setCurrentSpeakerVolume

This API is used to set current speaker volume level.
```
void setCurrentSpeakerVolume(uint32_t volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint32_t | Speaker volume to be set. Value range: 0–100. |

>?The volume to be set is that of the system's speaker.



## Beauty Filter API Functions
### setBeautyStyle

This API is used to set effect levels of beauty, brightening, and rosy skin filters.
```
void setBeautyStyle(TRTCBeautyStyle style, uint32_t beauty, uint32_t white, uint32_t ruddiness)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| style | [TRTCBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35134#trtcbeautystyle) | Beauty filter style: smooth or natural. The smooth style has more obvious skin smoothing effect and is suitable for entertaining scenarios. |
| beauty | uint32_t | Effect level of the beauty filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |
| white | uint32_t | Effect level of the brightening filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. |
| ruddiness | uint32_t | Effect level of the rosy skin filter. Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect. This parameter does not take effect currently. |

__Overview__

The SDK is integrated with two skin smoothing algorithms of different styles. One is called "smooth" and is suitable for shows as its effect is more obvious. The other is called "natural", which retains more facial details and seems more natural subjectively.


### setWaterMark

This API is used to set watermark.
```
void setWaterMark(TRTCVideoStreamType streamType, const char * srcData, TRTCWaterMarkSrcType srcType, uint32_t nWidth, uint32_t nHeight, float xOffset, float yOffset, float fWidthRatio)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| streamType | [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Stream type of the watermark to be set. Valid values: TRTCVideoStreamTypeBig, TRTCVideoStreamTypeSub. |
| srcData | const char * | Source data of watermark image (if `NULL` is passed in, the watermark will be removed). |
| srcType | [TRTCWaterMarkSrcType](https://intl.cloud.tencent.com/document/product/647/35134#trtcwatermarksrctype) | Source data type of watermark image (if `NULL` is passed in, this parameter will be ignored). |
| nWidth | uint32_t | Pixel width of watermark image (this parameter will be ignored if the source data is a file path). |
| nHeight | uint32_t | Pixel height of watermark image (this parameter will be ignored if the source data is a file path). |
| xOffset | float | Top-left offset on the X axis of watermark. |
| yOffset | float | Top-left offset on the Y axis of watermark. |
| fWidthRatio | float | Ratio of watermark width to image width (the watermark will be scaled proportionally by this parameter). |

__Overview__

The watermark position is determined by the `xOffset`, `yOffset`, and `fWidthRatio` parameters.
- `xOffset`: X coordinate of watermark, which is a floating point number between 0 and 1.
- `yOffset`: Y coordinate of watermark, which is a floating point number between 0 and 1.
- `fWidthRatio`: watermark dimensions ratio, which is a floating point number between 0 and 1.

>?This feature is not supported in big and small image streams currently.



## Secondary Stream API Functions
### startRemoteSubStreamView

This API is used to start rendering the secondary stream image of a remote user.
```
void startRemoteSubStreamView(const char * userId, HWND rendHwnd)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | ID of remote user. |
| rendHwnd | HWND | `HWND` that renders the image. |

__Overview__

Different from [startRemoteView()](https://intl.cloud.tencent.com/document/product/647/35132#startremoteview) that is used to display the primary image, this API can only be used to display the image of the secondary channel (e.g., screen sharing and remote video playback).

>?This API must be called after `onUserSubStreamAvailable` is called back.



### stopRemoteSubStreamView

This API is used to stop displaying screen sharing image of a remote user.
```
void stopRemoteSubStreamView(const char * userId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | ID of remote user. |


### setRemoteSubStreamViewFillMode

This API is used to set rendering mode of the secondary stream image.
```
void setRemoteSubStreamViewFillMode(const char * userId, TRTCVideoFillMode mode)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| mode | [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideofillmode) | Fill (the image may be stretched or cropped) or fit (there may be black color in unmatched areas). Default value: TRTCVideoFillMode_Fit. |

__Overview__

Different from [setRemoteViewFillMode()](https://intl.cloud.tencent.com/document/product/647/35132#setremoteviewfillmode) that is used to set the remote image of the primary channel, this API can be used to set the remote image of the secondary channel (e.g., screen sharing and remote video playback).


### getScreenCaptureSources

This API is used to enumerate shareable windows.
```
ITRTCScreenCaptureSourceList * getScreenCaptureSources(const SIZE & thumbSize, const SIZE & iconSize)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| thumbSize | const SIZE & | Specifies thumbnail size of the window to be obtained. The thumbnail can be drawn on the window selection UI. |
| iconSize | const SIZE & | Specifies icon size of the window to be obtained. |

__Return__

List of windows (including the screen).

__Overview__

If you want to add the screen sharing feature to your application, a window selection UI needs to be displayed first generally, so that the user can select the window to be shared. You can use the related functions to get the ID, type, name, and thumbnail of shareable windows and implement the window selection UI with the obtained information. Or, you can use the UI implemented in the demo's source code.

>?The returned list includes the screen and application windows. The screen will be in the first several elements in the list.
>If deleting the `ITRTCScreenCaptureSourceList*` pointer causes a compilation error, the SDK will maintain the lifecycle of the `ITRTCScreenCaptureSourceList` object.


### selectScreenCaptureTarget

This API is used to set screen sharing parameters. This method can be called during screen sharing.
```
void selectScreenCaptureTarget(const TRTCScreenCaptureSourceInfo & source, const RECT & captureRect, bool captureMouse, bool highlightWindow)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| source | const TRTCScreenCaptureSourceInfo & | Specifies sharing source. |
| captureRect | const RECT & | Specifies the area to be captured. |
| captureMouse | bool | Specifies whether to capture mouse cursor. |
| highlightWindow | bool | Specifies whether to highlight the currently shared window and whether to highlight a covered window to remind the user to move the covering window away. |

__Overview__

If you want to switch to another window to be shared during screen sharing, you can call this function again with no need to start screen sharing again.
The following sharing modes are supported:
- Sharing the entire screen: for `source` whose `type` is `Screen` in `sourceInfoList`, set `captureRect` to `{ 0, 0, 0, 0 }`.
- Sharing a specified area: for `source` whose `type` is `Screen` in `sourceInfoList`, set `captureRect` to a non-null value, e.g., `{ 100, 100, 300, 300 }`.
- Sharing an entire window: for `source` whose `type` is `Window` in `sourceInfoList`, set `captureRect` to `{ 0, 0, 0, 0 }`.
- Sharing a specified window area: for `source` whose `type` is `Window` in `sourceInfoList`, set `captureRect` to a non-null value, e.g., `{ 100, 100, 300, 300 }`.


### startScreenCapture

This API is used to start screen sharing.
```
void startScreenCapture(HWND rendHwnd)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rendHwnd | HWND | `HWND` that carries the preview image. |


### pauseScreenCapture

This API is used to pause screen sharing.
```
void pauseScreenCapture()
```


### resumeScreenCapture

This API is used to resume screen sharing.
```
void resumeScreenCapture()
```


### stopScreenCapture

This API is used to stop screen capture.
```
void stopScreenCapture()
```


### setSubStreamEncoderParam

This API is used to set encoder parameters for screen sharing.
```
void setSubStreamEncoderParam(const TRTCVideoEncParam & params)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| params | const [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoencparam) & | Secondary stream encoding parameters. For more information, please see the definition of [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoencparam) in `TRTCCloudDef.h`. |

__Overview__

Different from [setVideoEncoderParam()](https://intl.cloud.tencent.com/document/product/647/35132#setvideoencoderparam) that is used to set the encoding quality of the image of the primary channel, this function is only used to set codec parameters for the image of the secondary channel (e.g., screen sharing and remote video playback). These settings determine the quality of image viewed by remote users, which is also the image quality of recorded video files in the cloud.


### setSubStreamMixVolume

This API is used to set audio mixing volume level of the secondary stream.
```
void setSubStreamMixVolume(uint32_t volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint32_t | Volume level of audio mixing. Value range: 0–100. |

__Overview__

The greater the value, the larger the ratio of the secondary stream volume level to the mic volume level. It is not recommended to set a high value for this parameter as a high volume level will cover the mic sound.



## Custom Capture and Rendering API Functions
### enableCustomVideoCapture

This API is used to enable custom video capture mode.
```
void enableCustomVideoCapture(bool enable)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | bool | Whether to enable. Default value: false. |

__Overview__

After the custom mode is enabled, the SDK will not run the original video capture process and retain only the encoding and sending capabilities. You need to use [sendCustomVideoData()](https://intl.cloud.tencent.com/document/product/647/35132#sendcustomvideodata) to continuously insert the captured video image into the SDK.


### sendCustomVideoData

This API is used to deliver the captured video data to the SDK.
```
void sendCustomVideoData(TRTCVideoFrame * frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | TRTCVideoFrame * | Video data. The I420 format is supported. |

__Overview__

It is recommended to enter the following information for `TRTCVideoFrame` (other fields can be left empty):
- pixelFormat: only `LiteAVVideoPixelFormat_I420` is supported.
- bufferType: only `LiteAVVideoBufferType_Buffer` is supported.
- data: video frame buffer.
- length: data length of a video frame. Its value in I420 format is `width * height * 3 / 2`.
- width: video image length.
- height: video image width.
- timestamp: if the intervals for `timestamp` are uneven, the audio/video sync and quality of MP4 recording will be seriously affected.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35158).

>?
>- The SDK has an internal frame rate control logic, and the target frame rate set in `setVideoEncoderParam` shall prevail. If the frame rate is too high, automatic frame discarding may occur; if too low, automatic frame interpolation will be implemented.
>- It is recommended to set `timestamp` in `frame` to 0, so that the SDK will set the timestamp by itself. However, please "evenly" set the calling interval of `sendCustomVideoData`; otherwise, the video frame rate will be unstable.


### enableCustomAudioCapture

This API is used to enable the custom audio capture mode. After this mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](https://intl.cloud.tencent.com/document/product/647/35132#sendcustomaudiodata) to continuously insert the captured audio data into the SDK.
```
void enableCustomAudioCapture(bool enable)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enable | bool | Whether to enable. Default value: false. |


### sendCustomAudioData

This API is used to deliver the captured audio data to the SDK.
```
void sendCustomAudioData(TRTCAudioFrame * frame)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| frame | TRTCAudioFrame * | Audio frame. Currently, only mono channel, 48 kHz sample rate, and the `LiteAVAudioFrameFormatPCM` format are supported. |

__Overview__

It is recommended to enter the following information for `TRTCAudioFrame` (other fields can be left empty):
- audioFormat: only `LiteAVAudioFrameFormatPCM` is supported.
- data: audio frame buffer.
- length: audio frame data length. It is recommended to set sampling time to 20 ms for each frame. **For example, if the PCM format is used and the sample rate is 48000, then the frame length for mono channel will be `48000 * 0.02s * 1 * 16 bit = 15360 bit = 1920 bytes`.**
- sampleRate: sample rate. Currently, only 48000 is supported.
- channel: number of channels (if stereo is used, data is interwoven). Valid values: 1: mono channel; 2: dual channel.
- timestamp: if the intervals for `timestamp` are uneven, the audio/video sync and quality of MP4 recording will be seriously affected.


For more information, please see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35158).

>?You can set `timestamp` in `frame` to `0`, so that the SDK will set the timestamp by itself. However, please "evenly" set the calling interval of `sendCustomAudioData`; otherwise, the audio will be unstable.



### setLocalVideoRenderCallback

This API is used to set custom rendering for local video.
```
int setLocalVideoRenderCallback(TRTCVideoPixelFormat pixelFormat, TRTCVideoBufferType bufferType, ITRTCVideoRenderCallback * callback)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| pixelFormat | TRTCVideoPixelFormat | Specifies the called back pixel format. |
| bufferType | TRTCVideoBufferType | Specifies video data structure type. |
| callback | [ITRTCVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtcvideorendercallback) * | Custom rendering callback. |

__Return__

0: success; values smaller than 0: error.

>?After this method is set, the SDK will internally call back the captured data, skip the `HWND` rendering logic, and call `setLocalVideoRenderCallback(TRTCVideoPixelFormat_Unknown, TRTCVideoBufferType_Unknown, nullptr)` to stop the callback.


### setRemoteVideoRenderCallback

This API is used to set custom rendering for remote video.
```
int setRemoteVideoRenderCallback(const char * userId, TRTCVideoPixelFormat pixelFormat, TRTCVideoBufferType bufferType, ITRTCVideoRenderCallback * callback)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| userId | const char * | User ID. |
| pixelFormat | TRTCVideoPixelFormat | Specifies the called back pixel format. |
| bufferType | TRTCVideoBufferType | Specifies video data structure type. |
| callback | [ITRTCVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtcvideorendercallback) * | Custom rendering callback. |

__Return__

0: success; values smaller than 0: error.

__Overview__

This method is similar to `setLocalVideoRenderDelegate`. The difference is that one is callback of rendering the local image, while the other is callback of rendering the remote image.

>?After this method is set, the SDK will internally call back the remote data after decoding it, skip the `HWND` rendering logic, and call `setRemoteVideoRenderCallback(userId, TRTCVideoPixelFormat_Unknown,  TRTCVideoBufferType_Unknown, nullptr)` to stop the callback.



### setAudioFrameCallback

This API is used to set audio data callback.
```
int setAudioFrameCallback(ITRTCAudioFrameCallback * callback)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| callback | [ITRTCAudioFrameCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtcaudioframecallback) * | Callback of audio frame data (in PCM format). If callback = nullptr, data callback will be stopped. |

__Return__

0: success; values smaller than 0: error.

__Overview__

After this method is set, the SDK will internally call back the data (in PCM format) from the audio module, including:
- onCapturedAudioFrame: audio data captured by current mic
- onPlayAudioFrame: audio data from each remote user before audio mixing
- onMixedPlayAudioFrame: audio data to be played back by speaker after audio data from each channel is mixed



## Custom Message Sending API Functions
### sendCustomCmdMsg

This API is used to send custom message to all users in the room.
```
bool sendCustomCmdMsg(uint32_t cmdId, const uint8_t * data, uint32_t dataSize, bool reliable, bool ordered)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| cmdId | uint32_t | Message ID. Value range: 1–10. |
| data | const uint8_t * | Message to be sent, which can contain up to 1 KB (1,000 bytes) of data. |
| dataSize | uint32_t | Size of the data to be sent. |
| reliable | bool | Whether reliable sending is enabled; if yes, the recipient needs to temporarily store the data of a certain period to wait for re-sending, which will cause certain delay. |
| ordered | bool | Whether orderly sending is enabled, i.e., whether the data should be received in the same order in which it is sent; if yes, the recipient needs to temporarily store and sort messages, which will cause certain delay. |

__Return__

true: message has been sent successful; false: failed to send message.

__Overview__

This API can be used to broadcast your custom data to other users in the room though the audio/video data channel. Due to reuse of this channel, please strictly control the frequency of sending custom messages and message size; otherwise, the quality control logic of the audio/video data will be affected, causing uncertain issues.

>?This API has the following restrictions:
>- Up to 30 messages can be sent per second to all users in the room.
>- A packet can contain up to 1 KB of data; if the threshold is exceeded, the packet is very likely to be discarded by the intermediate router or server.
>- A client can send up to 8 KB of data in total per second.
>- `reliable` and `ordered` must be set to the same value (`true` or `false`) and cannot be set to different values currently.
>- You are strongly recommended to use different `cmdIDs` for messages of different types. This can reduce message delay when orderly sending is required.


### sendSEIMsg

This API is used to embed custom data of a small size in video frames.
```
bool sendSEIMsg(const uint8_t * data, uint32_t dataSize, int32_t repeatCount)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| data | const uint8_t * | Data to be sent, which can contain up to 1 KB (1,000 bytes) of data. |
| dataSize | uint32_t | Size of the data to be sent. |
| repeatCount | int32_t | Data sending count. |

__Return__

true: the message is allowed and will be sent to subsequent video frames; false: the message is not allowed to be sent.

__Overview__

Different from how `sendCustomCmdMsg` works, `sendSEIMsg` directly inserts data into the video data header. Therefore, even if the video frames are relayed to LVB CDN, the data will always exist. However, as the data needs to be embedded in the video frames, it cannot be too large and is recommended to be of just several bytes.
The most common use is to embed the custom timestamp into video frames through `sendSEIMsg`. The biggest benefit of this scheme is that it can implement a perfect alignment between messages and video image.

>?This API has the following restrictions:
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
void playBGM(const char * path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | const char * | Path to music file. |


### stopBGM

This API is used to stop background music.
```
void stopBGM()
```


### pauseBGM

This API is used to pause background music.
```
void pauseBGM()
```


### resumeBGM

This API is used to resume background music.
```
void resumeBGM()
```


### getBGMDuration

This API is used to get the total length of the music file in milliseconds.
```
uint32_t getBGMDuration(const char * path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | const char * | Path to music file. If `path` is left empty, the length of the music file being played back will be returned. |

__Return__

The length will be returned if this API is successfully called; otherwise, `-1` will be returned.


### setBGMPosition

This API is used to set playback progress of background music.
```
void setBGMPosition(uint32_t pos)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| pos | uint32_t | In milliseconds. |


### setMicVolumeOnMixing

This API is used to set mic volume level. This API is used to adjust the mic volume level when background music is played back.
```
void setMicVolumeOnMixing(uint32_t volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint32_t | Volume level. 100 indicates normal volume level. Value range: 0–200. |


### setBGMVolume

This API is used to set background music volume level. This API is used to control the background music volume level during playback.
```
void setBGMVolume(uint32_t volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint32_t | Volume level. 100 indicates normal volume level. Value range: 0–200. |


### startSystemAudioLoopback

This API is used to enable system audio capture (the 64-bit SDK currently does not support system audio mixing).
```
void startSystemAudioLoopback(const char * path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | const char * | - If `path` is left empty, the audio of the entire OS will be captured.<br>- If `path` is set to the path to an .exe program (e.g., QQ Music), the program will be started, and only its audio will be captured. |

__Overview__

After this feature is enabled, the audio of the entire OS (i.e., `path` is left empty) or a player (i.e., `path` is set) will be captured and mixed with the audio captured by the current mic. The mixed audio will be uploaded to the cloud.


### stopSystemAudioLoopback

This API is used to disable system audio capture.
```
void stopSystemAudioLoopback()
```


### setSystemAudioLoopbackVolume

This API is used to set volume level for system audio capture.
```
void setSystemAudioLoopbackVolume(uint32_t volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | uint32_t | Volume level. Value range: 0–100. |



## Sound Effect API Functions
### playAudioEffect

This API is used to play back sound effect.
```
void playAudioEffect(TRTCAudioEffectParam * effect)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effect | [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcaudioeffectparam) * | Sound effect. |

__Overview__

You need to assign an ID to each sound effect, through which you can start, stop, or set the volume level of a sound effect. If you want to play back multiple sound effects at the same time, please assign different IDs to them. If you use the same ID for different sound effects, the SDK cannot play them back at the same time; instead, it will stop playing back the current sound effect and then start playing back the next one of the same ID.


### setAudioEffectVolume

This API is used to set sound effect volume level.
```
void setAudioEffectVolume(int effectId, int volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

>?This volume level will take precedence over the overall sound effect volume level specified in `setAllAudioEffectsVolume`.


### stopAudioEffect

This API is used to stop sound effect.
```
void stopAudioEffect(int effectId)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| effectId | int | Sound effect ID. |


### stopAllAudioEffects

This API is used to stop all sound effects.
```
void stopAllAudioEffects()
```


### setAllAudioEffectsVolume

This API is used to set volume level of all sound effects.
```
void setAllAudioEffectsVolume(int volume)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| volume | int | Volume level. Value range: 0–100. Default value: 100. |

>?The volume level set by this operation will take precedence over that of an individual sound effect specified in `setAudioEffectVolume`.




## Device and Network Test API Functions
### startSpeedTest

This API is used to start network speed test (do not test during a video call so as to avoid affecting the call quality).
```
void startSpeedTest(uint32_t sdkAppId, const char * userId, const char * userSig)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| sdkAppId | uint32_t | Application ID. |
| userId | const char * | User ID. |
| userSig | const char * | User signature. |

__Overview__

The speed test result will be used to optimize the SDK's subsequent selection policy. It is recommended to perform the speed test before users place the first call, which will help select the optimal server. If the test result is not satisfactory, you can use a noticeable UI prompt to remind the user to select a better network.

>?The speed test will consume a certain amount of traffic and generate a small amount of extra traffic fees as a result.



### stopSpeedTest

This API is used to stop network speed test.
```
void stopSpeedTest()
```


### startCameraDeviceTest

This API is used to start camera test.
```
void startCameraDeviceTest(HWND rendHwnd)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| rendHwnd | HWND | `HWND` that carries the preview image. |

__Overview__

The `onFirstVideoFrame` callback API will be triggered.

>?You can use the `setCurrentCameraDevice` API to switch cameras during the test.



### stopCameraDeviceTest

This API is used to stop camera test.
```
void stopCameraDeviceTest()
```


### startMicDeviceTest

This API is used to start mic test.
```
void startMicDeviceTest(uint32_t interval)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| interval | uint32_t | Time interval in ms for displaying volume level reminder. It is recommended to set this parameter to a value greater than 200 ms. |

__Overview__

The `onTestMicVolume` callback API can get the test data.
This method is used to test whether the mic can function properly, and `volume` ranges from 0 to 100.


### stopMicDeviceTest

This API is used to stop mic test.
```
void stopMicDeviceTest()
```


### startSpeakerDeviceTest

This API is used to start speaker test.
```
void startSpeakerDeviceTest(const char * testAudioFilePath)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| testAudioFilePath | const char * | Absolute path to audio file, which must be a string in UTF-8 format. Supported file formats: WAV, MP3. |

__Overview__

The `onTestSpeakerVolume` callback API can get the test data.
This method plays back the specified audio data to test whether the speaker can function properly. If sound can be heard, the speaker is normal.


### stopSpeakerDeviceTest

This API is used to stop speaker test.
```
void stopSpeakerDeviceTest()
```



## MixTranscoding and CDN Relayed Push
### setMixTranscodingConfig

This API is used to start (update) On-Cloud MixTranscoding: this method uses the transcoding service of Tencent Cloud to combine multiple image channels into one channel.
```
void setMixTranscodingConfig(TRTCTranscodingConfig * config)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| config | [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35134#trtctranscodingconfig) * | For more information, please see the description of [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35134#trtctranscodingconfig) in `TRTCCloudDef.h`. If `NULL` is passed in, On-Cloud MixTranscoding will be canceled. |

__Overview__

This API will send a command to the Tencent Cloud transcoding server to combine multiple image channels in the room into one channel.
If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each image channel in the room will have a corresponding LVB [CDN address](https://intl.cloud.tencent.com/document/product/647/35242), and you can use On-Cloud MixTranscoding to mix multiple image channels from the LVB addresses to one channel and view the mixed image on LVB CDN.
You can use the transcoding parameters to set the position of each channel of image and quality of the final output image.
Reference document: [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/35123/34618). Sample code: the demo provides the entry for trying out this feature. You can experience it in "On-Cloud Image Mix" and "Share Playback Address" in the "More Features" panel.


<pre>
**Image 1**=> decoding => =>
                        \
**Image 2**=> decoding =>  image mixing => encoding => **mixed image**
                        /
**Image 3**=> decoding => =>
</pre>


>?Notes on On-Cloud MixTranscoding:
>- On-cloud transcoding will cause a delay of 1–2 seconds in video playback with CDN.
>- If you call this function, the multiple channels of images will be mixed to the [CDN address](https://intl.cloud.tencent.com/document/product/647/35242) of your own channel.


### startPublishCDNStream

This API is used to relay stream to the specified push address.
```
void startPublishCDNStream(const TRTCPublishCDNParam & param)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| param | const [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcpublishcdnparam) & | For more information, please see the description of [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcpublishcdnparam) in `TRTCCloudDef.h`. |

__Overview__

This API will push a command to Tencent Cloud's relay server, and Tencent Cloud will push the current channel of audio/video to your specified RTMP push address.
If you have enabled the "automatic relayed LVB" feature on the feature configuration page in the TRTC [Console](https://console.cloud.tencent.com/rav/), each channel of image in the room will have a default CDN address. Therefore, this feature is not commonly used and required only if you need to configure multiple CDN providers.
As relaying an individual channel of image to LVB CDN is generally meaningless, this feature is usually used with On-Cloud MixTranscoding, i.e., `setMixTranscodingConfig` is used to mix multiple image channels to one channel and then relay it.

>?Notes on relayed push:
>- By default, audio/video streams can be relayed only to the Tencent Cloud RTMP [push address](https://intl.cloud.tencent.com/document/product/267/32480). To relay streams to other cloud services, please submit a ticket to contact us.
>- If you call this function, only your own channel of image will be relayed to the specified RTMP push address. Therefore, this API usually needs to be used together with `setMixTranscodingConfig`.
>- In TRTC, each channel of image in the room will have a default CDN address (which needs to be enabled). Therefore, this feature is not commonly used and required only if you need to configure multiple CDN providers.


### stopPublishCDNStream

This API is used to stop relayed push.
```
void stopPublishCDNStream()
```



## Log API Functions
### getSDKVersion

This API is used to get SDK version information.
```
const char * getSDKVersion()
```

__Return__

Version number in UTF-8 format.


### setLogLevel

This API is used to set log output level.
```
void setLogLevel(TRTCLogLevel level)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| level | [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35134#trtcloglevel) | For more information, please see `TRTCLogLevel`. Default value: TRTCLogLevelNone. |


### setConsoleEnabled

This API is used to disable or enable console log printing.
```
void setConsoleEnabled(bool enabled)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enabled | bool | Specifies whether to enable it, which is disabled by default. |


### setLogCompressEnabled

This API is used to enable or disable local log compression.
```
void setLogCompressEnabled(bool enabled)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| enabled | bool | Specifies whether to enable it, which is disabled by default. |

__Overview__

If compression is enabled, the log size will significantly reduce, but logs can be read only after being decompressed by the Python script provided by Tencent Cloud. If compression is disabled, logs will be stored in plaintext and can be read directly in Notepad, but will take up more storage capacity.


### setLogDirPath

This API is used to set log storage path.
```
void setLogDirPath(const char * path)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| path | const char * | Folder where logs are stored. This parameter is in UTF-8 format, such as "D:\\Log". |

>?The log files are stored in C:/Users/[System username]/AppData/Roaming/Tencent/liteav/log (i.e., appdata%/Tencent/liteav/log) by default. To change the path, call this API before calling other methods.



### setLogCallback

This API is used to set log callback.
```
void setLogCallback(ITRTCLogCallback * callback)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| callback | [ITRTCLogCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtclogcallback) * | Log callback. |


### showDebugView

This API is used to display dashboard.
```
void showDebugView(int showType)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| showType | int | 0: does not display; 1: displays lite edition; 2: displays full edition. Default value: 0. |

__Overview__

The dashboard is a floating view for status statistics and event notifications to facilitate debugging.


### callExperimentalAPI

This API is used to call experimental APIs.
```
void callExperimentalAPI(const char * jsonStr)
```

__Parameters__

| Parameter | Type | Description |
|-----|-----|-----|
| jsonStr | const char * | JSON string of API and parameter descriptions. |

>?This API is used to call some experimental APIs.



