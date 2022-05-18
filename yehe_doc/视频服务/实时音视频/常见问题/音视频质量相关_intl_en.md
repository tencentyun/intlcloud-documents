## 1. Video

[](id:v1)
### How do I remove the black bars in a TRTC video image?
You can solve this problem by setting `TRTCVideoFillMode_Fill` (rendering mode). TRTC has two video rendering modes: fill and fit. You can set the rendering mode of the local image using `setLocalViewFillMode()` and that of a remote image using `setRemoteViewFillMode`.
- TRTCVideoFillMode_Fill: The image fills the entire screen, and the excess parts are cropped. The image may not be displayed in whole.
- TRTCVideoFillMode_Fit: The image is stretched as large as the long side can go, and the blank area is filled with black bars. The image is displayed in whole.

[](idv2:)
### How do I fix stutter?
You can check call quality by room ID or user ID in **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)** in the TRTC console.
- Check the send and receive statistics from the recipient’s perspective.
- Check the send and receive packet loss. High packet loss suggest that the stutter may be caused by unstable network connections.
- Check the frame rate and CPU usage. Both low frame rates and high CPU usage can cause stutter.

[](id:v3)
### How do I fix low-quality, blurry and pixelated videos?
- Resolution is mainly associated with bitrate. Check whether the bitrate is set too low. Pixelation tends to occur when resolution is high but bitrate low.
- With its on-cloud QoS control policy, TRTC dynamically adjusts bitrate and resolution based on network conditions. It reduces the bitrate in case of poor network connections, which leads to decreased resolution.
- Check whether the `VideoCall` or `Live` mode is used during room entry. Because the `VideoCall` mode is designed for calls and features low latency and smoothness, it tends to sacrifice video quality for smoothness when network connections are poor. We recommend that you use the `Live` mode for application scenarios with high requirements on video quality.

[](id:v4)
### Why are the local preview and image seen by remote users horizontally reversed?
Images captured by the local camera are mirrored by default. For native applications, you can use [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) to set the mirror mode of the local preview, or `setVideoEncoderMirror` to set the mirror mode of encoded images, that is, images seen by remote users and recorded by the server. On web, you can set the mirror mode by specifying the `mirror` parameter when calling [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream).

[](id:v5)
### Why doesn’t my orientation setting for encoded video take effect?
You need to set `setGSensorMode()` to `TRTCGSensorMode_Disable` to disable gravity sensing; otherwise, the orientation of video seen by remote users will not change even after you call `setVideoEncoderRotation`.

[](id:v6)
### Upstream data transfer is normal, but why can’t I pull data from CDNs and why can’t remote users see an image?
Make sure you have enabled relayed to CDN in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Function Configuration**.

