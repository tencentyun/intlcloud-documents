### Create Instance And Event Callback
| API | DESC |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab6884975e069628328d05cf0e2c3dc67) | 1.1. Create `TRTCCloud` instance (singleton mode) |
| [destroySharedIntance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad8961d03736d8a52df5a3a991d0a77c4) | 1.2. Terminate `TRTCCloud` instance (singleton mode)  |
| [delegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6a8e20d57b7890e4dbf6652c426d7015) | 1.3. Set TRTC event callback |
| [delegateQueue](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a97158c52f2a4011454b4eb3ee369a8a1) | 1.4. Set the queue that drives the `TRTCCloudDelegate` event callback |

### Room APIs
| API | DESC |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d) | 2.1. Enter room |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a715f5b669ad1d7587ae19733d66954f3) | 2.2. Exit room |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5f4598c59a9c1e66938be9bfbb51589c) | 2.3. Switch role |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7c5a2aa06d649492f546d9c70a5de4a1) | 2.4. Switch room |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a062bc48550b479a6b7c1662836b8c4a5) | 2.5. Request cross-room call |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abd656e4c9b6a01231810ae897627e9bc) | 2.6. Exit cross-room call |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ada2e2155e0e7c3001c6bb6dca1d93048) | 2.7. Set subscription mode (which must be set before room entry for it to take effect) |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6100a5f395442d38ce9adab922382caf) | 2.8. Create room subinstance (for concurrent multi-room listen/watch) |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a19e0d7921ac494fb588a4654d97abe86) | 2.9. Terminate room subinstance |

### CDN APIs
| API | DESC |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6d2f4d81f0944072053d7dc9e9265f22) | 3.1. Start publishing audio/video streams to Tencent Cloud CSS CDN |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afc00ba747be5299cd7235928a628339e) | 3.2. Stop publishing audio/video streams to Tencent Cloud CSS CDN |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aad42e78d355fd563b959a5053bac54cb) | 3.3. Start publishing audio/video streams to non-Tencent Cloud CDN |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5d8a86795b8a2d7eaf9be7157dd9b8dd) | 3.4. Stop publishing audio/video streams to non-Tencent Cloud CDN |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d589d96e548a26c7afb5d1f2361ec93) | 3.5. Set the layout and transcoding parameters of On-Cloud MixTranscoding |

### Video APIs
| API | DESC |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | 4.1. Enable the preview image of local camera (mobile) |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa94bd93a491a7302cc85245c4810a68c) | 4.2. Enable the preview image of local camera (desktop) |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) | 4.3. Update the preview image of local camera |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) | 4.4. Stop camera preview |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | 4.5. Pause/Resume publishing local video stream |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2) | 4.6. Set placeholder image during local video pause |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | 4.7. Subscribe to remote user's video stream and bind video rendering control |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a518d3a8a3b4a4cfd8b5e0dfe7899756b) | 4.8. Update remote user's video rendering control |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | 4.9. Stop subscribing to remote user's video stream and release rendering control |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aaa75cd1b98c226bb7b8a19412b204d2b) | 4.10. Stop subscribing to all remote users' video streams and release all rendering resources |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | 4.11. Pause/Resume subscribing to remote user's video stream |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adf7cd002366760749c6f4d1ee9291db1) | 4.12. Pause/Resume subscribing to all remote users' video streams |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57938e5b62303d705da2ceecf119d74e) | 4.13. Set the encoding parameters of video encoder |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac72a8a85131cb7716b1eec799250aba9) | 4.14. Set network quality control parameters |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5d4f0aba952a355f153d374899e6dcec) | 4.15. Set the rendering parameters of local video image |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7147d9c93af6a92f594ea394fc796081) | 4.16. Set the rendering mode of remote video image |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) | 4.17. Set the direction of image output by video encoder |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a29a7cae6b4e82098fc342d4f0066d2ad) | 4.18. Set the mirror mode of image output by encoder |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7a8c22e2f02d313590d4c499e18ebe3f) | 4.19. Set the adaptation mode of G-sensor |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2aa9c464203b1c62cbb9ccabccc6334a) | 4.20. Enable dual-channel encoding mode with big and small images |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a49440df0907b12c0ad8fe9e93bdbed0d) | 4.21. Switch the big/small image of specified remote user |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | 4.22. Screencapture video |

