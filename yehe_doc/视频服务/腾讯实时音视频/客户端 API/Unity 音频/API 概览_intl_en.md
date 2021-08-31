### Basic APIs

| API                                                          | Description                            |
| ------------------------------------------------------------ | --------------------------------- |
| [getTRTCShareInstance](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getTRTCShareInstance) | Creates a `TRTCCloud` singleton.             |
| [destroyTRTCShareInstance](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_destroyTRTCShareInstance) | Releases a `TRTCCloud` singleton.        |
| [addCallback](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_addCallback_trtc_ITRTCCloudCallback_) | Sets the callback API `TRTCCloudCallback`. |
| [removeCallback](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_removeCallback_trtc_ITRTCCloudCallback_) | Removes event callback.                    |

### Room APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_enterRoom_trtc_TRTCParams__trtc_TRTCAppScene_) | Enters a room. If the room does not exist, the system will create one automatically.           |
| [exitRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_exitRoom) | Exits a room.                                                   |
| [switchRole](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_switchRole_trtc_TRTCRoleType_) | Switches roles. This API works only in live streaming scenarios (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [setDefaultStreamRecvMode](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setDefaultStreamRecvMode_System_Boolean_System_Boolean_) | Sets the audio/video data receiving mode, which must be set before room entry to take effect.           |
| [connectOtherRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_connectOtherRoom_System_String_) | Requests a cross-room call (anchor competition).                                    |
| [disconnectOtherRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_disconnectOtherRoom) | Exits a cross-room call.                                               |


### CDN APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startPublishing_System_String_trtc_TRTCVideoStreamType_) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopPublishing) | Stops pushing to Tencent Cloud’s live streaming CDN. |


### Audio APIs

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [startLocalAudio](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startLocalAudio_trtc_TRTCAudioQuality_) | Enables local audio capturing and upstream data transfer.          |
| [stopLocalAudio](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopLocalAudio) | Disables local audio capturing and upstream data transfer.          |
| [muteLocalAudio](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteLocalAudio_System_Boolean_) | Mutes/Unmutes local audio.           |
| [muteRemoteAudio](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteRemoteAudio_System_String_System_Boolean_) | Mutes/Unmutes a specified remote user. |
| [muteAllRemoteAudio](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_muteAllRemoteAudio_System_Boolean_) | Mutes/Unmutes all remote users.       |
| [setRemoteAudioVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setRemoteAudioVolume_System_String_System_Int32_) | Sets the playback volume of a remote user.        |
| [setAudioCaptureVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setAudioCaptureVolume_System_Int32_) | Sets the SDK capturing volume.                 |
| [getAudioCaptureVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getAudioCaptureVolume) | Gets the SDK capturing volume.                 |
| [setAudioPlayoutVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setAudioPlayoutVolume_System_Int32_) | Sets the SDK playback volume.                 |
| [getAudioPlayoutVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getAudioPlayoutVolume) | Gets the SDK playback volume.                 |
| [enableAudioVolumeEvaluation](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_enableAudioVolumeEvaluation_System_UInt32_) | Enables volume reminders.                  |
| [startAudioRecording](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startAudioRecording_trtc_TRTCAudioRecordingParams__) | Starts audio recording.                          |
| [stopAudioRecording](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopAudioRecording) | Stops audio recording.                          |

### Device management APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getDeviceManager](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getDeviceManager) | Gets the device management module. For details, please see [Specific Device Management APIs](#equipment). |


### Music and voice effect API

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getAudioEffectManager) | Gets the audio effect management class `TXAudioEffectManager`, which is used to manage background music, short audio effects, and voice effects. For details, please see [Specific Music and Voice Effect APIs](#music). |

### Custom capturing and rendering APIs

| API                                                          | Description                            |
| ------------------------------------------------------------ | ------------------------------- |
| [enableCustomAudioCapture](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_enableCustomAudioCapture_System_Boolean_) | Enables custom audio capturing.        |
| [sendCustomAudioData](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_sendCustomAudioData_trtc_TRTCAudioFrame_) | Sends captured audio to the SDK. |

### Custom message sending APIs

| API                                                          | Description                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [sendSEIMsg](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_sendSEIMsg_System_Byte___System_Int32_System_Int32_) | Embeds small-volume custom data in video frames. |


### Network testing APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startSpeedTest_System_Int32_System_String_System_String_) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopSpeedTest) | Stops server speed testing.                                             |


### Log APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_getSDKVersion) | Gets the SDK version.         |
| [setLogLevel](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLogLevel_trtc_TRTCLogLevel_) | Sets the log output level.         |
| [setLogDirPath](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLogDirPath_System_String_) | Changes the path to save logs.          |
| [setLogCompressEnabled](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_setLogCompressEnabled_System_Boolean_) | Enables/Disables console log printing. |
| [callExperimentalAPI](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_callExperimentalAPI_System_String_) | Calls the experimental API. |



## TRTCCloudCallback

Callback APIs for Tencent Cloud’s audio call feature.

### Error and warning event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onError_trtc_TXLiteAVError_String_IntPtr_) | Error callback. This indicates that the SDK encountered an irrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending on the situation. |
| [onWarning](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onWarning_trtc_TXLiteAVWarning_String_IntPtr_) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onEnterRoom_System_Int32_) | Callback of room entry                  |
| [onExitRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onExitRoom_System_Int32_) | Callback of room exit                |
| [onSwitchRole](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSwitchRole_trtc_TXLiteAVError_String_) | Callback of role switching                |
| [onConnectOtherRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onConnectOtherRoom_System_String_trtc_TXLiteAVError_System_String_) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisConnectOtherRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onDisconnectOtherRoom_trtc_TXLiteAVError_System_String_) | Callback of the result of ending a cross-room call (anchor competition) |


