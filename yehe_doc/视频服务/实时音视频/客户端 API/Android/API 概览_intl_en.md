## TRTCCloud @ TXLiteAVSDK

### Instance creation and event callback APIs
| API          | Description         |
|-----|-----|
| [sharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac5da416bb06d461c7e1e555e3fd143ee) | Creates a `TRTCCloud` instance (singleton). |
| [destroySharedInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a69e76ca12b727c7cbcbdda274fc007a2) | Terminates a `TRTCCloud` instance (singleton).  |
| [setListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a22fe2f31f2ef62fb3c6cba083dc6c016) | Sets a TRTC event listener. |
| [setListenerHandler](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a48c867145dcc09289f7af41871b4fdd9) | Sets the queue that drives `TRTCCloudDelegate` callbacks. |

### Room APIs
| API          | Description         |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41d16a97a9cb8f16ef92f5ef5bfebee1) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a915a4b3abca0e41f057022a4587faf66) | Switches roles. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09fbe471def0c1790357fc2b70149784) | Switches rooms. |
| [ConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac1ab7e4a017b99bb91d89ce1b0fac5fd) | Requests a cross-room call. |
| [DisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af777ac398ac47c8e5649c983fa2053fa) | Exits a cross-room call. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b8d004665d5003ce1d9a48a9ab551b3) | Sets the subscription mode. It must be set before room entry to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3c4a93d24e0ef076168b44cf3545a8d4) | Creates a sub-room instance (for concurrent playback from multiple rooms). |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6dc091ead812c50497c4b4e87e5c2fcf) | Terminates a sub-room instance. |

### CDN APIs
| API          | Description         |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c168a9aa35ccd0b24981526425e4730) | Starts publishing audio/video streams to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3067efa528fb9ffb8cf7685ce29925d4) | Stops publishing audio/video streams to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a41aefb8be652f8f6803020e543acaadc) | Starts publishing audio/video streams to a non-Tencent Cloud CDN. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0e1e8a1eb1cac3f5e5d4433b4aa21e8e) | Stops publishing audio/video streams to a non-Tencent Cloud CDN. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af7cf5544f9b8027e9526c32319a13838) | Sets layout and transcoding parameters for On-Cloud MixTranscoding. |

### Video APIs
| API          | Description         |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a84098740a2e69e3d1f02735861614116) | Enables local camera preview (mobile). |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae91432ada1767f793c460c7b897b6809) | Updates local camera preview. |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af6ee50bf2c4c592294061077fc727505) | Disables local camera preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | Pauses/Resumes publishing the local video stream. |
| [setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d) | Sets the image to display when local video is paused. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | Subscribes to a remote user’s video stream and binds a video rendering control. |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9be8a4c5ea4da16fb1ca42e8e258effd) | Updates a remote user’s video rendering control. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | Unsubscribes from a remote user’s video stream and unbinds the rendering control. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addaac0786ac0bd6e73a5f35c038df127) | Unsubscribes from all remote users’ video streams and unbinds all rendering controls. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | Pauses/Resumes receiving a remote user’s video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2d8a7b74068026a85158262cc9aedd66) | Pauses/Resumes receiving all remote users’ video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae047d96922cb1c19135433fa7908e6ce) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a02631a5e4251657875535c38ab319239) | Sets video preference. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a916eab6c78587300165008f61a473f8b) | Sets rendering parameters for the local image. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2e37d4b9555c58148ad507938375505f) | Sets rendering parameters for a remote image. |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272afecae1d291033cb9cd4b1d7b52e0) | Sets the rotation of encoded video images. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a32d9ba3696b305373508253f9bee8236) | Sets the mirror mode of encoded images. |
| [setGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abbbe1548bfba0bd082a08478ce35e9bc) | Sets the adaptation mode of the G-sensor. |
| [enableEncSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3a040c5012cf572b9dfabcca87f2cbb7) | Enables/Disables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2a018cc1010587ea9b0fbd791eb3c54f) | Switches between the small and big images of a remote user. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae75285c95fc53651e24fa23c4141093b) | Takes a video screenshot. |

