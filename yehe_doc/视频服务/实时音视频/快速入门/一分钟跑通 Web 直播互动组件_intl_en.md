[TWebLive](https://trtc.qcloud.com/tweblive/index.html#/) is Tencent Cloud’s interactive live streaming component for the web. It is a new [SDK](https://www.npmjs.com/package/tweblive) developed by Tencent Cloud that integrates [TRTC](https://intl.cloud.tencent.com/product/trtc) and [IM](https://intl.cloud.tencent.com/product/im). It provides features common in web-based interactive live streaming, including stream pushing, mic on/off, camera on/off, sharing and watching on WeChat, chatting, and liking. It also integrates simple and easy-to-use [APIs](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html) that allow quick implementation of features such as web-based stream pushing/pulling and real-time chatting.

## Demonstration


## Strengths

The SDK offers a substitute for Flash streaming and significantly simplifies the process of implementing web-based stream pushing, low-latency web streaming, CDN streaming, and real-time chatting (or on-screen comments). The example below helps guide you through the implementation process.

### Push
To use the push feature, you need to create a pusher object. A simple push feature takes only three steps to implement:
```
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
  // 3. Enter an `sdkappid`, a `roomid`, and other information, and push streams.
  // The URL must start with `room://`.
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
.catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
```
### Pull
To use the pull feature, you need to create a player object. A simple pull feature takes only three steps to implement:

```
<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a player object.
let player = TWebLive.createPlayer();

// 2. Set the rendering view.
player.setRenderView({ elementID: 'playerView' });

// 3. Enter an FLV or HLS URL and other information and pull CDN streams for playback. The URL must start with `https://`.
// Alternatively, enter the `sdkappid`, `roomid`, and other information and pull WebRTC low-latency streams for playback. The URL must start with `room://`.
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // Replace it with a valid playback URL.
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // Replace it with a valid playback URL.

// let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
```
### Interaction
To allow the anchor and viewers to chat or interact with each other, you need to create an IM object. A simple message sending/receiving feature takes only three steps to implement:

```
// 1. Create an IM object and subscribe to events.
let im = TWebLive.createIM({
  SDKAppID: 0 // Replace 0 with the `SDKAppID` of your IM app when connecting.
});
// Subscribe to events including `IM_READY`, `IM_TEXT_MESSAGE_RECEIVED`, etc.
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// Subscribe to this event on the access side, and you can call the APIs of the SDK to send messages or enable other features.
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// Text message received and displayed on screen
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2. Log in to the IM console.
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // Login successful.
  if (imResponse.data.repeatLogin === true) {
    // This indicates that the account is already logged in.
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // Message about the login failure
});

