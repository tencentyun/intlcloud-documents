## Introduction
Since version 8.0, TRTC has provided new APIs for C++ in addition to the original ones. They can be used on Windows, iOS, macOS, and Android.
See the following documents for how to integrate the C++ APIs.  
- [iOS](https://intl.cloud.tencent.com/document/product/647/35092)  
- [Android](https://intl.cloud.tencent.com/document/product/647/35093)  
- [macOS](https://intl.cloud.tencent.com/document/product/647/35094)  
- [Windows](https://intl.cloud.tencent.com/document/product/647/35095)  

>?
>- The C++ APIs are currently available in TRTC Lite only.  
>- On Windows, the TRTC header file automatically adopts the "trtc" namespace. You do not need to specify the namespace.

## ITRTCCloud @ TXLiteAVSDK
### Setting the `ITRTCCloudCallback` callback

| API | Description |
|-----|-----|
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | Sets the callback API [`ITRTCCloudCallback`](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#classtrtc_1_1ITRTCCloudCallback). |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | Removes the callback. |



### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | Switches roles. This API works only in live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae472af11c30db29fcd21ea01854ab32f) | Requests a cross-room call (anchor competition). |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | Ends cross-room co-anchoring. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | Sets the audio/video data receiving mode, which must be set before room entry for it to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | Creates a `TRTCCloud` sub-instance. |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0555e9e9d9d02c8c116946915f969d18) | Terminates a `TRTCCloud` sub-instance. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | Switches rooms. |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac2f616263c108bf6ac5ef2b66b83a380) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Stops relaying to non-Tencent Cloud addresses. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df) | Enables preview of the local video (for Windows and macOS). |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aaf4651f9913924560859f4541211f2df2) | Enables preview of the local video. If you call this function before `enterRoom`, the SDK will enable the camera but will wait till you call `enterRoom` to start pushing streams. If you call this function after `enterRoom`, the SDK will enable the camera and automatically start pushing video streams. You will receive the `onFirstVideoFrame(null)` callback in [`ITRTCCloudCallback`](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#classtrtc_1_1ITRTCCloudCallback) when the rendering of the first video frame starts. |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6db572d1e387b21328c6c78de561838c) | Updates preview of the local video.
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | Stops local video capturing and preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6070313a28d3302c94ad807c636eb60f) | Pauses/Resumes pushing local video data. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a25f09552efac99d88a7aad53960146d7) | Starts pulling and displaying the image of a specified remote user. |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9f774f9abb7970fb32c3172fa3229fd2) | Updates the image of a remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | Stops displaying the video images of all users and pulling their video streams. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a22155f6fe17dde77a16c273e0d5a02a3) | Pauses/Resumes receiving a specified remote video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aa2bc2739031035b40e8f2a76184c20d9) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a374f1000d443de80d70747cba876f879) | Sets QoS control parameters. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | Sets rendering parameters for the local image (primary stream). |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | Sets the rotation degree of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | Sets the mirror mode of encoded images. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | Sets the rendering mode of a remote image. |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a80648f76afbda35c9bf5d96701c62a9e) | Enables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#abd330074a9e99cb9c75d42ef3d1d63a0) | Specifies whether to view the big or small image of a specified `userId`. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | Takes a video screenshot. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | Enables local audio capturing and upstream data transfer. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | Disables local audio capturing and upstream data transfer. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | Mutes/Unmutes local audio. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | Mutes/Unmutes a specified remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | Mutes/Unmutes all users. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | Sets the SDK capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | Gets the SDK capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | Gets the SDK playback volume. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | Enables/Disables volume reminders. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a15b74c793aea807ef9142230c088473b) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | Stops audio recording. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | Starts local recording. |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | Stops local recording. |


### Device API

| API | Description |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | Gets the device management module. |


### Beauty filter and watermark APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | Sets the strength of the beauty, brightening and rosy skin filters. |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | Sets watermarks. |


### Music and voice effect API

| API | Description |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | Gets the audio effect management class `ITXAudioEffectManager`. |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ad6a651a786871927917b087ae7094c8a) | Enables system audio capturing. |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | Disables system audio capturing. |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | Sets system audio capturing volume. |


