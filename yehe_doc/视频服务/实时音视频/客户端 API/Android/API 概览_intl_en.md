## TRTCCloud @ TXLiteAVSDK

### Basic methods

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [sharedInstance](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ac5da416bb06d461c7e1e555e3fd143ee) | Creates [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) singleton. |
| [destroySharedInstance](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a69e76ca12b727c7cbcbdda274fc007a2) | Terminates [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) singleton. |
| [setListener](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a22fe2f31f2ef62fb3c6cba083dc6c016) | Sets the `TRTCCloudListener` callback API, through which users can get various status notifications from [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud). |
| [setListenerHandler](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a48c867145dcc09289f7af41871b4fdd9) | Sets the queue that drives the [TRTCCloudListener](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudListener) callback. |


### Room API functions

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) | Enters room. If the room does not exist, the system will automatically create a new room. |
| [exitRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) | Exits room. |
| [switchRole](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) | Switches role. This API applies only to the live streaming scenario (`TRTC_APP_SCENE_LIVE` and `TRTC_APP_SCENE_VOICE_CHATROOM`). |
| [ConnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) | Requests cross-room call (anchor competition). |
| [DisconnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af777ac398ac47c8e5649c983fa2053fa) | Exits cross-room call. |
| [setDefaultStreamRecvMode](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |
| [createSubCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3c4a93d24e0ef076168b44cf3545a8d4) | Creates a [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) sub-instance |
| [destroySubCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a6dc091ead812c50497c4b4e87e5c2fcf) | Terminates a [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud) sub-instance |

### CDN API functions

| API                                                          | Description                   |
| ------------------------------------------------------------ | ----------------------------- |
| [startPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a1c168a9aa35ccd0b24981526425e4730) | Starts pushing to Tencent Cloud LVB CDN. |
| [stopPublishing](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3067efa528fb9ffb8cf7685ce29925d4) | Stops pushing to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a41aefb8be652f8f6803020e543acaadc) | Starts relaying to the live streaming CDN of another cloud. |
| [stopPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a0e1e8a1eb1cac3f5e5d4433b4aa21e8e) | Stops relaying to non-Tencent Cloud address. |
| [setMixTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af7cf5544f9b8027e9526c32319a13838) | Sets On-Cloud MixTranscoding parameters. |


### Video API functions

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) | Enables the preview image of local video. |
| [stopLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af6ee50bf2c4c592294061077fc727505) | Stops local video capture and preview. |
| [muteLocalVideo](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a13a2e406bffafecb96bfeac48d82746b) | Pauses/Resumes pushing local video data. |
| [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a57541db91ce032ada911ea6ea2be3b2c) | Starts displaying remote video image. |
| [stopRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a8f3e86bc219090d0e8f2d5c2fab4467a) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [stopAllRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) | Stops displaying all remote video images and pulling the video data streams of all remote users. |
| [muteRemoteVideoStream](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a79f78532789dc6bbf67b128d004fab6a) | Pauses/Resumes receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a2d8a7b74068026a85158262cc9aedd66) | Pauses/Resumes receiving all remote video streams. |
| [setVideoEncoderParam](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) | Sets video encoder parameters. |
| [setNetworkQosParam](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a02631a5e4251657875535c38ab319239) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) | Sets the rendering mode of local image. |
| [setRemoteViewFillMode](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) | Sets the rendering mode of remote image. |
| [setLocalViewRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69) | Sets the clockwise rotation angle of local image. |
| [setRemoteViewRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a8478d804d2a07520ce2bc5466b727839) | Sets the clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a272afecae1d291033cb9cd4b1d7b52e0) | Sets the direction of image output by video encoder (i.e., video image viewed by remote user and recorded by server).
| [setLocalViewMirror](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1) | Sets the mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a32d9ba3696b305373508253f9bee8236) | Sets the mirror mode of image output by encoder. |
| [setGSensorMode](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abbbe1548bfba0bd082a08478ce35e9bc) | Sets the adaptation mode of g-sensor. |
| [enableEncSmallVideoStream](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3a040c5012cf572b9dfabcca87f2cbb7) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a2a018cc1010587ea9b0fbd791eb3c54f) | Specifies whether to view the big or small image of the specified `uid`. |
| [setPriorRemoteVideoStreamType](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ad2efc2703c86ee009bd4a1d440d0c1e0) | Sets the video quality preferred by viewers. |
| [snapshotVideo](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ae75285c95fc53651e24fa23c4141093b) | Video screenshot. |


