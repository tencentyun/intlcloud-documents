## Overview

### Basic APIs

| API                                                          | Description                            |
| ------------------------------------------------------------ | --------------------------------- |
| [getTRTCShareInstance](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getTRTCShareInstance) | Creates a `TRTCCloud` singleton.             |
| [destroyTRTCShareInstance](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_destroyTRTCShareInstance) | Releases a `TRTCCloud` singleton.        |
| [addCallback](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_addCallback_trtc_ITRTCCloudCallback_) | Sets the callback API `TRTCCloudCallback`. |
| [removeCallback](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_removeCallback_trtc_ITRTCCloudCallback_) | Removes event callback.                    |

### Room APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_enterRoom_trtc_TRTCParams__trtc_TRTCAppScene_) | Enters a room. If the room does not exist, the system will create one automatically.           |
| [exitRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_exitRoom) | Exits a room.                                                   |
| [switchRole](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_switchRole_trtc_TRTCRoleType_) | Switches roles. This API works only in live streaming scenarios (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [setDefaultStreamRecvMode](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setDefaultStreamRecvMode_System_Boolean_System_Boolean_) | Sets the audio/video data receiving mode, which must be set before room entry to take effect.           |
| [connectOtherRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_connectOtherRoom_System_String_) | Requests a cross-room call (anchor competition).                                    |
| [disconnectOtherRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_disconnectOtherRoom) | Exits a cross-room call.                                               |
| [switchRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_switchRoom_trtc_TRTCSwitchRoomConfig_) | Switches rooms.  |



### CDN APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startPublishing_System_String_trtc_TRTCVideoStreamType_) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopPublishing) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startPublishCDNStream_trtc_TRTCPublishCDNParam_) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor.      |
| [stopPublishCDNStream](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopPublishCDNStream) | Stops relaying to non-Tencent Cloud addresses.      |
| [setMixTranscodingConfig](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setMixTranscodingConfig_System_Nullable_trtc_TRTCTranscodingConfig__) | Sets On-Cloud MixTranscoding parameters.     |

### Video APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [startLocalPreview](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startLocalPreview_System_Boolean_System_Object_) | Enables local video preview (only custom rendering is supported currently).      |
| [stopLocalPreview](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopLocalPreview) | Stops local video capturing and preview.      |
| [muteLocalVideo](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteLocalVideo_System_Boolean_) | Pauses/Resumes sending local video data.      |
| [startRemoteView](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startRemoteView_System_String_trtc_TRTCVideoStreamType_System_Object_) | Starts pulling and displaying the image of a specified remote user (only custom rendering is supported currently).      |
| [stopRemoteView](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopRemoteView_System_String_trtc_TRTCVideoStreamType_) | Stops displaying and pulling the video image of a remote user.     |
| [stopAllRemoteView](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopAllRemoteView) | Stops displaying and pulling the video images of all remote users.     |
| [muteRemoteVideoStream](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteRemoteVideoStream_System_String_System_Boolean_) | Pauses/Resumes receiving the video stream of a specified remote user.     |
| [muteAllRemoteVideoStreams](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteAllRemoteVideoStreams_System_Boolean_) | Pauses/Resumes receiving all remote video streams.    |
| [setVideoEncoderParam](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setVideoEncoderParam_trtc_TRTCVideoEncParam__) | Sets video encoder parameters.    |
| [setNetworkQosParam](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setNetworkQosParam_trtc_TRTCNetworkQosParam__) | Sets QoS control parameters.    |
| [setVideoEncoderMirror](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setVideoEncoderMirror_System_Boolean_) | Sets the mirror mode of encoded images.    |

### Audio APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startLocalAudio_trtc_TRTCAudioQuality_) | Enables local audio capturing and upstream data transfer.          |
| [stopLocalAudio](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopLocalAudio) | Disables local audio capturing and upstream data transfer.          |
| [muteLocalAudio](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteLocalAudio_System_Boolean_) | Mutes/Unmutes local audio.           |
| [muteRemoteAudio](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteRemoteAudio_System_String_System_Boolean_) | Mutes/Unmutes a specified remote user. |
| [muteAllRemoteAudio](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteAllRemoteAudio_System_Boolean_) | Mutes/Unmutes all remote users.       |
| [setRemoteAudioVolume](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setRemoteAudioVolume_System_String_System_Int32_) | Sets the playback volume of a remote user.        |
| [setAudioCaptureVolume](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setAudioCaptureVolume_System_Int32_) | Sets the SDK capturing volume.                 |
| [getAudioCaptureVolume](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getAudioCaptureVolume) | Gets the SDK capturing volume.                 |
| [setAudioPlayoutVolume](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setAudioPlayoutVolume_System_Int32_) | Sets the SDK playback volume.                 |
| [getAudioPlayoutVolume](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getAudioPlayoutVolume) | Gets the SDK playback volume.                 |
| [enableAudioVolumeEvaluation](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_enableAudioVolumeEvaluation_System_UInt32_) | Enables volume reminders.                  |
| [startAudioRecording](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startAudioRecording_trtc_TRTCAudioRecordingParams__) | Starts audio recording.                          |
| [stopAudioRecording](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopAudioRecording) | Stops audio recording.                          |

### Device management APIs

| API | Description |
|-----|-----|
| [getDeviceManager](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getDeviceManager) | Gets the device management module. For details, please see [Specific Device Management APIs](#equipment). |


### Music and voice effect APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getAudioEffectManager) | Gets the audio effect management class `TXAudioEffectManager`, which is used to manage background music, short audio effects, and voice effects. For details, please see [Specific Music and Voice Effect APIs](#music). |

### Custom video rendering APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setLocalVideoRenderCallback](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLocalVideoRenderCallback_trtc_TRTCVideoPixelFormat_trtc_TRTCVideoBufferType_trtc_ITRTCVideoRenderCallback_) | Sets custom rendering for the local video.              |
| [setRemoteVideoRenderCallback](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setRemoteVideoRenderCallback_System_String_trtc_TRTCVideoPixelFormat_trtc_TRTCVideoBufferType_trtc_ITRTCVideoRenderCallback_) | Sets custom rendering for the video of a remote user.             |

### Custom message sending APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sendSEIMsg](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_sendSEIMsg_System_Byte___System_Int32_System_Int32_) | Embeds small-volume custom data in video frames. |


### Network testing APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startSpeedTest_System_Int32_System_String_System_String_) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopSpeedTest) | Stops server speed testing.                                             |


### Log APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getSDKVersion) | Gets the SDK version.         |
| [setLogLevel](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLogLevel_trtc_TRTCLogLevel_) | Sets the log output level.         |
| [setLogDirPath](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLogDirPath_System_String_) | Changes the path to save logs.          |
| [setLogCompressEnabled](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLogCompressEnabled_System_Boolean_) | Enables/Disables local log compression. |
| [callExperimentalAPI](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_callExperimentalAPI_System_String_) | Calls the experimental API. |



## TRTCCloudCallback

Callback APIs for the TRTC audio call feature

### Error and warning event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onError_trtc_TXLiteAVError_String_IntPtr_) | Error callback. This indicates that the SDK encountered an irrecoverable error. Such errors must be listened for, and UI reminders should be displayed to users if necessary. |
| [onWarning](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onWarning_trtc_TXLiteAVWarning_String_IntPtr_) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onEnterRoom_System_Int32_) | Callback of room entry                  |
| [onExitRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onExitRoom_System_Int32_) | Callback of room exit                |
| [onSwitchRole](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSwitchRole_trtc_TXLiteAVError_String_) | Callback of role switching                |
| [onConnectOtherRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onConnectOtherRoom_System_String_trtc_TXLiteAVError_System_String_) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisConnectOtherRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onDisconnectOtherRoom_trtc_TXLiteAVError_System_String_) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_switchRoom_trtc_TRTCSwitchRoomConfig_) | Callback of the result of room switching (`switchRoom`)      |


