
<h3 id="UserSig">What is UserSig?</h3>

UserSig is a security signature designed by Tencent Cloud to prevent attackers from accessing your Tencent Cloud account.
Currently, Tencent Cloud services including TRTC, IM, and MLVB all use this security mechanism. Whenever you want to use these services, you must provide three key pieces of information, i.e. `SDKAppID`, `UserID`, and `UserSig` in the initialization or login function of the corresponding SDK.
`SDKAppID` is used to identify your application, and `UserID` your user. `UserSig` is a security signature calculated based on the two parameters using the **HMAC SHA256** encryption algorithm. Attackers cannot use your Tencent Cloud traffic without authorization as long as they cannot forge a `UserSig`.
See the figure below for how `UserSig` is calculated. Basically, it involves hashing crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`.
```Cpp
// `UserSig` calculation formula, in which `secretkey` is the key used to calculate `UserSig`.

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```


[](id:que2)
### How many rooms can there be in TRTC at the same time?
There can be up to 4,294,967,294 concurrent rooms, and there is no limit on the cumulative number of rooms.


[](id:que3)
### How long is the average delay in TRTC?
The average end-to-end delay around the globe is less than 300 ms.


[](id:que4)
### Does TRTC support screen sharing on PCs?
Yes. For details, please see the following documents:
- [Screen Sharing (Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [Screen Sharing (macOS)](https://intl.cloud.tencent.com/document/product/647/37336)
- [Screen Sharing (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/35163)

For more information on the screen sharing APIs, see [Client APIs > All Platforms (C++)](https://intl.cloud.tencent.com/document/product/647/35131), [Client APIs > Windows (C#)](https://intl.cloud.tencent.com/document/product/647/35136), or [Client APIs > Electron](https://intl.cloud.tencent.com/document/product/647/35141).


[](id:que5)
### What platforms does TRTC support?
Supported platforms include iOS, Android, Windows (C++), Windows (C#), macOS, desktop browsers, and Electron. For more information, please see [Overview > Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35078).


[](id:que6)
### How many people can be in the same call in TRTC?
- In the call modes, each room can accommodate up to 300 concurrent users, and up to 50 of them can enable their cameras or mics.
- In the live streaming modes, each room can accommodate up to 100,000 concurrent viewers, and up to 50 of them can be assigned the anchor role and enable their cameras or mics.


[](id:que7)
### How do I start a live streaming session in TRTC?
TRTC offers a dedicated low-latency interactive live streaming solution that allows up to 100,000 participants with co-anchoring latency kept as low as 200 ms and watch latency below 1 s. It adapts excellently to poor network conditions and is optimized for the complicated mobile network environments.
For detailed directions, please see [Live Streaming Mode](https://intl.cloud.tencent.com/document/product/647/35107).



[](id:que8)

### What roles are supported during live streaming in TRTC? How do they differ from each other?
The live streaming modes (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`) support two roles: `TRTCRoleAnchor` (anchor) and `TRTCRoleAudience` (viewer). An anchor can both send and receive audio/video data, but a viewer can only receive and play back others' data. You can call `switchRole()` to switch roles.


[](id:que9)
### Can I kick out a user, forbid a user to speak, or mute a user in a TRTC room?  
Yes, you can.
- To enable the features through simple signaling operations, use `sendCustomCmdMsg`, the custom signaling API of TRTC, to define your own control signaling, and users who receive the signaling will perform the actions expected. For example, to kick out a user, just define a kick-out signaling, and the user receiving it will exit the room.
- If you want to implement a more comprehensive operation logic, we recommend that you use [Instant Messaging](https://intl.cloud.tencent.com/zh/document/product/1047) to map the TRTC room to an IM group and enable the features via the sending/receiving of custom messages in the group.


[](id:que10)
### Can TRTC pull and play back RTMP/FLV streams? 
Yes. For details, please see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).


