## ITRTCCloud @ TXLiteAVSDK

### Creating and terminating an ITRTCCloud singleton

| API | Description |
|-----|-----|
| [getTRTCShareInstance](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ga2fc755520711d5d8fd469f93bc9c2dc6) | Gets [ITRTCCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#classTRTC_1_1ITRTCCloud) object pointer in dynamic DLL loading. |
| [destroyTRTCShareInstance](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ga1b494c61ef1fe41531ce283aae4e015d) | Releases [ITRTCCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#classTRTC_1_1ITRTCCloud) singleton object. |


### Setting TRTCCloudCallback callback

| API | Description |
|-----|-----|
| [addCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | Sets callback API [ITRTCCloudCallback](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#classTRTC_1_1ITRTCCloudCallback). |
| [removeCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | Removes event callback. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) | Enters room. If the room does not exist, the system will automatically create a new room. |
| [exitRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | Exits room. |
| [switchRole](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | Switches role. This API applies only to the LVB scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [connectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae472af11c30db29fcd21ea01854ab32f) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | Disables cross-room co-anchoring. |
| [setDefaultStreamRecvMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### CDN API functions

| API | Description |
|-----|-----|
| [startPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac2f616263c108bf6ac5ef2b66b83a380) | Starts pushing to Tencent Cloud LVB CDN. |
| [stopPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Stops pushing to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | Starts relaying to the live streaming CDN of another cloud. |
| [stopPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Stops relaying to non-Tencent Cloud address. |
| [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | Sets On-Cloud MixTranscoding parameters. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0a3067221345da8eb3f32a3430dd42ff) | Enables the preview image of local video. |
| [stopLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | Stops local video capture and preview. |
| [muteLocalVideo](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6070313a28d3302c94ad807c636eb60f) | Pauses/Resumes pushing local video data. |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a33a6e3765d6ca52d572224bc6e25dbcb) | Starts displaying remote video image. |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7749979db2dd017d7cd8377c73e92720) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [stopAllRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | Stops displaying all remote video images and pulling the video data streams of all remote users. |
| [muteRemoteVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a22155f6fe17dde77a16c273e0d5a02a3) | Pauses/Resumes receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa2bc2739031035b40e8f2a76184c20d9) | Sets video encoder parameters. |
| [setNetworkQosParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a374f1000d443de80d70747cba876f879) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af05757058905160ae641266caafc9516) | Sets the rendering mode of local image. |
| [setRemoteViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0d665a28bb540815de7a2028854db260) | Sets the rendering mode of remote image. |
| [setLocalViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47859830694b7f71d447939d2c938455) | Sets the clockwise rotation angle of local image. |
| [setRemoteViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a571cbfb2eaef9f92b09f9e60b22cfd2b) | Sets the clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | Sets the direction of image output by video encoder (i.e., video image viewed by remote user and recorded by server).
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4ec409aae9d635222458316fca1e8a4d) | Sets the mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | Sets the mirror mode of image output by encoder. |
| [enableSmallVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a80648f76afbda35c9bf5d96701c62a9e) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abd330074a9e99cb9c75d42ef3d1d63a0) | Specifies whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a24642910f76b7fdf78b435d736a0d7ba) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [setAudioQuality](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aacf5923d535306c139d1b8b8025744c8) | Sets sound quality. The higher the sound quality of the anchor, the better the sound effect to viewers, but the higher the required bandwidth, so there may be lags if the bandwidth is limited. |
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a72ba04e850009e56505ee1cae0433abe) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | Mutes/Unmutes local audio. |
| [muteRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | Mutes/Unmutes specified remote user's audio. |
| [muteAllRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | Mutes/Unmutes all users' audio. |
| [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | Sets SDK capture volume level. |
| [getAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | Gets SDK capture volume level. |
| [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | Sets SDK playback volume level. |
| [getAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | Gets SDK playback volume level. |
| [enableAudioVolumeEvaluation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | Enables or disables volume reminder. |
| [startAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a15b74c793aea807ef9142230c088473b) | Starts audio recording. |
| [stopAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | Stops recording|


### Camera API functions

| API | Description |
|-----|-----|
| [getCameraDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa129bdc4cfd2d81ff7d57a2aab20da52) | Gets camera list. |
| [setCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af9e6848cc5f6b20268c2cf6eef034326) | Sets the camera to be used. |
| [getCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a25042fd580b846102e06ff92a74b8417) | Gets the currently used camera. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a84a4d58010c498d2bc44d8ff225e7a90) | Gets mic list. |
| [getCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a31669c8a64f8003b93e8fc7359e5ed11) | Gets the currently used camera. |
| [setCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4edae1445c3195d5d2ba2333ccbe4fff) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a342920bf68b0286b91a049f540de5ccb) | Gets current system mic volume level. |
| [setCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a227e6698697648b7a7ee9470a87f12f1) | Sets current system mic volume level. |
| [getSpeakerDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad500c64d8823bed4c4a31ab6b19c1e08) | Gets speaker list. |
| [getCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad0dc1a89532d3654b271ed724b4281fd) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab11c3c87d603a71dc1d3f2caef05bf98) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a24c9e3210c99e6331a3dff598f7fb490) | Gets current system speaker volume level. |
| [setCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad8393f22304422cb143a1362c03cca59) | Sets current system speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [setBeautyStyle](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5aeffc60ba8101363f267f40dd8425d8) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | Sets watermark. |


### Music effects and voice effects

| API | Description |
|-----|-----|
| [getAudioEffectManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | Gets the sound effect management class `ITXAudioEffectManager`. |
| [startSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6a651a786871927917b087ae7094c8a) | Enables system audio capture. |
| [stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | Disables system audio capture. |
| [setSystemAudioLoopbackVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | Sets system audio capture volume level. |


### Screen sharing API functions

| API | Description |
|-----|-----|
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3cc7f7152c18f6ffda7cfa2b0b133934) | Starts screen sharing. |
| [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | Stops screen capture. |
| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | Pauses screen sharing. |
| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | Resumes screen sharing. |
| [getScreenCaptureSources](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3777e1506f1aa806bee116e7117993b5) | Enumerates shareable windows. You are recommended to call this API before calling `startScreenCapture`. |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa5c3c7ed12993c155de77fb43ba0cf3b) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af82052cffdcd1fd2a8d50744b806ff7d) | Starts displaying the secondary channel image of remote user (`TRTCVideoStreamTypeSub`, which is usually used for screen sharing). |
| [stopRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4264ad8ab90a2582dc94617a3c686a46) | Stops displaying the secondary channel image of remote user (`TRTCVideoStreamTypeSub`, which is usually used for screen sharing). |
| [setRemoteSubStreamViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0059bffb1af2385304595917e85d1cf3) | Sets the display mode of secondary channel image (`TRTCVideoStreamTypeSub`, which is generally used for screen sharing). |
| [setRemoteSubStreamViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a11a2965ee1192569afd1482cfce6816e) | Sets the clockwise rotation angle of secondary channel image (`TRTCVideoStreamTypeSub`, which is generally used for screen sharing). |
| [setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abdc3d6339afd741bd8d3ed88ea551282) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | Sets the audio mixing volume level of screen sharing. |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac9d547341170330a70623299b366c44a) | Enables custom video capture mode. |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3a53ae79c1bd28825cb276c7555500fe) | Delivers captured video data to SDK. |
| [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | Enables the custom audio capture mode. After this mode is enabled, the SDK will not run the original audio capture process and retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) to continuously insert the captured audio data into the SDK. |
| [sendCustomAudioData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | Delivers captured audio data to SDK. |
| [setLocalVideoRenderCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | Sets custom rendering for remote video. |
| [setAudioFrameCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | Sends custom message to all users in room. |
| [sendSEIMsg](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | Embeds custom data of a small size in video frames. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af86b2903b95b6e74f02d701701ce3380) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | Stops network speed test. |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a27478c88ea2f0c3ad4d1747995bf4bad) | Starts camera test. |
| [stopCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9aa02ead51d4ba3119869c7c2ac57b9d) | Stops camera test. |
| [startMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae9982f55fa0e47646f43da2515584183) | Enables mic test. |
| [stopMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a60b8449c0b9c9ce8068e3e9960ea2237) | Stops mic test. |
| [startSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a93ff8bfeb6ddcc0432c90fb6ac54be94) | Enables speaker test. |
| [stopSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa2a27282ca4aaf6ccc347ec1fa14da1c) | Stops speaker test. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | Gets SDK version information. |
| [setLogLevel](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Sets log output level. |
| [setConsoleEnabled](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | Disables or enables console log printing. |
| [setLogCompressEnabled](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | Enables or disables local log compression. |
| [setLogDirPath](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | Sets log storage path. |
| [setLogCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | Sets log callback. |
| [showDebugView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | Displays dashboard. |
| [callExperimentalAPI](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab15fc0877664a8ac257ca4d6e7afc7b0) | Calls experimental API. |


### Disused API functions

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa8c0c6aceb1c0fe5de3a2083bc5a5b18) | Sets mic volume level. |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3cc7f7152c18f6ffda7cfa2b0b1339342) | Starts screen sharing. |
| [playBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9b15087f0a9c29d4442221ca36b7e916) | Starts background music. |
| [stopBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a11004f1ba27b057985850a25307b0bec) | Stops background music. |
| [pauseBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4b92d4c989e99612f6c4dab03a78764) | Pauses background music. |
| [resumeBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed6e8f224b5f834b1bc0c15f9701f692) | Resumes background music. |
| [getBGMDuration](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae89800361133fc7a04524b426a1c1cff) | Gets the total length of music file in milliseconds. |
| [setBGMPosition](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c656ebde9875a6bf8d4c30d4629161) | Sets the playback progress of background music. |
| [setBGMVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a7d8cca48ca7c864e0bec6d869ea387) | Sets the playback volume level of background music. |
| [setBGMPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0a4ab1fa2df3f0f1b7284ad9b2fbb921) | Sets the local playback volume level of background music. |
| [setBGMPublishVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2eb3a1958ea834729f1b6e844cc0ea9d) | Sets the remote playback volume level of background music. |
| [playAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a11827d3d124889d8b359644692e289) | Plays back sound effect. |
| [setAudioEffectVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a942a6f358980c8520e2155fb4ef55bd0) | Sets sound effect volume level. |
| [stopAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a61561195216ac575235b67d410070563) | Stops sound effect. |
| [stopAllAudioEffects](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7066509af1de32c290b7cc297cd00f2b) | Stops all sound effects. |
| [setAllAudioEffectsVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a19416181cce88c58052a4eb2e87adeb8) | Sets the volume level of all sound effects. |
| [pauseAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a43f83a1323cc39c1610c61cf79ab652c) | Pauses sound effect. |
| [resumeAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a23b65446d7dd9835da888b5285867629) | Resumes sound effect. |




## TRTCCloudCallback @ TXLiteAVSDK

Callback API class for TRTC video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a9724da0b3da9b2eca5736fa8e54aa410) | Callback for error, which indicates that the SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a53169ea41d90506cccbff507ba1932a4) | Callback for warning. This callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a236a49e0525615b6435eaa826b7caffe) | Callback of room entry. |
| [onExitRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) | Callback of room exit. |
| [onSwitchRole](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a248335805c125e225cfec249697f2299) | Callback of role switching. |
| [onConnectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a62333366a3a1ab09dc2b2f627a8a1bdd) | Callback of result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a292d6661cb93ba30ff68b1f88cf173f1) | Callback of result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a43704996ae1f50749b7c7140755350f1) | A user enters the current room. |
| [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a5f7c705f3894d3a430ef1fac8bf8e2c5) | A user exits the current room. |
| [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) | Whether the remote user has playable primary image (generally used for camera). |
| [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a460922e4fb4b000d1dbd27b596dd0e5c) | Whether the remote user has playable secondary image (generally used for screen sharing). |
| [onUserAudioAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a6f449dc5294e369750bc15a39eaa856c) | Whether the remote user has playable audio data. |
| [onFirstVideoFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ad28d27badd56ac274c44720cc9f253d5) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a123616289b3219bc36137bc77e8e8b7a) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a454ea7e7103b2838440cafba3e524433) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a0bd950cb774fd40cfdc2fbff885295d2) | The first local audio frame data has been sent. |
| [onUserEnter](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ad606b861a3545832fb4821a7e0230925) | Disused API: an anchor enters the current room. |
| [onUserExit](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#abbc4fe2ccac90f77c80f55d46d6c8951) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a377441bace65d98a1218817914a12ecb) | Network quality. This callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a681d301a576e65b354408576748c4477) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a34c34705bb67127ff6d28700cf2ab591) | The connection between SDK and server has been closed. |
| [onTryToReconnect](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#afe74dff22fde93fe0f07fcf18153d334) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ae90cd149a676418016cb8736b217f1a8) | The connection between SDK and server has been restored. |
| [onSpeedTest](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a455264cfcf2a7a3f022f3bce0659f9f7) | Callback of server speed test. The SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a13a9ad0933b7ab872987e432f005e8ad) | Camera is ready. |
| [onMicDidReady](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a0ba02a5d9009ebb9c4e80c0c43c80bca) | Mic is ready. |
| [onUserVoiceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a61df1f9eec0bfcebf421be865275ffc5) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ac86c1b0d445a33f6340394b3b78490bd) | Callback of local device connection and disconnection. |
| [onTestMicVolume](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a9f0101fa8222c6163f1b23fcce81e22b) | Callback of test mic volume level. |
| [onTestSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a04bb10b06af17cdc43b7831336736539) | Callback of test speaker volume level. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a0a5690652db3902e98e1168bad12ec1a) | Callback of receipt of custom message. |
| [onMissCustomCmdMsg](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ab5d0cb61c24b77ecdb177ff19fc95075) | Callback of loss of custom message. |
| [onRecvSEIMsg](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ab364b929cd0d9ffff6e47c20ec52372c) | Callback of receipt of SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a345ab7b45a9d0027926dbf580e8e0258) | Callback of starting pushing to Tencent Cloud LVB CDN, which corresponds to the `startPublishing()` API in `TRTCCloud`. |
| [onStopPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a8e046f5bd34498b13ae057caaab64913) | Callback of stopping pushing to Tencent Cloud LVB CDN, which corresponds to the `stopPublishing()` API in `TRTCCloud`. |
| [onStartPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a16164548764979e84d3b5301f28890ff) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a0da75e040521c0945c3735f4893e6c09) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#af228d4fa55fa17a48eb7424fb6ffe2b4) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#aab3c91276b6e570ea9acfe1581e1aa51) | Callback of audio effect playback end. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a490f827ffd6e7728a6ec49cba63875b1) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a8baff9a6c699ea1d82c5e7abb6ded97b) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a32acecdafd9058cc7d70a3abe6995051) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a63c073daf1ad93cfa2e6c79695434e22) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a4d182e6b60d8be536e69253d906af84d) | This callback will be returned by the SDK when screen sharing is stopped. |


### Background audio mixing event callbacks

| API | Description |
|-----|-----|
| [onPlayBGMBegin](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ad93b8204416558e63c18349bf29ff592) | Playback of background music starts. |
| [onPlayBGMProgress](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a1879cc4e50492431a3346828e9130f21) | Progress of background music playback. |
| [onPlayBGMComplete](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#abaf89c758a4dd21e21db488e997bef2a) | Playback of background music ends. |


### Custom video rendering callbacks

| API | Description |
|-----|-----|
| [onRenderVideoFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#aea602851c96370558a7eeb850d7eb6b8) | Callback of custom video rendering. |


### Audio data callbacks

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a57460e97c668b605a00ac498fc4aa40c) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#ab841da62beb88a9fa9bce58d25df6f23) | Audio data from each remote user before audio mixing, i.e., raw data of each channel before audio mixing. For example, when converting a certain channel of audio to text, you must use the raw audio data of the channel. |
| [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a6649f62d4138d9bc73ae484e63dec081) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks

| API | Description |
|-----|-----|
| [onLog](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a2fa3d9997c9810ffa6a95e0a7a4a50d0) | Callback of log printing. |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | Room entry parameters. |
| [TRTCVideoEncParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a43a83bd5122296aa87cc7f6e964921c5) | Video encoding parameters. |
| [TRTCNetworkQosParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a7cd5c078b248a32557a85226f1d30697) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#af6aab62536869726ee32b158ddbbf5ce) | Video quality. |
| [TRTCVolumeInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#abdeba26e639757957fd75f528ba14f6e) | Volume level. |
| [TRTCSpeedTestResult](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a8858167e09ab4d55f5e49c89bd4a1848) | Network speed test result. |
| [TRTCMixUser](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ac5b1947f21f77726cbff822eaf0003f9) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a6066a5537ad8c1bc6158d43e8a4765db) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a0b977361cb4d84b1ece0b26c949dcde6) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a724e3aa5cbc2249b7ce31bd7f9362d7b) | Audio recording parameters. |
| [TRTCAudioEffectParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#a87aff2ab3ece9f1130a73981838baf04) | Sound effect. |
| [TRTCLocalStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#structTRTC_1_1TRTCLocalStatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#structTRTC_1_1TRTCRemoteStatistics) | Remote audio/video statistics. |
| [TRTCStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#structTRTC_1_1TRTCStatistics) | Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gace04ad7a0bf531f4d09dc6a540f09f95) | Video resolution. |
| [TRTCVideoResolutionMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gaa6787a9059d7b725a30ffcf9f4aabb64) | Video resolution mode. |
| [TRTCVideoStreamType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga461563be214e8f0579a79741f37d18e3) | Video stream type. |
| [TRTCQuality](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gaa33845a1c994d38435a8f4a332cc3e95) | Image quality level. |
| [TRTCVideoFillMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga496a32286104187149b4e40284cbfb36) | Video image fill mode. |
| [TRTCBeautyStyle](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga46f49720df57d17b267054cb9ee4d079) | Beauty filter (skin smoothing) algorithm. |
| [TRTCAppScene](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gaa57f4545ef7331e3157eee1639d28780) | Application scenario. |
| [TRTCRoleType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga42ff820a33d9f3535d203fd5d6782cb5) | Role, which applies only to the live streaming scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [TRTCQosControlMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga6615b296e31fc3d03c0df92e9755b5aa) | Bandwidth limit mode. |
| [TRTCVideoQosPreference](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga60efcaeea7692bbce8dc362856683319) | Image quality preference. |
| [TRTCAudioSampleRate](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gab0f34072e93189a864688cb0375d462c) | Audio sample rate. |
| [TRTCAudioQuality](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga96f3d4cdcf3baa9df39ab4e1b3f0eb40) | Sound quality. |
| [TRTCLogLevel](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gafa83683b4840bcb3200d1da63c10276d) | Log level. |
| [TRTCDeviceState](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gac93bb27d49c2aeea8fc04242c5d0fc7e) | Device operation. |
| [TRTCDeviceType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#ga76eabab111ddd8a7b2e44d2cbcf45794) | Device type. |
| [TRTCWaterMarkSrcType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gab3426c24d07508781330231a35be0ae0) | Watermark image source type. |
| [TRTCTranscodingConfigMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__cplusplus.html#gaec50c849a17b7706f6989d718fc6b7df) | MixTranscoding parameter configuration mode. |