// 3. Enter the live streaming room.
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // Room entry successful
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: // You are already in the room.
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // Message about the room entry failure
});
```

>? To help you further reduce development and labor costs, in addition to the TWebLive SDK, we have published a [demo](https://github.com/tencentyun/TWebLive) applicable for both PCs and mobile browsers on GitHub. You can fork and clone the demo project to your local environment and run it after minor modifications, or integrate the demo into your own project for official launch.

## Integrating the SDK
### Notes
- TRTC and IM can share your account and authentication information only if you enter the same `SDKAppID` for your TRTC and IM applications.
- You can use the content filtering feature of the basic edition of IM to filter text messages. If you want to customize sensitive words, click **Upgrade** or go to the [**purchase page**](https://buy.cloud.tencent.com) to purchase [Content Filtering - Professional Edition](https://intl.cloud.tencent.com/document/product/1047/34350).
- Local calculation of `UserSig` is for development and local debugging only and not for official launch. If your `SECRETKEY` is leaked, attackers can steal your Tencent Cloud traffic.
- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).


[](id:step1)
### Step 1. Create an application.
#### TRTC
```
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Go to [**Application Management**](https://console.cloud.tencent.com/trtc/app), click **Create Application**, enter an application name, and click **Confirm**.
>? After you create a TRTC application, the [IM console](https://console.cloud.tencent.com/im) will create an IM application with the same `SDKAppID`
```
#### IM
```
1. Log in to the [IM Console](https://console.cloud.tencent.com/im).
2. Click **Create Application**, enter your application name in the dialog box that pos up, and click **Confirm**.
```

[](id:step2)
### Step 2. Obtain your `SDKAppID` and secret key.
#### TRTC
1. Go to **[Application Management](https://console.cloud.tencent.com/trtc/app)**, find your application, and click **Application Info** on the right to go to the details page.
2. In the **Application Info** section, click the copy button, and note your `SDKAppID`.
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
3. Go to the **Quick Start** tab and click **Copy Secret Key** in **Step 2: obtain the secret key to issue UserSig**.
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>? Follow these steps to enable CDN live streaming:
>1. In **Application Management** > **Function Configuration**, [enable relayed push](https://intl.cloud.tencent.com/zh/document/product/647/39080#open_bypass), after which each channel in a TRTC room will have its own playback address.
2. In the [LVB console](https://console.cloud.tencent.com/live/), configure the playback domain name and CNAME record. For detailed instructions, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).
#### IM
```
After creating an application, you can view its status, edition, `SDKAppID`, creation time, and expiration time on the overview page of the console.
1. Find and click the application you created to go the details page.
2. In the **Basic Information** section:
	- Click the copy button and note your `SDKAppID`.
	- Click **Display Key** and **Copy**, and note the key.
>! Key is sensitive information. Keep it confidential and do not share it with others.
3. In the **Activate TRTC** section, click **Activate** and **Confirm** in the dialog box that pops up to active TRTC.
```

>!
>- Local calculation of `UserSig` is for development and local debugging only and not for official launch. If your `SECRETKEY` is leaked, attackers can steal your Tencent Cloud traffic.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How to Calculate UserSig on the Server](https://intl.cloud.tencent.com/document/product/647/35166).


[](id:step3)
### Step 3. Download and configure the demo source code.

1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set parameters as follows.<ul style="margin:0">
<li/>SDKAPPID: set it to the actual `SDKAppID` obtained in <a href="#step2">Step 1</a>.
 <li/>SECRETKEY: set it to the actual key obtained in <a href="#step2">step 2</a>.
 <li/>PLAYDOMAIN: set the playback domain name for CDN live streaming. You don’t need to set this parameter if you don’t need the service.
 </ul>
3. Integrate the demo source code.
###  Installing via npm
1. Install the latest `tim-js-sdk`, `trtc-js-sdk`, and `tweblive` via npm.
```
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
>? If your project already has `tim-js-sdk` or `trtc-js-sdk`, upgrade it to the latest version.
2. Import `tweblive` to your project.
```
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```
### Installing via script tags
If you want to install the demo source code by referring to external files in the script tag, copy `tim-js.js`, `trtc.js`, and `tweblive.js` to your project and import them in the order below.
```javascript
<script src="trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```


[](id:step4)
### Step 4. Run the demo.

Open the `index.html` file in the `dist` directory with Chrome to run the demo.
>!
>- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers better support for the features of TRTC SDK for desktop browsers; therefore, Chrome is recommended for the demo.
>- TWebLive uses the camera and mic to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.



## Architecture and Supported Platforms
### TWebLive architecture
### Supported Platforms
Web-based stream pushing and low-latency streaming use the WebRTC technology. Proposed by Google, the technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.

- If your application scenario is mainly in the education sector, consider using [Electron](https://intl.cloud.tencent.com/document/product/647/35097) for the teacher end, which supports big/small video images and has more flexible screen sharing schemes and better recovery capabilities on poor network connections.

|  OS   |          Browser          | Minimum Browser Version Requirement | Receiving (Playback) | Sending (Broadcast) |
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
|   Android   |       QQ browser (mobile)       |         -          |    Not supported    |    Not supported    |
|   Android   |       UC browser (mobile)       |         -          |    Not supported    |    Not supported    |
|   Android   |   WeChat embedded browser (TBS core)   |         -          |     Supported     |     Supported     |
|   Android   |  WeChat embedded browser (XWEB core)   |         -          |     Supported     |    Not supported    |

>! Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support TRTC SDK for desktop browsers.


## FAQs
1.Only public and private key can be obtained when I try to view the secret key. How do I get the secret key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new secret key.
2.What should I do if the client error "RtcError:\sno\svalid\sice\scandidate\sfound" occurs?
It indicates that TRTC SDK for desktop browsers failed with regard to hole punching via Session Traversal Utilities for NAT (STUN). Please check your firewall policy against the environment requirements.
3.What should I do if the client error "tcError:\sICE/DTLS\sTransport\sconnection\sfailed" or "RtcError:\sDTLS\sTransport\sconnection\stimeout" occurs?
This error indicates that TRTC SDK for desktop browsers failed to establish a media transport connection. Please check your firewall configuration against the environment requirements.
4.What should I do if a `10006\serror\s` error occurs?
If the `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"` error occurs, log in to the [TRTC console](https://console.cloud.tencent.com/rav), find the application you created, click **Application Info**, and check in the **Application Info** tab if your TRTC service is available.
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)



## Summary

This document describes Tencent Cloud’s new web-based interactive live broadcasting component TWebLive. The SDK offers an ideal substitute for the traditional Flash streaming and allows you to quickly implement web-based stream pushing, web-based low-latency streaming, CDN streaming, real-time chatting (or on-screen comments), and other features.

We also provide detailed integration instructions and a [demo](https://trtc.qcloud.com/tweblive/index.html#/) for you to explore the component. Currently, TWebLIve is well supported by mainstream desktop browsers.

In the future, we plan to integrate more live streaming features into the component, for example, screen sharing on the push end, image messaging, multi-line (WebRTC low-latency and CDN) watching for viewers, and co-anchoring.

References

- [TWebLive API Guide](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [Demo](https://trtc.qcloud.com/tweblive/index.html#/)

