This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Web into your project.

## Supported Platforms

The TRTC SDK for web is based on WebRTC, which was originally released by Google and is well supported by many modern browsers such as Chrome, Edge, Firefox, Safari, and Opera. For a list of browsers supported by TRTC, see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664#supported-platforms).
- If your application scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports big and small (dual-channel) images, with more flexible screen sharing schemes and better recovery capabilities for poor network connections.


For details about the browsers supported by the TRTC SDK for web, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664).

> ! 
>- You can run the [TRTC Web SDK Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in a browser, for example, WebView, to test whether the environment fully supports WebRTC.
>- Due to patent issues, H.264 encoding, which is required for stream publishing, is unavailable for Chrome versions earlier than v88 on Huawei devices. To run the TRTC SDK for web on Chrome or Chrome WebView-based browsers on Huawei devices, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable VP8 encoding/decoding.

## URL Protocol Support
| Scenario     | Protocol             | Receive (Playback) | Send (Publish) | Share Screen | Remarks |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| Production     | HTTPS        | Supported         | Supported         | Supported     | Recommended |
| Commercial     | HTTP         | Supported         | Not supported       | Not supported   |      |
| Local development | http://localhost | Supported         | Supported         | Supported     | Recommended |
| Local development | http://127.0.0.1 | Supported         | Supported         | Supported     |      |
| Local development | http://[local IP address]  | Supported         | Not supported       | Not supported   |      |
| Local development | file:///         | Supported         | Supported         | Supported     |      |

## Firewall Configuration
The TRTC SDK for Web uses the following ports for data transfer, which should be added to the whitelist of the firewall.
- TCP port: 8687
- UDP ports: 8000, 8080, 8800, 843, 443, 16285
- Domain name: qcloud.rtc.qq.com

## Integrating the TRTC SDK for Web

### Integrating via npm

1. Use npm to install the SDK package in your project.
```
npm install trtc-js-sdk --save
```
2. Import the module in the project script.
```javascript
import TRTC from 'trtc-js-sdk';
```

### Integrating via script

Add the following code to your webpage:

```html
<script src="trtc.js"></script>
```

## Resources

Download the SDK [here](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip).

For more information on the initialization process and how to use APIs, please see the tutorials below:

| Feature                       | Sample Code                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Audio/Video call  | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)               |
| Interactive live streaming           | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)    |
| Switching cameras/mics | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)      |
| Setting local video attributes           | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)    |
| Dynamically enabling/disabling local audio/video | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html) |
| Screen sharing                   | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)                   |
| Detecting volume | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html) |
| Custom capturing and rendering | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| Limit on the number of upstream users in a room | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html) |
| Adding background music and audio effects | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html)                  |
| Environment and device check before calls| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| Network quality check before calls| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| Device plugging/unplugging check| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| Publishing to CDN| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html) |
| Enabling dual-channel mode| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| Enabling beauty filters| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| Enabling watermarking| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| Enabling cross-room communication| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |

>? Learn more about the features of the TRTC SDK for web [here](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html).
