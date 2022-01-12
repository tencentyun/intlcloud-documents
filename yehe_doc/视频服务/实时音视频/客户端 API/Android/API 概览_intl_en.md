### Create Instance And Event Callback
| API | DESC |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac5da416bb06d461c7e1e555e3fd143ee) | Create `TRTCCloud` instance (singleton mode) |
| [destroySharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a69e76ca12b727c7cbcbdda274fc007a2) | Terminate `TRTCCloud` instance (singleton mode)  |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a22fe2f31f2ef62fb3c6cba083dc6c016) | Set TRTC event callback |
| [setListenerHandler](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a48c867145dcc09289f7af41871b4fdd9) | Set the queue that drives the `TRTCCloudDelegate` event callback |

### Room APIs
| API | DESC |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) | Enter room |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) | Exit room |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) | Switch role |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09fbe471def0c1790357fc2b70149784) | Switch room |
| [ConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) | Request cross-room call |
| [DisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af777ac398ac47c8e5649c983fa2053fa) | Exit cross-room call |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) | Set subscription mode (which must be set before room entry for it to take effect) |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3c4a93d24e0ef076168b44cf3545a8d4) | Create room subinstance (for concurrent multi-room listen/watch) |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6dc091ead812c50497c4b4e87e5c2fcf) | Terminate room subinstance |

### CDN APIs
| API | DESC |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c168a9aa35ccd0b24981526425e4730) | Start publishing audio/video streams to Tencent Cloud CSS CDN |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3067efa528fb9ffb8cf7685ce29925d4) | Stop publishing audio/video streams to Tencent Cloud CSS CDN |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41aefb8be652f8f6803020e543acaadc) | Start publishing audio/video streams to non-Tencent Cloud CDN |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0e1e8a1eb1cac3f5e5d4433b4aa21e8e) | Stop publishing audio/video streams to non-Tencent Cloud CDN |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af7cf5544f9b8027e9526c32319a13838) | Set the layout and transcoding parameters of On-Cloud MixTranscoding |

### Video APIs
| API | DESC |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) | Enable the preview image of local camera (mobile) |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae91432ada1767f793c460c7b897b6809) | Update the preview image of local camera |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af6ee50bf2c4c592294061077fc727505) | Stop camera preview |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | Pause/Resume publishing local video stream |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d) | Set placeholder image during local video pause |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | Subscribe to remote user's video stream and bind video rendering control |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9be8a4c5ea4da16fb1ca42e8e258effd) | Update remote user's video rendering control |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | Stop subscribing to remote user's video stream and release rendering control |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) | Stop subscribing to all remote users' video streams and release all rendering resources |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | Pause/Resume subscribing to remote user's video stream |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2d8a7b74068026a85158262cc9aedd66) | Pause/Resume subscribing to all remote users' video streams |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) | Set the encoding parameters of video encoder |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a02631a5e4251657875535c38ab319239) | Set network quality control parameters |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#afe6ea1bf7c959722595356a9b7fc2179) | Set the rendering parameters of local video image |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a069766641cee1aff4844d0beaa18ee13) | Set the rendering mode of remote video image |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272afecae1d291033cb9cd4b1d7b52e0) | Set the direction of image output by video encoder |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a32d9ba3696b305373508253f9bee8236) | Set the mirror mode of image output by encoder |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abbbe1548bfba0bd082a08478ce35e9bc) | Set the adaptation mode of G-sensor |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3a040c5012cf572b9dfabcca87f2cbb7) | Enable dual-channel encoding mode with big and small images |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2a018cc1010587ea9b0fbd791eb3c54f) | Switch the big/small image of specified remote user |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae75285c95fc53651e24fa23c4141093b) | Screencapture video |

