<span id="UserSig"></span>
### What is UserSig?

`UserSig` is a security signature designed by Tencent Cloud for the purpose of preventing attackers from misappropriating your Tencent Cloud permissions.
Currently, the Tencent Cloud services of TRTC, IM, and MLVB all use this security mechanism. Whenever you want to use these services, you need to provide three key pieces of information (`SDKAppID`, `UserID`, and `UserSig`) for the initialization or login functions of the corresponding SDK.
`SDKAppID` is used to identify your application, while `UserID` is used to identify your user. `UserSig` is a security signature that is calculated based on these two parameters. It is calculated with the **HMAC SHA256** encryption algorithm. Attackers cannot make unauthorized use of your Tencent Cloud service traffic as long as they cannot forge your `UserSig`.
See the figure below for how `UserSig` is calculated. Basically, a one-time hash encryption is performed on crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`.
```Cpp
// `UserSig` calculation formula, in which `secretkey` is the encryption key for calculating `usersig`.

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```


<span id="que2"></span>
### How many rooms can be created in TRTC at the same time?
There can be up to 4,294,967,294 concurrent rooms, and there is no limit on the cumulative number of rooms.


<span id="que3"></span>
### How long is the average delay in TRTC?
The average end-to-end delay around the globe is less than 300 ms.


<span id="que4"></span>
### Does TRTC support screen sharing on PCs?
Yes. For more information, please see the following documents:
- [Screen Sharing (Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [Screen Sharing (macOS)](https://intl.cloud.tencent.com/document/product/647/37336)
- [Screen Sharing (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/35163)

For more information on screen sharing APIs, please see [APIs for Windows (C++)](https://intl.cloud.tencent.com/document/product/647/35131) or [APIs for Windows (C#)](https://intl.cloud.tencent.com/document/product/647/35136). In addition, you can also use [APIs for Electron](https://intl.cloud.tencent.com/document/product/647/35141).

<span id="que5"></span>
### What platforms does TRTC support?
Supported platforms include iOS, Android, Windows (C++), Windows (C#), macOS, desktop browser, Electron, and Linux. For more information, please see “Supported Platforms” in [Overview](https://intl.cloud.tencent.com/document/product/647/35078).

<span id="que6"></span>
### How many people can be in the same call in TRTC?
- In call mode, a single room can sustain up to 300 concurrent online users, and up to 30 of them can simultaneously enable their cameras or mics.
- In live streaming mode, a single room can sustain up to 100,000 concurrent online viewers, and up to 30 of them can simultaneously enable their cameras or mics as anchors.

>? 20 users can simultaneously enable their cameras or mics on the web.

<span id="que7"></span>
### How does TRTC implement live streaming applications?
TRTC provides the low-latency interactive live streaming solution specially for live streaming scenarios. It can sustain up to 100,000 concurrent users and ensure a latency between co-anchoring anchors of as short as 200 milliseconds and a latency between anchors and viewers of less than 1 second. In addition, it delivers a high performance even in weak network environments to adapt to the complex network environments of mobile devices.
For detailed directions, please see [Live Streaming Mode (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35107).



<span id="que8"></span>
### Which roles are supported by TRTC live streaming? What are the differences between them?
In live streaming scenarios (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`), two roles are supported: `TRTCRoleAnchor` (anchor) and `TRTCRoleAudience` (viewer). The difference is that an anchor can upstream and downstream audio/video data at the same time, while a viewer can only downstream and play back others' data. You can call `switchRole()` to switch between roles.


<span id="que9"></span>
### Can I kick out a user, forbid a user to speak, or mute a user in a TRTC room?  
Yes.
- To perform a simple signaling operation, you can use the custom signaling API `sendCustomCmdMsg` of TRTC to define the corresponding control signaling, and the user in the call will perform the corresponding operation after receiving the control signaling. For example, to kick out a user is to define a kick-out signaling, and the user receiving it will exit the room automatically.
- If you want to implement a more comprehensive operation logic, we recommend you use [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047) to map the TRTC room to an IM group and receive/send custom messages in the group, so as to perform the corresponding operation.


<span id="que10"></span>
### Can TRTC audio/video streams be pulled through CDN for playback? 
Yes. For more information, please see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).


