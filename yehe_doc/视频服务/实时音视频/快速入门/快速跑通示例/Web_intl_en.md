This document describes how to quickly run the demo for the TRTC web SDK.
## Preparations
Before you run the demo for the TRTC web SDK, pay attention to the following:

### Supported platforms
The TRTC web SDK is based on WebRTC. For details about the browsers supported, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664).
If your browser (for example, WebView) is not in the list, you can run a [TRTC Web SDK Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in the browser to test whether it fully supports WebRTC.

If your application scenario is mainly in the education sector, consider using the [TRTC Electron SDK](https://intl.cloud.tencent.com/document/product/647/35097), which supports the dual-stream mode (big and small images), with more flexible screen sharing schemes and better recovery capabilities for poor network connections. 

### URL protocol support
Because of the security policies of browsers, when you use WebRTC, there are requirements on the protocol used for access. For details, see the table below.

| Scenario     | Protocol             | Receive (Playback) | Send (Publish) | Share Screen | Remarks |
|----------|:-----------------|:---------|----------|--------|----------|
| Production     | HTTPS        | Supported         | Supported         | Supported     | **Recommended** |
| Production     | HTTP         | Supported         | Not supported       | Not supported   |      |
| Local development | http://localhost | Supported         | Supported         | Supported     | **Recommended** |
| Local development | http://127.0.0.1 | Supported         | Supported         | Supported     |      |
| Local development | http://[local IP address]  | Supported         | Not supported       | Not supported   |      |
| Local development | file:///         | Supported         | Supported         | Supported     |      |

### Firewall configuration
The TRTC web SDK uses the following ports and domain names for data transfer, which should be added to the allowlist of your firewall. You can use our [demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html) to check whether the configuration has taken effect. For details, see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
- TCP port: 8687
- UDP ports: 8000, 8080, 8800, 843, 443, 16285
- Domain names: `*.rtc.qq.com`, `yun.tim.qq.com`


## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account.

## Directions

[](id:step1)

### Step 1. Create an application
1. In the TRTC console, click **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Select **New** and enter an application name such as `TestTRTC`. If you have already created an application, select **Existing**.
3. Add or edit tags according to your actual business needs and click **Create**.

![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)

>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to mark and sort your Tencent Cloud resources. For example, your company may have multiple business units, each using one or more TRTC applications. You can tag the applications with the information of the corresponding business units. Tags are optional. You can add and edit tags for your applications as needed.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the web SDK and demo source code.
2. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:step3)
### Step 3. Get the SDKAppID and secret key
1. In the **Modify Configuration** step, note the `SDKAppID` and secret key.
2. Paste the `SDKAppID` and secret key and click **Next**.

![](https://qcloudimg.tencent-cloud.cn/raw/e210b7b71cf273de59d6e2df917101e4.png)

[](id:step4)
### Step 4. Run the demo 

We offer the following demos for the TRTC web SDK to meet different customer needs:
- **`base-js`**: The TRTC web standard demo, which integrates capabilities including audio/video calls and device selection. It was developed using jQuery and can be run in a browser. You can try it out [here](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html).
- **`quick-demo-js`**: The TRTC web quick demo (JavaScript), which integrates capabilities including audio/video call and device selection. It was developed based on JavaScript without using any libraries and can be run in a browser. You can try it out [here](https://web.sdk.qcloud.com//trtc/webrtc/demo/quick-demo-js/index.html).
- **`quick-demo-vue2-js`**: The TRTC web quick demo (Vue.js 2.0), which integrates capabilities including audio/video call and device selection. It was developed using Vue.js 2.0. To use it, you need to install Node.js. You can try it out [here](https://web.sdk.qcloud.com/trtc/webrtc/demo/quick-demo-vue2-js/index.html).

<dx-tabs>
::: Demo 1: base-js       
1. Find and open `TRTC_Web/base-js/js/debug/GenerateTestUserSig.js`.
2. Set parameters in the `GenerateTestUserSig.js` file as follows:
  - SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
  - `SECRETKEY`: Left empty by default. Set it to the actual key. 
3. Run the demo:
Open `index.html` in the root directory of the demo with Chrome to run the demo.
<dx-alert infotype="notice">
<li>Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.</li>
<li>Currently, the desktop version of Chrome offers better support for the features of the TRTC web SDK; therefore, Chrome is recommended.</li></dx-alert>


- Click **Join** to join a room and publish the local stream.
  You can open multiple pages and click **Join Room** on each of them. You should be able to see multiple videos, which simulate a real-time audio/video call.
- Click **Camera Select** to select a camera.
- Click **Microphone Select** to select a mic.

<dx-alert infotype="explain">WebRTC uses the camera and mic of your device to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.</dx-alert>

 

:::
::: Demo 2: quick-demo-js    
1. Find `TRTC_Web/quick-demo-js/index.html` and open it with a browser.
<dx-alert infotype="explain">
<li>For details about the browsers supported by the TRTC web SDK, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664).</li>
<li>For information about the ports and domain names used by the TRTC web SDK, see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164#webrtc-.E9.9C.80.E8.A6.81.E9.85.8D.E7.BD.AE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.E6.88.96.E5.9F.9F.E5.90.8D.E4.B8.BA.E7.99.BD.E5.90.8D.E5.8D.95.EF.BC.9F).</li></dx-alert>
2. Enter the `SDKAppID` and secret key obtained in <a href="#step3">Step 3</a>.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f22cfb136e41ebb28100ea5fc1d6fa6f.png" width="800px">
3. You can try the following:
 - Click **Join** to join a room.
 - Click **Publish** to publish the local stream.
 - Click **Unpublish** to stop publishing the local stream.
 - Click **Leave** to leave the room.
 - Click **Share Screen** to publish the screen sharing stream.
 - Click **Stop Share Screen** to stop publishing the screen sharing stream.
4. After joining a room, you can use a share link to invite others to try the audio/video call feature with you.
:::
::: Demo 3: quick-demo-vue2-js      
1. Go to the `TRTC_Web/quick-demo-vue2-js/` directory.
2. Run the demo:
```shell
npm start
```
The `[http://localhost:8080/](http://localhost:8080/)` address will be opened in your default browser automatically.
<dx-alert infotype="notice">
<li>The default port number is 8080. Please use the number of the actual port used to run the demo locally.</li>
<li>For details about the browsers supported by the TRTC web SDK, see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664).</li>
<li>For information about the URL protocols supported, see [URL Protocol Support](https://intl.cloud.tencent.com/document/product/647/41664).</li>
<li>For information about the ports and domain names used by the TRTC web SDK, see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164#webrtc-.E9.9C.80.E8.A6.81.E9.85.8D.E7.BD.AE.E5.93.AA.E4.BA.9B.E7.AB.AF.E5.8F.A3.E6.88.96.E5.9F.9F.E5.90.8D.E4.B8.BA.E7.99.BD.E5.90.8D.E5.8D.95.EF.BC.9F).</li></dx-alert>
3. Enter the `SDKAppID` and secret key obtained in <a href="#step3">Step 3</a>.
<img src="https://qcloudimg.tencent-cloud.cn/raw/621de0ce3313a39bca88905185d40658.png" width="800px">
4. You can try the following:
 - Click **Join** to join a room.
 - Click **Publish** to publish the local stream.
 - Click **Unpublish** to stop publishing the local stream.
 - Click **Leave** to leave the room.
 - Click **Share Screen** to publish the screen sharing stream.
 - Click **Stop Share Screen** to stop publishing the screen sharing stream.
5. After joining a room, you can use a share link to invite others to try the audio/video call feature with you.
:::
</dx-tabs>

>!
>- The method used to generate `UserSig` in this document is to configure the secret key in the client code. This makes the key vulnerable to decompilation and reverse engineering. Once your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and debugging**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).


## FAQs
### 1. There is only information of the public and private keys when I try to view the secret key. How do I get the secret key?
Since the release of v6.6 for app and v4.0 for web in August 2019, the new signature algorithm HMAC-SHA256 has been used. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **asymmetric encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This error indicates that the TRTC web SDK failed with regard to hole punching via Session Traversal Utilities for NAT (STUN). Please check your firewall configuration against the [Environment Requirements](#requirements).

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates that the TRTC web SDK failed to establish a media transmission channel. Please check your firewall configuration against the [Environment Requirements](#requirements).

### 4. What should I do if a 10006 error occurs?
If the error "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether the TRTC service status for your application is “normal”.
Log in to the [TRTC console](https://console.cloud.tencent.com/rav), select the application you created, and click **Application Info** to view its service status.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? For other questions, see [Web](https://intl.cloud.tencent.com/document/product/647/37340).