### Audio APIs
| API | DESC |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | Enable local audio capturing and publishing |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272bba21d046347ac42d76069ba5972c) | Stop local audio capturing and publishing |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86) | Pause/Resume publishing local audio stream |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) | Pause/Resume playing back remote audio stream |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) | Pause/Resume playing back all remote users' audio streams |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4a3dda74823afa597b42b981257e9e22) | Set audio route |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3dabe4a4e13509cf1bd5b3d58aabaa06) | Set the audio playback volume of remote user |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6af5e2c4819a683042f382688aff41e9) | Set the capturing volume of local audio |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a81037b960fb2b3501b1e8e60f2b5f9f3) | Get the capturing volume of local audio |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b20e1eec637c82190c5264d78d686af) | Set the playback volume of remote audio |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5a1636fa1300b0b4e2829846c36450a2) | Get the playback volume of remote audio |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a43e99323fd5680fd377b95b97f0885c3) | Enable volume reminder |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8b04666d32535637308605d5e15b7220) | Start audio recording |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7d55e5f15d1291afc89f7e1dfe0a25d8) | Stop audio recording |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5d6bf60e9d3051f601988e55106b296c) | Start local media recording |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae982c3c04c0195711ee4e56132522c4b) | Stop local media recording |
| [checkAudioCapabilitySupport](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a225161d0c1028708b4c043653ea0ee4b) | Query whether a certain audio capability is supported (only for Android) |
| [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6d7f5080d804137be1bd3541f533b275) | Set the parallel strategy of remote audio streams |

### Device management APIs
| API | DESC |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae66395bc404d205fcd7fe9082ca85ce9) | Get device management class (TXDeviceManager) |

### Beauty filter and watermark APIs
| API | DESC |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) | Get beauty filter management class (TXBeautyManager) |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1083aaf0441e3d90ce6641d278a97a63) | Add watermark |

### Background music and sound effect APIs
| API | DESC |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) | Get sound effect management class (TXAudioEffectManager) |

### Screen sharing APIs
| API | DESC |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | Start screen sharing |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab6c3014f6f88c775aa91fccea19ce8a4) | Stop screen sharing |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | Pause screen sharing |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e) | Resume screen sharing |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a34d994fbba559994aaf3a1f20420a885) | Set the video encoding parameters of screen sharing (i.e., substream) (for desktop and mobile systems) |

### Custom capturing and rendering APIs
| API | DESC |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | Enable/Disable custom video capturing mode |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | Deliver captured video frames to SDK |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a206b9ce3594aa535b633d4f7c8f97210) | Enable custom audio capturing mode |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a30a542b7d540c8699595a22ca3401f29) | Deliver captured audio data to SDK |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7b7d3707d2ed8e8f1221faf73af49027) | Enable/Disable custom audio track |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a899a1e9d42c9bf9ce1474aec13ac6747) | Mix custom audio track into SDK |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a362490afb9028595635b52d041a2bfb0) | Set the publish volume and playback volume of mixed custom audio track |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b36383129314d70f150c08de182e2b8) | Generate custom capturing timestamp |
| [setLocalVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b565dc8c77df7fb826f0c45d8ad2d85) | Set video data callback for third-party beauty filters |
| [setLocalVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa3cbb7a501c3151d94473965e2538c7a) | Set the callback of custom rendering for local video |
| [setRemoteVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4fca6803d13e4c7ff00dcac2974637e4) | Set the callback of custom rendering for remote video |
| [setAudioFrameListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034b6fce9a517267acd874c243efc575) | Set custom audio data callback |
| [setCapturedRawAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9047b34857b12d85688b3b3f1ca1c3f0) | Set the callback format of original audio frames captured by local mic |
| [setLocalProcessedAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac0f65e13815edc05ebd765826a94e3dc) | Set the callback format of preprocessed local audio frames |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a98a2e38d75366fbc2c4da92fec5c0a30) | Set the callback format of audio frames to be played back by system |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803) | Enabling custom audio playback |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c1c268173ab9b1bc24d34766e433931) | Getting playable audio data |

