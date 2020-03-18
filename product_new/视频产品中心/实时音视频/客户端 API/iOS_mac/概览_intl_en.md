## TRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.

### Creation and termination

| API | Description |
|-----|-----|
| [delegate](https://intl.cloud.tencent.com/document/product/647/35120#delegate) | Sets the `TRTCCloudDelegate` callback API. |
| [delegateQueue](https://intl.cloud.tencent.com/document/product/647/35120#delegatequeue) | Sets the queue that drives the `TRTCCloudDelegate` callback. |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/35120#sharedinstance) | Creates [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35120#trtccloud) singleton. |
| [destroySharedIntance](https://intl.cloud.tencent.com/document/product/647/35120#destroysharedintance) | Terminates [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35120#trtccloud) singleton. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](https://intl.cloud.tencent.com/document/product/647/35120#enterroom) | Enters room. |
| [exitRoom](https://intl.cloud.tencent.com/document/product/647/35120#exitroom) | Exits room. |
| [switchRole](https://intl.cloud.tencent.com/document/product/647/35120#switchrole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [connectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35120#connectotherroom) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35120#disconnectotherroom) | Exits cross-room call. |
| [setDefaultStreamRecvMode](https://intl.cloud.tencent.com/document/product/647/35120#setdefaultstreamrecvmode) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35120#startlocalpreview) | Enables preview image of local video (for iOS). |
| [startLocalPreview](https://intl.cloud.tencent.com/document/product/647/35120#startlocalpreview2) | Enables preview image of local video (for macOS). |
| [stopLocalPreview](https://intl.cloud.tencent.com/document/product/647/35120#stoplocalpreview) | Stops local video capture and preview. |
| [muteLocalVideo](https://intl.cloud.tencent.com/document/product/647/35120#mutelocalvideo) | Specifies whether to block local video image. |
| [startRemoteView](https://intl.cloud.tencent.com/document/product/647/35120#startremoteview) | Starts displaying remote video image. |
| [stopRemoteView](https://intl.cloud.tencent.com/document/product/647/35120#stopremoteview) | Stops displaying remote video image. |
| [stopAllRemoteView](https://intl.cloud.tencent.com/document/product/647/35120#stopallremoteview) | Stops displaying all remote video images. |
| [muteRemoteVideoStream](https://intl.cloud.tencent.com/document/product/647/35120#muteremotevideostream) | Pauses receiving the specified remote video stream. |
| [muteAllRemoteVideoStreams](https://intl.cloud.tencent.com/document/product/647/35120#muteallremotevideostreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://intl.cloud.tencent.com/document/product/647/35120#setvideoencoderparam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35120#setnetworkqosparam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://intl.cloud.tencent.com/document/product/647/35120#setlocalviewfillmode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://intl.cloud.tencent.com/document/product/647/35120#setremoteviewfillmode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://intl.cloud.tencent.com/document/product/647/35120#setlocalviewrotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://intl.cloud.tencent.com/document/product/647/35120#setremoteviewrotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://intl.cloud.tencent.com/document/product/647/35120#setvideoencoderrotation) | Sets direction of image output by video encoder (i.e., video image viewed by remote user or recorded by server). |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35120#setlocalviewmirror) | Sets mirror mode of local camera's preview image (for iOS). |
| [setLocalViewMirror](https://intl.cloud.tencent.com/document/product/647/35120#setlocalviewmirror2) | Sets mirror mode of local camera's preview image (for macOS). |
| [setVideoEncoderMirror](https://intl.cloud.tencent.com/document/product/647/35120#setvideoencodermirror) | Sets mirror mode of image output by encoder. |
| [setGSensorMode](https://intl.cloud.tencent.com/document/product/647/35120#setgsensormode) | Sets adaptation mode of the g-sensor. |
| [enableEncSmallVideoStream](https://intl.cloud.tencent.com/document/product/647/35120#enableencsmallvideostream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35120#setremotevideostreamtype) | Specifies whether to view the big or small image of the specified `uid`. |
| [setPriorRemoteVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35120#setpriorremotevideostreamtype) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://intl.cloud.tencent.com/document/product/647/35120#startlocalaudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://intl.cloud.tencent.com/document/product/647/35120#stoplocalaudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://intl.cloud.tencent.com/document/product/647/35120#mutelocalaudio) | Mutes local audio. |
| [setAudioRoute](https://intl.cloud.tencent.com/document/product/647/35120#setaudioroute) | Sets audio routing. |
| [muteRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35120#muteremoteaudio) | Mutes user's audio. |
| [muteAllRemoteAudio](https://intl.cloud.tencent.com/document/product/647/35120#muteallremoteaudio) | Mutes all users' audio. |
| [enableAudioVolumeEvaluation](https://intl.cloud.tencent.com/document/product/647/35120#enableaudiovolumeevaluation) | Enables volume reminder. |
| [startAudioRecording](https://intl.cloud.tencent.com/document/product/647/35120#startaudiorecording) | Starts audio recording. |
| [stopAudioRecording](https://intl.cloud.tencent.com/document/product/647/35120#stopaudiorecording) | Stops audio recording. |
| [setSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35120#setsystemvolumetype) | Sets the system volume type used during call. |
| [enableAudioEarMonitoring](https://intl.cloud.tencent.com/document/product/647/35120#enableaudioearmonitoring) | Enables in-ear monitoring. |


### Camera API functions

| API | Description |
|-----|-----|
| [switchCamera](https://intl.cloud.tencent.com/document/product/647/35120#switchcamera) | Switches cameras. |
| [isCameraZoomSupported](https://intl.cloud.tencent.com/document/product/647/35120#iscamerazoomsupported) | Queries whether the current camera supports zoom. |
| [setZoom](https://intl.cloud.tencent.com/document/product/647/35120#setzoom) | Sets zoom factor (focal length) of camera. |
| [isCameraTorchSupported](https://intl.cloud.tencent.com/document/product/647/35120#iscameratorchsupported) | Queries whether the device supports flash (flash mode). |
| [enbaleTorch](https://intl.cloud.tencent.com/document/product/647/35120#enbaletorch) | Enables or disables flash. |
| [isCameraFocusPositionInPreviewSupported](https://intl.cloud.tencent.com/document/product/647/35120#iscamerafocuspositioninpreviewsupported) | Queries whether the device supports setting focus. |
| [setFocusPosition](https://intl.cloud.tencent.com/document/product/647/35120#setfocusposition) | Sets camera focus. |
| [isCameraAutoFocusFaceModeSupported](https://intl.cloud.tencent.com/document/product/647/35120#iscameraautofocusfacemodesupported) | Queries whether the device supports automatic recognition of face position. |
| [enableAutoFaceFoucs](https://intl.cloud.tencent.com/document/product/647/35120#enableautofacefoucs) | Enables automatic recognition of face position. |
| [getCameraDevicesList](https://intl.cloud.tencent.com/document/product/647/35120#getcameradeviceslist) | Gets list of cameras. |
| [getCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35120#getcurrentcameradevice) | Gets the currently used camera. |
| [setCurrentCameraDevice](https://intl.cloud.tencent.com/document/product/647/35120#setcurrentcameradevice) | Sets the camera to be used. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](https://intl.cloud.tencent.com/document/product/647/35120#getmicdeviceslist) | Gets list of mics. |
| [getCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35120#getcurrentmicdevice) | Gets the current mic device. |
| [setCurrentMicDevice](https://intl.cloud.tencent.com/document/product/647/35120#setcurrentmicdevice) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35120#getcurrentmicdevicevolume) | Gets current mic volume level. |
| [setCurrentMicDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35120#setcurrentmicdevicevolume) | Sets mic volume level. |
| [getSpeakerDevicesList](https://intl.cloud.tencent.com/document/product/647/35120#getspeakerdeviceslist) | Gets list of speakers. |
| [getCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35120#getcurrentspeakerdevice) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://intl.cloud.tencent.com/document/product/647/35120#setcurrentspeakerdevice) | Sets the speaker to be used. |
| [getCurrentSpeakerDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35120#getcurrentspeakerdevicevolume) | Gets current speaker volume level. |
| [setCurrentSpeakerDeviceVolume](https://intl.cloud.tencent.com/document/product/647/35120#setcurrentspeakerdevicevolume) | Sets current speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [getBeautyManager](https://intl.cloud.tencent.com/document/product/647/35120#getbeautymanager) | Gets the beauty filter management object. |
| [setBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35120#setbeautystyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setFilter](https://intl.cloud.tencent.com/document/product/647/35120#setfilter) | Specifies material filter effect. |
| [setFilterConcentration](https://intl.cloud.tencent.com/document/product/647/35120#setfilterconcentration) | Sets effect level of a filter. |
| [setWatermark](https://intl.cloud.tencent.com/document/product/647/35120#setwatermark) | Adds a watermark. |
| [setEyeScaleLevel](https://intl.cloud.tencent.com/document/product/647/35120#seteyescalelevel) | Sets effect level of the eye enlarging filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceScaleLevel](https://intl.cloud.tencent.com/document/product/647/35120#setfacescalelevel) | Sets effect level of the face slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceVLevel](https://intl.cloud.tencent.com/document/product/647/35120#setfacevlevel) | Sets effect level of the chin slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setChinLevel](https://intl.cloud.tencent.com/document/product/647/35120#setchinlevel) | Sets effect level of the chin lengthening/shortening or shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setFaceShortLevel](https://intl.cloud.tencent.com/document/product/647/35120#setfaceshortlevel) | Sets effect level of the face shortening filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setNoseSlimLevel](https://intl.cloud.tencent.com/document/product/647/35120#setnoseslimlevel) | Sets effect level of the nose slimming filter (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setGreenScreenFile](https://intl.cloud.tencent.com/document/product/647/35120#setgreenscreenfile) | Sets green screen video (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [selectMotionTmpl](https://intl.cloud.tencent.com/document/product/647/35120#selectmotiontmpl) | Selects AI animated effect pendant (it takes effect only in TRTC Commercial edition and is invalid in other editions). |
| [setMotionMute](https://intl.cloud.tencent.com/document/product/647/35120#setmotionmute) | Mutes animated effect (it takes effect only in TRTC Commercial edition and is invalid in other editions). |


### Secondary stream API functions (macOS)

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35120#startremotesubstreamview) | Starts displaying screen sharing image of a remote user. |
| [stopRemoteSubStreamView](https://intl.cloud.tencent.com/document/product/647/35120#stopremotesubstreamview) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://intl.cloud.tencent.com/document/product/647/35120#setremotesubstreamviewfillmode) | Sets display mode of screen sharing image. |
| [getScreenCaptureSourcesWithThumbnailSize](https://intl.cloud.tencent.com/document/product/647/35120#getscreencapturesourceswiththumbnailsize) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://intl.cloud.tencent.com/document/product/647/35120#selectscreencapturetarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://intl.cloud.tencent.com/document/product/647/35120#startscreencapture) | Starts screen sharing. |
| [stopScreenCapture](https://intl.cloud.tencent.com/document/product/647/35120#stopscreencapture) | Stops screen capture. |
| [pauseScreenCapture](https://intl.cloud.tencent.com/document/product/647/35120#pausescreencapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://intl.cloud.tencent.com/document/product/647/35120#resumescreencapture) | Resumes screen sharing. |
| [setSubStreamEncoderParam](https://intl.cloud.tencent.com/document/product/647/35120#setsubstreamencoderparam) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://intl.cloud.tencent.com/document/product/647/35120#setsubstreammixvolume) | Sets audio mixing volume level of screen sharing. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://intl.cloud.tencent.com/document/product/647/35120#enablecustomvideocapture) | Enables custom video capture mode. |
| [sendCustomVideoData](https://intl.cloud.tencent.com/document/product/647/35120#sendcustomvideodata) | Delivers the captured video data to the SDK. |
| [setLocalVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35120#setlocalvideorenderdelegate) | Sets callback of custom rendering for local video. |
| [setRemoteVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35120#setremotevideorenderdelegate) | Sets callback of custom rendering for remote video. |
| [enableCustomAudioCapture](https://intl.cloud.tencent.com/document/product/647/35120#enablecustomaudiocapture) | Enables custom audio capture mode. |
| [sendCustomAudioData](https://intl.cloud.tencent.com/document/product/647/35120#sendcustomaudiodata) | Delivers the captured audio data to the SDK. |
| [setAudioFrameDelegate](https://intl.cloud.tencent.com/document/product/647/35120#setaudioframedelegate) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://intl.cloud.tencent.com/document/product/647/35120#sendcustomcmdmsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://intl.cloud.tencent.com/document/product/647/35120#sendseimsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing API functions

| API | Description |
|-----|-----|
| [playBGM](https://intl.cloud.tencent.com/document/product/647/35120#playbgm) | Starts background music. |
| [stopBGM](https://intl.cloud.tencent.com/document/product/647/35120#stopbgm) | Stops background music. |
| [pauseBGM](https://intl.cloud.tencent.com/document/product/647/35120#pausebgm) | Pauses background music. |
| [resumeBGM](https://intl.cloud.tencent.com/document/product/647/35120#resumebgm) | Resumes background music. |
| [getBGMDuration](https://intl.cloud.tencent.com/document/product/647/35120#getbgmduration) | Gets the total length of the music file in milliseconds. |
| [setBGMPosition](https://intl.cloud.tencent.com/document/product/647/35120#setbgmposition) | Sets playback progress of background music. |
| [setMicVolumeOnMixing](https://intl.cloud.tencent.com/document/product/647/35120#setmicvolumeonmixing) | Adjusts the mic volume level when background music is played back. |
| [setBGMVolume](https://intl.cloud.tencent.com/document/product/647/35120#setbgmvolume) | Sets background music volume level. This API is used to control the background music volume level during playback. |
| [setReverbType](https://intl.cloud.tencent.com/document/product/647/35120#setreverbtype) | Sets reverb effect (currently, this is supported only for iOS). |
| [setVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35120#setvoicechangertype) | Sets voice changer type (currently, this is supported only for iOS). |

### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://intl.cloud.tencent.com/document/product/647/35120#playaudioeffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://intl.cloud.tencent.com/document/product/647/35120#setaudioeffectvolume) | Sets volume level of a single sound effect. |
| [stopAudioEffect](https://intl.cloud.tencent.com/document/product/647/35120#stopaudioeffect) | Stops sound effect. |
| [stopAllAudioEffects](https://intl.cloud.tencent.com/document/product/647/35120#stopallaudioeffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://intl.cloud.tencent.com/document/product/647/35120#setallaudioeffectsvolume) | Sets volume level of all sound effects. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://intl.cloud.tencent.com/document/product/647/35120#startspeedtest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://intl.cloud.tencent.com/document/product/647/35120#stopspeedtest) | Stops server speed test. |
| [startCameraDeviceTestInView](https://intl.cloud.tencent.com/document/product/647/35120#startcameradevicetestinview) | Starts camera test. |
| [stopCameraDeviceTest](https://intl.cloud.tencent.com/document/product/647/35120#stopcameradevicetest) | Stops video test preview. |
| [startMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35120#startmicdevicetest) | Starts mic test. |
| [stopMicDeviceTest](https://intl.cloud.tencent.com/document/product/647/35120#stopmicdevicetest) | Stops mic test. |
| [startSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35120#startspeakerdevicetest) | Starts speaker test. |
| [stopSpeakerDeviceTest](https://intl.cloud.tencent.com/document/product/647/35120#stopspeakerdevicetest) | Stops speaker test. |


### MixTranscoding and CDN relayed push APIs

| API | Description |
|-----|-----|
| [setMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35120#setmixtranscodingconfig) | Sets On-Cloud MixTranscoding parameters. |
| [startPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35120#startpublishcdnstream) | Relays stream to the specified push address. |
| [stopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35120#stoppublishcdnstream) | Stops relayed push. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](https://intl.cloud.tencent.com/document/product/647/35120#getsdkversion) | Gets SDK version information. |
| [setLogLevel](https://intl.cloud.tencent.com/document/product/647/35120#setloglevel) | Sets log output level. |
| [setConsoleEnabled](https://intl.cloud.tencent.com/document/product/647/35120#setconsoleenabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://intl.cloud.tencent.com/document/product/647/35120#setlogcompressenabled) | Enables or disables local log compression. |
| [setLogDirPath](https://intl.cloud.tencent.com/document/product/647/35120#setlogdirpath) | Modifies log storage path. |
| [setLogDelegate](https://intl.cloud.tencent.com/document/product/647/35120#setlogdelegate) | Sets log callback. |
| [showDebugView](https://intl.cloud.tencent.com/document/product/647/35120#showdebugview) | Displays dashboard. |
| [setDebugViewMargin](https://intl.cloud.tencent.com/document/product/647/35120#setdebugviewmargin) | Sets dashboard margin. |
| [callExperimentalAPI](https://intl.cloud.tencent.com/document/product/647/35120#callexperimentalapi) | Calls experimental API. |


## TRTCCloudDelegate @ TXLiteAVSDK

Event callback API for TRTC video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](https://intl.cloud.tencent.com/document/product/647/35121#onerror) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://intl.cloud.tencent.com/document/product/647/35121#onwarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://intl.cloud.tencent.com/document/product/647/35121#onenterroom) | Callback of room entry. |
| [onExitRoom](https://intl.cloud.tencent.com/document/product/647/35121#onexitroom) | Callback of room exit. |
| [onSwitchRole](https://intl.cloud.tencent.com/document/product/647/35121#onswitchrole) | Callback of role switching. |
| [onConnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35121#onconnectotherroom) | Callback of the result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](https://intl.cloud.tencent.com/document/product/647/35121#ondisconnectotherroom) | Callback of the result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://intl.cloud.tencent.com/document/product/647/35121#onremoteuserenterroom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://intl.cloud.tencent.com/document/product/647/35121#onremoteuserleaveroom) | A user exits the current room. |
| [onUserVideoAvailable](https://intl.cloud.tencent.com/document/product/647/35121#onuservideoavailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://intl.cloud.tencent.com/document/product/647/35121#onusersubstreamavailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://intl.cloud.tencent.com/document/product/647/35121#onuseraudioavailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://intl.cloud.tencent.com/document/product/647/35121#onfirstvideoframe) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://intl.cloud.tencent.com/document/product/647/35121#onfirstaudioframe) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://intl.cloud.tencent.com/document/product/647/35121#onsendfirstlocalvideoframe) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://intl.cloud.tencent.com/document/product/647/35121#onsendfirstlocalaudioframe) | The first local audio frame data has been sent. |
| [onUserEnter](https://intl.cloud.tencent.com/document/product/647/35121#onuserenter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://intl.cloud.tencent.com/document/product/647/35121#onuserexit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://intl.cloud.tencent.com/document/product/647/35121#onnetworkquality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://intl.cloud.tencent.com/document/product/647/35121#onstatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://intl.cloud.tencent.com/document/product/647/35121#onconnectionlost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://intl.cloud.tencent.com/document/product/647/35121#ontrytoreconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://intl.cloud.tencent.com/document/product/647/35121#onconnectionrecovery) | The connection between SDK and server has been restored. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://intl.cloud.tencent.com/document/product/647/35121#oncameradidready) | Camera is ready. |
| [onMicDidReady](https://intl.cloud.tencent.com/document/product/647/35121#onmicdidready) | Mic is ready. |
| [onAudioRouteChanged](https://intl.cloud.tencent.com/document/product/647/35121#onaudioroutechanged) | Audio routing changes (for iOS only), i.e., whether the audio is output by speaker or receiver. |
| [onUserVoiceVolume](https://intl.cloud.tencent.com/document/product/647/35121#onuservoicevolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDevice](https://intl.cloud.tencent.com/document/product/647/35121#ondevice) | Callback of local device connection and disconnection. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://intl.cloud.tencent.com/document/product/647/35121#onrecvcustomcmdmsguserid) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsgUserId](https://intl.cloud.tencent.com/document/product/647/35121#onmisscustomcmdmsguserid) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://intl.cloud.tencent.com/document/product/647/35121#onrecvseimsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35121#onstartpublishcdnstream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://intl.cloud.tencent.com/document/product/647/35121#onstoppublishcdnstream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35121#onsetmixtranscodingconfig) | Callback of setting On-Cloud MixTranscoding parameters. This callback corresponds to the `setMixTranscodingConfig()` API in [TRTCCloud](https://intl.cloud.tencent.com/document/product/647/35120#trtccloud). |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35121#onaudioeffectfinished) | Callback of ending an audio effect. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureStarted](https://intl.cloud.tencent.com/document/product/647/35121#onscreencapturestarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://intl.cloud.tencent.com/document/product/647/35121#onscreencapturepaused) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://intl.cloud.tencent.com/document/product/647/35121#onscreencaptureresumed) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://intl.cloud.tencent.com/document/product/647/35121#onscreencapturestoped) | This callback will be returned by the SDK when screen sharing is stopped. |

### Custom video rendering callbacks
Redirect to [TRTCVideoRenderDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcvideorenderdelegate)

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://intl.cloud.tencent.com/document/product/647/35121#onrendervideoframe) | Callback of custom video rendering. |


### Custom audio data frame processing callbacks
Redirect to [TRTCAudioFrameDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtcaudioframedelegate)

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://intl.cloud.tencent.com/document/product/647/35121#oncapturedaudioframe) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35121#onplayaudioframe) | Audio data from each remote user before audio mixing (for example, if you want to convert the audio of a channel to text, you need to use the source data instead of the data after audio mixing). |
| [onMixedPlayAudioFrame](https://intl.cloud.tencent.com/document/product/647/35121#onmixedplayaudioframe) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
Redirect to [TRTCLogDelegate](https://intl.cloud.tencent.com/document/product/647/35121#trtclogdelegate)

It is recommended to set the callback delegation object in a class that is initialized early, e.g., `AppDelegate`.

| API | Description |
|-----|-----|
| [onLog](https://intl.cloud.tencent.com/document/product/647/35121#onlog) | Callback of log printing. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://intl.cloud.tencent.com/document/product/647/35121#onaudioeffectfinished) | Callback of ending an audio effect. |

## Definitions of Key Classes

| Class Definition | Description |
|-----|-----|
| [TRTCParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcparams) | Room entry parameters. |
| [TRTCVideoEncParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoencparam) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcnetworkqosparam) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcqualityinfo) | Video quality. |
| [TRTCVolumeInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcvolumeinfo) | Volume level. |
| [TRTCMediaDeviceInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcmediadeviceinfo) | Media device description. |
| [TRTCScreenCaptureSourceInfo](https://intl.cloud.tencent.com/document/product/647/35123#trtcscreencapturesourceinfo) | Screen sharing target information (only for MacOS). |
| [TRTCSpeedTestResult](https://intl.cloud.tencent.com/document/product/647/35123#trtcspeedtestresult) | Network speed test result. |
| [TRTCVideoFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoframe) | Video frame information. |
| [TRTCAudioFrame](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioframe) | Audio frame data. |
| [TRTCMixUser](https://intl.cloud.tencent.com/document/product/647/35123#trtcmixuser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://intl.cloud.tencent.com/document/product/647/35123#trtctranscodingconfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcpublishcdnparam) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudiorecordingparams) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioeffectparam) | Sound effect. |
| [TRTCLocalStatistics](https://intl.cloud.tencent.com/document/product/647/35123#trtclocalstatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](https://intl.cloud.tencent.com/document/product/647/35123#trtcremotestatistics) | Remote audio/video statistics. |
| [TRTCStatistics](https://intl.cloud.tencent.com/document/product/647/35123#trtcstatistics) | Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoresolution) | Video resolution. |
| [TRTCVideoResolutionMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoresolutionmode) | Video aspect ratio mode. |
| [TRTCVideoStreamType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideostreamtype) | Video stream type. |
| [TRTCQuality](https://intl.cloud.tencent.com/document/product/647/35123#trtcquality) | Image quality level. |
| [TRTCVideoFillMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideofillmode) | Video image fill mode. |
| [TRTCVideoRotation](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideorotation) | Video image rotation direction. |
| [TRTCBeautyStyle](https://intl.cloud.tencent.com/document/product/647/35123#trtcbeautystyle) | Beauty filter (skin smoothing) algorithm. |
| [TRTCVideoPixelFormat](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideopixelformat) | Video pixel format. |
| [TRTCVideoBufferType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideobuffertype) | Video data container format. |
| [TRTCLocalVideoMirrorType](https://intl.cloud.tencent.com/document/product/647/35123#trtclocalvideomirrortype) | Mirror type of local video preview. |
| [TRTCAppScene](https://intl.cloud.tencent.com/document/product/647/35123#trtcappscene) | Application scenario. |
| [TRTCRoleType](https://intl.cloud.tencent.com/document/product/647/35123#trtcroletype) | Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcqoscontrolmode) | Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://intl.cloud.tencent.com/document/product/647/35123#trtcvideoqospreference) | Image quality preference. |
| [TRTCAudioSampleRate](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudiosamplerate) | Audio sample rate. |
| [TRTCAudioRoute](https://intl.cloud.tencent.com/document/product/647/35123#trtcaudioroute) | Audio playback mode (audio routing). |
| [TRTCReverbType](https://intl.cloud.tencent.com/document/product/647/35123#trtcreverbtype) | Audio reverb mode. |
| [TRTCVoiceChangerType](https://intl.cloud.tencent.com/document/product/647/35123#trtcvoicechangertype) | Voice changer mode. |
| [TRTCSystemVolumeType](https://intl.cloud.tencent.com/document/product/647/35123#trtcsystemvolumetype) | System volume type. |
| [TRTCLogLevel](https://intl.cloud.tencent.com/document/product/647/35123#trtcloglevel) | Log level. |
| [TRTCGSensorMode](https://intl.cloud.tencent.com/document/product/647/35123#trtcgsensormode) | Switch of the g-sensor. |
| [TRTCMediaDeviceType](https://intl.cloud.tencent.com/document/product/647/35123#trtcmediadevicetype) | Device type (only for macOS). |
| [TRTCScreenCaptureSourceType](https://intl.cloud.tencent.com/document/product/647/35123#trtcscreencapturesourcetype) | Screen sharing target type (only for macOS). |
| [TRTCTranscodingConfigMode](https://intl.cloud.tencent.com/document/product/647/35123#trtctranscodingconfigmode) | MixTranscoding parameter configuration mode. |


