## TRTCCloud

### Basic methods

| API                                                          | Description                  |
| ------------------------------------------------------------ | --------------------- |
| [sharedInstance](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sharedInstance.html) | Creates a TRTCCloud singleton. |
| [destroySharedInstance](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/destroySharedInstance.html) | Destroys a TRTCCloud singleton.  |
| [registerListener](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/registerListener.html) | Subscribes to events.        |
| [unRegisterListener](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/unRegisterListener.html) | Unsubscribes from events.         |


### Room APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enterRoom.html) | Enters a room. If the room does not exist. The system will create one automatically.           |
| [exitRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/exitRoom.html) | Exits the room.                                                   |
| [switchRole](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/switchRole.html) | Switches roles. This API works only in the live streaming modes (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [setDefaultStreamRecvMode](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setDefaultStreamRecvMode.html) | Sets the audio/video data receiving mode. The parameter takes effect only if it is set before room entry.           |
| [connectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/connectOtherRoom.html) | Requests a cross-room call (anchor competition).                                    |
| [disconnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/disconnectOtherRoom.html) | Exits a cross-room call.                                               |
| [switchRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/switchRoom.html) | Switches rooms.                                                   |



### CDN APIs

| API                                                          | Description |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishing.html) | Starts pushing to Tencent Cloud’s LVB CDN. |
| [stopPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishing.html) | Stops pushing to Tencent Cloud’s LVB CDN. |
| [startPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startPublishCDNStream.html) | Starts relaying to the live streaming CDNs of non-Tencent Cloud vendors. |
| [stopPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopPublishCDNStream.html) | Stops relaying to the live streaming CDNs of non-Tencent Cloud vendors.      |
| [setMixTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setMixTranscodingConfig.html) | Sets On-Cloud MixTranscoding parameters.      |


### Video APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalPreview](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startLocalPreview.html) | Enables preview of the local video.                                     |
| [stopLocalPreview](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalPreview.html) | Stops local video capture and preview.                                     |
| [muteLocalVideo](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteLocalVideo.html) | Pauses/Resumes pushing local video data.                                |
| [startRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startRemoteView.html) | Starts displaying remote video images.                                       |
| [stopRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopRemoteView.html) | Stops displaying the video image of a remote user and pulling the user’s video stream.   |
| [stopAllRemoteView](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopAllRemoteView.html) | Stops displaying the video images of all users and pulling their video streams.  |
| [muteRemoteVideoStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteRemoteVideoStream.html) | Pauses/Resumes receiving a specified remote video stream.                              |
| [muteAllRemoteVideoStreams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteAllRemoteVideoStreams.html) | Pauses/Resumes receiving all remote video streams.                                |
| [setVideoEncoderParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderParam.html) | Sets video encoder parameters.                                     |
| [setNetworkQosParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setNetworkQosParam.html) | Sets QoS control parameters.                                       |
| [setLocalRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLocalRenderParams.html) | Sets the rendering mode of the local image.                                     |
| [setRemoteRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setRemoteRenderParams.html) | Sets remote image parameters.                                       |
| [setVideoEncoderRotation](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderRotation.html) | Sets the rotation degree of encoded video images, i.e., images presented to remote users and recorded by the server.  |
| [setVideoEncoderMirror](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoEncoderMirror.html) | Sets the mirror mode for encoded images.                               |
| [setGSensorMode](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setGSensorMode.html) |  Sets the adaptation mode of the G-sensor.                                     |
| [enableEncSmallVideoStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enableEncSmallVideoStream.html) | Enables the dual-channel (big and small images) encoding mode.                                   |
| [setRemoteVideoStreamType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setRemoteVideoStreamType.html) | Sets whether to view the big or small image of a specified `uid`.                          |
| [snapshotVideo](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/snapshotVideo.html) | Takes a video screenshot.                                               |


### Audio APIs

