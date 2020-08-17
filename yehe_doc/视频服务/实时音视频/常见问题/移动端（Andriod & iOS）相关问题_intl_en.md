### Which system volume types are supported by the mobile client (for Android/iOS)?
Two system volume types, i.e., call volume and media volume, are supported.
- Call volume is specially designed for call scenarios on mobile phones. It uses the acoustic echo cancellation (AEC) feature built in phones and has a lower sound quality than media volume, and its volume level cannot be adjusted to 0 with volume buttons, but it supports mics on Bluetooth earphones.
- Media volume is specially designed for music scenarios on mobile phones. It has a higher sound quality than call volume, and its volume level can be adjusted to 0 with volume buttons. When using it, if you want to enable the AEC feature, the SDK will enable its built-in acoustic processing algorithms to further process the audio. With media volume, only the mics on phones instead of those on Bluetooth earphones can be used to capture audio.

### How do I set the resolution to 1080p for push in the mobile SDK?
1080p is defined as 114 in `TX_Enum_Type_VideoResolution`. You can directly set the resolution by passing in the enumerated value.

### Can I enter a room created on Mini Program through the mobile client?
Yes. TRTC supports interconnection across all platforms.

### How does the TRTC mobile client implement screen sharing?	
From v7.2 on, the entire screen can be shared on Android, and the screen of a single application can be shared on iOS. For more information, please see the source code in the [official demo](https://github.com/tencentyun/TRTCSDK).

### Does the TRTC mobile client for Android support 64-bit arm64-v8a architecture?
From TRTC v6.3 on, the arm64-v8a architecture is supported as ABI.

### Is Swift integration supported for iOS?
Yes. You can directly integrate the SDK in the process of integrating third-party libraries. For more information, you can also see [Running Demo (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35086).

### Does the TRTC SDK support running in the background on iOS?
Yes. You can select the current project, set **Background Modes** under **Capabilities** to **ON**, and check **Audio, AirPlay and Picture in Picture** to implement execution in the background as shown below:
![](https://main.qcloudimg.com/raw/d960dfec88388936abce2d4cb77ac766.jpg)
