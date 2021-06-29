## TRTCCloud @ TXLiteAVSDK

### Basic APIs

| API | Description |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac5da416bb06d461c7e1e555e3fd143ee) | Creates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) singleton. |
| [destroySharedInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a69e76ca12b727c7cbcbdda274fc007a2) | Terminates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) singleton. |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a22fe2f31f2ef62fb3c6cba083dc6c016) | Sets the `TRTCCloudListener` callback API, through which users can receive status notifications from [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud). |
| [setListenerHandler](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a48c867145dcc09289f7af41871b4fdd9) | Sets the queue that drives the [TRTCCloudListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudListener) callback. |


### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) | Switches roles. This API works only in live streaming scenarios (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [ConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) | Requests a cross-room call (anchor competition). |
| [DisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af777ac398ac47c8e5649c983fa2053fa) | Exits a cross-room call. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) | Sets the audio/video data receiving mode, which must be set before room entry for it to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3c4a93d24e0ef076168b44cf3545a8d4) | Creates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) sub-instance. |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a6dc091ead812c50497c4b4e87e5c2fcf) | Terminates a [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) sub-instance. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a09fbe471def0c1790357fc2b70149784) | Switches rooms. |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a1c168a9aa35ccd0b24981526425e4730) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3067efa528fb9ffb8cf7685ce29925d4) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a41aefb8be652f8f6803020e543acaadc) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0e1e8a1eb1cac3f5e5d4433b4aa21e8e) | Stops relaying to non-Tencent Cloud addresses. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af7cf5544f9b8027e9526c32319a13838) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) | Enables preview of the local video. |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af6ee50bf2c4c592294061077fc727505) | Disables preview of the local video. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a13a2e406bffafecb96bfeac48d82746b) | Pauses/Resumes pushing local video data. |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d) | Sets the image to be pushed when local video pushing is paused. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) | Starts pulling and displaying the video image of a specified remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) | Stops displaying the video images of all users and pulling their video streams. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a79f78532789dc6bbf67b128d004fab6a) | Pauses/Resumes receiving a specified remote video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a2d8a7b74068026a85158262cc9aedd66) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) | Sets video encoder parameters. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a34d994fbba559994aaf3a1f20420a885) | Sets encoder parameters for substream video. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a02631a5e4251657875535c38ab319239) | Sets QoS control parameters. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#afe6ea1bf7c959722595356a9b7fc2179) | Sets rendering parameters for the local image. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a069766641cee1aff4844d0beaa18ee13) | Sets rendering parameters for a remote image. |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a272afecae1d291033cb9cd4b1d7b52e0) | Sets the rotation degree of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a32d9ba3696b305373508253f9bee8236) | Sets the mirror mode of encoded images. |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abbbe1548bfba0bd082a08478ce35e9bc) | Sets the adaptation mode of the G-sensor. |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3a040c5012cf572b9dfabcca87f2cbb7) | Enables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a2a018cc1010587ea9b0fbd791eb3c54f) | Switches between the small and big images of a specified remote user. |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ad2efc2703c86ee009bd4a1d440d0c1e0) | Sets video quality preferences for viewers. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae75285c95fc53651e24fa23c4141093b) | Takes a video screenshot. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) | Enables local audio capturing and upstream data transfer. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a272bba21d046347ac42d76069ba5972c) | Disables local audio capturing and upstream data transfer. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86) | Mutes/Unmutes local audio. |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a4a3dda74823afa597b42b981257e9e22) | Sets the audio route. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) | Mutes/Unmutes a specified remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) | Mutes/Unmutes all users. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3dabe4a4e13509cf1bd5b3d58aabaa06) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a6af5e2c4819a683042f382688aff41e9) | Sets the SDK capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a81037b960fb2b3501b1e8e60f2b5f9f3) | Gets the SDK capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b20e1eec637c82190c5264d78d686af) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5a1636fa1300b0b4e2829846c36450a2) | Gets the SDK playback volume. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ad1dbca6b3f22072d7b3963473d02e0d7) | Enables volume reminders. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af89a64fd6ccb822850f9bf7e8a1c8462) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a7d55e5f15d1291afc89f7e1dfe0a25d8) | Stops audio recording. |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5438dcc45dc2f26a3771a5feddcdef5d) | Sets the system volume type to use during calls. |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9306bca7c6a13e0443a3fa1b40c9f343) | Enables in-ear monitoring. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5d6bf60e9d3051f601988e55106b296c) | Starts local recording. |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae982c3c04c0195711ee4e56132522c4b) | Stops local recording. |


