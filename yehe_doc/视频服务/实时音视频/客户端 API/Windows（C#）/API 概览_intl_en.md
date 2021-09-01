## ITRTCCloud @ TXLiteAVSDK

### Creating and terminating an ITRTCCloud singleton

| API | Description |
|-----|-----|
| [getTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aaab1651edd65e6ab0abec12efb945714) | Gets [ITRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#classManageLiteAV_1_1ITRTCCloud) singleton object. |
| [destroyTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4a0722972418aa87ae602f7e12d466ac) | Releases [ITRTCCloud](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#classManageLiteAV_1_1ITRTCCloud) singleton object. |


### Setting `TRTCCloudCallback` callbacks

| API | Description |
|-----|-----|
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a09b1c2ec021a62334da5fff4bd36d805) | Sets [ITRTCCloudCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#interfaceManageLiteAV_1_1ITRTCCloudCallback) callback API. |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afdcaecebad62bfcceecb97f5cbe2bf88) | Removes event callback. |


### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a28b2d3ec27af8c9bfd5cf687dd8e002b) | Enters room. If the room does not exist, the system will automatically create a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a715f5b669ad1d7587ae19733d66954f3) | Exits room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a94ab2e8a7df0c120def9d4b0c7658d84) | Switches role. This API applies only to the live streaming scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`). |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa29407e4c40f2bf61777bbe054f6bf0f) | Requests cross-room call (anchor competition). |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abd656e4c9b6a01231810ae897627e9bc) | Disables cross-room co-anchoring. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae870243f89b5829cd7ac5612ec958cdf) | Sets audio/video data reception mode, which must be set before room entry for it to take effect. |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad23040b25685bed8a9fa35bec28024bd) | Starts pushing streams to Tencent Cloud LVB CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afc00ba747be5299cd7235928a628339e) | Stops pushing stream to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adf6a56b335c9860c3ea1a090cad9bf7b) | Starts relaying to the live streaming CDN of another cloud. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | Stops relaying to non-Tencent Cloud address. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9a92140403d83a22f4334c0002f71d8d) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad8c3209fababfee7491605fd288e83df) | Enables the preview image of local video. |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | Stops local video capture and preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad531b6af4f07d93b937901aea73d9008) | Specifies whether to block local video image. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3c630b75a0e4452f4003b78e56770cda) | Starts displaying remote video image. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a94c9bede8c6630418ea7e960578c033f) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aaa75cd1b98c226bb7b8a19412b204d2b) | Stops displaying all remote video images and pulling the video data streams of all remote users. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3ab42b16228893891003df17c51fa2c4) | Pauses receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a129fb0485b0ba8b002e5806e57642715) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9445f85f7e8aef1c63829842ea801c11) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa1b61a44d79e6f6b11163594077d93b7) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ada1aa39d0b579f0f939d17c3ca78df92) | Sets the rendering mode of local image. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aeeb9e236aaa9c2ae9846af86ff3195d4) | Sets the rendering mode of remote image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8d5dc6995392c71257493353e3571e86) | Sets the clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a87f256d5148e34bd59756fa516307fce) | Sets the clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a291f1c48e5446135c29188f759f023cb) | Sets the direction of image output by video encoder (i.e., video image viewed by remote user and recorded by server). |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a050a53b8bed638f76a64ad82ecd89078) | Sets the mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3e6dae3e385f1e15d528ec3d6f57a59c) | Sets the mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4a83369f8798e273caf0a6550cb19cfe) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0c980fb80401d6fc14a69bfd16283b76) | Specifies whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5cc9f8652845ff0d7adc5b2d24b8a269) | Sets the video quality preferred by viewers. |


### Audio APIs

| API | Description |
|-----|-----|
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae241d03683fdde1e033078a6057f609c) | Sets sound quality. The higher the sound quality of the anchor, the better the sound effect to viewers, but the higher the required bandwidth, so there may be lags if the bandwidth is limited. |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3177329bc84e94727a1be97563800beb) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab78601c38f1b872b03b662e6856be84c) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a16d9b4a197a7bc1955240a1ede889246) | Mutes local audio. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abe535ac1d0a74de860c85ae09a3317df) | Mutes specified remote user's audio and stops pulling the audio data stream of remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9c118b189a47109289528b3c00019649) | Mutes all users' audio and stops pulling audio data streams of remote users. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a53681962139b81140f2d66abc4ea6a0f) | Sets SDK capture volume level. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad3dd226f138590f0e2c6b03f108c4e38) | Gets SDK capture volume level. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9b8946403b8b3ac8e11f3a78e9d531ca) | Sets SDK playback volume level. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#acd6e6336d8f314cef76de9da831a58dd) | Gets SDK playback volume level. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac5711f9704dbea303cf746da26b16a6a) | Enables or disables volume reminder. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8e34f7bd3e4b1d63eced9a5273f5afa9) | Starts recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac8c12476bbcf3d691060954fcdb6ebe6) | Stops recording. |


