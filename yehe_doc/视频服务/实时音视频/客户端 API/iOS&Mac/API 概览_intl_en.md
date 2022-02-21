## TRTCCloud @ TXLiteAVSDK

### Instance creation and event callback APIs
| API          | Description         |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) | Creates a `TRTCCloud` instance (singleton). |
| [destroySharedIntance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad8961d03736d8a52df5a3a991d0a77c4) | Terminates a `TRTCCloud` instance (singleton).  |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6a8e20d57b7890e4dbf6652c426d7015) | Sets TRTC event callbacks. |
| [delegateQueue](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a97158c52f2a4011454b4eb3ee369a8a1) | Sets the queue that drives `TRTCCloudDelegate` callbacks. |

### Room APIs
| API          | Description         |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) | Switches roles. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7c5a2aa06d649492f546d9c70a5de4a1) | Switches rooms. |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) | Requests a cross-room call. |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abd656e4c9b6a01231810ae897627e9bc) | Exits a cross-room call. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) | Sets the subscription mode. It must be set before room entry to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6100a5f395442d38ce9adab922382caf) | Creates a sub-room instance (for concurrent playback from multiple rooms). |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a19e0d7921ac494fb588a4654d97abe86) | Terminates a sub-room instance. |

### CDN APIs
| API          | Description         |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6d2f4d81f0944072053d7dc9e9265f22) | Starts publishing audio/video streams to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afc00ba747be5299cd7235928a628339e) | Stops publishing audio/video streams to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aad42e78d355fd563b959a5053bac54cb) | Starts publishing audio/video streams to a non-Tencent Cloud CDN. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | Stops publishing audio/video streams to a non-Tencent Cloud CDN. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) | Sets layout and transcoding parameters for On-Cloud MixTranscoding. |

### Video APIs
| API          | Description         |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | Enables local camera preview (mobile). |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | Enables local camera preview (desktop). |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) | Updates local camera preview. |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | Disables local camera preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | Pauses/Resumes publishing the local video stream. |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2) | Sets the image to display when local video is paused. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | Subscribes to a remote user’s video stream and binds a video rendering control. |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a518d3a8a3b4a4cfd8b5e0dfe7899756b) | Updates a remote user’s video rendering control. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | Unsubscribes from a remote user’s video stream and unbinds the rendering control. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) | Unsubscribes from all remote users’ video streams and unbinds all rendering controls. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | Pauses/Resumes receiving a remote user’s video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adf7cd002366760749c6f4d1ee9291db1) | Pauses/Resumes receiving all remote users’ video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9) | Sets video preference. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5d4f0aba952a355f153d374899e6dcec) | Sets rendering parameters for the local image. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7147d9c93af6a92f594ea394fc796081) | Sets rendering parameters for a remote image. |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) | Sets the rotation of encoded video images. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a29a7cae6b4e82098fc342d4f0066d2ad) | Sets the mirror mode of encoded images. |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7a8c22e2f02d313590d4c499e18ebe3f) | Sets the adaptation mode of the G-sensor. |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2aa9c464203b1c62cbb9ccabccc6334a) | Enables/Disables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a49440df0907b12c0ad8fe9e93bdbed0d) | Switches between the small and big images of a remote user. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | Takes a video screenshot. |

### Audio APIs
| API          | Description         |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | Starts local audio capturing and publishing. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab78601c38f1b872b03b662e6856be84c) | Stops local audio capturing and publishing. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9) | Pauses/Resumes publishing the local audio stream. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) | Pauses/Resumes playing the audio stream of a remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) | Pauses/Resumes playing the audio streams of all remote users. |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa62f2af2d86a64c0ebc7b9f00e4a54fe) | Sets the audio route. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d38580f2c35f7e9828c4e41c56db35a) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5475b81c1712323257c10baaf7ad6969) | Sets the local audio capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7ce26486575e72bc445432929fdff26c) | Gets the local audio capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af2602b1e9dfe932c89dd411f2f227192) | Sets the playback volume of remote audio. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aba445625df38b8676d599df4a67a8407) | Gets the playback volume of remote audio. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57d48cb0dbd7705486453b46e30e3fea) | Enables the volume reminder. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9eadd65cef0ac6b9c04ddfd7265afb01) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac8c12476bbcf3d691060954fcdb6ebe6) | Stops audio recording. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b) | Starts local media recording. |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#affae72630393980fee79c21f2d20f602) | Stops local media recording. |
| [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a02ad0bcebe3962fefee9af07039f0657) | Configures policy for the playback of the audio of multiple remote speakers. |