### Screen sharing APIs

| API | Description |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a984f461eebe77819f40c4129fc5a71bb) | Starts screen sharing. |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | Resumes screen sharing. |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3777e1506f1aa806bee116e7117993b5) | Enumerates shareable windows. We recommend that you call this API before calling `startScreenCapture`. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#abdc3d6339afd741bd8d3ed88ea551282) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | Sets audio mixing volume for screen sharing. |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0edaac7111c63d9a00b7749ee0c7b137) | Adds a specified window to the exclusion list of screen sharing. Windows in the list will not be shared. |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a39db493034f2898788898e6669168c61) | Removes a specified window from the exclusion list of screen sharing. |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | Removes all windows from the exclusion list of screen sharing. |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a76c684e860bca4e48f06269261d73fc0) | Adds a specified window to the screen sharing list. Windows in the list will be shared if they are in the capturing area. |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae9e324dac071b6d2bbc7b6e2a676ea05) | Removes a specified window from the screen sharing list. |
| [removeAllIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | Removes all windows from the screen sharing list. |


### Custom capturing and rendering APIs

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3278ac2b7b2e093ef22332cff3e6d97f) | Enables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629) | Sends captured video data to the SDK. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | Enables custom audio capturing. After this mode is enabled, the SDK will stop the original audio capturing process while continuing to encode and send data. You need to keep feeding your audio data to the SDK using [`sendCustomAudioData()`](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d). |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | Sends captured audio data to the SDK. |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | Specifies whether external audio is mixed into the pushed and played streams. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f) | Sends custom substream audio data to the SDK. |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | Sets custom rendering for a remote video. |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | Sets the audio data callback. |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | Gets PTS for custom capturing. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | Sends a custom message to all users in the room. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | Embeds small-volume custom data in video frames. |


### Device and network testing APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#af86b2903b95b6e74f02d701701ce3380) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a call. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | Stops network speed testing. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | Sets the path to save logs. |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | Displays the dashboard. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab15fc0877664a8ac257ca4d6e7afc7b0) | Calls the experimental API. |