<span id="que11"></span>
### Is Swift integration supported for iOS?
Yes. You can directly integrate the SDK in the process of integrating third-party libraries. For more information, you can also see [Running the Demo (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35086).


<span id="que12"></span>
### Which browsers support the SDK for desktop browsers?  
It is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms (such as browsers on Android). For more information, please see “Supported Platforms” in [API Overview](https://intl.cloud.tencent.com/document/product/647/35143).
You can open the [WebRTC capability test](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) page in your browser to check whether WebRTC is fully supported.


<span id="que13"></span>
### What do the errors `NotFoundError`, `NotAllowedError`, `NotReadableError`, `OverConstrainedError`, and `AbortError` found in the log of the SDK for desktop browsers mean?


 | Error | Description | Suggested Solution | 
|---------|---------|---------|
| NotFoundError | No media types (including audio, video, and screen sharing) that meet the request parameters are found. <br>For example, this error will occur if the PC has no camera but the browser is requested to get a video stream. | Remind the user to check the required devices such as the camera or mic before making a call. If there are no cameras and the user needs to make an audio call, specify to capture the mic only in [TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream). | 
| NotAllowedError | The user has rejected the request to access audio, video, or screen sharing made by the current browser instance.| Inform the user that it is impossible to make video/audio calls without camera/mic access. | 
| NotReadableError | The user has granted access to the required device, but it is inaccessible due to an error in a certain hardware device on the operating system, browser, or webpage. | Process in response to the error reported by the browser and inform the user that "The camera/mic is temporarily inaccessible. Please make sure that no other applications are requesting access to the camera/mic and try again". | 
| OverConstrainedError| The value of the `cameraId`/`microphoneId` parameter is invalid. | Make sure that the value of the `cameraId`/`microphoneId` parameter is correct and valid. | 
| AbortError | The device cannot be used for an unknown reason. | - | 


For more information, please see [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize).


<span id="que14"></span>
### How do I check whether the SDK for desktop browsers can get the device (camera/mic) list properly?
1. Check whether the browser can use the devices properly:
Open the console directly on the page and enter `navigator.mediaDevices.enumerateDevices()` to check whether the device list can be obtained.
 - If the device list is obtained, a `Promise` will be returned, where there will be an array of `MediaDeviceInfo` objects and each object in the array corresponds to an available media device.
 - If the enumeration fails, the `Promise` will return `rejected`, indicating that the browser has not recognized the device, and you need to check the browser or device.
2. If the device list can be obtained, enter `navigator.mediaDevices.getUserMedia({ audio: true, video: true })` to check whether the `MediaStream` object can be returned properly. If it is not returned, the browser has not obtained the data, and you need to check the browser configuration.

<span id="que17"></span>
### What are the differences and relationships between LVB, ILVB, TRTC, and relayed live streaming?
- **LVB** (keywords: one-to-many, RTMP/HLS/HTTP-FLV, CDN)
 LVB consists of the push end, the playback end, and the LVB cloud service. The LVB cloud service uses CDN to deliver live streams, which are pushed over the universal standard protocol RTMP. After being delivered by CDN, live streams can be watched over protocols such as RTMP, HTTP-FLV, or HLS (for HTML5).
- **ILVB** (keywords: co-anchoring, anchor competition)
 ILVB is a live streaming mode where the anchor and viewers can interact through co-anchoring and different anchors can compete with each other.
- **TRTC** (keywords: multi-person interaction, UDP-based proprietary protocol, low-latency)
 Real-time communication (RTC) is mainly applicable to audio/video interaction and low-latency live streaming. With the aid of a UDP-based proprietary protocol, its latency can be reduced to 100 ms, which is ideal for scenarios such as QQ call, VooV Meeting, and big online classes. Tencent Real-Time Communication (TRTC) supports mainstream platforms and can relay live streams to CDN through on-cloud stream mix.
- **Relayed live streaming** (keywords: on-cloud stream mix, RTC relayed live streaming, CDN)
 The relayed live streaming technology replicates and mixes multiple pushed streams in a low-latency co-anchoring room into one stream in the cloud and then pushes the mixed stream to CDN for delivery and playback. 


<span id="que18"></span>
### How do I view the call duration and usage in TRTC?  
You can view the information on the **[Usage Statistics](https://console.cloud.tencent.com/trtc/statistics)** page in the TRTC Console.

<span id="que19"></span>
### How do I troubleshoot lagging in TRTC?
You can view the call quality of the corresponding `RoomID` and `UserID` on the **[Monitoring Dashboard](https://console.cloud.tencent.com/trtc/monitor)** page in the TRTC console:
- Check the sender and receiver status on the receiver client.
- Check whether the packet loss rate is high for the sender and receiver, and if so, check whether the lag is generally caused by unstable network conditions.
- Check the frame rate and CPU utilization. Either a low frame rate or a high CPU utilization can cause lag.


<span id="que20"></span>
### How do I troubleshoot blurry video image, low image quality, and other problems in TRTC?
- The definition is mainly subject to the bitrate. Check whether the bitrate configured in the SDK is low. Blurring tends to occur when the resolution is high but the bitrate is low.
- TRTC dynamically adjusts the bitrate and resolution based on the network conditions according to the on-cloud QoS bandwidth limit policy. If the network is poor, the bitrate tends to be reduced, which will lead to decreased definition.
- Check whether the `VideoCall` or `Live` mode is used during room entry. As the `VideoCall` mode is dedicated to call scenarios and features low-latency and smoothness, it tends to reduce the image quality on a weak network in order to ensure the smoothness. Therefore, we recommend you use the `Live` mode in scenarios with a high requirement for image quality.