### Device management APIs
| API          | Description         |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a950f3f1c949def9e1e470f467db7b27a) | Gets the device management class `TXDeviceManager`. |

### Beauty filter and watermark APIs
| API          | Description         |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4fb05ae6b5face276ace62558731280a) | Gets the beauty filter management class `TXBeautyManager`. |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad0bedbddf415d26cff8242d5842a0908) | Adds watermarks. |

### Background music and audio effect APIs
| API          | Description         |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) | Gets the audio effect management class `TXAudioEffectManager`. |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) | Starts system audio capturing (for macOS only). |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adef486f26a2c7d74a8cccb537367e66a) | Stops system audio capturing (for desktop systems only). |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae) | Sets system audio capturing volume. |

### Screen sharing APIs
| API          | Description         |
|-----|-----|
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) | Starts in-application screen sharing (for iOS 13.0 or above). |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) | Starts system-level screen sharing (for iOS 11.0 or above). |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | Starts desktop screen sharing (for desktop systems only). |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6f536bcc3df21b38885809d840698280) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af257a8fb6969fe908ca68a039e6dba15) | Resumes screen sharing. |
| [getScreenCaptureSourcesWithThumbnailSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a37df498cbc8d9b1135e3caafdcee906f) | Enumerates shareable screens and windows (for macOS only). |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) | Selects a screen or window to share (for macOS only). |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) | Sets encoding parameters for screen sharing (substream video). This API works on both desktop and mobile OS. |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a18d3fb6535c9884784c5ad5f8dfd0b12) | Sets audio mixing volume for screen sharing (for desktop systems only). |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa567171999b17a7f5655213b193415a7) | Adds a window to the exclusion list of screen sharing (for desktop systems only). |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a95b1f3fbc6ff755f67f7e9b86240ea5f) | Removes a window from the exclusion list of screen sharing (for desktop systems only). |
| [removeAllExcludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab2b6a778a528d58e2a42c9adfc7684f2) | Removes all windows from the exclusion list of screen sharing (for desktop systems only). |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233) | Adds a window to the screen sharing list (for desktop systems only). |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a058ac1e2141d6eb1962219167add42bc) | Removes a window from the screen sharing list (for desktop systems only). |
| [removeAllIncludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a18a20767a0e1076ba16cd473a2512156) | Removes all windows from the screen sharing list (for desktop systems only). |

### Custom capturing and rendering APIs
| API          | Description         |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | Enables/Disables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | Sends captured video frames to the SDK. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) | Enables/Disables custom audio capturing. |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a62cab4ec7c336ae135c2f681aca25da1) | Sends captured audio data to the SDK. |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1101d883d65882f735e3d17f874a25cb) | Enables/Disables custom audio tracks. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9f408915460e86e889056066ca4e0908) | Mixes a custom audio track into the SDK. |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abd8823c40d31e122ed34f7ac33c678a6) | Sets the publishing and playback volumes of external audio mixed into the published stream. |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) | Gets the PTS for custom capturing. |
| [setLocalVideoProcessDelegete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2f73c33b1010a63bd3a06e639b3cf348) | Sets the callback of video data for the application of third-party beauty filters. |
| [setLocalVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aba3d309645d27304b6d4ea31b21a4cda) | Sets the callback of local video for custom rendering. |
| [setRemoteVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5244e73ac27599370f966575e11959ff) | Sets the callback of a remote video for custom rendering. |
| [setAudioFrameDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01726b03b102c32222a2a26b16abcd48) | Sets the callback of audio data for custom rendering. |
| [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) | Sets the format of the callback of raw audio frames captured by the local mic. |
| [setLocalProcessedAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9ec7c7123eb2f333769508de193ea51f) | Sets the format of the callback of audio frames captured locally and pre-processed by the audio module. |
| [setMixedPlayAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a24ad642b88cd3b2ca2d3044d72817090) | Sets the format of the callback of audio frames played by the system. |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a325da4ec57db06b91b74da8699b47d7c) | Enables/Disables custom audio rendering. |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aeebe3811918c8250d32d872fee83a2c2) | Gets playable audio frames. |

### Custom message sending APIs
| API          | Description         |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acbc86da0cb558c549f42e7e987c7beaf) | Sends a custom message to all users in a room via TRTC’s UDP channel. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6de26e5efddf899d31158e4d48f17c02) | Sends a custom message to all users in a room via TRTC’s SEI channel. |

