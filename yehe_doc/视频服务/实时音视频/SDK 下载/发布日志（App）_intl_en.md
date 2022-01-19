## Version 9.4 Released on December 8, 2021

**New features:**
- All platforms: supported highlighting the speaking user, which is useful in large-scale audio co-anchoring scenarios. It enables users to focus on the audio of whoever is speaking when there are multiple speakers in the room. You can call the [setRemoteAudioParallelParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0e6e6434aaa03ce878280125a9c0fa4b) API to set this feature.
- macOS: supported dual channels for the system audio capturing API [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486).
- iOS: supported background music files in 24-bit WAV format.
- Android & iOS: This version complies with China’s privacy and security regulations and has been tested by multiple Tencent products.

**Bug fixing:**
- All platforms: fixed the issue where room switching fails if [switchRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a1f3bed34f92b3ff908beb2d0ed2866c9) is called frequently.
– iOS: fixed the issue where [setVideoEncoderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a200c174b27bbe7397b0639e707ee6547) does not work during in-app screen sharing ([startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf51acf26b2212192f7145468886b791)).
- iOS: fixed the occasional issue of rising memory usage during screen sharing ([startScreenCaptureByReplaykit](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abebcd402e310d5d7dcbef9f6b601cfc4)).

**Improvement:**
- All platforms: sped up room entry, reducing the fluctuation in room entry speed.
- macOS: fixed the issue of high CPU and memory usage when mouse cursor is captured during screen sharing.
- Android: made the capturing resolution in line with the resolution of the screen during screen sharing to avoid black bars.
- Android: improved the compatibility of the hardware video decoder, fixing the issue of black bars due to change of playback resolution on some devices.
- Windows: optimized the audio gain control algorithm, fixing the issue of marked noise due to high audio gain on some devices.

## Version 9.3 Released on November 3, 2021

**Bug fixing**
- All platforms: fixed failure to obtain `point2PointDelay` (value is 0).
- All platforms: fixed occasional parsing failure, which causes SEI messages to be lost.
- macOS: fixed the issue where the camera does not output frames on macOS 12 beta.
- iOS & macOS: fixed the issue where no images are displayed when `startRemoteView` is called earlier.
- Windows: fixed the issue of aliasing when video is encoded in portrait mode and beauty filters are enabled.
- Windows: fixed the issue where, when third-party beauty filters are used, no callback for custom rendering is returned after resolution change.

**Improvement**
- All platforms: improved instant streaming performance under poor network conditions.
- All platforms: optimized the QoS control policy under poor network conditions, ensuring smoother communication.
- All platforms: improved the speed test to support testing the current bandwidth.
- All platforms: improved support for TCP for better adaptability to different network environments.

## Version 9.2 Released on September 23, 2021

**New features**
- Android & iOS: supported SOCKS5 proxies.
- Windows: enabled adaptive echo cancellation for the `TRTCAudioQualityMusic` mode to automatically balance between audio quality and echo cancellation strength.
- All platforms: allowed audio pitch setting.

**Bug fixing**
- Windows: fixed the issue where some cameras do not output data on Windows installed on Mac.
- Android: fixed the issue where there is no upstream audio after switch between CDN live streaming and TRTC.
- iOS: fixed the issue where, when a screen is shared from web, users on iOS see pixelated video if they enable custom rendering.

**Improvement**
- Android: fixed the issue where the “Application Not Responding” error occurs during hardware decoding.
- Android: fixed the compatibility issue for the rotation of local camera preview.
- Android: improved instant streaming performance.
- Android & iOS: optimized the 3A policy for the duet mode.
- Windows: improved the AGC algorithm, reducing cases of excessively low or high volume.
- All platforms: optimized the jitter control algorithm under poor network conditions, enabling smoother video playback.

## Version 9.1 Released on September 4, 2021

