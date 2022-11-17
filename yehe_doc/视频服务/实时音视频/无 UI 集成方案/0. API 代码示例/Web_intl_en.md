This document describes how to quickly run the demo for the TRTC web SDK.
## Limits
Before you run the demo for the TRTC web SDK, pay attention to the following:

### Supported platforms
The TRTC web SDK is based on WebRTC. For details about the browsers supported, see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/41664).
If your browser (for example, WebView) is not in the list, you can run a [TRTC Web SDK Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in the browser to test whether it fully supports WebRTC.

If your application scenario is mainly in the education sector, consider using the [TRTC Electron SDK](https://intl.cloud.tencent.com/document/product/647/35097), which supports the dual-stream mode (low-quality and high-quality streams), with more flexible screen sharing schemes and better recovery capabilities for poor network connections. 

### URL protocol support
Because of the security policies of browsers, when you use WebRTC, there are requirements on the protocol used for access. For details, see the table below.

| Scenario     | Protocol             | Receive (Playback) | Send (Publish) | Share Screen | Remarks |
|----------|:-----------------|:---------|----------|--------|----------|
| Production     | HTTPS        | Supported         | Supported         | Supported     | **Recommended** |
| Production     | HTTP         | Supported         | Not supported       | Not supported   |   -   |
| Local development | http://localhost | Supported         | Supported         | Supported     | **Recommended** |
| Local development | http://127.0.0.1 | Supported         | Supported         | Supported     |   -   |
| Local development | http://[local IP address]  | Supported         | Not supported       | Not supported   |   -   |
| Local development | file:///         | Supported         | Supported         | Supported     |   -   |

### Firewall configuration
Users may fail to have an audio/video call due to firewall restrictions. To avoid this, add the ports and domains specified in [Firewall Restrictions](https://www.tencentcloud.com/document/product/647/35164) to the firewall allowlist.


## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create an application

1. Log in to the TRTC console and select [Application Management](https://console.cloud.tencent.com/trtc/app) on the left sidebar.

2. Click **Create application**, enter an application name such as `APIExample`. If you already have an application, select **Existing** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### Step 2. Download the sample code

1. Select **No UI** and go to GitHub to download the sample code for your platform.
2. Click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### Step 3. Configure the project
1. If you are running a demo project, select **Testing**. Note the `SDKAppID` and secret key.
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. Open the file downloaded previously. Follow the instructions in the console to modify the `SDKAppID` and secret key, and click **Next**.

>?
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of TRTC-API-Example**.
>- The best practice is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to your server for a dynamic `UserSig`. For more information, see [How do I calculate `UserSig` during production?](https://www.tencentcloud.com/document/product/647/35166).


## FAQs

### 1. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
It indicates that STUN hole punching failed. Refer to [Firewall Restrictions](https://www.tencentcloud.com/document/product/647/35164) to check your firewall configuration.

### 2. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates the TRTC web SDK failed to establish a media transport connection. Check your firewall configuration against [Firewall Restrictions](https://www.tencentcloud.com/document/product/647/35164).

### 3. What should I do if a 10006 error occurs?
If the error "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" occurs, check whether the TRTC service status for your application is “normal”.
Log in to the [TRTC console](https://console.cloud.tencent.com/rav), select the application you created, and click **Application Info** to view its service status.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? For other questions, see [Web](https://intl.cloud.tencent.com/document/product/647/37340).