### User event callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------ |
| [onRemoteUserEnterRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onRemoteUserEnterRoom_String_) | Callback of the entry of a user                              |
| [onRemoteUserLeaveRoom](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onRemoteUserLeaveRoom_String_System_Int32_) | Callback of the exit of a user                              |
| [onUserAudioAvailable](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onUserAudioAvailable_String_System_Boolean_) | Callback of whether a remote user has playable audio               |
| [onFirstAudioFrame](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onFirstAudioFrame_String_) | Callback of the playing of the first audio frame of a remote user. No notifications are sent for local audio. |
| [onSendFirstLocalAudioFrame](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSendFirstLocalAudioFrame) | Callback of the sending of the first local audio frame                     |


### Callback APIs for statistics on network quality and technical metrics

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onNetworkQuality_trtc_TRTCQualityInfo_trtc_TRTCQualityInfo___UInt32_) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the current upstream and downstream data transfer. |
| [onStatistics](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStatistics_trtc_TRTCStatistics_) | Callback of statistics on technical metrics                                           |


### Server event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onConnectionLost) | Callback of the disconnection of the SDK from the server                                      |
| [onTryToReconnect](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onTryToReconnect) | Callback of the SDK trying to connect to the server again                                   |
| [onConnectionRecovery](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onConnectionRecovery) | Callback of the reconnection of the SDK to the server                                     |
| [onSpeedTest](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onSpeedTest_trtc_TRTCSpeedTestResult_System_Int32_System_Int32_) | Callback of server speed test. The SDK tests the speed of multiple server addresses, and the test result of each IP address is returned through this callback. |


### Hardware event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onMicDidReady](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onMicDidReady) | Callback of the camera being ready                                             |
| [onUserVoiceVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onUserVoiceVolume_trtc_TRTCVolumeInfo___UInt32_UInt32_) | Callback of volume, including the volume of each `userId` and the total remote volume |

[](id:reback)

### Custom message receiving callback APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------- |
| [onRecvSEIMsg](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onRecvSEIMsg_String_Byte___UInt32_) | Callback of the receipt of an SEI message |

[](id:cdn)