### Device management APIs

| API | Description |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae66395bc404d205fcd7fe9082ca85ce9) | Gets the device management module. |


### Beauty filter APIs

| API | Description |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) | Gets the beauty filter management object. |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a1083aaf0441e3d90ce6641d278a97a63) | Adds watermarks. |


### Music and voice effect API

| API | Description |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) | Gets the audio effect management class `TXAudioEffectManager`. |


### Substream APIs

| API | Description |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) | Starts screen sharing. |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab6c3014f6f88c775aa91fccea19ce8a4) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e) | Resumes screen sharing. |


### Custom capturing and rendering APIs

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | Enables custom video capturing. You can choose to publish the subsream or the big or small image of the primary stream.   |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | Sends captured video data to the SDK. |
| [setLocalVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b565dc8c77df7fb826f0c45d8ad2d85) | Sets the callback of video data for application of third-party beauty filters. |
| [setLocalVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa3cbb7a501c3151d94473965e2538c7a) | Sets the callback of local video for custom rendering. |
| [setRemoteVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a4fca6803d13e4c7ff00dcac2974637e4) | Sets the callback of remote videos for custom rendering. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a206b9ce3594aa535b633d4f7c8f97210) | Enables custom audio capturing. |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a30a542b7d540c8699595a22ca3401f29) | Sends captured audio data to the SDK. |
| [setAudioFrameListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a034b6fce9a517267acd874c243efc575) | Sets the audio data callback. |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0b36383129314d70f150c08de182e2b8) | Gets PTS for custom capturing. |
| [setCapturedRawAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9047b34857b12d85688b3b3f1ca1c3f0) | Sets the format of the callback of audio frames captured by the local mic. |
| [setLocalProcessedAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac0f65e13815edc05ebd765826a94e3dc) | Sets the format of the callback of audio frames captured locally and pre-processed by the audio module. |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a98a2e38d75366fbc2c4da92fec5c0a30) | Sets the format of the callback of audio frames sent to the speaker. |

| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a7b7d3707d2ed8e8f1221faf73af49027) | Specifies whether to mix external audio into the streams for pushing and playback. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa411a035318c3a757c5d361d143c929d) | Sends external audio data to the SDK. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa4847ad53acc9ab5990194b21ff5b070) | Sends a custom message to all users in the room. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a034f9e1effbdadf8b9bfb7f3f06486c4) | Embeds small-volume custom data in video frames. |


### Network testing APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0dbceb18d61d99ca33e967427dd0a344) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3e862cef0e818ddecdc3dc4d66a6f8f9) | Stops server speed testing. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aeb5168abbd62c631b65247e6289d1e2d) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a0ec9520dda7e2062f7455956d093113b) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a2942d9d05045d3f0e0add45a3e10b3ee) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a495d2122a4098ab371d825c1f0bb90f5) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a44c20358d08da798e0f15d142c9c3914) | Changes the path to save logs. |
| [setLogListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a299a71f4addb3638c7790de446fbdf37) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ad2cdb5d447114534f53bad5bdc48afba) | Displays the dashboard. |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa2014c293033e9ea60aa6ffd525ee2fa) | Sets the dashboard margin. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f331dd0cfff51ab5a3becf4950a55e) | Calls the experimental API. |