### Audio API functions

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setAudioQuality](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55) | Sets sound quality. The higher the sound quality of the anchor, the better the sound effect to viewers, but the higher the required bandwidth, so there may be lags if the bandwidth is limited. |
| [startLocalAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9428ef48d67e19ba91272c9cf967e35e) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a272bba21d046347ac42d76069ba5972c) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86) | Mutes/Unmutes local audio. |
| [setAudioRoute](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a4a3dda74823afa597b42b981257e9e22) | Sets audio routing. |
| [muteRemoteAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) | Mutes/Unmutes specified remote user's audio. |
| [muteAllRemoteAudio](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) | Mutes/Unmutes all users' audio. |
| [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a6af5e2c4819a683042f382688aff41e9) | Sets SDK capture volume level. |
| [getAudioCaptureVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a81037b960fb2b3501b1e8e60f2b5f9f3) | Gets SDK capture volume level. |
| [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a0b20e1eec637c82190c5264d78d686af) | Sets SDK playback volume level. |
| [getAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a5a1636fa1300b0b4e2829846c36450a2) | Gets SDK playback volume level. |
| [enableAudioVolumeEvaluation](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ad1dbca6b3f22072d7b3963473d02e0d7) | Enables volume reminder. |
| [startAudioRecording](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af89a64fd6ccb822850f9bf7e8a1c8462) | Starts audio recording. |
| [stopAudioRecording](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a7d55e5f15d1291afc89f7e1dfe0a25d8) | Stops recording|
| [setSystemVolumeType](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a5438dcc45dc2f26a3771a5feddcdef5d) | Sets the system volume type used during call. |
| [enableAudioEarMonitoring](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9306bca7c6a13e0443a3fa1b40c9f343) | Enables in-ear monitoring. |


### Camera API functions

| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------------- |
| [switchCamera](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a1b43a65a32f9dcb81b39b9c51c5bc4c6) | Switches camera. |
| [isCameraZoomSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ac7ae26eca2f9a673121803d6d175b034) | Queries whether the current camera supports zoom. |
| [setZoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9f761eebdf04f724e0d1591c41c6045f) | Sets the zoom factor (focal length) of camera. |
| [isCameraTorchSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a645183ba7c0cea748973796cb38aad8c) | Queries whether the device supports flash (flash mode). |
| [enableTorch](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a09253f6547914d54058831b61325e770) | Enables or disables flash. |
| [isCameraFocusPositionInPreviewSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abd39aca40adfc8da6beaf32141f84cfa) | Queries whether the device supports setting focus. |
| [setFocusPosition](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa7c65fb033727804e7a79b8f135c776c) | Sets camera focus. |
| [isCameraAutoFocusFaceModeSupported](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a23f25ffb81215a32517da78455459ff2) | Queries whether the device supports automatic recognition of face position. |


### Beauty filter API functions

| API                                                          | Description        |
| ------------------------------------------------------------ | ------------------ |
| [getBeautyManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) | Gets beauty filter management object. |
| [setWatermark](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a1083aaf0441e3d90ce6641d278a97a63) | Adds watermark. |


### Music effects and voice effects

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [getAudioEffectManager](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) | Gets the sound effect management class `TXAudioEffectManager` to manage background music, short sound effects, and vocal effects. |


