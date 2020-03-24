This document describes how to quickly run the TRTC SDK for Web Demo.

>The TRTC SDK for Web Demo is mainly for developers. If you want to try out the features of the TRTC SDK for Web, please directly use the [official demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html).
Before the trial, you are recommended to view [TRTC SDK for Web API Overview](https://trtc-1252463788.file.myqcloud.com/web/docs/index.html) and [Tutorials for Basic Audio/Video Calls](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-01-basic-video-call.html).

<span id="requirements"></span>
## Environment Requirements
- Please use the latest version of Chrome.
- The TRTC SDK for Web uses the following ports for data transfer, which should be added to the whitelist of the firewall. After configuring these ports, please use the [official demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) to check whether the ports work.
 - TCP port: 8687
 - UDP ports: 8000, 8800, 843, 443
 - Domain name: qcloud.rtc.qq.com
 
 
## Directions
<span id="step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and click **Create Application**.
  If you already have an application, please note down its `SDKAppID` and then [download the SDK and demo source code](#step2) directly; otherwise, please proceed to the next step.
2. Enter the application's name and other information and click **OK**.
  After the application is created, an application ID (SDKAppID) will be automatically generated, which should be noted down.


<span id="step2"></span>
### Step 2. Download the SDK and demo source code
1. Click the application card to enter the **Getting Started** page.
2. Click **Web** in **Step 1: download SDK + auxiliary demo source code** to get redirected to [GitHub](https://github.com/tencentyun/TRTCSDK) (or visit [Gitee](https://gitee.com/cloudtencent/TRTCSDK)) and download the relevant SDK and demo source code.


<span id="step3"></span>
### Step 3. View and copy the encryption key
1. Click **View Key** in **Step 2: obtain the secret key to issue UserSig** to get the encryption key used to calculate `UserSig`.
2. Click **Copy Secret Key** to copy the key to the clipboard.

<span id="CopyKey"></span>
### Step 4. Configure demo project files
The `GenerateTestUserSig.js` file in the demo project can be used to calculate `UserSig` locally by using the HMAC-SHA256 algorithm for quick demo execution.
 
1. Decompress the source package downloaded in [step 2](#step2).
2. Find and open the `Web/js/debug/GenerateTestUserSig.js` file.
3. Set the relevant parameters in the `GenerateTestUserSig.js` file:
  - SDKAPPID: please enter the actual `SDKAppID` obtained in [step 1](#step1).
  - SECRETKEY: please enter the actual key information obtained in [step 3](#step3).

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166#Server).

### Step 5. Run the demo
Open the `index.html` in the root directory of the demo with Chrome to run the demo.

>!
> - Generally, the demo needs to be deployed on your server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers more comprehensive support for the features of the TRTC SDK for Web; therefore, Chrome is recommended for the demo.


- Click**Enter Room** to enter an audio/video call room and publish local audio/video stream.
 You can open multiple pages and click **Enter Room* on each of them. Normally, multiple video images can be seen with audio/video call simulated.
- Click **Exit Room** to exit the audio/video call.
- Click **Start Push** to publish local audio/video streams.
- Click **Stop Push** to stop publishing local audio/video streams.

>WebRTC needs to use camera and mic to capture audio and video. During the trial, you may receive relevant prompts from Chrome and you should click **Allow**.


## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to click **Upgrade** in **Step 2: obtain the secret key to issue UserSig** to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [legacy algorithm](https://intl.cloud.tencent.com/document/product/647/35166#old-version-of-algorithm).

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This error indicates that the TRTC SDK for Web failed with regard to Session Traversal Utilities for NAT (STUN). Please check the firewall configuration according to the [Environment Requirements](#requirements).

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
This error indicates that the TRTC SDK for Web failed to establish a media transport tunnel. Please check the firewall configuration according to the [Environment Requirements](#requirements).

### 4. What should I do if a 10006 error occurs?
If "Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it" is displayed, please check whether your TRTC application service is available.
Log in to the TRTC Console, click the application you created, click **Account Info**, and you can view the service status in the account information tab.