### Camera APIs

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac089937783fa14655f4944e7137e9fe6) | Gets camera list. |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa0f185dd21e3e55fadf5c21528223e5f) | Sets the camera to be used. |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a24ac636304cb989cce4e43a460ad659e) | Gets the currently used camera. |


### Audio device APIs

| API | Description |
|-----|-----|
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af52dcefa14a0838a98d878620e4a8e83) | Gets mic list. |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aeea733cfe13334913e7e8d1cbb4d35ff) | Gets the currently used mic. |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7a7bc332f677f536e2697e6f30235241) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5feaad27747bc7e909de43444aa86e2f) | Gets current system mic volume level. |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a02cdbf0a22ec4effeb662da83d7b5218) | Sets current system mic volume level. |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9f680a2953562c62e5024ef98e691803) | Gets speaker list. |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af38430fc0b347637e5b050481b2d6065) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3d8a1b1f3c71a08faaff27edaef3f80f) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1617113ec7db9d646b27233da8132b48) | Gets current system speaker volume level. |
| [setCurrentSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5fe7bfacc946565df7d14a91f6de9f21) | Sets current system speaker volume level. |


### Beauty effects and image watermark APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a3eb000f9a504e96d2f12fc1d8a6e47b9) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ac6451172a12f33274215785b029be727) | Sets watermark. |



### Music and voice effects API

| API | Description |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab43456e2e7d83986fd66708131d8c264) | Gets the sound effect management class `TXAudioEffectManager`. |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aac7057a9556fc1b1b106733a87069e06) | Enables system audio capture |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adef486f26a2c7d74a8cccb537367e66a) | Disables system audio capture |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2bb76d46a5fcf037c560ab8f09b1825f) | Sets system audio capture volume level |


### Substream APIs

| API | Description |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e254) | Starts screen sharing. |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad02093be5c603f66f356978169946a18) | Stops screen capture. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a448e432a91c092f80421d377425fb1bb) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad1fc32927622168e9b3cbb3f70043450) | Resumes screen sharing. |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1eda1853bfc49c43a35e4d945dfccd7a) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a92) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) | Starts rendering the substream image of remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a92ad3b6468abc72890c053a94765c4de) | Stops displaying the screen sharing image of remote user. |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a23a2fc554362748ef3d0c543918fd35d) | Sets the rendering mode of substream image. |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#acd8fb23b00e6638466f65512723a7395) | Sets the clockwise rotation angle of screen sharing image. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7e9588c951feaf2d70c8bd6412432f09) | Sets encoder parameters for screen sharing. |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aabc643e4be3add7e08b8fb3f1a9789a9) | Sets the audio mixing volume level of substream. |


### Custom capture and rendering APIs

| API | Description |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a87dace307d0df1eb4a5801d65517f40b) | Enables custom video capture mode. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a5d27319a247b7a592726994055b3c318) | Delivers captured video data to SDK. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a6cf1f1f480d3a6228f55d7e57ad506a8) | Enables custom audio capture mode. |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a0a4c65597f32583b10fc9340d679ac2e) | Delivers captured audio data to SDK. |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad229dd9299a1bc2f025443045bf4a83d) | Sets custom rendering for local video. |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a9bca8939353ec025d81db79f2791206f) | Sets custom rendering for remote video. |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae5b754d3ca87d0a653ae604238465efc) | Sets audio data callback. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a824ae2f32e2b2cf553b1a9709bea9f30) | Sends custom message to all users in room. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a253023d332139a09cbb4d592042b84e6) | Embeds custom data of a small size in video frames. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7dc88d324541c15e2781d1df10625fed) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a58d732ba648d1f9a3a460c02de79bb9b) | Stops network speed test. |
| [startCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adfdfd81465003ac6d21e5be20c119c41) | Starts camera test. |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1b67fa3f322efe538d924b381c06e676) | Stops camera test. |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aaa98e72f47a57ee2ff4e8b3670573688) | Enables mic test. |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a8cca1c5913ac021987680195075e5fc9) | Stops mic test. |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2adcedc6f4e867eca4d6db7c1923009a) | Enables speaker test. |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#abf383f971dc54f0254b2d40f100cc9ca) | Stops speaker test. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a85b31ef9401eadb11981cce536e1e85e) | Gets SDK version information. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ab941d390cf7df8034c522edd8dd2f3eb) | Sets log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a452f7778aaba21498765444f907bb0a0) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#af6d9f433c0c17ca34b040c51403865db) | Enables or disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#acca01dd55d9e0b30cfaac7df0ed3fe55) | Sets log storage path. |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a44ad1112f3666f86131c5e8cbf3093eb) | Sets log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a08d4c264ef3f43eea7616e4264a1e4e6) | Displays dashboard. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#add201789a0da7c5893cc5636ad9e783e) | Calls experimental API. |