### Callback APIs for CDN relayed push

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStartPublishing_System_Int32_String_) | Callback of starting to push to Tencent Cloud’s live streaming CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_startPublishing_System_String_trtc_TRTCVideoStreamType_) |
| [onStopPublishing](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloudCallback.html#trtc_ITRTCCloudCallback_onStopPublishing_System_Int32_String_) | Callback of stopping pushing to Tencent Cloud’s live streaming CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](https://testcomm.qq.com/trtc/api/api/trtc.ITRTCCloud.html#trtc_ITRTCCloud_stopPublishing) |

[](id:key)

## Definitions of Key Classes

| Class                                                         | Description                                                |
| ------------------------------------------------------------ | --------------------------------------------------- |
| [TRTCParams](https://testcomm.qq.com/trtc/api/api/trtc.TRTCParams.html) | Room entry parameters                                          |
| [TRTCSwitchRoomConfig](https://testcomm.qq.com/trtc/api/api/trtc.TRTCSwitchRoomConfig.html) | Room switching parameters                                  |
| [TRTCNetworkQosParam](https://testcomm.qq.com/trtc/api/api/trtc.TRTCNetworkQosParam.html) | QoS control parameters                                  |
| [TXVoiceReverbType](https://testcomm.qq.com/trtc/api/api/trtc.TXVoiceReverbType.html) | Reverb effects (karaoke, room, hall, low and deep, resonant, etc.) |
| [AudioMusicParam](https://testcomm.qq.com/trtc/api/api/trtc.AudioMusicParam.html) | Parameters for music and voice effect setting APIs                             |
| [TRTCAudioRecordingParams](https://testcomm.qq.com/trtc/api/api/trtc.TRTCAudioRecordingParams.html) | Audio recording parameters                                          |

[](id:equipment)

## Specific Device Management APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ------------------------------ |
| [setSystemVolumeType](https://testcomm.qq.com/trtc/api/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_setSystemVolumeType_trtc_TXSystemVolumeType_) | Sets the system volume type to use during calls. |
| [setAudioRoute](https://testcomm.qq.com/trtc/api/api/trtc.ITXDeviceManager.html#trtc_ITXDeviceManager_setAudioRoute_trtc_TXAudioRoute_) | Sets the audio route.                 |

[](id:music)

## Specific Music and Voice Effect APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setVoiceReverbType](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setVoiceReverbType_trtc_TXVoiceReverbType_) | Sets the voice change effects (karaoke, room, hall, low and deep, resonant, etc.)    |
| [setMusicObserver](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicObserver_System_Int32_trtc_ITXMusicPlayObserver_) | Sets the playback progress of background music.                             |
| [startPlayMusic](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_startPlayMusic_trtc_AudioMusicParam_) | Starts playing background music.                                           |
| [stopPlayMusic](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_stopPlayMusic_System_Int32_) | Stops playing background music.                                           |
| [pausePlayMusic](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_pausePlayMusic_System_Int32_) | Pauses background music.                                           |
| [resumePlayMusic](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_resumePlayMusic_System_Int32_) | Resumes playing background music.                                           |
| [setMusicPublishVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicPublishVolume_System_Int32_System_Int32_) | Sets the remote playback volume of background music, i.e., the volume heard by remote users. |
| [setMusicPlayoutVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicPlayoutVolume_System_Int32_System_Int32_) | Sets the local playback volume of background music. |
| [setAllMusicVolume](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setAllMusicVolume_System_Int32_) | Sets the local and remote playback volume of background music.                     |
| [setMusicPitch](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicPitch_System_Int32_System_Double_) | Changes the pitch of background music.                                     |
| [setMusicSpeedRate](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_setMusicSpeedRate_System_Int32_System_Double_) | Changes the playback speed of background music.                                     |
| [getMusicCurrentPosInMS](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#methods) | Gets the playback progress (ms) of background music.                     |
| [seekMusicToPosInMS](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_seekMusicToPosInMS_System_Int32_System_Int32_) | Sets the playback progress (ms) of background music.                         |
| [getMusicDurationInMS](https://testcomm.qq.com/trtc/api/api/trtc.ITXAudioEffectManager.html#trtc_ITXAudioEffectManager_getMusicDurationInMS_System_String_) | Gets the length (ms) of the background music file.                          |
