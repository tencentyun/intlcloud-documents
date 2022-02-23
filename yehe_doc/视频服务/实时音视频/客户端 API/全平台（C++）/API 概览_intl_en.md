## Introduction
Since version 8.0, TRTC has provided new APIs for C++ in addition to the original ones. They can be used on Windows, iOS, macOS, and Android.
See the following documents for how to integrate the C++ APIs.  
- [iOS](https://intl.cloud.tencent.com/document/product/647/35092)  
- [Android](https://intl.cloud.tencent.com/document/product/647/35093)  
- [macOS](https://intl.cloud.tencent.com/document/product/647/35094)  
- [Windows](https://intl.cloud.tencent.com/document/product/647/35095)  

>?
>- The C++ APIs are currently available in LiteAV_TRTC only.  
>- On Windows, the TRTC header file automatically adopts the "trtc" namespace. You do not need to specify the namespace.

## ITRTCCloud @ TXLiteAVSDK

### Instance creation and event callback APIs
| API          | Description         |
|-----|-----|
| [getTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ga0ef57994050abf58a18a3defd4cc5fd0) | Creates a `TRTCCloud` instance (singleton). |
| [destroyTRTCShareInstance](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#gaadc9070c962327451dbc949a4c5a4681) | Terminates a `TRTCCloud` instance (singleton).  |
| [addCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a6a8317825ffe59ddcf1159a778dd7577) | Sets TRTC event callbacks. |
| [removeCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad088226e8af2d6764851efe7bd94652d) | Removes TRTC event callbacks. |

### Room APIs
| API          | Description         |
|-----|-----|
| [enterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) | Enters a room. |
| [exitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab3881c8829e7b8a3132e7b551e62fbf1) | Exits a room. |
| [switchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4705f2f116a1ec85bbc60ecaf552c89d) | Switches roles. |
| [switchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) | Switches rooms. |
| [connectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab5a0622e5d3d521d79ba4f85c44244eb) | Requests a cross-room call. |
| [disconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a08870fd955f90d02879e966dcd02bfd3) | Exits a cross-room call. |
| [setDefaultStreamRecvMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5) | Sets the subscription mode. It must be set before room entry to take effect. |
| [createSubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5ce8b3f393ad3e46a3af39b045c1c5a2) | Creates a sub-room instance (for concurrent playback from multiple rooms). |
| [destroySubCloud](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a980cf4d173abfb58c00ef35a20e12c85) | Terminates a sub-room instance. |

### CDN APIs
| API          | Description         |
|-----|-----|
| [startPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7cbe48ea2cd3fb05a5b10350b6d81265) | Starts publishing audio/video streams to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac4d3f88b6e067f32d1191878b6db1645) | Stops publishing audio/video streams to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a26e2d0b06211185d52836ffbdeddc3d1) | Starts publishing audio/video streams to a non-Tencent Cloud CDN. |
| [stopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9cf56c1f3a9aadf4c6123f44e1494a1b) | Stops publishing audio/video streams to a non-Tencent Cloud CDN. |
| [setMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8c835f1d49ab0f80a85569e030689850) | Sets layout and transcoding parameters for On-Cloud MixTranscoding. |

### Video APIs
| API          | Description         |
|-----|-----|
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8ac23e725c7ed75488df1be2ee514884) | Enables local camera preview (mobile). |
| [startLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8ac23e725c7ed75488df1be2ee514884) | Enables local camera preview (desktop). |
| [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0af978a75d5ba671b7ce5f0b81b003c8) | Updates local camera preview. |
| [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#af7003d2c12f5f783115ada43a715abe7) | Disables local camera preview. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) | Pauses/Resumes publishing the local video stream. |
| [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9) | Subscribes to a remote user’s video stream and binds a video rendering control. |
| [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a027a8b23a363dc91e6ce1c9773ee8664) | Updates a remote user’s video rendering control. |
| [stopRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abd186570272cd61b4a6e4aea870437e1) | Unsubscribes from a remote user’s video stream and unbinds the rendering control. |
| [stopAllRemoteView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7a55fb85c4135abfbe00af529cdaf9bc) | Unsubscribes from all remote users’ video streams and unbinds all rendering controls. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) | Pauses/Resumes receiving a remote user’s video stream. |
| [muteAllRemoteVideoStreams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa0d0d63eff6bbee7651ead569646b70b) | Pauses/Resumes receiving all remote users’ video streams. |
| [setVideoEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55b0710284e44ba3703e22b07c3665c8) | Sets video encoder parameters. |
| [setNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad21668c7550aad44f1ed61265ffceb24) | Sets video preference. |
| [setLocalRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acf1e58c46f0c160ab1a17706ea1aa735) | Sets rendering parameters for the local image. |
| [setRemoteRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab0bd203a8dd3c07910249b1c3e0df9e6) | Sets rendering parameters for a remote image. |
| [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a932ff32ec07b20a0e0d83bb434cfb691) | Sets the rotation of encoded video images. |
| [setVideoEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a251af554d7257ec64e84027136ae21ef) | Sets the mirror mode of encoded images. |
| [enableSmallVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5019a8005cd96662ce2cface662a811e) | Enables/Disables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad2c6cc256f6e24178cd7c9cd2290ea4d) | Switches between the small and big images of a remote user. |
| [snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c) | Takes a video screenshot. |

### Audio APIs
| API          | Description         |
|-----|-----|
| [startLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a86c80ed357798e50ccf5c7ae47317f4c) | Starts local audio capturing and publishing. |
| [stopLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47c51247d112b86d2397744c8f3c686b) | Stops local audio capturing and publishing. |
| [muteLocalAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1e1f27f131da042ca6e80beaa18055a8) | Pauses/Resumes publishing the local audio stream. |
| [muteRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae22224501b484166dac65c1873ecdbc3) | Pauses/Resumes playing the audio stream of a remote user. |
| [muteAllRemoteAudio](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a38177742eaf9bedf11109452230319c4) | Pauses/Resumes playing the audio streams of all remote users. |
| [setRemoteAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac49fa4a92105f01e2e296b20881a8324) | Sets the playback volume of a remote user. |
| [setAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8677a812326511ef92f963bbe049d42e) | Sets the local audio capturing volume. |
| [getAudioCaptureVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aed4cdd35906d151cd97f543332fb9f02) | Gets the local audio capturing volume. |
| [setAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a338984f5503d59ae06d67f55bd8f0766) | Sets the playback volume of remote audio. |
| [getAudioPlayoutVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae66cc77d6dfccb4c473eff062d0eb717) | Gets the playback volume of remote audio. |
| [enableAudioVolumeEvaluation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3127ec82f1610ac2bc0cb7d32b9bb4b9) | Enables the volume reminder. |
| [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5224523e00d5167eb75cee9b65f72677) | Starts audio recording. |
| [stopAudioRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a052a606496ce98cdc5a7e93098598a32) | Stops audio recording. |
| [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a55c3e8982056532a6cce56e3f7f29241) | Starts local media recording. |
| [stopLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a8b9b6f0608e48c27fc7c646718cb41ba) | Stops local media recording. |
| [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0e6e6434aaa03ce878280125a9c0fa4b) | Configures policy for the playback of the audio of multiple remote speakers. |

### Device management APIs
| API          | Description         |
|-----|-----|
| [getDeviceManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#acbe34e3a11decb05d8ea28eb494a113a) | Gets the device management class `TXDeviceManager`. |

### Beauty filter and watermark APIs
| API          | Description         |
|-----|-----|
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a78c7b8eaa17d721cfd6dcac0224dd50b) | Sets the beauty, skin brightening, and rosy skin filters. |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a4a1c376670ff4f3fdac8cf30bec78576) | Adds watermarks. |

