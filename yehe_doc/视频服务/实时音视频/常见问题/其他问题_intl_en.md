[](id:que1)
### How do live streaming, interactive live streaming, TRTC, and relayed live streaming differ from and relate to each other?
- Live streaming (keywords: one-to-many, RTMP/HLS/HTTP-FLV, CDN)
 Live streaming consists of the push end, the playback end, and the cloud live streaming service. Streams are pushed over the universal protocol RTMP, delivered through CDNs, and can be watched over protocols including RTMP, HTTP-FLV, or HLS (for HTML5).
- Interactive live streaming (keywords: co-anchoring, anchor competition)
 In interactive live streaming, audience can co-anchor with anchors and anchors from different rooms can compete with each other.
- TRTC (keywords: multi-person interaction, UDP-based proprietary protocol, low-latency)
 The main application scenarios for TRTC (Tencent Real-Time Communication) are audio/video interaction and low-latency live streaming. It uses a UDP-based proprietary protocol and can keep the latency as low as 100 ms. Typical applications include QQ calls, VooV Meeting, and online group classes. TRTC is supported by mainstream platforms including iOS, Android, and Windows and can communicate with WebRTC. It supports relaying streams to CDNs through on-cloud stream mixing.
- Relayed live streaming (keywords: on-cloud stream mixing, RTC relayed live streaming, CDN)
 The relayed live streaming technology replicates multiple streams in a low-latency co-anchoring room and mixes them into one stream in the cloud before pushing it to a live streaming CDN for delivery and playback. 


[](id:que2)
### The demo is running on two devices, but why can't they display the images of each other?
Make sure that the two devices use different `UserIDs`. With TRTC, you cannot use the same `UserID` on two devices simultaneously unless the `SDKAppIDs` are different.

[](id:que3)
### When there is only one user in a room, why is CDN playback stuttering and blurry?
Please set the `TRTCAppScene` parameter in `enterRoom` to **TRTCAppSceneLIVE*.
The `VideoCall` mode is optimized for video calls, so when there is only one user in a room, TRTC tends to maintain a low bitrate and frame rate to reduce traffic usage, which makes the video choppy and blurry.

[](id:que4)
### Why can't I enter any online room?

