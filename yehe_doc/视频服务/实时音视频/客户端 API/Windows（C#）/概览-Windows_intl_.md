## Introduction
Since version 8.0, TRTC has provided new APIs for C++ in addition to the original ones. They can be used on Windows, iOS, macOS, and Android.
See the following documents for how to integrate the C++ APIs.  
- [iOS](https://cloud.tencent.com/document/product/647/32173#using_cpp)  
- [Android](https://cloud.tencent.com/document/product/647/32175#using_cpp)  
- [macOS](https://cloud.tencent.com/document/product/647/32176#using_cpp)  
- [Windows](https://cloud.tencent.com/document/product/647/32178#using_cpp)  

>?
>- The C++ APIs are currently available in TRTC Lite only.  
>- On Windows, the TRTC header file automatically adopts the "trtc" namespace. You do not need to specify the namespace.

## TRTCCloud @ TXLiteAVSDK
### Setting `TRTCCloudCallback` callbacks

| API | Description |
|-----|-----|
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | Sets the callback API [TRTCCloudCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#classtrtc_1_1TRTCCloudCallback). |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | Removes callbacks. |



### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | Switches roles. This API works only in live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab5a0622e5d3d521d79ba4f85c44244eb) | Requests a cross-room call (anchor competition). |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | Ends cross-room co-anchoring. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | Sets the audio/video data receiving mode, which must be set before room entry for it to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | Creates a `TRTCCloud` sub-instance. |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a980cf4d173abfb58c00ef35a20e12c85) | Terminates a `TRTCCloud` sub-instance. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | Switches rooms. |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Stops relaying to non-Tencent Cloud address. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aef6d61f571304066aaf839f7db00a17b) | Enables preview of the local video (for Windows and macOS). |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8ac23e725c7ed75488df1be2ee514884) | Enables preview of the local video. If you call this API before `enterRoom`, the SDK will turn on the camera, but will wait till you call `enterRoom` to start pushing streams. If you call this API after `enterRoom`, the SDK will turn on the camera and start pushing video streams automatically. You will receive the `onFirstVideoFrame(null)` callback in [TRTCCloudCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#classtrtc_1_1TRTCCloudCallback) when the first video frame is rendered. |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0af978a75d5ba671b7ce5f0b81b003c8) | Updates preview of the local video.
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | Stops local video capturing and preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a6070313a28d3302c94ad807c636eb60f) | Pauses/Resumes pushing local video data. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9) | Starts pulling and displaying the image of a specified remote user. |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a027a8b23a363dc91e6ce1c9773ee8664) | Updates the video rendering window of a remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abd186570272cd61b4a6e4aea870437e1) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | Stops displaying the video images of all users and pulling their video streams. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22155f6fe17dde77a16c273e0d5a02a3) | Pauses/Resumes receiving a specified remote video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55b0710284e44ba3703e22b07c3665c8) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad21668c7550aad44f1ed61265ffceb24) | Sets QoS control parameters. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | Sets rendering parameters for the local image (primary stream). |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | Sets the rotation of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | Sets the mirror mode of encoded images. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | Sets the rendering mode of a remote image. |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5019a8005cd96662ce2cface662a811e) | Enables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abd330074a9e99cb9c75d42ef3d1d63a0) | Specifies whether to view the big or small image of a specified `userId`. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | Takes a video screenshot. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a86c80ed357798e50ccf5c7ae47317f4c) | Enables local audio capturing and upstream data transfer. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | Disables local audio capturing and upstream data transfer. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | Mutes/Unmutes local audio. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | Mutes/Unmutes a specified remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | Mutes/Unmutes all users. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | Sets the SDK capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | Gets the SDK capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | Gets the SDK playback volume. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | Enables/Disables volume reminders. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | Stops audio recording. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | Starts local recording. |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | Stops local recording. |


### Device API

| API | Description |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | Gets the device management module. |


### Beauty filter and watermark APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | Sets the strength of the beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | Sets watermarks. |


### Music and voice effect APIs

| API | Description |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | Gets the audio effect management class `ITXAudioEffectManager`. |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad6a651a786871927917b087ae7094c8a) | Enables system audio capturing. |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | Disables system audio capturing. |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | Sets system audio capturing volume. |


