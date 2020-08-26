## TRTCCloud @ TXLiteAVSDK

### Creation and termination

| API | Description |
|-----|-----|
| [delegate](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6a8e20d57b7890e4dbf6652c426d7015) | Sets [TRTCCloudDelegate](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#protocolTRTCCloudDelegate) callback API. |
| [delegateQueue](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a97158c52f2a4011454b4eb3ee369a8a1) | Sets the queue that drives the [TRTCCloudDelegate](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#protocolTRTCCloudDelegate) callback. |
| [sharedInstance](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) | Creates [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#interfaceTRTCCloud) singleton. |
| [destroySharedIntance](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad8961d03736d8a52df5a3a991d0a77c4) | Terminates [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#interfaceTRTCCloud) singleton. |


### Room API functions

| API | Description |
|-----|-----|
| [enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) | Enters room. If the room does not exist, the system will automatically create a new room. |
| [exitRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) | Exits room. |
| [switchRole](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) | Switches role. This API applies only to the live streaming scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [connectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abd656e4c9b6a01231810ae897627e9bc) | Exits cross-room call. |
| [setDefaultStreamRecvMode](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### CDN API functions

| API | Description |
|-----|-----|
| [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad6e5d54708867b8d9c9c492a02f2a1d5) | Starts pushing to Tencent Cloud LVB CDN. |
| [stopPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#afc00ba747be5299cd7235928a628339e) | Stops pushing to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aad42e78d355fd563b959a5053bac54cb) | Starts relaying to the live streaming CDN of another cloud. |
| [stopPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | Stops relaying to non-Tencent Cloud address. |
| [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) | Sets On-Cloud MixTranscoding parameters. |


### Video API functions

| API | Description |
|-----|-----|
| [startLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e) | Enables the preview image of local video (for iOS). |
| [startLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3fc1ae11b21944b2f354db258438100e2) | Enables the preview image of local video (for macOS). |
| [stopLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | Stops local video capture and preview. |
| [muteLocalVideo](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85ea151beebda2f86c3802f3a6a9e82) | Pauses/Resumes pushing local video data. |
| [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) | Starts displaying remote video image. |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2b7e96e4b527798507ff743c61a6a066) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [stopAllRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) | Stops displaying all remote video images and pulling the video data streams of all remote users. |
| [muteRemoteVideoStream](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aaf4376c4822aa9924733f8f165f17683) | Pauses/Resumes receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#adf7cd002366760749c6f4d1ee9291db1) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) | Sets video encoder parameters. |
| [setNetworkQosParam](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) | Sets the rendering mode of local image. |
| [setRemoteViewFillMode](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) | Sets the rendering mode of remote image. |
| [setLocalViewRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4d2d95ad8fbaf8edce18667aa835848e) | Sets the clockwise rotation angle of local image. |
| [setRemoteViewRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90) | Sets the clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) | Sets the direction of image output by video encoder (i.e., video image viewed by remote user and recorded by server).
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a97a2c690c467d58f74e17efe871b8403) | Sets the mirror mode of local camera's preview image (for iOS). |
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a97a2c690c467d58f74e17efe871b84032) | Sets the mirror mode of local camera's preview image (for macOS). |
| [setVideoEncoderMirror](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a29a7cae6b4e82098fc342d4f0066d2ad) | Sets the mirror mode of image output by encoder. |
| [setGSensorMode](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a7a8c22e2f02d313590d4c499e18ebe3f) | Sets the adaptation mode of g-sensor. |
| [enableEncSmallVideoStream](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2aa9c464203b1c62cbb9ccabccc6334a) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab6d4c9a4946e85b35547d73e9b232d92) | Specifies whether to view the big or small image of the specified `uid`. |
| [setPriorRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#adadb7a837e1b50ebdbb928d4bd81b5d5) | Sets the video quality preferred by viewers. |
| [snapshotVideo](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af8a1345d9c7bf0e1b1c782243eafbd93) | Video screenshot. |


### Audio API functions

| API | Description |
|-----|-----|
| [setAudioQuality](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53) | Sets sound quality. The higher the sound quality of the anchor, the better the sound effect to viewers, but the higher the required bandwidth, so there may be lags if the bandwidth is limited. |
| [startLocalAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3177329bc84e94727a1be97563800beb) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab78601c38f1b872b03b662e6856be84c) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9) | Mutes/Unmutes local audio. |
| [setAudioRoute](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa62f2af2d86a64c0ebc7b9f00e4a54fe) | Sets audio routing. |
| [muteRemoteAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) | Mutes/Unmutes specified remote user's audio. |
| [muteAllRemoteAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) | Mutes/Unmutes all users' audio. |
| [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5475b81c1712323257c10baaf7ad6969) | Sets SDK capture volume level. |
| [getAudioCaptureVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a7ce26486575e72bc445432929fdff26c) | Gets SDK capture volume level. |
| [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af2602b1e9dfe932c89dd411f2f227192) | Sets SDK playback volume level. |
| [getAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aba445625df38b8676d599df4a67a8407) | Gets SDK playback volume level. |
| [enableAudioVolumeEvaluation](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a57d48cb0dbd7705486453b46e30e3fea) | Enables volume reminder. |
| [startAudioRecording](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a9eadd65cef0ac6b9c04ddfd7265afb01) | Starts audio recording. |
| [stopAudioRecording](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ac8c12476bbcf3d691060954fcdb6ebe6) | Stops recording|
| [setSystemVolumeType](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab098daa610ae506dbf6c2a4f666ae32c) | Sets the system volume type used during call. |


### Camera API functions

| API | Description |
|-----|-----|
| [switchCamera](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa9a1952f442020bc92ce1beb65959e56) | Switches camera. |
| [isCameraZoomSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8662b8ecab04a55a321ee9f16d0680a7) | Queries whether the current camera supports zoom. |
| [setZoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | Sets the zoom factor (focal length) of camera. |
| [isCameraTorchSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#acd005524f8e2c2fbfcc415049e666ced) | Queries whether the device supports flash (flash mode). |
| [enbaleTorch](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af6b128ee01d91a63dc1976db7a9be555) | Enables or disables flash. |
| [isCameraFocusPositionInPreviewSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a0e164f727b990581a42f97dca1bf7548) | Queries whether the device supports setting focus. |
| [setFocusPosition](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6a77cc99c41b926cd99909ae1ace39ae) | Sets camera focus. |
| [isCameraAutoFocusFaceModeSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5af361145f04227ff1a451fee2705a77) | Queries whether the device supports automatic recognition of face position. |
| [enableAutoFaceFoucs](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a32a8f584879b17f211df75494a5be96c) | Enables automatic recognition of face position. |
| [getCameraDevicesList](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad93f6748f695f6735b8b22fdbda45115) | Gets camera list. |
| [getCurrentCameraDevice](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2d0a4120dfbc830aa53837cc019f450e) | Gets the currently used camera. |
| [setCurrentCameraDevice](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) | Sets the camera to be used. |


### Audio device API functions

| API | Description |
|-----|-----|
| [getMicDevicesList](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96fe0c67212fbc8ac9ddf648a40c70ca) | Gets mic list. |
| [getCurrentMicDevice](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a94b64d50649a7e99b8d6f22c094182e2) | Gets the currently used mic. |
| [setCurrentMicDevice](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af69d237159163eebcb6876e767d7692e) | Gets current mic volume level. |
| [setCurrentMicDeviceVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aaa6810f64c153e779697dc2d5bd30f6a) | Sets mic volume level. |
| [getSpeakerDevicesList](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a0267678df702f119b8124ed31533d74a) | Gets speaker list. |
| [getCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6c951071ac218930680febd84314ee05) | Sets the speaker to be used. |
| [getCurrentSpeakerDeviceVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa25ac85f6f84b352175aebb9c7007247) | Gets current speaker volume level. |
| [setCurrentSpeakerDeviceVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a019001b23569c8b6da7f3276af58e0a7) | Sets current speaker volume level. |


### Beauty filter API functions

| API | Description |
|-----|-----|
| [getBeautyManager](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) | Gets beauty filter management object. |
| [setWatermark](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad0bedbddf415d26cff8242d5842a0908) | Adds watermark. |


### Music effects and voice effects

| API | Description |
|-----|-----|
| [getAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) | Gets the sound effect management class `TXAudioEffectManager`. |


### Screen sharing API functions

| API | Description |
|-----|-----|
| [startScreenCaptureInApp](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5dbd40c4ad65152e85591c8535b4ee90) | Starts in-app screen sharing (this API supports only iPhones and iPads on iOS 13.0 and above). |
| [startScreenCaptureByReplaykit](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff) | Starts system-level screen sharing (this API supports iPhones and iPads on iOS 11.0 and above). |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | Starts screen sharing (for macOS). |
| [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) | Stops screen capture. |
| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | Pauses screen sharing. |
| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15) | Resumes screen sharing. |
| [getScreenCaptureSourcesWithThumbnailSize](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8e5286e1035b64b7d2bf8fadd721123) | Enumerates shareable windows. This API is supported only for macOS. You are recommended to call this API before calling `startScreenCapture`. |
| [selectScreenCaptureTarget](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) | Sets screen sharing parameters (supported only for macOS). This method can be called during screen sharing. |
| [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) | Starts displaying the secondary image of remote user (`TRTCVideoStreamTypeSub`, which is usually used for screen sharing). |
| [stopRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#acab6e31898857af876af66e779216203) | Stops displaying the secondary image of remote user (`TRTCVideoStreamTypeSub`, which is usually used for screen sharing). |
| [setRemoteSubStreamViewFillMode](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a487b3cd9a6b41581d4b45c752c5ede4c) | Sets the display mode of secondary image (`TRTCVideoStreamTypeSub`, which is generally used for screen sharing). |
| [setRemoteSubStreamViewRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a72c66b67eacd24a0e796a3213219fb6d) | Sets the clockwise rotation angle of secondary image (`TRTCVideoStreamTypeSub`, which is generally used for screen sharing). |
| [setSubStreamEncoderParam](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) | Sets encoder parameters for screen sharing (this API is supported only for macOS). |
| [setSubStreamMixVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a18d3fb6535c9884784c5ad5f8dfd0b12) | Sets the audio mixing volume level of screen sharing (this API is supported only for macOS). |


### Custom capture and rendering API functions

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ade46563b03208042e61bcc693e4a5d06) | Enables custom video capture mode. |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831) | Delivers captured video data to SDK. |
| [setLocalVideoRenderDelegate](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aba3d309645d27304b6d4ea31b21a4cda) | Sets the callback of custom rendering for local video. |
| [setRemoteVideoRenderDelegate](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5244e73ac27599370f966575e11959ff) | Sets the callback of custom rendering for remote video. |
| [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) | Enables custom audio capture mode. |
| [sendCustomAudioData](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a62cab4ec7c336ae135c2f681aca25da1) | Delivers captured audio data to SDK. |
| [setAudioFrameDelegate](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01726b03b102c32222a2a26b16abcd48) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#acbc86da0cb558c549f42e7e987c7beaf) | Sends custom message to all users in room. |
| [sendSEIMsg](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6de26e5efddf899d31158e4d48f17c02) | Embeds custom data of a small size in video frames. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a058556b224315dcde3601ab621a09dee) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a58d732ba648d1f9a3a460c02de79bb9b) | Stops server speed test. |
| [startCameraDeviceTestInView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a1bd6289b969adde0096c83d6a5532332) | Starts camera test. |
| [stopCameraDeviceTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a1b67fa3f322efe538d924b381c06e676) | Stops video test preview. |
| [startMicDeviceTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa6f467c12fcea7e09cc97861d511498a) | Starts mic test. |
| [stopMicDeviceTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a8cca1c5913ac021987680195075e5fc9) | Stops mic test. |
| [startSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a60aa520016687bea03f17cb4ec19c1b6) | Starts speaker test. |
| [stopSpeakerDeviceTest](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abf383f971dc54f0254b2d40f100cc9ca) | Stops speaker test. |


