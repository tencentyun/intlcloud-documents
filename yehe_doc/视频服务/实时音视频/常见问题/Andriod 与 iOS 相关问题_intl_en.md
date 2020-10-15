<span id="que1"></span>
### Which system volume types are supported by the mobile client (for Android/iOS)?
Two system volume types, i.e., call volume and media volume, are supported.
- Call volume is specially designed for call scenarios on mobile phones. It uses the acoustic echo cancellation (AEC) feature built in phones and has a lower sound quality than media volume, and its volume level cannot be adjusted to 0 with volume buttons, but it supports mics on Bluetooth earphones.
- Media volume is specially designed for music scenarios on mobile phones. It has a higher sound quality than call volume, and its volume level can be adjusted to 0 with volume buttons. When using it, if you want to enable the AEC feature, the SDK will enable its built-in acoustic processing algorithms to further process the audio. With media volume, only the mics on phones instead of those on Bluetooth earphones can be used to capture audio.

<span id="que2"></span>
### How do I set the resolution to 1080p for push in the mobile SDK?
1080p is defined as 114 in `TX_Enum_Type_VideoResolution`. You can directly set the resolution by passing in the enumerated value.

<span id="que4"></span>
### How does the TRTC mobile client implement screen sharing?	
From v7.2 on, the entire screen can be shared on Android, and the screen of a single application can be shared on iOS. For more information, please see the source code in the [official demo](https://github.com/tencentyun/TRTCSDK).

<span id="que5"></span>
### Does the TRTC mobile client for Android support 64-bit arm64-v8a architecture?
From TRTC v6.3 on, the arm64-v8a architecture is supported as ABI.

<span id="que7"></span>
### Is Swift integration supported for iOS?
Yes. You can directly integrate the SDK in the process of integrating third-party libraries. For more information, you can also see [Running Demo (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35086).

<span id="que9"></span>
### Does the TRTC SDK support running in the background on iOS?
Yes. You can select the current project, set **Background Modes** under **Capabilities** to **ON**, and check **Audio, AirPlay and Picture in Picture** to implement execution in the background as shown below:
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

<span id="que10"></span>
### Can I listen on remote room exit events on iOS?
You can use [onRemoteUserLeaveRoom](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) to listen on room exit events, and this API will trigger callbacks only when all users of `VideoCall` exit the room or when anchors (rather than viewers) in `LIVE` mode exit the room. 

<span id="que11"></span>
### How do I make a video call when the phone is locked?
For more information on how to implement offline answering, please see [Android](https://intl.cloud.tencent.com/document/product/647/36068)

<span id="que12"></span>
### Does TRTC support interconnection between Android and web?
Yes. To make a call, use the same [SDKAppID](https://console.cloud.tencent.com/trtc/app) and enter the same room. For more information, please see the following demos:
- [Android](https://intl.cloud.tencent.com/document/product/647/35084)
- [Desktop Browser](https://intl.cloud.tencent.com/document/product/647/35607)

<span id="que13"></span>
### Can both anchors and viewers actively initiate co-anchoring during live streaming?
Yes. The initiation logic is the same for both anchors and viewers. For more information, please see [Android](https://intl.cloud.tencent.com/document/product/647/35108).

<span id="que14"></span>
### During video conferencing, can mobile users and web users enter the same room?
Yes, but it should be ensured that the same [SDKAppID](https://console.cloud.tencent.com/trtc/app) and room ID values are used while the user ID values are different.

<span id="que15"></span>
### Can N TRTC objects be created on the same page to log in to N rooms through N UserID values?
Yes. Starting from [v7.6](https://intl.cloud.tencent.com/document/product/647/34615), the same user can enter multiple rooms.
