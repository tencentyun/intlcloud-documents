## Overview

This document describes WebRTC components (with UI) that are developed by integrating [Instant Messaging (IM)](https://intl.cloud.tencent.com/product/im) with [Tencent Real-Time Communication (TRTC)](https://intl.cloud.tencent.com/product/trtc).

IM offers a series of solutions specific to different demands and scenarios. Interactions via chat rooms, relationship chain hosting, and third-party callback features of IM perfectly fit demands in an LVB scenario, such as interactive chats, audience management, and interactive lucky draw. In addition, to satisfy developers’ demands for a low latency and rapid integration, IM together with TRTC introduces two WebRTC components (with UI): TUIPusher and TUIPlayer.

The components [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) and [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer) provide features including audience list, chat interactions, beauty filters, screen sharing, and so on. They are out-of-the-box and can adapt to mainstream desktop browsers. You can find below a demonstration of their features. We also provide [TUIPusher Demo](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html) and [TUIPlayer Demo](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html), with user and room management systems.




## Feature Overview

### TUIPusher

- Capturing and pushing streams from camera and mic
  - Customizing video parameters including frame rate, resolution, and bitrate
  - Applying beauty filters and setting beauty filter parameters
- Capturing and publishing data from the screen
- Publishing to the TRTC backend and Tencent Cloud’s CDNs
- Text chatting with the anchor and other audience
- Getting the audience list and muting audience

### TUIPlayer

- Playing the audio/video stream and screen sharing stream at the same time
- Interactively chatting with the anchor and other audience
- Three playback options: ultra-low-latency live streaming (300 ms latency), high-speed live streaming (latency within 1,000 ms), and standard live streaming (ultra-high concurrency)


## Integration

### Notes

- `TUIPusher` and `TUIPlayer` are developed based on Tencent Cloud TRTC and IM services. The account and authentication system can be reused only if the TRTC and IM applications have the same `SDKAppID`. 
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization. The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

[](id:step1)

### Step 1. Activate the Tencent Cloud services

<dx-tabs>
::: Method 1: via IM\sIM
#### Step 1. Create an IM app

1. Log in to the [IM console](https://console.cloud.tencent.com/im), and click **Create Application**.
   ![](https://main.qcloudimg.com/raw/b2acb7f79117f0828928e13a17ea9a6a.png)
2. In the pop-up window, enter an application name and click **Confirm**.
   ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
3. Go to the [overview page](https://console.cloud.tencent.com/im) to view the status, edition, `SDKAppID`, creation time, and expiration time of the application created. Note the `SDKAppID`.

#### Step 2. Obtain the key and activate TRTC

1. On the overview page of the [IM console](https://console.cloud.tencent.com/im), click the application you have created to go to the **Basic Configuration** page. In the **Basic Information** section, click **Display key**, and copy and save the key.
   ![](https://main.qcloudimg.com/raw/610dee5720e94e324a48b44f4728816a.png)

>! Please store the key information properly to prevent disclosure.

2. On the **Basic Configuration** page, activate TRTC.
   ![](https://main.qcloudimg.com/raw/8fb2940618dfb8b7ea06eecd62212468.png)

:::
::: Method 2: via TRTC

#### Step 1. Create a TRTC application

1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/register) and activate [TRTC](https://console.cloud.tencent.com/trtc) and [IM](https://console.cloud.tencent.com/im) services.
2. In the [TRTC console](https://console.cloud.tencent.com/trtc), click **Application Management > Create Application** to create an application.
   ![Create Application](https://main.qcloudimg.com/raw/871c535f4b539ad7791f10d57ef0a9f3.png)

#### Step 2. Get the TRTC key information

1. In the application list, find the application created and click **Application Info** to view the `SDKAppID`.
   ![](https://qcloudimg.tencent-cloud.cn/raw/4efba95edf4073238420a40ec9a6b3b3.png)
2. Select the **Quick Start** tab to view the application’s secret key.
   ![](https://main.qcloudimg.com/raw/8ec16ab9cab85e324a347dea511f7e4e.png)

>?
>
>- Accounts creating their first application in the TRTC console will get a 10,000-minute free trial package.
>- After you create a TRTC application, an IM application with the same `SDKAppID` will be created automatically. You can configure package information for the application in the [IM console](https://console.cloud.tencent.com/im).

:::
</dx-tabs>

[](id:step2)
### Step 2. Prepare your project

1. Download the code for `TUIPusher` and `TUIPlayer` at [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web).
2. Install dependencies for `TUIPusher` and `TUIPlayer`.
   ```bash
   cd Web/TUIPusher
   npm install
   
   cd Web/TUIPlayer
   npm install
   ```
3. Paste `SDKAppID` and the secret key to the specified locations below in the `TUIPusher/src/config/basic-info-config.js` and `TUIPlayer/src/config/basic-info-config.js` files.
   ![](https://qcloudimg.tencent-cloud.cn/raw/2367f9c25773bc5d5de9db00d0962f06.png)
4. Run `TUIPusher` and `TUIPlayer` in a local development environment.
   ```bash
   cd Web/TUIPusher
   npm run serve
   
   cd Web/TUIPlayer
   npm run serve
   ```
5. You can open `http://localhost:8080` and `http://localhost:8081` to try out the features of `TUIPusher` and `TUIPlayer`.
6. You can modify the room, anchor, and audience information in `TUIPusher/src/config/basic-info-config.js` and `TUIPlayer/src/config/basic-info-config.js`, but **make sure the room and anchor information is consistent in the two files**.
>!
>
>- You can now use `TUIPusher` and `TUIPlayer` for ultra-low-latency live streaming. If you want to support high-speed and standard live streaming too, go on with [Step 3. Enable relayed push](#step3).
- The local `UserSig` calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your `SECRETKEY` is disclosed, attackers can use your Tencent Cloud traffic without authorization.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/1047/34385).


[](id:step3)
### Step 3. Enable relayed push

The high-speed and standard live streaming services implemented by `TUIPusher` and `TUIPlayer` depend on the Tencent Cloud [CSS](https://intl.cloud.tencent.com/document/product/267) service, so you need to enable the relayed push feature first.

1. In the [TRTC console](https://console.cloud.tencent.com/trtc), enable relayed push for your application. You can choose **Specified stream for relayed push** or **Global auto-relayed push** based on your needs.
   ![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
2. On the **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** page, add your playback domain name. For detailed directions, please see [Adding Your Own Domain Names](https://intl.cloud.tencent.com/document/product/267/35970).
3. Configure the playback domain name in `TUIPlayer/src/config/basic-info-config.js`.

You can now use all features of `TUIPusher` and `TUIPlayer`, including ultra-low-latency live streaming, high-speed live streaming, and standard live streaming.

[](id:step4)
### Step 4. Apply in a production environment

To apply `TUIPusher` and `TUIPlayer` to a production environment, in addition to integrating them into your project, you also need to do the following:

- Create a user management system to manage user information such as user IDs, usernames, and profile pictures
- Create a room management system to manage room information such as room IDs, room names, and anchors
- Generate `UserSig` on your server

> !
>
>- In this document, `UserSig` is generated on the client based on the `SDKAppID` and secret key you provide. The secret key may be easily decompiled and reversed, and if your key is disclosed, attackers will be able to steal your traffic. Therefore, **this method is for local debugging only**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

- Submit account information such as user information, room information, `SDKAppID`, and `UserSig` to `store` of `vuex` for global storage, as in `TUIPusher/src/pusher.vue` and `TUIPlayer/src/player.vue`, and you will be able to use all features of the two components on publishing and playback clients. The diagram below shows the process in detail: 
   ![](https://main.qcloudimg.com/raw/ab2b13a441da8b0631cc664f95ad18db.png)

## FAQs

1. How do I implement the beauty filter feature on the web?
   See [Enabling Beauty Filters](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html).

2. How do I implement the screen sharing feature on the web?
   See [Screen Sharing](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html).

3. How do I implement the on-cloud recording feature on the web?
   For information about enabling on-cloud recording, see [On-Cloud Recording and Playback](https://intl.cloud.tencent.com/document/product/647/35426).
   After enabling [On-Cloud Recording] > [Specified User Recording], you can start recording on the web by passing in the `userDefineRecordId` when calling the [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient) API.

4. How do I publish stream to CDN on the web?
   For publishing a stream to CDN on the web, see [Publishing to CDN](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html).


## Notes

### Supported platforms

| Operating System | Browser (Desktop)                   | Required Version | TUIPlayer | TUIPusher | TUIPusher Screen Sharing           |
| -------- | ---------------------------- | ------------------ | --------- | --------- | ---------------------------- |
| macOS   | Safari         | 11+                | Supported      | Supported      | Supported (on Safari 13+)  |
| macOS   | Chrome         | 56+                | Supported      | Supported      | Supported (on Chrome 72+)  |
| macOS   | Firefox        | 56+                |Supported      | Supported      | Supported (on Firefox 66+) |
| macOS   | Edge           | 80+                | Supported      | Supported     | Supported                        |
| macOS   | WeChat built-in browser           | -                  | Supported      | Not supported    | Not supported                       |
| macOS   | WeCom built-in browser       | -                  | Supported      | Not supported    | Not supported                       |
| Windows   | Chrome         | 56+                | Supported      | Supported      | Supported (on Chrome 72+)  |
| Windows  | QQ browser (WebKit core)   | 10.4+              | Supported     | Supported     | Not supported                       |
| Windows   | Firefox        | 56+                |Supported      | Supported      | Supported (on Firefox 66+) |
| Windows   | Edge           | 80+                | Supported      | Supported     | Supported                        |
| Windows   | WeChat built-in browser           | -                  | Supported      | Not supported    | Not supported                       |
| Windows   | WeCom built-in browser       | -                  | Supported      | Not supported    | Not supported                       |

### Domain requirements

For security and privacy reasons, only HTTPS URLs can access all features of `TUIPusher` and `TUIPlayer`. Therefore, please use the HTTPS protocol for the web page of your application in production environments.

>! Note: You can use `http://localhost` for local development.

The table below lists the supported URL domain names and protocols.

| Scenario | Protocol | TUIPlayer | TUIPusher | TUIPusher Screen Sharing | Remarks |
| ------------ | ------------------ | --------- | --------- | ------------------ | ---- |
| Production     | HTTPS        | Supported         | Supported         | Supported     | Recommended |
| Production     | HTTP         | Supported         | Not supported       | Not supported   |   -   |
| Local development | `http://localhost` | Supported         | Supported         | Supported     | Recommended |
| Local development | `http://127.0.0.1` | Supported         | Supported         | Supported     |   -   |
| Local development | `http://[local IP address]`  | Supported         | Not supported       | Not supported   |   -   |

### Firewall configuration

`TUIPusher` and `TUIPlayer` rely on the following ports and domain for data transfer, which should be added to the allowlist of your firewall.

- TCP port: 8687
- UDP ports: 8000, 8080, 8800, 843, 443, 16285
- Domain name: qcloud.rtc.qq.com

## Summary

In future versions, we expect to support communication between the web components described here and the SDKs for iOS, Android, etc. and introduce features such as co-anchoring, advanced filters, custom layout, relaying to multiple platforms, and image/text/music upload. In terms of the live shopping scenario, we plan to launch more interactive features, such as item addition/removal, password-based lucky draw, and Q&A-based lucky draw, and other interactive features based on [IM](https://intl.cloud.tencent.com/product/im). We welcome your comments and suggestions.

If you have any suggestion or comment, [contact us](https://intl.cloud.tencent.com/contact-us).