| API                                                          | Description                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [startLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startLocalAudio.html) | Enables local audio capture and upstream data transfer.           |
| [stopLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalAudio.html) | Disables local audio capture and upstream data transfer.           |
| [muteLocalAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteLocalAudio.html) | Mutes/Unmutes the local audio.            |
| [setVideoMuteImage](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setVideoMuteImage.html) | Sets the image to be pushed when local video pushing is paused. |
| [setAudioRoute](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager/setAudioRoute.html) | Sets the audio route.                       |
| [muteRemoteAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteRemoteAudio.html) | Mutes/Unmutes the audio of a specified remote user.  |
| [muteAllRemoteAudio](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/muteAllRemoteAudio.html) | Mutes/Unmutes all users' audio.        |
| [setAudioCaptureVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setAudioCaptureVolume.html) | Sets the SDK capture volume.                  |
| [getAudioCaptureVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioCaptureVolume.html) | Gets the SDK capture volume.                  |
| [setAudioPlayoutVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setAudioPlayoutVolume.html) | Sets the SDK playback volume.                  |
| [getAudioPlayoutVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioPlayoutVolume.html) | Gets the SDK playback volume.                  |
| [enableAudioVolumeEvaluation](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/enableAudioVolumeEvaluation.html) | Enables volume reminders.                   |
| [startAudioRecording](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startAudioRecording.html) | Starts audio recording.                           |
| [stopAudioRecording](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopAudioRecording.html) | Stops audio recording.                           |
| [setSystemVolumeType](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager/setSystemVolumeType.html) | Sets the system volume type used during calls.       |


### Device management APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getDeviceManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getDeviceManager.html) | Gets the device management module. For details, see the document on [device management](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_device_manager/TXDeviceManager-class.html). |


### Beauty filter APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getBeautyManager.html) | Gets the beauty filter management object. For details, see the document on [beauty filter management](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html). |
| [setWatermark](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setWatermark.html) | Adds watermarks.                                                   |


### Music and voice effect APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getAudioEffectManager.html) | Gets the audio effect management class `TXAudioEffectManager`, which is used to manage background music, short audio effects and voice effects. For details, see the document on [audio effect management](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html). |

### Custom message sending APIs

| API                                                          | Description                                 |
| ------------------------------------------------------------ | ------------------------------------ |
| [sendCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sendCustomCmdMsg.html) | Sends a custom message to all users in the room.     |
| [sendSEIMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/sendSEIMsg.html) | Embeds small-volume custom data in video frames. |


### Network testing APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startSpeedTest.html) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a call. |
| [stopSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopSpeedTest.html) |  Stops server speed testing.                                             |


### Log APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/getSDKVersion.html) | Gets the SDK version.         |
| [setLogLevel](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogLevel.html) | Sets the log output level.         |
| [setLogDirPath](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogDirPath.html) | Changes the path to save logs.          |
| [setLogCompressEnabled](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setLogCompressEnabled.html) | Enables/Disables local log compression. |
| [setConsoleEnabled](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/setConsoleEnabled.html) | Enables/Disables console log printing.  |


## TRTCCloudListener

Callback APIs for Tencent Cloud’s video call feature

### Error and warning event callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onError) | Error callback. This indicates that the SDK encountered an irrecoverable error. Such errors must be listened for, and UI messages should be displayed to users if necessary. |
| [onWarning](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onWarning) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onEnterRoom) | Callback of room entry                  |
| [onExitRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onExitRoom) | Callback of room exit                |
| [onSwitchRole](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSwitchRole) | Callback of role switching                |
| [onConnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onConnectOtherRoom) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisConnectOtherRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onDisConnectOtherRoom) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSwitchRoom) | Callback of the result of room switching (`switchRoom`)  |

### User event callback APIs

| API                                                          | Description                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onRemoteUserEnterRoom) | Callback of the entry of a user                                   |
| [onRemoteUserLeaveRoom](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onRemoteUserLeaveRoom) | Callback of the exit of a user                                   |
| [onUserVideoAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onUserVideoAvailable) | Callback of whether a remote user has a playable primary image (usually the image of the camera)   |
| [onUserSubStreamAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onUserSubStreamAvailable) | Callback of whether a remote user has a playable secondary image (usually the screen sharing image) |
| [onUserAudioAvailable](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onUserAudioAvailable) | Callback of whether a remote user has playable audio data                     |
| [onFirstVideoFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onFirstVideoFrame) | Callback of the rendering of the first video frame of the local user or remote users                      |
| [onFirstAudioFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onFirstAudioFrame) | Callback of the playing of the first audio frame of remote users. No notifications are sent for local audio       |
| [onSendFirstLocalVideoFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSendFirstLocalVideoFrame) | Callback of the sending of the first local video frame                           |
| [onSendFirstLocalAudioFrame](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSendFirstLocalAudioFrame) | Callback of the sending of the first local audio frame                           |

### Callback APIs for background music playback

