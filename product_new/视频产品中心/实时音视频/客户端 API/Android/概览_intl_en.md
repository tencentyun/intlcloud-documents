## TRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.

### Basic methods

| API | Description |
|-----|-----|
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/32264#sharedinstance) | Creates [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/32264#trtccloud) singleton. |
| [destroySharedInstance](https://intl.cloud.tencent.com/document/product/647/32264#destroysharedinstance) | Terminates [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/32264#trtccloud) singleton. |
| [setListener](https://intl.cloud.tencent.com/document/product/647/32264#setlistener) | Sets the `TRTCCloudListener` callback API, through which users can get various status notifications from [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/32264#trtccloud). |
| [setListenerHandler](https://intl.cloud.tencent.com/document/product/647/32264#setlistenerhandler) | Sets the queue that drives the [TRTCCloudListener](https://intl.cloud.tencent.com/document/product/647/32265#trtccloudlistener) callback. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/32264#enterroom) | Enters room. |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/32264#exitroom) | Exits room. |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/32264#switchrole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [ConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/32264#connectotherroom) | Requests cross-room call (anchor competition). |
| [DisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/32264#disconnectotherroom) | Exits cross-room call. |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/32264#setdefaultstreamrecvmode) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/32264#startlocalpreview) | Enables preview image of local video. |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/32264#stoplocalpreview) | Stops local video capture and preview. |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/32264#mutelocalvideo) | Specifies whether to block local video image. |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/32264#startremoteview) | Starts displaying remote video image. |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/32264#stopremoteview) | Stops displaying remote video image. |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/32264#stopallremoteview) | Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/32264#muteremotevideostream) | Pauses receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/32264#muteallremotevideostreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/32264#setvideoencoderparam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/32264#setnetworkqosparam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/32264#setlocalviewfillmode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/32264#setremoteviewfillmode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/32264#setlocalviewrotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/32264#setremoteviewrotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/32264#setvideoencoderrotation) | Sets direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server). |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/32264#setlocalviewmirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/32264#setvideoencodermirror) | Sets mirror mode of image output by encoder. |
| [setGSensorMode](https://intl.cloud.tencent.com/document/product/647/32264#setgsensormode) | Sets adaptation mode of the g-sensor. |
| [enableEncSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/32264#enableencsmallvideostream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/32264#setremotevideostreamtype) | Specifies whether to view the big or small image of the specified `uid`. |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/32264#setpriorremotevideostreamtype) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/32264#startlocalaudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/32264#stoplocalaudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/32264#mutelocalaudio) | Mutes local audio. |
| [setAudioRoute](https://intl.cloud.tencent.com/document/product/647/32264#setaudioroute) | Sets audio routing. |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/32264#muteremoteaudio) | Mutes user's audio. |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/32264#muteallremoteaudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/32264#enableaudiovolumeevaluation) | Enables volume reminder. |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/32264#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/32264#stopaudiorecording) | Stops audio recording. |
| [setSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/32264#setsystemvolumetype) | Sets the system volume type used during call. |
| [enableAudioEarMonitoring](https://intl.cloud.tencent.com/document/product/647/32264#enableaudioearmonitoring) | Enables in-ear monitoring. |

### Camera API functions

| API | Description |
|-----|-----|
| [switchCamera](https://intl.cloud.tencent.com/document/product/647/32264#switchcamera) | Switches cameras. |
| [isCameraZoomSupported](https://intl.cloud.tencent.com/document/product/647/32264#iscamerazoomsupported) | Queries whether the current camera supports zoom. |
| [setZoom](https://intl.cloud.tencent.com/document/product/647/32264#setzoom) | Sets zoom factor (focal length) of camera. |
| [isCameraTorchSupported](https://intl.cloud.tencent.com/document/product/647/32264#iscameratorchsupported) | Queries whether the device supports flash (flash mode). |
| [enableTorch](https://intl.cloud.tencent.com/document/product/647/32264#enabletorch) | Enables or disables flash. |
| [isCameraFocusPositionInPreviewSupported](https://intl.cloud.tencent.com/document/product/647/32264#iscamerafocuspositioninpreviewsupported) | Queries whether the device supports setting focus. |
| [setFocusPosition](https://cloud.tencent.com/document/product/647/32264#setfocusposition) | Sets camera focus. |
| [isCameraAutoFocusFaceModeSupported](https://cloud.tencent.com/document/product/647/32264#iscameraautofocusfacemodesupported) | Queries whether the device supports automatic recognition of face position. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [getBeautyManager](https://cloud.tencent.com/document/product/647/32264#getbeautymanager) | Gets the beauty filter management object. |
| [setBeautyStyle](https://cloud.tencent.com/document/product/647/32264#setbeautystyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setFilter](https://cloud.tencent.com/document/product/647/32264#setfilter) | Specifies material filter effect. |
| [setFilterConcentration](https://cloud.tencent.com/document/product/647/32264#setfilterconcentration) | Sets effect level of a filter. |
| [setWatermark](https://cloud.tencent.com/document/product/647/32264#setwatermark) | Adds a watermark. |
| [setEyeScaleLevel](https://cloud.tencent.com/document/product/647/32264#seteyescalelevel) | Sets effect level of the eye enlarging filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceSlimLevel](https://cloud.tencent.com/document/product/647/32264#setfaceslimlevel) | Sets effect level of the face slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceVLevel](https://cloud.tencent.com/document/product/647/32264#setfacevlevel) | Sets effect level of the chin slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceShortLevel](https://cloud.tencent.com/document/product/647/32264#setfaceshortlevel) | Sets effect level of the face shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setChinLevel](https://cloud.tencent.com/document/product/647/32264#setchinlevel) | Sets effect level of the chin lengthening/shortening or shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setNoseSlimLevel](https://cloud.tencent.com/document/product/647/32264#setnoseslimlevel) | Sets effect level of the nose slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setGreenScreenFile](https://cloud.tencent.com/document/product/647/32264#setgreenscreenfile) | Sets green screen video (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [selectMotionTmpl](https://cloud.tencent.com/document/product/647/32264#selectmotiontmpl) | Selects AI animated effect pendant (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setMotionMute](https://cloud.tencent.com/document/product/647/32264#setmotionmute) | Mutes animated effect (it takes effect only in TRTC Commercial edition and is invalid in other editions). |


### Secondary stream API functions

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://cloud.tencent.com/document/product/647/32264#startremotesubstreamview) | Starts displaying screen sharing image of a remote user. |
| [stopRemoteSubStreamView](https://cloud.tencent.com/document/product/647/32264#stopremotesubstreamview) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://cloud.tencent.com/document/product/647/32264#setremotesubstreamviewfillmode) | Sets display mode of screen sharing image. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://cloud.tencent.com/document/product/647/32264#enablecustomvideocapture) | Enables custom video capture mode. |
| [sendCustomVideoData](https://cloud.tencent.com/document/product/647/32264#sendcustomvideodata) | Delivers the captured video data to the SDK. |
| [setLocalVideoRenderListener](https://cloud.tencent.com/document/product/647/32264#setlocalvideorenderlistener) | Sets callback of custom rendering for local video. |
| [setRemoteVideoRenderListener](https://cloud.tencent.com/document/product/647/32264#setremotevideorenderlistener) | Sets callback of custom rendering for remote video. |
| [enableCustomAudioCapture](https://cloud.tencent.com/document/product/647/32264#enablecustomaudiocapture) | Enables custom audio capture mode. |
| [sendCustomAudioData](https://cloud.tencent.com/document/product/647/32264#sendcustomaudiodata) | Delivers the captured audio data to the SDK. |
| [setAudioFrameListener](https://cloud.tencent.com/document/product/647/32264#setaudioframelistener) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://cloud.tencent.com/document/product/647/32264#sendcustomcmdmsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://cloud.tencent.com/document/product/647/32264#sendseimsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://cloud.tencent.com/document/product/647/32264#playbgm) | Starts background music. |
| [stopBGM](https://cloud.tencent.com/document/product/647/32264#stopbgm) | Stops background music. |
| [pauseBGM](https://cloud.tencent.com/document/product/647/32264#pausebgm) | Pauses background music. |
| [resumeBGM](https://cloud.tencent.com/document/product/647/32264#resumebgm) | Resumes background music. |
| [getBGMDuration](https://cloud.tencent.com/document/product/647/32264#getbgmduration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://cloud.tencent.com/document/product/647/32264#setbgmposition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://cloud.tencent.com/document/product/647/32264#setmicvolumeonmixing) | Adjusts the mic volume level when background music is played back. |
| [setBGMVolume](https://cloud.tencent.com/document/product/647/32264#setbgmvolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [setReverbType](https://cloud.tencent.com/document/product/647/32264#setreverbtype) | Sets reverb effect. |
| [setVoiceChangerType](https://cloud.tencent.com/document/product/647/32264#setvoicechangertype) | Sets voice changer type. |

### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://cloud.tencent.com/document/product/647/32264#playaudioeffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://cloud.tencent.com/document/product/647/32264#setaudioeffectvolume) | Sets volume level of a single sound effect. |
| [stopAudioEffect](https://cloud.tencent.com/document/product/647/32264#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](https://cloud.tencent.com/document/product/647/32264#stopallaudioeffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://cloud.tencent.com/document/product/647/32264#setallaudioeffectsvolume) | Sets volume level of all sound effects. |


### Network test

| API | Description |
|-----|-----|
| [startSpeedTest](https://cloud.tencent.com/document/product/647/32264#startspeedtest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://cloud.tencent.com/document/product/647/32264#stopspeedtest) | Stops server speed test. |


### MixTranscoding and release to CDN

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://cloud.tencent.com/document/product/647/32264#setmixtranscodingconfig) | Sets On-Cloud MixTranscoding parameters. |
| [startPublishCDNStream](https://cloud.tencent.com/document/product/647/32264#startpublishcdnstream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://cloud.tencent.com/document/product/647/32264#stoppublishcdnstream) | Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://cloud.tencent.com/document/product/647/32264#getsdkversion) | Gets SDK version information.. |
| [setLogLevel](https://cloud.tencent.com/document/product/647/32264#setloglevel) | Sets log output level. |
| [setConsoleEnabled](https://cloud.tencent.com/document/product/647/32264#setconsoleenabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://cloud.tencent.com/document/product/647/32264#setlogcompressenabled) | Enables or disables local log compression. |
| [setLogDirPath](https://cloud.tencent.com/document/product/647/32264#setlogdirpath) | Modifies log storage path. |
| [setLogListener](https://cloud.tencent.com/document/product/647/32264#setloglistener) | Sets log callback. |
| [showDebugView](https://cloud.tencent.com/document/product/647/32264#showdebugview) | Displays dashboard. |
| [setDebugViewMargin](https://cloud.tencent.com/document/product/647/32264#setdebugviewmargin) | Sets dashboard margin. |
| [callExperimentalAPI](https://cloud.tencent.com/document/product/647/32264#callexperimentalapi) | Calls experimental API. |


### Callback APIs of background music playback

Callback APIs of background music playback.

| API | Description |
|-----|-----|
| [onBGMStart](https://cloud.tencent.com/document/product/647/32264#onbgmstart) | Callback notification of music playback start. |
| [onBGMProgress](https://cloud.tencent.com/document/product/647/32264#onbgmprogress) | Callback notification of music playback progress. |
| [onBGMComplete](https://cloud.tencent.com/document/product/647/32264#onbgmcomplete) | Callback notification of music playback end. |

### Others

| API | Description |
|-----|-----|
| [TRTCViewMargin](https://cloud.tencent.com/document/product/647/32264#trtcviewmargin) | View margin. |

## TRTCCloudListener @ TXLiteAVSDK

Event callback API for TRTC video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](https://cloud.tencent.com/document/product/647/32265#onerror) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://cloud.tencent.com/document/product/647/32265#onwarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://cloud.tencent.com/document/product/647/32265#onenterroom) | Callback of room entry. |
| [onExitRoom](https://cloud.tencent.com/document/product/647/32265#onexitroom) | Callback of room exit. |
| [onSwitchRole](https://cloud.tencent.com/document/product/647/32265#onswitchrole) | Callback of role switching. |
| [onConnectOtherRoom](https://cloud.tencent.com/document/product/647/32265#onconnectotherroom) | Callback of the result of requesting cross-room call (anchor competition). |
| [onDisConnectOtherRoom](https://cloud.tencent.com/document/product/647/32265#ondisconnectotherroom) | Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://cloud.tencent.com/document/product/647/32265#onremoteuserenterroom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://cloud.tencent.com/document/product/647/32265#onremoteuserleaveroom) | A user exits the current room. |
| [onUserVideoAvailable](https://cloud.tencent.com/document/product/647/32265#onuservideoavailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://cloud.tencent.com/document/product/647/32265#onusersubstreamavailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://cloud.tencent.com/document/product/647/32265#onuseraudioavailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://cloud.tencent.com/document/product/647/32265#onfirstvideoframe) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://cloud.tencent.com/document/product/647/32265#onfirstaudioframe) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://cloud.tencent.com/document/product/647/32265#onsendfirstlocalvideoframe) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://cloud.tencent.com/document/product/647/32265#onsendfirstlocalaudioframe) | The first local audio frame data has been sent. |
| [onUserEnter](https://cloud.tencent.com/document/product/647/32265#onuserenter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://cloud.tencent.com/document/product/647/32265#onuserexit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://cloud.tencent.com/document/product/647/32265#onnetworkquality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://cloud.tencent.com/document/product/647/32265#onstatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://cloud.tencent.com/document/product/647/32265#onconnectionlost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://cloud.tencent.com/document/product/647/32265#ontrytoreconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://cloud.tencent.com/document/product/647/32265#onconnectionrecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://cloud.tencent.com/document/product/647/32265#onspeedtest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://cloud.tencent.com/document/product/647/32265#oncameradidready) | Camera is ready. |
| [onMicDidReady](https://cloud.tencent.com/document/product/647/32265#onmicdidready) | Mic is ready. |
| [onAudioRouteChanged](https://cloud.tencent.com/document/product/647/32265#onaudioroutechanged) | Audio routing changes, i.e., whether the audio is output by speaker or receiver. |
| [onUserVoiceVolume](https://cloud.tencent.com/document/product/647/32265#onuservoicevolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://cloud.tencent.com/document/product/647/32265#onrecvcustomcmdmsg) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://cloud.tencent.com/document/product/647/32265#onmisscustomcmdmsg) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://cloud.tencent.com/document/product/647/32265#onrecvseimsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://cloud.tencent.com/document/product/647/32265#onstartpublishcdnstream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://cloud.tencent.com/document/product/647/32265#onstoppublishcdnstream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://cloud.tencent.com/document/product/647/32265#onsetmixtranscodingconfig) | Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in [TRTCCloud](https://cloud.tencent.com/document/product/647/32264#trtccloud). |

### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://cloud.tencent.com/document/product/647/32265#onaudioeffectfinished) | Callback of ending an audio effect. |

### Custom video data frame rendering callbacks
Redirect to [TRTCVideoRenderListener](https://cloud.tencent.com/document/product/647/32265#trtcvideorenderlistener)

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://cloud.tencent.com/document/product/647/32265#onrendervideoframe) | Callback of custom video rendering. |


### Custom audio data frame processing callbacks (read only)
Redirect to [TRTCAudioFrameListener](https://cloud.tencent.com/document/product/647/32265#trtcaudioframelistener)

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://cloud.tencent.com/document/product/647/32265#oncapturedaudioframe) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://cloud.tencent.com/document/product/647/32265#onplayaudioframe) | Audio data from each remote user before audio mixing (for example, if you want to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing). |
| [onMixedPlayAudioFrame](https://cloud.tencent.com/document/product/647/32265#onmixedplayaudioframe) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
Redirect to [TRTCLogListener](https://cloud.tencent.com/document/product/647/32265#trtcloglistener)

It is recommended to set the callback object in a class that is initialized early, e.g., `Application`.

| API | Description |
|-----|-----|
| [onLog](https://cloud.tencent.com/document/product/647/32265#onlog) | Callback of log printing. |


## Definitions of Key Classes
| API | Description |
|-----|-----|
| [TRTCParams](https://cloud.tencent.com/document/product/647/32266#trtcparams) | Room entry parameters. |
| [TRTCVideoEncParam](https://cloud.tencent.com/document/product/647/32266#trtcvideoencparam) | Encoding parameters. |
| [TRTCNetworkQosParam](https://cloud.tencent.com/document/product/647/32266#trtcnetworkqosparam) | Network bandwidth limit parameters. |
| [TRTCQuality](https://cloud.tencent.com/document/product/647/32266#trtcquality) | Video (or network) quality. |
| [TRTCTexture](https://cloud.tencent.com/document/product/647/32266#trtctexture) | Video texture data, including texture ID and EGL environment. |
| [TRTCVideoFrame](https://cloud.tencent.com/document/product/647/32266#trtcvideoframe) | Video frame information. |
| [TRTCAudioFrame](https://cloud.tencent.com/document/product/647/32266#trtcaudioframe) | Audio frame data. |
| [TRTCVolumeInfo](https://cloud.tencent.com/document/product/647/32266#trtcvolumeinfo) | Volume level. |
| [TRTCSpeedTestResult](https://cloud.tencent.com/document/product/647/32266#trtcspeedtestresult) | Network speed test result. |
| [TRTCMixUser](https://cloud.tencent.com/document/product/647/32266#trtcmixuser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://cloud.tencent.com/document/product/647/32266#trtctranscodingconfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://cloud.tencent.com/document/product/647/32266#trtcpublishcdnparam) | relayed push parameters. |
| [TRTCAudioRecordingParams](https://cloud.tencent.com/document/product/647/32266#trtcaudiorecordingparams) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://cloud.tencent.com/document/product/647/32266#trtcaudioeffectparam) | Sound effect. |
| [TRTCStatistics](https://cloud.tencent.com/document/product/647/32266#trtcstatistics) | Statistics. |
| [TRTCRemoteStatistics](https://cloud.tencent.com/document/product/647/32266#trtcremotestatistics) | Remote audio/video statistics. |
| [TRTCLocalStatistics](https://cloud.tencent.com/document/product/647/32266#trtclocalstatistics) | Local audio/video statistics. |
