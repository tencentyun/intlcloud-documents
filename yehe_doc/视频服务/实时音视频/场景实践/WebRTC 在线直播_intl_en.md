## Overview

TWebLive is Tencent Cloud’s interactive live streaming component for web. A new SDK developed by Tencent Cloud’s terminal R&D team, it integrates TRTC, IM, and TCPlayer, and offers features common for web-based interactive live streaming, including stream publishing, mic on/off, camera on/off, sharing and watch on WeChat, chatting, and liking. It also comes with easy-to-use [APIs](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html) that can be used for stream publishing, playback, and real-time chatting. You can use the [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) to try out the features.




## Strengths

The [TWebLive SDK](https://www.npmjs.com/package/tweblive) offers a substitute for Flash streaming and significantly simplifies the process of implementing web-based stream publishing, web-based low-latency playback, CDN streaming, and real-time chatting (or on-screen comments). The example below guides you through the implementation process.


<dx-tabs>
::: Push
To use the push feature, you need to create a pusher object. A simple push feature takes only three steps to implement:
<dx-codeblock>
::: html html
<div id="pusherView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a pusher object.
let pusher = TWebLive.createPusher({ userID: 'your userID' });

// 2. Set the rendering view and have the mic capture audio and the camera capture video (720p by default).
pusher.setRenderView({
  elementID: 'pusherView',
  audio: true,
  video: true
}).then(() => {
  // 3. Enter the SDKAppID, room ID, and other information, and push streams.
  // The URL must start with `room://`.
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: Pull
To use the pull feature, you need to create a player object. A simple pull feature takes only three steps to implement:
<dx-codeblock>
::: html html
<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a player object.
let player = TWebLive.createPlayer();

// 2. Set the rendering view.
player.setRenderView({ elementID: 'playerView' });

// 3. Enter an FLV or HLS URL and other information and pull CDN streams for playback. The URL must start with `https://`.
// Alternatively, enter the SDKAppID, room ID, and other information and pull WebRTC low-latency streams for playback. The URL must start with `room://`.
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // Replace it with a valid playback URL.
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // Replace it with a valid playback URL.

// let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: Interaction
To allow the anchor and audience to chat with each other, you need to create an IM object. A simple message sending/receiving feature takes only three steps to implement:
<dx-codeblock>
::: javascript javascript
// 1. Create an IM object and subscribe to events.
let im = TWebLive.createIM({
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM app when connecting.
});
// Listen for events including `IM_READY`, `IM_TEXT_MESSAGE_RECEIVED`, etc.
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// Listen for this event on the access side, and call the SDK to send messages or enable other features.
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// Text message received and displayed on screen
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2. Log in to the IM console
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // Login successful
  if (imResponse.data.repeatLogin === true) {
    // This indicates that the account is already logged in
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // Message about failed login
});

// 3. Enter the live streaming room
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // Room entry successful
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: // Already in the room
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // Message about failed room entry
});
</script>
:::
</dx-codeblock>
:::
</dx-tabs>

To help you reduce development and labor costs, in addition to the TWebLive SDK, we have published a [demo](https://github.com/tencentyun/TWebLive) applicable for both desktop and mobile browsers on GitHub. You can fork and clone the demo project to your local environment and run it after minor modifications, or integrate the demo into your own project for official launch.



## Use
### Notes
- TRTC and IM can share your account and authentication information only if you enter the same SDKAppID for your TRTC and IM apps.
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization. The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).


