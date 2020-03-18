## ITRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.


### Creation and termination

| API | Description |
|-----|-----|
| [getTRTCShareInstance](https://cloud.tencent.com/document/product/647/36778#gettrtcshareinstance) | Creates `ITRTCCloud` singleton. |
| [destroyTRTCShareInstance](https://cloud.tencent.com/document/product/647/36778#destroytrtcshareinstance) | Releases `ITRTCCloud` singleton object.          |


### Setting the `ITRTCCloudCallback` callback

| API | Description |
|-----|-----|
| [addCallback](https://cloud.tencent.com/document/product/647/36778#addcallback) | Sets the [ITRTCCloudCallback](https://cloud.tencent.com/document/product/647/36779) callback API. |
| [removeCallback](https://cloud.tencent.com/document/product/647/36778#removecallback) | Removes event callback. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://cloud.tencent.com/document/product/647/36778#enterroom) | Enters room. |
| [exitRoom](https://cloud.tencent.com/document/product/647/36778#exitroom) | Exits room. |
| [switchRole](https://cloud.tencent.com/document/product/647/36778#switchrole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [connectOtherRoom](https://cloud.tencent.com/document/product/647/36778#connectotherroom) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](https://cloud.tencent.com/document/product/647/36778#disconnectotherroom) | Exits cross-room co-anchoring. |
| [setDefaultStreamRecvMode](https://cloud.tencent.com/document/product/647/36778#setdefaultstreamrecvmode) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://cloud.tencent.com/document/product/647/36778#startlocalpreview) | Enables preview image of local video. |
| [stopLocalPreview](https://cloud.tencent.com/document/product/647/36778#stoplocalpreview) | Stops local video capture and preview. |
| [muteLocalVideo](https://cloud.tencent.com/document/product/647/36778#mutelocalvideo) | Specifies whether to block local video image. |
| [startRemoteView](https://cloud.tencent.com/document/product/647/36778#startremoteview) | Starts displaying remote video image. |
| [stopRemoteView](https://cloud.tencent.com/document/product/647/36778#stopremoteview) | Stops displaying remote video image. |
| [stopAllRemoteView](https://cloud.tencent.com/document/product/647/36778#stopallremoteview) | Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://cloud.tencent.com/document/product/647/36778#muteremotevideostream) | Pauses receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://cloud.tencent.com/document/product/647/36778#muteallremotevideostreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://cloud.tencent.com/document/product/647/36778#setvideoencoderparam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://cloud.tencent.com/document/product/647/36778#setnetworkqosparam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://cloud.tencent.com/document/product/647/36778#setlocalviewfillmode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://cloud.tencent.com/document/product/647/36778#setremoteviewfillmode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://cloud.tencent.com/document/product/647/36778#setlocalviewrotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://cloud.tencent.com/document/product/647/36778#setremoteviewrotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://cloud.tencent.com/document/product/647/36778#setvideoencoderrotation) | Sets direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server). |
| [setLocalViewMirror](https://cloud.tencent.com/document/product/647/36778#setlocalviewmirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://cloud.tencent.com/document/product/647/36778#setvideoencodermirror) | Sets mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://cloud.tencent.com/document/product/647/36778#enablesmallvideostream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://cloud.tencent.com/document/product/647/36778#setremotevideostreamtype) | Selects whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://cloud.tencent.com/document/product/647/36778#setpriorremotevideostreamtype) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://cloud.tencent.com/document/product/647/36778#startlocalaudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://cloud.tencent.com/document/product/647/36778#stoplocalaudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://cloud.tencent.com/document/product/647/36778#mutelocalaudio) | Mutes local audio. |
| [muteRemoteAudio](https://cloud.tencent.com/document/product/647/36778#muteremoteaudio) | Mutes the specified user's audio. |
| [muteAllRemoteAudio](https://cloud.tencent.com/document/product/647/36778#muteallremoteaudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://cloud.tencent.com/document/product/647/36778#enableaudiovolumeevaluation) | Enables or disables volume reminder. |
| [startAudioRecording](https://cloud.tencent.com/document/product/647/36778#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](https://cloud.tencent.com/document/product/647/36778#stopaudiorecording) | Stops audio recording. |


### Camera API functions

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://cloud.tencent.com/document/product/647/36778#getcameradeviceslist) | Gets list of cameras. |
| [setCurrentCameraDevice](https://cloud.tencent.com/document/product/647/36778#setcurrentcameradevice) | Sets the camera to be used. |
| [getCurrentCameraDevice](https://cloud.tencent.com/document/product/647/36778#getcurrentcameradevice) | Gets the currently used camera. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](https://cloud.tencent.com/document/product/647/36778#getmicdeviceslist) | Gets list of mics. |
| [getCurrentMicDevice](https://cloud.tencent.com/document/product/647/36778#getcurrentmicdevice) | Gets the currently used mic. |
| [setCurrentMicDevice](https://cloud.tencent.com/document/product/647/36778#setcurrentmicdevice) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://cloud.tencent.com/document/product/647/36778#getcurrentmicdevicevolume) | Gets current mic volume level of the system. |
| [setCurrentMicDeviceVolume](https://cloud.tencent.com/document/product/647/36778#setcurrentmicdevicevolume) | Sets current mic volume level of the system. |
| [getSpeakerDevicesList](https://cloud.tencent.com/document/product/647/36778#getspeakerdeviceslist) | Gets list of speakers. |
| [getCurrentSpeakerDevice](https://cloud.tencent.com/document/product/647/36778#getcurrentspeakerdevice) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://cloud.tencent.com/document/product/647/36778#setcurrentspeakerdevice) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://cloud.tencent.com/document/product/647/36778#getcurrentspeakervolume) | Gets current speaker volume level. |
| [setCurrentSpeakerVolume](https://cloud.tencent.com/document/product/647/36778#setcurrentspeakervolume) | Sets current speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [setBeautyStyle](https://cloud.tencent.com/document/product/647/36778#setbeautystyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://cloud.tencent.com/document/product/647/36778#setwatermark) | Sets watermark. |


### Secondary stream API functions

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://cloud.tencent.com/document/product/647/36778#startremotesubstreamview) | Starts rendering the secondary stream image of a remote user. |
| [stopRemoteSubStreamView](https://cloud.tencent.com/document/product/647/36778#stopremotesubstreamview) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://cloud.tencent.com/document/product/647/36778#setremotesubstreamviewfillmode) | Sets rendering mode of the secondary stream image. |
| [getScreenCaptureSources](https://cloud.tencent.com/document/product/647/36778#getscreencapturesources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://cloud.tencent.com/document/product/647/36778#selectscreencapturetarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://cloud.tencent.com/document/product/647/36778#startscreencapture) | Starts screen sharing. |
| [pauseScreenCapture](https://cloud.tencent.com/document/product/647/36778#pausescreencapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://cloud.tencent.com/document/product/647/36778#resumescreencapture) | Resumes screen sharing. |
| [stopScreenCapture](https://cloud.tencent.com/document/product/647/36778#stopscreencapture) | Stops screen capture. |
| [setSubStreamEncoderParam](https://cloud.tencent.com/document/product/647/36778#setsubstreamencoderparam) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://cloud.tencent.com/document/product/647/36778#setsubstreammixvolume) | Sets audio mixing volume level of the secondary stream. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://cloud.tencent.com/document/product/647/36778#enablecustomvideocapture) | Enables custom video capture mode. |
| [sendCustomVideoData](https://cloud.tencent.com/document/product/647/36778#sendcustomvideodata) | Delivers the captured video data to the SDK. |
| [enableCustomAudioCapture](https://cloud.tencent.com/document/product/647/36778#enablecustomaudiocapture) | Enables the custom audio capture mode. After this mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](https://cloud.tencent.com/document/product/647/36778#sendcustomaudiodata) to continuously insert the captured audio data into the SDK. |
| [sendCustomAudioData](https://cloud.tencent.com/document/product/647/36778#sendcustomaudiodata) | Delivers the captured audio data to the SDK. |
| [setLocalVideoRenderCallback](https://cloud.tencent.com/document/product/647/36778#setlocalvideorendercallback) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](https://cloud.tencent.com/document/product/647/36778#setremotevideorendercallback) | Sets custom rendering for remote video. |
| [setAudioFrameCallback](https://cloud.tencent.com/document/product/647/36778#setaudioframecallback) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://cloud.tencent.com/document/product/647/36778#sendcustomcmdmsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://cloud.tencent.com/document/product/647/36778#sendseimsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://cloud.tencent.com/document/product/647/36778#playbgm) | Starts background music. |
| [stopBGM](https://cloud.tencent.com/document/product/647/36778#stopbgm) | Stops background music. |
| [pauseBGM](https://cloud.tencent.com/document/product/647/36778#pausebgm) | Pauses background music. |
| [resumeBGM](https://cloud.tencent.com/document/product/647/36778#resumebgm) | Resumes background music. |
| [getBGMDuration](https://cloud.tencent.com/document/product/647/36778#getbgmduration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://cloud.tencent.com/document/product/647/36778#setbgmposition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://cloud.tencent.com/document/product/647/36778#setmicvolumeonmixing) | Adjusts the mic volume level when background music is played back. |
| [setBGMVolume](https://cloud.tencent.com/document/product/647/36778#setbgmvolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [startSystemAudioLoopback](https://cloud.tencent.com/document/product/647/36778#startsystemaudioloopback) | Enables system audio capture (the 64-bit SDK currently does not support system audio mixing). |
| [stopSystemAudioLoopback](https://cloud.tencent.com/document/product/647/36778#stopsystemaudioloopback) | Disables system audio capture. |
| [setSystemAudioLoopbackVolume](https://cloud.tencent.com/document/product/647/36778#setsystemaudioloopbackvolume) | Sets system audio capture volume level. |


### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://cloud.tencent.com/document/product/647/36778#playaudioeffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://cloud.tencent.com/document/product/647/36778#setaudioeffectvolume) | Sets sound effect volume level. |
| [stopAudioEffect](https://cloud.tencent.com/document/product/647/36778#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](https://cloud.tencent.com/document/product/647/36778#stopallaudioeffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://cloud.tencent.com/document/product/647/36778#setallaudioeffectsvolume) | Sets volume level of all sound effects. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://cloud.tencent.com/document/product/647/36778#startspeedtest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://cloud.tencent.com/document/product/647/36778#stopspeedtest) | Stops network speed test. |
| [startCameraDeviceTest](https://cloud.tencent.com/document/product/647/36778#startcameradevicetest) | Starts camera test. |
| [stopCameraDeviceTest](https://cloud.tencent.com/document/product/647/36778#stopcameradevicetest) | Stops camera test. |
| [startMicDeviceTest](https://cloud.tencent.com/document/product/647/36778#startmicdevicetest) | Starts mic test. |
| [stopMicDeviceTest](https://cloud.tencent.com/document/product/647/36778#stopmicdevicetest) | Stops mic test. |
| [startSpeakerDeviceTest](https://cloud.tencent.com/document/product/647/36778#startspeakerdevicetest) | Starts speaker test. |
| [stopSpeakerDeviceTest](https://cloud.tencent.com/document/product/647/36778#stopspeakerdevicetest) | Stops speaker test. |


### MixTranscoding and CDN relayed push APIs

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://cloud.tencent.com/document/product/647/36778#setmixtranscodingconfig) | Starts (update) On-Cloud MixTranscoding: this method uses the transcoding service of Tencent Cloud to combine multiple image channels into one channel. |
| [startPublishCDNStream](https://cloud.tencent.com/document/product/647/36778#startpublishcdnstream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://cloud.tencent.com/document/product/647/36778#stoppublishcdnstream) | Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://cloud.tencent.com/document/product/647/36778#getsdkversion) | Gets SDK version information.. |
| [setLogLevel](https://cloud.tencent.com/document/product/647/36778#setloglevel) | Sets log output level. |
| [setConsoleEnabled](https://cloud.tencent.com/document/product/647/36778#setconsoleenabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://cloud.tencent.com/document/product/647/36778#setlogcompressenabled) | Enables or disables local log compression. |
| [setLogDirPath](https://cloud.tencent.com/document/product/647/36778#setlogdirpath) | Sets log storage path. |
| [setLogCallback](https://cloud.tencent.com/document/product/647/36778#setlogcallback) | Sets log callback. |
| [showDebugView](https://cloud.tencent.com/document/product/647/36778#showdebugview) | Displays dashboard. |
| [callExperimentalAPI](https://cloud.tencent.com/document/product/647/36778#callexperimentalapi) | Calls experimental API. |


## TRTCCloudCallback @ TXLiteAVSDK

Callback API class for TRTC video call feature.

### General event callbacks

| API | Description |
|-----|-----|
| [onError](https://cloud.tencent.com/document/product/647/36779#onerror) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://cloud.tencent.com/document/product/647/36779#onwarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://cloud.tencent.com/document/product/647/36779#onenterroom) | Callback of room entry. |
| [onExitRoom](https://cloud.tencent.com/document/product/647/36779#onexitroom) | Callback of room exit. |
| [onSwitchRole](https://cloud.tencent.com/document/product/647/36779#onswitchrole) | Callback of role switching. |
| [onConnectOtherRoom](https://cloud.tencent.com/document/product/647/36779#onconnectotherroom) | Callback of the result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](https://cloud.tencent.com/document/product/647/36779#ondisconnectotherroom) | Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://cloud.tencent.com/document/product/647/36779#onremoteuserenterroom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://cloud.tencent.com/document/product/647/36779#onremoteuserleaveroom) | A user exits the current room. |
| [onUserVideoAvailable](https://cloud.tencent.com/document/product/647/36779#onuservideoavailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://cloud.tencent.com/document/product/647/36779#onusersubstreamavailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://cloud.tencent.com/document/product/647/36779#onuseraudioavailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://cloud.tencent.com/document/product/647/36779#onfirstvideoframe) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://cloud.tencent.com/document/product/647/36779#onfirstaudioframe) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://cloud.tencent.com/document/product/647/36779#onsendfirstlocalvideoframe) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://cloud.tencent.com/document/product/647/36779#onsendfirstlocalaudioframe) | The first local audio frame data has been sent. |
| [onUserEnter](https://cloud.tencent.com/document/product/647/36779#onuserenter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://cloud.tencent.com/document/product/647/36779#onuserexit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://cloud.tencent.com/document/product/647/36779#onnetworkquality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://cloud.tencent.com/document/product/647/36779#onstatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://cloud.tencent.com/document/product/647/36779#onconnectionlost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://cloud.tencent.com/document/product/647/36779#ontrytoreconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://cloud.tencent.com/document/product/647/36779#onconnectionrecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://cloud.tencent.com/document/product/647/36779#onspeedtest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://cloud.tencent.com/document/product/647/36779#oncameradidready) | Camera is ready. |
| [onMicDidReady](https://cloud.tencent.com/document/product/647/36779#onmicdidready) | Mic is ready. |
| [onUserVoiceVolume](https://cloud.tencent.com/document/product/647/36779#onuservoicevolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://cloud.tencent.com/document/product/647/36779#ondevicechange) | Callback of local device connection and disconnection. |
| [onTestMicVolume](https://cloud.tencent.com/document/product/647/36779#ontestmicvolume) | Callback of mic volume level in test. |
| [onTestSpeakerVolume](https://cloud.tencent.com/document/product/647/36779#ontestspeakervolume) | Callback of speaker volume level in test. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://cloud.tencent.com/document/product/647/36779#onrecvcustomcmdmsg) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://cloud.tencent.com/document/product/647/36779#onmisscustomcmdmsg) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://cloud.tencent.com/document/product/647/36779#onrecvseimsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://cloud.tencent.com/document/product/647/36779#onstartpublishcdnstream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://cloud.tencent.com/document/product/647/36779#onstoppublishcdnstream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://cloud.tencent.com/document/product/647/36779#onsetmixtranscodingconfig) | Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://cloud.tencent.com/document/product/647/36779#onaudioeffectfinished) | Callback of ending an audio effect. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://cloud.tencent.com/document/product/647/36779#onscreencapturecovered) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://cloud.tencent.com/document/product/647/36779#onscreencapturestarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://cloud.tencent.com/document/product/647/36779#onscreencapturepaused) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://cloud.tencent.com/document/product/647/36779#onscreencaptureresumed) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://cloud.tencent.com/document/product/647/36779#onscreencapturestoped) | This callback will be returned by the SDK when screen sharing is stopped. |


### Background audio mixing event callbacks

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://cloud.tencent.com/document/product/647/36779#onplaybgmbegin) | Playback of background music starts. |
| [onPlayBGMProgress](https://cloud.tencent.com/document/product/647/36779#onplaybgmprogress) | Progress of background music playback. |
| [onPlayBGMComplete](https://cloud.tencent.com/document/product/647/36779#onplaybgmcomplete) | Playback of background music ends. |


### Custom video rendering callbacks
This callback API is defined by the [ITRTCVideoRenderCallback](https://cloud.tencent.com/document/product/647/36779#itrtcvideorendercallback) class.

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://cloud.tencent.com/document/product/647/36779#onrendervideoframe) | Callback of custom video rendering. |


### Audio data callbacks
This callback API is defined by the [ITRTCAudioFrameCallback](https://cloud.tencent.com/document/product/647/36779#itrtcaudioframecallback) class.

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://cloud.tencent.com/document/product/647/36779#oncapturedaudioframe) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://cloud.tencent.com/document/product/647/36779#onplayaudioframe) | Audio data from each remote user before audio mixing (for example, if you need to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing). |
| [onMixedPlayAudioFrame](https://cloud.tencent.com/document/product/647/36779#onmixedplayaudioframe) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
This callback API is defined by the [ITRTCLogCallback](https://cloud.tencent.com/document/product/647/36779#itrtclogcallback) class.

| API | Description |
|-----|-----|
| [onLog](https://cloud.tencent.com/document/product/647/36779#onlog) | Callback of log printing. |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://cloud.tencent.com/document/product/647/36780#trtcparams) | Room entry parameters. |
| [TRTCVideoEncParam](https://cloud.tencent.com/document/product/647/36780#trtcvideoencparam) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://cloud.tencent.com/document/product/647/36780#trtcnetworkqosparam) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://cloud.tencent.com/document/product/647/36780#trtcqualityinfo) | Video quality. |
| [TRTCVolumeInfo](https://cloud.tencent.com/document/product/647/36780#trtcvolumeinfo) | Volume level. |
| [TRTCSpeedTestResult](https://cloud.tencent.com/document/product/647/36780#trtcspeedtestresult) | Network speed test result. |
| [TRTCMixUser](https://cloud.tencent.com/document/product/647/36780#trtcmixuser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://cloud.tencent.com/document/product/647/36780#trtctranscodingconfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://cloud.tencent.com/document/product/647/36780#trtcpublishcdnparam) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://cloud.tencent.com/document/product/647/36780#trtcaudiorecordingparams) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://cloud.tencent.com/document/product/647/36780#trtcaudioeffectparam) | Sound effect. |
| [TRTCLocalStatistics](https://cloud.tencent.com/document/product/647/36780#trtclocalstatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](https://cloud.tencent.com/document/product/647/36780#trtcremotestatistics) | Remote audio/video statistics. |
| [TRTCStatistics](https://cloud.tencent.com/document/product/647/36780#trtcstatistics) | Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://cloud.tencent.com/document/product/647/36780#trtcvideoresolution) | Video resolution. |
| [TRTCVideoResolutionMode](https://cloud.tencent.com/document/product/647/36780#trtcvideoresolutionmode) | Video resolution mode. |
| [TRTCVideoStreamType](https://cloud.tencent.com/document/product/647/36780#trtcvideostreamtype) | Video stream type. |
| [TRTCQuality](https://cloud.tencent.com/document/product/647/36780#trtcquality) | Image quality level. |
| [TRTCVideoFillMode](https://cloud.tencent.com/document/product/647/36780#trtcvideofillmode) | Video image fill mode. |
| [TRTCBeautyStyle](https://cloud.tencent.com/document/product/647/36780#trtcbeautystyle) | Beauty filter (skin smoothing) algorithm. |
| [TRTCAppScene](https://cloud.tencent.com/document/product/647/36780#trtcappscene) | Application scenario. |
| [TRTCRoleType](https://cloud.tencent.com/document/product/647/36780#trtcroletype) | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://cloud.tencent.com/document/product/647/36780#trtcqoscontrolmode) | Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://cloud.tencent.com/document/product/647/36780#trtcvideoqospreference) | Image quality preference. |
| [TRTCLogLevel](https://cloud.tencent.com/document/product/647/36780#trtcloglevel) | Log level. |
| [TRTCDeviceState](https://cloud.tencent.com/document/product/647/36780#trtcdevicestate) | Device operation. |
| [TRTCDeviceType](https://cloud.tencent.com/document/product/647/36780#trtcdevicetype) | Device type. |
| [TRTCWaterMarkSrcType](https://cloud.tencent.com/document/product/647/36780#trtcwatermarksrctype) | Watermark image source type. |
| [TRTCTranscodingConfigMode](https://cloud.tencent.com/document/product/647/36780#trtctranscodingconfigmode) | MixTranscoding parameter configuration mode. |


