This document describes how to quickly integrate the Tencent Cloud TRTC SDK for Web into your project.

## Supported Platforms

To implement TRTC on the web, the browser is required to fully support WebRTC capabilities. Currently known browsers that support WebRTC are as listed below:

| OS | Browser/WebView | Version Requirement | Remarks |
| ------------ | -------------- | -------- | ------------------------------------ |
| iOS | Safari | 11.1.2 | As Safari still has occasional bugs, it is recommended to restrain from developing iOS applications before Apple fixes such bugs. <br >Therefore, the WeChat Mini Program solution with better compatibility is recommended for iOS.  |
| Android | TBS | 43600 | The default built-in browser kernel of WeChat and Mobile QQ is [TBS](http://x5.tencent.com/). |
| Android | Chrome | 60+ | H264 codec needs to be supported. |
| macOS          | Chrome         | 47+      | - |
| macOS          | Safari         | 11+      | - |
| Windows (PC)  | Chrome         | 52+      | - |
| Windows (PC)  | QQ Browser      | 10.2     | - |

> ?The WebView based on TBS kernel should be v43600 or above.
> You can open the [WebRTC capability test](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) page in your browser to check whether WebRTC is fully supported, such as the browser environments like WeChat Official Account.
> Chrome on Huawei devices and Chrome WebView-based browsers do not support H264 encoding.


## Environment Requirements
The TRTC SDK for Web uses the following ports for data transfer, which should be added to the whitelist of the firewall.
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

| Feature                       | Sample Code Guide   |
| -------------------------- | --------------------------- |
| Basic audio/video call  | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-01-basic-video-call.html)               |
| ILVB | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-02-live-video.html)                           |
| Switch cameras/mics | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-03-advanced-switch-camera-mic.html)      |
| Setting local video attributes  | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-04-advanced-set-video-profile.html)      |
| Dynamically enabling/disabling local audio/video | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-05-advanced-dynamic-add-video.html) |
| Sharing screen | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-06-advanced-screencast.html)   |
| Detecting volume level | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-07-advanced-detect-volume.html) |