### User event callback APIs

| API                                                          | Description                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onRemoteUserEnterRoom_String_) | Callback of the entry of a user                              |
| [onRemoteUserLeaveRoom](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onRemoteUserLeaveRoom_String_System_Int32_) | Callback of the exit of a user                              |
| [onUserVideoAvailable](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onUserVideoAvailable_String_System_Boolean_) | Callback of whether a user has turned the camera on                |
| [onUserAudioAvailable](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onUserAudioAvailable_String_System_Boolean_) | Callback of whether a remote user has playable audio               |
| [onFirstVideoFrame](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onFirstVideoFrame_String_trtc_TRTCVideoStreamType_System_Int32_System_Int32_) | Callback of rendering the first video frame of the local user or a remote user                |
| [onFirstAudioFrame](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onFirstAudioFrame_String_) | Callback of playing the first audio frame of a remote user. No notifications are sent for local audio. |
| [onSendFirstLocalVideoFrame](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSendFirstLocalVideoFrame_trtc_TRTCVideoStreamType_) | Callback of sending the first local video frame              |
| [onSendFirstLocalAudioFrame](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSendFirstLocalAudioFrame) | Callback of sending the first local audio frame                     |


### Callback APIs for statistics on network quality and technical metrics

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onNetworkQuality_trtc_TRTCQualityInfo_trtc_TRTCQualityInfo___UInt32_) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the current upstream and downstream data transfer. |
| [onStatistics](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStatistics_trtc_TRTCStatistics_) | Callback of statistics on technical metrics                                           |