**New features**
- All platforms: supported using a C++ API to set the format of called back audio frames.
- Windows: supported streaming VOD files in AC3 format.
- Windows: supported getting the resolutions supported by a camera. For details, please see [ITXDeviceCollection.getDeviceProperties](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__cplusplus.html#ad502f48cb2a4470943134e4b48904450).
- Windows: supported NVIDIA, Intel, and AMD hardware decoding.
- macOS: supported recording local media.

**Bug fixing**
- All platforms: fixed occasional failure to enter a room.
- macOS: fixed the issue where, during screen sharing, the preview flickers when the resolution is changed.
- Android: fixed display error of the substream video after switching from a sub-room to the main room.
- Android: fixed the occasional issue where the frame rate setting does not take effect in some scenarios.
- Windows: fixed failure to pull streams after audience switch to CDN playback.
- Windows: fixed the issue where the image disappears when VOD files in certain formats are streamed.

**Quality improvement**
- All platforms: improved experience under poor network conditions.
- Android: improved audio status management during room exit.
- Android: improved the logic of recovery in the case of audio capturing failure, to increase the success rate of audio capturing.
- Android: fixed video overexposure under certain conditions.

## Version 9.0 Released on August 6, 2021

**New features**
- iOS: allowed setting the capturing volume of system audio. For details, please see [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae).
- All platforms: allowed setting the volume of custom audio tracks. For details, please see [setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418).
- All platforms: separated audio and video packet loss in the status callback. For details, please see [TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatistic__cplusplus.html#structliteav_1_1TRTCRemoteStatistics).

**Quality improvement**
- All platforms: optimized the subscription process to improve instant streaming performance for manual subscription.
- All platforms: fixed the issue of repeated `onExitRoom` callback in some scenarios.

**Bug fixing**
- Android: fixed the issue where bitrate and frame rate settings during custom capturing do not take effect.
- iOS: fixed failure to publish streams if users enable the screen sharing substream first and then turn the camera on.
- iOS: fixed blurriness of recorded local video.
- iOS: fixed several stability issues.
- Windows: fixed frame rate exception for the capturing of screen sharing images.
- Windows: fixed the issue where, after the sharing source is changed during screen sharing, audience see a frame of the old source before the new source is played.

## Version 8.9 Released on July 15, 2021

**New features** 
- Android: supported specifying external GL contexts for custom capturing, allowing more flexible use of OpenGL contexts.
- Windows: allowed specifying the speaker for system audio capturing ([startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e)).
- Windows: supported NVIDIA hardware encoding, improving stream publishing performance.
- All platforms: supported cloud proxies, which are a secure and easy way to access TRTC from inside a corporate firewall.
- All platforms: added the stream type parameter to the APIs [muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) and [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65).
- All platforms: added the gateway RTT parameter `gatewayRtt` to the status callback [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#ae7e4117f9c8004c9bcc5a29d64e840c9), which indicates the quality of network between users and their Wi-Fi routers.
- All platforms: supported recording audio into more formats using the [startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5224523e00d5167eb75cee9b65f72677) API.

**Quality improvement**
- All platforms: fixed shaky audio in some scenarios.
- Android: improved instant streaming performance.
- Android: upgraded the audio pre-processing algorithm for clearer audio in calls.

**Bug fixing**
- Windows: fixed the issue of echo in recorded local video if VODPlayer is used to stream VOD files.
- Windows: fixed crash when the window filtering feature is enabled during screen sharing on high DPI displays.
- iOS: fixed the issue where the landscape mode does not take effect for system-level screen sharing via the substream.
- iOS: fixed the issue of memory leak when custom rendering is enabled only for remote videos and the RGBA format is used.
- All platforms: fixed occasional failure to enter a room.

## Version 8.8 Released on June 21, 2021

**New features**
Android & macOS & iOS: allowed playing audio via peripheral devices. For details, please see the API [enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803).

**Quality improvement**
- All platforms: made it easier to use `mixExternalAudioFrame`. You no longer need to call the API at a regular interval.
- macOS: reduced the CPU usage of screen sharing when mouse cursor capturing is enabled.
- Windows: made AGC faster and more timely for better results.
- Windows: reduced the performance overhead of screen sharing when the window filtering feature is enabled.

**Bug fixing**
- iOS: fixed the issue where, when a local audio file in AAC format is played, the total length is inaccurate.
- Android: fixed the issue of audio stutter after the SDK is switched to the background on some devices.

## Version 8.7 Released on May 25, 2021
**New features**
- All platforms: supported anomaly detection for peripheral audio devices. After registering `onStatistics`, you can detect in real time when there is no audio for a long time and when audio cracks or is interrupted via the `audioCaptureState` field in [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#structtrtc_1_1TRTCLocalStatistics).
- Windows: supported RGBA video data for custom capturing.

**Quality improvement**
- All platforms: optimized background music management to release memory resources in a timely manner.
- All platforms: ensured that audience receive the [onUserVideoAvailable(false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) notification in a timely manner after stream publishing is paused because the application is switched to the background.
- macOS: reduced the CPU and memory usage of mouse cursor capturing during screen sharing.

**Bug fixing**
- Android: fixed the issue where `setRemoteViewFillMode` doesn’t work on some devices.
- iOS & macOS: fixed the memory release issue of custom beauty filters after they are disabled.

## Version 8.6 Released on May 8, 2021
- All platforms: optimized the QoS control algorithm, enhancing audio/video transmission quality.
- All platforms: improved audio playback smoothness when users switch between the anchor and audience roles.
- iOS & macOS & Windows: optimized the audio processing module, improving audio quality in the speech and default modes.
- iOS & macOS: improved the adaptability of custom audio capturing to situations of high CPU usage.
- iOS & Android: supported publishing screen recording data via the substream, as in SDKs for desktop platforms.
- macOS: added native support for Apple M1.
- Windows: optimized the memory allocation logic to enhance stability.


## Version 8.5 Released on March 24, 2021
**New features**
- macOS: optimized the screen sharing feature. You can now share other windows along with the target window. For details, see the API [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233).
- All platforms: supported publishing VOD content. You can now bind [TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#classcom_1_1tencent_1_1rtmp_1_1TXVodPlayer) with `TRTCCloud` and publish the content played by VOD via TRTC’s substream.</li>
- All platforms: supported custom capturing of substream data. For details, see the API [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629).
- All platforms: supported custom audio mixing. You can feed a local audio track into the SDK’s audio processing. The SDK will mix the two tracks before publishing. For details, see the API [mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f).
- All platforms: supported mixing only video streams, allowing for more flexible stream mixing control.

**Quality improvement**
- macOS: enabled the `startSystemAudioLoopback` API to support dual sound channels.
- Windows: supported automatic switch to the slideshow window when a slideshow is selected for screen sharing.
- All platforms: included end-to-end latency in the information returned via the status callback.

**Bug fixing**
- iOS: fixed occasional crash when images are rendered using OpenGL in the background.
- iOS: fixed playback failure when shared images are static.


## Version 8.4 Released on February 8, 2021
**New features**
- macOS: supported capturing system audio, i.e., the system loopback feature that is enabled on Windows. The feature allows the SDK to capture system audio so that anchors can stream local audio or video files to other users.
- macOS: supported local preview for screen sharing. You can now display screen sharing preview in a small window.
- Windows: supported setting the volume of the current process. You can now use [setApplicationPlayVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1) to set the volume of the volume mixer.
- All platforms: supported local recording. An anchor can now record local audio and video into an MP4 file during streaming. For details, see [startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b).

**Quality improvement**
- All platforms: improved audio quality in the [music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) mode, which makes it more suitable for Clubhouse-like audio streaming scenarios.
- All platforms: improved the adaptability to poor network conditions. Smooth audio and video can be delivered even when the packet loss rate reaches 70%.
- Windows: improved audio quality in some streaming scenarios by significantly reducing audio damage.
- Windows: improved performance by 20%-30% in some scenarios.

**Bug fixing**
- Windows: fixed the issue where the SDK crashes when the desktop is shared on Windows Server 2019 Datacenter x64.
- Windows: fixed the issue where screen sharing sometimes ends unexpectedly when the target window is resized during screen sharing.
- Windows: fixed image capturing failure with some cameras.
- iOS: fixed the issue where `snapvideoshot` causes stuttering with CAAnimation.
- iOS & macOS: fixed the black screen issue when the same view is used to display camera and screen sharing images in turn.
- iOS: fixed the blurry screen issue on iPhone 6S when a third-party beauty filter component is used.
- iOS: fixed the issue where, in cases where TRTC and VOD are used at the same time, the SDK occasionally crashes after VOD is stopped.
- Android: fixed the issue where audio is played via the speaker after a user using Bluetooth earphone rejects an incoming call.

## Version 8.3 Released on January 15, 2021

**New features**

Optimized the business logic of custom capturing:
- iOS & Android & macOS: optimized the audio module to ensure acoustic echo cancellation (AEC) and active noise suppression (ANS) effects when you use [enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) to capture audio data and send it to the SDK for processing.
- iOS & Android: if you need to add your own audio effects and audio processing logic in addition to those of the TRTC SDK, we recommend you use version 8.3, with which you can use [setCapturedRawAudioFrameDelegateFormat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) and other APIs to set what to include in the audio data callback, for example, the audio sample rate, the number of sound channels, and the number of samples, so that you can process audio data in your preferred format.
- All platforms: if you collect video data by yourself and use the audio module of the TRTC SDK at the same time, lip-sync errors may occur. This is because the SDK has its own timeline control logic. To solve this problem, we have provided the [generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) API. When a video image frame is captured, call this API and record the PTS (timestamp), and provide the timestamp when you call [sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831).
- Windows: supported SOCKS5 proxy addresses for domain names.

**Bug fixing**
- All platforms: fixed occasional lip-sync errors for recorded content due to timestamp exceptions in audio data.
- Windows: improved the compatibility of window sharing with high DPI displays.
- Windows: added minimized windows to the shareable window list. The thumbnails of minimized windows are their application icons.
- Windows: fixed the issue of unnecessary CPU usage by DXGI after the SDK is started.
- iOS: fixed the ANR error caused by manual focus setting.
- iOS: fixed occasional failure to switch between the front and rear cameras.
- iOS: fixed VODPlayer crash when video is played back in slow motion.
- iOS: fixed the issue where audio is occasionally played via the speaker after room entry.
- iOS & Android: optimized the AEC and ANS effects and supported reverb effects for in-ear monitoring.
- Android: fixed occasional green or blurry screen during hardware decoding.
- macOS: fixed the issue where, during screen sharing with the highlighting feature enabled, the highlighted borders of the shared window flash when the window is moved near the edge of the screen.
- macOS: fixed black screen when the view rendered is moved.


## Version 8.2 Released on December 23, 2020

**New features**
- iOS & Android: supported callback of a combination of locally captured audio and all played back audio, making local recording easier.
- Android: the video rendering component TXCloudVideoView supported using `TextureView` for local rendering through the calling of the `addVideoView(new TextureView(getApplicationContext()))` API.
- Android: supported RGBA video data for custom rendering.
- Windows: supported taking screenshots of locally captured video and played back remote video. For details, see [ITRTCCloud.snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96).
- Windows: supported using `addExcludedShareWindow` and `addIncludedShareWindow` to exclude or include windows you specify, increasing the flexibility of screen sharing.
- macOS & iOS: supported calling `TRTCCloud.snapshotVideo` to take screenshots of video in the custom rendering mode.

**Quality improvement**
- Android: improved encoding quality for live streaming, enabling clearer video images.
- Windows: improved the AEC algorithm.

**Bug fixing**
- iOS: fixed occasional audio playback errors when VODPlayer and TRTC are used at the same time.
- Android: fixed black screen when custom beauty filters are used.
- Windows: fixed occasional failure to exit the current process.


## Version 8.1 Released on December 3, 2020

**New features**
- All platforms: added statistics on remote video stuttering to `onStatistics`.
- All platforms: supported using the volume adjustment API `setAudioPlayoutVolume` (100-150) to enable audio gain.
- iOS & Android: added the `setLocalVideoProcessListener` API to better support the integration of third-party beauty filters.
- C#: upgraded to the latest APIs.

**Quality improvement**
- All platforms: optimized the audio processing algorithm when earphones are used to deliver better audio quality.
- Android: optimized the audio pre-processing algorithm to reduce the impact of AEC, ANS, and AGC on audio quality.

**Bug fixing**
- iOS: fixed occasional crash when the application is force killed.
- Android: fixed the issue where beauty filters do not produce desired results when the frame rate of captured video is high.
- Windows: fixed occasional crash during screen sharing when high DPI displays are used.


## Version 8.0 Released on November 13, 2020

**Added**
- All platforms: added cross-platform C++ APIs. For more information, see cpp_interface/[ITRTCCloud.h](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html).
- All platforms: supported string-type room IDs. For more information, see `TRTCParams.strRoomId`.
- All platforms: added the device management class `TXDeviceManager`.
- All platforms: added the `TRTCCloud.switchRoom` API to allow room switching with capturing uninterrupted.
- All platforms: added the `TRTCCloud.startRemoteView` API to start rendering remote video images.
- All platforms: added the `TRTCCloud.stopRemoteView` API to stop rendering remote video images.
- All platforms: added the `TRTCCloud.getDeviceManager` API to get the device management class.
- All platforms: added the `TRTCCloud.startLocalAudio` API to enable local audio capturing and upstream data transfer.
- All platforms: added the `TRTCCloud.setRemoteRenderParams` API to configure rendering for remote images.
- All platforms: added the `TRTCCloud.setLocalRenderParams` API to configure rendering for local images.

**Optimization**
- Android: optimized the logic for switching between software and hardware decoding.
- Windows: improved audio quality and AEC for system loopback.
- Windows: optimized the audio device selection logic to reduce cases of no audio.
- Windows: reduced audio loss in double-talk scenarios.
- All platforms: optimized instant streaming for role switching in the manual subscription mode.
- All platforms: optimized the audio receiving logic, improving audio quality.
- All platforms: improved the reliability of `sendCustomCmdMsg`.

**Bug fixing**
- iOS: fixed the issue where the calling of `muteLocalVideo` suspends local video rendering.
- iOS: fixed the issue where the application occasionally freezes when a component is called during foreground-background switch.
- iOS: fixed intermittent in-ear monitoring audio when audio effects are enabled.
- Android: fixed the issue where audio effects played in the call volume mode do not stop when there is an incoming call.
- Android: fixed occasional failure to enable audio capturing.
- Windows: fixed occasional black screen during local video rendering.
- Windows: fixed occasional crash when users exit the app.
- Windows: improved support for Bluetooth earphones and fixed the no audio issue.
- Windows: fixed the focus stealing problem that occurs when screen sharing stops.
- All platforms: fixed failure to collect statistics on packet loss rate for status callback.



## Version 7.9 Released on October 27, 2020
**Added**
- macOS: supported filtering out selected windows from screen sharing. Users can exclude windows they do not want to share, better ensuring privacy.
- Windows: supported configuring the border color and width of the "Sharing" message box during screen sharing.
- Windows: supported the high performance mode during desktop sharing.
- All platforms: supported custom encryption, allowing users to process encoded audio/video data using an exposed C API.
- All platforms: added audio stuttering information `audioTotalBlockTime` and `audioBlockRate` to `TRTCRemoteStatistics`.

**Optimization**
- iOS: shortened the startup time of the audio module, allowing quicker capturing and sending of the first audio frame.
- Windows: optimized the AEC algorithm for system audio loopback.
- Windows: allowed users to filter out certain windows from screen sharing to prevent the target window from being covered.
- Android: optimized the in-ear monitoring effect for most Android devices, reducing in-ear monitoring latency to a more acceptable level.
- Android: reduced end-to-end delay in the music mode (specified in `startLocalAudio`).
- All platforms: enhanced audio smoothness when a user switches between the anchor and audience role in the manual subscription mode.
- All platforms: improved audio/video call performance and audio smoothness in poor network conditions.

**Bug fixing**
- iOS: fixed occasional failure to render video images in certain scenarios.
- iOS: fixed occasional noise when users use earphones in the default mode.
- iOS: fixed known memory leak issues.
- iOS: fixed occasional crash after ReplayKit screen recording ends.
- iOS: fixed compilation problems on simulators.
- Android: fixed occasional lip-sync errors on certain phones after the application remains in the background for a long time.
- Android: fixed the issue where the mic is not released after the application is switched to the background.
- Android: fixed the issue where certain OpenGL resources in the SDK are not released in time.
- Windows: fixed occasional noise in some scenarios.
- All platforms: fixed occasional crash, improving the SDK’s performance stability.

## Version 7.8 Released on September 29, 2020
**Added**
- macOS: added the callback of system volume change. For details, please see [TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f).
- Windows: supported specifying content for screen sharing across screens.
- Windows: supported filtering out specified windows from screen sharing to prevent the target window from being covered. For more information, please see [TRTCCloud.addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5141a9331c3675f17fbdc922f376b06) and [TRTCCloud.removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a08504ce347b593c0191904611da5cfd2).
- Windows: added the callback of system volume change. For details, please see [ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12).

**Optimization**
- iOS: allowed using VODPlayer and TRTC at the same time with AEC enabled.
- iOS & macOS: supported pushing a specified image when stream pushing pauses. For more information, please see [TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2).
- Android: supported pushing a specified image when stream pushing pauses. For more information, please see [TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d).
- Android: optimized the audio routing policy to make sure that audio is always played back via earphones when earphones are connected.
- Android: allowed low-delay capturing and playback in certain systems, reducing call delay.
- Android: supported using VODPlayer and TRTC at the same time with AEC enabled.
- Windows: made the SDK compatible with the virtual webcam e2eSoft VCam.
- Windows: allowed calling `startLocalPreview` and `startCameraDeviceTest` at the same time.
- Windows: allowed publishing screen sharing images via the primary stream and at the same time calling `startLocalPreview` to enable local preview.
- Windows: fixed long audio delay caused by the playback buffer of the SDK.
- Windows: optimized the audio enablement logic to prevent mic occupation in the playback-only mode.



**Bug fixing**
- iOS: fixed low playback volume on iPhone SE.
- iOS: fixed crash when a sub-instance (`TRTCCloud.createSubCloud`) calls `muteRemoteAudio`.
- iOS: fixed occasional crash during rendering.
- iOS: fixed the issue where video rendering on certain iPad devices occasionally causes the main thread to crash during foreground/background switching.
- iOS: fixed known memory leak issues.
- iOS: fixed the issue where iOS 14 prompts "the app would like to find and connect to devices on your local network".
- macOS: fixed the issue where `getCurrentCameraDevice` returns `nil`.
- macOS: fixed the issue where certain USB cameras cannot be turned on.
- macOS: fixed crash when the area of shared content is set to `0`.
- Android: fixed crash on Android 5.0 when the `READ_PHONE_STATE` permission is not granted.
- Android: fixed audio capturing and playback exceptions after Bluetooth earphones are disconnected and connected again.
- Android: fixed known crash issues.
- Windows: fixed crash on 64-bit Windows when screen sharing is enabled and disabled multiple times.
- Windows: fixed crash on certain systems when OpenGL is used.


## Version 7.7 Released on September 8, 2020

**Optimization**

- All platforms: improved instant streaming performance of the substream (screen sharing images).
- iOS: optimized the internal thread model to improve stability when 30 or more channels of audio/video are played back at the same time.
- iOS & Android: improved the performance of the audio module and reduced the capturing delay of the first audio frame.
- iOS & Android: improved volume and audio quality when VODPlayer and TRTC are used at the same time.
- iOS & Android: supported files in WAV format for audio effects and background music.
- Windows: fixed the issue of high CPU utilization when some low-end cameras are used.
- Windows: optimized the compatibility with multiple USB cameras and mics to make it easier to turn on such devices.
- Windows: optimized the selection policy of cameras and mics to avoid audio/video capturing exceptions caused by the connection/disconnection of cameras and mics.

**Bug fixing**

- All platforms: fixed occasional playback exceptions when the `muteLocalVideo` and `muteLocalAudio` APIs are called in poor network conditions.
- iOS: fixed occasional failure to play audio effects on earlier generations of iPhone or iPad devices.
- iOS: fixed distorted screen sharing images on iPad Pro.
- iOS: fixed the issue where the application keeps requesting screen recording permission after the user denies it.
- Windows: fixed the issue where [onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd) fails after laptops or desktops remain in sleep mode for a long time.
- Windows: fixed echo after system audio capturing is enabled via the calling of [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) in the music mode.
- Windows: fixed the issue where no audio is played sometimes when a user uses `enterRoom` and `exitRoom` to enter and leave the room in a short period of time.
- Windows: fixed project compilation problems with Visual Studio 2010.
- Windows: fixed the issue where the `onUserVideoAvailable` event callback is returned multiple times in the manual subscription mode ([setDefaultStreamRecvMode(false，false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5)).


## Version 7.6 Released on August 21, 2020
**Added**

- Windows: added the [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5211a2739df8d8ec6017559b3aa0299) and [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8c8247cbc679ea144ffb393b6b940c9e) APIs to improve user experience in adjusting HWND rendering windows in real time.
- Windows: added the [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) API to get whether the PC is muted.
- Windows: added the [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) API to turn on global mute for the PC.
- macOS: added the [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) and [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) APIs to optimize user experience in adjusting the view rendering area in real time.
- macOS: added the [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f) API to get whether the PC is muted.
- macOS: added the [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) API to turn on global mute for the PC.
- iOS: added the [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) and [updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) APIs to optimize user experience in adjusting the view rendering area in real time.
- iOS: added the [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) callback to `TRTCCloudDelegate`, and changed the names of a number of other callback functions. The names used now are [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0), [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a), and [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e).
- Android: added the [onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) callback to `TRTCCloudListener`, and changed the names of a number of other callback functions. The names used now are [onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46), [onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902), and [onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7).

**Optimization**

- All platforms: optimized the protocol policy of `enterRoom` to improve the speed and success rate of room entry.
- All platforms: fixed reduced performance and stuttering when a large number of audio channels are subscribed at the same time.
- macOS: supported sharing specified area of a specified window.

**Bug fixing**

- All platforms: fixed the issue where the SDK does not trigger the `onEnterRoom` callback when users enter the same room without exiting.
- All platforms: fixed a few internal bugs that may cause a black screen.
- All platforms: fixed failure to display screen sharing images when `startRemoteSubStreamView` is called early.
- Windows: fixed known handle and GDI leaks.
- Windows: fixed known crash issues.
- Windows: fixed the issue where cameras and mics are not started automatically after being disconnected and connected again.
- iOS: fixed crash on iOS 10 when certain file paths are passed in the background music API.
- Android: fixed the occasional no audio issue when `enterRoom` and `exitRoom` are called multiple times in a short period of time.
- Android: fixed occasional black screen during the streaming of screen recording.


## Version 7.5 Released on July 31, 2020

**Added**

- Supported dual-stack IPv6 and IPv6-only.
- Allowed playing back streams in multiple rooms. This feature can be used for ultra-small classes.
- Allowed setting a background image for MCU On-Cloud MixTranscoding (for regulatory purposes, the image must be uploaded to the TRTC console first).
- Added two new modes for MCU On-Cloud MixTranscoding: `A+B=>C` and `A+B=>A`.
- Added the `jitterBufferDelay` field, which indicates the playback buffer time, to the real-time status callback API `onStatistics`.

**Optimization**

- Reduced end-to-end delay for co-anchoring by 40% from that in version 7.4.
- Reduced in-ear monitoring delay on phones and allowed setting voice change and reverb effects for in-ear monitoring.
- Optimized the algorithm for evaluating network jitter at the player end to reduce playback delay.
- Reduced end-to-end delay for co-anchoring in TRTC SDK for Android.
- Reduced in-ear monitoring delay.
- Optimized the issue where playback view switching causes a black screen.

**Bug fixing**

- Fixed the issue where playback fails after `playBGM` and pauseBGM` are called successively in a function.
- Fixed the occasional issue where users continue to receive the `onEnterRoom` callback after exiting the room.
- Fixed the issue on certain devices where ultra-low-resolution encoding fails and cannot be recovered. 

## Version 7.4 Released on June 24, 2020 

**Optimization**

Allowed setting volume for in-ear monitoring.

**Bug fixing**

- Fixed the issue where the local image flickers during landscape/portrait mode switch on Android.
- Fixed encoding failure when custom videos are published from certain Android phones.
- Fixed occasional crash during audio packet processing.



## Version 7.3 Released on June 1, 2020

**Added**

- Added a new audio effect management API `TXAudioEffectManager` to offer more diverse audio effects while continuing to support the legacy API.
- Added the `minVideoBitrate` option to `setVideoEncoderParam`, the API used to set video encoding parameters. The option is recommended for scenarios with high requirements on video quality.

**Optimization**

- Supported transient noise reduction, which can be enabled using `setAudioQuality(TRTCAudioQualitySpeech)`.
- Supported asset packages for audio effect files.
- Improved local video clarity.
- Supported custom rendering by texture for the player end, reducing resource consumption.
- Optimized the resolution selection logic for video captured by the camera, enhancing visual experience.
- Optimized echo cancellation.
- Supported 128 Kbps high-quality stereo sound from sender to recipient, which can be set using the `setAudioQuality(TRTCAudioQualityMusic)` API.
- Supported the `SPEECH` audio mode, which provides better ANS capabilities for audio conferencing calls. This mode can be set using the `setAudioQuality(TRTCAudioQualitySpeech)` API.
- Supported playing back multiple tracks of background music at the same time. This feature can be used in karaoke scenarios, where vocals and instrumentals are separate tracks. Loop playback of background music is also supported now.
- Supported calling `muteLocalVideo` before `startLocalPreview` to preview without pushing streams. This can be achieved by calling `startLocalPreview` before `enterRoom` as well.

**Bug fixing**

- Fixed occasional crash due to OpenGL context error during custom video capturing.
- Fixed the issue where the custom rendering callback is not triggered after `setLocalVideoRenderListener` is called before room entry.
- Fixed the issue where, when a user switches to the front/rear camera in the landscape mode, other users see upside down video of the user.
- Fixed the occasional issue where, if a user calls `startLocalPreview` before room entry, other users see corrupted image of the user.
- Fixed occasional crash of the hardware encoder.
- Fixed occasional intermittent audio for local recording.
- Fixed the issue where, when the user publishing streams enters the room again after the pausing of stream pushing (`muteLocalVideo`, `muteLocalAudio`) causes crash or forces the application to close, streams are not played back automatically at the player end.



## Version 7.2 Released on April 16, 2020 

**Added**

Supported screen recording on Android, allowing users to stream screen recording on phones.

**Optimization**

- Optimized call performance on low-end and mid-range Android phones, improving audio experience.
- Optimized visual effect APIs such as filters and green screen and aggregated them into the `TXCBeautyManager` class so that they share a calling method.

**Bug fixing**

Fixed the occasional issue where the custom stream ID fails to take effect in time during role switching.



## Version 7.1 Released on March 27, 2020 

**Optimization**

- Supported static build of projects using the C++ STL library.
- Enabled ANS and AGC by default in the call volume mode to improve audio quality.
- Improved the usability of the preset stream mixing template.
- Enhanced the success rate of stream mixing.

**Bug fixing**

- Fixed the issue where all audio processing values become zero when AGC is enabled/disabled frequently during room entry.
- Fixed the issue where speed testing slows down the calling of other APIs.
- Fixed the issue where the volume of upstream data doubles and noise is heard after real-time communication is interrupted by an incoming call.
- Fixed the issue where streams are relayed automatically after room entry.



## Version 7.0 Released on March 9, 2020 

- Optimized the 3A enabling policy.
- Improved the usability of MCU On-Cloud MixTranscoding.
- Enhanced audio smoothness in poor network conditions.
- Fixed memory leaks caused by frequent room entry and exit.



## Version 6.9 Released on January 14, 2020 

**Added**

- Supported Android 10.0.
- Added the `snapshotVideo()` API for taking screenshots of local or remote video.
- Added the `pauseAudioEffect` and `resumeAudioEffect` APIs for pausing and resuming an audio effect.
- Added the `setBGMPlayoutVolume` and `setBGMPublishVolume` APIs for setting the local playback volume and publishing volume of background music respectively.
- Added the `setRemoteSubStreamViewRotation` API for adjusting the rotation of played back substream video.
- Added a global volume mode setting API `setSystemVolumeType(TRTCSystemVolumeTypeVOIP)`, which can ensure that call volume is used all the time. This is mainly to prevent the switch from Bluetooth earphones to the built-in mic during audio capturing.
- Added the `streamId` attribute to the `TRTCParams` parameter of `enterRoom`, which can be used to set the user’s CDN stream ID, making it easier to bind to live streaming CDNs.
- Added the `cloudRecordFileName` attribute to the `TRTCParams` parameter of `enterRoom`, which can be used to set the on-cloud recording filename for a live stream.
- Added the `TRTCAppSceneAudioCall` scenario, which is optimized for audio calls and can be set during the calling of `enterRoom`.
- Added the `TRTCAppSceneVoiceChatRoom` scenario, which is optimized for audio chat rooms and can be set during the calling of `enterRoom`.

**Optimization**

- Improved the recording feature’s tolerance of video interruption, enabling remote recording of more complete video.
- Fixed lip-sync errors during hardware decoding on certain devices.
- Supported capturing 1080p video, allowing PC audience to watch clearer video published from phones.
- Simplified the error codes for room entry.
- Fixed occasional slow streaming.

**Bug fixing**

- Fixed occasional crash of the HTTP component.
- Fixed the occasional issue where no callback is returned for the completion of audio effect playback.
- Fixed the occasional issue where the system cannot be recovered from room entry failures.



## Version 6.8 Released on November 15, 2019 

**Added**

- Added the in-ear monitoring capability.
- Allowed users to disable automatic stream pulling upon room entry.
- Added the `getBeautyManager` API, which aggregates beauty filter, retouching, and animated effect APIs.
- Added retouching features including skin polishing, eye brightening, teeth whitening, wrinkle removal, and eye bag removal to the Enterprise Edition.
- Added the `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` callbacks for the entry and exit of a user.

**Optimization**

- Optimized the PTS generation mechanism.
- Enabled automatic selection of the best access point after network change.
- Supported calling `startRemoteView` in advance.

**Bug fixing**

Fixed known crashes.



## Version 6.7 Released on September 30, 2019 

**Added**

- Added permission requesting configuration for AAR packaging.
- Supported CPU usage evaluation on Android 8.0 and above.

**Optimization**

- Sped up relayed push.
- Supported adjusting the playback volume of a specific user.

## Version 6.6 Released on August 2, 2019 

**Added**

- Supported local audio recording.
- Added callback APIs for sending the first audio and video frame.
- Added the system volume type setting API.
- Added the audio effect API for playing short audio effects.
- Made the data returned via the custom audio callback modifiable.

**Optimization**

- Sped up room entry and improved its success rate.
- Added an API to mute remote video.
- Unified room entry error codes, which are returned via `onEnterRoom`. If `result` is smaller than 0, it indicates failure to enter the room.
- Optimized the demo to support low-latency big rooms.
- Added a volume setting API and a volume callback API for the player.
- Supported local rendering for custom video publishing.
- Supported custom capturing and publishing of 1080p video.
- Supported the `SurfaceView` method for local and remote rendering.

**Bug fixing**

- Fixed the problems with relayed push and stream mixing.
- Fixed incorrect rotation for local preview.



## Version 6.5 Released on June 12, 2019 

**Added**

Added the "low-latency big room" feature for the live streaming mode (`TRTCAppSceneLIVE`):

- Adopted a UDP protocol optimized for audio/video, allowing the SDK to better adapt to poor network conditions.
- Reduced the average watch latency to around 1 second, enhancing anchor-audience interaction experience.
- Supported rooms with up to 100,000 users.

**Optimization**

- Fixed lip-sync errors in poor network conditions.
- Optimized the `onStatistics` status callback. Callbacks are returned for only existing streams now.
- Optimized the playback buffer logic of `TXLivePlayer`, reducing stuttering.
- Sped up playback at the player end after local video is muted via `muteLocalVideo` and unmuted again.
- Optimized the QoE algorithm for high-latency and high-packet-loss network environments.
- Improved decoder performance and fixed increasing delay on earlier generations of Android phones.
- Optimized the volume evaluation algorithm (`enableAudioVolumeEvaluation`), improving accuracy.
- Optimized the QoE algorithm in the video call mode (`TRTCAppSceneVideoCall`), further enhancing the smoothness of one-to-one calls in poor network conditions.

  

**Bug fixing**

- Fixed the occasional issue where no callback is returned for `enterRoom`.
- Fixed the issue where a user cannot play audio after disabling audio capturing.
- Fixed green screen after the local rendering view is removed and added again.
- Fixed the issue where the custom rendering callback (`setRemoteVideoRenderDelegate`) is returned only 10 times at most when the resolution of the remote video is 540p or above.



## Version 6.4 Released on April 25, 2019 

**Added**

- Added APIs for mirroring local video and encoded video.
- Added a callback for the `setMixTranscodingConfig` API.
- Added the eye enlarging, face slimming, chin slimming, and animated widget features to the Enterprise Edition.

**Optimization**

- Improved smoothness in poor network conditions.
- Optimized the volume callback algorithm, improving the accuracy of the values returned.
- Supported specifying data frame timestamps externally for the publishing of custom audio and video.
- Optimized the `setMixTranscodingConfig` API by adding the `roomID` parameter for stream mixing during cross-room co-anchoring.
- Optimized the `setMixTranscodingConfig` API by adding the `pureAudio` parameter for audio mixing and recording in audio-only call scenarios.
- Improved the 720p video decoding performance on low-end Android devices.

**Bug fixing**
- Fixed failure to switch to the hands-free mode.
- Fixed the occasional issue where live streaming (TXLivePlayer) latency increases and does not fall back.
- Fixed failure to use `setVideoEncoderRotation` in live streaming scenarios.
- Fixed the issue where no error callback is returned after the mic permission is denied on Android.
- Fixed the issue where a window pops up after the demo is opened on Android 9.0.
- Fixed failure by audience to adjust the volume using the volume buttons.



## Version 6.3 Released on April 2, 2019 

**Added**

- Supported 64-bit Android.
- Added a custom video capturing API: TRTCCloud > sendCustomVideoData.
- Added a custom audio capturing API: TRTCCloud > sendCustomAudioData.
- Added custom video rendering APIs: TRTCCloud > setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate.
- Added a custom audio data callback API: TRTCCloud > setAudioFrameDelegate, which you can use to do the following:
  - Return the data captured by the mic: TRTCAudioFrameDelegate > onCapturedAudioFrame.
  - Return the audio data of each remote user: TRTCAudioFrameDelegate > onPlayAudioFrame.
  - Return the mixed audio data sent to the speaker for playback: TRTCAudioFrameDelegate > onMixedPlayAudioFrame.





## Version 6.2 Released on March 8, 2019 

**Added**

- Added the filter strength setting API `setFilterConcentration()`.
- Added the `sendSEIMsg()` API for sending custom messages through SEI headers in video frames. The feature is mainly used to insert timestamp information into video streams.
- Added the cross-room call feature `connectOtherRoom`, which allows two existing TRTC rooms to communicate with each other. This feature can be used to enable anchor competition across rooms.



**Optimization**

- Improved CPU utilization and stability.
- Enhanced video clarity in poor network conditions.
- Disabled the creation of multiple `TRTCCloud` instances and restricted instance creation to singletons. This can avoid cases where different instances of `TRTCCloud` compete for network resources, which compromise user experience.

**Bug fixing**

Fixed the problems with relayed push in audio-only call scenarios (such as Werewolf playing). You must specify the `bussInfo` field in `TRTCParam` to use the feature.



## Version 6.1 Released on January 31, 2019 

**Optimization**

- Supported watching screen sharing streams.
- Supported publishing custom video.
- Optimized CDN live streaming and stream mixing.
- Introduced two types of scenarios: live streaming and video calls, which are specified during room entry.
- Enhanced stability and fixed occasional crash.
- Optimized QoS control and improved performance in poor network conditions.



## Version 6.0 Released on January 18, 2019 

**Optimization**

- Updated the architecture to the LiteAV kernel.
- Adopted a new QoS algorithm, reducing stuttering and improving smoothness.
- Introduced a new audio module, enhancing audio quality in various network conditions.
- Supported dual-channel (primary stream and substream) encoding. We recommend you use this feature on Windows and macOS only.
- Supported CDN live streaming and stream mixing.
