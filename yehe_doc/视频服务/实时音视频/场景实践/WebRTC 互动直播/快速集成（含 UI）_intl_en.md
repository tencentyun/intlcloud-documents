## Overview
If you are looking for an application with publishing and playback capabilities to live stream your events, have different latency requirements for different live streaming scenarios, or want to interact with audience during live streaming, try Tencent Cloud’s publishing/playback solutions.

Borrowing from common publishing and playback solutions on the market, we have launched [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) and [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer), which come with UI. You can find below a demonstration of their features. We also provide [TUIPusher Demo](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html) and [TUIPlayer Demo](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html), with user and room management systems, for you to try out the features.
![TUIPusher demonstration](https://qcloudimg.tencent-cloud.cn/raw/8d33df705c07c80d75ad19096e681903.png)
![TUIPlayer demonstration](https://qcloudimg.tencent-cloud.cn/raw/6490fdf7db4980db3a98b4b103fb52f1.png)


## Feature Overview
### TUIPusher
- Capturing and publishing data from the mic and camera
  - Customizing video parameters including frame rate, resolution, and bitrate
  - Applying beauty filters and setting beauty filter parameters
- Capturing and publishing data from the screen
- Publishing to the TRTC backend and Tencent Cloud’s CDNs
- Text chatting with the anchor and other audience
- Getting the audience list and muting audience

### TUIPlayer
- Playing the audio/video stream and screen sharing stream at the same time
- Text chatting with the anchor and other audience
- Three playback options: ultra-low-latency live streaming (300 ms latency), high-speed live streaming (latency within 1,000 ms), and standard live streaming (ultra-high concurrency)


## Integration
### Notes
- `TUIPusher` and `TUIPlayer` are based on TRTC and IM. Make sure you use the same `SDKAppID` for your TRTC and IM applications so that they can share your account and authentication information.
- You can use the basic-edition **content filtering** capability of IM to filter text messages. If you want to customize restricted words, go to the IM console > **Content Filtering**, and click **Upgrade**.
- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization. The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Step 1. Create an application
<dx-tabs>
::: Method 1: via TRTC
[](id:step1)
#### Step 1. Create a TRTC application

1. Sign up for a [Tencent Cloud account](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2Fdocument%2Fproduct%2F647%2F49327) and activate [TRTC](https://console.cloud.tencent.com/trtc) and [IM](https://console.cloud.tencent.com/im).
2. In the [TRTC console](https://console.cloud.tencent.com/trtc), click **Application Management > Create Application**.
![Create Application](https://main.qcloudimg.com/raw/34f87b8c0a817d8d3e49baac5b82a1fa.png)

#### Step 2. Get the key

1. In the application list, find the application created and click **Application Info** to view the `SDKAppID`.
![](https://qcloudimg.tencent-cloud.cn/raw/f7915fbbeb48518c2b25a413960f3432.png)
2. Select the **Quick Start** tab to view the application’s secret key.
![](https://qcloudimg.tencent-cloud.cn/raw/06d38bbdbaf43e1f2b444edae00019fa.png)

>?
>- Accounts creating their first application in the TRTC console will get a 10,000-minute free trial package.
>- After you create a TRTC application, an IM application with the same `SDKAppID` will be created automatically. You can configure package information for the application in the [IM console](https://console.cloud.tencent.com/im).

:::
::: Method 2: via IM\sIM
#### Step 1. Create an IM application
1. Log in to the [IM console](https://console.cloud.tencent.com/im), and click **Create Application**.
   ![](https://main.qcloudimg.com/raw/c8d1dc415801404e30e49ddd4e0c0c13.png)
2. In the pop-up window, enter an application name and click **Confirm**.
   ![](https://main.qcloudimg.com/raw/496cdc614f7a9d904cb462bd4d1e7120.png)
3. Go to the [overview page](https://console.cloud.tencent.com/im) to view the status, edition, `SDKAppID`, creation time, and expiration time of the application created. Note the `SDKAppID`.

#### Step 2. Get the key and activate TRTC
1. On the [overview page](https://console.cloud.tencent.com/im), click the application created to go to the **Basic Configuration** page. In the **Basic Information** section, click **Display key**, and copy and save the key.
![](https://main.qcloudimg.com/raw/030440f94a14cd031476ce815ed8e2bc.png)
>! Please store the key information properly to prevent leakage.
2. On the **Basic Configuration** page, activate TRTC.
![](https://main.qcloudimg.com/raw/1c2ce5008dad434d9206aabf0c07fd04.png)
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
![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)
4. Run `TUIPusher` and `TUIPlayer` in a local development environment.
```bash
cd Web/TUIPusher
npm run serve

cd Web/TUIPlayer
npm run serve
```
5. You can open `http://localhost:8080` and `http://localhost:8081` to try out the features of `TUIPusher` and `TUIPlayer`.
6. You can modify the room, anchor, and audience information in `TUIPusher/src/config/basic-info-config.js` and `TUIPlayer/src/config/basic-info-config.js`, but **make sure the room and anchor information are consistent in the two files**.

>! 
>- You can now use `TUIPusher` and `TUIPlayer` for ultra-low-latency live streaming. If you want to support high-speed and standard live streaming too, go on with [Step 3. Enable relayed push](#step3).
>- The local UserSig calculation method is used for local development and debugging only. Do not publish it to your online systems. Once your SECRETKEY is disclosed, attackers can use your Tencent Cloud traffic without authorization.
>- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

[](id:step3)
### Step 3. Enable relayed push

As the high-speed and standard live streaming features of `TUIPusher` and `TUIPlayer` are powered by CSS, you need to enable relayed push to use the features.

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
>- In this document, `UserSig` is generated on the client based on the `SDKAppID` and secret key you provide. The secret key may be easily decompiled and reversed, and if your key is leaked, attackers will be able to steal your traffic. Therefore, **this method is for local debugging only**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).
- Submit account information such as user information, room information, `SDKAppID`, and `UserSig` to `store` of `vuex` for global storage, as in `TUIPusher/src/pusher.vue` and `TUIPlayer/src/player.vue`, and you will be able to use all features of the two components on publishing and playback clients. The diagram below describes the process in details:
![](https://qcloudimg.tencent-cloud.cn/raw/d2cafd2e0f029908859f7498e9d92297.png)

## Notes
### Supported platforms

| OS | Browser | Browser Minimum Version Requirement | TUIPlayer | TUIPusher | TUIPusher Screen Sharing |
| ------- | ------- | ------- | ------- | ------- | ------- |
| macOS | Safari (desktop) | 11+ | Supported | Supported | Supported (on Safari 13+)  |
| macOS  | Chrome (desktop) |  56+ | Supported | Supported | Supported (on Chrome 72+) |
| macOS   | Firefox (desktop) | 56+ | Supported | Supported | Supported (on Firefox 66+) |
| macOS   | Edge (desktop) | 80+ | Supported | Supported | Supported |
| macOS   | WeChat built-in browser (desktop) | - | Supported      | Not supported    | Not supported |
| macOS   | WeCom built-in browser (desktop) | - | Supported      | Not supported    | Not supported |
| Windows  | Chrome (desktop) |  56+ | Supported | Supported | Supported (on Chrome 72+) |
|   Windows   | QQ browser (desktop, WebKit core) | 10.4+ | Supported | Supported | Not supported |
| Windows   | Firefox (desktop) | 56+ | Supported | Supported | Supported (on Firefox 66+) |
| Windows | Edge (desktop) | 80+ | Supported | Supported | Supported |
| Windows   | WeChat built-in browser (desktop) | - | Supported | Not supported | Not supported |
| Windows  | WeCom built-in browser (desktop) | - | Supported | Not supported | Not supported |

### Domain requirements
For security and privacy reasons, only HTTPS URLs can access all features of `TUIPusher` and `TUIPlayer`. Therefore, please use the HTTPS protocol for the web page of your application in production environments.
>! Note: You can use `http://localhost` for local development.

The table below lists the supported URL domain names and protocols.

| Scenario | Protocol | TUIPlayer | TUIPusher | TUIPusher Screen Sharing | Remarks |
| ------- | ------- | ------- | ------- | ------- | ------- |
| Production | HTTPS        | Supported | Supported | Supported | Recommended |
| Production     | HTTP | Supported       | Not supported   | Not supported   | - |
| Development | `http://localhost` | Supported | Supported | Supported | Recommended |
| Development | `http://127.0.0.1` | Supported | Supported | Supported   | - |
| Development | `http://[local IP address]` | Supported | Not supported | Not supported | - |

### Firewall configuration
`TUIPusher` and `TUIPlayer` rely on the following ports and domain for data transfer, which should be added to the allowlist of your firewall.
- TCP port: 8687
- UDP ports: 8000, 8080, 8800, 843, 443, 16285
- Domain name: qcloud.rtc.qq.com

## Summary
In newer versions to come, we expect to support communication between the web components and the TRTC SDKs for iOS, Android, etc. and introduce features such as co-anchoring, advanced filters, custom layout, relaying to multiple platforms, and image/text/music upload.

If you have any suggestion or comment, please contact us at colleenyu@tencent.com.