### Background music and audio effect APIs
| API          | Description         |
|-----|-----|
| [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad9da9a5121bb52fbb85890dd857d7e8a) | Gets the audio effect management class `TXAudioEffectManager`. |
| [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) | Starts system audio capturing (for desktop systems only). |
| [stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) | Stops system audio capturing (for desktop systems only). |
| [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a52d0f9a999296633b1d859f75d36d5e8) | Sets system audio capturing volume. |

### Screen sharing APIs
| API          | Description         |
|-----|-----|
| [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab1fc5a303726a666d30051c836e33fdd) | Starts desktop screen sharing (for desktop systems only). |
| [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0e09090fe4281c0e78d8eb38496a8ed0) | Stops screen sharing. |
| [pauseScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0dcd89ed2e23706239db98b55dd806d4) | Pauses screen sharing. |
| [resumeScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9dc10db068b9d8c6a0fcb8b085359f33) | Resumes screen sharing. |
| [getScreenCaptureSources](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad23c03ad142e8a42c49967ff9ccf9592) | Enumerates shareable screens and windows (for desktop systems only). |
| [selectScreenCaptureTarget](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a9d16af81b2ea2db7b91a8346add13393) | Selects a screen or window to share (for desktop systems only). |
| [setSubStreamEncoderParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a542913f5081fb2479137a7416c970e2d) | Sets encoding parameters for screen sharing (substream video). This API works on both desktop and mobile OS. |
| [setSubStreamMixVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aff8dd1456e5bebff5495d84683c7f83e) | Sets audio mixing volume for screen sharing (for desktop systems only). |
| [addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff) | Adds a window to the exclusion list of screen sharing (for desktop systems only). |
| [removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf) | Removes a window from the exclusion list of screen sharing (for desktop systems only). |
| [removeAllExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#abb20ff837f1f5955bea349ff95002a10) | Removes all windows from the exclusion list of screen sharing (for desktop systems only). |
| [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a442186322939f9b93d6c6e0a3ace7bd3) | Adds a window to the screen sharing list (for desktop systems only). |
| [removeIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3674c0ee6514d118fddd9a500ccafb03) | Removes a window from the screen sharing list (for desktop systems only). |
| [removeAllIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a5d2812b4068e89e6d2a422cd74257246) | Removes all windows from the screen sharing list (for desktop systems only). |

### Custom capturing and rendering APIs
| API          | Description         |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | Enables/Disables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | Sends captured video frames to the SDK. |
| [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a166d6ea0b36bc1adf3d3eddde35207c3) | Enables/Disables custom audio capturing. |
| [sendCustomAudioData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a47ba3ba599134e902299dda9c5596c0d) | Sends captured audio data to the SDK. |
| [enableMixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a896ff4b2731488821dd1ce382276ca0c) | Enables/Disables custom audio tracks. |
| [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd) | Mixes a custom audio track into the SDK. |
| [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418) | Sets the publishing and playback volumes of external audio mixed into the published stream. |
| [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a33ed1b26695b6b75dc9ce78e5280cbb4) | Gets the PTS for custom capturing. |
| [setLocalVideoProcessCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a3f6d32bdf3cb0fe72b61455304b975c6) | Sets the callback of video data for the application of third-party beauty filters. |
| [setLocalVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad64031e060146f7985263aad994fc733) | Sets the callback of local video data for custom rendering. |
| [setRemoteVideoRenderCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1efc475e32f06c768330ff80ebffbc8a) | Sets the callback of a remote user’s video data for custom rendering. |
| [setAudioFrameCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a607dc63d8d944869537457c5b92b56e9) | Sets the callback of audio data for custom rendering. |
| [setMixedPlayAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1c4e3c6d0c2653609e748ceeda8bb46e) | Sets the format of the callback of audio frames played by the system. |
| [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7047f52811cefa10cf020ee20db1b087) | Enables/Disables custom audio rendering. |
| [getCustomAudioRenderingFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ac986d3ec66ab6681d94c8eb933b519de) | Gets playable audio frames. |

### Custom message sending APIs
| API          | Description         |
|-----|-----|
| [sendCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a858b11d4d32ee0fd69b42d64a1d65389) | Sends a custom message to all users in a room via TRTC’s UDP channel. |
| [sendSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa91b261d10bbdb43508e9e2c33697c29) | Sends a custom message to all users in a room via TRTC’s SEI channel. |

### Network testing APIs
| API          | Description         |
|-----|-----|
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab9052b69fd4e12b5860da03a868e87d7) | Starts network speed testing. This API must be called before room entry. |
| [stopSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ad6ba6ea2c5beace98b99ce98d326be4c) | Stops network speed testing. |

