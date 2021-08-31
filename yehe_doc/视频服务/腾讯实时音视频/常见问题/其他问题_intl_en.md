<span id="que1"></span>
### What are the differences and relationships between LVB, ILVB, TRTC, and relayed live streaming?
- LVB (keywords: one-to-many, RTMP/HLS/HTTP-FLV, CDN)
 LVB consists of the push end, playback end, and LVB cloud service. The LVB cloud service uses CDN to deliver live streams, which are pushed over the universal standard protocol RTMP. After being delivered by CDN, live streams can be watched over protocols such as RTMP, HTTP-FLV, or HLS (for HTML5).
- ILVB (keywords: co-anchoring, anchor competition)
 ILVB is a live streaming mode where the anchor and viewers can interact through co-anchoring and different anchors can compete with each other.
- TRTC (keywords: multi-person interaction, UDP-based proprietary protocol, low-latency)
 Real-time communication (RTC) is mainly applicable to audio/video interaction and low-latency live streaming. With the aid of a UDP-based proprietary protocol, its latency can be reduced to 100 ms, which is ideal for scenarios such as QQ call, VooV Meeting, and online big classes. Tencent Real-Time Communication (TRTC) supports mainstream platforms including iOS, Android, Windows, Mini Program, and WebRTC and can relay live streams to CDN through on-cloud stream mix.
- Relayed live streaming (keywords: on-cloud stream mix, RTC relayed live streaming, CDN)
 The relayed live streaming technology replicates and mixes multiple pushed streams in a low-latency co-anchoring room into one stream in the cloud and then pushes the mixed stream to CDN for delivery and playback. 

<span id="que2"></span>
### The demo is running on two devices, but why can't they display the images of each other?
Please make sure that the two devices use different `UserID` values when running the demo, as TRTC does not support using the same `UserID` on two devices simultaneously, unless different `SDKAppID` values are used.

<span id="que3"></span>
### During CDN live watching, there is only one user in the room, but the video image is lagging and blurry. Why?
Please specify the `TRTCAppScene` parameter in `enterRoom` as **`TRTCAppSceneLIVE`**.
The `VideoCall` mode is optimized for video calls, so when there is only one user in the room, the video image will maintain a low bitrate and frame rate to reduce network traffic usage, which will look lagging and blurry.

<span id="que4"></span>
### Why can't I enter any online room?

