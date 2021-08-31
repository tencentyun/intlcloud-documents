## TRTCCloud @ TXLiteAVSDK

### Creating and terminating instances

| API | Description |
|-----|-----|
| [delegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6a8e20d57b7890e4dbf6652c426d7015) | Sets the callback API [TRTCCloudDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#protocolTRTCCloudDelegate). |
| [delegateQueue](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a97158c52f2a4011454b4eb3ee369a8a1) | Sets the queue that drives [TRTCCloudDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#protocolTRTCCloudDelegate) callbacks. |
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) | Creates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) singleton. |
| [destroySharedIntance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad8961d03736d8a52df5a3a991d0a77c4) | Terminates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) singleton. |


### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) | Switches roles. This API works only in live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) | Requests a cross-room call (anchor competition). |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abd656e4c9b6a01231810ae897627e9bc) | Exits a cross-room call. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) | Sets the audio/video data receiving mode, which must be set before room entry to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6100a5f395442d38ce9adab922382caf) | Creates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) sub-instance. |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a19e0d7921ac494fb588a4654d97abe86) | Terminates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) sub-instance. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7c5a2aa06d649492f546d9c70a5de4a1) | Switches rooms. |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc00ba747be5299cd7235928a628339e) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aad42e78d355fd563b959a5053bac54cb) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | Stops relaying to non-Tencent Cloud addresses. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) | Enables preview of the local video (for iOS). |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e2) | Enables preview of the local video (for macOS). |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) | Updates preview of the local video. |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | Stops local video capturing and preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85ea151beebda2f86c3802f3a6a9e82) | Pauses/Resumes pushing local video data. |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2) | Sets the image to be pushed when local video pushing is paused. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) | Starts pulling and displaying the image of a specified remote user. |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) | Updates the image of a remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) | Stops displaying the video images of all users and pulling their video streams. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaf4376c4822aa9924733f8f165f17683) | Pauses/Resumes receiving a specified remote video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adf7cd002366760749c6f4d1ee9291db1) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9) | Sets QoS control parameters. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5d4f0aba952a355f153d374899e6dcec) | Sets rendering parameters for the local image. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae04d890786fc8c176cd5834e5892951a) | Sets rendering parameters for a remote image. |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) | Sets the rotation of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a29a7cae6b4e82098fc342d4f0066d2ad) | Sets the mirror mode of encoded images. |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7a8c22e2f02d313590d4c499e18ebe3f) | Sets the adaptation mode of the G-sensor. |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2aa9c464203b1c62cbb9ccabccc6334a) | Enables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab6d4c9a4946e85b35547d73e9b232d92) | Switches between the small and big images of a specified remote user. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96) | Takes a video screenshot. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) | Enables local audio capturing and upstream data transfer. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab78601c38f1b872b03b662e6856be84c) | Disables local audio capturing and upstream data transfer. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9) | Mutes/Unmutes local audio. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) | Mutes/Unmutes a specified remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) | Mutes/Unmutes all users. |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa62f2af2d86a64c0ebc7b9f00e4a54fe) | Sets the audio route. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a8d38580f2c35f7e9828c4e41c56db35a) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5475b81c1712323257c10baaf7ad6969) | Sets the SDK capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7ce26486575e72bc445432929fdff26c) | Gets the SDK capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af2602b1e9dfe932c89dd411f2f227192) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aba445625df38b8676d599df4a67a8407) | Gets the SDK playback volume. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a57d48cb0dbd7705486453b46e30e3fea) | Enables volume reminders. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9eadd65cef0ac6b9c04ddfd7265afb01) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac8c12476bbcf3d691060954fcdb6ebe6) | Stops audio recording. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b) | Starts local recording (for iOS). |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#affae72630393980fee79c21f2d20f602) | Stops local recording. |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) | Starts recording system audio (for macOS only). |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adef486f26a2c7d74a8cccb537367e66a) | Stops recording system audio (for macOS only). |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae) | Sets system audio capturing volume (for macOS only). |


### Device management APIs

| API | Description |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a950f3f1c949def9e1e470f467db7b27a) | Gets the device management class `TXDeviceManager`. |


### Beauty filter APIs

| API | Description |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) | Gets the beauty filter management object. |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad0bedbddf415d26cff8242d5842a0908) | Adds watermarks. |


### Music and voice effect APIs

| API | Description |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) | Gets the audio effect management class `TXAudioEffectManager`. |


### Screen sharing APIs

