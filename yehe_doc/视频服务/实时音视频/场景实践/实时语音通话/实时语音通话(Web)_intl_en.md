This document describes how to implement a browser-based audio call solution.
- Part 1 describes how to activate the service and run the demo.
- Part 2 describes how to build your own audio call feature using the `TRTCCalling` component.

## Environment Requirements
Currently, the desktop version of Chrome offers better support for the features of the TRTC SDK for web; therefore, Chrome is recommended for the demo.

TRTCCalling uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuration, please use [Official Demo](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html) to check whether the ports work.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, 16285
  - Domain name: qcloud.rtc.qq.com

The service supports the following platforms:

| OS |          Browser (Desktop)         | Minimum Browser Version Requirement |
| :------: | :--------------------------: | :----------------: |
|  macOS  |     Safari     |        11+         |
|  macOS  |     Chrome     |        56+         |
|  macOS  |    Firefox     |        56+         |
|  macOS  |      Edge      |        80+         |
| Windows  |     Chrome     |        56+         |
| Windows | QQ Browser (WebKit core) |      10.4+       |
| Windows  |    Firefox     |        56+         |
| Windows  |      Edge      |        80+         |

## Running the Demo

[](id:step1)
### Step 1. Create an application
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and verify your identity.
2. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
3. Enter an application name such as `TestTRTC` and click **Create**.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open the `Web/js/debug/GenerateTestUserSig.js` file.
3. Set parameters in the `GenerateTestUserSig.js` file:
  <ul><li>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step4)
### Step 4. Run the demo
1. In the demo directory, run the following commands in turn:
```
npm install
npm run serve
```
2. Open Chrome and visit `http://localhost:8080/`. If the above steps are performed correctly.
3. Enter your user ID and click **Log In**. Then, click **Audio Call**.
4. Enter the user ID of the callee and click **Call**.
5. Start the audio call.


## Building Your Own Audio Call
### Step 1. Import the `TRTCCalling` component
>?
>- Since version 0.6.0, you need to manually install dependencies [trtc-js-sdk](https://www.npmjs.com/package/trtc-js-sdk), [tim-js-sdk](https://www.npmjs.com/package/tim-js-sdk), and [tsignaling](https://www.npmjs.com/package/tsignaling).
>- To reduce the size of `trtc-calling-js.js` and prevent version conflict between `trtc-calling-js.js` and the already in use `trtc-js-sdk`, `tim-js-sdk` or `tsignaling`(which may cause the latter three to be packaged as external dependencies), you need to manually install the dependencies before use.

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

### Step 2. Create a `TRTCCalling` object
Create a `TRTCCalling` object and set the `SDKAppID` parameter to your `SDKAppID`.
```javascript
import TRTCCalling from 'trtc-calling-js';


let options = {
  SDKAppID: 0, // Replace 0 with your `SDKAppID` when connecting
  // The `tim` parameter is added starting from v0.10.2
  // The `tim` parameter is applicable to existing TIM instances in the business to ensure the uniqueness of TIM instances
  tim: tim
};
const trtcCalling = new TRTCCalling(options);
```

### Step 3. Log in
```javascript
trtcCalling.login({
  userID,
  userSig,
});
```

### Step 4. Make a one-to-one call
- **Caller: making a call**
```javascript
trtcCalling.call({
  userID,  // User ID
  type: 2, // Call type. `0`: unknown; `1`: audio call; `2`: video call
  timeout  // Timeout threshold, in seconds
});
```
- **Callee: answering a call**
```javascript
// Answer
trtcCalling.accept({
  inviteID, // Invitation ID, which identifies an invitation
  roomID,   // Room ID
  callType  // `0`: unknown; `1`: audio call; `2`: video call
});
// Decline
trtcCalling.reject({ 
  inviteID, // Invitation ID, which identifies an invitation
  isBusy // Whether the line is busy. `0`: unknown; `1`: audio call; `2`: video call
})
```
- **Ending a call**
```javascript
trtcCalling.hangup()
```