### Audio APIs
| API | DESC |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | 5.1. Enable local audio capturing and publishing |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab78601c38f1b872b03b662e6856be84c) | 5.2. Stop local audio capturing and publishing |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4ada386a75d8042a432da05fde5552d9) | 5.3. Pause/Resume publishing local audio stream |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afede3cc79a8d68994857b410fb5572d2) | 5.4. Pause/Resume playing back remote audio stream |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a75148bf8a322c852965fe774cbc7dd14) | 5.5. Pause/Resume playing back all remote users' audio streams |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa62f2af2d86a64c0ebc7b9f00e4a54fe) | 5.6. Set audio route |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8d38580f2c35f7e9828c4e41c56db35a) | 5.7. Set the audio playback volume of remote user |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5475b81c1712323257c10baaf7ad6969) | 5.8. Set the capturing volume of local audio |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7ce26486575e72bc445432929fdff26c) | 5.9. Get the capturing volume of local audio |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af2602b1e9dfe932c89dd411f2f227192) | 5.10. Set the playback volume of remote audio |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aba445625df38b8676d599df4a67a8407) | 5.11. Get the playback volume of remote audio |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a57d48cb0dbd7705486453b46e30e3fea) | 5.12. Enable volume reminder |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9eadd65cef0ac6b9c04ddfd7265afb01) | 5.13. Start audio recording |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac8c12476bbcf3d691060954fcdb6ebe6) | 5.14. Stop audio recording |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b) | 5.15. Start local media recording |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#affae72630393980fee79c21f2d20f602) | 5.16. Stop local media recording |

### Device management APIs
| API | DESC |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a950f3f1c949def9e1e470f467db7b27a) | 6.1. Get device management class (TXDeviceManager) |

### Beauty filter and watermark APIs
| API | DESC |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a950f3f1c949def9e1e470f467db7b27a) | 7.1. Get beauty filter management class (TXBeautyManager) |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ad0bedbddf415d26cff8242d5842a0908) | 7.2. Add watermark |

### Background music and sound effect APIs
| API | DESC |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) | 8.1. Get sound effect management class (TXAudioEffectManager) |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486) | 8.2. Enable system audio capturing (for desktop systems only) |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adef486f26a2c7d74a8cccb537367e66a) | 8.3. Stop system audio capturing (for desktop systems only) |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae) | 8.4. Set the volume of system audio capturing (for desktop systems only) |

### Screen sharing APIs
| API | DESC |
|-----|-----|
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7e331c1533895d6c559ccf04ff7035de) | 9.1. Start in-app screen sharing (for iOS 13.0 and above only) |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a78a8da8c2f235446d03cd2db26f97b60) | 9.1. Start system-level screen sharing (for iOS 11.0 and above only) |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | 9.1. Start desktop screen sharing (for desktop systems only) |
| [stopScreenCapture] | 9.2. Stop screen sharing |
| [pauseScreenCapture] | 9.3. Pause screen sharing |
| [pauseScreenCapture] | 9.4. Resume screen sharing |
| [getScreenCaptureSourcesWithThumbnailSize](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a37df498cbc8d9b1135e3caafdcee906f) | 9.5. Enumerate shareable screens and windows (for macOS only) |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01ead6fb3106ea266caa922f5901bf18) | 9.6. Select the screen or window to share (for macOS only) |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abc0f3cd5c320d0e65163bd07c3c0a735) | 9.7. Set the video encoding parameters of screen sharing (i.e., substream) (for desktop systems only) |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a18d3fb6535c9884784c5ad5f8dfd0b12) | 9.8. Set the audio mixing volume of screen sharing (for desktop systems only) |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa567171999b17a7f5655213b193415a7) | 9.9. Add specified windows to the exclusion list of screen sharing (for desktop systems only) |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a95b1f3fbc6ff755f67f7e9b86240ea5f) | 9.10. Remove specified windows from the exclusion list of screen sharing (for desktop systems only) |
| [removeAllExcludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab2b6a778a528d58e2a42c9adfc7684f2) | 9.11. Remove all windows from the exclusion list of screen sharing (for desktop systems only) |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233) | 9.12. Add specified windows to the inclusion list of screen sharing (for desktop systems only) |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a058ac1e2141d6eb1962219167add42bc) | 9.13. Remove specified windows from the inclusion list of screen sharing (for desktop systems only) |
| [removeAllIncludedShareWindows](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a18a20767a0e1076ba16cd473a2512156) | 9.14. Remove all windows from the inclusion list of screen sharing (for desktop systems only) |