### Custom message sending APIs
| API | DESC |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa4847ad53acc9ab5990194b21ff5b070) | Use UDP channel to send custom message to all users in room  |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034f9e1effbdadf8b9bfb7f3f06486c4) | Use SEI channel to send custom message to all users in room  |

### Network test APIs
| API | DESC |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6db053500be88a8735bfc69730447912) | Start network speed test (used before room entry) |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3e862cef0e818ddecdc3dc4d66a6f8f9) | Stop network speed test |

### Debugging APIs
| API | DESC |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aeb5168abbd62c631b65247e6289d1e2d) | Get SDK version information |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0ec9520dda7e2062f7455956d093113b) | Set log output level |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2942d9d05045d3f0e0add45a3e10b3ee) | Enable/Disable console log printing |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a495d2122a4098ab371d825c1f0bb90f5) | Enable/Disable local log compression |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a44c20358d08da798e0f15d142c9c3914) | Set local log storage path |
| [setLogListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a299a71f4addb3638c7790de446fbdf37) | Set log callback |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2cdb5d447114534f53bad5bdc48afba) | Display dashboard |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa2014c293033e9ea60aa6ffd525ee2fa) | Set dashboard margin |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f331dd0cfff51ab5a3becf4950a55e) | Call experimental APIs |
| [setNetEnv](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a28ae49c86c5e5ba7e5ad2eae171bde76) | Set TRTC backend cluster (for use by Tencent Cloud R&D team only) |

### Disused APIs
| API | DESC |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab356494d1b7dd924be69b23aa631a85a) | Set mic volume |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) | Set the strength of beauty, brightening, and rosy skin filters |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4ff69ce783f648f23dd737641344ac52) | Set the strength of eye enlarging filter |
| [setFaceSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78a159a2a45d24dbd5722eb73d237e8a) | Set the strength of face slimming filter |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a58bb7ce1fbbc40a50647d64693ac5d41) | Set the strength of chin slimming filter |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a774eb948494cecec024771434ccd9d3c) | Set the strength of chin lengthening/shortening filter |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa14091f0d02330cbd02da5186e9dd874) | Set the strength of face shortening filter |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3f806534b2596d7e29ea0ea6c070b591) | Set the strength of nose slimming filter |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a521a0446d0922d480a1eec4b86f1ecb2) | Set animated sticker |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a066cbf8f4f6c1cd23fe9451b82c5a073) | Mute animated sticker |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a925323ab809957ccaeb4cef30841cb72) | Set color filter |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5fb4c8bc9948e61a75b9ef85f618309d) | Set the strength of color filter |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aef56a36b901d5e525ee539e7d5642063) | Set green screen video |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3df738557f5c658c37174ac9aeae9684) | Start background music |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3ee7bdd15de4ba9010aa5ece3abff0ab) | Stop background music |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a21ddee03e6f4cec028a24e5d5e30955e) | Stop background music |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aaa8b34ef2b334bd22a1cb6541a4c6702) | Stop background music |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae7342a8bcfda22a872aa684f06a4677f) | Get the total length of background music in ms |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78f901b6175352a31b0236776bfdc661) | Set background music playback progress |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ada9c2b4aaf9a1a9ab9cd846593fdf9e6) | Set background music volume |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab1e1c94c9efd967dbffb46d3ba08fef5) | Set the local playback volume of background music |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a535eab48f9df390f4de5ebd5afcd59e3) | Set the remote playback volume of background music |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6f4f89be3c810acfa2430ad65fd7ea68) | Set reverb effect |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37acaf3b2539e0b1c18123a646e91189) | Set voice changing type |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad1ed7667282eccfac1992c1e547a5aeb) | Play sound effect |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | Set sound effect volume |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | Stop sound effect |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a770543c80d3a5629a26d1382535fb6c4) | Stop all sound effects |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9bb41c4ff1a5b24ca742fe3ce45a2bc0) | Set the volume of all sound effects |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab32923d04ce164b82879b3e05833959f) | Pause sound effect |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a33ab6e798d3da245435166464b702d4f) | Pause sound effect |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9306bca7c6a13e0443a3fa1b40c9f343) | Enable or disable in-ear monitoring |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | Start displaying remote video image |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | Stop displaying remote video image and pulling the video data stream of remote user |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) | Set the rendering mode of remote image |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8478d804d2a07520ce2bc5466b727839) | Set the clockwise rotation angle of remote image |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) | Set the rendering mode of local image |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69) | Set the clockwise rotation angle of local image |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1) | Set the mirror mode of local camera's preview image |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#acdbe3829d20f58cedd5a0c2f49ea24dc) | Start displaying the substream image of remote user |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae5f540d795425046c9166b0a2361a8de) | Stop displaying the substream image of remote user |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a73f66e66ffee44e19ebb4d8c56c89718) | Set the fill mode of substream image |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#affdf177b468fdf40a41782e2e47524cc) | Set the clockwise rotation angle of substream image |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2efc2703c86ee009bd4a1d440d0c1e0) | Specify whether to view the big or small image |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55) | Set sound quality |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | Set sound quality |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1b43a65a32f9dcb81b39b9c51c5bc4c6) | Switch camera |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac7ae26eca2f9a673121803d6d175b034) | Query whether the current camera supports zoom |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9f761eebdf04f724e0d1591c41c6045f) | Set camera zoom ratio (focal length) |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a645183ba7c0cea748973796cb38aad8c) | Query whether the device supports flash |
| [enableTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09253f6547914d54058831b61325e770) | Enable/Disable flash |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abd39aca40adfc8da6beaf32141f84cfa) | Query whether the camera supports setting focus |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa7c65fb033727804e7a79b8f135c776c) | Set the focal position of camera |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a23f25ffb81215a32517da78455459ff2) | Query whether the device supports the automatic recognition of face position |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5438dcc45dc2f26a3771a5feddcdef5d) | Setting the system volume type (for mobile OS) |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | Enable custom video capturing mode |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | Deliver captured video data to SDK |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | Start screen sharing |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | Pause/Resume publishing local video stream |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | Pause/Resume subscribing to remote user's video stream |
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6db053500be88a8735bfc69730447912) | Start network speed test (used before room entry) |