### Server event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onConnectionLost) | Callback of the disconnection of the SDK from the server                                      |
| [onTryToReconnect](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onTryToReconnect) | Callback of the SDK trying to connect to the server again                                   |
| [onConnectionRecovery](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onConnectionRecovery) | Callback of the reconnection of the SDK to the server                                     |
| [onSpeedTest](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSpeedTest_trtc_TRTCSpeedTestResult_System_Int32_System_Int32_) | Callback of server speed test results. The SDK tests the speed of multiple server addresses, and the result of each test is returned through this callback. |


### Hardware event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onCameraDidReady) | Callback of the camera being ready                |
| [onMicDidReady](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onMicDidReady) | Callback of the mic being ready                                             |
| [onUserVoiceVolume](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onUserVoiceVolume_trtc_TRTCVolumeInfo___UInt32_UInt32_) | Callback of volume, including the volume of each `userId` and the total remote volume |
| [onDeviceChange](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onDeviceChange_String_trtc_TRTCDeviceType_trtc_TRTCDeviceState_) |Callback of connecting/disconnecting a local device                |



[](id:reback)

### Custom message receiving callback APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------- |
| [onRecvSEIMsg](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onRecvSEIMsg_String_Byte___UInt32_) | Callback of receiving an SEI message |

[](id:cdn)