This may be because that room permission control has been enabled. Once room permission control is enabled, all rooms under the current `SDKAppID` can be entered only after `privateMapKey` is set in `TRTCParamEnc`, so if your online business is in operation and the relevant logic of `privateMapKey` has not been added to it, please do not enable this feature. For more information, please see [Configuring Permission for Entering Room](https://intl.cloud.tencent.com/document/product/647/35157).


<span id="que5"></span>
### How do I view TRTC logs?
TRTC logs are compressed and encrypted by default in the `.xlog` extension. You can set `setLogCompressEnabled` to specify whether to encrypt logs. If the generated log filename contains `C (compressed)`, the log is compressed and encrypted; if it contains `R (raw)`, the log is in plaintext.

- iOS/macOS: `Documents/log` of `sandbox`
- Android:
 - 6.7 or below: `/sdcard/log/tencent/liteav`
 - 6.8 or above: `/sdcard/Android/data/package name/files/log/tencent/liteav/`
- Windows: `%appdata%/tencent/liteav/log`
- Web: open the browser console or use vConsole to log the printed SDK information
- Mini Program: enable the `debug` attribute of the &lt;live-pusher&gt; and &lt;live-player&gt; tags and use vConsole to log the printed information

>?
>- You need to download the decryption tool to view a .xlog file. Place the tool in the same directory of the .xlog file in Python 2.7 and directly run `python decode_mars_log_file.py` to launch the tool.
>- Download address of log decryption tool: `dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`.
 
 <span id="que6"></span>
### What should I do if a 10006 error occurs?
If "Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it" is displayed, please check whether your TRTC application service is available.
Log in to the [TRTC Console](https://console.cloud.tencent.com/rav), click the application you created, click **Account Info**, and you can view the service status in the account information tab.
![](https://main.qcloudimg.com/raw/57e63830a368520c5e81e8e4b43d09b7.png)

<span id="que7"></span>
### Why is error code -100018 returned for room entry?
This error is due to a `UserSig` verification failure, which may be caused by the following:
- The `SDKAppID` parameter passed in is incorrect. You can log in to the TRTC Console, select **[Application Management](https://console.cloud.tencent.com/trtc/app)**, and view the corresponding `SDKAppID`.
- The corresponding verification signature `UserSig` passed in for the `UserID` parameter is incorrect. You can log in to the TRTC Console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)** to verify the `UserSig`.

<span id="que8"></span>
### How do I implement cross-room co-anchoring (anchor competition)?
The `connectOtherRoom` API can be used. After calling `connectOtherRoom()`, the anchors can get the cross-room competition result through the `onConnectOtherRoom` callback. All users in the room of anchor A/B will receive the notification of anchor B/A's room entry through the `onUserEnter` callback.

<span id="que9"></span>
### Why do exceptions such as occupied device camera or mic occur?
When the `exitRoom()` API is called, the logic related to room exit will be executed, such as releasing resources of audio/video devices and codecs. Release of hardware devices is an async operation. After resources are released, the SDK will use the `onExitRoom()` callback in `TRTCCloudListener` to notify the upper layer. If you want to call `enterRoom()` again or switch to another audio/video SDK, please do so after receiving the `onExitRoom()` callback.

<span id="que10"></span>
### Is it necessary to call the exitRoom() API?
No matter whether room entry is successful, `enterRoom` must be used together with `exitRoom`. If `enterRoom` is called again before `exitRoom` is called, an unexpected error will occur.

<span id="que11"></span>
### How do I remove the black bars in the TRTC video image?
You can solve this problem by setting `TRTCVideoFillMode_Fill` (fill mode). The video rendering modes of TRTC include fill and fit. You can set the rendering mode of the local or remote image through `setLocalViewFillMode()` or `setRemoteViewFillMode`, respectively.
- TRTCVideoFillMode_Fill: the entire screen will be covered by the image, where parts that exceed the screen will be cropped, so the displayed image may be incomplete.
- TRTCVideoFillMode_Fit: the long side of the image will fit the screen, while the short side will be proportionally scaled with unmatched areas being filled with black color blocks, but the displayed image is definitely complete.

<span id="que12"></span>
### Why are the local and remote images of TRTC horizontally reversed?
The locally captured image is horizontally reversed by default, which can be set through the [setLocalViewMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html?&_ga=1.239476867.1286123284.1593759269#setLocalViewMirror) API on App. This API changes only the mirroring mode of the preview image of the local camera. You can also use the `setVideoEncoderMirror` API to set the mirroring mode of the image output by the encoder. This API does not change the preview image of the local camera; instead, it changes the video image viewed by the remote user (and recorded by the server).  Moreover, you can set this on web by using [createStream](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?&_ga=1.196570732.1964829293.1601453695#.createStream) API to modify `mirror` parameter.

<span id="que13"></span>
### Why doesn't the set video encoding output direction take effect in TRTC?
You need to set `setGSensorMode()` to `TRTCGSensorMode_Disable` to disable gravity sensing; otherwise, after `setVideoEncoderRotation` is called, the image viewed by the remote user will not change.

<span id="que14"></span>
### What should I do if a TRTC call uses the TXVodPlayer player for playback together, but the playback volume level is very low?
You can use the `setSystemVolumeTyp` API to set the system volume type used during the call to `TRTCSystemVolumeTypeMedia` (media volume mode).

<span id="que15"></span>
### There is normal TRTC upstream data, but relayed pull failed and the video image couldn't be viewed. Why?	
Please check whether auto-relay push is enabled in the [TRTC Console](https://console.cloud.tencent.com/trtc).

<span id="que16"></span>
### What are the formats of the recording files generated in various relayed recording scenarios?	
The recording file formats configured in the [TRTC Console](https://console.cloud.tencent.com/trtc) shall prevail.

<span id="que17"></span>
### How do I select the media or call volume type?
You can call the `setSystemVolumeType` API to select the media or call volume type as needed.
- TRTCAudioVolumeTypeAuto: call volume type is used when the mic is on and media volume type is used when the mic is off, which is the default value.
- TRTCAudioVolumeTypeVOIP: call volume type is always used.
- TRTCAudioVolumeTypeMedia: media volume mode is always used.

<span id="que18"></span>
### How do I know whether the camera is enabled successfully?
If the `onCameraDidReady` callback is received, the camera is ready.

<span id="que19"></span>
### How do I know whether the mic is enabled successfully?
If the `onMicDidReady` callback is received, the mic is ready.

<span id="que20"></span>
### How do I know whether the audio/video call stream is successfully pushed?
You can use the `onSendFirstLocalVideoFrame` callback. The system will start capturing the camera and encode the captured image after successful call of `enterRoom` and `startLocalPreview`. This callback event will be returned after the SDK successfully sends the first video frame data to the cloud.

<span id="que21"></span>
### How do I know whether the pure audio call stream is successfully pushed?
You can use the `onSendFirstLocalAudioFrame` callback. The system will start capturing the mic and encoding the captured audio after successful call of `enterRoom` and `startLocalPreview`. This callback event will be returned after the SDK successfully sends the first audio frame data to the cloud.

<span id="que22"></span>
### Can I query all UserID values?
Currently, statistics of all `UserID` values are not available. After user accounts are successfully signed up on the client, you can write all user information into SQL for management and query.

<span id="que23"></span>	
### Can users with the same UserID be in the same room at the same time?
In TRTC, users with the same `UserID` cannot be in the same room at the same time; otherwise, there will be a conflict.

<span id="que24"></span>
### Why doesn't audio routing (receiver/speaker) configured by calling the `setAudioRoute` API take effect?	
Receiver/Speaker can be switched only in call volume mode, that is, this API will take effect only if it is called when two or more users are co-anchoring.

<span id="que25"></span>
### Does TRTC only support enabling auto-recording in the console? How do I enable manual recording?
You can enable manual recording in TRTC in the following steps:
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc), enable **auto-relay push**, and disable **on-cloud recording**.
2. After a user enters a room, the `streamid` corresponding to the `UserID` will be calculated according to the stream ID generation rule.
3. Use the [CreateLiveRecord API](https://intl.cloud.tencent.com/document/product/267/30847) of LVB to start the recording task of the `streamid`.
 - DomainName: [bizid].livepush.myqcloud.com
 - AppName: trtc_[sdkappid]
 - StreamName: streamid
4. After the recording task is completed, LVB will directly write the file into VOD and [send the event notification through the recording callback](https://intl.cloud.tencent.com/document/product/267/31566).

<span id="que26"></span>
### How does TRTC verify the generated UserSig? How do I troubleshoot errors -3319 and -3320 reported during room entry?	
You can log in to the TRTC Console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)** to verify the `UserSig`.

<span id="que27"></span>
### How do I view the call duration and usage in TRTC?	
You can view the information on the **[Usage Statistics](https://console.cloud.tencent.com/trtc/statistics)** page in the TRTC Console.

<span id="que28"></span>
### How do I maintain the user list and count the number of viewers in a live room in TRTC?	
If [IM](https://intl.cloud.tencent.com/document/product/1047) is integrated into your project, you can directly use the IM group user counting API to count the number of viewers in a room. However, the number counted in this method is not very accurate. If you have a low requirement for online viewer count, you can directly use this method.
If you want to count the number of online viewers very accurately, we recommend you implement the following statistics logic on your own:
1. Increase the viewer count (client -> server): when a new viewer enters a room, add 1 to the viewer count of the room. To implement this, you can make the application's viewer client send an increment request to the server during room entry.
2. Decrease the viewer count (client -> server): when a viewer exits a room, subtract 1 from the viewer count of the room. To implement this, you can make the application's viewer client send a decrement request to the server during room exit.


<span id="que29"></span>
### An error -100013 was reported during room entry, and the error message was `ERR_SERVER_INFO_SERVICE_SUSPENDED`. What should I do?	
This error indicates that the service is unavailable. Please check the following:
- Whether the remained validity period in minutes in the package is greater than 0.
- Whether your Tencent Cloud account has overdue payment.

<span id="que30"></span>
### How do I monitor the network status and implement the signal strength display feature in TRTC?	
You can use `onNetworkQuality()` to listen on the current upstream/downstream quality of the network and implement the signal strength display feature as instructed [here](https://github.com/tencentyun/TRTCSDK).

<span id="que31"></span>
### How do I know whether the new MCU stream mix or legacy on-cloud stream mix is used in TRTC?
If the following conditions are met and `mcumix = 1` is printed in the client log, the new MCU stream mix is used:
- The application is created on or after January 9, 2020.
- The TRTC SDK is on v6.9 or above.

<span id="que32"></span>
### What should I do if the stream mix API failed to be called and did not take effect in TRTC.?
1. Make sure that **auto-relay push** is enabled in the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. Listen on the `onSetMixTranscodingConfig()` API and make changes based on the returned error message.
3. If the relayed stream ID is customized through an SDK API, the legacy on-cloud stream mix scheme will fail.
4. If `onSetMixTranscodingConfig()` returns a success, but the relayed pull through CDN still cannot take effect, it may be caused by the lack of playback domain name. We recommend you check the playback domain name configuration.

<span id="que33"></span>
### TRTC started on-cloud recording but generated no recording files. What should I do?
1. Make sure that **auto-relay push** and **on-cloud recording** are enabled in the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. TRTC will start recording only if there is a user upstreaming audio/video data normally in the room.
3. A recording file will be generated only if the relayed pull through CDN is normal.
4. If an audio stream is played back at first and then switched to a video stream, based on the recording template, the recording file may be generated for only the audio or video data.

<span id="que34"></span>
### How do I troubleshoot if lag occurs in TRTC?
You can view the call quality of the corresponding `RoomID` and `UserID` on the **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)** page in the TRTC Console:
- Check the sender and receiver status on the receiver client.
- Check whether the packet loss rate is high for the sender and receiver, and if so, the lag is generally caused by unstable network conditions.
- Check the frame rate and CPU utilization. Either a low frame rate or a high CPU utilization can cause lag.

<span id="que35"></span>
### How do I troubleshoot blurry video image, low image quality, and other problems in TRTC?
- The definition is mainly subject to the bitrate. Check whether the bitrate configured in the SDK is low. If the resolution is high, but the bitrate is low, blurs tend to occur.
- TRTC dynamically adjusts the bitrate and resolution based on the network conditions according to the on-cloud QoS bandwidth limit policy. If the network is poor, the bitrate tends to be reduced, which will cause decreased definition.
- Check whether the `VideoCall` or `Live` mode is used during room entry. As the `VideoCall` mode is dedicated to call scenarios and features low-latency and smoothness, it tends to reduce the image quality on a weak network in order to ensure the smoothness. Therefore, we recommend you use the `Live` mode in scenarios with a high requirement for image quality.

<span id="que36"></span>
### How do I give the room number to the co-anchor I invite？
You can add roomid in the custom message for parsing. For more information on how to do this, see [Creating a custom message](https://intl.cloud.tencent.com/document/product/1047/34322#.E5.88.9B.E5.BB.BA.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF) and [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgsendnewmsg).

<span id="que37"></span>
###  Can I wait for at least two members join the room before the recording?
Yes. If you want to obtain the mixed audio data, please [enable On-Cloud MixTranscoding](https://intl.cloud.tencent.com/document/product/647/34618#.E5.90.AF.E5.8A.A8.E6.B7.B7.E6.B5.81), specify the output stream ID, and call the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API.