[](id:que11)
### Does TRTC support Swift integration on iOS?
Yes. Just integrate the SDK in the same steps as you do a third-party library or by following the steps in [Demo Quick Start (iOS & macOS)](https://intl.cloud.tencent.com/document/product/647/35086).


[](id:que12)
### What browsers support TRTC SDK for desktop browsers?  
It is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms such as browsers on Android. For more information, please see [Client APIs > Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35143).
You can open [WebRTC Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in a browser to test whether the environment fully supports WebRTC.


[](id:que13)
### What do the errors `NotFoundError`, `NotAllowedError`, `NotReadableError`, `OverConstrainedError`, and `AbortError` found in the log of the SDK for desktop browsers mean?


| Error | Description | Suggested Solution |
|---------|---------|---------|
| NotFoundError | The media (audio, video, or screen sharing) of the request parameters are not found. <br>For example, this error occurs if the PC has no cameras but the browser is requested to get a video stream.   | Remind users to check devices such as cameras and mics before making a call. If a user does not have a camera and wants to make an audio call, use [TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream) to make the SDK capture audio only. |
| NotAllowedError| The user has rejected the request of the current browser instance to access camera/mic or share screens.| Remind the user that audio/video calls are not possible without camera/mic access. |
| NotReadableError  | The user has granted access to the requested device, but it is still inaccessible due to a hardware, browser or webpage error.  | Handle the error according to the error message returned, and send this message to the user: “the camera/mic cannot be accessed. Please make sure that no other applications are requesting access and try again.”|
| OverConstrainedError | The `cameraId/microphoneId` value is invalid. | Make sure that the `cameraId/microphoneId` value passed in is valid.|
| AbortError| The device cannot be accessed due to an unknown reason. | - |


For more information, please see [initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize).


[](id:que14)
### How do I check whether TRTC SDK for desktop browsers can get the device (camera/mic) list?
1. Check whether the browser can access the devices:
Open the console with the browser and enter `navigator.mediaDevices.enumerateDevices()` to see if the device list can be obtained.
 - Normally, a promise containing an array of `MediaDeviceInfo` objects will be returned, each object corresponding to an available media device.
 - If the SDK fails to enumerate the devices, a rejected promise will be returned, indicating that the browser fails to detect any devices. You need to check the browser or devices.
2. If the device list can be obtained, enter `navigator.mediaDevices.getUserMedia({ audio: true, video: true })` to see if the `MediaStream` object can be returned. If it is not returned, it indicates that the browser fails to obtain any data. You need to check your browser configuration.



[](id:que15)

### What are the differences and relationships between LVB, ILVB, TRTC, and relayed live streaming?
- **LVB** (keywords: one-to-many, RTMP/HLS/HTTP-FLV, CDN)
 LVB consists of the push end, the playback end, and cloud live streaming service. The cloud live streaming service uses CDNs to deliver live streams, which are pushed over the universal protocol RTMP and can be watched over protocols such as RTMP, HTTP-FLV, or HLS (for HTML5).
- **ILVB** (keywords: co-anchoring, anchor competition)
 ILVB is a live streaming mode where the anchor and viewers can interact through co-anchoring and different anchors can compete with each other.
- **TRTC** (keywords: multi-person interaction, UDP-based proprietary protocol, low latency)
 The main application scenarios for real-time communication (RTC) are audio/video interaction and low-latency live streaming. It uses UDP-based proprietary protocols and can keep the latency as low as 100 ms. Typical applications include QQ calls, VooV Meeting, and online group classes. Tencent Real-Time Communication (TRTC) is supported by mainstream platforms including iOS, Android, and Windows. It can communicate with WebRTC and relay live streams to CDNs through on-cloud stream mixing.
- **Relayed live streaming** (keywords: on-cloud stream mixing, RTC relayed live streaming, CDN)
 The relayed live streaming technology replicates multiple streams in a low-latency co-anchoring room and mixes them into one stream in the cloud before pushing it to a live streaming CDN for delivery and playback. 

[](id:que16)

### How do I view my call duration and usage?  
You can find the information on the **[Usage Statistics](https://console.cloud.tencent.com/trtc/statistics)** page of the TRTC console.



[](id:que17)

### How do I fix lag in TRTC?
You can check call quality by `RoomID` and `UserID` in **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)** in the TRTC console.
- Check the sender and receiver status from the receiver’s perspective.
- Check the packet loss rate for the sender and receiver. High packet loss rates suggest that the lag may be caused by unstable network connections.
- Check the frame rate and CPU usage. Both low frame rates and high CPU usage can cause lagging.

[](id:que18)

### How do I fix low-quality and blurry videos in TRTC?
- Resolution is mainly associated with bitrate. Check whether the bitrate is set too low. Blurring tends to occur when resolution is high but bitrate is low.
- TRTC dynamically adjusts bitrate and resolution based on network conditions according to its on-cloud QoS control policy. It reduces the bitrate in case of poor network connections, which leads to decreased definition.
- Check whether it is the `VideoCall` or `Live` mode that is used during room entry. As the `VideoCall` mode is designed for calls and features low latency and smoothness, it tends to sacrifice image quality for image quality when network connections are poor. We recommend that you use the `Live` mode for application scenarios with high requirements on image quality.
