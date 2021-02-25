## ITRTCCloud @ TXLiteAVSDK
### Setting ITRTCCloudCallback callbacks

| API | Description |
|-----|-----|
| [addCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | Sets callback API. |
| [removeCallback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | Removes event callback. |


### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) | Enters room. If the room does not exist, the system will automatically create a new room. |
| [exitRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | Exits room. |
| [switchRole](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | Switches role. This API applies only to the LVB scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [connectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae472af11c30db29fcd21ea01854ab32f) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | Disables cross-room co-anchoring. |
| [setDefaultStreamRecvMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |
| [createSubCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | Creates `TRTCCloud` subinstance. |
| [destroySubCloud](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0555e9e9d9d02c8c116946915f969d18) | Terminates TRTCCloud subinstance. |
| [switchRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | Switches room. |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac2f616263c108bf6ac5ef2b66b83a380) | Starts pushing to Tencent Cloud LVB CDN. |
| [stopPublishing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Stops pushing to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | Starts relaying to the live streaming CDN of another cloud. |
| [stopPublishCDNStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Stops relaying to non-Tencent Cloud address. |
| [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | Sets On-cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a64a9d40eba291e0447b63542a6a66f3c) | Enables the preview image of local video. |
| [startLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df) | Enables the preview image of local video (for iOS and Android). If this function is called before `enterRoom`, the SDK will only enable the camera and wait until `enterRoom` is called before starting push. If it is called after `enterRoom`, the SDK will enable the camera and automatically start pushing the video stream. When the first camera frame is rendered, you will receive the `onFirstVideoFrame(null)` callback in ITRTCCloudCallback. |
| [updateLocalView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6db572d1e387b21328c6c78de561838c) | Updates the preview window of local video. |
| [stopLocalPreview](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | Stops local video capturing and preview. |
| [muteLocalVideo](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a6070313a28d3302c94ad807c636eb60f) | Pauses/Resumes pushing local video data. |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a50ec31c281de91903a1ef492a2ec7997) | Starts displaying remote video image. |
| [updateRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9f774f9abb7970fb32c3172fa3229fd2) | Updates the rendering window of remote video. |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [stopAllRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | Stops displaying all remote video images and pulling the video data streams of all remote users. |
| [muteRemoteVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a22155f6fe17dde77a16c273e0d5a02a3) | Pauses/Resumes receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa2bc2739031035b40e8f2a76184c20d9) | Sets video encoder parameters. |
| [setNetworkQosParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a374f1000d443de80d70747cba876f879) | Sets network bandwidth limit parameters. |
| [setLocalRenderParams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | Sets the rendering parameter of local image (primary stream). |
| [setVideoEncoderRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | Sets the direction of image output by video encoder (i.e., video image viewed by remote user and recorded by server).
| [setVideoEncoderMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | Sets the mirror mode of image output by encoder. |
| [setRemoteRenderParams](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | Sets the rendering mode of remote image. |
| [enableSmallVideoStream](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a80648f76afbda35c9bf5d96701c62a9e) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abd330074a9e99cb9c75d42ef3d1d63a0) | Specifies whether to view the big or small image of the specified `userId`. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a86c80ed357798e50ccf5c7ae47317f4c) | Enables local audio capturing and upstreaming. |
| [stopLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | Disables local audio capturing and upstreaming. |
| [muteLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | Mutes/Unmutes local audio. |
| [muteRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | Mutes/Unmutes specified remote user's audio. |
| [muteAllRemoteAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | Mutes/Unmutes all users' audio. |
| [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | Sets the SDK capturing volume level. |
| [getAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | Gets the SDK capturing volume level. |
| [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | Sets SDK playback volume level. |
| [getAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | Gets SDK playback volume level. |
| [enableAudioVolumeEvaluation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | Enables or disables volume reminder. |
| [startAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a15b74c793aea807ef9142230c088473b) | Starts audio recording. |
| [stopAudioRecording](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | Stops recording|


### Device APIs

| API | Description |
|-----|-----|
| [getDeviceManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | Gets device management module. |


### Beauty filter and watermark APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | Sets the effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | Sets watermark. |


### Music and voice effect APIs

| API | Description |
|-----|-----|
| [getAudioEffectManager](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | Gets the sound effect management class `ITXAudioEffectManager`. |
| [startSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad6a651a786871927917b087ae7094c8a) | Enables system audio capturing. |
| [stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | Disables system audio capturing. |
| [setSystemAudioLoopbackVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | Sets the system audio capturing volume level. |


### Screen sharing APIs

| API | Description |
|-----|-----|
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab0f8b23d8c48b9a056ca0e61ddcc894f) | Starts screen sharing. |
| [stopScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | Stops screen capturing. |
| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | Pauses screen sharing. |
| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | Resumes screen sharing. |
| [getScreenCaptureSources](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3777e1506f1aa806bee116e7117993b5) | Enumerates shareable windows. You are recommended to call this API before calling `startScreenCapture`. |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abdc3d6339afd741bd8d3ed88ea551282) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | Sets the audio mixing volume level of screen sharing. |
| [addExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0edaac7111c63d9a00b7749ee0c7b137) | Adds specified windows to the exclusion list of screen sharing. After being added, the windows will not be shared. |
| [removeExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a39db493034f2898788898e6669168c61) | Removes specified windows from the exclusion list of screen sharing. |
| [removeAllExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | Removes all windows from the exclusion list of screen sharing. |


### Custom capturing and rendering APIs

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac9d547341170330a70623299b366c44a) | Enables custom video capturing mode. |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3a53ae79c1bd28825cb276c7555500fe) | Delivers captured video data to SDK. |
| [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | Enables custom audio capturing mode. After this mode is enabled, the SDK will not run the original audio capturing process and will retain only the encoding and sending capabilities. You need to use [sendCustomAudioData()](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) to continuously insert the captured audio data into the SDK. |
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


### Log APIs

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


### Disused APIs

| API | Description |
|-----|-----|
| [startLocalAudio](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | Enables local audio capturing and upstreaming. |
| [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a50ec31c281de91903a1ef492a2ec7997) | Starts displaying remote video image. |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [setLocalViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#acdfe0dc822f074d5c42dfe308dc313a0) | Sets the fill mode of local image. |
| [setLocalViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4447783c52960cffbaedb7ccd7c456a2) | Sets the clockwise rotation angle of local image. |
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5a04c60eb2e9997e745412374b7b8d19) | Sets the mirror mode of local camera's preview image. |
| [setRemoteViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab5be71379d671f77b99cf6ccd86cdbc7) | Sets the rendering mode of remote image. |
| [setRemoteViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a385042d69e79468c9ef60dee8ec8cc96) | Sets the clockwise rotation angle of remote image. |
| [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5935a852496c1a033576cc6fbf676746) | Starts displaying the substream image of remote user (`TRTCVideoStreamTypeSub`, which is usually used for screen sharing). |
| [stopRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a56a7770d90cad9141aecbd70d93af588) | Stops displaying the substream image of remote user (`TRTCVideoStreamTypeSub`, which is usually used for screen sharing). This API was disused in v8.0. Please use the `stopRemoteView(userId,streamType)` API. |
| [setRemoteSubStreamViewFillMode](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7832e5870431ccb0e75614b51af51205) | Sets the display mode of substream image (`TRTCVideoStreamTypeSub`, which is generally used for screen sharing). |
| [setRemoteSubStreamViewRotation](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab63344839afca9bd4a890f6f609fd9e7) | Sets the clockwise rotation angle of substream image (`TRTCVideoStreamTypeSub`, which is generally used for screen sharing). |
| [setAudioQuality](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a742eefe8508e744918f704e2fa0d3405) | Sets audio quality. |
| [setPriorRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a074579fcbcd5f4639ab40a2d5884fa3f) | Sets the video quality preferred by viewers. |
| [getCameraDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ace7e563213b43c1763b1eb60d5b2e8c5) | Gets camera list. |
| [setCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af5ce3a160a7f0dc889322983f5cfa68a) | Sets the camera to be used. |
| [getCurrentCameraDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0f4a19bdc82b81dd1e0a8ac8b735261a) | Gets the currently used camera. |
| [getMicDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab85ff9472d499bd740f953ccff549147) | Gets mic list. |
| [getCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a5a17cc110f2b9c146df4498aa35eebc6) | Gets the currently used mic. |
| [setCurrentMicDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aded68bf47cb1e381961b0b69dde8931b) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#addb5ea84bf67a3fdd49eee30e66f4826) | Gets current system mic volume level. |
| [setCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aaa35154699a59962bc065519e79761fa) | Sets current system mic volume level. |
| [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a44453f04c53f19f65ca362a1cb55963b) | Sets whether to mute the current system mic. |
| [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac7df6f29e11ded5faf7996334d4af61b) | Gets the mute status of the current system mic. |
| [getSpeakerDevicesList](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a20fa0073543ed1bd1df5dbb825b408bf) | Gets speaker list. |
| [getCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a0ac0ecdbf0d077563fd6d2fb1ee65bee) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a768367aba35b104f8529740b86802b73) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#accb2d6bc752f550b968462ba5a5c0538) | Gets current system speaker volume level. |
| [setCurrentSpeakerVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae99882060b048467a0f39f13b168775f) | Sets current system speaker volume level. |
| [setCurrentSpeakerDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ad8c3800ba3e2101ff63de7117dc729f3) | Sets whether to mute the current system speaker. |
| [getCurrentSpeakerDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4ec49fc0c07c04031d328db5814793f) | Gets the mute status of the current system speaker. |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | Starts camera test. |
| [startCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | Starts camera test. |
| [stopCameraDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a3cb3fd62d04b5975c9c50210e98f0a2d) | Stops camera test. This API was disused in v8.0. Please use the `ITXDeviceManager::stopCameraDeviceTest` API. |
| [startMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aca6add13bdd6535bed6d28407b5468af) | Starts mic test. |
| [stopMicDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a29c2a5a42f65108074174e0bc58c0aee) | Stops mic test. This API was disused in v8.0. Please use the `ITXDeviceManager::stopMicDeviceTest` API. |
| [startSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af60f0db87d1f7001860f1bf330eeee3c) | Starts speaker test. |
| [stopSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aa4b7a172067664fe50015c758e02a822) | Stops speaker test. This API was disused in v8.0. Please use the `ITXDeviceManager::stopSpeakerDeviceTest` API. |
| [setMicVolumeOnMixing](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4e3fb7ca730f15b6ab201e73e21f1260) | Sets mic volume level. |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a984f461eebe77819f40c4129fc5a71bb) | Starts screen sharing. |
| [playBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a815aa5a969dcb0617e02f955a9ee7cd4) | Starts background music. |
| [stopBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8eec0a8a7edf45d3b49b897286154b4f) | Stops background music. |
| [pauseBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aed6272ead63eb14b9f64a92a59196c28) | Pauses background music. |
| [resumeBGM](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a221c73557814b71880c9a9323e3f31d2) | Resumes background music. |
| [getBGMDuration](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a487cff035a50da09ab39e87f7488d647) | Gets the total length of music file in milliseconds. |
| [setBGMPosition](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2e2050b96d2b453e0ca83e483efec02c) | Sets the playback progress of background music. |
| [setBGMVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ab651d0daff2d1b7e25b43606a4776796) | Sets the playback volume level of background music. |
| [setBGMPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a9c083e91e2af46503e522443a7b51b32) | Sets the local playback volume level of background music. |
| [setBGMPublishVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af193ff23e008485cf949d761028ce6e9) | Sets the remote playback volume level of background music. |
| [playAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a4db6f176c155c0f83d11eb302f6e1dab) | Plays back sound effect. |
| [setAudioEffectVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a401d82c610be2136896c0f60621d66cf) | Sets sound effect volume level. |
| [stopAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a254acc2f0fe96ffcce33629eb4309877) | Stops sound effect. |
| [stopAllAudioEffects](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a07a2dfd7ce4e76b28172d73ee8405dbe) | Stops all sound effects. |
| [setAllAudioEffectsVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a06219d65076c6c7024fab30d2516b167) | Sets the volume level of all sound effects. |
| [pauseAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a2b004f3a3a7bdde7b2926930f31afa6c) | Pauses sound effect. |
| [resumeAudioEffect](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#af10583316f15ed709247590a081b2307) | Resumes sound effect. |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a) | Sets screen sharing parameters. |