### Debugging APIs
| API          | Description         |
|-----|-----|
| [getSDKVersion](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a11a1bc22514ac5a7bd9052a5cc444147) | Gets the SDK version. |
| [setLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aa6551d4e61a7a003d91b045ed2e13466) | Sets the log output level. |
| [setConsoleEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a589f4eefb2d7380e6bb145a9b0111634) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a357393d1eb2f92b7219395162c531e65) | Enables/Disables local log compression. |
| [setLogDirPath](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#afbacbfc33a72f8fdd6995cf1ec3d04a6) | Sets the path to save local logs. |
| [setLogCallback](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a239c5b9962a95a1eb4662440fab682fd) | Sets the log callback. |
| [showDebugView](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a7df528c2024556a073b4668879dff91f) | Sets whether to display the dashboard. |
| [callExperimentalAPI](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a187cb56ce8bbdf9a74e347954d2c7c6a) | Calls the experimental API. |

### Disused APIs
| API          | Description         |
|-----|-----|
| [enableCustomVideoCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#aaeab72ed55be06685e293c3cf92b6f90) | Enables/Disables custom video capturing. |
| [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6) | Sends captured video data to the SDK. |
| [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) | Pauses/Resumes publishing the local video stream. |
| [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65) | Pauses/Resumes receiving a remote user’s video stream. |
| [startSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__cplusplus.html#ab9052b69fd4e12b5860da03a868e87d7) | Starts network speed testing. This API must be called before room entry. |

### Error and warning callback APIs
| API          | Description         |
|-----|-----|
| [onError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a9724da0b3da9b2eca5736fa8e54aa410) | Callback for errors |
| [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a53169ea41d90506cccbff507ba1932a4) | Callback for warnings |

### Room event callback APIs
| API          | Description         |
|-----|-----|
| [onEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a236a49e0525615b6435eaa826b7caffe) | Callback of the result of room entry |
| [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) | Callback for room exit |
| [onSwitchRole](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a248335805c125e225cfec249697f2299) | Callback for role switching |
| [onSwitchRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ac5889e412f38769f2d21887f9bd7eeec) | Callback for room switching |
| [onConnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a62333366a3a1ab09dc2b2f627a8a1bdd) | Callback of the result of requesting a cross-room call |
| [onDisconnectOtherRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a292d6661cb93ba30ff68b1f88cf173f1) | Callback of the result of ending a cross-room call |

### User event callback APIs
| API          | Description         |
|-----|-----|
| [onRemoteUserEnterRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a43704996ae1f50749b7c7140755350f1) | Callback for the entry of a user |
| [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a5f7c705f3894d3a430ef1fac8bf8e2c5) | Callback for the exit of a user |
| [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) | Callback for publishing/unpublishing the primary-stream video by a remote user |
| [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a460922e4fb4b000d1dbd27b596dd0e5c) | Callback for publishing/unpublishing the substream video by a remote user |
| [onUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a6f449dc5294e369750bc15a39eaa856c) | Callback for publishing/unpublishing audio by a remote user |
| [onFirstVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad28d27badd56ac274c44720cc9f253d5) | Callback for rendering the first video frame of the local user or a remote user |
| [onFirstAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a123616289b3219bc36137bc77e8e8b7a) | Callback for playing the first audio frame of a remote user |
| [onSendFirstLocalVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a454ea7e7103b2838440cafba3e524433) | Callback for sending the first local video frame |
| [onSendFirstLocalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0bd950cb774fd40cfdc2fbff885295d2) | Callback for sending the first local audio frame |
| [onRemoteVideoStatusUpdated](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a967a9b593385a8081083e84d3f5648b5) | Callback for change of the video status of a remote user |

### Callback APIs for statistics on network and technical metrics
| API          | Description         |
|-----|-----|
| [onNetworkQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a377441bace65d98a1218817914a12ecb) | Callback of real-time statistics on network quality |
| [onStatistics](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ae7e4117f9c8004c9bcc5a29d64e840c9) | Callback of real-time statistics on technical metrics |
| [onSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a7bbfbd86185f20935f8a23d7dad94d9a) | Callback of network speed testing results |

### Callback APIs for change of connection status
| API          | Description         |
|-----|-----|
| [onConnectionLost](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a34c34705bb67127ff6d28700cf2ab591) | Callback for the disconnection of the SDK from the server |
| [onTryToReconnect](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#afe74dff22fde93fe0f07fcf18153d334) | Callback for the SDK trying to reconnect to the server |
| [onConnectionRecovery](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ae90cd149a676418016cb8736b217f1a8) | Callback for the reconnection of the SDK to the server |

### Hardware event callback APIs
| API          | Description         |
|-----|-----|
| [onCameraDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a13a9ad0933b7ab872987e432f005e8ad) | Callback for the camera being ready |
| [onMicDidReady](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0ba02a5d9009ebb9c4e80c0c43c80bca) | Callback for the mic being ready |
| [onUserVoiceVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a61df1f9eec0bfcebf421be865275ffc5) | Callback of volume |
| [onDeviceChange](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ac86c1b0d445a33f6340394b3b78490bd) | Callback for change of the connection status of a local device (for desktop systems only) |
| [onAudioDeviceCaptureVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a40eeba4a6034450bc055b8f62c763520) | Callback for change of the mic’s system audio capturing volume |
| [onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad87c12c924b781b3b8429f8e8aafc338) | Callback for change of the system’s playback volume |
| [onSystemAudioLoopbackError](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a296665d16719c02dc055c983f88b40c3) | Callback of whether system audio capturing is enabled successfully (for macOS only) |
| [onTestMicVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a9f0101fa8222c6163f1b23fcce81e22b) | Volume callback for mic testing |
| [onTestSpeakerVolume](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a04bb10b06af17cdc43b7831336736539) | Volume callback for speaker testing |

### Callback APIs for receiving custom messages
| API          | Description         |
|-----|-----|
| [onRecvCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0a5690652db3902e98e1168bad12ec1a) | Callback for receiving a custom message |
| [onMissCustomCmdMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab5d0cb61c24b77ecdb177ff19fc95075) | Callback for losing a custom message |
| [onRecvSEIMsg](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab364b929cd0d9ffff6e47c20ec52372c) | Callback for receiving an SEI message |

### CDN event callback APIs
| API          | Description         |
|-----|-----|
| [onStartPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a345ab7b45a9d0027926dbf580e8e0258) | Callback for publishing audio/video streams to Tencent Cloud’s live streaming CDN |
| [onStopPublishing](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a8e046f5bd34498b13ae057caaab64913) | Callback for stopping publishing audio/video streams to Tencent Cloud’s live streaming CDN |
| [onStartPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a16164548764979e84d3b5301f28890ff) | Callback for publishing audio/video streams to a non-Tencent Cloud CDN |
| [onStopPublishCDNStream](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0da75e040521c0945c3735f4893e6c09) | Callback for stopping publishing audio/video streams to a non-Tencent Cloud CDN |
| [onSetMixTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0f11cee9e2659f7ea8484fdffd6b8583) | Callback for setting layout and transcoding parameters for On-Cloud MixTranscoding |

### Screen sharing callback APIs
| API          | Description         |
|-----|-----|
| [onScreenCaptureStarted](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a8baff9a6c699ea1d82c5e7abb6ded97b) | Callback for starting screen sharing |
| [onScreenCapturePaused](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a32acecdafd9058cc7d70a3abe6995051) | Callback for pausing screen sharing |
| [onScreenCaptureResumed](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a63c073daf1ad93cfa2e6c79695434e22) | Callback for resuming screen sharing |
| [onScreenCaptureStoped](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4d182e6b60d8be536e69253d906af84d) | Callback for stopping screen sharing |
| [onScreenCaptureCovered](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a490f827ffd6e7728a6ec49cba63875b1) | Callback for the window to share being covered (for Windows only) |

### Callback APIs for local recording and screenshot taking
| API          | Description         |
|-----|-----|
| [onLocalRecordBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4a40b1b338d93c871f73354d1d45f24b) | Callback for starting local recording |
| [onLocalRecording](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a0b226b8e627dad7850a880d48ffb91dd) | Callback of the progress of local recording |
| [onLocalRecordComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a4455252d3e0f5d869db18641e24da106) | Callback for ending local recording |
| [onSnapshotComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a10501027a79d1d05231319570c0e5603) | Callback for taking a screenshot |

### Disused callback APIs
| API          | Description         |
|-----|-----|
| [onUserEnter](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad606b861a3545832fb4821a7e0230925) | Callback for the entry of an anchor (disused) |
| [onUserExit](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#abbc4fe2ccac90f77c80f55d46d6c8951) | Callback for the exit of an anchor (disused) |
| [onAudioEffectFinished](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aab3c91276b6e570ea9acfe1581e1aa51) | Callback for ending an audio effect (disused) |
| [onPlayBGMBegin](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ad93b8204416558e63c18349bf29ff592) | Callback for starting background music (disused) |
| [onPlayBGMProgress](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a1879cc4e50492431a3346828e9130f21) | Callback of the playback progress of background music (disused) |
| [onPlayBGMComplete](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#abaf89c758a4dd21e21db488e997bef2a) | Callback for ending background music (disused) |
| [onSpeedTest](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a455264cfcf2a7a3f022f3bce0659f9f7) | Callback of server speed testing results. This callback has been disused. |

### Callback APIs for custom video
| API          | Description         |
|-----|-----|
| [onRenderVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aea602851c96370558a7eeb850d7eb6b8) | Callback of video frames for custom rendering |
| [onProcessVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#aa416979597d1bec68dc268a9432619ae) | Callback of video frames for processing by third-party beauty filters |

### Callback APIs for custom audio
| API          | Description         |
|-----|-----|
| [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a1488e35460441c351cab75d9702498f6) | Callback of audio data captured by the local mic and pre-processed by the audio module |
| [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#affb432a77f938d1e8dfb6c0d5488dbcf) | Callback of locally captured audio data that is pre-processed by the audio module, added with audio effects, and mixed with background music |
| [onPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#ab841da62beb88a9fa9bce58d25df6f23) | Audio data of each remote user before audio mixing |
| [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a6649f62d4138d9bc73ae484e63dec081) | Callback of data mixed from the audio of each user before playback |

### Other callback APIs
| API          | Description         |
|-----|-----|
| [onLog](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudCallback__cplusplus.html#a2fa3d9997c9810ffa6a95e0a7a4a50d0) | Callback for printing local logs |

### Definitions of video enumerated values
| API          | Description         |
|-----|-----|
| [TRTCVideoResolution](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gace04ad7a0bf531f4d09dc6a540f09f95) | Resolution |
| [TRTCVideoResolutionMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaa6787a9059d7b725a30ffcf9f4aabb64) | Aspect ratio mode |
| [TRTCVideoStreamType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga461563be214e8f0579a79741f37d18e3) | Stream type |
| [TRTCVideoFillMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga496a32286104187149b4e40284cbfb36) | Image fill mode |
| [TRTCVideoRotation](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga4f8ab82260baa03f83f123ebeaa82b2e) | Rotation |
| [TRTCBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga46f49720df57d17b267054cb9ee4d079) | Beauty (skin smoothing) algorithm |
| [TRTCVideoPixelFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga98b07c6c79303f486682b3b92fa88c7e) | Pixel format |
| [TRTCVideoBufferType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga3a075ea5603cdd730550b37fc0032c68) | Video data transfer method |
| [TRTCVideoMirrorType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga778fcc2797d6076745997327c8b20009) | Mirror mode |
| [TRTCSnapshotSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga65de3d8416c7faabe1a8b77a6fd9cc7c) | Source of local screenshots |

### Definitions of network enumerated values
| API          | Description         |
|-----|-----|
| [TRTCAppScene](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaa57f4545ef7331e3157eee1639d28780) | Application scenario |
| [TRTCRoleType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga42ff820a33d9f3535d203fd5d6782cb5) | Role |
| [TRTCQosControlMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga6615b296e31fc3d03c0df92e9755b5aa) | QoS control mode (disused) |
| [TRTCVideoQosPreference](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga60efcaeea7692bbce8dc362856683319) | Video quality preference |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCQualityInfo) | Network quality |
| [TRTCAVStatusType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga9ab84e3f9458dacd479937e5a24c95f2) | Video status |
| [TRTCAVStatusChangeReason](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga37b6311e4d5ba7376070ba65de520865) | Reason for change of video status |

### Definitions of audio enumerated values
| API          | Description         |
|-----|-----|
| [TRTCAudioQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga96f3d4cdcf3baa9df39ab4e1b3f0eb40) | Audio quality |

### Definitions of other enumerated values
| API          | Description         |
|-----|-----|
| [TRTCLogLevel](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gafa83683b4840bcb3200d1da63c10276d) | Log level |
| [TRTCScreenCaptureSourceType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gad96fcfd4a65c0f99579b0c35ef86645d) | Type of the content to share (for desktop systems only) |
| [TRTCTranscodingConfigMode](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#gaec50c849a17b7706f6989d718fc6b7df) | Layout mode for On-Cloud MixTranscoding |
| [TRTCLocalRecordType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga92580ecee493fb524b84234305316238) | Type of the media to record |
| [TRTCMixInputType](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga323584f89d0479be0a1b554ec05672f7) | Input type for stream mixing |
| [TRTCDeviceType](https://liteav.sdk.qcloud.com/doc/api/en/namespaceliteav.html#abaf3d3254d2b2e11fb2064478975be17) | Device type (for desktop systems only) |
| [TRTCAudioRecordingContent](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ga5adbddb520b6eea48142c3b5be740205) | Type of audio to record |

### Definitions of TRTC key types
| API          | Description         |
|-----|-----|
| [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCParams) | Room entry parameters |
| [TRTCVideoEncParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVideoEncParam) | Video encoding parameters |
| [TRTCNetworkQosParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCNetworkQosParam) | QoS control parameters |
| [TRTCRenderParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCRenderParams) | Video rendering parameters |
| [TRTCQualityInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCQualityInfo) | Network quality |
| [TRTCVolumeInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVolumeInfo) | Volume |
| [TRTCSpeedTestParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSpeedTestParams) | Network speed testing parameters |
| [TRTCSpeedTestResult](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSpeedTestResult) | Results of network speed testing |
| [TRTCVideoFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCVideoFrame) | Video frame information |
| [TRTCAudioFrame](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioFrame) | Audio frame information |
| [TRTCMixUser](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#ac5b1947f21f77726cbff822eaf0003f9) | Information of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCTranscodingConfig) | Layout and transcoding parameters for On-Cloud MixTranscoding |
| [TRTCPublishCDNParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCPublishCDNParam) | Relaying parameters for publishing audio/video streams to a non-Tencent Cloud CDN |
| [TRTCAudioRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioRecordingParams) | Local audio recording parameters |
| [TRTCLocalRecordingParams](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCLocalRecordingParams) | Local media recording parameters |
| [TRTCAudioEffectParam](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioEffectParam) | Audio effect parameters (disused) |
| [TRTCSwitchRoomConfig](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCSwitchRoomConfig) | Room switching parameters |
| [TRTCAudioFrameCallbackFormat](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCAudioFrameCallbackFormat) | Parameters for the format of the custom audio callback |
| [TRTCScreenCaptureSourceInfo](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#structliteav_1_1TRTCScreenCaptureSourceInfo) | Information of the content to share (for desktop systems only) |
| [ITRTCScreenCaptureSourceList](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__cplusplus.html#classliteav_1_1ITRTCScreenCaptureSourceList) | List of sharable sources |