### Audio APIs
| API          | Description         |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | Starts local audio capturing and publishing. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a272bba21d046347ac42d76069ba5972c) | Stops local audio capturing and publishing. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86) | Pauses/Resumes publishing the local audio stream. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8d8b8edf120036d4049cc3639a1ce81f) | Pauses/Resumes playing the audio stream of a remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5b63c0796404b80323ae67aafe0384ba) | Pauses/Resumes playing the audio streams of all remote users. |
| [setAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4a3dda74823afa597b42b981257e9e22) | Sets the audio route. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3dabe4a4e13509cf1bd5b3d58aabaa06) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6af5e2c4819a683042f382688aff41e9) | Sets the local audio capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a81037b960fb2b3501b1e8e60f2b5f9f3) | Gets the local audio capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b20e1eec637c82190c5264d78d686af) | Sets the playback volume of remote audio. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5a1636fa1300b0b4e2829846c36450a2) | Gets the playback volume of remote audio. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a43e99323fd5680fd377b95b97f0885c3) | Enables the volume reminder. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8b04666d32535637308605d5e15b7220) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7d55e5f15d1291afc89f7e1dfe0a25d8) | Stops audio recording. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5d6bf60e9d3051f601988e55106b296c) | Starts local media recording. |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae982c3c04c0195711ee4e56132522c4b) | Stops local media recording. |
| [checkAudioCapabilitySupport](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a225161d0c1028708b4c043653ea0ee4b) | Quires whether an audio capability is supported. This API works only on Android. |
| [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6d7f5080d804137be1bd3541f533b275) | Configures policy for the playback of the audio of multiple remote speakers. |

### Device management APIs
| API          | Description         |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae66395bc404d205fcd7fe9082ca85ce9) | Gets the device management class `TXDeviceManager`. |

### Beauty filter and watermark APIs
| API          | Description         |
|-----|-----|
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) | Gets the beauty filter management class `TXBeautyManager`. |
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1083aaf0441e3d90ce6641d278a97a63) | Adds watermarks. |

### Background music and audio effect APIs
| API          | Description         |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) | Gets the audio effect management class `TXAudioEffectManager`. |

### Screen sharing APIs
| API          | Description         |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | Starts screen sharing. |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab6c3014f6f88c775aa91fccea19ce8a4) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a56af9ada2d43cfb497fe44fa6d4b99cf) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a155ed7b6bcf2edf3259d26b8f8fdfe7e) | Resumes screen sharing. |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a34d994fbba559994aaf3a1f20420a885) | Sets encoding parameters for screen sharing (substream video). This API works on both desktop and mobile OS. |

### Custom capturing and rendering APIs
| API          | Description         |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | Enables/Disables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | Sends captured video frames to the SDK. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a206b9ce3594aa535b633d4f7c8f97210) | Enables/Disables custom audio capturing. |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a30a542b7d540c8699595a22ca3401f29) | Sends captured audio data to the SDK. |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a7b7d3707d2ed8e8f1221faf73af49027) | Enables/Disables custom audio tracks. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a899a1e9d42c9bf9ce1474aec13ac6747) | Mixes a custom audio track into the SDK. |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a362490afb9028595635b52d041a2bfb0) | Sets the publishing and playback volumes of external audio mixed into the published stream. |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b36383129314d70f150c08de182e2b8) | Gets the PTS for custom capturing. |
| [setLocalVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0b565dc8c77df7fb826f0c45d8ad2d85) | Sets the callback of video data for application of third-party beauty filters. |
| [setLocalVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa3cbb7a501c3151d94473965e2538c7a) | Sets the callback of local video for custom rendering. |
| [setRemoteVideoRenderListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4fca6803d13e4c7ff00dcac2974637e4) | Sets the callback of a remote video for custom rendering. |
| [setAudioFrameListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034b6fce9a517267acd874c243efc575) | Sets the audio data callback. |
| [setCapturedRawAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9047b34857b12d85688b3b3f1ca1c3f0) | Sets the format of the callback of raw audio frames captured by the local mic. |
| [setLocalProcessedAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac0f65e13815edc05ebd765826a94e3dc) | Sets the format of the callback of pre-processed local audio frames. |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a98a2e38d75366fbc2c4da92fec5c0a30) | Sets the format of the callback of audio frames played by the system. |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803) | Enables/Disables custom audio rendering. |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1c1c268173ab9b1bc24d34766e433931) | Gets playable audio frames. |