| API | Description |
|-----|-----|
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a16d30ca3f89863da2581ff3872bf31f0) | Starts in-application screen sharing. This API works on iPhone or iPad with iOS 13.0 or above. |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a12414559fc82b18e671262c4da37b171) | Starts system-level screen sharing. This API works on iPhone or iPad with iOS 11.0 or above. |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9a4b3b61c39c1c65e3426b35b0ace95f) | Starts desktop screen sharing (for macOS only). |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15) | Resumes screen sharing. |
| [getScreenCaptureSourcesWithThumbnailSize](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8e5286e1035b64b7d2bf8fadd721123) | Enumerates shareable windows (for macOS only). We recommend that you call this API before calling `startScreenCapture`. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) | Sets screen sharing parameters (for macOS only). This API can be called during screen sharing. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) | Sets encoder parameters for substream video (for macOS and iOS). |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a18d3fb6535c9884784c5ad5f8dfd0b12) | Sets the audio mixing volume for screen sharing (for macOS only). |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa567171999b17a7f5655213b193415a7) | Adds a specified window to the exclusion list of screen sharing. Windows in the list will not be shared. This API works on macOS only. |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a95b1f3fbc6ff755f67f7e9b86240ea5f) | Removes a specified window from the exclusion list of screen sharing. This API works on macOS only. |
| [removeAllExcludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab2b6a778a528d58e2a42c9adfc7684f2) | Removes all windows from the exclusion list of screen sharing. This API works on macOS only. |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233) | Adds a specified window to the inclusion list of screen sharing. All windows in the list will be shared. This API works on macOS only. |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a058ac1e2141d6eb1962219167add42bc) | Removes a specified window from the inclusion list of screen sharing. This API works on macOS only. |
| [removeAllIncludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a18a20767a0e1076ba16cd473a2512156) | Removes all windows from the inclusion list of screen sharing. This API works on macOS only. |


### Custom capturing and rendering APIs

| API | Description |
|-----|-----|
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) | Gets PTS for custom capturing. |
| [setLocalVideoProcessDelegete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2f73c33b1010a63bd3a06e639b3cf348) | Sets the callback of video data for the application of third-party beauty filters. |
| [setLocalVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aba3d309645d27304b6d4ea31b21a4cda) | Sets the callback of local video for custom rendering. |
| [setRemoteVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5244e73ac27599370f966575e11959ff) | Sets the callback of a remote video for custom rendering. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) | Enables custom audio capturing. |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a62cab4ec7c336ae135c2f681aca25da1) | Sends captured audio data to the SDK. |
| [setAudioFrameDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01726b03b102c32222a2a26b16abcd48) | Sets audio data callback. |
| [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) | Sets the format of the callback of audio frames captured by the local mic. |
| [setLocalProcessedAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9ec7c7123eb2f333769508de193ea51f) | Sets the format of the callback of audio frames captured locally and pre-processed by the audio module. |
| [setMixedPlayAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a24ad642b88cd3b2ca2d3044d72817090) | Sets the format of the callback of audio frames sent to the speaker. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ade46563b03208042e61bcc693e4a5d062) | Enables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c68312) | Sends captured video data to the specified `streamType` in the SDK. |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1101d883d65882f735e3d17f874a25cb) | Specifies whether to mix external audio into the streams for pushing and playback. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad1ecf9e33044cc83d109b36287b54e97) | Sends external audio data to the SDK. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acbc86da0cb558c549f42e7e987c7beaf) | Sends a custom message to all users in the room. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6de26e5efddf899d31158e4d48f17c02) | Embeds small-volume custom data in video frames. |


### Device and network testing APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a058556b224315dcde3601ab621a09dee) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a58d732ba648d1f9a3a460c02de79bb9b) | Stops server speed testing. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ace5acd2fe597b6656b45aaa93e3e45a1) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9d2b6a99e137a9667743edc8ac909493) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a177c4f1fbb2a011ff496417dc0245667) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa51a341a43a854ac6e3fa1d0093fec95) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a93b48089741f7022aea1f8f93ce8fff9) | Changes the path to save logs. |
| [setLogDelegate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a41497e4242e3c42acfa35730cdc1ddf6) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3bd71c8a99029c1a4708bf1c176aa299) | Displays the dashboard. |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aad41ff6d5b5565046911acf27bb3dee4) | Sets the dashboard margin. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | Calls the experimental API. |


