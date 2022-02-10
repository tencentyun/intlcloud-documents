**The TWebLive SDK will no longer be iterated.** If you want to implement a web-side stream push/pull scenario, we recommend you use [TUIPusher and TUIPlayer](https://intl.cloud.tencent.com/document/product/647/43303), web-side interactive live streaming components with UI.
Different from the way TWebLive provides an integrated SDK, TUIPusher and TUIPlayer have the following features:
- Direct access to basic SDKs such as IM, TRTC, and TCPlayer, which can flexibly expand business features.
- Component source code with UI, which can be used out of the box to help launch businesses quickly.

>? **TUIPusher and TUIPlayer** and **TWebLive** are incompatible with each other in terms of design and code logic. If you have already connected to the TWebLive SDK, you need to connect to TUIPusher and TUIPlayer before using them.

## Overview
TWebLive is Tencent Cloud's interactive live streaming component for web. A new SDK developed by Tencent Cloud’s terminal R&D team, it integrates TRTC, IM, and TCPlayer, and offers features common for web-based interactive live streaming, including stream publishing, mic on/off, camera on/off, sharing and watch on WeChat, chatting, and liking. It also comes with easy-to-use [APIs](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html) that can be used for stream publishing, playback, and real-time chatting. You can use the [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) to try out the features.





## Strengths

The [TWebLive SDK](https://www.npmjs.com/package/tweblive) offers a substitute for flash streaming and significantly simplifies the process of implementing web-based stream publishing, web-based low-latency playback, CDN streaming, and real-time chatting (or on-screen comments). The example below guides you through the implementation process.


<dx-tabs>
::: Push
To use the stream pushing feature, you need to create a pusher object. A simple stream pushing feature takes only three steps to implement:
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
.then(() => {
  // 3. Enter the SDKAppID, room ID, and other information, and push streams.
  // The URL must start with `room://`.
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
.catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
:::
</dx-codeblock>
:::
::: Pull
To use the stream pulling feature, you need to create a player object. A simple stream pulling feature takes only three steps to implement:
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
// 1. Create an IM object and listen for events.
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



## Using TWebLive
### Notes
- TRTC and IM can share your account and authentication information only if you enter the same SDKAppID for your TRTC and IM apps.
- The IM application provides the basic version of content filtering capabilities for text messages. If you want to customize banned keywords, you can click **Upgrade** or go to the [purchase page](https://buy.cloud.tencent.com/avc?position=1400399435) to purchase the **Premium Edition of the content filtering service**.
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization. The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).


### Directions
<dx-tabs>
::: Method 1: via TRTC
[](id:step1)
#### Step 1. Create a TRTC application
On the left sidebar of the [TRTC console](https://console.cloud.tencent.com/trtc/app), click **Application Management** > **Create Application**, enter an app name, and click **Confirm**. Take note of the SDKAppID of the app you have created.
![](https://qcloudimg.tencent-cloud.cn/raw/9a50fca02d951862a3d0d38251835f76.png)

>? An IM app with the same SDKAppID will be created automatically.

#### Step 2: enable relayed push
1. In the [TRTC console](https://console.cloud.tencent.com/trtc/app), click **Application Management** on the left sidebar, find the app you have created, and click **Function Configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/248dbff1360ff65253fb4e8fa30826e2.png)
2. Click **Enable Relayed Push**, and select **Global auto-relayed push** for **Relayed Push Mode**. This will give each stream in a TRTC room a dedicated playback address.
![](https://qcloudimg.tencent-cloud.cn/raw/b65584a5b096481ade6e302dabedcd5f.png)

>? You can skip this step if you don’t need to enable CDN live streaming.
3. Click **Quick Start** to view and note your key.[](id:step2)
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)
4. In the [CSS console](https://console.cloud.tencent.com/live/), configure the playback domain name and CNAME record. For detailed instructions, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).

>? You can skip this step if you don't need to enable CDN live streaming.

#### Step 3: download and configure the demo source code
1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set the parameters as follows.
 - SDKAPPID: set it to the actual SDKAppID obtained in [step 1](#step1).
 - SECRETKEY: enter the actual key obtained in [step 2](#step2).
 - PUSHDOMAIN set a push domain name for CDN live streaming. Skip this if you don't need the service.
   ![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
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
5. If you want to use `script` tags to import JS files, copy `tim-js.js`, `trtc.js`, and `tweblive.js` to your project and import them in the order below.
```javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```
>!
>- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization.
>- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

#### Step 4: run the demo
Open the `index.html` file in the `dist` directory with Chrome to run the demo.
>!
>- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
>- Currently, the desktop version of Chrome offers better support for the features of the TRTC SDK for web; therefore, Chrome is recommended for the demo.
>?`TWebLive` uses the camera and mic of your device to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.

 :::
 ::: Method 2: via IM\sIM
#### Step 1: create an IM app
1. Log in to the [IM console](https://console.cloud.tencent.com/im), and click **Create Application**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7382cbcd81df7afbad1e9af641697c87.png)
2. Enter an application name and click **Confirm**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b3a630da00564cf7ef4a91b8492b646e.png)
3. On the overview page of the [IM console](https://console.cloud.tencent.com/im), you can view the status, edition, SDKAppID, creation time, and expiration date of the app created.

#### Step 2: obtain the key and activate TRTC
1. On the overview page of the [IM console](https://console.cloud.tencent.com/im), click the application you have created to go to the **Basic Configuration** page. In the **Basic Information** section, click **Display key**, and copy and save the key.
![](https://qcloudimg.tencent-cloud.cn/raw/6f284cf687e9648d209567ed32983c84.png)
>! Please store the key information properly to prevent leakage.
2. On the **Basic Configuration** page, activate TRTC.
![](https://qcloudimg.tencent-cloud.cn/raw/8a9d1ca2c395fc6ebd26298a0f5226c4.png)

#### Step 3: download and configure the demo source code
1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set the parameters as follows.
 - SDKAPPID: set it to the actual SDKAppID obtained in [step 1](#step1).
 - SECRETKEY: enter the actual key obtained in [step 2](#step2).
 - PUSHDOMAIN set a push domain name for CDN live streaming. Skip this if you don't need the service.
   ![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
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
5. If you want to use `script` tags to import JS files, copy `tim-js.js`, `trtc.js`, and `tweblive.js` to your project and import them in the order below.
```javascript
<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```
>!
>- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization.
>- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

#### Step 4: run the demo
Open the `index.html` file in the `dist` directory with Chrome to run the demo.
>!
>- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
>- Currently, the desktop version of Chrome offers better support for the features of the TRTC SDK for web; therefore, Chrome is recommended for the demo.
>?`TWebLive` uses the camera and mic of your device to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.

 :::
 </dx-tabs>

## Architecture and Supported Platforms

### TWebLive architecture

The figure below demonstrates TWebLive's architecture.
![](https://main.qcloudimg.com/raw/5d28f48be5c82c929acf46b05e02ebeb.png)
Web-based stream pushing and low-latency playback use the WebRTC technology.

If your application scenario is mainly in the education sector, consider using the [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports big and small (dual-channel) images, with more flexible screen sharing schemes and better recovery capabilities on poor network connections.

>? Proposed by Google, the WebRTC technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.

### Supported platforms

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

>! Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support the TRTC SDK for web.
>[](id:sos)



## FAQs
<dx-accordion>
::: Only public and private key can be obtained when I try to view the secret key. How do I get the secret key?
By default, TRTC and IM apps (SDKAppID) created before August 2019 use the ECDSA-SHA256 algorithm for signature calculation, which uses public and private keys. You are strongly advised to upgrade to the HMAC-SHA256 algorithm.
- To upgrade the algorithm via the TRTC console, see [FAQs > UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
- To upgrade the algorithm via the IM console, see [Basic Configuration](https://intl.cloud.tencent.com/document/product/1047/34540).
:::
::: What should I do if the client error "RtcError: sno valid ice candidate found" occurs?
This error indicates that TRTC SDK for web failed with regard to Session Traversal Utilities for NAT (STUN). Please configure your firewall policy against the environment requirements. You can use the [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) to check whether the configuration has taken effect.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, 16285
  - Domain name: qcloud.rtc.qq.com
:::
::: What should I do if the client error "RtcError:ICE/DTLS Transport connection failed" or "RtcError:DTLS Transport connection timeout" occurs?
This error indicates that TRTC SDK for web failed with regard to Session Traversal Utilities for NAT (STUN). Please configure your firewall policy against the environment requirements. You can use the [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) to check whether the configuration has taken effect.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, 16285
  - Domain name: qcloud.rtc.qq.com
:::
::: What should I do if a 10006 error occurs?
If the `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"` error occurs, log in to the [TRTC console](https://console.cloud.tencent.com/rav), find the application you have created, click **Application Info**, and check in the **Application Info** tab if your TRTC service is available.
<img src="https://qcloudimg.tencent-cloud.cn/raw/46397166ef537cb0c1acc2453b2a4a9f.png">
:::
::: What should I do if I cannot play back streams on iOS?
1. Upgrade the TWebLive SDK to 1.2.0.
2. After calling `player.startPlay()`, listen for the `PLAYER_AUTOPLAY_NOT_ALLOWED` callback, which indicates that the browser forbids autoplay.
3. After the callback is received, display a play button, and trigger [resumePlay()](https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/Player.html#resumePlay) upon clicking of the button to start playback.
For how to deal with iOS restrictions on autoplay, please see [Suggested Solutions for Autoplay Restrictions](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html).
:::
</dx-accordion>



## Summary
This document describes Tencent Cloud's new web-based interactive live streaming component TWebLive. The SDK offers an ideal substitute for the traditional Flash streaming and allows you to quickly implement web-based stream pushing, web-based low-latency streaming, CDN streaming, real-time chatting (or on-screen comments), and other features.

We also provide detailed integration instructions and a [demo](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html) for you to explore the component. Currently, TWebLive is well supported on the web.

In the future, we plan to integrate more live streaming features into the component, for example, screen sharing on the push end, image messaging, multi-line (WebRTC low-latency and CDN) watching, and co-anchoring between anchors and viewers.

References:

- <a href="https://web.sdk.qcloud.com/component/tweblive/doc/zh-cn/TWebLive.html">TWebLive API Guide</a>
- [Online demos](https://web.sdk.qcloud.com/component/tweblive/demo/latest/index.html)