### Disused APIs

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a1fff2c9d17bc4197c0097c01397bf70e) | Sets mic volume level. |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#adde6382876b0afab78bab89e8be8e2542) | Starts screen sharing. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2dc777ac9dbc51c01eb735a62318fcc5) | Starts background music. |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a11004f1ba27b057985850a25307b0bec) | Stops background music. |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa4b92d4c989e99612f6c4dab03a78764) | Pauses background music. |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aed6e8f224b5f834b1bc0c15f9701f692) | Resumes background music. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a05d821f12515462f9f1f441a30064e10) | Gets the total length of music file in milliseconds. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a4e0ae301ab2c14afe7f7a5656e4b0693) | Sets the playback progress of background music. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aaf6c2319fd42b0453b7408d3f3d60cb4) | Sets the playback volume level of background music. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a74be58163008d9a85701663e8cfcd3d0) | Sets the local playback volume level of background music. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ad3dd3d419d87c3518088bce81fd5749b) | Sets the remote playback volume level of background music. |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#aa0464fd4855bf9d3275036d04a3e4c74) | Plays back sound effect. |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a942a6f358980c8520e2155fb4ef55bd0) | Sets sound effect volume level. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a61561195216ac575235b67d410070563) | Stops sound effect. |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a7066509af1de32c290b7cc297cd00f2b) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a19416181cce88c58052a4eb2e87adeb8) | Sets the volume level of all sound effects. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a43f83a1323cc39c1610c61cf79ab652c) | Pauses sound effect. |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a23b65446d7dd9835da888b5285867629) | Resumes sound effect. |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#a2aabe079ed38fb5122be988434a81a922) | Sets screen sharing parameters. |


## TRTCCloudCallback @ TXLiteAVSDK

Callback APIs for Tencent Cloud video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa90039556e52de79965ca4d338c83ebf) | Callback for error, which indicates that the SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a2e4c89560e538402907c1aa8fa6b68d1) | Callback for warning. This callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9540be761c1563aa2d8eddb62ccb5578) | Callback of room entry. |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad5ac26478033ea9c0339462c69f9c89e) | Callback of room exit. |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a497f7b16f98dae3e8aa735d7d19df1ff) | Callback of role switching result. |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9bc4aec6ac8593f3171f8ab6b6e91658) | Callback of result of requesting cross-room call (anchor competition). |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6c11aecb5474f578ce0b83e346b14cac) | Callback of result of ending cross-room call (anchor competition). |


### User event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ac917f8d9bfc0ba8fdf86a33baba14149) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7d921af747d72aa87a88ade6a238efc0) | A user exits the current room, which corresponds to `onuserEnterRoom`. |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#af6669bcf5f2fd63ee63fd6d3f6b5823a) | Whether the remote user has playable primary image (generally used for camera). |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) | Whether the remote user has playable secondary image (generally used for screen sharing). |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a166aaaff75287cfbb84f64e0dcab79dc) | Whether the remote user has playable audio data. |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa25eb882b81fd83b1aedf7a4248fd15a) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6c059e46c986cfae0f959cd833a08130) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a266f7551ab47384616b36ad2783615d1) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#acb73daf4ce82cd03f787f057b233b412) | The first local audio frame data has been sent. |
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad236edc28918b6fc28104f69547964ba) | Disused API: an anchor enters the current room. |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ab1d8d76808cf417b6f859f3991b2e8f8) | A user (anchor) exits the current room. |


### Callbacks of statistics on quality and technical metrics

| API | Description |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7a959df0ee5e4d6fa45f0e0785998daf) | Network quality. This callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ab392e7b7325c89a260ce47b1a6b7dde4) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aed43a70b4a95eb95181e2b410013bf54) | The connection between SDK and server has been closed. |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#abeea4e8810cce9a13a4cbb2e020f0da8) | Callback of server speed test. The SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aaa74021e5fd2564afb2df50e25eedeff) | Camera is ready. |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#afdac7dee94451913a4dc9982badc8035) | Mic is ready. |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a04422f826fccefdd91d4ecd42b124686) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a2ce42edc00da08dd4aafa5e1e60927be) | Callback of local device connection and disconnection. |
| [onTestMicVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a199c708ee69b2667e89515d14250de5f) | Callback of test mic volume level. |
| [onTestSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7cc29016572d6aa30f389df92d70c048) | Callback of test speaker volume level. |


