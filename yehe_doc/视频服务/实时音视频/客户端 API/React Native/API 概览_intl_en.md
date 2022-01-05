## TRTCCloud

### Basic APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#sharedInstance) | Creates a `TRTCCloud` singleton. |
| [destroySharedInstance](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#destroySharedInstance) | Terminates a `TRTCCloud` singleton. |
| [registerListener](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#registerListener) | Registers a listener. |
| [unRegisterListener](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#unRegisterListener) | Unregisters a listener. |

### Room APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#enterRoom) | Enters a room. If the room does not exist, the system will create one.           |
| [exitRoom](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#exitRoom) | Leaves a room.                                                   |
| [switchRole](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#switchRole) | Switches roles. This API works only in live streaming scenarios (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [setDefaultStreamRecvMode](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setDefaultStreamRecvMode) | Sets the audio/video data receiving mode, which must be set before room entry to take effect.           |
| [connectOtherRoom](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#connectOtherRoom) | Requests a cross-room call (anchor competition).          |
| [disconnectOtherRoom](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#disconnectOtherRoom) | Exits a cross-room call.                                               |
| [switchRoom](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#switchRoom) | Switches rooms.         |



### CDN APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startPublishing) | Starts publishing to Tencent Cloud’s live streaming CDN.      |
| [stopPublishing](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopPublishing) | Stops publishing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startPublishCDNStream) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor.      |
| [stopPublishCDNStream](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopPublishCDNStream) | Stops relaying to non-Tencent Cloud addresses.      |
| [setMixTranscodingConfig](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setMixTranscodingConfig) | Sets On-Cloud MixTranscoding parameters.      |


### Video APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [muteLocalVideo](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#muteLocalVideo) | Pauses/Resumes publishing local video data.                                |
| [startRemoteView](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startRemoteView) | Starts playing the video of a remote user.                                        |
| [stopRemoteView](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopRemoteView) | Stops playing and pulling the video of a remote user.   |
| [muteRemoteVideoStream](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#muteRemoteVideoStream) | Pauses/Resumes receiving the video of a remote user.                              |
| [muteAllRemoteVideoStreams](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#muteAllRemoteVideoStreams) | Pauses/Resumes receiving the videos of all remote users.                                |
| [setVideoEncoderParam](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setVideoEncoderParam) | Sets video encoder parameters.                                     |
| [setNetworkQosParam](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setNetworkQosParam) | Sets video preference.                                       |
| [setVideoEncoderRotation](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setVideoEncoderRotation) | Sets the rotation of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setVideoEncoderMirror](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setVideoEncoderMirror) | Sets the mirror mode of encoded images. |
| [setGSensorMode](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setGSensorMode) | Sets the adaptation mode of the G-sensor. | 
| [setVideoMuteImage](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setVideoMuteImage) | Sets the image to display when local video publishing is paused.                                    |

### Audio APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalAudio](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startLocalAudio) | Enables local audio capturing and publishing.                                   |
| [stopLocalAudio](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopLocalAudio) | Disables local audio capturing and publishing.                                   |
| [muteLocalAudio](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#muteLocalAudio) | Mutes/Unmutes the local user.                                    |
| [setAudioRoute](https://comm.qq.com/trtc-react-native/api/classes/tx_device_manager.default.html#setAudioRoute) | Sets the audio route.                                               |
| [muteRemoteAudio](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#muteRemoteAudio) | Mutes/Unmutes a remote user.                          |
| [muteAllRemoteAudio](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#muteAllRemoteAudio) | Mutes/Unmutes all remote users.                                |
| [setAudioCaptureVolume](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setAudioCaptureVolume) | Sets the SDK capturing volume.                                          |
| [getAudioCaptureVolume](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#getAudioCaptureVolume) | Gets the SDK capturing volume.                 |
| [setAudioPlayoutVolume](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setAudioPlayoutVolume) | Sets the SDK playback volume.                                          |
| [getAudioPlayoutVolume](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#getAudioPlayoutVolume) | Gets the SDK playback volume.                 |
| [enableAudioVolumeEvaluation](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#enableAudioVolumeEvaluation) | Enables the volume reminder.                                           |
| [startAudioRecording](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startAudioRecording) | Starts audio recording.                                                   |
| [stopAudioRecording](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopAudioRecording) | Stops audio recording.                                                   |


### Device management APIs

| API                                             | Description                                                         |
|-----|-----|
| [getDeviceManager](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#getDeviceManager) | Gets the device manager. For API details, see the document on [device management](https://comm.qq.com/trtc-react-native/api/classes/tx_device_manager.default.html). |


### Beauty filter APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#getBeautyManager) | Gets the beauty filter manager. For API details, see the document on [beauty filter management](https://comm.qq.com/trtc-react-native/api/classes/tx_beauty_manager.default.html). |
| [setWatermark](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setWatermark) | Adds a watermark.                                                   |


### Music and audio effect APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#getAudioEffectManager) | Gets the audio effect manager `TXAudioEffectManager`, which is used to manage background music, short audio effects, and voice changing effects. For API details, see the document on [audio effect management](https://comm.qq.com/trtc-react-native/api/classes/tx_audio_effect_manager.default.html). |

### Network testing APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startSpeedTest) | Starts network speed testing, which should be avoided during video calls to ensure call quality. |
| [stopSpeedTest](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopSpeedTest) | Stops server speed testing.                                             |


### Log APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#getSDKVersion) | Gets the SDK version.         |
| [setLogLevel](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setLogLevel) | Sets the log output level.         |
| [setLogDirPath](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setLogDirPath) | Changes the path to save logs.         |
| [setLogCompressEnabled](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setLogCompressEnabled) | Enables/Disables local log compression.         |
| [setConsoleEnabled](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setConsoleEnabled) | Enables/Disables console log printing.  |


## TRTCCloudListener

TRTC callback APIs

### Error and warning event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onError) | Error callback. This indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI reminders should be sent to users if necessary.  |
| [onWarning](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onWarning) | Warning callback. This callback alerts you to non-serious problems such as stutter or recoverable decoding failure. |


### Room event callback APIs

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onEnterRoom) | Callback for room entry                  |
| [onExitRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onExitRoom) | Callback for room exit                |
| [onSwitchRole](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onSwitchRole) | Callback for role switching                |
| [onConnectOtherRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onConnectOtherRoom) | Callback of the result of requesting a cross-room call (anchor competition)         |
| [onDisConnectOtherRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onDisConnectOtherRoom) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onSwitchRoom) | Callback of the result of room switching (`switchRoom`)               |

### User event callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onRemoteUserEnterRoom) | Callback for the entry of a remote user                |
| [onRemoteUserLeaveRoom](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onRemoteUserLeaveRoom) | Callback for the exit of a remote user                |
| [onUserVideoAvailable](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onUserVideoAvailable) | Callback of whether a remote user has a playable primary image (usually the image of the camera) |
| [onUserSubStreamAvailable](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onUserSubStreamAvailable) | Callback of whether a remote user has a playable substream image (usually the screen sharing image) |
| [onUserAudioAvailable](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onUserAudioAvailable) | Callback of whether a remote user has playable audio data        |
| [onFirstVideoFrame](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onFirstVideoFrame) | Callback for rendering the first video frame of the local user or a remote user           |
| [onFirstAudioFrame](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onFirstAudioFrame) | Callback for playing the first audio frame of a remote user. No notifications are sent for local audio. |
| [onSendFirstLocalVideoFrame](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onSendFirstLocalVideoFrame) | Callback for sending the first local video frame                           |
| [onSendFirstLocalAudioFrame](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onSendFirstLocalAudioFrame) | Callback for sending the first local audio frame                     |

### Callback APIs for background music playback

Callback APIs for background music playback

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverStart) | Callback for starting music |
| [onMusicObserverPlayProgress](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverPlayProgress) | Callback of the music playback progress |
| [onMusicObserverComplete](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onMusicObserverComplete) | Callback for ending music |

### Callback APIs for statistics on network quality and technical metrics

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onNetworkQuality) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the quality of current upstream and downstream data transfer. |
| [onStatistics](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onStatistics) | Callback of statistics on technical metrics                          |


### Server event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onConnectionLost) | Callback for the disconnection of the SDK from the server                                      |
| [onTryToReconnect](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onTryToReconnect) | Callback for the SDK trying to reconnect to the server                                   |
| [onConnectionRecovery](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onConnectionRecovery) | Callback for the reconnection of the SDK to the server                                     |
| [onSpeedTest](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onSpeedTest) | Callback of server speed test results. The SDK tests the speed of multiple server addresses, and the result of each test is returned through this callback. |


### Hardware event callback APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onCameraDidReady) | Callback for the camera being ready                                             |
| [onMicDidReady](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onMicDidReady) | Callback for the mic being ready                         |
| [onUserVoiceVolume](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onUserVoiceVolume) | Callback of volume, including the volume of each `userId` and the total remote volume |

### Callback APIs for CDN relayed push

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishing) | Callback for starting publishing to Tencent Cloud’s live streaming CDN. This callback is triggered by the `startPublishing()` API in [TRTCCloud](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#startPublishing). |
| [onStopPublishing](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onStopPublishing) | Callback for stopping publishing to Tencent Cloud’s live streaming CDN. This callback is triggered by the `stopPublishing()` API in [TRTCCloud](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#stopPublishing). |
| [onStartPublishCDNStream](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onStartPublishCDNStream) | Callback for starting relayed push to CDNs |
| [onStopPublishCDNStream](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onStopPublishCDNStream) | Callback for stopping relayed push to CDNs |
| [onSetMixTranscodingConfig](https://comm.qq.com/trtc-react-native/api/enums/trtc_cloud.TRTCCloudListener.html#onSetMixTranscodingConfig) | Callback for setting On-Cloud MixTranscoding parameters. This callback is triggered by the `setMixTranscodingConfig()` API in [TRTCCloud](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud.default.html#setMixTranscodingConfig). |

## Definitions of Key Types

| Class                                                         | Description                                    |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCCloudDef](https://comm.qq.com/trtc-react-native/api/classes/trtc_cloud_def.TRTCCloudDef.html) | Variables of key type definitions                              |
| [TRTCParams](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCParams) | Room entry parameters                              |
| [TRTCSwitchRoomConfig](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCSwitchRoomConfig) | Room switching parameters                                  |
| [TRTCVideoEncParam](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCVideoEncParam) | Video encoding parameters                              |
| [TRTCNetworkQosParam](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCNetworkQosParam) | QoS control parameters                                  |
| [TRTCRenderParams](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCRenderParams) | Remote video parameters |
| [TRTCMixUser](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCMixUser) | Position of the image of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCTranscodingConfig) | On-Cloud MixTranscoding configuration                           |
| [TXVoiceChangerType](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TXVoiceChangerType) | Voice changing effects (little girl, middle-aged man, metal, punk, etc.) |
| [TXVoiceReverbType](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TXVoiceReverbType) | Reverb effects (karaoke, room, hall, low and deep, resonant, etc.) |
| [AudioMusicParam](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#AudioMusicParam) | Parameters for music and audio effect setting APIs |
| [TRTCAudioRecordingParams](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCAudioRecordingParams) | Audio recording parameters |
| [TRTCPublishCDNParam](https://comm.qq.com/trtc-react-native/api/modules/trtc_cloud_def.html#TRTCPublishCDNParam) | CDN relaying parameters |
