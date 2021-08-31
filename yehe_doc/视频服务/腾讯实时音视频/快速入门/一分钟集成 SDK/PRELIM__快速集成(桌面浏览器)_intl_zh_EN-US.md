This document describes how to quickly integrate TRTC SDK for desktop browsers into your project.

## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.
- If your application scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports two-channel big/small video images, with more flexible screen sharing schemes and better recovery capabilities on poor network connections.


<table>
<tr>
<th>OS</th>
<th width="22%">Browser</th><th>Minimum Browser<br>Version Requirement</th><th width="16%">Receive (Playback)</th><th width="16%">Send (Publish)</th><th>Screen Sharing</th><th>SDK Version Requirement</th>
</tr><tr>
<td rowspan="4">macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Safari 13+)</td>
<td>-</td>
</tr>
<tr>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
<td>-</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>4.7.0+</td>
</tr>
<tr>
<td  rowspan="4">Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
<td>-</td>
</tr>
<tr>
<td>QQ browser (desktop, WebKit core)</td>
<td>10.4+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>Safari (mobile)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat built-in browser</td>
<td>-</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat built-in browser</td>
<td>WeChat 6.5+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td  rowspan="4">Android</td>
<td>QQ browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>UC browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat built-in browser (TBS core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat built-in browser (XWEB core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
</table>


> ! 
>- You can perform [WebRTC Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in a browser (for example, WeChat’s built-in browser) to test whether the environment fully supports WebRTC.
>- Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support TRTC SDK for desktop browsers.


## Firewall Configuration
TRTC SDK for desktop browsers uses the following ports and domain name for data transfer, which should be added to the allowlist of the firewall.
- TCP port: 8687
- UDP ports: 8000, 8080, 8800, 843, 443, 16285
- Domain name: qcloud.rtc.qq.com

## Integrating the SDK

### Integrating via npm

Use npm to install the SDK package in your project.

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

## Resources

Download the SDK [here](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip).

For more information on the initialization process and how to use APIs, please see the tutorials below:

| Feature                       | Sample Code                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Audio/Video call  | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html)               |
| Interactive live streaming | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-12-basic-live-video.html)                           |
| Switching cameras/mics | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html)      |
| Setting local video attributes  | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-14-basic-set-video-profile.html)      |
| Dynamically enabling/disabling local audio/video | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-15-basic-dynamic-add-video.html) |
| Screen sharing                   | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)                   |
| Detecting volume | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-17-basic-detect-volume.html) |
| Custom capturing and rendering | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-20-advanced-customized-capture-rendering.html) |
| Limiting the number of upstream users in a room | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-04-info-uplink-limits.html) |
| Adding background music and audio effects | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-22-advanced-audio-mixer.html)                  |