### Custom message sending APIs
| API          | Description         |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa4847ad53acc9ab5990194b21ff5b070) | Sends a custom message to all users in a room via TRTC’s UDP channel. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a034f9e1effbdadf8b9bfb7f3f06486c4) | Sends a custom message to all users in a room via TRTC’s SEI channel. |

### Network testing APIs
| API          | Description         |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6db053500be88a8735bfc69730447912) | Starts network speed testing. This API must be called before room entry. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3e862cef0e818ddecdc3dc4d66a6f8f9) | Stops network speed testing. |

### Debugging APIs
| API          | Description         |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aeb5168abbd62c631b65247e6289d1e2d) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a0ec9520dda7e2062f7455956d093113b) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2942d9d05045d3f0e0add45a3e10b3ee) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a495d2122a4098ab371d825c1f0bb90f5) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a44c20358d08da798e0f15d142c9c3914) | Sets the path to save local logs. |
| [setLogListener](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a299a71f4addb3638c7790de446fbdf37) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2cdb5d447114534f53bad5bdc48afba) | Sets whether to display the dashboard. |
| [setDebugViewMargin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa2014c293033e9ea60aa6ffd525ee2fa) | Sets the dashboard margin. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37f331dd0cfff51ab5a3becf4950a55e) | Calls the experimental API. |
| [setNetEnv](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a28ae49c86c5e5ba7e5ad2eae171bde76) | Sets TRTC’s backend clusters (for use by Tencent Cloud R&D team only). |

