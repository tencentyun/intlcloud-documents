## Demonstration

This document describes how to quickly enable browser-based live streaming features, including stream pulling and pushing, chat rooms, and co-anchoring.

## How It Works

[**TWebLive**] is a browser-based live streaming component Tencent Cloud developed based on its TRTC, IM and CDN services. With this component, you can use simple code to enable features including stream pushing/pulling and chat rooms.

### Stream pushing
To use the stream pushing feature, you need to create a pusher object. A simple stream pushing feature takes only three steps to implement:
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
</script>
```
### Stream pulling
To use the stream pulling feature, you need to create a player object. A simple stream pulling feature takes only three steps to implement:

```
<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a player object.
let player = TWebLive.createPlayer();

// 2. Set the rendering view.
player.setRenderView({ elementID: 'playerView' });

// 3-1. Enter a CDN playback address in the FLV or HLS format, which must start with `https://`.
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // Replace it with a valid playback URL.
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // Replace it with a valid playback URL.

// 3-2. You can also enter a WebRTC playback address that starts with `room://`. Such addresses allow ultra-low-latency playback.
let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
```
### Chat room
To allow the anchor and viewers to chat with each other, you need to create an IM object. A simple message sending/receiving feature takes only three steps to implement:

```
// 1. Create an IM object and listen for events.
let im = TWebLive.createIM({
  SDKAppID: 0 // Replace 0 with the `SDKAppID` of your IM app when connecting.
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

// 2. Log in to IM.
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // Login succeeds.
  if (imResponse.data.repeatLogin === true) {
    // This indicates that the account is already logged in.
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // Message about failed login
});

// 3. Enter the live streaming room.
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
```

>? To help you reduce development and labor costs, in addition to the TWebLive SDK, we have published a [demo](https://github.com/tencentyun/TWebLive) applicable for both desktop and mobile browsers on GitHub. You can fork and clone the demo project to your local environment and run it after minor modifications, or integrate the demo into your own project for official launch.

## Integration Instructions

<span id="step1"></span>
### Step 1. create an application.
First, you need to create an application in the TRTC console. Tencent Cloud will automatically bind the application with the IM application having the same `SDKAppID`.

1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Go to [**Application Management**](https://console.cloud.tencent.com/trtc/app), click **Create Application**, enter an application name, and click **Confirm**.

<span id="step2"></span>
### Step 2. Obtain the `SDKAppID` and key.
1. Go to **[Application Management](https://console.cloud.tencent.com/trtc/app)**, find your application, and click **Application Info** on the right to go to the details page.
2. In **Application Info** section, click the copy button, and note the `SDKAppID`.
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
3. Go to the **Quick Start** tab and click **Copy Secret Key** in **Step 2: obtain the secret key to issue UserSig**.
    ![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>!
>- Local calculation of `UserSig` is for development and local debugging only and not for official launch. If your `SECRETKEY` is leaked, attackers can steal your Tencent Cloud traffic.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="step3"></span>
### Step 3. Enable CDN live streaming (optional).
To enable CDN live streaming, you need to activate Tencent Cloud CSS. Follow the steps below to enable the feature.
1. In **Application Management** > **Function Configuration**, [enable relayed push](https://intl.cloud.tencent.com/document/product/647/39080). This will give each channel in a TRTC room a playback address.
2. In the [CSS console](https://console.cloud.tencent.com/live/), configure the playback domain name and CNAME record. For detailed instructions, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242).


<span id="step4"></span>

### Step 4. Download and configure the demo source code.
1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set the parameters as follows.<ul style="margin:0">
   <li/>SDKAPPID: set it to the actual `SDKAppID` obtained in <a href="#step2">Step 2</a>.
    <li/>SECRETKEY: set it to the actual key obtained in <a href="#step2">step 2</a>.
    <li/>PLAYDOMAIN: set a playback domain name for CDN live streaming. Skip this if you don’t need the service.
    </ul>
3. Integrate the demo source code.
#### Installing via npm
1. Install the latest `tim-js-sdk`, `trtc-js-sdk`, and `tweblive` via npm.
```javascript
npm install tim-js-sdk --save
npm install trtc-js-sdk --save
npm install tweblive --save
```
>? If your project already has `tim-js-sdk` or `trtc-js-sdk`, upgrade it to the latest version.
2. Import `tweblive` to your project.
```javascript
import TWebLive from 'tweblive'
Vue.prototype.TWebLive = TWebLive
```

#### Installing via script tags
If you want to install the demo source code by referring to external files in the script tag, copy `tim-js.js`, `trtc.js`, and `tweblive.js` to your project and import them in the order below.
```
<script src="trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tweblive.js"></script>
```

<span id="step5"></span>

### Step 5. Run the demo.

Open the `index.html` file in the `dist` directory with Chrome to run the demo.

>!
>
>- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers better support for the features of TRTC SDK for desktop browsers; therefore, Chrome is recommended for the demo.
>- TWebLive uses the camera and mic to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.

### Supported Platforms

Browser-based stream pushing and low-latency playback are based on the WebRTC technology. Proposed by Google, the technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.

- If your application scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097) for the teacher end, which supports big/small video images and has more flexible screen sharing schemes and better recovery capabilities on poor network connections.

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
| iOS 14.3+   |         WeChat embedded browser         |   WeChat 6.5+ |     Supported     |    Supported     |
|   Android   |       QQ browser (mobile)       |         -          |    Not supported    |    Not supported    |
|   Android   |       UC browser (mobile)       |         -          |    Not supported    |    Not supported    |
|   Android   |   WeChat embedded browser (TBS core)   |         -          |     Supported     |     Supported     |
|   Android   |  WeChat embedded browser (XWEB core)   |         -          |     Supported     |    Not supported    |

>! Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support TRTC SDK for desktop browsers.

## FAQs
**1. Only public and private keys can be obtained when I try to view the key. How do I get a key?**

TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key.

**2. What should I do if the client error "RtcError:no valid ice candidate found" occurs?**

This error indicates that TRTC SDK for desktop browsers failed with regard to Session Traversal Utilities for NAT (STUN). Please check your firewall policy against the environment requirements.

**3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?**

It indicates that TRTC SDK for desktop browsers failed to establish a media transmission channel. Please check your firewall configuration against the environment requirements.

** 4. What should I do if a 10006 error occurs?**

If the `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"` error occurs, log in to the [TRTC console](https://console.cloud.tencent.com/rav), find the application you created, click **Application Info**, and check in the **Application Info** tab if your TRTC service is available.
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)

## References

- [TWebLive API Guide](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [Online demos](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)

