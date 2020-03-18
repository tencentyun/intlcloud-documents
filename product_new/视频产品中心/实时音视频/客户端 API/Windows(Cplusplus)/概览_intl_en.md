## ITRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.


### Creation and termination

| API | Description |
|-----|-----|
| [getTRTCShareInstance](https://intl.cloud.tencent.com/document/product/647/35132#gettrtcshareinstance) | Creates `ITRTCCloud` singleton. |
| [destroyTRTCShareInstance](https://intl.cloud.tencent.com/document/product/647/35132#destroytrtcshareinstance) | Releases `ITRTCCloud` singleton object.          |


### Setting the `ITRTCCloudCallback` callback

| API | Description |
|-----|-----|
| [addCallback](https://intl.cloud.tencent.com/document/product/647/35132#addcallback) | Sets the [ITRTCCloudCallback](https://intl.cloud.tencent.com/document/product/647/35133) callback API. |
| [removeCallback](https://intl.cloud.tencent.com/document/product/647/35132#removecallback) | Removes event callback. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/35132#enterroom) | Enters room. |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/35132#exitroom) | Exits room. |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/35132#switchrole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [connectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35132#connectotherroom) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35132#disconnectotherroom) | Exits cross-room co-anchoring. |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/35132#setdefaultstreamrecvmode) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35132#startlocalpreview) | Enables preview image of local video. |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/35132#stoplocalpreview) | Stops local video capture and preview. |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/35132#mutelocalvideo) | Specifies whether to block local video image. |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/35132#startremoteview) | Starts displaying remote video image. |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/35132#stopremoteview) | Stops displaying remote video image. |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/35132#stopallremoteview) | Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/35132#muteremotevideostream) | Pauses receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/35132#muteallremotevideostreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/35132#setvideoencoderparam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35132#setnetworkqosparam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/35132#setlocalviewfillmode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/35132#setremoteviewfillmode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/35132#setlocalviewrotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/35132#setremoteviewrotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/35132#setvideoencoderrotation) | Sets direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server). |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35132#setlocalviewmirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/35132#setvideoencodermirror) | Sets mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/35132#enablesmallvideostream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35132#setremotevideostreamtype) | Specifies whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35132#setpriorremotevideostreamtype) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/35132#startlocalaudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/35132#stoplocalaudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/35132#mutelocalaudio) | Mutes local audio. |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35132#muteremoteaudio) | Mutes the specified user's audio. |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35132#muteallremoteaudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/35132#enableaudiovolumeevaluation) | Enables or disables volume reminder. |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/35132#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/35132#stopaudiorecording) | Stops audio recording. |


### Camera API functions

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://intl.cloud.tencent.com/document/product/647/35132#getcameradeviceslist) | Gets list of cameras. |
| [setCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35132#setcurrentcameradevice) | Sets the camera to be used. |
| [getCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35132#getcurrentcameradevice) | Gets the currently used camera. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](https://intl.cloud.tencent.com/document/product/647/35132#getmicdeviceslist) | Gets list of mics. |
| [getCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35132#getcurrentmicdevice) | Gets the currently used mic. |
| [setCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35132#setcurrentmicdevice) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35132#getcurrentmicdevicevolume) | Gets current mic volume level of the system. |
| [setCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35132#setcurrentmicdevicevolume) | Sets current mic volume level of the system. |
| [getSpeakerDevicesList](https://intl.cloud.tencent.com/document/product/647/35132#getspeakerdeviceslist) | Gets list of speakers. |
| [getCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35132#getcurrentspeakerdevice) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35132#setcurrentspeakerdevice) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://intl.cloud.tencent.com/document/product/647/35132#getcurrentspeakervolume) | Gets current speaker volume level. |
| [setCurrentSpeakerVolume](https://intl.cloud.tencent.com/document/product/647/35132#setcurrentspeakervolume) | Sets current speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [setBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35132#setbeautystyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://intl.cloud.tencent.com/document/product/647/35132#setwatermark) | Sets watermark. |


### Secondary stream API functions

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35132#startremotesubstreamview) | Starts rendering the secondary stream image of a remote user. |
| [stopRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35132#stopremotesubstreamview) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://intl.cloud.tencent.com/document/product/647/35132#setremotesubstreamviewfillmode) | Sets rendering mode of the secondary stream image. |
| [getScreenCaptureSources](https://intl.cloud.tencent.com/document/product/647/35132#getscreencapturesources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://intl.cloud.tencent.com/document/product/647/35132#selectscreencapturetarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/35132#startscreencapture) | Starts screen sharing. |
| [pauseScreenCapture](https://intl.cloud.tencent.com/document/product/647/35132#pausescreencapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://intl.cloud.tencent.com/document/product/647/35132#resumescreencapture) | Resumes screen sharing. |
| [stopScreenCapture](https://intl.cloud.tencent.com/document/product/647/35132#stopscreencapture) | Stops screen capture. |
| [setSubStreamEncoderParam](https://intl.cloud.tencent.com/document/product/647/35132#setsubstreamencoderparam) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://intl.cloud.tencent.com/document/product/647/35132#setsubstreammixvolume) | Sets audio mixing volume level of the secondary stream. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://intl.cloud.tencent.com/document/product/647/35132#enablecustomvideocapture) | Enables custom video capture mode. |
| [sendCustomVideoData](https://intl.cloud.tencent.com/document/product/647/35132#sendcustomvideodata) | Delivers the captured video data to the SDK. |
| [enableCustomAudioCapture](https://intl.cloud.tencent.com/document/product/647/35132#enablecustomaudiocapture) | Enables the custom audio capture mode. After this mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](https://intl.cloud.tencent.com/document/product/647/35132#sendcustomaudiodata) to continuously insert the captured audio data into the SDK. |
| [sendCustomAudioData](https://intl.cloud.tencent.com/document/product/647/35132#sendcustomaudiodata) | Delivers the captured audio data to the SDK. |
| [setLocalVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35132#setlocalvideorendercallback) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35132#setremotevideorendercallback) | Sets custom rendering for remote video. |
| [setAudioFrameCallback](https://intl.cloud.tencent.com/document/product/647/35132#setaudioframecallback) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35132#sendcustomcmdmsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://intl.cloud.tencent.com/document/product/647/35132#sendseimsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://intl.cloud.tencent.com/document/product/647/35132#playbgm) | Starts background music. |
| [stopBGM](https://intl.cloud.tencent.com/document/product/647/35132#stopbgm) | Stops background music. |
| [pauseBGM](https://intl.cloud.tencent.com/document/product/647/35132#pausebgm) | Pauses background music. |
| [resumeBGM](https://intl.cloud.tencent.com/document/product/647/35132#resumebgm) | Resumes background music. |
| [getBGMDuration](https://intl.cloud.tencent.com/document/product/647/35132#getbgmduration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://intl.cloud.tencent.com/document/product/647/35132#setbgmposition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://intl.cloud.tencent.com/document/product/647/35132#setmicvolumeonmixing) | Adjusts the mic volume level when background music is played back. |
| [setBGMVolume](https://intl.cloud.tencent.com/document/product/647/35132#setbgmvolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [startSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35132#startsystemaudioloopback) | Enables system audio capture (the 64-bit SDK currently does not support system audio mixing). |
| [stopSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35132#stopsystemaudioloopback) | Disables system audio capture. |
| [setSystemAudioLoopbackVolume](https://intl.cloud.tencent.com/document/product/647/35132#setsystemaudioloopbackvolume) | Sets system audio capture volume level. |


### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://intl.cloud.tencent.com/document/product/647/35132#playaudioeffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://intl.cloud.tencent.com/document/product/647/35132#setaudioeffectvolume) | Sets sound effect volume level. |
| [stopAudioEffect](https://intl.cloud.tencent.com/document/product/647/35132#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](https://intl.cloud.tencent.com/document/product/647/35132#stopallaudioeffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://intl.cloud.tencent.com/document/product/647/35132#setallaudioeffectsvolume) | Sets volume level of all sound effects. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://intl.cloud.tencent.com/document/product/647/35132#startspeedtest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://intl.cloud.tencent.com/document/product/647/35132#stopspeedtest) | Stops network speed test. |
| [startCameraDeviceTest](https://intl.cloud.tencent.com/document/product/647/35132#startcameradevicetest) | Starts camera test. |
| [stopCameraDeviceTest](https://intl.cloud.tencent.com/document/product/647/35132#stopcameradevicetest) | Stops camera test. |
| [startMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35132#startmicdevicetest) | Starts mic test. |
| [stopMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35132#stopmicdevicetest) | Stops mic test. |
| [startSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35132#startspeakerdevicetest) | Starts speaker test. |
| [stopSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35132#stopspeakerdevicetest) | Stops speaker test. |


### MixTranscoding and CDN relayed push APIs

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35132#setmixtranscodingconfig) | Starts (update) On-Cloud MixTranscoding: this method uses the transcoding service of Tencent Cloud to combine multiple image channels into one channel. |
| [startPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35132#startpublishcdnstream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35132#stoppublishcdnstream) | Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://intl.cloud.tencent.com/document/product/647/35132#getsdkversion) | Gets SDK version information.. |
| [setLogLevel](https://intl.cloud.tencent.com/document/product/647/35132#setloglevel) | Sets log output level. |
| [setConsoleEnabled](https://intl.cloud.tencent.com/document/product/647/35132#setconsoleenabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://intl.cloud.tencent.com/document/product/647/35132#setlogcompressenabled) | Enables or disables local log compression. |
| [setLogDirPath](https://intl.cloud.tencent.com/document/product/647/35132#setlogdirpath) | Sets log storage path. |
| [setLogCallback](https://intl.cloud.tencent.com/document/product/647/35132#setlogcallback) | Sets log callback. |
| [showDebugView](https://intl.cloud.tencent.com/document/product/647/35132#showdebugview) | Displays dashboard. |
| [callExperimentalAPI](https://intl.cloud.tencent.com/document/product/647/35132#callexperimentalapi) | Calls experimental API. |


## TRTCCloudCallback @ TXLiteAVSDK

Callback API class for TRTC video call feature.

### General event callbacks

| API | Description |
|-----|-----|
| [onError](https://intl.cloud.tencent.com/document/product/647/35133#onerror) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://intl.cloud.tencent.com/document/product/647/35133#onwarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://intl.cloud.tencent.com/document/product/647/35133#onenterroom) | Callback of room entry. |
| [onExitRoom](https://intl.cloud.tencent.com/document/product/647/35133#onexitroom) | Callback of room exit. |
| [onSwitchRole](https://intl.cloud.tencent.com/document/product/647/35133#onswitchrole) | Callback of role switching. |
| [onConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35133#onconnectotherroom) | Callback of the result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35133#ondisconnectotherroom) | Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://intl.cloud.tencent.com/document/product/647/35133#onremoteuserenterroom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://intl.cloud.tencent.com/document/product/647/35133#onremoteuserleaveroom) | A user exits the current room, which corresponds to `onuserEnterRoom`. |
| [onUserVideoAvailable](https://intl.cloud.tencent.com/document/product/647/35133#onuservideoavailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://intl.cloud.tencent.com/document/product/647/35133#onusersubstreamavailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://intl.cloud.tencent.com/document/product/647/35133#onuseraudioavailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://intl.cloud.tencent.com/document/product/647/35133#onfirstvideoframe) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://intl.cloud.tencent.com/document/product/647/35133#onfirstaudioframe) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://intl.cloud.tencent.com/document/product/647/35133#onsendfirstlocalvideoframe) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://intl.cloud.tencent.com/document/product/647/35133#onsendfirstlocalaudioframe) | The first local audio frame data has been sent. |
| [onUserEnter](https://intl.cloud.tencent.com/document/product/647/35133#onuserenter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://intl.cloud.tencent.com/document/product/647/35133#onuserexit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://intl.cloud.tencent.com/document/product/647/35133#onnetworkquality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://intl.cloud.tencent.com/document/product/647/35133#onstatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://intl.cloud.tencent.com/document/product/647/35133#onconnectionlost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://intl.cloud.tencent.com/document/product/647/35133#ontrytoreconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://intl.cloud.tencent.com/document/product/647/35133#onconnectionrecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://intl.cloud.tencent.com/document/product/647/35133#onspeedtest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://intl.cloud.tencent.com/document/product/647/35133#oncameradidready) | Camera is ready. |
| [onMicDidReady](https://intl.cloud.tencent.com/document/product/647/35133#onmicdidready) | Mic is ready. |
| [onUserVoiceVolume](https://intl.cloud.tencent.com/document/product/647/35133#onuservoicevolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://intl.cloud.tencent.com/document/product/647/35133#ondevicechange) | Callback of local device connection and disconnection. |
| [onTestMicVolume](https://intl.cloud.tencent.com/document/product/647/35133#ontestmicvolume) | Callback of mic volume level in test. |
| [onTestSpeakerVolume](https://intl.cloud.tencent.com/document/product/647/35133#ontestspeakervolume) | Callback of speaker volume level in test. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35133#onrecvcustomcmdmsg) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35133#onmisscustomcmdmsg) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://intl.cloud.tencent.com/document/product/647/35133#onrecvseimsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35133#onstartpublishcdnstream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35133#onstoppublishcdnstream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35133#onsetmixtranscodingconfig) | Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35133#onaudioeffectfinished) | Callback of ending an audio effect. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://intl.cloud.tencent.com/document/product/647/35133#onscreencapturecovered) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://intl.cloud.tencent.com/document/product/647/35133#onscreencapturestarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://intl.cloud.tencent.com/document/product/647/35133#onscreencapturepaused) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://intl.cloud.tencent.com/document/product/647/35133#onscreencaptureresumed) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://intl.cloud.tencent.com/document/product/647/35133#onscreencapturestoped) | This callback will be returned by the SDK when screen sharing is stopped. |


### Background audio mixing event callbacks

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://intl.cloud.tencent.com/document/product/647/35133#onplaybgmbegin) | Playback of background music starts. |
| [onPlayBGMProgress](https://intl.cloud.tencent.com/document/product/647/35133#onplaybgmprogress) | Progress of background music playback. |
| [onPlayBGMComplete](https://intl.cloud.tencent.com/document/product/647/35133#onplaybgmcomplete) | Playback of background music ends. |


### Custom video rendering callbacks
Redirect to [ITRTCVideoRenderCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtcvideorendercallback)

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://intl.cloud.tencent.com/document/product/647/35133#onrendervideoframe) | Callback of custom video rendering. |


### Audio data callbacks
Redirect to [ITRTCAudioFrameCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtcaudioframecallback)

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://intl.cloud.tencent.com/document/product/647/35133#oncapturedaudioframe) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35133#onplayaudioframe) | Audio data from each remote user before audio mixing (for example, if you want to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing). |
| [onMixedPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35133#onmixedplayaudioframe) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
Redirect to [ITRTCLogCallback](https://intl.cloud.tencent.com/document/product/647/35133#itrtclogcallback)

| API | Description |
|-----|-----|
| [onLog](https://intl.cloud.tencent.com/document/product/647/35133#onlog) | Callback of log printing. |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35134#trtcparams) | Room entry parameters. |
| [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoencparam) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcnetworkqosparam) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://intl.cloud.tencent.com/document/product/647/35134#trtcqualityinfo) | Video quality. |
| [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35134#trtcvolumeinfo) | Volume level. |
| [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35134#trtcspeedtestresult) | Network speed test result. |
| [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35134#trtcmixuser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35134#trtctranscodingconfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcpublishcdnparam) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35134#trtcaudiorecordingparams) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35134#trtcaudioeffectparam) | Sound effect. |
| [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35134#trtclocalstatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35134#trtcremotestatistics) | Remote audio/video statistics. |
| [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35134#trtcstatistics) | Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoresolution) | Video resolution. |
| [TRTCVideoResolutionMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoresolutionmode) | Video resolution mode. |
| [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideostreamtype) | Video stream type. |
| [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35134#trtcquality) | Image quality level. |
| [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideofillmode) | Video image fill mode. |
| [TRTCBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35134#trtcbeautystyle) | Beauty filter (skin smoothing) algorithm. |
| [TRTCAppScene](https://intl.cloud.tencent.com/document/product/647/35134#trtcappscene) | Application scenario. |
| [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35134#trtcroletype) | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://intl.cloud.tencent.com/document/product/647/35134#trtcqoscontrolmode) | Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://intl.cloud.tencent.com/document/product/647/35134#trtcvideoqospreference) | Image quality preference. |
| [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35134#trtcloglevel) | Log level. |
| [TRTCDeviceState](https://intl.cloud.tencent.com/document/product/647/35134#trtcdevicestate) | Device operation. |
| [TRTCDeviceType](https://intl.cloud.tencent.com/document/product/647/35134#trtcdevicetype) | Device type. |
| [TRTCWaterMarkSrcType](https://intl.cloud.tencent.com/document/product/647/35134#trtcwatermarksrctype) | Watermark image source type. |
| [TRTCTranscodingConfigMode](https://intl.cloud.tencent.com/document/product/647/35134#trtctranscodingconfigmode) | MixTranscoding parameter configuration mode. |