### Custom capturing and rendering APIs
| API | DESC |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | 10.1. Enable/Disable custom video capturing mode |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | 10.2. Deliver captured video frames to SDK |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) | 10.3. Enable custom audio capturing mode |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a62cab4ec7c336ae135c2f681aca25da1) | 10.4. Deliver captured audio data to SDK |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1101d883d65882f735e3d17f874a25cb) | 10.5. Enable/Disable custom audio track |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9f408915460e86e889056066ca4e0908) | 10.6. Mix custom audio track into SDK |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) | 10.7. Generate custom capturing timestamp |
| [setLocalVideoProcessDelegete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2f73c33b1010a63bd3a06e639b3cf348) | 10.8. Set video data callback for third-party beauty filters |
| [setLocalVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aba3d309645d27304b6d4ea31b21a4cda) | 10.9. Set the callback of custom rendering for local video |
| [setRemoteVideoRenderDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5244e73ac27599370f966575e11959ff) | 10.10. Set the callback of custom rendering for remote video |
| [setAudioFrameDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a01726b03b102c32222a2a26b16abcd48) | 10.11. Set custom audio data callback |
| [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) | 10.12. Set the callback format of original audio frames captured by local mic |
| [setLocalProcessedAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9ec7c7123eb2f333769508de193ea51f) | 10.13. Set the callback format of preprocessed local audio frames |
| [setMixedPlayAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a24ad642b88cd3b2ca2d3044d72817090) | 10.14. Set the callback format of audio frames to be played back by system |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a325da4ec57db06b91b74da8699b47d7c) | Enabling custom audio playback |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aeebe3811918c8250d32d872fee83a2c2) | Getting playable audio data |

### Custom message sending APIs
| API | DESC |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acbc86da0cb558c549f42e7e987c7beaf) | 11.1. Use UDP channel to send custom message to all users in room  |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6de26e5efddf899d31158e4d48f17c02) | 11.2. Use SEI channel to send custom message to all users in room  |

### Network test APIs
| API | DESC |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a058556b224315dcde3601ab621a09dee) | 12.1. Start network speed test (used before room entry) |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a58d732ba648d1f9a3a460c02de79bb9b) | 12.2. Stop network speed test |

### Debugging APIs
| API | DESC |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ace5acd2fe597b6656b45aaa93e3e45a1) | 13.1. Get SDK version information |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9d2b6a99e137a9667743edc8ac909493) | 13.2. Set log output level |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a177c4f1fbb2a011ff496417dc0245667) | 13.3. Enable/Disable console log printing |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa51a341a43a854ac6e3fa1d0093fec95) | 13.4. Enable/Disable local log compression |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a93b48089741f7022aea1f8f93ce8fff9) | 13.5. Set local log storage path |
| [setLogDelegate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a41497e4242e3c42acfa35730cdc1ddf6) | 13.6. Set log callback |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3bd71c8a99029c1a4708bf1c176aa299) | 13.7. Display dashboard |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aad41ff6d5b5565046911acf27bb3dee4) | 13.8. Set dashboard margin |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a16c53e91f9b32aaf4bf3d409a3790ef6) | 13.9. Call experimental APIs |

