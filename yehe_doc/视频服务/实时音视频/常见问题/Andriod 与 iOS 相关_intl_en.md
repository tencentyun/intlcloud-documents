[](id:que1)
### What system volume types does TRTC support on mobile devices (Android and iOS)?
It supports two system volume types, i.e., call volume and media volume.
- Call volume is designed for call scenarios. It uses phones’ built-in acoustic echo cancellation (AEC) technique and delivers lower audio quality than media volume does. In the call volume mode, the volume cannot be turned to 0 with the volume buttons, but the mics of Bluetooth earphones can be used for audio capturing.
- Media volume is designed for music scenarios. It delivers higher sound quality than call volume does. In the media volume mode, the volume can be turned to 0 with the volume buttons, and if you want to enable the AEC feature, the SDK will use its built-in acoustic processing algorithm to process the audio. With media volume, only the mics on phones can be used to capture audio.

[](id:que2)
### How do I set the resolution for push to 1080p in the SDK on mobile devices?
1080p is defined as `114` in `TX_Enum_Type_VideoResolution`. You can use the resolution simply by passing in the enumerated value.

[](id:que4)

### How do I use the screen sharing feature in TRTC on mobile devices?	
- **Android**: version 7.2 and above support screen sharing. For detailed instructions on how to implement the feature, see [Real-Time Screen Sharing (Android)](https://intl.cloud.tencent.com/document/product/647/37337).
- **iOS**: version 7.2 and above support in-app screen sharing, and version 7.6 and above support both system-level and in-app screen sharing. For detailed instructions on how to implement the feature, see [Real-Time Screen Sharing (iOS)](https://intl.cloud.tencent.com/document/product/647/37338).



[](id:que5)
### Does TRTC support the 64-bit arm64-v8a architecture on Android?
TRTC has supported the arm64-v8a ABI since version 6.3.


[](id:que7)
### Does TRTC support Swift integration on iOS?
Yes. Just integrate the SDK in the same steps as you do a third-party library or by following the steps in [Demo Quick Start (iOS & macOS)](https://intl.cloud.tencent.com/document/product/647/35086).

[](id:que9)
### Can I run the TRTC SDK in the background on iOS?
Yes, you can. To run the SDK in the background, select the project, set **Background Modes** under **Capabilities** to **ON**, and check **Audio, AirPlay and Picture in Picture**, as shown below:
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)

[](id:que10)
### Can I listen for room exit by remote users on iOS?
You can use [onRemoteUserLeaveRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28) to listen for the room exit event. In the `VideoCall` mode, this callback is triggered when any user leaves the room; in the `LIVE` mode, it is triggered only when an anchor leaves the room. 

[](id:que11)
### How to call a user whose phone screen is locked or when the application is in the background or closed on the user’s phone?
It can be achieved through the offline answering feature. For details, please see [Real-Time Audio Call (Android) - Enable offline call answering](https://intl.cloud.tencent.com/document/product/647/36068).

[](id:que12)
### Can Android and web users call each other?
Yes. They just need to use the same [SDKAppID](https://console.cloud.tencent.com/trtc/app) and enter the same room. For more information, see the documents below:
- [Demo Quick Start (Android)](https://intl.cloud.tencent.com/document/product/647/35084)
- [Demo Quick Start (Web)](https://intl.cloud.tencent.com/document/product/647/35607)

[](id:que13)
### Can both anchors and audience initiate co-anchoring during live streaming?
Yes. Both anchors and audience can initiate co-anchoring using the same logic. For more information, please see [Demo Quick Start (Android)](https://intl.cloud.tencenxt.com/document/product/647/35108).

[](id:que14)
### During video conferencing, can mobile users and web users enter the same room?
Yes, make sure the [SDKAppID](https://console.cloud.tencent.com/trtc/app) and room ID are the same while the user IDs are different.

[](id:que15)
### Can I create N TRTC objects and log in to N rooms with N user IDs on the same page?
Yes. Since [version 7.6](https://intl.cloud.tencent.com/document/product/647/34615), a user can enter multiple rooms.


[](id:que16)
### How do I view the latest version number of the SDK?
- In the case of automatic loading, `latest.release` will load the latest version automatically. You don’t need to modify the version number. For detailed instructions on integration, please see [SDK Quick Integration](https://intl.cloud.tencent.com/document/product/647/35092).
- You can find the latest version number of the SDK on the release notes page.
  - For iOS & Android, please see [Release Notes (App)](https://intl.cloud.tencent.com/document/product/647/39426).
  - For web, please see [Release Notes (Web)](https://intl.cloud.tencent.com/document/product/647/39779).
  - For Electron, please see [Release Notes (Electron)](https://intl.cloud.tencent.com/document/product/647/38702).


