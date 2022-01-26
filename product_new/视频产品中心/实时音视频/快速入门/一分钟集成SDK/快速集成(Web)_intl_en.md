This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Web into your project.

## Supported Platforms

To implement TRTC on the web, the browser is required to fully support WebRTC capabilities. Currently known browsers that support WebRTC are as listed below:

| OS | Browser/WebView | Version Requirement | Remarks |
| ------------ | -------------- | -------- | ------------------------------------ |
| iOS | Safari | 11.1.2 | As Safari still has occasional bugs, it is recommended to restrain from developing iOS applications before Apple fixes such bugs. <br >Therefore, the WeChat Mini Program solution with better compatibility is recommended for iOS.  |
| Android | TBS | 43600 | The default built-in browser kernel of WeChat and Mobile QQ is [TBS](http://x5.tencent.com/). |
| Android | Chrome | 60+ | H264 codec needs to be supported. |
| macOS          | Chrome         | 47+      | - |
| macOS          | Safari         | 11+      | - |
| Windows (PC)  | Chrome         | 52+      | - |
| Windows (PC)  | QQ Browser      | 10.2     | - |

> The WebView based on TBS kernel should be v43600 or above.
> You can open the [WebRTC capability test](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) page in your browser to check whether WebRTC is fully supported, such as the browser environments like WeChat Official Account.
> Chrome on Huawei devices and Chrome WebView-based browsers do not support H264 encoding.


## Environment Requirements
The TRTC SDK for Web uses the following ports for data transfer, which should be added to the allowlist of the firewall.
- TCP port: 8687
- UDP ports: 8000, 8800, 843, 443
- Domain name: qcloud.rtc.qq.com

## Integrating the TRTC SDK for Web

### Integrating via npm

Install the SDK package by using the npm command in your project:

```
npm install trtc-js-sdk --save
```

Import the module into the project script:

```javascript
import TRTC from 'trtc-js-sdk';
```

### Integrating via script

You just need to add the following code to your webpage:

```html
<script src="trtc.js"></script>
```

## Relevant Resources

SDK download address: [click here](http://trtc-1252463788.cosgz.myqcloud.com/web/sdk/trtc.js)

For more information on the initialization process and how to use APIs, please see the guide below:

| Feature                       | Sample Code Guide   |
| -------------------------- | --------------------------- |
| Basic audio/video call  | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)               |
| ILVB | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)                           |
| Switch cameras/mics | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)      |
| Setting local video attributes  | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)      |
| Dynamically enabling/disabling local audio/video | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html) |
| Sharing screen | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)   |
| Detecting volume level | [Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html) |