### Disused APIs
| API | DESC |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abb57991f5e4f4ca1b95c2181a7e538c8) | Set mic volume |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1336146862fb742de6cbe5718f9b7008) | Set the strength of beauty, brightening, and rosy skin filters |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae0e4341ef565cc5ba28101574179cd56) | Set the strength of eye enlarging filter |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | Set the strength of face slimming filter |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | Set the strength of chin slimming filter |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a145d4ed3d5790a449a9884d282420216) | Set the strength of chin lengthening/shortening filter |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | Set the strength of face shortening filter |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae94b107a9c476337585906c79b42ee95) | Set the strength of nose slimming filter |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3aa8c561d744e3d921dff6186a6e4ade) | Set animated sticker |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | Mute animated sticker |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a59b16baa51d86cc0465dc6edd3cbfc97) | Start screen sharing |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1b0c2a9e82a408881281c7468a74f2c0) | Set color filter |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a3b0d7db70674f961c14b316f4e8e7a2b) | Set the strength of color filter |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | Set green screen video |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4d9983591fa2a847e226b7a30e8db294) | Start background music |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a11004f1ba27b057985850a25307b0bec) | Stop background music |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa4b92d4c989e99612f6c4dab03a78764) | Stop background music |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aed6e8f224b5f834b1bc0c15f9701f692) | Stop background music |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac1f96932d02198cd045ee96f1306c8ba) | Get the total length of background music in ms |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7fd043ae358c43f6a178837fb2846ef9) | Set background music playback progress |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#adbfc8e226df7c6caaaca1a89a9842f23) | Set background music volume |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a08c468f48d99aef0e89716111db1f422) | Set the local playback volume of background music |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0cf0c090285038b23843c646009073d1) | Set the remote playback volume of background music |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a555cde4eda63d13bbad0dbdba7094a47) | Set reverb effect |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa60f54923826cc59d8a4526669c4ea5e) | Set voice changing type |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2ae175694198a9b3d1b1647b7ce1dae0) | Play sound effect |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | Set sound effect volume |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a22854b4e9f698cceb1bbb7f7de466ec1) | Stop sound effect |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7066509af1de32c290b7cc297cd00f2b) | Stop all sound effects |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6b345c95b5b68198d8dbc64a3652ed35) | Set the volume of all sound effects |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab0d46ccb8fca811851b30e7731958024) | Pause sound effect |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a207dd8909c05d4a8a1431d33e644d4fe) | Pause sound effect |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa26564f3388bc249ecbd2813d9c45390) | Enable or disable in-ear monitoring |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5ef41fa3d7f5e88f638747325a0b9fa1) | Start displaying remote video image |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a07b8d05d93d2ef7d543772bff6d451a5) | Stop displaying remote video image and pulling the video data stream of remote user |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afda6658d1bf7dc9bc1445838b95d21ff) | Set the rendering mode of remote image |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2ef26a9ede0ba4fa6c5739229e1eee90) | Set the clockwise rotation angle of remote image |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a961596f832657bfca81fd675878a2d15) | Set the rendering mode of local image |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a4d2d95ad8fbaf8edce18667aa835848e) | Set the clockwise rotation angle of local image |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af68f13fba5a02e4e9ca338596fb64916) | Set the mirror mode of local camera's preview image |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a68d048ccd0d018995e33e9e714e14474) | Start displaying the substream image of remote user |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acab6e31898857af876af66e779216203) | Stop displaying the substream image of remote user |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a487b3cd9a6b41581d4b45c752c5ede4c) | Set the fill mode of substream image |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a72c66b67eacd24a0e796a3213219fb6d) | Set the clockwise rotation angle of substream image |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2b2d43a3955480f2d6200bf20e66f3cf) | Specify whether to view the big or small image |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a2cdffa1529fcaec866404f4f9b92ec53) | Set sound quality |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd85c726c425eda7cac82cba0f83a465) | Set sound quality |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa9a1952f442020bc92ce1beb65959e56) | Switch camera |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8662b8ecab04a55a321ee9f16d0680a7) | Query whether the current camera supports zoom |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | Set camera zoom ratio (focal length) |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#acd005524f8e2c2fbfcc415049e666ced) | Query whether the device supports flash |
| [enbaleTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af6b128ee01d91a63dc1976db7a9be555) | Enable/Disable flash |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0e164f727b990581a42f97dca1bf7548) | Query whether the camera supports setting focus |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6a77cc99c41b926cd99909ae1ace39ae) | Set the focal position of camera |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5af361145f04227ff1a451fee2705a77) | Query whether the device supports the automatic recognition of face position |
| [enableAutoFaceFoucs](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a32a8f584879b17f211df75494a5be96c) | Enable/Disable face auto focus |
| [startCameraDeviceTestInView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1bd6289b969adde0096c83d6a5532332) | Start camera test |
| [stopCameraDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a1b67fa3f322efe538d924b381c06e676) | Start camera test |
| [startMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa6f467c12fcea7e09cc97861d511498a) | Start mic test |
| [stopMicDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a8cca1c5913ac021987680195075e5fc9) | Start mic test |
| [startSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a60aa520016687bea03f17cb4ec19c1b6) | Start speaker test |
| [stopSpeakerDeviceTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#abf383f971dc54f0254b2d40f100cc9ca) | Stop speaker test |
| [getMicDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5e267aa0d820f78b761be1d485369b3b) | Get the list of mics |
| [getCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#afa6a82cbf407b0bd6eb63093940e189d) | Get the current mic device |
| [setCurrentMicDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5141fec83e7f071e913bfc539c193ac6) | Select the currently used mic |
| [getCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af69d237159163eebcb6876e767d7692e) | Get the current mic volume |
| [setCurrentMicDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aaa6810f64c153e779697dc2d5bd30f6a) | Set the current mic volume |
| [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae9c936081b96348ce047337a1d3bb7b0) | Get the mute status of the current system mic |
| [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) | Set the mute status of the current system mic |
| [getSpeakerDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5b888d0ebe697fdc5e11759f1b154fc3) | Get the list of speakers |
| [getCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a9d6d48c3937e3cb2632ced9a6a002368) | Get the currently used speaker |
| [setCurrentSpeakerDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a6c951071ac218930680febd84314ee05) | Set the speaker to use |
| [getCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa25ac85f6f84b352175aebb9c7007247) | Get the current speaker volume |
| [setCurrentSpeakerDeviceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a019001b23569c8b6da7f3276af58e0a7) | Set the current speaker volume |
| [getCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a793d11364882c7fac7f9200f8761400c) | Get the mute status of the current system speaker |
| [setCurrentSpeakerDeviceMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a738ea0dffd48d5bc2b05b146eb79ec46) | Set whether to mute the current system speaker |
| [getCameraDevicesList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a0a1b764ff4238afaeaba41ee728a1451) | Get the list of cameras |
| [getCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aa238683cb00f508b05b9ac031a17bc37) | Get the currently used camera |
| [setCurrentCameraDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#aae9955bb39985586f7faba841d2692fc) | Set the camera to be used currently |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ab098daa610ae506dbf6c2a4f666ae32c) | Setting the system volume type (for mobile OS) |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac0db9a4bcb61e3b369740a1986683cdf) | Screencapture video |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#af53f530fe2025d72e2479928dd6db52f) | Enable custom video capturing mode |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a5a68c4f0cd3a79100b331fc17d4b2858) | Deliver captured video data to SDK |
| [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a7e331c1533895d6c559ccf04ff7035de) | tart in-app screen sharing (for iOS 13.0 and above only) |
| [startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#a78a8da8c2f235446d03cd2db26f97b60) | Start system-level screen sharing (for iOS 11.0 and above only) |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ac3a158f935a99abd4965d308c0f88977) | Pause/Resume publishing local video stream |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__ios.html#ae5b271bc92a7a4d8ffbcbd4c2e509305) | Pause/Resume subscribing to remote user's video stream |

### Error and warning events
| API | DESC |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a10a711eb68abcacc1ca690501fc7c9fb) | Error event callback |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a25ac0da9ad798a2313bdf8f296828541) | Warning event callback |

### Room event callback
| API | DESC |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6960aca54e2eda0f424f4f915908a3c5) | Whether room entry is successful |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6a98fcaac43fa754cf9dd80454897bea) | Room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ade2c2eab48a30e7ca1c9246e573b7f28) | Role switching |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ad848cbee89f8b6258c9f03f4cb253a31) | Result of room switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a69e5b1d59857956f736c204fe765ea9a) | Result of requesting cross-room call |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a26b34d83afac68928a156096862c9c06) | Result of ending cross-room call |

