[](id:que1)
### What is a `RoomID` in TRTC? What is its value range?
A `RoomID` (room ID) uniquely identifies a room and can range from 1 to 4294967295. You are responsible for maintaining and assigning the Room IDs of your applications.

[](id:que2)
### What is a `UserID` in TRTC? What is its value range? 
A `UserID` (user ID) uniquely identifies a user in a TRTC application. It can contain letters (case sensitive), digits, and underscores, preferably not longer than 32 bytes.


[](id:que3)
### How long is the lifecycle of a TRTC room?
- The first user who enters a room is the owner of the room. Room owners cannot close rooms manually.
- **In the call modes**, TRTC closes a room when all users exit the room.
- **In the live streaming modes**, if the last user who exits a room is an anchor, TRTC will close the room immediately; if the user is audience, TRTC will close the room in 10 minutes.
- A user will be removed from a room 90 seconds after unexpected disconnection. If all users are unexpectedly disconnected, the room will be closed after 90 seconds. **The waiting time after disconnection is also billed**.
- If a user attempts to enter a room that does not exist, TRTC will automatically create a room with the ID entered.

[](id:que4)
### Can users not subscribe to audio/video streams? 
To enable instant streaming, TRTC subscribes users to audio/video streams by default upon room entry. You can call the `setDefaultStreamRecvMode` API to switch to the manual subscription mode.

[](id:que5)
### Can I specify a stream ID for relayed push in TRTC?  
Yes. You can specify a `streamId` via `TRTCParams` of `enterRoom` or call the `startPublishing` API to pass in the `streamId`.