### Disused APIs (consider using new ones)

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abb57991f5e4f4ca1b95c2181a7e538c8) | Sets the mic volume. |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1336146862fb742de6cbe5718f9b7008) | Sets the strength of the beauty, brightening, and rosy skin filters. |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae0e4341ef565cc5ba28101574179cd56) | Sets the strength of the eye enlarging filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | Sets the strength of the face slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | Sets the strength of the chin slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a145d4ed3d5790a449a9884d282420216) | Sets the strength of the jaw lengthening/shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | Sets the strength of the face shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae94b107a9c476337585906c79b42ee95) | Sets the strength of the nose slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3aa8c561d744e3d921dff6186a6e4ade) | Selects an AI animated effect widget. This API works only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | Mutes animated effects. This API works only in the [SDK Enterprise Edition](https://intl.cloud.tencent.com/document/product/647/34615). |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9a4b3b61c39c1c65e3426b35b0ace95f2) | Starts screen sharing. |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) | Sets filters for specified materials. |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3b0d7db70674f961c14b316f4e8e7a2b) | Sets filter strength. |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | Sets green screen effects for videos. This API works only in the Enterprise Edition. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4d9983591fa2a847e226b7a30e8db294) | Starts background music. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ac1f96932d02198cd045ee96f1306c8ba) | Gets the total length of the music file, in milliseconds. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a7fd043ae358c43f6a178837fb2846ef9) | Sets the playback progress of background music. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adbfc8e226df7c6caaaca1a89a9842f23) | Sets the playback volume of background music. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a08c468f48d99aef0e89716111db1f422) | Sets the local playback volume of background music. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a0cf0c090285038b23843c646009073d1) | Sets the remote playback volume of background music. |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a555cde4eda63d13bbad0dbdba7094a47) | Sets the reverb effect. This API works only on iOS currently. |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa60f54923826cc59d8a4526669c4ea5e) | Sets the voice changing type. This API works only on iOS currently. |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2ae175694198a9b3d1b1647b7ce1dae0) | Plays an audio effect. |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | Sets the volume of an audio effect. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aacf50bc1e6040c11331e3c23b319f97b) | Stops an audio effect. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6b345c95b5b68198d8dbc64a3652ed35) | Sets the volume of all audio effects. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab0d46ccb8fca811851b30e7731958024) | Pauses an audio effect. |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a207dd8909c05d4a8a1431d33e644d4fe) | Resumes an audio effect. |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa26564f3388bc249ecbd2813d9c45390) | Enables in-ear monitoring. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed492) | Starts displaying the video image of a remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a0662) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) | Sets the rendering mode of a remote image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90) | Sets the clockwise rotation of a remote image. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) | Starts displaying the substream image (`TRTCVideoStreamTypeSub`, usually used for screen sharing) of a remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#acab6e31898857af876af66e779216203) | Stops displaying the substream image (`TRTCVideoStreamTypeSub`, usually used for screen sharing) of a remote user. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) | Sets the rendering mode of the local image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4d2d95ad8fbaf8edce18667aa835848e) | Sets the clockwise rotation of the local image. |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a97a2c690c467d58f74e17efe871b8403) | Sets the mirror mode of the local camera's preview image (for iOS). |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a97a2c690c467d58f74e17efe871b84032) | Sets the mirror mode of the local camera's preview image (for macOS). |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a487b3cd9a6b41581d4b45c752c5ede4c) | Sets the display mode of substream images (`TRTCVideoStreamTypeSub`, usually used for screen sharing). |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a72c66b67eacd24a0e796a3213219fb6d) | Sets the clockwise rotation of substream images (`TRTCVideoStreamTypeSub`, usually used for screen sharing). |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#adadb7a837e1b50ebdbb928d4bd81b5d5) | Sets video quality preferences for viewers. |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53) | Sets audio quality. |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) | Enables local audio capturing and upstream data transfer. |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6a77cc99c41b926cd99909ae1ace39ae) | Sets camera focus. This API does not work if `enableAutoFaceFocus` is set to `YES`. |
| [enableAutoFaceFocus](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a32a8f584879b17f211df75494a5be96c) | Enables automatic recognition of the facial position. |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | Sets camera zoom factor (focal length). |
| [enbaleTorch](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af6b128ee01d91a63dc1976db7a9be555) | Enables/Disables flash. |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab098daa610ae506dbf6c2a4f666ae32c) | Sets the system volume type to use during calls. |
| [startCameraDeviceTestInView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a1bd6289b969adde0096c83d6a5532332) | Starts camera testing. |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa6f467c12fcea7e09cc97861d511498a) | Starts mic testing. |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a60aa520016687bea03f17cb4ec19c1b6) | Starts speaker testing. |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) | Sets the mic to use. |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aaa6810f64c153e779697dc2d5bd30f6a) | Sets the current mic volume. |
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) | Sets whether to mute the current mic. |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6c951071ac218930680febd84314ee05) | Sets the speaker to use. |
| [setCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a019001b23569c8b6da7f3276af58e0a7) | Sets the current speaker volume. |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a738ea0dffd48d5bc2b05b146eb79ec46) | Sets whether to mute the current speaker. |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) | Sets the camera to use. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe962) | Takes a video screenshot. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ade46563b03208042e61bcc693e4a5d06) | Enables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831) | Sends captured video data to the SDK. |