### Network testing APIs
| API          | Description         |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a914bc4bdd1f0f0e02f27f873acb7e576) | Starts network speed testing. This API must be called before room entry. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a58d732ba648d1f9a3a460c02de79bb9b) | Stops network speed testing. |

### Debugging APIs
| API          | Description         |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ace5acd2fe597b6656b45aaa93e3e45a1) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9d2b6a99e137a9667743edc8ac909493) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a177c4f1fbb2a011ff496417dc0245667) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa51a341a43a854ac6e3fa1d0093fec95) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a93b48089741f7022aea1f8f93ce8fff9) | Sets the path to save local logs. |
| [setLogDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a41497e4242e3c42acfa35730cdc1ddf6) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3bd71c8a99029c1a4708bf1c176aa299) | Sets whether to display the dashboard. |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aad41ff6d5b5565046911acf27bb3dee4) | Sets the dashboard margin. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | Calls the experimental API. |

### Disused APIs
| API          | Description         |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abb57991f5e4f4ca1b95c2181a7e538c8) | Sets the mic volume. |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1336146862fb742de6cbe5718f9b7008) | Sets the strength of the beauty, brightening, and rosy skin filters. |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae0e4341ef565cc5ba28101574179cd56) | Sets the strength of the eye enlarging filter. |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | Sets the strength of the face slimming filter. |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | Sets the strength of the chin slimming filter. |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a145d4ed3d5790a449a9884d282420216) | Sets the strength of the jaw lengthening/shortening filter. |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | Sets the strength of the face shortening filter. |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae94b107a9c476337585906c79b42ee95) | Sets the strength of the nose slimming filter. |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3aa8c561d744e3d921dff6186a6e4ade) | Sets animated stickers. |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | Mutes/Unmutes animated effects. |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | Starts screen sharing. |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) | Sets the color filter. |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3b0d7db70674f961c14b316f4e8e7a2b) | Sets the strength of the color filter. |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | Sets green screen effects. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4d9983591fa2a847e226b7a30e8db294) | Starts background music. |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a11004f1ba27b057985850a25307b0bec) | Stops background music. |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa4b92d4c989e99612f6c4dab03a78764) | Pauses background music. |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aed6e8f224b5f834b1bc0c15f9701f692) | Resumes background music. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac1f96932d02198cd045ee96f1306c8ba) | Gets the total length of the music file, in milliseconds. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7fd043ae358c43f6a178837fb2846ef9) | Sets the playback progress of background music. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adbfc8e226df7c6caaaca1a89a9842f23) | Sets the volume of background music. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a08c468f48d99aef0e89716111db1f422) | Sets the local playback volume of background music. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0cf0c090285038b23843c646009073d1) | Sets the remote playback volume of background music. |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a555cde4eda63d13bbad0dbdba7094a47) | Sets the reverb effect. |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa60f54923826cc59d8a4526669c4ea5e) | Sets the voice changing effect. |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2ae175694198a9b3d1b1647b7ce1dae0) | Plays an audio effect. |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | Sets the volume of an audio effect. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | Stops an audio effect. |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7066509af1de32c290b7cc297cd00f2b) | Stops all audio effects. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6b345c95b5b68198d8dbc64a3652ed35) | Sets the volume of all audio effects. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab0d46ccb8fca811851b30e7731958024) | Pauses an audio effect. |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a207dd8909c05d4a8a1431d33e644d4fe) | Resumes an audio effect. |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa26564f3388bc249ecbd2813d9c45390) | Enables/Disables in-ear monitoring. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | Plays the video of a remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | Stops playing the video of a remote user and pulling the user’s video data. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) | Sets the rendering mode of a remote image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90) | Sets the clockwise rotation of a remote image. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) | Sets the rendering mode of the local image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4d2d95ad8fbaf8edce18667aa835848e) | Sets the clockwise rotation of the local image. |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af68f13fba5a02e4e9ca338596fb64916) | Sets the mirror mode of the local camera's preview image. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) | Starts playing the substream video of a remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acab6e31898857af876af66e779216203) | Stops playing the substream video of a remote user. |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a487b3cd9a6b41581d4b45c752c5ede4c) | Sets the fill mode of the substream video of a remote user. |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a72c66b67eacd24a0e796a3213219fb6d) | Sets the clockwise rotation of the substream video of a remote user. |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2b2d43a3955480f2d6200bf20e66f3cf) | Sets playback preference. |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53) | Sets audio quality. |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | Enables local audio capturing and publishing. |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa9a1952f442020bc92ce1beb65959e56) | Switches cameras. |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8662b8ecab04a55a321ee9f16d0680a7) | Queries whether the current camera supports zoom. |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | Sets the camera zoom factor (focal length). |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd005524f8e2c2fbfcc415049e666ced) | Queries whether the camera supports flash. |
| [enbaleTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af6b128ee01d91a63dc1976db7a9be555) | Enables/Disables flash. |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0e164f727b990581a42f97dca1bf7548) | Queries whether the camera supports focus setting. |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6a77cc99c41b926cd99909ae1ace39ae) | Sets the coordinates of camera focus.|
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5af361145f04227ff1a451fee2705a77) | Queries whether the camera supports automatic facial recognition. |
| [enableAutoFaceFoucs](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a32a8f584879b17f211df75494a5be96c) | Enables/Disables auto focus on face. |
| [startCameraDeviceTestInView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1bd6289b969adde0096c83d6a5532332) | Starts camera testing. |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1b67fa3f322efe538d924b381c06e676) | Stops camera testing. |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa6f467c12fcea7e09cc97861d511498a) | Starts mic testing. |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8cca1c5913ac021987680195075e5fc9) | Stops mic testing. |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a60aa520016687bea03f17cb4ec19c1b6) | Starts speaker testing. |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf383f971dc54f0254b2d40f100cc9ca) | Stops speaker testing. |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5e267aa0d820f78b761be1d485369b3b) | Gets the mic list. |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afa6a82cbf407b0bd6eb63093940e189d) | Gets the mic currently in use. |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) | Sets the mic to use. |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af69d237159163eebcb6876e767d7692e) | Gets the current mic volume. |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aaa6810f64c153e779697dc2d5bd30f6a) | Sets the current mic volume. |
| [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae9c936081b96348ce047337a1d3bb7b0) | Gets whether the current mic is muted. |
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) | Mutes/Unmutes the current mic. |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5b888d0ebe697fdc5e11759f1b154fc3) | Gets the speaker list. |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9d6d48c3937e3cb2632ced9a6a002368) | Gets the speaker currently in use. |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6c951071ac218930680febd84314ee05) | Sets the speaker to use. |
| [getCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa25ac85f6f84b352175aebb9c7007247) | Gets the current speaker volume. |
| [setCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a019001b23569c8b6da7f3276af58e0a7) | Sets the current speaker volume. |
| [getCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a793d11364882c7fac7f9200f8761400c) | Gets whether the current speaker is muted. |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a738ea0dffd48d5bc2b05b146eb79ec46) | Mutes/Unmutes the current speaker. |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0a1b764ff4238afaeaba41ee728a1451) | Gets the camera list. |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa238683cb00f508b05b9ac031a17bc37) | Gets the camera currently in use. |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) | Sets the camera to use. |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab098daa610ae506dbf6c2a4f666ae32c) | Sets the system volume type. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | Takes a video screenshot. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | Enables/Disables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | Sends captured video data to the SDK. |
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791) | Starts in-application screen sharing (for iOS). |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4) | Starts system-level screen sharing (for iOS). |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | Pauses/Resumes publishing the local video stream. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | Pauses/Resumes receiving a remote user’s video stream. |
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a914bc4bdd1f0f0e02f27f873acb7e576) | Starts network speed testing. This API must be called before room entry. |

