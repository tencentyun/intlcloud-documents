This document describes how to quickly run the TRTC SDK for Web Demo.

## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms (such as browsers on Android).
- For mobile devices, the Mini Program solution is recommended, which is supported by both WeChat and Mobile QQ. This solution is implemented through native technologies of corresponding platforms to deliver excellent audio/video performance and specifically adapted to major mobile phone brands.
- If your application scenario is mainly in the education sector, the [Electron](https://intl.cloud.tencent.com/document/product/647/35097) solution is recommended for the teacher end, which is more stable and supports two-channel big/small video images, more flexible screen sharing schemes, and more powerful recovery capabilities on poor network connections.

| OS | Browser | Minimum Version Requirement | Receipt (Playback) | Sending (Mic-on) |
|:-------:|:-------:|:-------:|:-------:|:-------:|
| macOS | Safari (desktop) | 11+ | Supported | Supported |
| macOS | Chrome (desktop) | 47+ | Supported | Supported |
| Windows | Chrome (desktop) | 52+ | Supported | Supported |
| Windows | QQ Browser (desktop) | 10.2 | Supported | Supported |
| iOS | Safari (mobile) | 11.1.2 | Supported | Supported |
| iOS | WeChat embedded browser | 12.1.4 | Supported | Not supported |
| Android | QQ Browser (mobile) | - | Not supported | Not supported |
| Android | UC Browser (mobile) | - | Not supported | Not supported |
| Android | WeChat embedded browser | - | Not supported | Not supported |

>
>- You can open the [WebRTC capability test](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) page in your browser to check whether WebRTC is fully supported, such as the browser environments like WeChat Official Account.
>- Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support the TRTC SDK for Web.

<span id="requirements"></span>
## Environment Requirements
- Please use the latest version of Chrome.
- The TRTC SDK for Web uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuring these ports, please use the [official demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) to check whether the ports work.
 - TCP port: 8687
 - UDP ports: 8000, 8800, 843, 443
 - Domain name: qcloud.rtc.qq.com

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name such as `TestTRTC`, and click **Create Application**.

<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding card, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Web)** to redirect to GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/H5_latest.zip?_ga=1.195966252.185644906.1567570704)**) and download the relevant SDK and supporting demo source code.
 
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `Web/js/debug/GenerateTestUserSig.js` file.
3. Set the relevant parameters in the `GenerateTestUserSig.js` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul>

4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-Side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo
Open the `index.html` in the root directory of the demo with Chrome to run the demo.

>
> - Generally, the demo needs to be deployed on your server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers more comprehensive support for the features of the TRTC SDK for Web; therefore, Chrome is recommended for the demo.


- Click**Enter Room** to enter an audio/video call room and publish local audio/video stream.
 You can open multiple pages and click **Enter Room* on each of them. Normally, multiple video images can be seen with audio/video call simulated.
- Click the camera icon to select a camera.
- Click the mic icon to select a mic.

>WebRTC needs to use camera and mic to capture audio and video. During the trial, you may receive relevant prompts from Chrome and you should click **Allow**.

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166).

Upgrade operation:
1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
3. Select the **Quick Start** tab and click **Upgrade** in **Step 2: obtain the secret key to issue UserSig**.

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This error indicates that the TRTC SDK for Web failed with regard to Session Traversal Utilities for NAT (STUN). Please check the firewall configuration according to the [Environment Requirements](#requirements).

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
This error indicates that the TRTC SDK for Web failed to establish a media transport tunnel. Please check the firewall configuration according to the [Environment Requirements](#requirements).

### 4. What should I do if a 10006 error occurs?
If "Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it" is displayed, please check whether your TRTC application service is available.
Log in to the [TRTC Console](https://console.cloud.tencent.com/rav), click the application you created, click **Account Info**, and you can view the service status in the account info tab.