### Secondary stream API functions

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------------- |
| [startScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58) | Starts screen sharing. |
| [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ab6c3014f6f88c775aa91fccea19ce8a4) | Stops screen capture. |
| [pauseScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | Pauses screen sharing. |
| [resumeScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e) | Resumes screen sharing. |
| [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#acdbe3829d20f58cedd5a0c2f49ea24dc) | Starts displaying the screen sharing image of remote user. |
| [stopRemoteSubStreamView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ae5f540d795425046c9166b0a2361a8de) | Stops displaying the screen sharing image of remote user. |
| [setRemoteSubStreamViewFillMode](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a73f66e66ffee44e19ebb4d8c56c89718) | Sets the display mode of screen sharing image. |
| [setRemoteSubStreamViewRotation](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#affdf177b468fdf40a41782e2e47524cc) | Sets the clockwise rotation angle of screen sharing image. |


### Custom capture and rendering API functions

| API                                                          | Description                     |
| ------------------------------------------------------------ | ------------------------------- |
| [enableCustomVideoCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a68187fc9a1656bb32cf825363745f7e7) | Enables custom video capture mode. |
| [sendCustomVideoData](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a39b79b77e3795e918383e945e9513d35) | Delivers captured video data to SDK. |
| [setLocalVideoRenderListener](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa3cbb7a501c3151d94473965e2538c7a) | Sets the callback of custom rendering for local video. |
| [setRemoteVideoRenderListener](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a4fca6803d13e4c7ff00dcac2974637e4) | Sets the callback of custom rendering for remote video. |
| [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a206b9ce3594aa535b633d4f7c8f97210) | Enables custom audio capture mode. |
| [sendCustomAudioData](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a30a542b7d540c8699595a22ca3401f29) | Delivers captured audio data to SDK. |
| [setAudioFrameListener](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a034b6fce9a517267acd874c243efc575) | Sets audio data callback. |


### Custom message sending APIs

| API                                                          | Description                          |
| ------------------------------------------------------------ | ------------------------------------ |
| [sendCustomCmdMsg](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa4847ad53acc9ab5990194b21ff5b070) | Sends custom message to all users in room. |
| [sendSEIMsg](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a034f9e1effbdadf8b9bfb7f3f06486c4) | Embeds custom data of a small size in video frames. |


### Network test

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startSpeedTest](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a0dbceb18d61d99ca33e967427dd0a344) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3e862cef0e818ddecdc3dc4d66a6f8f9) | Stops server speed test. |


### Log API functions

| API                                                          | Description                 |
| ------------------------------------------------------------ | --------------------------- |
| [getSDKVersion](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aeb5168abbd62c631b65247e6289d1e2d) | Gets SDK version information. |
| [setLogLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a0ec9520dda7e2062f7455956d093113b) | Sets log output level. |
| [setConsoleEnabled](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a2942d9d05045d3f0e0add45a3e10b3ee) | Disables or enables console log printing. |
| [setLogCompressEnabled](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a495d2122a4098ab371d825c1f0bb90f5) | Enables or disables local log compression. |
| [setLogDirPath](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a44c20358d08da798e0f15d142c9c3914) | Modifies log storage path. |
| [setLogListener](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a299a71f4addb3638c7790de446fbdf37) | Sets log callback. |
| [showDebugView](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ad2cdb5d447114534f53bad5bdc48afba) | Displays dashboard. |
| [setDebugViewMargin](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa2014c293033e9ea60aa6ffd525ee2fa) | Sets dashboard margin. |
| [TRTCViewMargin](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#adeb72b7f954af864743cdbeb283c534b) | View margin. |
| [callExperimentalAPI](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a37f331dd0cfff51ab5a3becf4950a55e) | Calls experimental API. |


### Disused API functions

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [setMicVolumeOnMixing](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ab356494d1b7dd924be69b23aa631a85a) | Sets mic volume level. |
| [setBeautyStyle](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setEyeScaleLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a4ff69ce783f648f23dd737641344ac52) | Sets the effect level of eye enlarging filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceSlimLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a78a159a2a45d24dbd5722eb73d237e8a) | Sets the effect level of face slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceVLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a58bb7ce1fbbc40a50647d64693ac5d41) | Sets the effect level of chin slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setChinLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a774eb948494cecec024771434ccd9d3c) | Sets the effect level of chin lengthening/shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFaceShortLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa14091f0d02330cbd02da5186e9dd874) | Sets the effect level of face shortening filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setNoseSlimLevel](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3f806534b2596d7e29ea0ea6c070b591) | Sets the effect level of nose slimming filter. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [selectMotionTmpl](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a521a0446d0922d480a1eec4b86f1ecb2) | Selects the AI animated effect pendant to be used. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setMotionMute](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a066cbf8f4f6c1cd23fe9451b82c5a073) | Mutes animated effect. This API takes effect only in the [Enterprise Edition SDK](https://intl.cloud.tencent.com/document/product/647/34615). |
| [setFilter](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a925323ab809957ccaeb4cef30841cb72) | Sets filter effect for specified material. This API is disused in v7.2. Please use [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html) to set the filter effect. |
| [setFilterConcentration](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a5fb4c8bc9948e61a75b9ef85f618309d) | Sets filter effect level. This API is disused in v7.2. Please use [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html) to set filter effect level. |
| [setGreenScreenFile](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aef56a36b901d5e525ee539e7d5642063) | Sets green screen video (it takes effect only in the Enterprise Edition and is invalid in other editions). This API is disused in v7.2. Please use [TXBeautyManager](http://doc.qcloudtrtc.com/group__TXBeautyManager__android.html) to set green screen video. |
| [playBGM](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3df738557f5c658c37174ac9aeae9684) | Starts background music. Supported audio file formats: AAC, MP and WAV.<br>This API is disused in v7.3. Please use  [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [stopBGM](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a3ee7bdd15de4ba9010aa5ece3abff0ab) | Stops background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [pauseBGM](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a21ddee03e6f4cec028a24e5d5e30955e) | Pauses background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [resumeBGM](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aaa8b34ef2b334bd22a1cb6541a4c6702) | Resumes background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [getBGMDuration](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ae7342a8bcfda22a872aa684f06a4677f) | Gets the total length of music file in milliseconds. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setBGMPosition](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a78f901b6175352a31b0236776bfdc661) | Sets the playback progress of background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setBGMVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ada9c2b4aaf9a1a9ab9cd846593fdf9e6) | Sets the playback volume level of background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setBGMPlayoutVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ab1e1c94c9efd967dbffb46d3ba08fef5) | Sets the local playback volume level of background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setBGMPublishVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a535eab48f9df390f4de5ebd5afcd59e3) | Sets the remote playback volume level of background music. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setReverbType](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a6f4f89be3c810acfa2430ad65fd7ea68) | Sets reverb effect. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setVoiceChangerType](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a37acaf3b2539e0b1c18123a646e91189) | Sets voice changer type. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [playAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ad1ed7667282eccfac1992c1e547a5aeb) | Plays back sound effect. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setAudioEffectVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | Sets sound effect volume level. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [stopAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a18e4ca6939d005a1d67cef397ee8b8d4) | Stops sound effect. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [stopAllAudioEffects](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a770543c80d3a5629a26d1382535fb6c4) | Stops all sound effects. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [setAllAudioEffectsVolume](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a9bb41c4ff1a5b24ca742fe3ce45a2bc0) | Sets the volume level of all sound effects. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [pauseAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#ab32923d04ce164b82879b3e05833959f) | Pauses sound effect. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |
| [resumeAudioEffect](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a33ab6e798d3da245435166464b702d4f) | Resumes sound effect. This API is disused in v7.3. Please use [TXAudioEffectManager](http://doc.qcloudtrtc.com/group__TXAudioEffectManager__android.html) to set sound effect and background music. |


### Callback APIs of background music playback

Callback APIs of background music playback.

| API                                                          | Description              |
| ------------------------------------------------------------ | ------------------------ |
| [onBGMStart](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#af7f9f419dafff42ef750256f953a88c9) | Callback notification of music playback start. |
| [onBGMProgress](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a30ab555520fa5a478f633394b9cd4d14) | Callback notification of music playback progress. |
| [onBGMComplete](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a444c6749e7cb77466940ec1de1c88546) | Callback notification of music playback end. |



## TRTCCloudListener @ TXLiteAVSDK

Event callback API for TRTC video call feature.

### Error events and warning events

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onError](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a511d0007e1990e63e853e46ce3f02670) | Callback for error, which indicates that the SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a9871472ee8195dfc5d0c34fae3294465) | Callback for warning. This callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API                                                          | Description                         |
| ------------------------------------------------------------ | ----------------------------------- |
| [onEnterRoom](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) | Callback of room entry. |
| [onExitRoom](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) | Callback of room exit. |
| [onSwitchRole](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a6a4b7f39bc5dfb0c5d75ef8802e2e758) | Callback of role switching. |
| [onConnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) | Callback of result of requesting cross-room call (anchor competition). |
| [onDisConnectOtherRoom](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a6f7db4f0aaadad2cdfa822ba0060414c) | Callback of result of ending cross-room call (anchor competition). |


### Member event callbacks

| API                                                          | Description                                            |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| [onRemoteUserEnterRoom](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a891f38e4cdeaf3ff18937726f0269c2c) | A user enters the current room. |
| [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abfec3607f97823956fad77a7a63dc441) | A user exits the current room. |
| [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) | Whether the remote user has playable primary image (generally used for camera). |
| [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) | Whether the remote user has playable secondary image (generally used for screen sharing). |
| [onUserAudioAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) | Whether the remote user has playable audio data. |
| [onFirstVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a0c1ccf1bec2d3261e9f11894b32e357e) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a3516aaef4cb63e512cd713e4ec96d118) | Playback of the first audio frame of a remote user starts (local audio currently is not supported for notification). |
| [onSendFirstLocalVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a181788d7441d41022ce014095ee05353) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#acb73daf4ce82cd03f787f057b233b412) | The first local audio frame data has been sent. |
| [onUserEnter](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#aff18b3bc5b1e448b21b7614e5716e73e) | Disused API: an anchor enters the current room. |
| [onUserExit](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a0d1361e52e96b4c7c1a5f1b89f4ef0fb) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onNetworkQuality](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b) | Network quality. This callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a003278cb7647cd577702e8367c9e0a58) | Callback of technical metric statistics. |


