## Introduction
[TWebLive](https://www.npmjs.com/package/tweblive) is a Tencent Cloud Web ILVB component. It’s a new SDK developed by Tencent Cloud’s terminal development team that integrates [Tencent Real-Time Communication (TRTC)](https://intl.cloud.tencent.com/product/trtc), [Tencent Cloud Instant Messaging (IM)](https://intl.cloud.tencent.com/product/im), and the Tencent Cloud superplayer TCPlayer. It provides common features for web interactive livestreaming scenarios, including push, enabling/disabling the microphone, enabling/disabling the camera, WeChat video sharing, chat, and likes. It is also encapsulated with simple and easy-to-use APIs that can be accessed to implement web push, pull, and real-time chat interaction features.

## 

## Demo Operation

- [Online Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
- [Local Quick Demo](https://github.com/tencentyun/TWebLive)

## Architecture and API Design
Its architecture and API design are as follows:

![](https://main.qcloudimg.com/raw/b4b436ddca16028ef2e5fcdb82f27399.png)
![](https://main.qcloudimg.com/raw/45bc84eac66a599db0eeeb7192e99390.png)
![](https://main.qcloudimg.com/raw/6d49dbc3d1b81773b820ed61c92b7f8c.png)
![](https://main.qcloudimg.com/raw/8401c463ebb4142df8331c04b3d6878d.png)

## Advantages of Web ILVB Component
Developers can use this SDK to **completely replace the flash push solution**, which **greatly reduces the complexity and time costs** for implementing web push, web low-latency streaming, CDN streaming, and real-time chat interactions.

1. To use the push feature, you need to create a pusher object. The simplest push takes only three steps.

```javascript
<div id="pusherView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a pusher object.
let pusher = TWebLive.createPusher({ userID: 'your userID' });

// 2. Set the rendering view, and use the microphone to capture audio and use the camera to capture video (720p by default).
pusher.setRenderView({
  elementID: 'pusherView',
  audio: true,
  video: true
}).then(() => {
  // 3. Input the sdkappid, roomid, and other information for push.
  // The URL must start with `room://`.
  let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}&livedomainname=${liveDomainName}&streamid=${streamID}`;
  pusher.startPush(url).then(() => {
    console.log('pusher | startPush | ok');
  });
}).catch(error => {
  console.error('pusher | setRenderView | failed', error);
});
</script>
```

2. To use the pull playback feature, you need to create a player object. The simplest pull takes only three steps.

```javascript
<div id="playerView" style="width:100%; height:auto;"></div>
<script>
// 1. Create a player object.
let player = TWebLive.createPlayer();

// 2. Set the rendering view.
player.setRenderView({ elementID: 'playerView' });

// 3. Input the flv and hls addresses and other information to pull CDN streams for playback. In this case, the URL must start with `https://`.
// Alternatively, input the sdkappid, roomid, and other information to pull WebRTC low-latency streams for playback. In this case, the URL must start with `room://`.
let url = 'https://'
  + 'flv=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.flv' + '&' // Replace this string with an actual available playback address.
  + 'hls=https://200002949.vod.myqcloud.com/200002949_b6ffc.f0.m3u8' // Replace this string with an actual available playback address.

// let url = `room://sdkappid=${SDKAppID}&roomid=${roomID}&userid=${userID}&usersig=${userSig}`;
player.startPlay(url).then(() => {
  console.log('player | startPla,y | ok');
}).catch((error) => {
  console.error('player | startPlay | failed', error);
});
</script>
```

3. To use the chat interaction feature, you need to create an IM object. The simplest message receiving and sending process takes only three steps.

```javascript
// 1. Create an IM object and listen to events.
let im = TWebLive.createIM({
  SDKAppID: 0 // Replace 0 with the SDKAppID of your IM instance when connecting.
});
// Listen to IM_READY IM_TEXT_MESSAGE_RECEIVED and other events.
let onIMReady = function(event) {
  im.sendTextMessage({ roomID: 'your roomID', text: 'hello from TWebLive' });
};
let onTextMessageReceived = function(event) {
  event.data.forEach(function(message) {
    console.log((message.from || message.nick) + ' : ', message.payload.text);
  });
};
// Listen to this event on the access side, and then you can call the SDK to send messages or perform other operations.
im.on(TWebLive.EVENT.IM_READY, onIMReady);
// Receive a text message and display it on the screen.
im.on(TWebLive.EVENT.IM_TEXT_MESSAGE_RECEIVED, onTextMessageReceived);

// 2. Log in.
im.login({userID: 'your userID', userSig: 'your userSig'}).then((imResponse) => {
  console.log(imResponse.data); // Login successful.
  if (imResponse.data.repeatLogin === true) {
    // This indicates that the account has been logged in and that the current login is a repeated login.
    console.log(imResponse.data.errorInfo);
  }
}).catch((imError) => {
  console.warn('im | login | failed', imError); // Information about the login failure.
});

// 3. Enter the live room.
im.enterRoom('your roomID').then((imResponse) => {
  switch (imResponse.data.status) {
    case TWebLive.TYPES.ENTER_ROOM_SUCCESS: // Entered the live room successfully.
      break;
    case TWebLive.TYPES.ALREADY_IN_ROOM: // You are already in the live room.
      break;
    default:
      break;
  }
}).catch((imError) => {
  console.warn('im | enterRoom | failed', imError); // Information about the failure to enter the live room.
});
</script>
```

To further reduce developers’ development and manpower costs, on the basis of the TWebLive SDK, we provide an open-source [Demo](https://github.com/tencentyun/TWebLive) in GitHub, which is adaptable to both PC and mobile browsers. Developers can fork and clone a project to their local device, make simple modifications, and then run the demo. Alternatively, they can integrate the demo into their own projects for deployment and launch.

## Accessing for Use
Before accessing this component, you need to complete the following preparations:
- Create a TRTC instance on the [Tencent Cloud TRTC console](https://console.cloud.tencent.com/trtc/app) (at the same time, an IM instance with the same `SDKAppID` is automatically created) and save the `SDKAPPID`. Then, choose **App Management** > **Feature Configuration** and enable automatic relayed push. After relayed push is enabled, each video stream in the TRTC room is assigned a playback URL. (If CDN livestreaming is not needed, you do not have to enable relayed push.)
- Configure the playback domain name and CNAME on the [Tencent Cloud LVB console](https://console.cloud.tencent.com/live/). For detailed directions, see [Implementing CDN Livestream](https://intl.cloud.tencent.com/document/product/647/35242). (If CDN livestreaming is not needed, skip this step.)
- Download TWebLive via npm:
```javascript
npm i tweblive --save
```

## Notes

- TRTC and IM instances can share each other’s account and authentication data only if they have the same `SDKAppID`.
- The IM instance provides the basic-version content filtering capability for text messages. If you want to use to the sensitive word customization feature, click **Upgrade**.
- The method of local calculation of UserSig is used for local development debugging only. Do not directly publish it to your online systems. Once your `SECRETKEY` is disclosed, attackers can use your Tencent Cloud traffic without authorization. The correct `UserSig` distribution method is to integrate the computing code of the `UserSig` into your server and provide an app-oriented API. When `UserSig` is required, your app can send a request to the business server to obtain the dynamic `UserSig`. For more information, see [How to Generate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).
- Web push and web low-latency streaming adopt the WebRTC technology, which works well with Chrome (desktop version) and Safari (desktop and mobile versions) but poorly or not at all with other platforms (such as browsers on Android terminals).
- For mobile devices, the [Mini Program](https://intl.cloud.tencent.com/document/product/647/35150) solution is recommended, which is supported by both WeChat and Mobile QQ. This solution is implemented through native technologies of corresponding platforms to deliver excellent audio/video performance and specifically adapted to major mobile phone brands.
- If your application scenario is mainly in the education sector, the [Electron](https://intl.cloud.tencent.com/document/product/647/35097) solution is recommended for the teacher end. This solution is more stable and supports two-channel large/small video images, more flexible screen sharing schemes, and more powerful recovery capabilities on poor network connections.
- Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support the TRTC SDK for Desktop Browser.

| OS | Browser | Minimum Browser Version Requirement | Receipt (Playback) | Sending (Mic-on) | Screen Sharing |
|:-------:|:-------:|:-------:|:-------:|:-------:| :-------:|
| macOS | Safari (desktop) | 11+ | Supported | Supported | Not supported |
| macOS | Chrome (desktop) | 56+ | Supported | Supported | Supported (on Chrome 72+) |
| Windows | Chrome (desktop) | 56+ | Supported | Supported | Supported (on Chrome 72+) |
| Windows | QQ Browser (desktop) | 10.4 | Supported | Supported | Not supported |
| iOS | Safari (mobile) | 11.1.2 | Supported | Supported | Not supported |
| iOS | WeChat embedded browser | 12.1.4 | Supported | Not supported | Not supported |
| Android | QQ Browser (mobile) | - | Not supported | Not supported | Not supported |
| Android | UC Browser (mobile) | - | Not supported | Not supported | Not supported |
| Android | WeChat embedded browser | - | Not supported | Not supported | Not supported |


## Future Features

- Screen sharing supported on the push end
- Image message interaction
- Multi-line display for viewers (WebRTC low-latency line and CDN line)
- Anchor-viewer co-anchoring interaction


## Reference

 [TWebLive API Guide](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