### Screen sharing APIs

| API | Description |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd) | Starts screen sharing. |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | Resumes screen sharing. |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad23c03ad142e8a42c49967ff9ccf9592) | Enumerates shareable windows. We recommend that you call this API before calling `startScreenCapture`. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a542913f5081fb2479137a7416c970e2d) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | Sets audio mixing volume for screen sharing. |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff) | Adds a specified window to the exclusion list of screen sharing. Windows in the list will not be shared. |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf) | Removes a specified window from the exclusion list of screen sharing. |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | Removes all windows from the exclusion list of screen sharing. |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a442186322939f9b93d6c6e0a3ace7bd3) | Adds a specified window to the screen sharing list. Windows in the list will be shared if they are in the capturing area. |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | Removes a specified window from the screen sharing list. |
| [removeAllIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | Removes all windows from the screen sharing list. |


### Custom capturing and rendering APIs

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | Enables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | Sends captured video data to the SDK. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | Enables custom audio capturing. After this mode is enabled, the SDK will stop the original audio capturing process while continuing to encode and send data. You need to keep feeding your audio data to the SDK using [sendCustomAudioData()](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d). |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | Delivers captured audio data to SDK. |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | Specifies whether to mix external audio into the streams for pushing and playback. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd) | Sends custom substream audio data to the SDK. |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | Gets PTS for custom capturing. |
| [setLocalVideoProcessCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3f6d32bdf3cb0fe72b61455304b975c6)| Sets the callback of video data for the application of third-party beauty filters. |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | Sets custom rendering for a remote video. |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | Sets the audio data callback. |




### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | Sends a custom message to all users in the room. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | Embeds small-volume custom data in video frames. |



### Device and network testing APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#af86b2903b95b6e74f02d701701ce3380) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | Stops network speed testing. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | Sets the path to save logs. |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | Displays the dashboard. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab15fc0877664a8ac257ca4d6e7afc7b0) | Calls the experimental API. |