### Server event callbacks

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onConnectionLost](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#aed43a70b4a95eb95181e2b410013bf54) | The connection between SDK and server has been closed. |
| [onTryToReconnect](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | The connection between SDK and server has been restored. |
| [onSpeedTest](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ab77a0dff287e1642527cd414fc5fe5f5) | Callback of server speed test. The SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCameraDidReady](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#aaa74021e5fd2564afb2df50e25eedeff) | Camera is ready. |
| [onMicDidReady](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#afdac7dee94451913a4dc9982badc8035) | Mic is ready. |
| [onAudioRouteChanged](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a1a608275247d2912e26bd83f648d6378) | Audio routing changes, i.e., whether the audio is output by speaker or receiver. |
| [onUserVoiceVolume](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a4e3b79968ccbb86de5b79e326a2daafa) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |


### Custom message reception callbacks

| API                                                          | Description           |
| ------------------------------------------------------------ | --------------------- |
| [onRecvCustomCmdMsg](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a51fd654c5ec030ff84f208f2ba50298d) | Callback of receipt of custom message. |
| [onMissCustomCmdMsg](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a98af11ba5b25d3124bd9533dc5197127) | Callback of loss of custom message. |
| [onRecvSEIMsg](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ad3640e6bf80a1f93991644701e9b0d96) | Callback of receipt of SEI message. |


### CDN relayed push callbacks

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onStartPublishing](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a03d0ef687b2973b9b13cb041bd35bb85) | Callback of starting pushing to Tencent Cloud LVB CDN, which corresponds to the `startPublishing()` API in [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud). |
| [onStopPublishing](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ad3cb7e5ceb69954d762eafca5a0e3a62) | Callback of stopping pushing to Tencent Cloud LVB CDN, which corresponds to the `stopPublishing()` API in [TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud). |
| [onStartPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a64df36d6c56dd69d8b6f051fd9fffcbc) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a6c3d63538897ddb9ed1b170819c41dca) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#af1c79a5ec3e0c106939e7f0d7849d694) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `[TRTCCloud](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloud)`. |


### Audio effect callbacks

| API                                                          | Description        |
| ------------------------------------------------------------ | ------------------ |
| [onAudioEffectFinished](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abe967d855abae66836877fe0dacf8b5f) | Callback of audio effect playback end. |


### Screen sharing callbacks

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onScreenCaptureStarted](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a7d15537d26fb001045ff95157d59ed3f) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a12c57991389e32f04a56774df5d1ce76) | This callback will be returned by the SDK when screen sharing is paused by calling [TRTCCloud.pauseScreenCapture()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf). |
| [onScreenCaptureResumed](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#ade88963a254d297d3be1993e8a599f6e) | This callback will be returned by the SDK when screen sharing is resumed by calling [TRTCCloud.resumeScreenCapture()](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e). |
| [onScreenCaptureStopped](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a6c09b21b733da7d314d1db2cb03c8bcb) | This callback will be returned by the SDK when screen sharing is stopped. |


### Custom video data frame rendering callbacks

| API                                                          | Description          |
| ------------------------------------------------------------ | -------------------- |
| [onRenderVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a41b44f9b0583bbf56ad9e96065ea825c) | Callback of custom video rendering. |


### Custom audio data frame processing callbacks (read-only)

| API                                                          | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [onCapturedRawAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e)| Callback of audio data captured by local mic. |
| [onLocalProcessedAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46) | Calls back the audio data which is locally collected and pre-processed by the audio module |
| [onRemoteUserAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902)  | Audio data from each remote user before audio mixing, i.e., raw data of each channel before audio mixing. For example, when converting a certain channel of audio to text, you must use the raw audio data of the channel. |
| [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log callbacks
>It is recommended to set the callback object in a class that is initialized early, e.g., `Application`.

| API                                                          | Description          |
| ------------------------------------------------------------ | -------------------- |
| [onLog](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a77d78090666e330606b670bf8ce2d854) | Callback of log printing. |


### Screencapturing callback

| API                                                          | Description      |
| ------------------------------------------------------------ | ---------------- |
| [onSnapshotComplete](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#aa9c6d0488175f6d19f5f38f6307cfea4) | Callback of screencapturing completion. |


## Definitions of Key Classes

| Class                                                        | Description                             |
| ------------------------------------------------------------ | --------------------------------------- |
| [TRTCParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a1751af68516425e5556e2057d0c90915) | Room entry parameters. |
| [TRTCVideoEncParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam) | Encoding parameters. |
| [TRTCNetworkQosParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCNetworkQosParam) | Network bandwidth limit parameters. |
| [TRTCQuality](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCQuality) | Video (or network) quality. |
| [TRTCTexture](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCTexture) | Video texture data, including texture ID and EGL environment. |
| [TRTCVideoFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFrame) | Video frame information. |
| [TRTCAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrame) | Audio frame data. |
| [TRTCVolumeInfo](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVolumeInfo) | Volume level. |
| [TRTCSpeedTestResult](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestResult) | Network speed test result. |
| [TRTCMixUser](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#afe6b433091e7b7219c4e55194855612e) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#a6066a5537ad8c1bc6158d43e8a4765db) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCPublishCDNParam) | Relayed push parameters. |
| [TRTCAudioRecordingParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams) | Audio recording parameters. |
| [TRTCAudioEffectParam](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#ad82a59c2209c0596dabaee1152820494) | Sound effect. |
| [TRTCScreenShareParams](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCScreenShareParams) | Screen sharing parameters. |
| [TRTCStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCStatistics) | Statistics. |
| [TRTCRemoteStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCStatistics_1_1TRTCRemoteStatistics) | Remote audio/video statistics. |
| [TRTCLocalStatistics](http://doc.qcloudtrtc.com/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCStatistics_1_1TRTCLocalStatistics) | Local audio/video statistics. |