### Disused APIs (consider using new ones)

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab356494d1b7dd924be69b23aa631a85a) | Sets the mic volume. |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) | Sets the strength of the beauty, brightening, and rosy skin filters. |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a4ff69ce783f648f23dd737641344ac52) | Sets the strength of the eye enlarging filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceSlimLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78a159a2a45d24dbd5722eb73d237e8a) | Sets the strength of the face slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a58bb7ce1fbbc40a50647d64693ac5d41) | Sets the strength of the chin slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a774eb948494cecec024771434ccd9d3c) | Sets the strength of the jaw lengthening/shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa14091f0d02330cbd02da5186e9dd874) | Sets the strength of the face shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3f806534b2596d7e29ea0ea6c070b591) | Sets the strength of the nose slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a521a0446d0922d480a1eec4b86f1ecb2) | Selects an AI animated effect widget. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a066cbf8f4f6c1cd23fe9451b82c5a073) | Mutes animated effects. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a925323ab809957ccaeb4cef30841cb72) | Sets filters for specified materials. This API is no longer used since version 7.2. Please use `TXBeautyManager` instead. |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a5fb4c8bc9948e61a75b9ef85f618309d) | Sets filter strength. This API is no longer used since version 7.2. Please use `TXBeautyManager` instead. |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aef56a36b901d5e525ee539e7d5642063) | Sets green background effects for videos (valid only in the Enterprise Edition). This API is no longer used since version 7.2. Please use `TXBeautyManager` instead. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3df738557f5c658c37174ac9aeae9684) | Starts background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3ee7bdd15de4ba9010aa5ece3abff0ab) | Stops background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a21ddee03e6f4cec028a24e5d5e30955e) | Pauses background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aaa8b34ef2b334bd22a1cb6541a4c6702) | Resumes background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae7342a8bcfda22a872aa684f06a4677f) | Gets the total length of the music file, in milliseconds. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78f901b6175352a31b0236776bfdc661) | Sets the playback progress of background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ada9c2b4aaf9a1a9ab9cd846593fdf9e6) | Sets the playback volume of background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab1e1c94c9efd967dbffb46d3ba08fef5) | Sets the local playback volume of background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a535eab48f9df390f4de5ebd5afcd59e3) | Sets the remote playback volume of background music. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a6f4f89be3c810acfa2430ad65fd7ea68) | Sets the reverb effect. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37acaf3b2539e0b1c18123a646e91189) | Sets the voice changing type. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ad1ed7667282eccfac1992c1e547a5aeb) | Plays an audio effect. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | Sets the volume of an audio effect. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a18e4ca6939d005a1d67cef397ee8b8d4) | Stops an audio effect. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a770543c80d3a5629a26d1382535fb6c4) | Stops all audio effects. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9bb41c4ff1a5b24ca742fe3ce45a2bc0) | Sets the volume of all audio effects. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab32923d04ce164b82879b3e05833959f) | Pauses an audio effect. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a33ab6e798d3da245435166464b702d4f) | Resumes an audio effect. This API is no longer used since version 7.3. Please use `TXAudioEffectManager` instead.|
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c2) | Starts displaying a remote video image. This API is no longer used since version 8.0. Please use `startRemoteView(userId, streamType, view)` instead. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a2) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) | Sets the rendering mode of the local image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69) | Sets the clockwise rotation degree of the local image. |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1) | Sets the mirror mode of the local camera's preview image. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) | Sets the rendering mode of a remote image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a8478d804d2a07520ce2bc5466b727839) | Sets the clockwise rotation degree of a remote image. |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55) | Sets audio quality. Higher audio quality of the anchor means better listening experience for viewers, but higher audio quality is more demanding on bandwidth and therefore may lead to lag when bandwidth is insufficient. |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e2) | Enables local audio capturing and upstream data transfer. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#acdbe3829d20f58cedd5a0c2f49ea24dc) | Starts displaying the screen sharing image of a remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ae5f540d795425046c9166b0a2361a8de) | Stops displaying the screen sharing image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a73f66e66ffee44e19ebb4d8c56c89718) | Sets the display mode of screen sharing images. |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#affdf177b468fdf40a41782e2e47524cc) | Sets the clockwise rotation degree of screen sharing images. |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a1b43a65a32f9dcb81b39b9c51c5bc4c6) | Switches cameras. This API is no longer used since version 8.0. Please use the functions in `TXDeviceManager` instead. |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ac7ae26eca2f9a673121803d6d175b034) | Queries whether the current camera supports zoom. This API is no longer used since version 8.0. Please use the functions in `TXDeviceManager` instead. |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a9f761eebdf04f724e0d1591c41c6045f) | Sets camera zoom factor (focal length). |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a645183ba7c0cea748973796cb38aad8c) | Queries whether flash (torch mode) is supported. This API is no longer used since version 8.0. Please use the functions in `TXDeviceManager` instead. |
| [enableTorch](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a09253f6547914d54058831b61325e770) | Enables/Disables flash. |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abd39aca40adfc8da6beaf32141f84cfa) | Queries whether focus setting is supported. This API is no longer used since version 8.0. Please use the functions in `TXDeviceManager` instead. |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa7c65fb033727804e7a79b8f135c776c) | Sets camera focus. |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a23f25ffb81215a32517da78455459ff2) | Queries whether automatic facial recognition is supported. This API is no longer used since version 8.0. Please use the functions in `TXDeviceManager` instead. |
| [TRTCViewMargin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#adeb72b7f954af864743cdbeb283c534b) | Sets view margins. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a68187fc9a1656bb32cf825363745f7e7) | Enables custom video capturing |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | Sends captured video data to the SDK. |
### Callback APIs for background music playback

Callback APIs for background music playback

| API | Description |
|-----|-----|
| [onBGMStart](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#af7f9f419dafff42ef750256f953a88c9) | Callback of starting background music playback |
| [onBGMProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a30ab555520fa5a478f633394b9cd4d14) | Callback of the music playback progress |
| [onBGMComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a444c6749e7cb77466940ec1de1c88546) | Callback of ending background music playback |


## TRTCCloudListener @ TXLiteAVSDK

Callback APIs for Tencent Cloud’s video call feature

### Error and warning event callback APIs

| API | Description |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a511d0007e1990e63e853e46ce3f02670) | Error callback. This indicates that the SDK encountered an irrecoverable error. Such errors must be listened for, and UI reminders should be sent to users depending on the situation. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a9871472ee8195dfc5d0c34fae3294465) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API | Description |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) | Callback of room entry |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) | Callback of room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a6a4b7f39bc5dfb0c5d75ef8802e2e758) | Callback of role switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a6f7db4f0aaadad2cdfa822ba0060414c) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a9778a84932f02de9be52ea7513f606c1) | Callback of the result of room switching (`switchRoom`) |


