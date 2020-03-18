## TRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.

**Main documentation address: [TRTC SDK for Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/index.html)**


### Creating TRTC object
```js
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
```

### Setting callbacks
```js
subscribeEvents = (rtcCloud) => {
    rtcCloud.on('onError', (errcode, errmsg) => {
    console.info('trtc_demo: onError :' + errcode + " msg" + errmsg);
    }); 
    rtcCloud.on('onEnterRoom', (elapsed) => {
    console.info('trtc_demo: onEnterRoom elapsed:' + elapsed);
    });
    rtcCloud.on('onExitRoom', (reason) => {
    console.info('onExitRoom: userenter reason:' + reason);
    });
};

subscribeEvents(this.rtcCloud);
```

### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) | Enters room. |
| [exitRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) | Exits room. |
| [switchRole](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [connectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#disconnectOtherRoom)| Ends cross-room co-anchoring. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview)| Enables preview of local video. |
| [stopLocalPreview](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopLocalPreview)| Disables local video capture and preview. |
| [muteLocalVideo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteLocalVideo)| Specifies whether to block local video image. |
| [startRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) | Starts displaying remote video image. |
| [stopRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteView)| Stops displaying remote video image. |
| [stopAllRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllRemoteView)| Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteVideoStream)| Suspends receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteVideoStreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setNetworkQosParam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode)| Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteViewFillMode)| Sets rendering mode of remote image. |
| [setLocalViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewRotation)| Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteViewRotation)| Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderRotation)| Sets direction of image output by video encoder (i.e., image viewed by remote user and recorded by server). |
| [setLocalViewMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewMirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderMirror)| Sets mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enableSmallVideoStream)| Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteVideoStreamType) | Selects whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setPriorRemoteVideoStreamType) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio)| Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopLocalAudio)| Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteLocalAudio) | Mutes local audio. |
| [muteRemoteAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio) | Mutes user's audio. |
| [muteAllRemoteAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteAudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enableAudioVolumeEvaluation)| Enables or disables volume reminder. |
| [startAudioRecording](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startAudioRecording) | Starts audio recording. |
| [stopAudioRecording](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAudioRecording) | Stops audio recording. |


### Camera API functions

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCameraDevicesList)| Gets list of cameras. |
| [setCurrentCameraDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentCameraDevice)| Sets the camera to be used. |
| [getCurrentCameraDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentCameraDevice)| Gets the currently used camera. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getMicDevicesList) | Gets list of mics. |
| [getCurrentMicDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDevice) | Gets the currently used mic. |
| [setCurrentMicDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDevice) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceVolume) | Gets current mic volume level. |
| [setCurrentMicDeviceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceVolume)| Sets mic volume level. |
| [getSpeakerDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getSpeakerDevicesList)| Gets list of speakers. |
| [getCurrentSpeakerDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDevice)| Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDevice) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerVolume) | Gets current speaker volume level. |
| [setCurrentSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerVolume) | Sets current speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [setBeautyStyle](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setWaterMark)| Sets watermark. |