### Disused APIs
| API          | Description         |
|-----|-----|
| [setMicVolumeOnMixing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab356494d1b7dd924be69b23aa631a85a) | Sets the mic volume. |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a46ffe2b60f916a87345fb357110adf10) | Sets the strength of the beauty, skin brightening, and rosy skin filters. |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4ff69ce783f648f23dd737641344ac52) | Sets the strength of the eye enlarging filter. |
| [setFaceSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78a159a2a45d24dbd5722eb73d237e8a) | Sets the strength of the face slimming filter. |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a58bb7ce1fbbc40a50647d64693ac5d41) | Sets the strength of the chin slimming filter. |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a774eb948494cecec024771434ccd9d3c) | Sets the strength of the jaw lengthening/shortening filter. |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa14091f0d02330cbd02da5186e9dd874) | Sets the strength of the face shortening filter. |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3f806534b2596d7e29ea0ea6c070b591) | Sets the strength of the nose slimming filter. |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a521a0446d0922d480a1eec4b86f1ecb2) | Sets animated stickers. |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a066cbf8f4f6c1cd23fe9451b82c5a073) | Mutes/Unmutes animated effects. |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a925323ab809957ccaeb4cef30841cb72) | Sets the color filter. |
| [setFilterConcentration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5fb4c8bc9948e61a75b9ef85f618309d) | Sets the strength of the color filter. |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aef56a36b901d5e525ee539e7d5642063) | Sets green screen effects. |
| [playBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3df738557f5c658c37174ac9aeae9684) | Starts background music. |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a3ee7bdd15de4ba9010aa5ece3abff0ab) | Stops background music. |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a21ddee03e6f4cec028a24e5d5e30955e) | Pauses background music. |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aaa8b34ef2b334bd22a1cb6541a4c6702) | Resumes background music. |
| [getBGMDuration](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae7342a8bcfda22a872aa684f06a4677f) | Gets the total length of the music file, in milliseconds. |
| [setBGMPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a78f901b6175352a31b0236776bfdc661) | Sets the playback progress of background music. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ada9c2b4aaf9a1a9ab9cd846593fdf9e6) | Sets the volume of background music. |
| [setBGMPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab1e1c94c9efd967dbffb46d3ba08fef5) | Sets the local playback volume of background music. |
| [setBGMPublishVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a535eab48f9df390f4de5ebd5afcd59e3) | Sets the remote playback volume of background music. |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6f4f89be3c810acfa2430ad65fd7ea68) | Sets the reverb effect. |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a37acaf3b2539e0b1c18123a646e91189) | Sets the voice changing effect. |
| [playAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad1ed7667282eccfac1992c1e547a5aeb) | Plays an audio effect. |
| [setAudioEffectVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | Sets the volume of an audio effect. |
| [stopAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a214846db40c2d1be2fe8008c6637f631) | Stops an audio effect. |
| [stopAllAudioEffects](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a770543c80d3a5629a26d1382535fb6c4) | Stops all audio effects. |
| [setAllAudioEffectsVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9bb41c4ff1a5b24ca742fe3ce45a2bc0) | Sets the volume of all audio effects. |
| [pauseAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab32923d04ce164b82879b3e05833959f) | Pauses an audio effect. |
| [resumeAudioEffect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a33ab6e798d3da245435166464b702d4f) | Resumes an audio effect. |
| [enableAudioEarMonitoring](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9306bca7c6a13e0443a3fa1b40c9f343) | Enables/Disables in-ear monitoring. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a360eac7e67afcfab4390e7f37fa29a69) | Plays the video of a remote user. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a2391ba04b2d54fa1664b52f8f8546a32) | Stops playing the video of a remote user and pulling the user’s video data. |
| [setRemoteViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ab4197bc2efb62b471b49f926bab9352f) | Sets the rendering mode of a remote image. |
| [setRemoteViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a8478d804d2a07520ce2bc5466b727839) | Sets the clockwise rotation of a remote image. |
| [setLocalViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#af36ab721c670e5871e5b21a41518b51d) | Sets the rendering mode of the local image. |
| [setLocalViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a87fd1307871debc7c051de4878eb6d69) | Sets the clockwise rotation of the local image. |
| [setLocalViewMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa353b5cf5662c43252eb8e5132f041c1) | Sets the mirror mode of the local camera's preview image. |
| [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#acdbe3829d20f58cedd5a0c2f49ea24dc) | Starts playing the substream video of a remote user. |
| [stopRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ae5f540d795425046c9166b0a2361a8de) | Stops playing the substream video of a remote user. |
| [setRemoteSubStreamViewFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a73f66e66ffee44e19ebb4d8c56c89718) | Sets the fill mode of the substream video of a remote user. |
| [setRemoteSubStreamViewRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#affdf177b468fdf40a41782e2e47524cc) | Sets the clockwise rotation of the substream video of a remote user. |
| [setPriorRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad2efc2703c86ee009bd4a1d440d0c1e0) | Sets playback preference. |
| [setAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55) | Sets audio quality. |
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1dadf09b10a2d128e4cef11707934329) | Enables local audio capturing and publishing. |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a1b43a65a32f9dcb81b39b9c51c5bc4c6) | Switches cameras. |
| [isCameraZoomSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac7ae26eca2f9a673121803d6d175b034) | Queries whether the current camera supports zoom. |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a9f761eebdf04f724e0d1591c41c6045f) | Sets the camera zoom factor (focal length). |
| [isCameraTorchSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a645183ba7c0cea748973796cb38aad8c) | Queries whether the camera supports flash. |
| [enableTorch](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a09253f6547914d54058831b61325e770) | Enables/Disables flash. |
| [isCameraFocusPositionInPreviewSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#abd39aca40adfc8da6beaf32141f84cfa) | Queries whether the camera supports focus setting. |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa7c65fb033727804e7a79b8f135c776c) | Sets the coordinates of camera focus. |
| [isCameraAutoFocusFaceModeSupported](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a23f25ffb81215a32517da78455459ff2) | Queries whether the camera supports automatic facial recognition. |
| [setSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a5438dcc45dc2f26a3771a5feddcdef5d) | Sets the system volume type. |
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa29d36eaa707f6acf622e2f87f14b26a) | Enables/Disables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ad898c0d44a55b86af57de9854638193e) | Sends captured video data to the SDK. |
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aacbe76e164030701d261a2edbc43668f) | Starts screen sharing (for Android). |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#ac334d2c625c487d38eb3311de6831643) | Pauses/Resumes publishing the local video stream. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a4048ba6edaa0a959d0918a72cf98b576) | Pauses/Resumes receiving a remote user’s video stream. |
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a6db053500be88a8735bfc69730447912) | Starts network speed testing. This API must be called before room entry. |

