This document describes how to quickly run the demo of Tencent Cloud TWebLive (interactive web live streaming) component.

## Environment Requirements

- Please use the latest version of Chrome.
- TWebLive uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuring these ports, please use the [official demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html) to check whether the ports work.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, 16285
  - Domain name: qcloud.rtc.qq.com

## Prerequisites

You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

### Step 1. Create an application<span id="step1"></span>

1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
2. Go to **[Application Management](https://console.cloud.tencent.com/trtc/app)**, click **Create Application**, enter the application name such as `testtrtc`, and click **OK**.
<span id="step2"></span>
### Step 2. Get SDKAppID and key

1. In the application list, find the created application, click **Application Info** on the right to enter the details page, and copy and save the `SDKAppID` information.
![](https://main.qcloudimg.com/raw/a65b6631553159ce553620e40f9c2040.png)
2. Click the **Quick Start** tab and click **Copy Secret Key** in **Step 2: obtain the secret key to issue UserSig**.
![](https://main.qcloudimg.com/raw/99f03c367c43416bd7c7e8c6d6ff5002.png)

>! Please keep the key information confidential and avoid disclosure.
>

<span id="step3"></span>
### Step 3. Download and configure the demo source code

1. Download the demo project of the TWebLive component [here](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set relevant parameters:
 - SDKAPPID: please enter the actual `SDKAppID` obtained in [step 2](#step2).
 - SECRETKEY: please enter the actual key information obtained in [step 2](#step2).




>!
>- A locally calculated `UserSig` should be only used for local development and debugging. Please do not publish it directly online. If your `SECRETKEY` is leaked, attackers can steal your Tencent Cloud traffic.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

<span id="step4"></span>
### Step 4. Run the demo

Open the `index.html` file in the `dist` directory of the demo with Chrome to run the demo.

>!
>- Generally, the demo needs to be deployed on your server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
- Currently, the desktop version of Chrome offers more comprehensive support for the features of the TRTC SDK for Desktop Browser; therefore, Chrome is recommended for the demo.

TWebLive needs to use camera and mic to capture audio and video. During the trial, you may receive relevant prompts from Chrome and you should click **Allow**.


## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms (such as browsers on Android).

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

>! Due to H.264 copyright restrictions, Chrome and Chrome WebView-based browsers on Huawei devices do not support the TRTC SDK for Desktop Browser.

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?

Starting from TRTC SDK 6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key.

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?

This error indicates that the TRTC SDK for Desktop Browser failed with regard to Session Traversal Utilities for NAT (STUN) hole punching. Please check the firewall configuration according to the environment requirements.

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?

This error indicates that the TRTC SDK for Desktop Browser failed to establish a media transport tunnel. Please check the firewall configuration according to the environment requirements.

### 4. What should I do if a 10006 error occurs?

If `"Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it"` is displayed, please check whether your TRTC application service is available.
Log in to the [TRTC Console](https://console.cloud.tencent.com/rav), click the application you created, click **Account Info**, and you can view the service status in the account information tab.
![](https://main.qcloudimg.com/raw/33bd04fe44f1a9b4163709f3c513643c.png)


## Related Documents

- [TWebLive API documentation](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [Online demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