### Error and warning events
| API | DESC |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a511d0007e1990e63e853e46ce3f02670) | Error event callback |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9871472ee8195dfc5d0c34fae3294465) | Warning event callback |

### Room event callback
| API | DESC |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) | Whether room entry is successful |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) | Room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6a4b7f39bc5dfb0c5d75ef8802e2e758) | Role switching |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9778a84932f02de9be52ea7513f606c1) | Result of room switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) | Result of requesting cross-room call |
| [onDisConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6f7db4f0aaadad2cdfa822ba0060414c) | Result of ending cross-room call |

### User event callback
| API | DESC |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a891f38e4cdeaf3ff18937726f0269c2c) | A user entered the room |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abfec3607f97823956fad77a7a63dc441) | A user exited the room |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) | A remote user published/unpublished primary stream video |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) | A remote user published/unpublished substream video |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) | A remote user published/unpublished audio |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0c1ccf1bec2d3261e9f11894b32e357e) | The SDK started rendering the first video frame of the local or a remote user |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a3516aaef4cb63e512cd713e4ec96d118) | The SDK started playing the first audio frame of a remote user |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a181788d7441d41022ce014095ee05353) | The first local video frame was published |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#acb73daf4ce82cd03f787f057b233b412) | The first local audio frame was published |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aa75cd2a93cfb096357e2de226ff2ea47) | Change of remote video status |

### Callback of statistics on network and technical metrics
| API | DESC |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b) | Real-time network quality statistics |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a24a6ee3b3709a42af226be7258521612) | Real-time statistics on technical metrics |
| [onSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0dc9967589d6d3277f0e429e520f2c51) | Callback of network speed test |