### Error and warning callback APIs
| API          | Description         |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a511d0007e1990e63e853e46ce3f02670) | Callback for errors |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9871472ee8195dfc5d0c34fae3294465) | Callback for warnings |

### Room event callback APIs
| API          | Description         |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abf0525c3433cbd923fd1f13b42c416a2) | Callback of the result of room entry |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad5ac26478033ea9c0339462c69f9c89e) | Callback for room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6a4b7f39bc5dfb0c5d75ef8802e2e758) | Callback for role switching |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a9778a84932f02de9be52ea7513f606c1) | Callback for room switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac9fd524ab9de446f4aaf502f80859e95) | Callback of the result of requesting a cross-room call |
| [onDisConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6f7db4f0aaadad2cdfa822ba0060414c) | Callback of the result of ending a cross-room call |

### User event callback APIs
| API          | Description         |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a891f38e4cdeaf3ff18937726f0269c2c) | Callback for the entry of a user |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abfec3607f97823956fad77a7a63dc441) | Callback for the exit of a user |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) | Callback for publishing/unpublishing the primary-stream video by a remote user |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a80bcaac82e5372245746a4bc63656390) | Callback for publishing/unpublishing the substream video by a remote user |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac474bbf919f96c0cfda87c93890d871f) | Callback for publishing/unpublishing audio by a remote user |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0c1ccf1bec2d3261e9f11894b32e357e) | Callback for rendering the first video frame of the local user or a remote user |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a3516aaef4cb63e512cd713e4ec96d118) | Callback for playing the first audio frame of a remote user |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a181788d7441d41022ce014095ee05353) | Callback for sending the first local video frame |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#acb73daf4ce82cd03f787f057b233b412) | Callback for sending the first local audio frame |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aa75cd2a93cfb096357e2de226ff2ea47) | Callback for change of the video status of a remote user |

### Callback APIs for statistics on network and technical metrics
| API          | Description         |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b) | Callback of real-time statistics on network quality |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a24a6ee3b3709a42af226be7258521612) | Callback of real-time statistics on technical metrics |
| [onSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0dc9967589d6d3277f0e429e520f2c51) | Callback of network speed testing results |

### Callback APIs for change of connection status
| API          | Description         |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aed43a70b4a95eb95181e2b410013bf54) | Callback for the disconnection of the SDK from the server |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1c8654b64e4bde42a8a24954ecf2cb2d) | Callback for the SDK trying to reconnect to the server |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a36d96a42ec4b00a0e3808f7f8460cd7f) | Callback for the reconnection of the SDK to the server |

### Hardware event callback APIs
| API          | Description         |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aaa74021e5fd2564afb2df50e25eedeff) | Callback for the camera being ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#afdac7dee94451913a4dc9982badc8035) | Callback for the mic being ready |
| [onAudioRouteChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a1a608275247d2912e26bd83f648d6378) | Callback for change of the audio route (for mobile devices only) |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4e3b79968ccbb86de5b79e326a2daafa) | Callback of volume |