[](id:que6)
### What roles are supported during live streaming in TRTC? How do they differ from each other?
The live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`) support two roles: `TRTCRoleAnchor` (anchor) and `TRTCRoleAudience` (audience). An anchor can both send and receive audio/video data, but audience can only receive and play back others' data. You can call `switchRole()` to switch roles.

[](id:que7)
### What is a role in TRTC? 
The concept of roles (anchors and audience) is applicable only in the live streaming scenarios. The anchor role (`TRTCRoleAnchor`), which can be assigned to 50 users at the same time, can both send and receive audio/video, and the audience role (`TRTCRoleAudience`), which can be assigned to 100,000 users at the same time, can only receive audio/video.


[](id:que8)
### What application scenarios are supported in TRTC rooms?  
The following application scenarios are supported:
- TRTCAppSceneVideoCall: the video call scenario, which is suitable for one-to-one video calls, video conferences with up to 300 participants, online medical consultation, video chat, and video interviews
- TRTCAppSceneLIVE: the interactive video live broadcasting scenario, which is suitable for low-latency video live streaming, interactive classroom for up to 100,000 participants, live video competition, video dating, remote training, and mega conferences
- TRTCAppSceneAudioCall: the audio call scenario, which is suitable for one-to-one audio calls, audio conferences with up to 300 participants, audio chat, and online Werewolf playing
- TRTCAppSceneVoiceChatRoom: the interactive audio live broadcasting scenario, which is suitable for low-latency audio live streaming, live audio co-anchoring, audio chat rooms, karaoke, and FM broadcasting


[](id:que9)
### What platforms does TRTC support?
TRTC supports platforms including iOS, Android, Windows (C++), Unity, macOS, web, and Electron. For more information, see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35078).

[](id:que10)
### What are the differences among LiteAV_TRTC, TRTC Professional, and TRTC Enterprise? 
See [Differences Among Editions](https://intl.cloud.tencent.com/document/product/647/34615).


[](id:que11)
### Does TRTC support co-anchoring during live streaming?
Yes. For detailed instructions, see:
- [Live Streaming Mode (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35107)
- [Live Streaming Mode (Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [Live Streaming Mode (Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [Live Streaming Mode (Electron)](https://intl.cloud.tencent.com/document/product/647/36070)
- [Live Streaming Mode (Web)](https://intl.cloud.tencent.com/document/product/647/35110)


[](id:que12)
### How many rooms can there be in TRTC at the same time?
There can be up to 4,294,967,294 concurrent rooms in TRTC. No limits are set on the number of non-concurrent rooms.

[](id:que13)
### How do I create a room?
A room is automatically created by TRTC when a user enters a room. Therefore, you do not need to manually create a room. Just call the client API for room entry.
- [iOS & macOS > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- [Windows（C++） > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)
- [Windows（C#） > enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#afbb3a1e6f73f339d47368a7d620a995f)
- [Electron > enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)
- [Web > join](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)

[](id:que14)
### What is the upper limit on the bandwidth used for the video service of TRTC?
There isn’t a limit.


[](id:que15)
### Can TRTC be deployed on-premises?
On-premises TRTC is not commercially available yet. If you have questions about it or want to use it, please contact us at colleenyu@tencent.com.

[](id:que16)
### To enable relayed live streaming in TRTC, do I need to get an ICP filing for my domain name?
To enable relayed live streaming, according to the requirements of applicable authorities, the playback domain name needs an ICP filing before it can be used. For more information, please see [Watch over CDN](https://intl.cloud.tencent.com/document/product/647/35242).

[](id:que17)
### How long is the average delay in TRTC?
The average end-to-end delay of TRTC around the globe is less than 300 ms.

[](id:que18)
### Does TRTC support active calling?
You can enable this feature using signaling channels. For example, you can use the custom message feature of [IM](https://intl.cloud.tencent.com/product/im) to enable active calling. For more information, see the scenario-specific demos in the [SDK](https://intl.cloud.tencent.com/document/product/647/34615) source code.

[](id:que19)
### Can users use Bluetooth earphones when having one-to-one video calls in TRTC?
Yes, you can.


[](id:que20)
### Can TRTC be used outside the Chinese mainland?
Yes, you can.

[](id:que21)
### Does TRTC support screen sharing on PCs?
Yes. For details, see the following documents:
- [Real-Time Screen Sharing (Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [Real-Time Screen Sharing (macOS)](https://intl.cloud.tencent.com/document/product/647/37336)
- [Real-Time Screen Sharing (Web)](https://intl.cloud.tencent.com/document/product/647/35163)

For more information on the screen sharing APIs, see [Client APIs > All Platforms (C++)](https://intl.cloud.tencent.com/document/product/647/35131). You can also use [Electron APIs](https://intl.cloud.tencent.com/document/product/647/35141).

[](id:que23)

### Can I share local video files in TRTC?

Yes. You can achieve this using the [Custom Capturing and Rendering](https://intl.cloud.tencent.com/document/product/647/35158) feature.

[](id:que24)
### Can I record live streaming videos and store the recording files locally on my phone?
Recording files cannot be stored locally on phones. They are stored in VOD by default. You can download and save them to your phone. For more information, please see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).


[](id:que25)
### Does TRTC support audio-only streams?
Yes, it does.


[](id:que26)
### Can there be more than one screen sharing image in the same room?
Currently, only one screen sharing substream is allowed in a room.

[](id:que27)
### When a specified window is shared (`SourceTypeWindow`), if the window size changes, will the resolution of the video stream change accordingly?
By default, the SDK automatically adjusts encoding parameters according to the size of the shared window.
If you want a fixed resolution, call the `setSubStreamEncoderParam` API to set encoding parameters for screen sharing or specify the parameters when calling the `startScreenCapture` API.


[](id:que28)
### Does TRTC support 1080p videos?
Yes. You can set the resolution through `setVideoEncoderParam`, the video encoding parameter of the SDK.

[](id:que29)
### Can I customize data capturing in TRTC?
You can on some platforms. For details, see [Custom Capture and Rendering](https://intl.cloud.tencent.com/document/product/647/35158).

[](id:que30)
### Is communication between TRTC and the ILVB SDK possible?
No, it's not.

[](id:que31)
### Is communication between TRTC and MLVB possible? 
TRTC and MLVB have different backend architectures and therefore cannot communicate with each other. Relayed push from TRTC to CDNs is possible though.



[](id:que32)
### How do different room entry modes (`AppScene`) vary from one another in TRTC?
TRTC has four room entry modes. Video call (`VideoCall`) and audio call (·VoiceCall`) are the call modes, and interactive video live streaming (`Live`) and interactive audio live streaming (`VoiceChatRoom`) are the live streaming modes.
- The call modes allow a maximum of 300 users in each TRTC room, and up to 50 of them can speak at the same time. The call modes are suitable for scenarios such as one-to-one video calls, video conferences with up to 300 participants, online medical consultation, video interviews, video customer service, and online Werewolf playing.
- The live streaming modes allow a maximum of 100,000 concurrent users in each room, with smooth mic connection/disconnection. Co-anchoring latency is kept below 300 ms and watch latency below 1,000 ms. The live streaming modes are suitable for scenarios such as low-latency interactive live streaming, interactive classrooms for up to 100,000 participants, video dating, online education, remote training, and mega conferences.


[](id:que33)
### Can I use the hands-free mode during video calls in TRTC?
Yes. You can use the hands-free mode by setting the audio route via the `setAudioRoute` API in native apps and the `sound-mode` attribute of the &lt;live-player&gt; tag in Mini Program.

[](id:que34)
### Does TRTC support volume reminders?
Yes. You can call the `enableAudioVolumeEvaluation` API to enable volume reminders.