### Callback of connection to the cloud
| API | DESC |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aed43a70b4a95eb95181e2b410013bf54) | The SDK was disconnected from the cloud |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | The SDK is reconnecting to the cloud |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | The SDK is reconnected to the cloud |

### Callback of hardware events
| API | DESC |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aaa74021e5fd2564afb2df50e25eedeff) | The camera is ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#afdac7dee94451913a4dc9982badc8035) | The mic is ready |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1a608275247d2912e26bd83f648d6378) | The audio route changed (for mobile devices only) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4e3b79968ccbb86de5b79e326a2daafa) | Volume |

### Callback of the receipt of a custom message
| API | DESC |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a51fd654c5ec030ff84f208f2ba50298d) | Receipt of custom message |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a98af11ba5b25d3124bd9533dc5197127) | Loss of custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3640e6bf80a1f93991644701e9b0d96) | Receipt of SEI message |

### CDN event callback
| API | DESC |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a03d0ef687b2973b9b13cb041bd35bb85) | Started publishing to Tencent Cloud CSS CDN |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3cb7e5ceb69954d762eafca5a0e3a62) | Stopped publishing to Tencent Cloud CSS CDN |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a64df36d6c56dd69d8b6f051fd9fffcbc) | Started publishing to non-Tencent Cloud’s live streaming CDN |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c3d63538897ddb9ed1b170819c41dca) | Stopped publishing to non-Tencent Cloud’s live streaming CDN |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af1c79a5ec3e0c106939e7f0d7849d694) | Set the layout and transcoding parameters for On-Cloud MixTranscoding |

### Screen sharing event callback
| API | DESC |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a7d15537d26fb001045ff95157d59ed3f) | Screen sharing started |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a12c57991389e32f04a56774df5d1ce76) | Screen sharing was paused |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ade88963a254d297d3be1993e8a599f6e) | Screen sharing was resumed |
| [onScreenCaptureStopped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c09b21b733da7d314d1db2cb03c8bcb) | Screen sharing stopped |

### Callback of local recording and screenshot events
| API | DESC |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6d252931944577cc08d40db1f5ecd7bb) | Local recording started |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22f09234dc198d33fa38bbb595fb5764) | Local media is being recorded |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0a3eef0daeb5107290cb5190ceb9467b) | Local recording stopped |

### Disused callbacks
| API | DESC |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aff18b3bc5b1e448b21b7614e5716e73e) | An anchor entered the room (disused) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0d1361e52e96b4c7c1a5f1b89f4ef0fb) | An anchor left the room (disused) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abe967d855abae66836877fe0dacf8b5f) | Audio effects ended (disused) |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ab77a0dff287e1642527cd414fc5fe5f5) | Result of server speed testing (disused) |

### Callback of custom video processing
| API | DESC |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a41b44f9b0583bbf56ad9e96065ea825c) | Custom video rendering |
| [onGLContextCreated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af4a7a3a4e4945bf216d87f81b6926dab) | An OpenGL context was created in the SDK. |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22afb08b2a1a18563c7be28c904b166a) | Video processing by third-party beauty filters |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a5f6d5ef01d3cd610959433107f78aa60) | The OpenGL context in the SDK was destroyed |

### Callback of custom audio processing
| API | DESC |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) | Audio data captured by the local mic and pre-processed by the audio module |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46) | Audio data captured by the local mic, pre-processed by the audio module, effect-processed and BGM-mixed |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902) | Audio data of each remote user before audio mixing |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7) | Data mixed from each channel before being submitted to the system for playback |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a96923a9286a88b83d6890f607884ceb3) | Data mixed from all the captured and to-be-played audio in the SDK |

### Other event callbacks
| API | DESC |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a77d78090666e330606b670bf8ce2d854) | Printing of local log |