This may be because advanced permission control is enabled. If you enable advanced permission control for an application (`SDKAppid`), users must pass `PrivateMapKey` in TRTCParams` to enter the rooms under the application. Therefore, if your online business is running, and you haven’t integrated into it the `privateMapKey` logic, please do not enable the feature. For more information, please see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157).



[](id:que5)
### How do I view TRTC logs?
TRTC logs are compressed and encrypted by default with the XLOG extension. You can set `setLogCompressEnabled` to specify whether to encrypt logs. If a log filename contains `C` (compressed), the log is compressed and encrypted; if it contains `R` (raw), the log is in plaintext.

- iOS/macOS: `Documents/log` of the application sandbox
- Android:
 - 6.7 or below: `/sdcard/log/tencent/liteav`
 - 6.8 or above: `/sdcard/Android/data/package name/files/log/tencent/liteav/`
- Windows: `%appdata%/tencent/liteav/log`
- Web: open the browser console or use vConsole to log the printed SDK information

>?
>- You need to download a decryption tool to view an XLOG file. Place the tool in the same directory of the XLOG file in Python 2.7 and run `python decode_mars_log_file.py`.
>- You can download the log decryption tool at `dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`.


[](id:que6)
### What should I do if a 10006 error occurs?
If the "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether your TRTC application service is available.
Log in to the TRTC console, click **[Application Management](https://console.cloud.tencent.com/trtc/app)**, find the application you created, and click **Application Info** to view the service status.
![](https://main.qcloudimg.com/raw/57e63830a368520c5e81e8e4b43d09b7.png)

[](id:que7)
### Why is the error code “-100018” returned during room entry?
This error is a result of `UserSig` verification failure, which may be caused by the following reasons:
- The `SDKAppID` parameter passed in is incorrect. You can log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)** to view the `SDKAppID`.
- The `UserSig` passed in, which should match the `UserID`, is incorrect. To verify your `UserSig`, log in to the TRTC console and click **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.


[](id:que8)
### How do I make a cross-room call (anchor competition)?
You can make a cross-room call using the `connectOtherRoom` API. Anchor A calls `connectOtherRoom()` to connect to anchor B and gets the result via the `onConnectOtherRoom` callback. All users in anchor A’s room will be notified via the `onUserEnter` callback that anchor B has entered the room, and all users in anchor B’s room will be notified via the `onUserEnter` callback that anchor A has entered the room.

[](id:que9)
### Why is my camera or mic occupied?
When the `exitRoom()` API is called, the logic related to room exit will be executed, such as releasing resources of audio/video devices and codecs. Release of hardware devices is an async operation. After resources are released, the SDK will use the `onExitRoom()` callback in `TRTCCloudListener` to notify the upper layer. If you want to call `enterRoom()` again or switch to another audio/video SDK, please do so after receiving the `onExitRoom()` callback.

[](id:que10)
### Do I have to call the `exitRoom()` API?
After you call `enterRoom`, regardless of whether room entry succeeds, you must call `exitRoom` before calling `enterRoom` again; otherwise, an unexpected error will occur.

[](id:que11)
### How do I remove the black bars in a TRTC video image?
You can solve this problem by setting `TRTCVideoFillMode_Fill` (fill mode). TRTC has two video rendering modes: fill and fit. You can set the rendering mode of the local image through `setLocalViewFillMode()` and that of a remote image through `setRemoteViewFillMode`.
- TRTCVideoFillMode_Fill: The image fills the entire screen, and the excess parts are cropped. The image may not be displayed in whole.
- TRTCVideoFillMode_Fit: The long side of the image is stretched to fit the screen, and the blank area is filled with black bars. The image is displayed in whole.

[](id:que12)
### Why are the local and remote images of TRTC horizontally reversed?
Locally captured images are mirrored by default. Application users can use [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) to set the mirror mode of the local camera preview, or `setVideoEncoderMirror` to set the mirror mode of encoded images, i.e., images viewed by remote users and recorded by the server. Web users can set the mirror mode by specifying the `mirror` parameter when calling [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream). 


[](id:que13)
### Why doesn’t my orientation setting for encoded video take effect?
You need to set `setGSensorMode()` to `TRTCGSensorMode_Disable` to disable gravity sensing; otherwise, after `setVideoEncoderRotation` is called, the orientation of video watched by remote users will not change.

[](id:que14)
### What should I do if the volume is low when I use TXVodPlayer during a TRTC call?
You can use the `setSystemVolumeTyp` API to set the system volume type used during the call to `TRTCSystemVolumeTypeMedia` (media volume mode).

[](id:que15)
### Upstream data transfer is normal, but why does relayed pull fail and why can’t remote users see an image?	
Make sure you have enabled relayed push in **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Function Configuration**.


[](id:que16)
### What are the formats of the recording files generated in different relayed recording scenarios?	
Recording files are generated in whatever format specified in the [TRTC console](https://console.cloud.tencent.com/trtc).

[](id:que17)
### How do I select the media or call volume type?
You can call the `setSystemVolumeType` API to select the media or call volume type as needed.
- TRTCAudioVolumeTypeAuto (default): The call volume type is used when the mic is on and the media volume type is used when the mic is off.
- TRTCAudioVolumeTypeVOIP: The call volume type is always used.
- TRTCAudioVolumeTypeMedia: The media volume type is always used.

[](id:que18)
### How do I know whether the camera is enabled successfully?
If the `onCameraDidReady` callback is received, the camera is ready.

[](id:que19)
### How do I know whether the mic is enabled successfully?
If the `onMicDidReady` callback is received, the mic is ready.

[](id:que20)
### How do I know whether an audio/video stream is published successfully?
You know when you receive the `onSendFirstLocalVideoFrame` callback. After `enterRoom` and `startLocalPreview` are called successfully, the SDK will capture video from the camera and encode the video captured. It will return this callback after sending the first video frame to the cloud.

[](id:que21)
### How do I know whether a stream is published successfully in an audio call?
You know when you receive the `onSendFirstLocalAudioFrame` callback, After `enterRoom()` and `startLocalAudio()` are called successfully, the SDK will capture audio from the mic and encode the audio captured. It will return this callback after sending the first audio frame to the cloud.

[](id:que22)
### Can I query all `UserID` values?
Currently, statistics of all `UserID` values are not available. After user accounts are successfully signed up on the client, you can write all user information into SQL for management and query.


[](id:que23)
### Can users with the same `UserID` be in the same room at the same time?
In TRTC, users with the same `userID` cannot be in the same room at the same time as it will cause a conflict.

[](id:que24)
### Why doesn't the audio route (receiver/speaker) configured via the `setAudioRoute` API take effect?	
You can switch between the receiver and speaker only in the call volume mode. That is to say, the API works only if two or more users are co-anchoring.


[](id:que25)
### In addition to enabling auto-recording in the console, how can I manually enable recording for a call?
You can manually enable recording for a call in the following steps:
1. In the TRTC console, click **[Application Management](https://console.cloud.tencent.com/trtc/app)** > **Function Configuration**, enable relayed push, and disable on-cloud recording.
2. After a user (`userid`) enters a room, splice the user’s `streamid` according to the stream ID generation rule.
3. Use the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API of CSS to start a recording task for the `streamid`.
 - Set `DomainName` to `[bizid].livepush.myqcloud.com`.
 - Set `AppName` to `trtc_[sdkappid]`.
 - Set `StreamName` to `streamid`.
4. After the recording task is completed, CSS will save the file in VOD and notify you via the [recording callback](https://intl.cloud.tencent.com/document/product/267/38080).

[](id:que26)
### How does TRTC verify `UserSig`? How do I troubleshoot the “-3319” or “-3320” error during room entry?	
Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)** to verify your `UserSig`.

[](id:que27)
### How do I view my call duration and usage?	
You can find the information on the **[Usage Statistics](https://console.cloud.tencent.com/trtc/statistics)** page of the TRTC console.

[](id:que28)
### How do I maintain the user list and count the number of users in a TRTC room?	
If you have integrated [IM](https://intl.cloud.tencent.com/document/product/1047) into your project, you can use the IM group user counting API to calculate the number of users in a room. However, such calculation is not always accurate. You may use this method if you don’t have a high requirement on accuracy.
If you do have a high requirement on the accuracy of the calculation, we recommend you implement the following calculation logic:
1. Increase the user count (client -> server): Whenever a user enters the room, increase the user count by 1. To achieve this, you can make the user’s client send a count increasing request to the server upon room entry.
2. Decrease the user count (client -> server): When a user leaves a room, decrease the user count by 1. To achieve this, you can make the user’s client send a count decreasing request to the server during room exit.

[](id:que29)
### A “-100013” error is reported during room entry, with the error message “ERR_SERVER_INFO_SERVICE_SUSPENDED”. What should I do?	
This error indicates that the service is unavailable. Please check the following:
- Whether you have used up your package
- Whether your Tencent Cloud account has overdue payment

[](id:que30)
### How do I monitor network status and display signal strength in TRTC?	
You can use `onNetworkQuality()` to monitor the current upstream/downstream network quality and refer to the [official demo](https://github.com/tencentyun/TRTCSDK) to display signal strength.

[](id:que31)
### How do I know whether the new MCU stream mixing scheme or legacy on-cloud stream mixing scheme is used?
If the following conditions are met and `mcumix = 1` is printed in the client log, the new MCU stream mixing scheme is used:
- The application is created on or after January 9, 2020.
- The version of the TRTC SDK is v6.9 or above.

[](id:que32)
### What should I do if the stream mixing API fail to work?
1. Make sure you have enabled relayed push in the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Listen for `onSetMixTranscodingConfig()` and make modifications based on the error message returned.
3. If a relayed stream ID is specified through an SDK API, the legacy on-cloud stream mixing scheme will fail.
4. If the `onSetMixTranscodingConfig()` callback indicates that stream mixing is successful, but no mixed stream can be pulled via CDN, it may be caused by failure to set a playback domain name. Please check the configuration of your playback domain name.

[](id:que33)
### What should I do if I have enabled on-cloud recording but no recording files are generated?
1. Make sure you have enabled relayed push and on-cloud recording in the [TRTC console](https://console.cloud.tencent.com/trtc).
2. TRTC starts recording only if there is a user publishing audio/video data in a room.
3. A recording file will be generated only if CDN relayed pull is successful.
4. If there is only audio in a room at first before video is published, depending on the recording template configured, the recording file generated may contain only the video segment or the audio-only segment.

[](id:que34)
### How do I fix stutter?
You can check call quality by `RoomID` or `UserID` in **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)** in the TRTC console.
- Check the send and receive statistics from the recipient’s perspective.
- Check the send and receive packet loss. High packet loss suggest that the stutter may be caused by unstable network connections.
- Check the frame rate and CPU usage. Both low frame rates and high CPU usage can cause stutter.

[](id:que35)
### How do I fix low-quality, blurry and pixelated videos?
- Resolution is mainly associated with bitrate. Check whether the bitrate is set too low. Pixelation tends to occur when resolution is high but bitrate low.
- TRTC dynamically adjusts bitrate and resolution based on network conditions according to its on-cloud QoS control policy. It reduces the bitrate in case of poor network connections, which leads to decreased definition.
- Check whether the `VideoCall` or `Live` mode is used during room entry. As the `VideoCall` mode is designed for calls and features low latency and smoothness, it tends to sacrifice video quality for smoothness when network connections are poor. We recommend that you use the `Live` mode for application scenarios with high requirements on video quality.


[](id:que36)
### How do I give the room ID to the co-anchor I invite?
You can insert the room ID in a custom message. The invitee can get the room ID after parsing the message. For details, please see [Message Sending and Receiving](https://intl.cloud.tencent.com/document/product/1047/34322) and [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391).

[](id:que37)
### Is it possible to start audio recording only if there are two or more users in a room?
Yes, it is. If you want to record mixed audio data, call [On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618) first, specifying the output stream ID, and call the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API of CSS.

 [](id:que38)
### How do I capture the audio played back by the shared application on Windows?
You can call [startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) to enable system audio capturing.

[](id:que39)
### How to implement the feature that allows anchors to invite audience to audio/video interaction in the conference mode on Windows?
You need to use another Tencent Cloud product, [IM](https://intl.cloud.tencent.com/document/product/1047/33996), to enable the feature.

This is how it works: A sends a custom message X (you can determine how the message is displayed) to B, and the calling page is triggered; B receives X and the called page is triggered; B uses [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) to enter the room and sends a custom message X1 to A; A receives X1 (you can determine whether to display the message) and uses `enterRoom` to enter the room. The messages are sent via IM.

[](id:que40)
### How do audience watch the videos of co-anchors in a room?
In live streaming scenarios, audience get the `userid` of anchors in a room via the [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) callback in `TRTCCloudDelegate` (co-anchoring users enter the room via [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b) and are also anchors for audience). They then call [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9) to play the videos of the anchors.
For more information, please see [Live Streaming Mode > Windows](https://intl.cloud.tencent.com/document/product/647/35109).

[](id:que41)
### Is there a TRTC SDK for Linux?
The TRTC SDK for Linux is not commercially available yet. If you have questions about the SDK or want to use it, please contact us at colleenyu@tencent.com.