### Disused APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a05765322423454da0ad304faa7efba4a) | Enables local audio capturing and upstream data transfer. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a50ec31c281de91903a1ef492a2ec7997) | Starts displaying a remote video image. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a20d2004010563e37804a6b82ed9d09ec) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#acdfe0dc822f074d5c42dfe308dc313a0) | Sets the fill mode of the local image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a4447783c52960cffbaedb7ccd7c456a2) | Sets the clockwise rotation degree of the local image. |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a5a04c60eb2e9997e745412374b7b8d19) | Sets the mirror mode of the local camera's preview image. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab5be71379d671f77b99cf6ccd86cdbc7) | Sets the rendering mode of a remote image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a385042d69e79468c9ef60dee8ec8cc96) | Sets the clockwise rotation degree of a remote image. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a5935a852496c1a033576cc6fbf676746) | Starts displaying the substream image (`TRTCVideoStreamTypeSub`, usually used for screen sharing) of a remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a56a7770d90cad9141aecbd70d93af588) | Stops displaying the substream image (`TRTCVideoStreamTypeSub`, usually used for screen sharing) of a remote user. This API is no longer used since version 8.0. Please use the `stopRemoteView(userId,streamType)` API instead. |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7832e5870431ccb0e75614b51af51205) | Sets the display mode of substream images (`TRTCVideoStreamTypeSub`, usually used for screen sharing). |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab63344839afca9bd4a890f6f609fd9e7) | Sets the clockwise rotation degree of substream images (`TRTCVideoStreamTypeSub`, usually used for screen sharing). |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a742eefe8508e744918f704e2fa0d3405) | Sets audio quality. |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a074579fcbcd5f4639ab40a2d5884fa3f) | Sets video quality preferences for viewers. |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ace7e563213b43c1763b1eb60d5b2e8c5) | Gets the camera list. |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#af5ce3a160a7f0dc889322983f5cfa68a) | Sets the camera to use. |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0f4a19bdc82b81dd1e0a8ac8b735261a) | Gets the camera currently in use. |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab85ff9472d499bd740f953ccff549147) | Gets the mic list. |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a5a17cc110f2b9c146df4498aa35eebc6) | Gets the mic currently in use. |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aded68bf47cb1e381961b0b69dde8931b) | Sets the mic to use. |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#addb5ea84bf67a3fdd49eee30e66f4826) | Gets the current mic volume. |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aaa35154699a59962bc065519e79761fa) | Sets the current mic volume. |
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a44453f04c53f19f65ca362a1cb55963b) | Sets whether to mute the current mic. |
| [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac7df6f29e11ded5faf7996334d4af61b) | Gets whether the current mic is muted. |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a20fa0073543ed1bd1df5dbb825b408bf) | Gets the speaker list. |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0ac0ecdbf0d077563fd6d2fb1ee65bee) | Gets the speaker currently in use. |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a768367aba35b104f8529740b86802b73) | Sets the speaker to use. |
| [getCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#accb2d6bc752f550b968462ba5a5c0538) | Gets the current speaker volume. |
| [setCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae99882060b048467a0f39f13b168775f) | Sets the current speaker volume. |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ad8c3800ba3e2101ff63de7117dc729f3) | Sets whether to mute the current speaker. |
| [getCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aa4ec49fc0c07c04031d328db5814793f) | Gets whether the current speaker is muted. |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | Starts camera testing. |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a32c469879fca0afec360690ee36c1b6b) | Starts camera testing. |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3cb3fd62d04b5975c9c50210e98f0a2d) | Stops camera testing. This API is no longer used since version 8.0. Please use the `ITXDeviceManager::stopCameraDeviceTest` API instead. |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aca6add13bdd6535bed6d28407b5468af) | Starts mic testing. |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a29c2a5a42f65108074174e0bc58c0aee) | Stops mic testing. This API is no longer used since version 8.0. Please use the `ITXDeviceManager::stopMicDeviceTest` API instead. |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#af60f0db87d1f7001860f1bf330eeee3c) | Starts speaker testing. |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aa4b7a172067664fe50015c758e02a822) | Stops speaker testing. This API is no longer used since version 8.0. Please use the `ITXDeviceManager::stopSpeakerDeviceTest` API instead. |
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a4e3fb7ca730f15b6ab201e73e21f1260) | Sets the mic volume. |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab0f8b23d8c48b9a056ca0e61ddcc894f2) | Starts screen sharing. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a815aa5a969dcb0617e02f955a9ee7cd4) | Starts background music. |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8eec0a8a7edf45d3b49b897286154b4f) | Stops background music. |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aed6272ead63eb14b9f64a92a59196c28) | Pauses background music. |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a221c73557814b71880c9a9323e3f31d2) | Resumes background music. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a487cff035a50da09ab39e87f7488d647) | Gets the total length of the music file, in milliseconds. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a2e2050b96d2b453e0ca83e483efec02c) | Sets the playback progress of background music. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ab651d0daff2d1b7e25b43606a4776796) | Sets the playback volume of background music. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a9c083e91e2af46503e522443a7b51b32) | Sets the local playback volume of background music. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#af193ff23e008485cf949d761028ce6e9) | Sets the remote playback volume of background music. |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a4db6f176c155c0f83d11eb302f6e1dab) | Plays an audio effect. |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a401d82c610be2136896c0f60621d66cf) | Sets the volume of an audio effect. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a254acc2f0fe96ffcce33629eb4309877) | Stops an audio effect. |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a07a2dfd7ce4e76b28172d73ee8405dbe) | Stops all audio effects. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a06219d65076c6c7024fab30d2516b167) | Sets the volume of all audio effects. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a2b004f3a3a7bdde7b2926930f31afa6c) | Pauses an audio effect. |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#af10583316f15ed709247590a081b2307) | Resumes an audio effect. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#adc372b21294cd36bf4f4af0d1ac6624a2) | Sets screen sharing parameters. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac9d547341170330a70623299b366c44a) | Enables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3a53ae79c1bd28825cb276c7555500fe) | Sends captured video data to the SDK. |