[](id:que35)
### Does TRTC support mirror images? 
Yes. You can call the `setLocalViewMirror` API to set the mirroring mode for the preview image of the local camera or call `setVideoEncoderMirror` to set the mirroring mode for encoded images.

[](id:que36)
### Can I record the audio of a TRTC call and save the recording file locally? 
Yes. You can call `startAudioRecording` to record all the audio of a call, including that of the local user, remote users and the background music, into a single file in the format of PCM, WAV, or AAC.

[](id:que37)
### Can I record the video of a TRTC call into a file?
TRTC supports audio/video recording on a local server. To use this feature, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for the SDK and instructions.
You can also use the [on-cloud recording and playback](https://intl.cloud.tencent.com/document/product/647/35426) feature to record videos.

[](id:que38)
### Does TRTC support floating windows (like those in WeChat) or switching between the big and small images?
These features are part of UI design, for which the TRTC SDK sets no restrictions. The official demo provides sample code for image floating and the grid layout and supports floating windows, switching between big and small images, and dragging images. For more information, see the [official demo](https://github.com/tencentyun/TRTCSDK).

[](id:que39)
### How do I make an audio-only call in TRTC?
TRTC does not use separate channels for audio and video. You can make an audio-only call by calling only `startLocalAudio` but not `startLocalPreview.

[](id:que40)
### How do I enable relayed push and recording for an audio-only call in TRTC?
- In TRTC SDK below version 6.9, you need to construct `json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}` and pass it in `TRTCParams.businessInfo` during room entry. `1` means relayed push, and `2` means relayed push and recording.
- In TRTC SDK 6.9 or above, just set the scene parameter to `TRTCAppSceneAudioCall` or `TRTCAppSceneVoiceChatRoom` during room entry.

[](id:que41)
### Can I kick a user out, forbid a user to speak, or mute a user in a TRTC room?  
Yes, you can.
- To enable the features through simple signaling operations, use `sendCustomCmdMsg`, the custom signaling API of TRTC, to define your own control signaling, and users who receive the message will perform the action expected. For example, to kick out a user, just define a kick-out signaling, and the user receiving it will exit the room.
- If you want to implement a more comprehensive operation logic, we recommend that you use [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047) to map the TRTC room to an IM group and enable the features via the sending/receiving of custom messages in the group.

[](id:que42)
### Can TRTC pull and play back RTMP/FLV streams?  
Yes. The TRTC SDK has integrated TXLivePlayer. If you need more player features, consider using the all-featured LiteAVSDK_Professional.

[](id:que43)
### How many people can there be in a TRTC call?
- In call scenarios, each room can accommodate up to 300 concurrent users, and up to 50 of them can turn on their cameras or mics.
- In live streaming scenarios, each room can accommodate up to 100,000 concurrent users, and up to 50 of them can be assigned the anchor role and turn on their cameras or mics.


[](id:que44)
### How do I start a live streaming session in TRTC?
TRTC offers a dedicated low-latency interactive live streaming solution that allows up to 100,000 participants with co-anchoring latency kept as low as 200 ms and watch latency below 1s. It adapts excellently to poor network conditions and is optimized for the complicated mobile network environments.
For detailed directions, please see [Live Streaming Mode](https://intl.cloud.tencent.com/document/product/647/35107).

[](id:que45)
### Can I use the custom message sending API of TRTC to implement features such as chat rooms and on-screen comments?
No. Custom message sending is intended for simple and low-frequency signaling scenarios. For details, see [Sending Custom Messages > Use Limits](https://intl.cloud.tencent.com/document/product/647/35159).

[](id:que46)
### Can I loop background music in TRTC? Can I adjust the playback progress of background music?  
Yes. You can call the playback API again in the playback completion callback to loop background music. `seekMusicToPosInMS` of `TXAudioEffectManager` can be used to set the playback progress.

>?  `setBGMPosition()` of `TXAudioEffectManager` has been replaced with `seekMusicToPosInMS` since version 7.3.

[](id:que47)
### Can I listen for the entry/exit of users through callbacks in TRTC? Can I use `onUserEnter` or `onUserExit`?
Yes. You can use `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` to listen for the entry/exit of users, but callbacks are triggered only for users who can send data.
>?`onUserEnter` and `onUserExit` have been replaced with `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` since version 6.8.

[](id:que48)
### How do I listen for network disconnection and reconnection in TRTC?
You can listen for the events through the following callbacks:
- `onConnectionLost`: the SDK is disconnected from the server.
- `onTryToReconnect`: the SDK tries to reconnect to the server.
- `onConnectionRecovery`: the SDK is reconnected to the server.

[](id:que49)
### Is there a callback for first frame rendering? Can I listen for the start of image rendering or audio playback?
Yes. You can use `onFirstVideoFrame` and `onFirstAudioFrame` to listen for the events.

[](id:que50)
### Can I take a screenshot of a video in TRTC?
Currently, you can call `snapshotVideo()` on iOS and Android to take screenshots of local and remote videos.

[](id:que51)
### Why do I fail to connect peripheral devices such as Bluetooth earphones to TRTC?
Currently, TRTC supports mainstream Bluetooth earphones and peripherals, but for some devices, there are still compatibility issues. We recommend that you use our official demos and QQ audio/video calls to test the compatibility of a device.

[](id:que52)
### How do I get information such as the upstream/downstream bitrate, resolution, packet loss rate, and audio sample rate of a TRTC audio/video call?
You can call the `onStatistics()` API of the SDK to get the statistics.

[](id:que53)
### Does TRTC’s background music API `playBGM()` support online music?
No. Currently, it supports only local music. You can download an online music file and then call `playBGM()` to play it back.

[](id:que54)
### Can I set the local audio capturing volume or the playback volume of each remote user?
Yes. You can call `setAudioCaptureVolume()` to set the audio capturing volume of the SDK and `setRemoteAudioVolume()` to set the playback volume of a remote user.

[](id:que55)
### What are the differences between `stopLocalPreview` and `muteLocalVideo`?
- `stopLocalPreview` is used to stop local video capturing. If you call this API, both you and other users will not be able to see your image.
- `muteLocalVideo` is used to stop the sending of local video images. If you call this API, other users will not see your image, but you can still preview your own image.

[](id:que56)
### What are the differences between `stopLocalAudio` and `muteLocalAudio`? 
- `stopLocalAudio` is used to disable the capturing and sending of local audio.
- When `muteLocalAudio` is called, TRTC does not stop the sending of audio/video data. It continues to send muted data packets at extremely low bitrate.

[](id:que57)
### What resolutions does the TRTC SDK support?
We recommend that you set the resolution as instructed in [Setting Image Quality](https://intl.cloud.tencent.com/document/product/647/35153) for better image quality.

[](id:que58)
### How do I set the upstream video bitrate, resolution, and frame rate in the TRTC SDK? 
Call the `setVideoEncoderParam()` API of `TRTCCloud` and set `videoResolution` (resolution), `videoFps` (frame rate), and `videoBitrate` (bitrate) in `TRTCVideoEncParam`.

[](id:que59)
### How do I rotate videos in the TRTC SDK?  
Please see [Video Image Rotation and Zooming](https://intl.cloud.tencent.com/document/product/647/35154).

[](id:que60)
### How do I make a video call in the landscape mode? 
Please see [Video Image Rotation and Zooming](https://intl.cloud.tencent.com/document/product/647/35154).

[](id:que61)
### How do I match the rotation degrees of the local and remote images if they are different?  
Please see [Video Image Rotation and Zooming](https://intl.cloud.tencent.com/document/product/647/35154).


[](id:que62)
### What image quality-related settings (bitrate, resolution, and frame rate) does TRTC recommend?
See [Setting Image Quality > Recommended Configuration](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE).

[](id:que63)
### Can I test my network speed in TRTC? How?  
Yes, you can. For details, see [Testing Network Speed Before Chat](https://intl.cloud.tencent.com/document/product/647/35156).

[](id:que64)
### Can I control access to a TRTC room to allow only authorized users to enter the room? 
Yes. For details, please see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157).

[](id:que65)
### Can I pull and play back streams through CDNs? 
Yes. For details, please see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

[](id:que66)
### What formats does TRTC support for custom rendering? 
- iOS: I420, NV12, and BGRA
- Android: I420 and Texture2D

[](id:que67)
### What is TRTC?
Tencent Real-Time Communication (TRTC) leverages Tencent's years of experience in network and audio/video technologies to offer group audio/video calls and low-latency interactive live streaming solutions, allowing you to quickly develop cost-effective, low-latency, and high-quality interactive audio/video services. For details, please see [Product Introduction > Overview](https://intl.cloud.tencent.com/document/product/647/35078).

[](id:que68)
### How can I try out the TRTC demo?
Please see [Free Demo](https://intl.cloud.tencent.com/document/product/647/35076).

[](id:que69)
### How can I get started quickly with TRTC?
TRTC offers demo source code for different platforms to allow you to quickly build your own apps. For details, please see [User Tutorial](https://intl.cloud.tencent.com/document/product/647/39386).

[](id:que70)
### How do I enable on-cloud recording and playback in TRTC?
Please see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).

[](id:que71)
### How do I record streams on the server side?
Server-side recording relies on the SDK for Linux, which is not commercially available yet. If you have questions about the SDK or want to use it, please contact us at colleenyu@tencent.com.


