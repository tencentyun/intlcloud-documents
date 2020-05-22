
### Does TRTC support live streaming co-anchoring?
Yes. For detailed directions, please see:
- [Online Live Streaming (iOS and macOS)](https://intl.cloud.tencent.com/document/product/647/35107)
- [Online Live Streaming (Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [Online Live Streaming (Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [Online Live Streaming (Desktop Browser)](https://intl.cloud.tencent.com/document/product/647/35110)


### How many rooms can be created in TRTC at the same time?
There can be up to 4,294,967,294 concurrent rooms, and there is no limit on the cumulative number of rooms.

### What is the maximum bandwidth supported by the video server of TRTC?
Unlimited.

### How many people can be in the same video call in TRTC?
- In call mode, a single room can sustain up to 300 concurrent online users, and up to 50 of them can simultaneously enable the camera or mic.
- In live streaming mode, a single room can sustain up to 100,000 concurrent online viewers, and up to 50 of them can simultaneously enable the camera or mic as anchors.


### What is the value range of the TRTC room ID?
The room number can range from 1 to 4294967295 and is maintained and assigned on your own.

### Does TRTC support deployment in a private cloud?
No.

### To enable relayed live streaming in TRTC, do I need to get an ICP filing for my domain name?
To enable relayed live streaming, according to the requirements of applicable authorities, the playback domain name needs an ICP filing before it can be used. For more information, please see [Watch over CDN](https://intl.cloud.tencent.com/document/product/647/35242).

### How long is the average delay in TRTC?
The average end-to-end delay around the globe is less than 300 ms.

### Does TRTC support active calls?
This feature can be implemented together with the signaling channel. For example, you can use the custom message feature of [IM](https://intl.cloud.tencent.com/product/im) to make calls. For more information, please see the scenario-specific demos in the [SDK](https://intl.cloud.tencent.com/document/product/647/34615) source code.

### Does TRTC support Bluetooth earphones during one-to-one video call?
Yes.

### Which browsers are supported by TRTC?
The list of supported browsers is as shown below.

| OS | Browser | Minimum Version Requirement | Receipt (Playback) | Sending (Mic-on) |
|:-------:|:-------:|:-------:|:-------:|:-------:|
| macOS | Safari (desktop) | 11+ | Supported | Supported |
| macOS | Chrome (desktop) | 47+ | Supported | Supported |
| Windows | Chrome (desktop) | 52+ | Supported | Supported |
| Windows | QQ Browser (desktop) | 10.2 | Supported | Supported |
| iOS | Safari (mobile) | 11.1.2 | Supported | Supported |
| iOS | WeChat embedded browser | 12.1.4 | Supported | Not supported |
| Android | QQ Browser (mobile) | - | Not supported | Not supported |
| Android | UC Browser (mobile) | - | Not supported | Not supported |
| Android | WeChat embedded browser | - | Not supported | Not supported |

### Can TRTC be used outside Mainland China?
Yes.

### Does TRTC support screen sharing on PC?
Yes. For more information on the screen sharing API, please see [Windows (C++) API](https://intl.cloud.tencent.com/document/product/647/35131#.E5.B1.8F.E5.B9.95.E5.88.86.E4.BA.AB.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3.E5.87.BD.E6.95.B0) or [Windows (C#) API](https://intl.cloud.tencent.com/document/product/647/35136#.E8.BE.85.E6.B5.81.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3.E5.87.BD.E6.95.B0). You can also use the [Electron API](https://intl.cloud.tencent.com/document/product/647/35141).

### Can TRTC be used in a WeChat Official Account?

Due to the restrictions of WeChat Official Account, you are recommended to use the SDK for WeChat Mini Program for a better user experience.

### Can I share local video files in TRTC?

Yes. This can be implemented through the [custom collection](https://intl.cloud.tencent.com/document/product/647/35158) feature.

### Can TRTC record live streaming videos and store the recording files locally on the phone?
Recording files cannot be stored locally on the phone. Video recording files will be stored on the VOD platform by default. You can download and save them to the phone by yourself. For more information, please see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).


### Does TRTC support pure real-time audio?
Yes.

### What are the limits on room member quantity when TRTC is used to implement group chat?

- In call mode, a single room can sustain up to 300 concurrent online users, and up to 50 of them can simultaneously enable the camera or mic.
- In live streaming mode, a single room can sustain up to 100,000 concurrent online viewers, and up to 50 of them can simultaneously enable the camera or mic.

### Can there be more than one channel of screen sharing in the same room at the same time?
Currently, there can only be one secondary channel of screen sharing in a room.

### When window sharing (SourceTypeWindow) is specified, will the resolution of the video stream change as the window size changes?
By default, the SDK will automatically adjust the encoding parameters according to the shared window size.
If you want a fixed resolution, you need to call the `setSubStreamEncoderParam` API to set the encoding parameters for screen sharing or specify the corresponding encoding parameters when calling `startScreenCapture`.