### Log API functions

| API | Description |
|-----|-----|
| [getSDKVersion](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ace5acd2fe597b6656b45aaa93e3e45a1) | Gets SDK version information. |
| [setLogLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a9d2b6a99e137a9667743edc8ac909493) | Sets log output level. |
| [setConsoleEnabled](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a177c4f1fbb2a011ff496417dc0245667) | Disables or enables console log printing. |
| [setLogCompressEnabled](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa51a341a43a854ac6e3fa1d0093fec95) | Enables or disables local log compression. |
| [setLogDirPath](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a93b48089741f7022aea1f8f93ce8fff9) | Modifies log storage path. |
| [setLogDelegate](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a41497e4242e3c42acfa35730cdc1ddf6) | Sets log callback. |
| [showDebugView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3bd71c8a99029c1a4708bf1c176aa299) | Displays dashboard. |
| [setDebugViewMargin](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aad41ff6d5b5565046911acf27bb3dee4) | Sets dashboard margin. |
| [callExperimentalAPI](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | Calls experimental API. |


### Disused API functions

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abb57991f5e4f4ca1b95c2181a7e538c8) | Sets mic volume level. |
| [setBeautyStyle](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a1336146862fb742de6cbe5718f9b7008) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setEyeScaleLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ae0e4341ef565cc5ba28101574179cd56) | Sets the effect level of eye enlarging filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceScaleLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | Sets the effect level of face slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceVLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | Sets the effect level of chin slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setChinLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a145d4ed3d5790a449a9884d282420216) | Sets the effect level of chin lengthening/shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceShortLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | Sets the effect level of face shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setNoseSlimLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ae94b107a9c476337585906c79b42ee95) | Sets the effect level of nose slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [selectMotionTmpl](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3aa8c561d744e3d921dff6186a6e4ade) | Selects the AI animated effect pendant to be used. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setMotionMute](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | Mutes animated effect. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a9a4b3b61c39c1c65e3426b35b0ace95f) | Starts screen sharing. |
| [setFilter](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) | Specifies material filter effect. |
| [setFilterConcentration](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3b0d7db70674f961c14b316f4e8e7a2b) | Sets filter effect level. |
| [setGreenScreenFile](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | Sets green screen video. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [playBGM](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4d9983591fa2a847e226b7a30e8db294) | Starts background music. |
| [getBGMDuration](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ac1f96932d02198cd045ee96f1306c8ba) | Gets the total length of music file in milliseconds. |
| [setBGMPosition](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a7fd043ae358c43f6a178837fb2846ef9) | Sets the playback progress of background music. |
| [setBGMVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#adbfc8e226df7c6caaaca1a89a9842f23) | Sets the playback volume level of background music. |
| [setBGMPlayoutVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a08c468f48d99aef0e89716111db1f422) | Sets the local playback volume level of background music. |
| [setBGMPublishVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a0cf0c090285038b23843c646009073d1) | Sets the remote playback volume level of background music. |
| [setReverbType](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a555cde4eda63d13bbad0dbdba7094a47) | Sets reverb effect. This API currently is supported only for iOS. |
| [setVoiceChangerType](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa60f54923826cc59d8a4526669c4ea5e) | Sets voice changer type. This API currently is supported only for iOS. |
| [playAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a2ae175694198a9b3d1b1647b7ce1dae0) | Plays back sound effect. |
| [setAudioEffectVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | Sets sound effect volume level. |
| [stopAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aacf50bc1e6040c11331e3c23b319f97b) | Stops sound effect. |
| [setAllAudioEffectsVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6b345c95b5b68198d8dbc64a3652ed35) | Sets the volume level of all sound effects. |
| [pauseAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab0d46ccb8fca811851b30e7731958024) | Pauses sound effect. |
| [resumeAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a207dd8909c05d4a8a1431d33e644d4fe) | Resumes sound effect. |
| [enableAudioEarMonitoring](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa26564f3388bc249ecbd2813d9c45390) | Enables in-ear monitoring. |


## TRTCCloudDelegate @ TXLiteAVSDK

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a10a711eb68abcacc1ca690501fc7c9fb) | Callback for error, which indicates that the SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a25ac0da9ad798a2313bdf8f296828541) | Callback for warning. This callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) | Callback of room entry. |
| [onExitRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) | Callback of room exit. |
| [onSwitchRole](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ade2c2eab48a30e7ca1c9246e573b7f28) | Callback of role switching. |
| [onConnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) | Callback of result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a26b34d83afac68928a156096862c9c06) | Callback of result of ending cross-room call (anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) | A user enters the current room. |
| [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) | A user exits the current room. |
| [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) | Whether the remote user has playable primary image (generally used for camera). |
| [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) | Whether the remote user has playable secondary image (generally used for screen sharing). |
| [onUserAudioAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) | Whether the remote user has playable audio data. |
| [onFirstVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a7fc7fd0144af2bc4ce0797f9de530d96) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aafc4536f552199368e48c8527783c410) | Playback of the first audio frame of a remote user starts (local audio currently is not supported for notification). |
| [onSendFirstLocalVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a17567554f413629a80b5970bdffdff7b) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#acb73daf4ce82cd03f787f057b233b412) | The first local audio frame data has been sent. |
| [onUserEnter](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a27002c05cf5d87630d791efa69a92e29) | Disused API: an anchor enters the current room. |
| [onUserExit](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a7e69d4ce9e2a66731995297e519d147f) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28) | Network quality. This callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afb0811035e97c8544dbc9ecbef461dd9) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aed43a70b4a95eb95181e2b410013bf54) | The connection between SDK and server has been closed. |
| [onTryToReconnect](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | The connection between SDK and server has been restored. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aaa74021e5fd2564afb2df50e25eedeff) | Camera is ready. |
| [onMicDidReady](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afdac7dee94451913a4dc9982badc8035) | Mic is ready. |
| [onAudioRouteChanged](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a1859305732dfd03de63c9b780f99d513) | Audio routing changes (for iOS only), i.e., whether the audio is output by speaker or receiver. |
| [onUserVoiceVolume](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a7775c3fbd84b8da3b7a75bdea27ed5c5) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDevice](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a0152908c497bd5ee5225251d9e93e500) | Callback of local device connection and disconnection. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsgUserId](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a324311b3d4f3930d9a50b8449b155dd3) | Callback of receipt of custom message. |
| [onMissCustomCmdMsgUserId](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#af1b8e7d0f73773eca509afc1cf4c9ece) | Callback of loss of custom message. |
| [onRecvSEIMsg](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a6e4365456cb4df6e1bdf870511b72042) | Callback of receipt of SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishing](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a75c6bf4a7c7ec60a24aabfe8e47ea1f4) | Callback of starting pushing to Tencent Cloud LVB CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#interfaceTRTCCloud). |
| [onStopPublishing](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a379dcf84e15f93b64efe2cb9f362877c) | Callback of stopping pushing to Tencent Cloud LVB CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#interfaceTRTCCloud). |
| [onStartPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a817783f364bf9f6f0a1df4bc26bad628) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aab032eb48a56e8351ada60ce5b510d5e) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ab5c98341b7536b5b65c04b835c4d28fb) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `[TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#interfaceTRTCCloud)`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#accb36b0eb1d1b72f32cf72617bb1c730) | Callback of audio effect playback end. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureStarted](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a7d15537d26fb001045ff95157d59ed3f) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a9cc6106085b2049838e21bb50e192786) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ae9c08ef9dd260cf6fd946209fda8a011) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a323d2b3e5b8b364722e0b161ab11c816) | This callback will be returned by the SDK when screen sharing is stopped. |