### User event callback APIs

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a891f38e4cdeaf3ff18937726f0269c2c) | Callback of the entry of a user |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abfec3607f97823956fad77a7a63dc441) | Callback of the exit of a user |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) | Callback of whether a remote user has a playable primary image (usually the image of the camera) |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) | Callback of whether a remote user has a playable substream image (usually the screen sharing image) |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) | Callback of whether a remote user has playable audio data |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a0c1ccf1bec2d3261e9f11894b32e357e) | Callback of the rendering of the first video frame of the local user or a remote user |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a3516aaef4cb63e512cd713e4ec96d118) | Callback of the playing of the first audio frame of a remote user. No notifications are sent for local audio. |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a181788d7441d41022ce014095ee05353) | Callback of the sending of the first local video frame |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#acb73daf4ce82cd03f787f057b233b412) | Callback of the sending of the first local audio frame |
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aff18b3bc5b1e448b21b7614e5716e73e) | Disused API: callback of the entry of an anchor |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a0d1361e52e96b4c7c1a5f1b89f4ef0fb) | Disused API: callback of the exit of an anchor |


### Callback APIs for statistics on network quality and technical metrics

| API | Description |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b) | Callback of network quality. This callback is triggered every 2 seconds to collect statistics on the current upstream and downstream data transfer. |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a003278cb7647cd577702e8367c9e0a58) | Callback of statistics on technical metrics |


### Server event callback APIs

| API | Description |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aed43a70b4a95eb95181e2b410013bf54) | Callback of the disconnection of the SDK from the server |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | Callback of the SDK trying to connect to the server again |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | Callback of the reconnection of the SDK to the server |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ab77a0dff287e1642527cd414fc5fe5f5) | Callback of server speed test. The SDK tests the speed of multiple server addresses, and the test result of each IP address is returned through this callback. |


### Hardware event callback APIs

| API | Description |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aaa74021e5fd2564afb2df50e25eedeff) | Callback of the camera being ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#afdac7dee94451913a4dc9982badc8035) | Callback of the mic being ready |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a1a608275247d2912e26bd83f648d6378) | Callback of the change of the audio route, i.e., audio output (speaker or receiver) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a4e3b79968ccbb86de5b79e326a2daafa) | Callback of volume, including the volume of each `userId` and the total remote volume |


### Custom message receiving callback APIs

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a51fd654c5ec030ff84f208f2ba50298d) | Callback of the receipt of a custom message |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a98af11ba5b25d3124bd9533dc5197127) | Callback of the loss of a custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad3640e6bf80a1f93991644701e9b0d96) | Callback of the receipt of an SEI message |


### Callback APIs for CDN relayed push

