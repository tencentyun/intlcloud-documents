## V2TXLivePlayer

### Video player

For details, please see [V2TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html).
The player pulls audio/video data from the specified live streaming URL and plays the data after decoding and local rendering.
The player has the following capabilities:
- Playing over protocols including RTMP, HTTP-FLV, TRTC, and WebRTC
- Taking screenshots of streamed video
- Delay adjustment. You can set the minimum and maximum cache time for auto adjustment by the player.
- Custom video processing. You can process live video based on your project requirements before rendering and playback.

### Basic SDK APIs

| API | Description |
| -------------------- | ---------------- |
| [setObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#aabeb99813cc5848e3106b64d8de11287) | Sets player callbacks. |


### Basic playback APIs  

| API | Description |
| --------------- | --------------------------- |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a5bf0688f150c9b724a7237e2bcff96cd) | Sets the player’s rendering view. |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a5c186e91db27840ec1ff4c9605248359) | Starts playback. |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a768b1c3893d15ae73d76d1a4c3b29aa6) | Stops playback.                  |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a0bdbaa951f2110e5f7af91be5dfd7c67) | Gets whether playback is ongoing.              |

### Video APIs

| API                                             | Description                                                         |
| --------------------- | -------------------------- |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a953256f3f232eb24e18c54f0d5ef0eaa)     | Sets video rotation. |
| [setRenderFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#ad1674b2b37e210af8a53f3684ac57a28)     | Sets the fill mode.       |
| [pauseVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#af0bf373d9d4c4509aedfd8814e537333)            | Pauses the player’s video.       |
| [resumeVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a1fc6989bb7eb53c6d6953554ceb9e418)           | Resumes the player’s video.       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a7d6e28ab61e78b8185e5ea9713adad59)              | Takes a screenshot of played video. |
| [enableCustomRendering](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#abe456bc3437418e7b250e3ea173eb850) | Sets the callback for custom video rendering.   |

### Audio APIs

| API  | Description       |
| ---------------------- | ---------------------- |
| [pauseAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a8bb9976e8a0d9711a9e17f8888b2aa80)             | Pauses the player’s audio.   |
| [resumeAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a6c34ddc58f1715d905b9864afee7c4b7)            | Resumes the player’s audio.   |
| [setPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a88a48339b54a168c403a22f0b0bd2704)       | Sets the volume.             |
| [enableVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#aeed74080dd72e52b15475a54ca5fd86b) | Enables the volume reminder for playback. |

### Other APIs

| API  | Description       |
| ---------------------- | ---------------------- |
| [setCacheParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#ae439fa2774477dc54b8c27e994d0d42c)             | Sets the minimum and maximum cache time (s) for auto adjustment by the player.   |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__ios.html#a94005f62b788b1030636b51bb5a0210a)            | Sets whether to show the debug view of player status information.   |

## V2TXLivePlayerObserver
Player callbacks
### Basic SDK callback APIs

| API                                             | Description                                                         |
| --------- | --------------- |
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#aeba95a71e4698ea19780de253d3a0099)   | Callback for error. This callback is returned when the player encounters an error. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a6e977d51482a006ad0ce2adc507510a2) | Callback for warning                                 |

### Video callback APIs
| API                                             | Description                                                         |
| --------- | --------------- |
| [onVideoPlayStatusUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a3b0ae3081c30cb1a920d09333813df89)   | Callback for the change of video status |
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a5754eb816b91fd0d0ac1559dd7884dad) | Callback for a screenshot taken                                 |
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a1ee10f163275f3b9316ce387573fcbe1) | Callback for custom video rendering|

### Audio callback APIs
| API                                             | Description                                                         |
| --------- | --------------- |
| [onAudioPlayStatusUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a7a467cced525d22cf1c0e7aeeee90acb)   | Callback for the change of audio status|
| [onPlayoutVolumeUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a5439ba0397be3943c6ebfb6083c27664) | Callback of the player’s volume                       |

### Statistics callback APIs
| API                                             | Description                                                         |
| --------- | --------------- |
| [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a4cdfa0b36d4b9e910c1e0d1b5dc44cde)   | Callback of player statistics |

## V2TXLivePusher

### Stream publisher

For details, please see [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html).

`V2TXLivePusher` encodes local audio/video and publishes the encoded data to a specified URL. It supports any publishing server.
It has the following capabilities:
- Custom video capturing. You can customize audio/video data sources based on your project requirements.
- Retouching, filters, and stickers. `V2TXLivePusher` integrates multiple retouching algorithms (natural & smooth) and color space filters (custom filters are supported).
- QoS control technology. `V2TXLivePusher` can adapt automatically to different upstream network conditions by controlling audio/video traffic in real time based on the network conditions of hosts.
- Facial feature adjustment and animated widgets. Powered by YouTu’s AI facial recognition technology, `V2TXLivePusher` supports animated widgets and fine-tuning of facial features, such as eye enlarging, face slimming, and nose reshaping. You need to purchase a **YouTu license** to use these live streaming effects.

### Basic SDK APIs

| API | Description |
| ----------- | ---------------- |
| [setObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#aa523f8cd2bab159e3723819ab1fe4fe2) | Sets publisher callbacks. |

### Basic publishing APIs

| API                                             | Description                                                         |
| ------------------ | --------------- |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a5bf0688f150c9b724a7237e2bcff96cd)      | Sets the rendering view for local camera preview. |
| [startPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a33b38f236a439e7d848606acb68cc087)          | Starts publishing audio/video data.                                         |
| [stopPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a7332411d6264bc743b0b2bae0b8a73ae)           | Stops publishing audio/video data.                                         |
| [isPushing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a59ba29c9ce1f9dec5c63e6e06b861820)          | Gets whether publishing is ongoing.                                   |

### Video APIs

| API                                             | Description                                                         |
| --------------- | --------------------------------------------------- |
| [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#aa0185a41505a38ad458f9ccf762de4fc) | Sets video encoding parameters for publishing. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a953256f3f232eb24e18c54f0d5ef0eaa) | Sets video rotation for local camera preview.                  |
| [setRenderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#adf4cd57c705a1022d6730fd722f8dab5) | Sets the mirror mode for local camera preview.                            |
| [startCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#aa0b3bda940078de28d0350e9f57910a4)                                                  | Turns the local camera on.                                    |
| [stopCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a082890fe66c00c9b97277a4351c62027) | Turns the local camera off.                                    |
| [startVirtualCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#ada4e34221f16c55efe8f9610042a6647) | Starts image publishing.                  |
| [stopVirtualCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a481f299a96078ba77fbfc1780c0cedb2)  | Stops image publishing.                  |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a9db6d67c2e8dc94c6d9d658366b2dbb2) | Starts screen capturing.                                               |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#ad2fe97c868e0187d82cb44a1204f7f89)  | Stops screen capturing.                                               |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a7d6e28ab61e78b8185e5ea9713adad59) | Takes a screenshot of published video.                          |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#ad48aacbfad38b8f5389c159283fae859)                                                 | Sets watermarks for the publisher. Watermarking is disabled by default.            |
| [setEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#ae4464d33567ce1a31d92530e02a48dd7) | Sets the mirror mode for encoded video.                                  |
|[enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a35e33064526da7f360c786a63d4e33e5) | Enables/Disables custom video capturing. |
|[sendCustomVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a70770d15cc87cf91c174df97cf45a683) |  Sends captured video data to the SDK in the custom video capturing mode. |
|[enableCustomVideoProcess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a36a27d1112103ca70954c72a5d9109ce) | Enables/Disables custom video processing. |
|[sendSeiMessage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a106dc65c2616b80e193aad95876f7fe6) | Sends an SEI message. |

### Beauty filter APIs

| API                                             | Description                                                         |
| --------------- | --------------- |
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a4fb05ae6b5face276ace62558731280a) | Gets the beauty filter management object [TXBeautyManager](https://intl.cloud.tencent.com/document/product/1071/41671), which is used to set beauty filters. |

### Audio APIs

| API | Description |
| --------------- | ---------------------- |
| [startMicrophone](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a368d5e7a2e660dee8e48acb3daa51f24) | Turns the mic on.           |
| [stopMicrophone](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a340ff45f184ca5c08acd4e834a4b78ef) | Turns the mic off.           |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a88956a3ad5e030af7b2f7f46899e5f13) | Sets the quality of published audio.     |
| [enableVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#aeed74080dd72e52b15475a54ca5fd86b) | Enables the volume reminder for capturing. |

### Audio effect APIs
| API                                             | Description                                                         |
| --------------- | ------------------ |
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html) | Gets the audio effect management object. |

### Device management APIs
| API                                             | Description                                                         |
| --------------- | ------------------ |
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__ios.html) | Gets the device management object. |

### Other APIs

| API                                             | Description                                                         |
| --------------- | ------------------------------------- |
| [setProperty](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#aff881e005a44666337a5424c7bf47915) | Calls an advanced API of `V2TXLivePusher`. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a4a4ce2993678b473eb355c1378be2898) | Sets On-Cloud MixTranscoding parameters.              |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a94005f62b788b1030636b51bb5a0210a) | Sets whether to display the dashboard. |


## V2TXLivePusherObserver

### Basic SDK callback APIs

| API                                             | Description                                                         |
| --------------- | --------------- |
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#aab2cdee2c2300208b9505a7e7d30f952) | Callback for error. This callback is returned when the publisher encounters an error. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#ab20068894aa672290b2e9d56c4cb76b2) | Callback for warning                                 |

### Video callback APIs
| API | Description |
| --------------- | ---------------------------------- |
| [onPushStatusUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#a5a976a5846b039ec722725e8203f1147) | Callback of the publisher’s connection status           |
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#a230ab28e6317ba6d440d6a797e218ecb) | Callback for a screenshot taken                         |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#acc0791841b998aecaaf414441af82504) | Callback for custom video processing                   |
| [onGLContextDestroyed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#a764cca49d39e166e8a1849f7ec3c026b) | Callback for destroying the OpenGL context in the SDK |
| [onCaptureFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#af6c3d8ad3f460670aee56187a001f587) | Callback for capturing the first video frame       |

### Audio callback APIs
| API | Description |
| --------------- | ---------------------------- |
| [onCaptureFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html#ad10ac31050e915d349a2a953915cbefe) | Callback for capturing the first audio frame |
| [onMicrophoneVolumeUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#a8a9798da9f593fb00878a823bc3fdbc7) | Callback of mic capturing volume       |

### Mixtranscoding callback APIs
| API                                             | Description                                                         |
| --------------- | ------------------------------ |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a0f11cee9e2659f7ea8484fdffd6b8583) | Callback for setting On-Cloud MixTranscoding parameters |

### Statistics callback APIs
| API                                             | Description                                                         |
| --------------- | ------------------------ |
| [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__ios.html#a4cdfa0b36d4b9e910c1e0d1b5dc44cde) | Callback of publisher statistics |