### Secondary stream API functions

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteSubStreamView)| Starts rendering the secondary stream image of a remote user. |
| [stopRemoteSubStreamView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteSubStreamView) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteSubStreamViewFillMode) | Sets rendering mode of the secondary stream image. |
| [getScreenCaptureSources](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getScreenCaptureSources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#selectScreenCaptureTarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) | Starts screen sharing. |
| [pauseScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseScreenCapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeScreenCapture) | Resumes screen sharing. |
| [stopScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopScreenCapture) | Stops screen capture. |
| [setSubStreamEncoderParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSubStreamEncoderParam) | Sets encoding parameters for screen sharing. |
| [setSubStreamMixVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSubStreamMixVolume) | Sets audio mixing volume level of the secondary stream. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#sendCustomCmdMsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#sendSEIMsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#playBGM) | Starts background music. |
| [stopBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopBGM) | Stops background music. |
| [pauseBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseBGM)| Pauses background music. |
| [resumeBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeBGM) | Resumes background music. |
| [getBGMDuration](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getBGMDuration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPosition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMicVolumeOnMixing) | Sets mic volume level. This API is used to adjust the mic volume level when background music is played back. |
| [setBGMVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMVolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [startSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSystemAudioLoopback) | Enables system audio capture. |
| [stopSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSystemAudioLoopback) | Disables system audio capture. |
| [setSystemAudioLoopbackVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSystemAudioLoopbackVolume) | Sets system audio capture volume level. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSpeedTest)| Starts network speed test (do not test during a video call so as to avoid affecting call quality). |
| [stopSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSpeedTest) | Stops server speed test. |
| [startCameraDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startCameraDeviceTest) | Starts camera test. |
| [stopCameraDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopCameraDeviceTest) | Stops camera test. |
| [startMicDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startMicDeviceTest) | Starts mic test. |
| [stopMicDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopMicDeviceTest) | Stops mic test. |
| [startSpeakerDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSpeakerDeviceTest) | Starts speaker test. |
| [stopSpeakerDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSpeakerDeviceTest) | Stops speaker test. |


### MixTranscoding and CDN relayed push APIs

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig) | Starts (updates) On-Cloud MixTranscoding: this method uses the transcoding service of Tencent Cloud to combine multiple image channels into one channel. |
| [startPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPublishCDNStream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPublishCDNStream)| Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getSDKVersion)| Gets SDK version information. |
| [setLogLevel](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogLevel)| Sets log output level. |
| [setConsoleEnabled](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setConsoleEnabled)| Enables or disables console log printing. |
| [setLogDirPath](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogDirPath)| Sets log storage path. |
| [callExperimentalAPI](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#callExperimentalAPI) | Calls experimental API. |


## TRTCCallback @ TXLiteAVSDK

Callback API class for TRTC video call feature.

### General event callbacks

| API | Description |
|-----|-----|
| [onError](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onError) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onWarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom)| Callback of room entry. |
| [onExitRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) | Callback of room exit. |
| [onSwitchRole](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSwitchRole)| Callback of role switching. |
| [onConnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom)| Callback of the result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDisconnectOtherRoom)| Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRemoteUserEnterRoom)| A user enters the current room. |
| [onRemoteUserLeaveRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRemoteUserLeaveRoom)| A user exits the current room. |
| [onUserEnter](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserEnter)| Disused API: an anchor enters the current room. |
| [onUserExit](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserExit)| Disused API: an anchor exits the current room. |
| [onUserVideoAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserSubStreamAvailable)| Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable)| Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onFirstVideoFrame) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onFirstAudioFrame) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSendFirstLocalAudioFrame)| The first local audio frame data has been sent. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onNetworkQuality)| Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStatistics)| Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectionLost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTryToReconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectionRecovery)| The connection between SDK and server has been restored. |
| [onSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSpeedTest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onCameraDidReady)| Camera is ready. |
| [onMicDidReady](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onMicDidReady) | Mic is ready. |
| [onUserVoiceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVoiceVolume)| Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDeviceChange) | Callback of local device connection and disconnection. |
| [onTestMicVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTestMicVolume) | Callback of mic volume level in test. |
| [onTestSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTestSpeakerVolume) | Callback of speaker volume level in test. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRecvCustomCmdMsg)| Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onMissCustomCmdMsg)| Callback of loss of a custom message. |
| [onRecvSEIMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRecvSEIMsg)| Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStartPublishCDNStream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStopPublishCDNStream)| Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSetMixTranscodingConfig)| Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureCovered)| This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureStarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCapturePaused)| This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureResumed)| This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureStoped)| This callback will be returned by the SDK when screen sharing is stopped. |


### Background audio mixing event callbacks

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMBegin) | Starts the playback of background music. |
| [onPlayBGMProgress](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMProgress)| Progress of background music playback. |
| [onPlayBGMComplete](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMComplete) | Ends the playback of background music. |


## Definitions of Key Classes
### Key classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)| Room entry parameters. |
| [TRTCVideoEncParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCVideoEncParam.html) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCNetworkQosParam.html) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCQualityInfo.html)| Video quality. |
| [TRTCVolumeInfo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCVolumeInfo.html) | Volume level. |
| [TRTCSpeedTestResult](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCSpeedTestResult.html)| Network speed test result. |
| [TRTCMixUser](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCMixUser.html)| Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCTranscodingConfig.html)| On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCPublishCDNParam.html)| CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCAudioRecordingParams.html)| Audio recording parameters. |
| [TRTCLocalStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCLocalStatistics.html)| Local audio/video statistics. |
| [TRTCRemoteStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCRemoteStatistics.html) | Remote audio/video statistics. |
| [TRTCStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCStatistics.html)| Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoResolution)| Video resolution. |
| [TRTCVideoResolutionMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoResolutionMode)| Video resolution mode. |
| [TRTCVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoStreamType) | Video stream type. |
| [TRTCQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCQuality)| Image quality level. |
| [TRTCVideoFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoFillMode)| Video image fill mode. |
| [TRTCBeautyStyle](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCBeautyStyle) | Beauty filter (skin smoothing) algorithm. |
| [TRTCAppScene](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)| Application scenario. |
| [TRTCRoleType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCRoleType)| Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCQosControlMode)| Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoQosPreference)| Image quality preference. |
| [TRTCDeviceState](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCDeviceState)| Device operation. |
| [TRTCDeviceType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCDeviceType)| Device type. |
| [TRTCWaterMarkSrcType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCWaterMarkSrcType)| Watermark image source type. |
| [TRTCTranscodingConfigMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode)| MixTranscoding parameter configuration mode. |