### User event callback
| API | DESC |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58) | A user entered the room |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) | A user exited the room |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) | A remote user published/unpublished primary stream video |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ac45fb0751f7dbd2466a35c8828c9911b) | A remote user published/unpublished substream video |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8c885eeb269fc3d2e085a5711d4431d5) | A remote user published/unpublished audio |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7fc7fd0144af2bc4ce0797f9de530d96) | The SDK started rendering the first video frame of the local or a remote user |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aafc4536f552199368e48c8527783c410) | The SDK started playing the first audio frame of a remote user |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a17567554f413629a80b5970bdffdff7b) | The first local video frame was published |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#acb73daf4ce82cd03f787f057b233b412) | The first local audio frame was published |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af7fef48407b65423871ed6f7652e4176) | Change of remote video status |

### Callback of statistics on network and technical metrics
| API | DESC |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a723002319845fbfc03db501aa9da6c28) | Real-time network quality statistics |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afb0811035e97c8544dbc9ecbef461dd9) | Real-time statistics on technical metrics |

### Callback of connection to the cloud
| API | DESC |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aed43a70b4a95eb95181e2b410013bf54) | The SDK was disconnected from the cloud |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | The SDK is reconnecting to the cloud |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | The SDK is reconnected to the cloud |

### Callback of hardware events
| API | DESC |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aaa74021e5fd2564afb2df50e25eedeff) | The camera is ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afdac7dee94451913a4dc9982badc8035) | The mic is ready |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1859305732dfd03de63c9b780f99d513) | The audio route changed (for mobile devices only) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7775c3fbd84b8da3b7a75bdea27ed5c5) | Volume |
| [onDevice](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a0152908c497bd5ee5225251d9e93e500) | The status of a local device changed (for desktop OS only) |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a1c36efd81dc4edf88fc3bc6af83b1b5a) | The capturing volume of the mic changed |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f) | The playback volume changed |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8644f5136138d13ffa8e0ea68f5c3676) | Whether system audio capturing is enabled successfully (for macOS only) |