Callback APIs for background music playback

| API                                                          | Description                     |
| ------------------------------------------------------------ | ------------------------ |
| [onMusicObserverStart](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onMusicObserverStart) | Callback of starting music playback |
| [onMusicObserverPlayProgress](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onMusicObserverPlayProgress) | Callback of the music playback progress |
| [onMusicObserverComplete](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onMusicObserverComplete) | Callback of ending music playback |

### Callback APIs for statistics on network quality and technical metrics

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onNetworkQuality) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the quality of current upstream and downstream data transfer. |
| [onStatistics](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onStatistics) | Callback of statistics on technical metrics                                           |


### Server event callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onConnectionLost) | Callback of the disconnection of the SDK from the server                                     |
| [onTryToReconnect](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onTryToReconnect) | Callback of the SDK trying to connect to the server again                                   |
| [onConnectionRecovery](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onConnectionRecovery) | Callback of the reconnection of the SDK to the server                                     |
| [onSpeedTest](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSpeedTest) | Callback of server speed test results. The SDK tests the speed of multiple server IPs, and the result of each test is returned through this callback. |


### Hardware event callback APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onCameraDidReady) | Callback of the camera being ready                                             |
| [onMicDidReady](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onMicDidReady) | Callback of the mic being ready                                             |
| [onUserVoiceVolume](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onUserVoiceVolume) | Callback of volume, including the volume of each `userId` and the total remote volume level |


### Custom message receiving callbacks

| API                                                          | Description                  |
| ------------------------------------------------------------ | --------------------- |
| [onRecvCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onRecvCustomCmdMsg) | Callback of the receipt of a custom message  |
| [onMissCustomCmdMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onMissCustomCmdMsg) | Callback of the missing of a custom message  |
| [onRecvSEIMsg](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onRecvSEIMsg) | Callback of the receipt of an SEI message |


### Callback APIs for CDN relayed push

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onStartPublishing) | Callback of starting to push to Tencent Cloud’s LVB CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud-class.html#startPublishing) |
| [onStopPublishing](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onStopPublishing) | Callback of stopping to push to Tencent Cloud’s LVB CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud-class.html#stopPublishing) |
| [onStartPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onStartPublishCDNStream) | Callback of completion of starting relayed push to CDNs                              |
| [onStopPublishCDNStream](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onStopPublishCDNStream) | Callback of completion of stopping relayed push to CDNs                              |
| [onSetMixTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSetMixTranscodingConfig) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `[TRTCCloud](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud-class.html#setMixTranscodingConfig) |


### Screenshot callback APIs

| API                                                          | Description             |
| ------------------------------------------------------------ | ---------------- |
| [onSnapshotComplete](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html#onSnapshotComplete) | Callback of the completion of a screenshot |


## Definitions of Key Classes

| Class                                                         | Description                                                |
| ------------------------------------------------------------ | --------------------------------------------------- |
| [TRTCCloudDef](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCCloudDef-class.html) | Key class definition variables                                  |
| [TRTCParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCParams-class.html) | Room entry parameters                                          |
| [TRTCSwitchRoomConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCSwitchRoomConfig-class.html) | Room switching parameters   |
| [TRTCVideoEncParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCVideoEncParam-class.html) | Video encoding parameters                                      |
| [TRTCNetworkQosParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCNetworkQosParam-class.html) | QoS control parameters                                  |
| [TRTCRenderParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCRenderParams-class.html) | Remote image parameters                                      |
| [TRTCMixUser](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCMixUser-class.html) | Position of the image of each channel in On-Cloud MixTranscoding                  |
| [TRTCTranscodingConfig](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCTranscodingConfig-class.html) | On-Cloud MixTranscoding configuration                              |
| [TXVoiceChangerType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TXVoiceChangerType-class.html) | Definitions of voice changing types (little girl, middle-aged man, heavy metal, foreigner, etc.)      |
| [TXVoiceReverbType](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TXVoiceReverbType-class.html) | Definitions of reverb effect types (KTV, small room, hall, deep voice, resonant voice, etc.) |
| [AudioMusicParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/AudioMusicParam-class.html) | Parameters for music and voice setting APIs                            |
| [TRTCAudioRecordingParams](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCAudioRecordingParams-class.html) | Audio recording parameters                                          |
| [TRTCPublishCDNParam](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud_def/TRTCPublishCDNParam-class.html) | CDN relayed push parameters                                      |