### Callback APIs for receiving custom messages
| API          | Description         |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a51fd654c5ec030ff84f208f2ba50298d) | Callback for receiving a custom message |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a98af11ba5b25d3124bd9533dc5197127) | Callback for losing a custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3640e6bf80a1f93991644701e9b0d96) | Callback for receiving an SEI message |

### CDN event callback APIs
| API          | Description         |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a03d0ef687b2973b9b13cb041bd35bb85) | Callback for publishing audio/video streams to Tencent Cloud’s live streaming CDN |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ad3cb7e5ceb69954d762eafca5a0e3a62) | Callback for stopping publishing audio/video streams to Tencent Cloud’s live streaming CDN |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a64df36d6c56dd69d8b6f051fd9fffcbc) | Callback for publishing audio/video streams to a non-Tencent Cloud CDN |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c3d63538897ddb9ed1b170819c41dca) | Callback for stopping publishing audio/video streams to a non-Tencent Cloud CDN |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af1c79a5ec3e0c106939e7f0d7849d694) | Callback for setting layout and transcoding parameters for On-Cloud MixTranscoding |

### Screen sharing callback APIs
| API          | Description         |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a7d15537d26fb001045ff95157d59ed3f) | Callback for starting screen sharing |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a12c57991389e32f04a56774df5d1ce76) | Callback for pausing screen sharing |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ade88963a254d297d3be1993e8a599f6e) | Callback for resuming screen sharing |
| [onScreenCaptureStopped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6c09b21b733da7d314d1db2cb03c8bcb) | Callback for stopping screen sharing |

### Callback APIs for local recording and screenshot taking
| API          | Description         |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a6d252931944577cc08d40db1f5ecd7bb) | Callback for starting local recording |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22f09234dc198d33fa38bbb595fb5764) | Callback of the progress of local recording |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0a3eef0daeb5107290cb5190ceb9467b) | Callback for ending local recording |

### Disused callback APIs
| API          | Description         |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aff18b3bc5b1e448b21b7614e5716e73e) | Callback for the entry of an anchor (disused) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a0d1361e52e96b4c7c1a5f1b89f4ef0fb) | Callback for the exit of an anchor (disused) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abe967d855abae66836877fe0dacf8b5f) | Callback for ending an audio effect (disused) |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ab77a0dff287e1642527cd414fc5fe5f5) | Callback of server speed testing results. This callback has been disused. |

### Callback APIs for custom video
| API          | Description         |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a41b44f9b0583bbf56ad9e96065ea825c) | Callback of video frames for custom rendering |
| [onGLContextCreated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#af4a7a3a4e4945bf216d87f81b6926dab) | Callback for creating an OpenGL context in the SDK |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a22afb08b2a1a18563c7be28c904b166a) | Callback of video frames for processing by third-party beauty filters |
| [onGLContextDestory](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a5f6d5ef01d3cd610959433107f78aa60) | Callback for destroying the OpenGL context in the SDK |

### Callback APIs for custom audio
| API          | Description         |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) | Callback of audio data captured by the local mic and pre-processed by the audio module |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46) | Callback of locally captured audio data that is pre-processed by the audio module, added with audio effects, and mixed with background music |
| [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902) | Callback of the audio data of each remote user before audio mixing |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7) | Callback of data mixed from the audio of each user before playback |
| [onMixedAllAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a96923a9286a88b83d6890f607884ceb3) | Callback of data mixed from all audio in the SDK, including captured and to-be-played audio |

### Other callback APIs
| API          | Description         |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#a77d78090666e330606b670bf8ce2d854) | Callback for printing local logs |

### Definitions of video enumerated values
| API          | Description         |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp01d5e1111c2ba49a53879c343fd484f2) | Resolution |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp509a1d5f7a44e1d60cf25e4afb640347) | Aspect ratio mode |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp8f7c7bceb683fdba0c3cb0a4766dd281) | Stream type |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFillMode) | Image fill mode |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp9edface2441370ef72f70dd4945ff0f9) | Rotation |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa173483f8f2f9cbfd604328c0a8cba50) | Beauty (skin smoothing) algorithm |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpde7f16ea7692e7c649e9a16638f48dbe) | Pixel format |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2c1424df181810edcbd68a9d2cb4adde) | Video data transfer method |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa367a3c86bde4916b80b03acd05ec218) | Mirror mode |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSnapshotSourceType) | Source of local screenshots |