### Definitions of video enumerated values
| API | DESC |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp01d5e1111c2ba49a53879c343fd484f2) | Video resolution |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp509a1d5f7a44e1d60cf25e4afb640347) | Video aspect ratio mode |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp8f7c7bceb683fdba0c3cb0a4766dd281) | Video stream type |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFillMode) | Video image fill mode |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp9edface2441370ef72f70dd4945ff0f9) | Video image rotation direction |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpde7f16ea7692e7c649e9a16638f48dbe) | Video pixel format |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2c1424df181810edcbd68a9d2cb4adde) | Video data transfer method |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa367a3c86bde4916b80b03acd05ec218) | Video mirror type |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSnapshotSourceType) | Data source of local video screenshot |

### Definitions of network enumerated values
| API | DESC |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa53ec28e9d73b79c701a709f44efbebe) | Use cases |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp32cd3ba884366b8a2d45cad705f28b18) | Role |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp39c937e1be1c70563f58a5a6fdde96a1) | QoS control mode (disused) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp3a953a9777c6e1447a27bc454f9f00b9) | Image quality preference |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp43d6beae8b3d7c79f02df2f125c090a7) | Network quality |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5f5cc2365ee675bbc0f5a14095b1e0fc) | Audio/Video playback status |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp66f48a69ecc92051ca32055008a19c3e) | Reasons for playback status changes |

### Definitions of audio enumerated values
| API | DESC |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2b7efdf7211746ab55166bb4d55ed619) | Audio sample rate |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp96d66d1098694549803eaba6baedb9c0) | Sound quality |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7340a7d82950a691c95bde594a44959f) | Audio route (i.e., audio playback mode) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp30e899d6cb29154e1d73867d199b7191) | Audio reverb mode |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpac19166c196a2905657f2a3b52a68ce0) | Voice changing type |
| [TRTCAudioCapabilityType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp29e12a3869cc165605dc0121e56888a3) | Audio capability type supported by the system (only for Android devices) |

### Definitions of other enumerated values
| API | DESC |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2f4911d8563ae1db783b963d626681d8) | Log level |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7821baad731a6db4d8977d304fafce63) | G-sensor switch (for mobile devices only) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5e2e800d31dc99373db17e2def3afc99) | Layout mode of On-Cloud MixTranscoding |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpaa193560ab798cc5dcdb9624ce9740aa) | Media recording type |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa7e631ba74d7c9f6832a6ad3be7a81af) | Stream mix input type |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp25c9df32061d8ad991f04b21fc6acacb) | Audio recording content type |

### Definitions of core TRTC classes
| API | DESC |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | Room entry parameters |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam) | Video encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCNetworkQosParam) | Network QoS control parameter set |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCRenderParams) | Rendering parameters of video image |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp43d6beae8b3d7c79f02df2f125c090a7) | Network quality |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVolumeInfo) | Volume |
| [TRTCSpeedTestParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestParams) | Network speed testing parameters |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestResult) | Network speed test result |
| [TRTCTexture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCTexture) | Video texture data (for Android only and including texture ID and EGL environment) |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFrame) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrame) | Audio frame data |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ac5b1947f21f77726cbff822eaf0003f9) | Description information of each video image in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a6066a5537ad8c1bc6158d43e8a4765db) | Layout and transcoding parameters of On-Cloud MixTranscoding |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCPublishCDNParam) | Push parameters required to be set when publishing audio/video streams to non-Tencent Cloud CDN |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams) | Local audio file recording parameters |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCLocalRecordingParams) | Local media file recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ad82a59c2209c0596dabaee1152820494) | Sound effect parameter (disused) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a1b79e0e45a5f137df2e1995af7c0885c) | Room switch parameter |
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9b833660fc60bd0b4e0c0625d2ad84f6) | Format parameter of custom audio callback |
| [TRTCScreenShareParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCScreenShareParams) | Screen sharing parameter (for Android only) |