### Error and warning callback APIs
| API          | Description         |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a10a711eb68abcacc1ca690501fc7c9fb) | Callback for errors |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a25ac0da9ad798a2313bdf8f296828541) | Callback for warnings |

### Room event callback APIs
| API          | Description         |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) | Callback of the result of room entry |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) | Callback for room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ade2c2eab48a30e7ca1c9246e573b7f28) | Callback for role switching |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ad848cbee89f8b6258c9f03f4cb253a31) | Callback for room switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) | Callback of the result of requesting a cross-room call |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a26b34d83afac68928a156096862c9c06) | Callback of the result of ending a cross-room call |

### User event callback APIs
| API          | Description         |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) | Callback for the entry of a user |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) | Callback for the exit of a user |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) | Callback for publishing/unpublishing the primary-stream video by a remote user |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) | Callback for publishing/unpublishing the substream video by a remote user |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) | Callback for publishing/unpublishing audio by a remote user |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7fc7fd0144af2bc4ce0797f9de530d96) | Callback for rendering the first video frame of the local user or a remote user |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aafc4536f552199368e48c8527783c410) | Callback for playing the first audio frame of a remote user |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a17567554f413629a80b5970bdffdff7b) | Callback for sending the first local video frame |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#acb73daf4ce82cd03f787f057b233b412) | Callback for sending the first local audio frame |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af7fef48407b65423871ed6f7652e4176) | Callback for change of the video status of a remote user |