### Disused APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a26bfd13c4838d9088273aaad55b3c621) | Enables local audio capturing and upstream data transfer. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a38ff46d7ee110cc4ed1b4832decc78e9) | Starts displaying a remote video image. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aca1818ea1557ede57153f79bf24dd4e6) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#adfd1abf930d90e48645033e8125f7ae6) | Sets the fill mode of the local image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#acf7401863d4c53ca8b90448fae696f24) | Sets the clockwise rotation of the local image. |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#acf7401863d4c53ca8b90448fae696f24) | Sets the mirror mode of the local camera's preview image. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae5eed51d0b55c2b2fd0410e2383a43aa) | Sets the rendering mode of a remote image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a20cc5354ee7290a4fe0c561c5a1002ed) | Sets the clockwise rotation of a remote image. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a8c558caa6b4db039d6f778dc3d9ec0b8) | Starts displaying the substream image (`TRTCVideoStreamTypeSub`, usually used for screen sharing) of a remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a56a7770d90cad9141aecbd70d93af588) | Stops displaying the substream image (`TRTCVideoStreamTypeSub`, usually used for screen sharing) of a remote user. This API is no longer used since version 8.0. Please use the `stopRemoteView(userId,streamType)` API instead. |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a749827fd1626bdf6940486cf4f94fb81) | Sets the display mode of substream images (`TRTCVideoStreamTypeSub`, usually used for screen sharing). |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aab3f678108829558bde252e4a44c9686) | Sets the clockwise rotation of substream images (`TRTCVideoStreamTypeSub`, usually used for screen sharing). |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae9e231a18f3fc150efcbea4d31dde2c4) | Sets audio quality. |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a03d1b864630501881eb7a5466a204bd7) | Sets video quality preferences for viewers. |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aa6b352a78cdaa536a4f381c18b12baeb) | Gets the camera list. |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aae18b8f818dadc61fc69e781fa2564e3) | Sets the camera to use. |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a5884efde03e6cbdd5956352821fc803e) | Gets the camera currently in use. |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a7f55dec965753a0e916daf545c4c02d1) | Gets the mic list. |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a6c9a18c9005436f93f2d78f66cb172ce) | Gets the mic currently in use. |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a0ffc8eb4e9050536cc96069797283465) | Sets the mic to use. |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a2f776bd91a3cae88c2b110cec0a2e4ad) | Gets the current mic volume. |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a01e881b34e3876a04198731b7cbd929a) | Sets the current mic volume. |
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ac91001367c541cca16828440edcf532e) | Mutes/Unmutes the current mic. |
| [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a3e501339c03f38e93be7596ff652675c) | Gets whether the current mic is muted. |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ace28dde50b14c71ea0487d5c90ed810a) | Gets the speaker list. |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a67bf9270553f52ec9081b9e001436473) | Gets the speaker currently in use. |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a36ddc9e11deb0fb9689c4bb652ce8893) | Sets the speaker to use. |
| [getCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#af2aa87f67810db076449fef67e0c7049) | Gets the current speaker volume. |
| [setCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae5bed3e0181663b739c019be7b220dcf) | Sets the current speaker volume. |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae5bed3e0181663b739c019be7b220dcf) | Mutes/Unmutes the current speaker. |
| [getCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ab33f3a25d63ba5dece8dc481934f0e42) | Gets whether the current speaker is muted. |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a39d3c3f2fff4803eeaba090c3236eebc) | Starts camera testing. |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aeb78c95028742c49d4ddd1e3b6e66aa2) | Starts camera testing. |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ab9c4b4fd13d707c7d009ebfd301cc08b) | Stops camera testing. This API is no longer used since version 8.0. Please use the `ITXDeviceManager::stopCameraDeviceTest` API instead. |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae959c197b632783ec298c6f549c21030) | Starts mic testing. |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aca5d21b834a8863263789410026a2183) | Stops mic testing. This API is no longer used since version 8.0. Please use the `ITXDeviceManager::stopMicDeviceTest` API instead. |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a98d817ca58986e756ae7a7e14002b60e) | Starts speaker testing. |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae8b569605b72a467eb6a01c664afa999) | Stops speaker testing. This API is no longer used since version 8.0. Please use the `ITXDeviceManager::stopSpeakerDeviceTest` API instead. |
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a9fc6194bde0fc945a2cda4562116fd7c) | Sets the mic volume. |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ac2abdde0c55332bc883e70ab794e929d) | Starts screen sharing. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ad489b4bd998bc1ce911b01b6561c7633) | Starts background music. |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#afc2d9d18c1f3187be7507c2b58b8e62f) | Stops background music. |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#ae92ddbca534bba79c82ddc2a4cbbb119) | Pauses background music. |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#acf40ba767f62e49b54d5461639268126) | Resumes background music. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a4e9542c204fba5deeda5a23d21ab936f) | Gets the total length of the music file, in milliseconds. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a6d11b2bae707addba872b54bc591d3f9) | Sets the playback progress of background music. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a8fa9cc7afdab2998a0fc04ee5ac28845) | Sets the playback volume of background music. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a5f2340b5b3549f7491977174b03d9e57) | Sets the local playback volume of background music. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a9a5c74f8adf60b91c0b8053b62636c75) | Sets the remote playback volume of background music. |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#adf967d9f8b43c2136067a56acb3cf706) | Plays an audio effect. |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a863d956d20f2d856ea4cb6e4dfe068b0) | Sets the volume of an audio effect. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aac03904c97a44815b4395a3b479dcd88) | Stops an audio effect. |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a68ca8ad66ec47323708f766d1222435c) | Stops all audio effects. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a3ab679a79420e3c2200690b800b80d07) | Sets the volume of all audio effects. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#aa41cf52f6c97467c83dfcec4d7b0587d) | Pauses an audio effect. |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a86593fb0c5bfb5e608f714dbcc78fff7) | Resumes an audio effect. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a428eb11858f268c8f4350424cd7f84e7) | Sets screen sharing parameters. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#af297f4b7cc710c8cd7cfe5cd02470c81) | Enables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__IDeprecatedTRTCCloud__cplusplus.html#a598de64893203c591b99d521946d46ce) | Sends captured video data to the SDK. |

