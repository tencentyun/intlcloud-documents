This document describes how to quickly run the experience demo of the Tencent Cloud Web ILVB component.

## Prerequisites
You have [signed up](https://intl.cloud.tencent.com/document/product/378/17985) for a Tencent Cloud account and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions

### Step 1: create an application

1. Log in to the [Instant Messaging console](https://console.cloud.tencent.com/im).
2. Click **Add Application**.
3. In the **Create Application** dialog box, enter an application name and click **OK**.
 After the application is created, you can view the status, service version, `SDKAppID`, creation time, and expiration time of the new application on the overview page of the console. Record the `SDKAppID`.


### Step 2: obtain the key information and activate the TRTC service

1. Click the target application card to go to its basic configuration page.
2. In the **Basic Information** area, click **Display Key**, and then copy and save the key information.
 >! Please store the key information properly to prevent leakage.
3. Activate the TRTC service.

### Step 3: download and configure the demo source code

1. Download the demo project of the Tencent Cloud Web ILVB component from the [download address](https://github.com/tencentyun/TWebLive).
2. Open the `TWebLive/dist/debug/GenerateTestUserSig.js` file and set relevant parameters:
 - SDKAPPID: set it to the actual SDKAppID obtained in Step 1.
 - SECRETKEY: enter the actual key obtained in Step 2.


>!
>- The method of local UserSig calculation is used for local development debugging only. Do not directly publish it to your online systems. Once your `SECRETKEY` is disclosed, attackers can use your Tencent Cloud traffic without authorization.
>- The correct `UserSig` distribution method is to integrate the computing code of the `UserSig` into your server and provide an app-oriented API. When `UserSig` is required, your app can send a request to the business server to obtain the dynamic `UserSig`. For more information, see [How to Generate UserSig on the Server](https://intl.cloud.tencent.com/document/product/1047/34385).

### Step 4. Run the demo
Open the `index.html` file in the `dist` directory with Chrome to run the demo.
>!
>- Generally, the demo needs to be deployed on your server and then accessed through `https://domain name/xxx`. You can also build a server locally and access the demo through `localhost:port`.
>- Currently, the desktop version of Chrome offers more comprehensive support for the features of the TRTC SDK for desktop browsers. Therefore, Chrome is recommended for the demo.




WebRTC needs to use a camera and mic to capture audio and video. During the trial, you may receive relevant prompts from Chrome and you should click **Allow**.

## Environment Requirements
- Please use the latest version of Chrome.
- TWebLive uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuring these ports, use the [official demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html) to check whether the ports work.
  - TCP port: 8687
  - UDP ports: 8000, 8080, 8800, 843, 443, and 16285
  - Domain name: qcloud.rtc.qq.com

## FAQs

### 1. Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK v6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before this version, you need to upgrade the signature algorithm before you can get a new encryption key.

### 2. What should I do if the client error "RtcError: no valid ice candidate found" occurs?
This indicates that the TRTC desktop browser SDK failed to pass Session Traversal Utilities for NAT (STUN). Please check your firewall policy based on the environment requirements.

### 3. What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
This indicates that the TRTC desktop browser SDK failed to build a media transfer channel. Please check your firewall policy based on the environment requirements.

### 4. What should I do if a 10006 error occurs?
If "Join room failed result: 10006 error: service is suspended, if charge is overdue,renew it" is displayed, please check whether your TRTC application service is available.
Log in to the [TRTC console](https://console.cloud.tencent.com/rav), click the application you created, click **Account Info**, and you can view the service status in the account info tab.


## References

- [TWebLive API Guide](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblive/TWebLive.html)
- [Online Demo](https://webim-1252463788.cos.ap-shanghai.myqcloud.com/tweblivedemo/index.html)