### Callback APIs for statistics on network and technical metrics
| API          | Description         |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28) | Callback of real-time statistics on network quality |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afb0811035e97c8544dbc9ecbef461dd9) | Callback of real-time statistics on technical metrics |
| [onSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6ca73040b7226a8297814694e95478fc) | Callback of network speed testing results |

### Callback APIs for change of connection status
| API          | Description         |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aed43a70b4a95eb95181e2b410013bf54) | Callback for the disconnection of the SDK from the server |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | Callback for the SDK trying to reconnect to the server |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | Callback for the reconnection of the SDK to the server |

### Hardware event callback APIs
| API          | Description         |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aaa74021e5fd2564afb2df50e25eedeff) | Callback for the camera being ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afdac7dee94451913a4dc9982badc8035) | Callback for the mic being ready |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1859305732dfd03de63c9b780f99d513) | Callback for change of the audio route (for mobile devices only) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7775c3fbd84b8da3b7a75bdea27ed5c5) | Callback of volume |
| [onDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a0152908c497bd5ee5225251d9e93e500) | Callback of the connection/disconnection of a local device (for desktop systems only) |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1c36efd81dc4edf88fc3bc6af83b1b5a) | Callback for change of the mic’s system audio capturing volume |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f) | Callback for change of the system’s playback volume |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676) | Callback of whether system audio capturing is enabled successfully (for macOS only) |

### Callback APIs for receiving custom messages
| API          | Description         |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a324311b3d4f3930d9a50b8449b155dd3) | Callback for receiving a custom message |
| [onMissCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af1b8e7d0f73773eca509afc1cf4c9ece) | Callback for losing a custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6e4365456cb4df6e1bdf870511b72042) | Callback for receiving an SEI message |

### CDN event callback APIs
| API          | Description         |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a75c6bf4a7c7ec60a24aabfe8e47ea1f4) | Callback for publishing audio/video streams to Tencent Cloud’s live streaming CDN |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a379dcf84e15f93b64efe2cb9f362877c) | Callback for stopping publishing audio/video streams to Tencent Cloud’s live streaming CDN |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a817783f364bf9f6f0a1df4bc26bad628) | Callback for publishing audio/video streams to a non-Tencent Cloud CDN |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aab032eb48a56e8351ada60ce5b510d5e) | Callback for stopping publishing audio/video streams to a non-Tencent Cloud CDN |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab5c98341b7536b5b65c04b835c4d28fb) | Callback for setting layout and transcoding parameters for On-Cloud MixTranscoding |

### Screen sharing callback APIs
| API          | Description         |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7d15537d26fb001045ff95157d59ed3f) | Callback for starting screen sharing |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a9cc6106085b2049838e21bb50e192786) | Callback for pausing screen sharing |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ae9c08ef9dd260cf6fd946209fda8a011) | Callback for resuming screen sharing |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a323d2b3e5b8b364722e0b161ab11c816) | Callback for stopping screen sharing |

### Callback APIs for local recording and screenshot taking
| API          | Description         |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a044ce179ac4bc0bc987a3b74ecd911e7) | Callback for starting local recording |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab4250c05ea4b843c27385f77d5004fc3) | Callback of the progress of local recording |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ae78ca25acea4152bfd9d0ccf71bd4108) | Callback for ending local recording |

### Disused callback APIs
| API          | Description         |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af26948706dc0dff24946470066e9c4e0) | Callback for the entry of an anchor (disused) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a72f0a872a13500cb5394f77c586ab3f5) | Callback for the exit of an anchor (disused) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#accb36b0eb1d1b72f32cf72617bb1c730) | Callback for ending an audio effect (disused) |

### Callback APIs for custom video
| API          | Description         |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7b43888945a9d12f088ed99a5854e3c1) | Callback of video frames for custom rendering |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8d4f000b4169a64a8a8af15e51e5dd95) | Callback of video frames for processing by third-party beauty filters |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a5f6d5ef01d3cd610959433107f78aa60) | Callback for destroying the OpenGL context in the SDK |

