This document describes how to quickly run the TRTC SDK demo for desktop browsers.

## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms such as browsers on Android.

- If your application scenario is mainly in the education sector, the [Electron](https://intl.cloud.tencent.com/document/product/647/35097) solution is recommended for the teacher end, which is more stable and supports two-channel big/small video images, more flexible screen sharing schemes, and better recovery capabilities on poor network connections.



<table>
<thead>
<tr>
<th width="15%">OS</th>
<th width="24%">Browser</th>
<th>Minimum Browser<br>Version Requirement</th>
<th>Receiving (Playback）</th>
<th>Sending (Mic-on)</th>
<th>Screen Sharing</th>
</tr>
</thead>
<tbody><tr>
<td>macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Safari 13+)</td>
</tr><tr>
<td>macOS</td>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
</tr><tr>
<td>macOS</td>
<td>Desktop Firefox</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+)</td>
</tr><tr>
<td>macOS</td>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr><tr>
<td>Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
</tr><tr>
<td>Windows</td>
<td>QQ browser (desktop, WebKit core)</td>
<td>10.4+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr><tr>
<td>Windows</td>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
</tr><tr>
<td>Windows</td>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr><tr>
<td>iOS 11.1.2+</td>
<td>Safari (mobile)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr><tr>
<td>iOS 12.1.4+</td>
<td>WeChat embedded browser</td>
<td>-</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr><tr>
<td>Android</td>
<td>QQ browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr><tr>
<td>Android</td>
<td>UC browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr><tr>
<td>Android</td>
<td>WeChat embedded browser (TBS core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr><tr>
<td>Android</td>
<td>WeChat embedded browser (XWEB core)</td>
<td>-</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
</tbody></table>

>! 
>- You can open [WebRTC Support Level Test](https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/web/demo/env-detect/index.html) in a browser, for example, through WeChat Official Account, to test whether the environment fully supports WebRTC.
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

### Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Web)** to visit GitHub (or click **[ZIP](https://liteavsdk-1252463788.cos.ap-guangzhou.myqcloud.com/H5_latest.zip?_ga=1.195966252.185644906.1567570704)**), and download the SDK and demo source code.
 ![](https://main.qcloudimg.com/raw/70f4f26e438e63b62b1dd55306d1c296.png)
2. After the download, return to the TRTC console and click **Downloaded and Next** to view your `SDKAppID` and secret key.

<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `Web/TRTCSimpleDemo/js/debug/GenerateTestUserSig.js` file.
3. Set parameters in the `GenerateTestUserSig.js` file:
  <ul><li>SDKAPPID: 0 by default. Set it to the actual SDKAppID.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual secret key.</li></ul> 
4. Return to the TRTC console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console to Manage Applications**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
> The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo
Open `index.html` in the root directory of the demo with Chrome to run the demo.

>!
> - Generally, the demo needs to be deployed on your server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers better support for the features of TRTC SDK for desktop browsers; therefore, Chrome is recommended for the demo.



- Click **Enter Room** to enter an audio/video call room and publish local audio/video stream.
 You can open multiple pages and click **Enter Room* on each of them. You should be able to see multiple video images, which simulate a real-time video/audio call.
- Click the camera icon to select a camera.
- Click the mic icon to select a mic.

>?WebRTC uses camera and mic to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.


## FAQs

### 1. Only public and private key information can be obtained when I try to view the secret key. How do I get the secret key?
TRTC SDK v6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to obtain a new secret key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find the target application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
  - Switch to the old algorithm ECDSA-SHA256:
   ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256.
   ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This error indicates that TRTC SDK for desktop browsers failed with regard to Session Traversal Utilities for NAT (STUN). Please check your firewall configuration against the [Environment Requirements](#requirements).

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
This error indicates that TRTC SDK for desktop browsers failed to establish a media transport connection. Please check your firewall configuration against the [Environment Requirements](#requirements).

### 4. What should I do if a 10006 error occurs?
If the "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether your TRTC application service is available.
Log in to the [TRTC console](https://console.cloud.tencent.com/rav), select the application you created, and click **Account Info** to view its service status.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)
