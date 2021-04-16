## 1. Introduction to TWebLive

[TWebLive](https://trtc.qcloud.com/tweblive/index.html#/) is a Tencent Cloud web ILVB component. As a new [SDK](https://www.npmjs.com/package/tweblive) developed by the Tencent Cloud terminal development team, it integrates [Tencent Cloud TRTC](https://intl.cloud.tencent.com/product/trtc), [Tencent Cloud IM](https://intl.cloud.tencent.com/product/im), and the Tencent Cloud superplayer TCPlayer. It provides common features in web interactive livestreaming scenarios, including push, enabling/disabling the microphone, enabling/disabling the camera, WeChat video sharing, chat, and likes. It also contains simple and easy-to-use [APIs](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html) for implementing web push/pull, real-time chat interaction, and other features.





## 2. TWebLive Advantages

Developers can use this SDK to completely replace the flash push solution, which greatly reduces the complexity and time for implementing web push, low-latency web streaming, CDN streaming, and real-time chat interactions (or on-screen comments). For more information, see the following examples.

### 1. Push

To use the push feature, you must create a pusher object. The simplest push operation takes only three steps, as shown below.

```javascript
<div id="pusherView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a pusher object.
let pusher = TWebLive.createPusher({ userID: 'your userID' });

// 2. Configure the rendering view, use the microphone to capture audio, and use the camera to capture video (720p by default).
pusher.setRenderView({
  elementID: 'pusherView',
  audio: true,
  video: true
}).then(() => {.then(() => {
  // 3. Enter the sdkappid, roomid, and other information for push.
  // The URL must start with `room://`
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
```

### 2. Pull

To use the pull feature, you must create a player object. The simplest pull operation takes only three steps, as shown below.

```javascript
<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a player object.
let player = TWebLive.createPlayer();

// 2. Configure the rendering view.
player.setRenderView({ elementID: 'playerView' });

// 3. Enter the FLV and HLS addresses and other required information for pulling CDN streams for playback. The URL must start with `https://`.
// Alternatively, enter the sdkappid, roomid, and other information for pulling WebRTC low-latency streams for playback. The URL must start with `room://`.
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // Replace the URL with an actual playback address
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // Replace the URL with an actual playback address

// let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPlay | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
```

### 3. Livestreaming interaction

To enable the host to chat with the audience, you must create an IM object. The simplest message receiving and sending process takes only three steps, as shown below.

```javascript
// 1. Create an IM object and monitor events.
let im = TWebLive.createIM({
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM instance
});
// Monitor IM_READY IM_TEXT_MESSAGE_RECEIVED and other events
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// Monitor this event on the access side, and then you can call the SDK to send messages or perform other operations
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// Receive a text message and display it on the screen
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2. Log in to the IM console.
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // Logged in successfully
  if (imResponse.data.repeatLogin === true) {
    // This indicates that the account has been logged in and that the current login is a repeated login
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // Information about the login failure
});

// 3. Enter the chat room.
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // Entered the chat room successfully
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: // You are already in the chat room
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // Information about the failure to enter the chat room
});
</script>
```

To further reduce developers' development and labor costs, in addition to the TWebLive SDK, we provide an open-source [demo](https://github.com/tencentyun/TWebLive) on GitHub, which is adaptable to both PC and mobile browsers. Developers can fork and clone a project to their local devices and make simple modifications to run the demo. Alternatively, they can integrate the demo into their own projects for deployment and launch.

## 3. Using TWebLive


Create a TRTC instance in the [Tencent Cloud TRTC console](https://console.cloud.tencent.com/trtc/app) and save the SDKAPPID. At the same time, an IM instance with the same SDKAppID will be automatically created. Then, choose **App Management** > **Feature Configuration** and enable automatic relayed push. After relayed push is enabled, each video stream in the TRTC room is assigned a playback URL. (If CDN livestreaming is not required, you do not need to enable relayed push.)

Configure the playback domain name and CNAME in the [Tencent Cloud LVB console](https://console.cloud.tencent.com/live/). For detailed instructions, see [CDN Relayed Live Streaming](https://intl.cloud.tencent.com/document/product/647/35242). (If CDN livestreaming is not required, skip this step.)

Download TWebLive through NPM as follows.
```javascript
npm i tweblive --save
```

## 4. Architecture and Platform Support
The following figure shows the TWebLive architecture design.
![](https://main.qcloudimg.com/raw/ab2b13a441da8b0631cc664f95ad18db.png)

Web push and low-latency web streaming adopt the WebRTC technology, which works well with Chrome (desktop version) and Safari (desktop and mobile versions) but poorly or not at all with other platforms (such as browsers on Android terminals).

| Operating System | Browser | Minimum Browser Version Requirement | Receiving (Playback) | Sending (Mic-on) | Screen Sharing |
|:-------:|:-------:|:-------:|:-------:|:-------:| :-------:|
| MacOS | Safari (desktop) | V11 and later | Supported | Supported | Not supported |
| MacOS | Chrome (desktop) | V56 and later | Supported | Supported | Supported (for Chrome V72 and later) |
| Windows | Chrome (desktop) | V56 and later | Supported | Supported | Supported (for Chrome V72 and later) |
| Windows | QQ Browser (desktop) | V10.4 | Supported | Supported | Not supported |
| iOS | Safari (mobile) | V11.1.2 | Supported | Supported | Not supported |
| iOS | WeChat embedded browser | V12.1.4 | Supported | Not supported | Not supported |
| Android | QQ Browser (mobile) | - | Not supported | Not supported | Not supported |
| Android | UC Browser (mobile) | - | Not supported | Not supported | Not supported |
| Android | WeChat embedded browser (with the TBS kernel) | - | Supported | Supported | Not supported |

We recommend that you use the [Mini Program] solution on mobile devices, which is supported by both WeChat and Mobile QQ. This solution is built around native technologies of corresponding platforms and delivers excellent audio/video performance. It is specifically adapted to major mobile phone brands. If your application scenario mainly involves the education sector, we recommend that you use the [Electron](https://intl.cloud.tencent.com/document/product/647/35097) solution for the teacher end. This solution is more stable and supports dual-channel pictures, more flexible screen sharing schemes, and more powerful recovery capabilities in poor network conditions.

## 5. Notes

- TRTC and IM instances can share each other's accounts and authentication data only if they have the same SDKAppID.
- The IM instance provides the basic-edition content filtering capability for text messages. To use the sensitive word customization feature, click **Upgrade**.
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization. To correctly distribute UserSigs, integrate the computing code of UserSigs into your server and provide an app-oriented API. When a UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
- Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support the TRTC SDK for desktop browsers.

## 6. Summary

This document describes the new Tencent Cloud web ILVB component TWebLive. With this SDK, developers can quickly implement web push, low-latency web streaming, CDN streaming, real-time chat interactions (or on-screen comments), and other features. In addition, this component can completely replace the traditional flash push solution.

This document also provides a detailed access solution and [online demo](https://trtc.qcloud.com/tweblive/index.html#/). Currently, TWebLive works well with mainstream desktop browsers and provides Mini Program solutions on mobile devices.

In the future, we will provide more livestreaming services, such as screen sharing on the push end, image message interaction, multi-line display for viewers (over the WebRTC low-latency and CDN lines), and host-viewer co-anchoring.

References

- [TWebLive](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [Quick Demo of the Web ILVB Component](https://intl.cloud.tencent.com/document/product/1047/38174)
