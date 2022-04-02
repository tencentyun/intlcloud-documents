This document describes how to quickly run the demo of the TRTC SDK for web.
## Preparations
Before you run the demo of the TRTC SDK for web, pay attention to the following:

### Supported platforms
The TRTC SDK for web is based on WebRTC. For details about the browsers supported, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664).
If your browser, for example, WebView, is not in the list, you can run a [TRTC Web SDK Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in the browser to test whether it fully supports WebRTC.

- If your application scenario is mainly in the education sector, consider using the [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports big and small (dual-channel) images, with more flexible screen sharing schemes and better recovery capabilities for poor network connections. 

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
The TRTC SDK for web uses the following ports and domain names for data transfer, which should be added to the allowlist of your firewall. You can use our [demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html) to check whether the configuration has taken effect. For details, see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).
- TCP port: 8687
- UDP ports: 8000, 8080, 8800, 843, 443, 16285
- Domain names: `*.rtc.qq.com`, `yun.tim.qq.com`


## Prerequisite
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

[](id:step1)

### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTRTC` and click **Create**. If you have already created an application, click **Existing** to select it.
3. Add or edit tags for your application if necessary, and click **Create**.

![](https://qcloudimg.tencent-cloud.cn/raw/7d1d1940f02ee954c369b5f749e0c663.png)

>?
>- An application name can contain up to 15 characters. Only digits, letters, Chinese characters, and underscores are allowed.
>- Tags are used to mark and sort your Tencent Cloud resources. For example, your company may have multiple business units, each using one or more TRTC applications. You can tag the applications with the information of the corresponding business units. Tags are optional. You can add and edit tags for your applications as needed.

[](id:step2)
### Step 2. Download the SDK and demo source code
1. Download the web SDK and demo source code.
2. After the download is completed, click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)


[](id:step3)
### Step 3. Configure the demo project file
1. In the **Modify Configuration** step, note the `SDKAppID` and key.
2. Find and open the `Web/base-js/js/debug/GenerateTestUserSig.js` file.
3. Set the following parameters in the `GenerateTestUserSig.js` file:
  - SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
  - `SECRETKEY`: Left empty by default. Set it to the actual key. 
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.

>!
>- In this document, the method to obtain UserSig is to configure a SECRETKEY in the client code. In this method, the SECRETKEY is vulnerable to decompilation and reverse engineering. Once your SECRETKEY is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Run the demo
Open `index.html` in the root directory of the demo with Chrome to run the demo.

>!
>- Normally, the demo needs to be deployed on the server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
> - Currently, the desktop version of Chrome offers better support for the features of the TRTC SDK for web; therefore, Chrome is recommended for the demo.



- Click **Join Room** to join a room and publish the local stream.
 You can open multiple pages and click **Join Room** on each of them. You should be able to see multiple videos, which simulate a real-time audio/video call.
- Click the camera icon to select a camera.
- Click the mic icon to select a mic.
>?WebRTC uses the camera and mic of your device to capture audio and video. During the demo run, when prompted by Chrome, you should click **Allow**.


## Running the Demo Online
You can also run your project using the online demo we provide: After obtaining the `SDKAppID` and key, open the [online demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/quick/index.html) and follow the instructions on the page.


## FAQs
### 1. Only public and private keys can be obtained when I try to view the key. How do I get a key?
Since the release of v6.6 for app and v4.0 for web in August 2019, the new signature algorithm HMAC-SHA256 has been used. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade

  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/49da46eea23847de79925a12e7a07102/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)4-%E8%BF%94%E8%BF%98.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/fbb69de98ae6ec0c6e1d09c8d95d57b7/%E8%B7%91%E9%80%9ADemo(%E6%A1%8C%E9%9D%A2%E6%B5%8F%E8%A7%88%E5%99%A8)5-%E8%BF%94%E8%BF%98.png)

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This error indicates that the TRTC SDK for web failed with regard to hole punching via Session Traversal Utilities for NAT (STUN). Please check your firewall configuration against the [Environment Requirements](#requirements).

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates that the TRTC SDK for web failed to establish a media transmission channel. Please check your firewall configuration against the [Environment Requirements](#requirements).

### 4. What should I do if a 10006 error occurs?
If the error "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether the TRTC service status for your application is “normal”.
Log in to the [TRTC console](https://console.cloud.tencent.com/rav), select the application you created, and click **Application Info** to view its service status.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? For other questions, see [Web](https://intl.cloud.tencent.com/document/product/647/37340).
