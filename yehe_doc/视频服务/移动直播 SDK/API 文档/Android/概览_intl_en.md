## V2TXLivePlayer

### Video player

For details, please see [V2TXLivePlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html).
The player pulls audio/video data from the specified live streaming URL and plays the data after decoding and local rendering.
The player has the following capabilities:
- Playing over protocols including RTMP, HTTP-FLV, TRTC, and WebRTC
- Taking screenshots of streamed video
- Delay adjustment. You can set the minimum and maximum cache time for auto adjustment by the player.
- Custom video processing. You can process live video based on your project requirements before rendering and playback.

### Basic SDK APIs

| API                          | Description   |
| --------------- | ---------------- |
| [setObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#aa851c4bf90929cddfd7067cfdd6049b4) | Sets player callbacks. |

### Basic playback APIs  
| API                          | Description  |
| --------------- | --------------------------- |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#afc848d88fe99790b8c0988b8525dd4d9) | Sets the player’s rendering view `TXCloudVideoView`. |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#af2ac91d628fe510008b3c169896a7e81) | Sets the player’s rendering view `TextureView`. |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a6b8f02711afe98f327743e699632e6ee) | Sets the player’s rendering view `SurfaceView`. |
| [startPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a08f6166ca792b84b76980830f845461d) | Starts playback.            |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a8c4e12608a45f5629dd198ed54d7d2b4) | Stops playback.                  |
| [isPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a69347e1e19d1f96a6c31977f90b8860b) | Gets whether playback is ongoing.              |

### Video APIs