## TRTCCloudDelegate @ TXLiteAVSDK

### Error and warning event callback APIs

| API | Description |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a10a711eb68abcacc1ca690501fc7c9fb) | Error callback. This indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI messages should be displayed to users if necessary. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a25ac0da9ad798a2313bdf8f296828541) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API | Description |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) | Callback of room entry |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) | Callback of room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ade2c2eab48a30e7ca1c9246e573b7f28) | Callback of role switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a26b34d83afac68928a156096862c9c06) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ad848cbee89f8b6258c9f03f4cb253a31) | Callback of the result of room switching (`switchRoom`) |


### User event callback APIs

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) | Callback of the entry of a user |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) | Callback of the exit of a user |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) | Callback of whether a remote user has a playable primary image (usually the image of the camera) |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) | Callback of whether a remote user has a playable substream image (usually the screen sharing image) |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) | Callback of whether a remote user has playable audio data |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7fc7fd0144af2bc4ce0797f9de530d96) | Callback of rendering the first video frame of the local user or remote users |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aafc4536f552199368e48c8527783c410) | Callback of playing the first audio frame of a remote user. No notifications are sent for local audio. |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a17567554f413629a80b5970bdffdff7b) | Callback of sending the first local video frame |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#acb73daf4ce82cd03f787f057b233b412) | Callback of sending the first local audio frame |
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a27002c05cf5d87630d791efa69a92e29) | Disused API: callback of the entry of an anchor |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7e69d4ce9e2a66731995297e519d147f) | Disused API: callback of the exit of an anchor |


### Callback APIs for statistics on network quality and technical metrics

| API | Description |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the current upstream and downstream data transfer. |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afb0811035e97c8544dbc9ecbef461dd9) | Callback of statistics on technical metrics |


### Server event callback APIs

| API | Description |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aed43a70b4a95eb95181e2b410013bf54) | Callback of the disconnection of the SDK from the server |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | Callback of the SDK trying to connect to the server again |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | Callback of the reconnection of the SDK to the server |


### Hardware event callback APIs

| API | Description |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aaa74021e5fd2564afb2df50e25eedeff) | Callback of the camera being ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afdac7dee94451913a4dc9982badc8035) | Callback of the mic being ready |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a1859305732dfd03de63c9b780f99d513) | Callback of the change of the audio route, i.e., audio output (speaker or receiver). This API works only on iOS. |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7775c3fbd84b8da3b7a75bdea27ed5c5) | Callback of volume, including the volume of each `userId` and the total remote volume |
| [onDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a0152908c497bd5ee5225251d9e93e500) | Callback of the connection/disconnection of a local device |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a1c36efd81dc4edf88fc3bc6af83b1b5a) | Callback of volume change of the current audio capturing device |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f) | Callback of volume change of the current audio playback device |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676) | Callback of the system audio capturing result |


### Custom message receiving callback APIs

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a324311b3d4f3930d9a50b8449b155dd3) | Callback of receiving a custom message |
| [onMissCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af1b8e7d0f73773eca509afc1cf4c9ece) | Callback of losing a custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a6e4365456cb4df6e1bdf870511b72042) | Callback of receiving an SEI message |


### Callback APIs for CDN relayed push

| API | Description |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a75c6bf4a7c7ec60a24aabfe8e47ea1f4) | Callback of starting to push to Tencent Cloud’s live streaming CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a379dcf84e15f93b64efe2cb9f362877c) | Callback of stopping pushing to Tencent Cloud’s live streaming CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a817783f364bf9f6f0a1df4bc26bad628) | Callback of the completion of starting relayed push to CDNs |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aab032eb48a56e8351ada60ce5b510d5e) | Callback of the completion of stopping relayed push to CDNs |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ab5c98341b7536b5b65c04b835c4d28fb) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud) |


### Audio effect callback APIs

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a81bb22a3a908757f9ac2cb455d59e4be) | Callback of ending an audio effect |


### Screen sharing callback APIs

| API | Description |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a7d15537d26fb001045ff95157d59ed3f) | Callback of starting screen sharing |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a9cc6106085b2049838e21bb50e192786) | Callback of pausing screen sharing |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ae9c08ef9dd260cf6fd946209fda8a011) | Callback of resuming screen sharing |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a323d2b3e5b8b364722e0b161ab11c816) | Callback of stopping screen sharing |