### Callback of the receipt of a custom message
| API | DESC |
|-----|-----|
| [onRecvCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a324311b3d4f3930d9a50b8449b155dd3) | Receipt of custom message |
| [onMissCustomCmdMsgUserId](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af1b8e7d0f73773eca509afc1cf4c9ece) | Loss of custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a6e4365456cb4df6e1bdf870511b72042) | Receipt of SEI message |

### CDN event callback
| API | DESC |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a75c6bf4a7c7ec60a24aabfe8e47ea1f4) | Started publishing to Tencent Cloud CSS CDN |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a379dcf84e15f93b64efe2cb9f362877c) | Stopped publishing to Tencent Cloud CSS CDN |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a817783f364bf9f6f0a1df4bc26bad628) | Started publishing to non-Tencent Cloud’s live streaming CDN |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aab032eb48a56e8351ada60ce5b510d5e) | Stopped publishing to non-Tencent Cloud’s live streaming CDN |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab5c98341b7536b5b65c04b835c4d28fb) | Set the layout and transcoding parameters for On-Cloud MixTranscoding |

### Screen sharing event callback
| API | DESC |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7d15537d26fb001045ff95157d59ed3f) | Screen sharing started |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a9cc6106085b2049838e21bb50e192786) | Screen sharing was paused |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ae9c08ef9dd260cf6fd946209fda8a011) | Screen sharing was resumed |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a323d2b3e5b8b364722e0b161ab11c816) | Screen sharing stopped |

### Callback of local recording and screenshot events
| API | DESC |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a044ce179ac4bc0bc987a3b74ecd911e7) | Local recording started |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab4250c05ea4b843c27385f77d5004fc3) | Local media is being recorded |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ae78ca25acea4152bfd9d0ccf71bd4108) | Local recording stopped |