| API | Description |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a03d0ef687b2973b9b13cb041bd35bb85) | Callback of starting to push to Tencent Cloud’s live streaming CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ad3cb7e5ceb69954d762eafca5a0e3a62) | Callback of stopping pushing to Tencent Cloud’s live streaming CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a64df36d6c56dd69d8b6f051fd9fffcbc) | Callback of the completion of starting relayed push to CDNs |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a6c3d63538897ddb9ed1b170819c41dca) | Callback of the completion of stopping relayed push to CDNs |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#af1c79a5ec3e0c106939e7f0d7849d694) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) |


### Audio effect callback API

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abe967d855abae66836877fe0dacf8b5f) | Callback of ending audio effects |


### Screen sharing callback APIs

| API | Description |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a7d15537d26fb001045ff95157d59ed3f) | Callback of starting screen sharing |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a12c57991389e32f04a56774df5d1ce76) | Callback of pausing screen sharing via the calling of [TRTCCloud.pauseScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#ade88963a254d297d3be1993e8a599f6e) | Callback of resuming screen sharing via the calling of [TRTCCloud.resumeScreenCapture()](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e) |
| [onScreenCaptureStopped](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a6c09b21b733da7d314d1db2cb03c8bcb) | Callback of stopping screen sharing |


### Local recording callback APIs

| API | Description |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a6d252931944577cc08d40db1f5ecd7bb) | Callback of starting a recording task |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a22f09234dc198d33fa38bbb595fb5764) | Callback of a recording task being executed |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a0a3eef0daeb5107290cb5190ceb9467b) | Callback of ending a recording task |


### Callback APIs for video frames for custom rendering
Directing to [TRTCVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#interfacecom_1_1tencent_1_1trtc_1_1TRTCCloudListener_1_1TRTCVideoRenderListener)

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a41b44f9b0583bbf56ad9e96065ea825c) | Callback of video frames for custom rendering |


### Callback APIs for third-party beauty filter data

| API | Description |
|-----|-----|
| [onGLContextCreated](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#af4a7a3a4e4945bf216d87f81b6926dab) | Callback of creating an OpenGL context in the SDK |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a22afb08b2a1a18563c7be28c904b166a) |Callback of video data to which third-party beauty filters are applied. This can be set using the `setLocalVideoProcessListener` API in [TRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud). |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a5f6d5ef01d3cd610959433107f78aa60) | Callback of destroying the OpenGL context in the SDK |


### Callback APIs for audio frames for custom processing (read-only)

| API | Description |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) | Callback of the audio data captured by the local mic |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46) | Callback of the audio data captured by the local mic and pre-processed by the audio module |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902) | Callback of the audio data of each remote user before audio mixing, i.e., the raw data of each channel before audio mixing. The data is needed when, for example, you want to convert the audio of a channel into text. |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7) | Callback of the audio data mixed from all channels and sent to the speaker |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a96923a9286a88b83d6890f607884ceb3) | Callback of data mixed from all audio in the SDK, including captured and played audio. |


### Log callback APIs

| API | Description |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a77d78090666e330606b670bf8ce2d854) | Callback of log printing |


### Screenshot callback API

| API | Description |
|-----|-----|
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#aa9c6d0488175f6d19f5f38f6307cfea4) | Callback of the completion of a screenshot |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a1751af68516425e5556e2057d0c90915) | Room entry parameters |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam) | Encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCNetworkQosParam) | QoS control parameters |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCRenderParams) | Remote image rendering parameters |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCQuality) | Network quality |
| [TRTCTexture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCTexture) | Video texture data, including texture ID and the EGL context |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFrame) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrame) | Audio frame information |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVolumeInfo) | Volume |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestResult) | Results of network speed tests |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a51966088a4a7382a37bc00fa78ff7385) | Position of the image of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a328b2e89495023a61efc342e3284477a) | On-Cloud MixTranscoding configuration |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCPublishCDNParam) | Relayed push parameters |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams) | Audio recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#ad82a59c2209c0596dabaee1152820494) | Audio effect parameters |
| [TRTCScreenShareParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCScreenShareParams) | Screen sharing parameters |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a1b79e0e45a5f137df2e1995af7c0885c) | Room switching parameters |
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrameCallbackFormat) | Parameters for the format of called back audio frames |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCLocalRecordingParams) | Local recording parameters |
| [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCStatistics) | Statistics |
| [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCStatistics_1_1TRTCRemoteStatistics) | Remote audio/video statistics |
| [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCStatistics_1_1TRTCLocalStatistics) | Local audio/video statistics |