### Callback APIs for CDN relayed push

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStartPublishing_System_Int32_String_) | Callback of starting to push to Tencent Cloud’s live streaming CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startPublishing_System_String_trtc_TRTCVideoStreamType_) |
| [onStopPublishing](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStopPublishing_System_Int32_String_) | Callback of stopping pushing to Tencent Cloud’s live streaming CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopPublishing) |
| [onStartPublishCDNStream](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStartPublishCDNStream_System_Int32_String_) |Callback of the completion of starting relayed push to CDNs                |
| [onStopPublishCDNStream](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStopPublishCDNStream_System_Int32_String_) |Callback of the completion of stopping relayed push to CDNs                |
| [onSetMixTranscodingConfig](https://comm.qq.com/en-trtc/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSetMixTranscodingConfig_System_Int32_String_) |Sets On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`                |

[](id:key)

## Definitions of Key Classes

| Class                                                         | Description                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCParams](https://comm.qq.com/en-trtc/api/trtc.TRTCParams.html) | Room entry parameters                                          |
| [TRTCVideoEncParam](https://comm.qq.com/en-trtc/api/trtc.TRTCVideoEncParam.html) | Video encoding parameters                           |
| [TRTCTranscodingConfig](https://comm.qq.com/en-trtc/api/trtc.TRTCTranscodingConfig.html) | On-Cloud MixTranscoding configuration                           |
| [TRTCSwitchRoomConfig](https://comm.qq.com/en-trtc/api/trtc.TRTCSwitchRoomConfig.html) | Room switching parameters                                  |
| [TRTCNetworkQosParam](https://comm.qq.com/en-trtc/api/trtc.TRTCNetworkQosParam.html) | QoS control parameters                                  |
| [TXVoiceReverbType](https://comm.qq.com/en-trtc/api/trtc.TXVoiceReverbType.html) | Reverb effects (karaoke, room, hall, low and deep, resonant, etc.) |
| [AudioMusicParam](https://comm.qq.com/en-trtc/api/trtc.AudioMusicParam.html) | Parameters for music and voice effect setting APIs |
| [TRTCAudioRecordingParams](https://comm.qq.com/en-trtc/api/trtc.TRTCAudioRecordingParams.html) | Audio recording parameters |

[](id:equipment)

## Specific Device Management APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [isFrontCamera](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_isFrontCamera) | Gets whether the front camera is being used.                           |
| [switchCamera](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_switchCamera_System_Boolean_) | Switches cameras.                           |
| [getCameraZoomMaxRatio](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_getCameraZoomMaxRatio) | Gets the maximum zoom level of the current camera.                            |
| [setCameraZoomRatio](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_setCameraZoomRatio_System_Double_) | Sets the zoom level of the current camera.                           |
| [isAutoFocusEnabled](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_isAutoFocusEnabled) | Gets whether automatic facial recognition is supported.                            |
| [enableCameraAutoFocus](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_enableCameraAutoFocus_System_Boolean_) | Enables/Disables automatic facial recognition.                           |
| [setCameraFocusPosition](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_setCameraFocusPosition_System_Int32_System_Int32_) | Sets camera focus.                           |
| [enableCameraTorch](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_enableCameraTorch_System_Boolean_) | Enables/Disables flash.                           |
| [setSystemVolumeType](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_setSystemVolumeType_trtc_TXSystemVolumeType_) | Sets the system volume type to use during calls. |
| [setAudioRoute](https://comm.qq.com/en-trtc/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_setAudioRoute_trtc_TXAudioRoute_) | Sets the audio route. |

[](id:music)

## Specific Music and Voice Effect APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setVoiceReverbType](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setVoiceReverbType_trtc_TXVoiceReverbType_) | Sets the voice change effects (karaoke, room, hall, low and deep, resonant, etc.) |
| [setMusicObserver](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicObserver_System_Int32_trtc_ITXMusicPlayObserver_) | Sets the callback of the playback progress of background music. |
| [startPlayMusic](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_startPlayMusic_trtc_AudioMusicParam_) | Starts playing background music. |
| [stopPlayMusic](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_stopPlayMusic_System_Int32_) | Stops playing background music. |
| [pausePlayMusic](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_pausePlayMusic_System_Int32_) | Pauses background music. |
| [resumePlayMusic](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_resumePlayMusic_System_Int32_) | Resumes playing background music. |
| [setMusicPublishVolume](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicPublishVolume_System_Int32_System_Int32_) | Sets the remote playback volume of background music, i.e., the volume heard by remote users. |
| [setMusicPlayoutVolume](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicPlayoutVolume_System_Int32_System_Int32_) | Sets the local playback volume of background music. |
| [setAllMusicVolume](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setAllMusicVolume_System_Int32_) | Sets the local and remote playback volume of background music. |
| [setMusicPitch](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicPitch_System_Int32_System_Double_) | Changes the pitch of background music. |
| [setMusicSpeedRate](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicSpeedRate_System_Int32_System_Double_) | Changes the playback speed of background music. |
| [getMusicCurrentPosInMS](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#methods) | Gets the playback progress (ms) of background music. |
| [seekMusicToPosInMS](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_seekMusicToPosInMS_System_Int32_System_Int32_) | Sets the playback progress (ms) of background music. |
| [getMusicDurationInMS](https://comm.qq.com/en-trtc/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_getMusicDurationInMS_System_String_) | Gets the length (ms) of the background music file. |