### Callback of custom processing of video data frames

| API | Description |
|-----|-----|
| [onRenderVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a7b43888945a9d12f088ed99a5854e3c1) | Callback of custom video rendering. |


### Custom audio data frame processing callbacks

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ab2296899861c97044513d6d21192f90c) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a3f4b821c6edf43b3744b5ca2749980d7) | Audio data from each remote user before audio mixing, i.e., raw data of each channel before audio mixing. For example, when converting a certain channel of audio to text, you must use the raw audio data of the channel. |
| [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e) | Audio data after audio data from each channel is mixed. |


### Log callbacks

>It is recommended to set the callback delegation object in a class that is initialized early, e.g., `AppDelegate`.

| API | Description |
|-----|-----|
| [onLog](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#ab1364c78a6f31a8c08d0138c4f6e9647) | Callback of log printing. |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCParams) | Room entry parameters. |
| [TRTCVideoEncParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) | Video encoding parameters. |
| [TRTCNetworkQosParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCNetworkQosParam) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | Video quality. |
| [TRTCVolumeInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVolumeInfo) | Volume level. |
| [TRTCMediaDeviceInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCMediaDeviceInfo) | Media device description. |
| [TRTCScreenCaptureSourceInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCScreenCaptureSourceInfo) | Screen sharing target information (only for MacOS). |
| [TRTCSpeedTestResult](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult) | Network speed test result. |
| [TRTCVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCVideoFrame) | Video frame information. |
| [TRTCAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrame) | Audio frame data. |
| [TRTCMixUser](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCMixUser) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCTranscodingConfig) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCPublishCDNParam) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams) | Audio recording parameters. |
| [TRTCAudioEffectParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCAudioEffectParam) | Sound effect. |
| [TRTCLocalStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCLocalStatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCRemoteStatistics) | Remote audio/video statistics. |
| [TRTCStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#interfaceTRTCStatistics) | Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5) | Video resolution. |
| [TRTCVideoResolutionMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gafdfe57c064658b38b78b0fd11e2706c0) | Video aspect ratio mode. |
| [TRTCVideoStreamType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga1974ff7e5e78b4455925faf74e38f1e8) | Video stream type. |
| [TRTCQuality](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga25f9ccb045890cb18a5f647ef3c1f974) | Image quality level. |
| [TRTCVideoFillMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga1a66aad6fff71205c7a266268e16f55c) | Video image fill mode. |
| [TRTCVideoRotation](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gae8bd6b06a2ca5f89f9b3cea393fc6eb9) | Video image rotation direction. |
| [TRTCBeautyStyle](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga9bafd3233be6cec1b380d469017ed3e6) | Beauty filter (skin smoothing) algorithm. |
| [TRTCVideoPixelFormat](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gabb58c142deac29da242c957f21c963e3) | Video pixel format. |
| [TRTCVideoBufferType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga0fce6f58df3d3021696d15eff683ed8b) | Video data container format. |
| [TRTCLocalVideoMirrorType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga1f76f60bf95c01dbf8d3f82f3d2cc097) | Mirror type of local video preview. |
| [TRTCAppScene](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga6ab617b26cf503a8c1bfec34a9918dbe) | Application scenario. |
| [TRTCRoleType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gad147b9b0249d0c2759cf1514c8978881) | Role, which applies only to the live streaming scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`).
| [TRTCQosControlMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga915f86fec1b00787147d40a189444823) | Bandwidth limit mode. |
| [TRTCVideoQosPreference](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga2c460e7365ad67ee0213545b0a67aa6d) | Image quality preference. |
| [TRTCAudioSampleRate](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga346b09a7691ce8c9813bac0feb057d08) | Audio sample rate. |
| [TRTCAudioQuality](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) | Sound quality. |
| [TRTCAudioRoute](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga81305fea3aae73346d04f0013e0194d4) | Audio playback mode (audio routing). |
| [TRTCReverbType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) | Audio reverb mode. |
| [TRTCVoiceChangerType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) | Voice changer mode. |
| [TRTCSystemVolumeType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gaac0cd0da9dd789dcec4ba16471006f23) | System volume type. |
| [TRTCLogLevel](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gacefec5143acae6d0524b5500f0155908) | Log level. |
| [TRTCGSensorMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga894251078222f9ac4ba5815aac4b493c) | G-sensor switch. |
| [TRTCMediaDeviceType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga4a04a7c25ed48ab15603e8c3db115b95) | Device type (only for macOS). |
| [TRTCScreenCaptureSourceType](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#gaeabd30a270055e48105a34c781c782b0) | Screen sharing target type (only for macOS). |
| [TRTCTranscodingConfigMode](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga907c7b1ef1f09fb7417a549e82110855) | MixTranscoding parameter configuration mode. |