### Definitions of network enumerated values
| API          | Description         |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa53ec28e9d73b79c701a709f44efbebe) | Application scenario |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp32cd3ba884366b8a2d45cad705f28b18) | Role |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp39c937e1be1c70563f58a5a6fdde96a1) | QoS control mode (disused) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp3a953a9777c6e1447a27bc454f9f00b9) | Video quality preference |
| [TRTCQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp43d6beae8b3d7c79f02df2f125c090a7) | Network quality |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5f5cc2365ee675bbc0f5a14095b1e0fc) | Video status |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp66f48a69ecc92051ca32055008a19c3e) | Reason for change of video status |

### Definitions of audio enumerated values
| API          | Description         |
|-----|-----|
| [TRTCAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2b7efdf7211746ab55166bb4d55ed619) | Audio sample rate |
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp96d66d1098694549803eaba6baedb9c0) | Audio quality |
| [TRTCAudioRoute](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7340a7d82950a691c95bde594a44959f) | Audio route (audio playback mode) |
| [TRTCReverbType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp30e899d6cb29154e1d73867d199b7191) | Reverb effect |
| [TRTCVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpac19166c196a2905657f2a3b52a68ce0) | Voice changing effect |
| [TRTCSystemVolumeType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp70bfa071c4ebab5e7ed1811a780a53d9) | System volume type (for mobile devices only) |
| [TRTCAudioCapabilityType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp29e12a3869cc165605dc0121e56888a3) | Audio capabilities supported. This is only applicable to Android. |

### Definitions of other enumerated values
| API          | Description         |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp2f4911d8563ae1db783b963d626681d8) | Log level |
| [TRTCGSensorMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp7821baad731a6db4d8977d304fafce63) | G-sensor mode (for mobile devices only) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp5e2e800d31dc99373db17e2def3afc99) | Layout mode for On-Cloud MixTranscoding |
| [TRTCRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpaa193560ab798cc5dcdb9624ce9740aa) | Type of media to record |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrpa7e631ba74d7c9f6832a6ad3be7a81af) | Input type for stream mixing |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#amgrp25c9df32061d8ad991f04b21fc6acacb) | Type of audio to record |

### Definitions of TRTC key types
| API          | Description         |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a7ff9e03272f5c8e7b585e8c4eea784e1) | Room entry parameters |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoEncParam) | Video encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCNetworkQosParam) | QoS control parameters |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCRenderParams) | Video rendering parameters |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCQualityInfo) | Network quality |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVolumeInfo) | Volume |
| [TRTCSpeedTestParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestParams) | Network speed testing parameters |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCSpeedTestResult) | Results of network speed testing |
| [TRTCTexture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCTexture) | Video texture data (applicable to Android only), including texture ID and the EGL context |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCVideoFrame) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioFrame) | Audio frame information |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ac5b1947f21f77726cbff822eaf0003f9) | Information of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a6066a5537ad8c1bc6158d43e8a4765db) | Layout and transcoding parameters for On-Cloud MixTranscoding |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCPublishCDNParam) | Relaying parameters for publishing audio/video streams to a non-Tencent Cloud CDN |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams) | Local audio recording parameters |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCLocalRecordingParams) | Local media recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#ad82a59c2209c0596dabaee1152820494) | Audio effect parameters (disused) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a1b79e0e45a5f137df2e1995af7c0885c) | Room switching parameters |
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#a9b833660fc60bd0b4e0c0625d2ad84f6) | Format of the custom audio callback |
| [TRTCScreenShareParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCScreenShareParams) | Screen sharing parameters. This is only applicable to Android. |

