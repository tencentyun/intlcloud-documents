## ITRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.


### Creation and termination

| API | Description |
|-----|-----|
| [getTRTCShareInstance](https://intl.cloud.tencent.com/document/product/647/35137#gettrtcshareinstance) | Creates `ITRTCCloud` singleton. |
| [destroyTRTCShareInstance](https://intl.cloud.tencent.com/document/product/647/35137#destroytrtcshareinstance) | Releases `ITRTCCloud` singleton object.          |


### Setting the `ITRTCCloudCallback` callback

| API | Description |
|-----|-----|
| [addCallback](https://intl.cloud.tencent.com/document/product/647/35137#addcallback) | Sets the [ITRTCCloudCallback](https://intl.cloud.tencent.com/document/product/647/35138) callback API. |
| [removeCallback](https://intl.cloud.tencent.com/document/product/647/35137#removecallback) | Removes event callback. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/35137#enterroom) | Enters room. |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/35137#exitroom) | Exits room. |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/35137#switchrole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [connectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35137#connectotherroom) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35137#disconnectotherroom) | Exits cross-room co-anchoring. |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/35137#setdefaultstreamrecvmode) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35137#startlocalpreview) | Enables preview image of local video. |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/35137#stoplocalpreview) | Stops local video capture and preview. |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/35137#mutelocalvideo) | Specifies whether to block local video image. |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/35137#startremoteview) | Starts displaying remote video image. |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/35137#stopremoteview) | Stops displaying remote video image. |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/35137#stopallremoteview) | Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/35137#muteremotevideostream) | Pauses receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/35137#muteallremotevideostreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/35137#setvideoencoderparam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35137#setnetworkqosparam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/35137#setlocalviewfillmode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/35137#setremoteviewfillmode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/35137#setlocalviewrotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/35137#setremoteviewrotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/35137#setvideoencoderrotation) | Sets direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server). |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35137#setlocalviewmirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/35137#setvideoencodermirror) | Sets mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/35137#enablesmallvideostream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35137#setremotevideostreamtype) | Selects whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35137#setpriorremotevideostreamtype) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/35137#startlocalaudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/35137#stoplocalaudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/35137#mutelocalaudio) | Mutes local audio. |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35137#muteremoteaudio) | Mutes the specified user's audio. |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35137#muteallremoteaudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/35137#enableaudiovolumeevaluation) | Enables or disables volume reminder. |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/35137#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/35137#stopaudiorecording) | Stops audio recording. |


### Camera API functions

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://intl.cloud.tencent.com/document/product/647/35137#getcameradeviceslist) | Gets list of cameras. |
| [setCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35137#setcurrentcameradevice) | Sets the camera to be used. |
| [getCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35137#getcurrentcameradevice) | Gets the currently used camera. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](https://intl.cloud.tencent.com/document/product/647/35137#getmicdeviceslist) | Gets list of mics. |
| [getCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35137#getcurrentmicdevice) | Gets the currently used mic. |
| [setCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35137#setcurrentmicdevice) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35137#getcurrentmicdevicevolume) | Gets current mic volume level of the system. |
| [setCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35137#setcurrentmicdevicevolume) | Sets current mic volume level of the system. |
| [getSpeakerDevicesList](https://intl.cloud.tencent.com/document/product/647/35137#getspeakerdeviceslist) | Gets list of speakers. |
| [getCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35137#getcurrentspeakerdevice) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35137#setcurrentspeakerdevice) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://intl.cloud.tencent.com/document/product/647/35137#getcurrentspeakervolume) | Gets current speaker volume level. |
| [setCurrentSpeakerVolume](https://intl.cloud.tencent.com/document/product/647/35137#setcurrentspeakervolume) | Sets current speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [setBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35137#setbeautystyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://intl.cloud.tencent.com/document/product/647/35137#setwatermark) | Sets watermark. |


### Secondary stream API functions

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35137#startremotesubstreamview) | Starts rendering the secondary stream image of a remote user. |
| [stopRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35137#stopremotesubstreamview) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://intl.cloud.tencent.com/document/product/647/35137#setremotesubstreamviewfillmode) | Sets rendering mode of the secondary stream image. |
| [getScreenCaptureSources](https://intl.cloud.tencent.com/document/product/647/35137#getscreencapturesources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://intl.cloud.tencent.com/document/product/647/35137#selectscreencapturetarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/35137#startscreencapture) | Starts screen sharing. |
| [pauseScreenCapture](https://intl.cloud.tencent.com/document/product/647/35137#pausescreencapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://intl.cloud.tencent.com/document/product/647/35137#resumescreencapture) | Resumes screen sharing. |
| [stopScreenCapture](https://intl.cloud.tencent.com/document/product/647/35137#stopscreencapture) | Stops screen capture. |
| [setSubStreamEncoderParam](https://intl.cloud.tencent.com/document/product/647/35137#setsubstreamencoderparam) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://intl.cloud.tencent.com/document/product/647/35137#setsubstreammixvolume) | Sets audio mixing volume level of the secondary stream. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://intl.cloud.tencent.com/document/product/647/35137#enablecustomvideocapture) | Enables custom video capture mode. |
| [sendCustomVideoData](https://intl.cloud.tencent.com/document/product/647/35137#sendcustomvideodata) | Delivers the captured video data to the SDK. |
| [enableCustomAudioCapture](https://intl.cloud.tencent.com/document/product/647/35137#enablecustomaudiocapture) | Enables the custom audio capture mode. After this mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](https://intl.cloud.tencent.com/document/product/647/35137#sendcustomaudiodata) to continuously insert the captured audio data into the SDK. |
| [sendCustomAudioData](https://intl.cloud.tencent.com/document/product/647/35137#sendcustomaudiodata) | Delivers the captured audio data to the SDK. |
| [setLocalVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35137#setlocalvideorendercallback) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35137#setremotevideorendercallback) | Sets custom rendering for remote video. |
| [setAudioFrameCallback](https://intl.cloud.tencent.com/document/product/647/35137#setaudioframecallback) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35137#sendcustomcmdmsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://intl.cloud.tencent.com/document/product/647/35137#sendseimsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://intl.cloud.tencent.com/document/product/647/35137#playbgm) | Starts background music. |
| [stopBGM](https://intl.cloud.tencent.com/document/product/647/35137#stopbgm) | Stops background music. |
| [pauseBGM](https://intl.cloud.tencent.com/document/product/647/35137#pausebgm) | Pauses background music. |
| [resumeBGM](https://intl.cloud.tencent.com/document/product/647/35137#resumebgm) | Resumes background music. |
| [getBGMDuration](https://intl.cloud.tencent.com/document/product/647/35137#getbgmduration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://intl.cloud.tencent.com/document/product/647/35137#setbgmposition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://intl.cloud.tencent.com/document/product/647/35137#setmicvolumeonmixing) | Adjusts the mic volume level when background music is played back. |
| [setBGMVolume](https://intl.cloud.tencent.com/document/product/647/35137#setbgmvolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [startSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35137#startsystemaudioloopback) | Enables system audio capture (the 64-bit SDK currently does not support system audio mixing). |
| [stopSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35137#stopsystemaudioloopback) | Disables system audio capture. |
| [setSystemAudioLoopbackVolume](https://intl.cloud.tencent.com/document/product/647/35137#setsystemaudioloopbackvolume) | Sets system audio capture volume level. |


### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://intl.cloud.tencent.com/document/product/647/35137#playaudioeffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://intl.cloud.tencent.com/document/product/647/35137#setaudioeffectvolume) | Sets sound effect volume level. |
| [stopAudioEffect](https://intl.cloud.tencent.com/document/product/647/35137#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](https://intl.cloud.tencent.com/document/product/647/35137#stopallaudioeffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://intl.cloud.tencent.com/document/product/647/35137#setallaudioeffectsvolume) | Sets volume level of all sound effects. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://intl.cloud.tencent.com/document/product/647/35137#startspeedtest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://intl.cloud.tencent.com/document/product/647/35137#stopspeedtest) | Stops network speed test. |
| [startCameraDeviceTest](https://intl.cloud.tencent.com/document/product/647/35137#startcameradevicetest) | Starts camera test. |
| [stopCameraDeviceTest](https://intl.cloud.tencent.com/document/product/647/35137#stopcameradevicetest) | Stops camera test. |
| [startMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35137#startmicdevicetest) | Starts mic test. |
| [stopMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35137#stopmicdevicetest) | Stops mic test. |
| [startSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35137#startspeakerdevicetest) | Starts speaker test. |
| [stopSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35137#stopspeakerdevicetest) | Stops speaker test. |


### MixTranscoding and CDN relayed push APIs

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35137#setmixtranscodingconfig) | Starts (update) On-Cloud MixTranscoding: this method uses the transcoding service of Tencent Cloud to combine multiple image channels into one channel. |
| [startPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35137#startpublishcdnstream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35137#stoppublishcdnstream) | Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://intl.cloud.tencent.com/document/product/647/35137#getsdkversion) | Gets SDK version information.. |
| [setLogLevel](https://intl.cloud.tencent.com/document/product/647/35137#setloglevel) | Sets log output level. |
| [setConsoleEnabled](https://intl.cloud.tencent.com/document/product/647/35137#setconsoleenabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://intl.cloud.tencent.com/document/product/647/35137#setlogcompressenabled) | Enables or disables local log compression. |
| [setLogDirPath](https://intl.cloud.tencent.com/document/product/647/35137#setlogdirpath) | Sets log storage path. |
| [setLogCallback](https://intl.cloud.tencent.com/document/product/647/35137#setlogcallback) | Sets log callback. |
| [showDebugView](https://intl.cloud.tencent.com/document/product/647/35137#showdebugview) | Displays dashboard. |
| [callExperimentalAPI](https://intl.cloud.tencent.com/document/product/647/35137#callexperimentalapi) | Calls experimental API. |


## TRTCCloudCallback @ TXLiteAVSDK

Callback API class for TRTC video call feature.

### General event callbacks

| API | Description |
|-----|-----|
| [onError](https://intl.cloud.tencent.com/document/product/647/35138#onerror) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://intl.cloud.tencent.com/document/product/647/35138#onwarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://intl.cloud.tencent.com/document/product/647/35138#onenterroom) | Callback of room entry. |
| [onExitRoom](https://intl.cloud.tencent.com/document/product/647/35138#onexitroom) | Callback of room exit. |
| [onSwitchRole](https://intl.cloud.tencent.com/document/product/647/35138#onswitchrole) | Callback of role switching. |
| [onConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35138#onconnectotherroom) | Callback of the result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35138#ondisconnectotherroom) | Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://intl.cloud.tencent.com/document/product/647/35138#onremoteuserenterroom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://intl.cloud.tencent.com/document/product/647/35138#onremoteuserleaveroom) | A user exits the current room. |
| [onUserVideoAvailable](https://intl.cloud.tencent.com/document/product/647/35138#onuservideoavailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://intl.cloud.tencent.com/document/product/647/35138#onusersubstreamavailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://intl.cloud.tencent.com/document/product/647/35138#onuseraudioavailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://intl.cloud.tencent.com/document/product/647/35138#onfirstvideoframe) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://intl.cloud.tencent.com/document/product/647/35138#onfirstaudioframe) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://intl.cloud.tencent.com/document/product/647/35138#onsendfirstlocalvideoframe) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://intl.cloud.tencent.com/document/product/647/35138#onsendfirstlocalaudioframe) | The first local audio frame data has been sent. |
| [onUserEnter](https://intl.cloud.tencent.com/document/product/647/35138#onuserenter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://intl.cloud.tencent.com/document/product/647/35138#onuserexit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://intl.cloud.tencent.com/document/product/647/35138#onnetworkquality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://intl.cloud.tencent.com/document/product/647/35138#onstatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://intl.cloud.tencent.com/document/product/647/35138#onconnectionlost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://intl.cloud.tencent.com/document/product/647/35138#ontrytoreconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://intl.cloud.tencent.com/document/product/647/35138#onconnectionrecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://intl.cloud.tencent.com/document/product/647/35138#onspeedtest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://intl.cloud.tencent.com/document/product/647/35138#oncameradidready) | Camera is ready. |
| [onMicDidReady](https://intl.cloud.tencent.com/document/product/647/35138#onmicdidready) | Mic is ready. |
| [onUserVoiceVolume](https://intl.cloud.tencent.com/document/product/647/35138#onuservoicevolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://intl.cloud.tencent.com/document/product/647/35138#ondevicechange) | Callback of local device connection and disconnection. |
| [onTestMicVolume](https://intl.cloud.tencent.com/document/product/647/35138#ontestmicvolume) | Callback of mic volume level in test. |
| [onTestSpeakerVolume](https://intl.cloud.tencent.com/document/product/647/35138#ontestspeakervolume) | Callback of speaker volume level in test. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35138#onrecvcustomcmdmsg) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35138#onmisscustomcmdmsg) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://intl.cloud.tencent.com/document/product/647/35138#onrecvseimsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35138#onstartpublishcdnstream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35138#onstoppublishcdnstream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35138#onsetmixtranscodingconfig) | Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35138#onaudioeffectfinished) | Callback of ending an audio effect. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://intl.cloud.tencent.com/document/product/647/35138#onscreencapturecovered) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://intl.cloud.tencent.com/document/product/647/35138#onscreencapturestarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://intl.cloud.tencent.com/document/product/647/35138#onscreencapturepaused) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://intl.cloud.tencent.com/document/product/647/35138#onscreencaptureresumed) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://intl.cloud.tencent.com/document/product/647/35138#onscreencapturestoped) | This callback will be returned by the SDK when screen sharing is stopped. |


### Background audio mixing event callbacks

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://intl.cloud.tencent.com/document/product/647/35138#onplaybgmbegin) | Playback of background music starts. |
| [onPlayBGMProgress](https://intl.cloud.tencent.com/document/product/647/35138#onplaybgmprogress) | Progress of background music playback. |
| [onPlayBGMComplete](https://intl.cloud.tencent.com/document/product/647/35138#onplaybgmcomplete) | Playback of background music ends. |


### Custom video rendering callbacks
This callback API is defined by the [ITRTCVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35138#itrtcvideorendercallback) class.

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://intl.cloud.tencent.com/document/product/647/35138#onrendervideoframe) | Callback of custom video rendering. |


### Audio data callbacks
This callback API is defined by the [ITRTCAudioFrameCallback](https://intl.cloud.tencent.com/document/product/647/35138#itrtcaudioframecallback) class.

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://intl.cloud.tencent.com/document/product/647/35138#oncapturedaudioframe) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35138#onplayaudioframe) | Audio data from each remote user before audio mixing (for example, if you need to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing). |
| [onMixedPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35138#onmixedplayaudioframe) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
This callback API is defined by the [ITRTCLogCallback](https://intl.cloud.tencent.com/document/product/647/35138#itrtclogcallback) class.

| API | Description |
|-----|-----|
| [onLog](https://intl.cloud.tencent.com/document/product/647/35138#onlog) | Callback of log printing. |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35139#trtcparams) | Room entry parameters. |
| [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideoencparam) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35139#trtcnetworkqosparam) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://intl.cloud.tencent.com/document/product/647/35139#trtcqualityinfo) | Video quality. |
| [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35139#trtcvolumeinfo) | Volume level. |
| [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35139#trtcspeedtestresult) | Network speed test result. |
| [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35139#trtcmixuser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35139#trtctranscodingconfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35139#trtcpublishcdnparam) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35139#trtcaudiorecordingparams) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35139#trtcaudioeffectparam) | Sound effect. |
| [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35139#trtclocalstatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35139#trtcremotestatistics) | Remote audio/video statistics. |
| [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35139#trtcstatistics) | Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideoresolution) | Video resolution. |
| [TRTCVideoResolutionMode](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideoresolutionmode) | Video resolution mode. |
| [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideostreamtype) | Video stream type. |
| [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35139#trtcquality) | Image quality level. |
| [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideofillmode) | Video image fill mode. |
| [TRTCBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35139#trtcbeautystyle) | Beauty filter (skin smoothing) algorithm. |
| [TRTCAppScene](https://intl.cloud.tencent.com/document/product/647/35139#trtcappscene) | Application scenario. |
| [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35139#trtcroletype) | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://intl.cloud.tencent.com/document/product/647/35139#trtcqoscontrolmode) | Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://intl.cloud.tencent.com/document/product/647/35139#trtcvideoqospreference) | Image quality preference. |
| [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35139#trtcloglevel) | Log level. |
| [TRTCDeviceState](https://intl.cloud.tencent.com/document/product/647/35139#trtcdevicestate) | Device operation. |
| [TRTCDeviceType](https://intl.cloud.tencent.com/document/product/647/35139#trtcdevicetype) | Device type. |
| [TRTCWaterMarkSrcType](https://intl.cloud.tencent.com/document/product/647/35139#trtcwatermarksrctype) | Watermark image source type. |
| [TRTCTranscodingConfigMode](https://intl.cloud.tencent.com/document/product/647/35139#trtctranscodingconfigmode) | MixTranscoding parameter configuration mode. |