### Directions
<dx-tabs>
::: Method 1: via TRTC
[](id:step1)
#### Step 1. Create a TRTC application
On the left sidebar of the [TRTC console](https://console.cloud.tencent.com/trtc/app), click **Application Management** > **Create Application**, enter an application name, and click **Confirm**. Take note of the `SDKAPPID` of the application you have created.

<dx-alert infotype="explain"> An IM application with the same `SDKAppID` will be created automatically.</dx-alert>

#### Step 2: enable relayed push
1. In the [TRTC console](https://console.cloud.tencent.com/trtc/app), click **Application Management** on the left sidebar, find the app you have created, and click **Function Configuration**.
2. Click **Enable Relayed Push**, and select **Global auto-relayed push** for **Relayed Push Mode**. This will give each stream in a TRTC room a dedicated playback address.
<dx-alert infotype="explain">You can skip this step if you don’t need to enable CDN live streaming.</dx-alert>
  
3. Click **Quick Start** to view and note your key.[](id:step2)
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)
4. In the [CSS console](https://console.cloud.tencent.com/live/), configure the playback domain name and CNAME record. For detailed instructions, please see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

<dx-alert infotype="explain">You can skip this step if you don’t need to enable CDN live streaming.</dx-alert>

#### Step 3: download and configure the demo source code

1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set the parameters as follows.
 - SDKAPPID: set it to the actual SDKAppID obtained in [step 1](#step1).
 - SECRETKEY: enter the actual key obtained in [step 2](#step2).
 - PUSHDOMAIN set a push domain name for CDN live streaming. Skip this if you don’t need the service.
3. Install the latest `tim-js-sdk`, `trtc-js-sdk`, and `tweblive` via npm. If your project already has `tim-js-sdk` or `trtc-js-sdk`, upgrade it to the latest version.
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
4. Import `tweblive` to your project.
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```
5. If you want to install the demo source code by referring to external files in the script tag, copy `tim-js.js`, `trtc.js`, and `tweblive.js` to your project and import them in the order below.
```javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```
<dx-alert infotype="notice"> 
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization.
- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).</dx-alert>

#### Step 4: run the demo
Open the `index.html` file in the `dist` directory with Chrome to run the demo.
<dx-alert infotype="notice"> 
- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
- Currently, the desktop version of Chrome offers better support for the features of TRTC SDK for web; therefore, Chrome is recommended for the demo.
- TWebLive uses the camera and mic to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.</dx-alert>
:::
  
::: Method 2: via IM\sIM
#### Step 1. Create an IM application
1. Log in to the [IM console](https://console.cloud.tencent.com/im), and click **Create Application**.
2. Enter an app name, and click **Confirm**.
3. On the overview page of the [IM console](https://console.cloud.tencent.com/im), you can view the status, edition, SDKAppID, creation time, and expiration date of the app created.

#### Step 2: obtain the key and activate TRTC
1. On the overview page of the [IM console](https://console.cloud.tencent.com/im), click the app you have created to go to the **Basic Configuration** page. In the **Basic Information** section, click **Display key**, and copy and save the key.
<dx-alert infotype="notice"> Please store the key information properly to prevent leakage.</dx-alert>
2. On the **Basic Configuration** page, activate TRTC.

#### Step 3: download and configure the demo source code
1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set the parameters as follows.
 - SDKAPPID: set it to the actual SDKAppID obtained in [step 1](#step1).
 - SECRETKEY: enter the actual key obtained in [step 2](#step2).
 - PUSHDOMAIN set a push domain name for CDN live streaming. Skip this if you don’t need the service.
3. Install the latest `tim-js-sdk`, `trtc-js-sdk`, and `tweblive` via npm. If your project already has `tim-js-sdk` or `trtc-js-sdk`, upgrade it to the latest version.
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
4. Import `tweblive` to your project.
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```
5. If you want to install the demo source code by referring to external files in the script tag, copy `tim-js.js`, `trtc.js`, and `tweblive.js` to your project and import them in the order below.
```javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```
<dx-alert infotype="notice"> 
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization.
- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).</dx-alert>

#### Step 4: run the demo
Open the `index.html` file in the `dist` directory with Chrome to run the demo.
<dx-alert infotype="notice"> 
- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
- Currently, the desktop version of Chrome offers better support for the features of TRTC SDK for web; therefore, Chrome is recommended for the demo.
- TWebLive uses the camera and mic to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.</dx-alert>

:::
</dx-tabs>

## Architecture and Supported Platforms

### TWebLive architecture

The figure below demonstrates TWebLive’s architecture.
![](https://main.qcloudimg.com/raw/403cca1412a4a99a2b4abdd326b65c5b.png)
Web-based stream pushing and low-latency playback use the WebRTC technology.

- If your app scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports two-channel big/small video images, with more flexible screen sharing schemes and better recovery capabilities on poor network connections.

>?Proposed by Google, the WebRTC technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.

### Supported Platforms

|  OS   |          Browser          | Minimum Browser Version Requirement | Receiving (Playback) | Sending (Publish) |
| :---------: | :--------------------------: | :----------------: | :----------: | :----------: |
|   macOS    |     Safari (desktop)     |        11+         |     Supported     |     Supported          |
|  macOS    |     Chrome (desktop)     |        56+         |     Supported     |     Supported     |
|   macOS    |    Firefox (desktop)     |        56+         |     Supported     |     Supported     |
|   macOS    |      Edge (desktop)      |        80+         |     Supported     |     Supported     |
|   Windows   |     Chrome (desktop)     |        56+         |     Supported     |     Supported     |
|   Windows   | QQ browser (desktop, WebKit core) |       10.4+        |     Supported     |     Supported     |
|   Windows   |    Firefox (desktop)     |        56+         |     Supported     |     Supported     |
|   Windows   |      Edge (desktop)      |        80+         |     Supported     |     Supported     |
| iOS 11.1.2+ |    Safari (mobile)     |        11+         |     Supported     |     Supported     |
| iOS 12.1.4+ |         WeChat embedded browser         |         -          |     Supported     |    Not supported    |
| iOS 14.3+   |         WeChat embedded browser         |   WeChat 6.5+ |     Supported     |    Supported     |
|   Android   |       QQ browser (mobile)       |         -          |    Not supported    |    Not supported    |
|   Android   |       UC browser (mobile)       |         -          |    Not supported    |    Not supported    |
|   Android   |   WeChat embedded browser (TBS core)   |         -          |     Supported     |     Supported     |
|   Android   |  WeChat embedded browser (XWEB core)   |         -          |     Supported     |    Not supported    |

>! Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support TRTC SDK for web.
>[](id:sos)



## FAQs
<dx-accordion>
::: Only public and private key can be obtained when I try to view the secret key. How do I get the secret key?
By default, TRTC and IM applications (`SDKAppID`) created before August 2019 use the ECDSA-SHA256 algorithm for signature calculation, which uses public and private keys. You are strongly advised to upgrade to the HMAC-SHA256 algorithm.
- To upgrade the algorithm via the TRTC console, please see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
- To upgrade the algorithm via the IM console, please see [Basic Configuration](https://intl.cloud.tencent.com/document/product/1047/34540).
:::
::: What should I do if the client error "RtcError:\sno\svalid\sice\scandidate\sfound" occurs?**
This error indicates that the TRTC SDK for web failed to establish a connection for media transfer. Please configure your firewall policy against the environment requirements. You can use the [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) to check whether the configuration has taken effect.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, 16285
  - Domain name: qcloud.rtc.qq.com
:::
::: What should I do if the client error "RtcError:ICE/DTLS\sTransport\sconnection\sfailed" or "RtcError:DTLS\sTransport\sconnection\stimeout" occurs?
This error indicates that the TRTC SDK for web failed to establish a connection for media transfer. Please configure your firewall policy against the environment requirements. You can use the [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) to check whether the configuration has taken effect.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, 16285
  - Domain name: qcloud.rtc.qq.com
:::
::: What should I do if a \s10006\serror\s error occurs?
If the `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"` error occurs, log in to the [TRTC console](https://console.cloud.tencent.com/rav), find the application you have created, click **Application Info**, and check in the **Application Info** tab if your TRTC service is available.<img src="https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png">
:::
::: What should I do if I cannot play back streams on iOS\s?
1. Upgrade the TWebLive SDK to 1.2.0.
2. After calling `player.startPlay()`, listen for the `PLAYER_AUTOPLAY_NOT_ALLOWED` callback, which indicates that the browser forbids autoplay.
3. After the callback is received, display a play button, and trigger [resumePlay()](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/Player.html#resumePlay) upon clicking of the button to start playback.
For how to deal with iOS restrictions on autoplay, please see [Suggested Solutions for Autoplay Restrictions](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html).
:::
</dx-accordion>



## Summary
This document describes Tencent Cloud's new web-based interactive live broadcasting component TWebLive. The SDK offers an ideal substitute for the traditional Flash streaming and allows you to quickly implement web-based stream pushing, web-based low-latency streaming, CDN streaming, real-time chatting (or on-screen comments), and other features.

We also provide detailed integration instructions and a [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) for you to explore the component. Currently, TWebLive is well supported on the web.

In the future, we plan to integrate more live streaming features into the component, for example, screen sharing on the push end, image messaging, multi-line (WebRTC low-latency and CDN) watching, and co-anchoring between anchors and viewers.

References:

- <a href="https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html">TWebLive API Guide</a>
- [Online demos](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)


