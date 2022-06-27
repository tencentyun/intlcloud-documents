## Overview
`TUICalling` is an open-source UI component for audio/video communication. You can use it to quickly integrate **video call** capabilities into your desktop website. It’s ideal for applications such as online medical consultation, online customer service, and remote insurance claim settlement.

>? All components of TUIKit use two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047/35448). When you activate TRTC, IM and the trial edition of the IM SDK (which supports only 100 DAUs) will be activated automatically. For the billing details of IM, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<table class="tablestyle">
<tbody><tr>
<td style="vertical-align: top;"><img src="https://qcloudimg.tencent-cloud.cn/raw/a2b6bdc19d17d4e105b1d04a53d67957.png"></td>
</tr>
</tbody></table>


#### Other platforms
In addition to web, we also provide source code for Android, iOS, and Flutter. The Android and iOS versions support incoming call notifications.

>?
>- **In addition to web, we also provide source code for Android, iOS, and Flutter. The Android and iOS versions support incoming call notifications.** 
>- If you have any questions or suggestions, feel free to [contact us](https://intl.cloud.tencent.com/contact-us).

## Integration
[](id:step1)
### Step 1. Get the `SDKAppID` and signature key
- Sign up for a Tencent Cloud account and go to the [Application Management](https://console.cloud.tencent.com/trtc/app) page of the TRTC console.
- If you don’t have an application yet, click **Create Application** to create an application. Then, click **Application Info** and select the **Quick Start** tab to view the `SDKAppID` and `SecretKey`.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png" width="700">
- **SDKAppID**: TRTC application ID, which uniquely identifies an application
- **Secretkey**: TRTC application key, which you can use together with `SDKAppID` to generate a `UserSig` required to authorize the use of TRTC. You will use this key in step 5.

[](id:step2)
### Step 2. Import the `TRTCCalling` component
Go to [GitHub](https://github.com/tencentyun/TUICalling) and clone or download the code. Refer to the `Web` directory.

>?
>- Since version 0.6.0, you need to manually install the dependencies [trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk), [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk), and [tsignaling](https://www.npmjs.com/package/tsignaling).
>- To reduce the size of `trtc-calling-js.js` and prevent version conflict between `trtc-calling-js.js` and the already-in-use `trtc-js-sdk`, `tim-js-sdk` or `tsignaling`, the latter three are packaged as external dependencies, which you need to install manually before use.

<dx-codeblock>
::: javascript javascript
// Import via npm
  npm install trtc-js-sdk --save

  npm install tim-js-sdk --save

  npm install tsignaling --save

  npm install trtc-calling-js --save
:::
</dx-codeblock>

<dx-codeblock>
::: html html
// If you import `trtc-calling-js` via a script, you need to manually import the following resources in the specified order.

<script src="./trtc.js"></script>
<script src="./tim-js.js"></script>
<script src="./tsignaling.js"></script>
<script src="./trtc-calling-js.js"></script>
:::
</dx-codeblock>

[](id:step3)
### Step 3. Create a `TRTCCalling` object
Create a `TRTCCalling` object, setting `SDKAppID` to the `SDKAppID` of your application.
```javascript
// You can refer to `Web/src/trtc-calling/index.js`
import TRTCCalling from 'trtc-calling-js';

let options = {
	SDKAppID: 0, // Replace 0 with your `SDKAppID` when connecting
	// The `tim` parameter is added starting from v0.10.2
	// The parameter guarantees the uniqueness of an existing TIM instance.
	tim: tim
};
const trtcCalling = new TRTCCalling(options);
```

[](id:step4)
### Step 4. Log in to the component and listen for events
```javascript
// You can refer to `Web/src/components/login/index.vue`
trtcCalling.login({
	userID,
	userSig,
});

// You can refer to `Web/src/App.vue`

export default {
	name: "App",
	components: {
	},
	async created() {
		this.initListener();
	},
	data() {
		return {};
	},
	destroyed() {
		this.removeListener();
	},
	methods: {
		initListener: function() {
			// A remote user called.
			trtcCalling.on(trtcCalling.EVENT.INVITED, this.handleNewInvitationReceived);
			// A remote user answered the call.
			trtcCalling.on(trtcCalling.EVENT.USER_ACCEPT, this.handleUserAccept);
			// A remote user rejected the call.
			trtcCalling.on(trtcCalling.EVENT.REJECT, this.handleInviteeReject);
			// ...
		},
		removeListener: function() {
			trtcCalling.off(trtcCalling.EVENT.INVITED, this.handleNewInvitationReceived);
			trtcCalling.off(trtcCalling.EVENT.USER_ACCEPT, this.handleUserAccept);
			trtcCalling.off(trtcCalling.EVENT.REJECT, this.handleInviteeReject);
		},
		handleNewInvitationReceived: async function(payload) {
		},
		handleUserAccept: function() {
		},
		handleInviteeReject: function() {
		}
	}
}
```

[](id:step5)
### Step 5. Make a one-to-one call
- **Caller: Calls a user**
```javascript
// You can refer to `Web/src/components/video-call/index.vue` or `Web/src/components/audio-call/index.vue`
trtcCalling.call({
  userID,  // User ID
  type: 2, // Call type. `0`: unknown; `1`: audio call; `2`: video call
  timeout  // Timeout period, in seconds
});
```
- **Callee: Answers the call**
```javascript
// You can refer to the `Web/src/App.vue handleAcceptCall` method
// Answer
trtcCalling.accept();
// Reject
trtcCalling.reject()
```
- **Turn the local camera on**
```javascript
trtcCalling.openCamera()
```
- **Play the video of the remote user**
```javascript
trtcCalling.startRemoteView({
  userID, // Remote user ID
  videoViewDomID // The user’s data will be rendered in this DOM node.
})
```
- **Show local video preview**
```javascript
trtcCalling.startLocalView({
  userID, // Local user ID
  videoViewDomID // The user’s data will be rendered in this DOM node.
})
```
- **Hang up**
```javascript
trtcCalling.hangup()
```

## FAQs

### Why can’t I get through to a user? Why am I kicked offline?
The component does not support login of multiple instances or **offline signaling**. Please make sure that your current login is unique.
>?
>- **Multiple instances**: A user ID logs in multiple times or on different devices, which disrupts signaling.
>- **Offline signaling**: Only online instances can receive a message. Messages sent to offline instances will not be sent again when the instances go online.

### What are the environment requirements?
The desktop version of Chrome offers better support for the features of the TRTC web SDK; therefore, Chrome is recommended for the demo.

`TRTCCalling` uses the following ports and domain name for data transfer, which should be added to the allowlist of the firewall. After configuration, please use the [official demo](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html) to check whether the configuration has taken effect.
- **TCP port**: 8687
- **UDP ports**: 8000, 8080, 8800, 843, 443, 16285
- **Domain name**: qcloud.rtc.qq.com. For details, see [Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
- **Supported platforms**: Currently, this solution supports the following platforms:
<table>
<thead><tr><th>OS</th><th> Browser</th><th>Minimum Browser Version Requirement</th></tr></thead>
<tbody><tr>
<td>macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
</tr><tr>
<td>macOS</td>
<td>Chrome (desktop)</td>
<td>56+</td>
</tr><tr>
<td>macOS</td>
<td>Firefox (desktop)</td>
<td>56+</td>
</tr><tr>
<td>macOS</td>
<td>Edge (desktop)</td>
<td>80+</td>
</tr><tr>
<td>Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>QQ Browser (desktop, WebKit core)</td>
<td>10.4+</td>
</tr><tr>
<td>Windows</td>
<td>Firefox (desktop)</td>
<td>56+</td>
</tr><tr>
<td>Windows</td>
<td>Edge (desktop)</td>
<td>80+</td>
</tr>
</tbody></table>

>? For more information on browser compatibility, see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html). You can also run an online test using the [TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html).

- **URL protocol support**:
<table>
<thead><tr><th>Scenario</th><th>Protocol</th><th>Receive (Playback)</th><th>Send (Publish)</th><th>Share Screen</th><th>Remarks</th></tr></thead>
<tbody><tr>
<td>Production</td>
<td>HTTPS</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Recommended</td>
</tr><tr>
<td>Production</td>
<td>HTTP</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>Local development</td>
<td>http://localhost</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Recommended</td>
</tr><tr>
<td>Local development</td>
<td>http://127.0.0.1</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr><tr>
<td>Local development</td>
<td>http://[local IP]</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>Local development</td>
<td align="left">file:///</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
</tbody></table>

### More
For other FAQs, see [TRTCCalling for Web](https://intl.cloud.tencent.com/document/product/647/43096).