### Callbacks of custom message receipt

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad8a3be194ced8ec841e628a285f64703) | Callback of receipt of custom message. |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a19d8b754611731c2c2e321293ba0d9dc) | Callback of loss of custom message. |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aa6b8f609e33400155de150bbf1231121) | Callback of receipt of SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a04ff5d445af7afbe35a68fde8c41b57a) | Callback of starting pushing to Tencent Cloud LVB CDN, which corresponds to the `startPublishing()` API in `TRTCCloud`. |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#acfd26e70f6c71dd1723b42c4be603eb8) | Callback of stopping pushing to Tencent Cloud LVB CDN, which corresponds to the `stopPublishing()` API in `TRTCCloud`. |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#afc7d31fcd57646ec375cc3ddc51b2d6c) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ab491cc44a65e04adb1d5230707e84597) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a77631560b26c7343df3d9bc9a2e0390e) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#abe967d855abae66836877fe0dacf8b5f) | Callback of audio effect playback end. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aca39d43f65ee8d5007ce075d8c808dc1) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a7d15537d26fb001045ff95157d59ed3f) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a9e49f6e6887d63e3e817033681f0ad95) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a399959bd81e349cb76c9b7c939202410) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad0c359a7cefb8f246d498a3fbf52b1ac) | This callback will be returned by the SDK when screen sharing is stopped. |


### Callbacks of background music related events

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a61d9fa641b1790094e955aeb355cca92) | Playback of background music starts. |
| [onPlayBGMProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a6dade9af4a799d8f47fba53c5f1015b6) | Progress of background music playback. |
| [onPlayBGMComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#aff8d7c6c3d2a5984ddd6448008041340) | Playback of background music ends. |


### Callbacks of video data frames for custom processing.

| API | Description |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a183dde7faae6b9c62b0b6d9e8422de65) | Callback of video data for custom rendering. |


### Callbacks of audio data frames for custom processing (read only)

The callback function is thrown synchronously in the internal thread of the SDK; therefore, please do not perform time-consuming operations. 
>?Please define related functions for implementation as needed to reduce unnecessary performance loss.

| API | Description |
|-----|-----|
| [onCapturedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ad207bbc5b8ab7885540fb5a2de1e4d3d) | Callback of audio data captured by local mic. |
| [onPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a0014b81d218cde7372580dd5995a1b24) | Audio data from each remote user before audio mixing, i.e., raw data of each channel before audio mixing. For example, when converting a certain channel of audio to text, you must use the raw audio data of the channel. |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#ac5262e14766154bda8ad437923285567) | Audio data to be played back by speaker after audio data from each channel is mixed. |


### Log related callbacks

| API | Description |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a12a92b897208733ffa67af6fe959611d) | Callback of log printing. |


## Definitions of Key Classes

| Class | Description |
|-----|-----|
| [TRTCImageBuffer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a115d7544222e40e31d1766f7770f4619) | Image buffer. |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a78b6e0861f6c951b7269e5b0e13b8c36) | Screencapturing information. |
| [SIZE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#classManageLiteAV_1_1SIZE) | Buffer length and width. |
| [ITRTCScreenCaptureSourceList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#interfaceManageLiteAV_1_1ITRTCScreenCaptureSourceList) | Screen window list. |
| [ITRTCDeviceCollection](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#interfaceManageLiteAV_1_1ITRTCDeviceCollection) | Device list. |
| [ITRTCDeviceInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#interfaceManageLiteAV_1_1ITRTCDeviceInfo) | Sets `Item` information. |
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | Room entry parameters. |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a43a83bd5122296aa87cc7f6e964921c5) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a7cd5c078b248a32557a85226f1d30697) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#af6aab62536869726ee32b158ddbbf5ce) | Video quality. |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#abdeba26e639757957fd75f528ba14f6e) | Volume level. |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a0f5d7607bc170be903d207b4e0c87fab) | Video frame data. |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a3c9f428bf1fc390b37a9c74accf226c6) | Audio frame data. |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a8858167e09ab4d55f5e49c89bd4a1848) | Network speed test result. |
| [RECT](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a04ac63459343f4b03b918f0496fdde7e) | Records the four point coordinates of rectangle. |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#ac5b1947f21f77726cbff822eaf0003f9) | Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a6066a5537ad8c1bc6158d43e8a4765db) | On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a0b977361cb4d84b1ece0b26c949dcde6) | CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#a724e3aa5cbc2249b7ce31bd7f9362d7b) | Audio recording parameters. |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#ada7b7fc07d775f1a553049e9d6f3f98c) | Sound effect playback. |
| [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#classManageLiteAV_1_1TRTCLocalStatistics) | Local audio/video statistics. |
| [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#classManageLiteAV_1_1TRTCRemoteStatistics) | Remote audio/video statistics. |
| [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__csharp.html#classManageLiteAV_1_1TRTCStatistics) | Statistics. |