### Media recording callback APIs

| API | Description |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a044ce179ac4bc0bc987a3b74ecd911e7) | Callback of media recording |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ab4250c05ea4b843c27385f77d5004fc3) | Callback of change of recording information |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ae78ca25acea4152bfd9d0ccf71bd4108) | Callback of ending recording |


### Third-party beauty filter callback APIs

| API | Description |
|-----|-----|
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a8d4f000b4169a64a8a8af15e51e5dd95) | Callback of video data to which third-party beauty filters are applied. This can be set using the·`setLocalVideoProcessDelegete` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#interfaceTRTCCloud). |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5f6d5ef01d3cd610959433107f78aa60) | Callback of destroying the OpenGL context in the SDK |


### Callback APIs for custom video processing

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#gadbe65ee6ef1d72cd5207cd5a0eb78391) | Callback of custom video rendering |


### Callback APIs for custom audio processing

| API | Description |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) | Callback of the raw audio data captured by the local mic |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0) | Callback of the audio data captured by the local mic and pre-processed by the audio module |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a) | Callback of the audio data of each remote user before audio mixing, i.e., the raw data of each channel before audio mixing. The data is needed when, for example, you want to convert the audio of a channel into text. |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e) | Callback of audio data mixed from all channels |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a905748efe966e94ec1212fda14161aee) | Callback of data mixed from all audio of the SDK (including captured and played back audio) |


### Log callback APIs

We recommend that you set the callback delegate object in a class that is initialized early, such as `AppDelegate`.

| API | Description |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#ab1364c78a6f31a8c08d0138c4f6e9647) | Callback of log printing |


## Definitions of Key Classes
| Class | Description |
|-----|-----|
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCRenderParams) | Video rendering parameters |
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) | Room entry parameters |
| [TRTCAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrameDelegateFormat) | Format of the callback of audio frames |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) | Video encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCNetworkQosParam) | QoS control parameters |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | Network quality |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCVolumeInfo) | Volume |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCScreenCaptureSourceInfo) | Screen sharing target (for macOS only) |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult) | Network speed testing result |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCVideoFrame) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrame) | Audio frame information |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCMixUser) | Position of the image of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCTranscodingConfig) | On-Cloud MixTranscoding configuration |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCPublishCDNParam) | CDN relayed push parameters |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams) | Audio recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCAudioEffectParam) | Audio effects |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCSwitchRoomConfig) | Room switching configuration |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCLocalRecordingParams) | Local media file recording parameters |
| [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCLocalStatistics) | Local audio/video statistics |
| [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCRemoteStatistics) | Remote audio/video statistics |
| [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCStatistics) | Statistics |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5) | Video resolution |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gafdfe57c064658b38b78b0fd11e2706c0) | Video aspect ratio mode |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga1974ff7e5e78b4455925faf74e38f1e8) | Video stream type |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga1a66aad6fff71205c7a266268e16f55c) | Video image fill mode |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gae8bd6b06a2ca5f89f9b3cea393fc6eb9) | Video image rotation |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga9bafd3233be6cec1b380d469017ed3e6) | Beauty filter (skin smoothing) algorithm |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gabb58c142deac29da242c957f21c963e3) | Video pixel format |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga0fce6f58df3d3021696d15eff683ed8b) | Video data container type |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga13da9775774c3251999f1e46d279305f) | Mirror type of local video preview |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga50f989651c9f893de7716ffbc2d2a5fc) | Source of video screenshots |
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga6ab617b26cf503a8c1bfec34a9918dbe) | Application scenario |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gad147b9b0249d0c2759cf1514c8978881) | Role, which applies only to live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`) |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga915f86fec1b00787147d40a189444823) | QoS control mode |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga2c460e7365ad67ee0213545b0a67aa6d) | Image quality preference |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga25f9ccb045890cb18a5f647ef3c1f974) | Network quality |
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga346b09a7691ce8c9813bac0feb057d08) | Audio sample rate |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) | Audio quality |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga81305fea3aae73346d04f0013e0194d4) | Audio playback mode (audio route) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) | Audio reverb type |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) | Voice changing type |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaac0cd0da9dd789dcec4ba16471006f23) | System volume type |
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gacefec5143acae6d0524b5500f0155908) | Log level |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga894251078222f9ac4ba5815aac4b493c) | G-sensor mode |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#gaeabd30a270055e48105a34c781c782b0) | Screen sharing target (for macOS only) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga907c7b1ef1f09fb7417a549e82110855) | Configuration mode for MixTranscoding parameters |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga4bb9927d377aa27b781fcfef5cf1058a) | Type of media to record |