[](id:v7)
### What should I do if preview/playback images are rotated?
- **If you use the TRTC SDK to capture camera data**:
  - Update the TRTC SDK to the latest version.
  - If you use special devices, you can call the local preview rotation API `setLocalViewRotation`, remote image rotation API `setRemoteViewRotation`, and encoded image rotation API `setVideoEncoderRotation` to adjust the rotation. For detailed directions, see [Video Rotation](https://intl.cloud.tencent.com/document/product/647/35154).
-**If you capture video data by yourself**:
  - Update the TRTC SDK to the latest version.
  - Check the original rotation of the video you capture.
  - Send the video data to the TRTC SDK and check whether a rotation angle is specified for `TRTCCloudDef.TRTCVideoFrame`.
  - If you use special devices, you can call the local preview rotation API `setLocalViewRotation`, remote image rotation API `setRemoteViewRotation`, and encoded image rotation API `setVideoEncoderRotation` to adjust the rotation. For detailed directions, see [Video Rotation](https://intl.cloud.tencent.com/document/product/647/35154).

[](id:v8)
### Why are videos mirrored?
When a user uses the front camera, his or her video will be mirrored, and the local preview and video seen by remote users will be horizontally reversed.

[](id:v9)
### How do I publish streams in landscape mode?
You may want to publish streams in landscape mode in certain scenarios, for example, if you use TVs for live streaming. For how to implement this, see [Video Rotation](https://intl.cloud.tencent.com/document/product/647/35154).

[](id:v10)
### What are the causes of black screen during live streaming?
- Playback or decoding failure. Please refer to the solutions to playback failure.
- Metadata issue. For example, the metadata contains only audio stream information, but there is also video in the actual data or there is only audio at the beginning but video is added later. If this is the case, we recommend you modify the metadata of the source stream.
- There are only frames such as SEI but no image information in encoded video data. As a result, there are no images to decode, hence the black screen. This usually occurs with custom video data.

[](id:v11)
### What are the causes of blurry or green screen during live streaming?
- Missing of I-frames. Both P- and B-frames rely on I-frames to decode, so if I-frames are missing, the decoding of P- and B-frames will fail, resulting in ghosting, or blurry or green screen. Use different players such as FFplay, VLC, and PotPlayer to play the stream at the same time. If blurry or green screen occurs on all players, the problem probably lies in the source stream, and you need to check your source stream.
- Change of metadata. Most players parse metadata only before decoding to configure decoding parameters. In case of video changes, for example, if the resolution changes, but the player doesn’t update the decoding parameters, the blurry or green screen issue may occur. The best solution to this issue is keeping encoding parameters unchanged during live streaming so that the metadata does not change.
- Compatibility issues of hardware encoders/decoders. This problem is usually found on Android devices. The hardware encoders/decoders of some Android devices are not well implemented and has poor compatibility. If this is the case, we recommend you switch to software encoders/decoders.
- Use of different color formats for publishing and playback. For example, if NV12 is used for publishing and I420 is used for playback, the issue of blurry or green screen may occur during decoding. To solve this, make sure the same color format is used for publishing and playback.



## 2. Audio

[](id:a1)
### What should I do if the audio volume is low when I use TXVodPlayer to play videos during a TRTC call?
Call the `setSystemVolumeTyp` API to set the system volume type used during the call to `TRTCSystemVolumeTypeMedia` (media volume mode).

[](id:a2)
### How do I select the media or call volume type?
You can call the `setSystemVolumeType` API to select the media or call volume type as needed.
- TRTCAudioVolumeTypeAuto (default): The call volume type is used when the mic is on and the media volume type is used when the mic is off.
- TRTCAudioVolumeTypeVOIP: The call volume type is always used.
- TRTCAudioVolumeTypeMedia: The media volume type is always used.


[](id:a4)
### What should I do if the audio volume is low?
- If **the volume is low for all users**, then it is an upstream issue.
  - Check whether `volume` is set to lower than 50 in the [setCurrentDeviceVolume](http://doc.qcloudtrtc.com/group__ITXDeviceManager__csharp.html#a1c9517a8a6a23558b4bd40c41eb97ee5) API for Windows and macOS or the [setAudioCaptureVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a53681962139b81140f2d66abc4ea6a0f) API for all platforms. If so, set it to a larger value.
  - Check whether automatic gain control (AGC) is enabled.
  - Check whether the use of Bluetooth earphones caused the problem.
-If **the volume is low for only some users**, then it is a downstream issue.
  - Check whether `volume` is set to lower than 50 in the [setAudioPlayoutVolume](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a9b8946403b8b3ac8e11f3a78e9d531ca) or [setCurrentDeviceVolume](http://doc.qcloudtrtc.com/group__ITXDeviceManager__csharp.html#a1c9517a8a6a23558b4bd40c41eb97ee5) API. If so, set it to a larger value.
  - On mobile phones, check whether the `setAudioRoute` API was called to switch to the receiver for playback.

[](id:a5)
### What should I do if audio stutters?
Open [Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor), go to the end-to-end details page, and select the **Audio** tab.
- In **Device Status**, if the CPU usage of the receiver and sender exceeds 90%, close other processes running in the background.
- If there are marked upstream and downstream packet loss and major fluctuations in RTT, it indicates poor network conditions. Change to a different network.

[](id:a6)
### Why do I hear echo?
The echo issue is common if the call participants are close to each other. Please ensure a certain distance between call participants when testing. Also, check whether you have unintentionally disabled acoustic echo cancellation (AEC).

[](id:a7)
### What should I do if audio is of low quality and the volume keeps changing?
This problem occurs if you use an external sound card and enable in-ear monitoring at the same time. This is because sound cards are often built in with in-ear monitoring. Please disable in-ear monitoring when you use an external sound card.

[](id:a8)
### What should I do if there is echo or noise during a call or the volume of a call is small?
The issues are common if the call participants are close to each other. Please ensure a certain distance between call participants when testing. If a non-web client hears echo or noise from a web client, it indicates that 3A is not working on web. If you use the browser’s built-in API [getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia) for custom capturing, you need to enable 3A manually using the parameters below:
- `echoCancellation`: echo cancellation
- `noiseSuppression`: noise suppression
- `autoGainControl`: automatic gain control

If you use the [TRTC.createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream) API for capturing, you don’t need to set the 3A parameters manually. The TRTC SDK enables 3A by default.

## 3. Others

[](id:q1)
### How do I monitor network status and display signal strength in TRTC?
You can use `onNetworkQuality()` to monitor the current upstream and downstream network quality. To display signal strength, on Android, for example, refer to [TRTC-API-Example](https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example/Advanced/SpeedTest).

[](id:q2)
### Why is my camera or mic occupied?
When the `exitRoom()` API is called, logic such as the release of audio/video devices and codecs will be executed. Releasing devices is an async operation. After the release, the SDK will use the `onExitRoom()` callback in `TRTCCloudListener` to notify the upper layer. Please wait until you receive the `onExitRoom()` callback before you call `enterRoom()` again or switch to another audio/video SDK.

[](id:q3)
### How do I know whether the camera is enabled successfully?
If the `onCameraDidReady` callback is received, the camera is ready.

[](id:q4)
### How do I know whether the mic is enabled successfully?
If the `onMicDidReady` callback is received, the mic is ready.

[](id:q5)
### What should I do if the camera fails to be turned on?
- Check whether you have granted access to the camera. 
- The TRTC SDK supports external cameras, which are required if you use TVs or set-top boxes. Check whether the external camera is properly connected to your device.

[](id:q6)
### What technical metrics does TRTC use?
>! The following applies to iOS, macOS, Android, and Windows.

The TRTC SDK offers the `onStatistics (TRTCStatistics statics)` callback. Every 2 seconds, the callback returns statistics on technical metrics including `appCpu` (app CPU usage), `systemCpu` (system CPU usage), `rtt` (latency), `upLoss` (upstream packet loss), `downLoss` (downstream packet loss), and audio/video statistics of the local user and remote users. For details, see [TRTCStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatisic__ios.html#interfaceTRTCStatistics).