### Callback APIs for custom audio
| API          | Description         |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) | Callback of audio data captured by the local mic and pre-processed by the audio module |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0) | Callback of locally captured audio data that is pre-processed by the audio module, added with audio effects, and mixed with background music |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a) | Callback of the audio data of each remote user before audio mixing |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e) | Callback of data mixed from the audio of each user before playback |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a905748efe966e94ec1212fda14161aee) | Callback of data mixed from all audios in the SDK, including captured and to-be-played audio |

### Other callback APIs
| API          | Description         |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab1364c78a6f31a8c08d0138c4f6e9647) | Callback for printing local logs |

### Definitions of video enumerated values
| API          | Description         |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaa58db9156c82d75257499cb5e0cdf0e5) | Resolution |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gafdfe57c064658b38b78b0fd11e2706c0) | Aspect ratio mode |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1974ff7e5e78b4455925faf74e38f1e8) | Stream type |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1a66aad6fff71205c7a266268e16f55c) | Image fill mode |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gae8bd6b06a2ca5f89f9b3cea393fc6eb9) | Rotation |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga9bafd3233be6cec1b380d469017ed3e6) | Beauty filter (skin smoothing) algorithm |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gabb58c142deac29da242c957f21c963e3) | Pixel format |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga0fce6f58df3d3021696d15eff683ed8b) | Video data transfer method |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga13da9775774c3251999f1e46d279305f) | Mirror mode |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga50f989651c9f893de7716ffbc2d2a5fc) | Source of local screenshots |

### Definitions of network enumerated values
| API          | Description         |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga6ab617b26cf503a8c1bfec34a9918dbe) | Application scenario |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gad147b9b0249d0c2759cf1514c8978881) | Role |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga915f86fec1b00787147d40a189444823) | QoS control mode (disused) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga2c460e7365ad67ee0213545b0a67aa6d) | Video quality preference |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | Network quality |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga0a200753a7e0c539ce4f584cd8d17510) | Video status |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga349e42c3f8a2de5a031e90a1240d7f54) | Reason for change of video status |

### Definitions of audio enumerated values
| API          | Description         |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga346b09a7691ce8c9813bac0feb057d08) | Audio sample rate |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) | Audio quality |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga81305fea3aae73346d04f0013e0194d4) | Audio route (audio playback mode) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) | Reverb effect |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) | Voice changing effect |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaac0cd0da9dd789dcec4ba16471006f23) | System volume type (for mobile devices only) |

### Definitions of other enumerated values
| API          | Description         |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gacefec5143acae6d0524b5500f0155908) | Log level |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga894251078222f9ac4ba5815aac4b493c) | G-sensor mode (for mobile devices only) |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaeabd30a270055e48105a34c781c782b0) | Type of the content to share (for desktop systems only) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga907c7b1ef1f09fb7417a549e82110855) | Layout mode for On-Cloud MixTranscoding |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga4bb9927d377aa27b781fcfef5cf1058a) | Type of media to record |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga9359cd77f4759e5b1a82fe1b94de638d) | Input type for stream mixing |
| [TRTCMediaDeviceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga4a04a7c25ed48ab15603e8c3db115b95) | Device type (for desktop systems only) |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gade0f3fa25d9d1c876660e230152567b0) | Type of audio to record |

### Definitions of TRTC key types
| API          | Description         |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCParams) | Room entry parameters |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCVideoEncParam) | Video encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCNetworkQosParam) | QoS control parameters |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCRenderParams) | Video rendering parameters |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCQualityInfo) | Network quality |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCVolumeInfo) | Volume |
| [TRTCSpeedTestParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestParams) | Network speed testing parameters |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCSpeedTestResult) | Results of network speed testing |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCVideoFrame) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrame) | Audio frame information |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCMixUser) | Information of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCTranscodingConfig) | Layout and transcoding parameters for On-Cloud MixTranscoding |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCPublishCDNParam) | Relaying parameters for publishing audio/video streams to a non-Tencent Cloud CDN |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioRecordingParams) | Local audio recording parameters |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCLocalRecordingParams) | Local media recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioEffectParam) | Audio effect parameters (disused) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCSwitchRoomConfig) | Room switching parameters |
| [TRTCAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCAudioFrameDelegateFormat) | Format of the custom audio callback |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCScreenCaptureSourceInfo) | Information of the content to share (for desktop systems only) |