### Disused callbacks
| API | DESC |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#af26948706dc0dff24946470066e9c4e0) | An anchor entered the room (disused) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a72f0a872a13500cb5394f77c586ab3f5) | An anchor left the room (disused) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#accb36b0eb1d1b72f32cf72617bb1c730) | Audio effects ended (disused) |

### Callback of custom video processing
| API | DESC |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a7b43888945a9d12f088ed99a5854e3c1) | Custom video rendering |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a8d4f000b4169a64a8a8af15e51e5dd95) | Video processing by third-party beauty filters |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a5f6d5ef01d3cd610959433107f78aa60) | The OpenGL context in the SDK was destroyed |

### Callback of custom audio processing
| API | DESC |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) | Raw audio data captured locally |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0) | Audio data captured by the local mic and pre-processed by the audio module |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a) | Audio data of each remote user before audio mixing |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e) | Data mixed from each channel before being submitted to the system for playback |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a905748efe966e94ec1212fda14161aee) | Data mixed from all the captured and to-be-played audio in the SDK |

### Other event callbacks
| API | DESC |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#ab1364c78a6f31a8c08d0138c4f6e9647) | Printing of local log |

### Definitions of video enumerated values
| API | DESC |
|-----|-----|
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gafdfe57c064658b38b78b0fd11e2706c0) | Video aspect ratio mode |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1974ff7e5e78b4455925faf74e38f1e8) | Video stream type |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1a66aad6fff71205c7a266268e16f55c) | Video image fill mode |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gae8bd6b06a2ca5f89f9b3cea393fc6eb9) | Video image rotation direction |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gabb58c142deac29da242c957f21c963e3) | Video pixel format |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga0fce6f58df3d3021696d15eff683ed8b) | Video data transfer method |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga13da9775774c3251999f1e46d279305f) | Video mirror type |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga50f989651c9f893de7716ffbc2d2a5fc) | Data source of local video screenshot |

### Definitions of network enumerated values
| API | DESC |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga6ab617b26cf503a8c1bfec34a9918dbe) | Use cases |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gad147b9b0249d0c2759cf1514c8978881) | Role |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga915f86fec1b00787147d40a189444823) | QoS control mode (disused) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga2c460e7365ad67ee0213545b0a67aa6d) | Image quality preference |
| [TRTCQualityInfo] | Network quality |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga0a200753a7e0c539ce4f584cd8d17510) | Audio/Video playback status |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga349e42c3f8a2de5a031e90a1240d7f54) | Reasons for playback status changes |

### Definitions of audio enumerated values
| API | DESC |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga346b09a7691ce8c9813bac0feb057d08) | Audio sample rate |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) | Sound quality |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga81305fea3aae73346d04f0013e0194d4) | Audio route (i.e., audio playback mode) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga1c0a768f9f7855e87c486617816c7759) | Audio reverb mode |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gaeb48457146f2279c912e345ce532ecef) | Voice changing type |

### Definitions of other enumerated values
| API | DESC |
|-----|-----|
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga894251078222f9ac4ba5815aac4b493c) | G-sensor switch (for mobile devices only) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga907c7b1ef1f09fb7417a549e82110855) | Layout mode of On-Cloud MixTranscoding |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga4bb9927d377aa27b781fcfef5cf1058a) | Media recording type |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga9359cd77f4759e5b1a82fe1b94de638d) | Stream mix input type |
| [TRTCMediaDeviceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#ga4a04a7c25ed48ab15603e8c3db115b95) | Device type (for desktop platforms only) |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#gade0f3fa25d9d1c876660e230152567b0) | Audio recording content type |

### Definitions of core TRTC classes
| API | DESC |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Room entry parameters |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Video encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Network QoS control parameter set |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Rendering parameters of video image |
| [TRTCQualityInfo] | Network quality |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Volume |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Network speed test result |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Audio frame data |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interfaceTRTCMixUser) | Description information of each video image in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Layout and transcoding parameters of On-Cloud MixTranscoding |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Push parameters required to be set when publishing audio/video streams to non-Tencent Cloud CDN |
| [TRTCAudioRecordingParams] | Local audio file recording parameters |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Local media file recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__ios.html#interface) | Sound effect parameter (disused) |