| API                                             | Description                                                         |
| --------------------- | -------------------------- |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#aa08046b0f429f318f36249fa9d0276f2)     | Sets video rotation. |
| [setRenderFillMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#af26f720280c7403e6ca23daf82a57c9a)     | Sets the fill mode.       |
| [pauseVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a0db95f1fb6d448b943400b3149bacff3)            | Pauses the player’s video.       |
| [resumeVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#ac6addf129d35e104ba087ee6a93718d3)           | Resumes the player’s video.       |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a2a507ea1cd894a1635dbfd772802fefd)              | Takes a screenshot of played video. |
| [enableCustomRendering](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a3c31a1de340f63433d486befa6371e7c) | Sets the callback for custom video rendering.   |

### Audio APIs

| API          | Description         |
| ---------------------- | ---------------------- |
| [pauseAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#aa4a006f050968e6d5e9405b40b8e299b)             | Pauses the player’s audio.   |
| [resumeAudio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a4ca6a40a3adba3699caaf1843a81b701)            | Resumes the player’s audio.   |
| [setPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a080762d51e26b2042c6d30de42f59288)       | Sets the volume.             |
| [enableVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#aaa893a96eff34a7ba660441f7597d6d8) | Enables the volume reminder for playback. |

### Other APIs

| API          | Description         |
| ---------------------- | ---------------------- |
| [setCacheParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a8a4f8f8e220a6e4aa2a04ca3e866efcb)             | Sets the minimum and maximum cache time (s) for auto adjustment by the player.   |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#ad3e02a7295f3ba2221fea015f352616b)            | Sets whether to show the debug view of player status information.   |

## V2TXLivePlayerObserver
Player callbacks
### Basic SDK callback APIs

| API       | Description                 |
| --------- | --------------- |
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#af2195d3dbecb37826a101dfe525202c0)   | Callback for error. This callback is returned when the player encounters an error. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a88c8cba39a928dd7964f8f1753bd5bfe) | Callback for warning                                 |
| [onConnected](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#aa511a51b9f4dad03d35cbe08ad616d45) | Callback for successfully connecting to the server    |

### Video callback APIs
| API       | Description                 |
| --------- | --------------- |
| [onVideoResolutionChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a3c69dfdfb02e1a3f3520b1a5a7a6c8e6)   | Callback for change of player resolution|
| [onVideoLoading](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a8a1796d37d96e925a4f2809f73ce8326) | Callback for loading video|
| [onVideoPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a5aaa9225a1d37b8f48ec825af0049945) | Callback for video playback|
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a2ae183e19890e89e216051653ccdfb89) | Callback for a screenshot taken                                 |
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a346a3206ad4d0f38385844c1456a012f) | Callback for custom video rendering|

### Audio callback APIs
| API       | Description                 |
| --------- | --------------- |
| [onAudioLoading](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a9ecbc1b3ff1a907c8110a2b3d00a703a)   | Callback for loading audio|
| [onAudioPlaying](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a00baf0a363714f7eca4baf94400d8a97)   | Callback for audio playback|
| [onPlayoutVolumeUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#a57fc000bf5e935f7253fa94e1750359e) | Callback of the player’s volume                       |

### Statistics callback APIs
| API       | Description                 |
| --------- | --------------- |
| [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#ab10e1f4e22e9bb73e3cea4ae15c36465)   | Callback of player statistics |

## V2TXLivePusher

### Stream publisher

For details, please see [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html).
`V2TXLivePusher` encodes local audio/video and publishes the encoded data to a specified URL. It supports any publishing server.
It has the following capabilities:

- Custom video capturing. You can customize audio/video data sources based on your project requirements.
- Retouching, filters, and stickers. `V2TXLivePusher` integrates multiple retouching algorithms (natural & smooth) and color space filters (custom filters are supported).
- QoS control technology. `V2TXLivePusher` can adapt automatically to different upstream network conditions by controlling audio/video traffic in real time based on the network conditions of hosts.
- Facial feature adjustment and animated widgets. Powered by YouTu’s AI facial recognition technology, `V2TXLivePusher` supports animated widgets and fine-tuning of facial features, such as eye enlarging, face slimming, and nose reshaping. You need to purchase a **YouTu license** to use these live streaming effects.

### Basic SDK APIs

| API                                             | Description                                                         |
| ----------- | ---------------- |
| [setObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ac76cbd3efa4fda66b4b569ec04a5e182) | Sets publisher callbacks. |

### Basic publishing APIs

| API      | Description                         |
| ------------------ | --------------- |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#afc848d88fe99790b8c0988b8525dd4d9)      | Sets the rendering view for local camera preview. |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#af2ac91d628fe510008b3c169896a7e81)      | Sets the rendering view for local camera preview. |
| [setRenderView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a6b8f02711afe98f327743e699632e6ee)      | Sets the rendering view for local camera preview. |
| [startPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ab4f8adaa0616d54d6ed920e49377a08a)          | Starts publishing audio/video data.                                         |
| [stopPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#af07c1dcff91b43a2309665b8663ed530)           | Stops publishing audio/video data.                                         |
| [isPushing](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aa328c59a0cba2e7231cdc8260c675eef)          | Gets whether publishing is ongoing.                                   |

### Video APIs

| API                          | Description                |
| --------------- | --------------------------------------------------- |
| [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ae678ad67285baf08852712abee2e3cc5) | Sets video encoding parameters for publishing. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aa08046b0f429f318f36249fa9d0276f2) | Sets video rotation for local camera preview.                  |
| [setRenderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#afd909d85fd0dda0db4078692b319681f) | Sets the mirror mode for local camera preview.                            |
| [startCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aefa5da30143194b8cf4b4d44b0388809)                                                  | Turns the local camera on.                                    |
| [stopCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aa4bf1dee9de8e4e6b2525ec58568a696) | Turns the local camera off.                                    |
| [startVirtualCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a06bdcdfab3764a18e25e83e62892d610) | Starts image publishing.                  |
| [stopVirtualCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ad29d896264d10ee765b52e53f8726af4)  | Stops image publishing.                  |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#acd14289e3bbf2708f23e61348136d9f9) | Starts screen capturing.                                               |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aab42643520b611c1f14a353d69c4782f)  | Stops screen capturing.                                               |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2a507ea1cd894a1635dbfd772802fefd) | Takes a screenshot of published video.                          |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a4f56a5a937d87e5b1ae6f77c5bab2335)                                                 | Sets watermarks for the publisher. Watermarking is disabled by default.            |
| [setEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ae025945b6f2633d8e3b879a6fe24dd99) | Sets the mirror mode for encoded video.                                  |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a9d945c58c4e0ff24e55aacef1ef3090f) | Enables/Disables custom video capturing.|
| [sendCustomVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a3802124d90bf00434245d2956dad1fe4) | Sends captured video data to the SDK in the custom video capturing mode. |
| [enableCustomVideoProcess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ab3d49118931e09d1d4954674ff8a8102) | Enables/Disables custom video processing.|
| [sendSeiMessage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a5ba3762815f11bf5005f151e06ae0b38) | Sends an SEI message.                                      |


### Beauty filter APIs

| API                          | Description                         |
| --------------- | --------------- |
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html) | Gets the beauty filter management object [TXBeautyManager](https://intl.cloud.tencent.com/document/product/1071/41677), which is used to set beauty filters. |


### Audio APIs

| API                          | Description         |
| --------------- | ---------------------- |
| [startMicrophone](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a26deb222d84392f554a698ef49bc45db) | Turns the mic on.           |
| [stopMicrophone](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a7dbdb37c3f274ce540d6c9b31e2db57f) | Turns the mic off.           |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a1e7830ca4c9ab2abab20b1415cf1d698) | Sets the quality of published audio.     |
| [enableVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aaa893a96eff34a7ba660441f7597d6d8)                                       | Enables the volume reminder for capturing. |

### Audio effect APIs
| API                          | Description     |
| --------------- | ------------------ |
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html) | Gets the audio effect management object. |

### Device management APIs
| API                          | Description     |
| --------------- | ------------------ |
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__android.html) | Gets the device management object. |

### Other APIs

| API                          | Description  |
| --------------- | ------------------------------------- |
| [setProperty](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#aa3c76edc981e68a754d5a450cb85eb43) | Calls an advanced API of `V2TXLivePusher`. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ade16e8f15b9f64e0339012554c1a8f67) | Sets On-Cloud MixTranscoding parameters.              |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ad3e02a7295f3ba2221fea015f352616b) | Sets whether to display the dashboard. |


## V2TXLivePusherObserver

### Basic SDK callback APIs

| API                          | Description                 |
| --------------- | --------------- |
| [onError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#a1c111d2497b029114f3d3ea755fbf9ae) | Callback for error. This callback is returned when the publisher encounters an error. |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#abd54414cbd5d52c096f9cc090cfe1fec) | Callback for warning                                 |

### Video callback APIs
| API                          | Description         |
| --------------- | ---------------------------------- |
| [onPushStatusUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#a430ba5120ee20b0120a952535aa3cdbc) | Callback of the publisher’s connection status           |
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#aa01faf2222f9c945025c4826a26e3a40) | Callback for a screenshot taken                         |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#a42eccd0ebc9aeee6905cea8b035750bf) | Callback for custom video processing                   |
| [onGLContextCreated](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af4a7a3a4e4945bf216d87f81b6926dab) | Callback for creating an OpenGL context in the SDK |
| [onGLContextDestroyed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#a764cca49d39e166e8a1849f7ec3c026b) | Callback for destroying the OpenGL context in the SDK |
| [onCaptureFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af6c3d8ad3f460670aee56187a001f587) | Callback for capturing the first video frame       |

### Audio callback APIs
| API                          | Description   |
| --------------- | ---------------------------- |
| [onCaptureFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#ad10ac31050e915d349a2a953915cbefe) | Callback for capturing the first audio frame |
| [onMicrophoneVolumeUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#a8a9798da9f593fb00878a823bc3fdbc7) | Callback of mic capturing volume       |

### Mixtranscoding callback APIs
| API                          | Description     |
| --------------- | ------------------------------ |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a0f11cee9e2659f7ea8484fdffd6b8583) | Callback for setting On-Cloud MixTranscoding parameters |

### Statistics callback APIs
| API                          | Description           |
| --------------- | ------------------------ |
| [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayerObserver__android.html#ab10e1f4e22e9bb73e3cea4ae15c36465) | Callback of publisher statistics |
