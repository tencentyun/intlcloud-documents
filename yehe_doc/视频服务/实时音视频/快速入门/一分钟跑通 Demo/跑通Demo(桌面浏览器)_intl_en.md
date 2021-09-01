This document describes how to quickly run the demo for TRTC SDK for desktop browsers.

## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.
- If your application scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports two-channel big/small video images, with more flexible screen sharing schemes and better recovery capabilities on poor network connections.



<table>
<tr>
<th>OS</th>
<th width="22%">Browser</th><th>Minimum Browser<br>Version Requirement</th><th width="16%">Receive (Playback)</th><th width="16%">Send (Broadcast)</th><th>Screen Sharing</th><th>SDK Version Requirement</th>
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
<td>WeChat embedded browser</td>
<td>-</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat embedded browser</td>
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
<td>WeChat embedded browser (TBS core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat embedded browser (XWEB core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
</table>

>! 
>- You can open [WebRTC Support Level Test](https:/web.sdk.qcloud.com/web/demo/env-detect/index.html) in a browser, for example, from WeChat Official Account, to test whether the environment fully supports WebRTC.
>- Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support TRTC SDK for desktop browsers.

<span id="requirements"></span>
## Environment Requirements
- Please use the latest version of Chrome.
- TRTC SDK for desktop browsers uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuration, please use the [official demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) to check whether the ports work.
 - TCP port: 8687
 - UDP ports: 8000, 8080, 8800, 843, 443, 16285
 - Domain name: qcloud.rtc.qq.com
 
## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

[](id:step1)

### Step 1. Create an application.
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc) and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestTRTC`, and click **Create**.

[](id:step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `Web/TRTCSimpleDemo/js/debug/GenerateTestUserSig.js` file.
3. Set parameters in `GenerateTestUserSig.js` as follows:
  <ul><li>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo.
Open `index.html` in the root directory of the demo with Chrome to run the demo.

>!
>- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers better support for the features of TRTC SDK for desktop browsers; therefore, Chrome is recommended for the demo.

On the demo landing page:
- Click **Enter Room** to enter a TRTC room and publish local audio/video streams.
 You can open multiple pages and click **Enter Room* on each of them. You should be able to see multiple video images, which simulate a real-time video/audio call.
- Click the camera icon to select a camera.
- Click the mic icon to select a mic.

>?WebRTC uses the camera and mic of your device to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.


## FAQs
### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** in the left navigation pane, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This error indicates that TRTC SDK for desktop browsers failed with regard to Session Traversal Utilities for NAT (STUN). Please check your firewall configuration against the [Environment Requirements](#requirements).

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates that TRTC SDK for desktop browsers failed to establish a media transmission channel. Please check your firewall configuration against the [Environment Requirements](#requirements).

### 4. What should I do if a 10006 error occurs?
If the "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether your TRTC application service is available.
Log in to the [TRTC console](https://console.cloud.tencent.com/rav), select the application you created, and click **Application Info** to view its service status.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)
