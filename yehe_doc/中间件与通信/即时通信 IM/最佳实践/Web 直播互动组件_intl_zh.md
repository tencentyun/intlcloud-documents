## 前言

本文介绍利用 [即时通信 IM ](https://intl.cloud.tencent.com/product/im) 和 [实时音视频 TRTC ](https://intl.cloud.tencent.com/product/trtc) 集成的 WebRTC 直播互动组件（带 UI）。

即时通信 IM 针对不同需求及不同场景，提供了一系列解决方案。即时通信 IM 强大的聊天室互动能力、关系链托管、第三方回调能力，完美契合直播场景对于聊天互动、观众管理、互动抽奖等需求，并且考虑开发者对于直播的低延时需求和开发者快速接入的诉求，IM 联合 TRTC 推出带 UI 的 Web 端互动直播推拉流组件 TUIPusher & TUIPlayer。

本次推出的 [TUIPusher](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPusher) 和 [TUIPlayer](https://github.com/tencentyun/TUILiveRoom/tree/main/Web/TUIPlayer) 组件涵盖观众列表、聊天互动、美颜、屏幕共享等功能，开箱即用，适配主流的桌面浏览器。TUIPusher 及 TUIPlayer 功能演示请观看下图。同时，我们结合用户管理系统和房间管理系统提供了 [TUIPusher 体验链接](https://web.sdk.qcloud.com/component/tuiliveroom/tuipusher/pusher.html) 及 [TUIPlayer 体验链接](https://web.sdk.qcloud.com/component/tuiliveroom/tuiplayer/player.html)。




## 功能介绍

### TUIPusher 推流组件

- 支持采集摄像头和麦克风的流并推流
  - 可根据需求设置视频参数（帧率，分辨率，码率）
  - 支持开启美颜并设置视频美颜参数
- 支持采集屏幕分享流并推流
- 支持推流到腾讯云实时音视频后台，推流到腾讯云 CDN
- 支持在线聊天室，和在线观众进行聊天互动
- 支持获取观众列表，对在线观众进行禁言操作

### TUIPlayer 拉流组件

- 支持同时播放音视频流和屏幕分享流
- 支持在线聊天室，和主播及其他观众进行聊天互动
- 支持超低延时直播（300ms 延时）, 快直播（1000ms 以内延时）以及标准直播（支持超高并发观看）三种拉流线路


## 接入方式

### 注意事项

- TUIPusher & TUIPlayer 基于腾讯云实时音视频和即时通信服务进行开发。实时音视频 TRTC 应用与 即时通信 IM 应用的 SDKAppID 一致，才能复用账号与鉴权。
- 本地计算 UserSig 的方式仅用于本地开发调试，请勿直接发布到线上，一旦 SECRETKEY 泄露，攻击者就可以盗用您的腾讯云流量。正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。

[](id:step1)

### 步骤一：开通腾讯云服务

<dx-tabs>
::: 方式1：基于即时通信\sIM
#### 步骤1：创建即时通信 IM 应用

1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)，单击 **创建新应用** 将弹出对话框。
   ![](https://main.qcloudimg.com/raw/b2acb7f79117f0828928e13a17ea9a6a.png)
2. 输入您的应用名称，单击 **确认** 即可完成创建。
   ![](https://main.qcloudimg.com/raw/7954cc2882d050f68cd5d1df2ee776a6.png)
3. 您可在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 总览页面查看新建应用的状态、业务版本、SDKAppID、创建时间以及到期时间。请记录 SDKAppID 信息。

#### 步骤2：获取 IM 密钥并开通实时音视频服务

1. 在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) 总览页单击您创建完成的即时通信 IM 应用，随即跳转至该应用的基础配置页。在 **基本信息** 区域，单击 **显示密钥**，复制并保存密钥信息。
   ![](https://main.qcloudimg.com/raw/610dee5720e94e324a48b44f4728816a.png)

>!请妥善保管密钥信息，谨防泄露。

2. 在该应用的基础配置页，开通腾讯云实时音视频服务。
   ![](https://main.qcloudimg.com/raw/8fb2940618dfb8b7ea06eecd62212468.png)

:::
::: 方式2：基于实时音视频

#### 步骤1：创建实时音视频 TRTC 应用

1. [注册腾讯云账号](https://intl.cloud.tencent.com/register) 并开通 [实时音视频](https://console.cloud.tencent.com/trtc) 和 [即时通信](https://console.cloud.tencent.com/im) 服务。
2. 在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 单击 **应用管理 > 创建应用** 创建新应用。
   ![创建应用](https://main.qcloudimg.com/raw/871c535f4b539ad7791f10d57ef0a9f3.png)

#### 步骤2: 获取 TRTC 密钥信息

1. 在 **应用管理 > 应用信息** 中获取 SDKAppID 信息。
   ![](https://qcloudimg.tencent-cloud.cn/raw/4efba95edf4073238420a40ec9a6b3b3.png)
2. 在 **应用管理 > 快速上手** 中获取应用的 secretKey 信息。
   ![](https://main.qcloudimg.com/raw/8ec16ab9cab85e324a347dea511f7e4e.png)

>?
>
>- 首次创建实时音视频应用的腾讯云账号，可获赠一个10000分钟的音视频资源免费试用包。
>- 创建实时音视频应用之后会自动创建一个 SDKAppID 相同的即时通信 IM 应用，可在 [即时通信控制台](https://console.cloud.tencent.com/im) 配置该应用的套餐信息。

:::
</dx-tabs>

[](id:step2)
### 步骤二：项目准备

1. 在 [GitHub](https://github.com/tencentyun/TUILiveRoom/tree/main/Web) 下载 TUIPusher & TUIPlayer 代码。
2. 为 TUIPusher & TUIPlayer 安装依赖。
   ```bash
   cd Web/TUIPusher
   npm install
   
   cd Web/TUIPlayer
   npm install
   ```
3. 将 sdkAppId 和 secretKey 填入 `TUIPusher/src/config/basic-info-config.js` 及 `TUIPlayer/src/config/basic-info-config.js` 配置文件中。
   ![](https://qcloudimg.tencent-cloud.cn/raw/2367f9c25773bc5d5de9db00d0962f06.png)
4. 本地开发环境运行 TUIPusher & TUIPlayer。
   ```bash
   cd Web/TUIPusher
   npm run serve
   
   cd Web/TUIPlayer
   npm run serve
   ```
5. 可打开 `http://localhost:8080` 和 `http://localhost:8081` 体验 TUIPusher 和 TUIPlayer 功能。
6. 可更改 `TUIPusher/src/config/basic-info-config.js` 及 `TUIPlayer/src/config/basic-info-config.js` 配置文件中的房间，主播及观众等信息，**注意保持 TUIPusher 和 TUIPlayer 的房间信息，主播信息一致**。
>!
>
> - 完成以上配置，您可以使用 TUIPusher & TUIPlayer 进行超低延时直播，如您需要支持快直播和标准直播，请继续阅读 [步骤三：旁路直播](#step3)。
> - 本地计算 UserSig 的方式仅用于本地开发调试，请勿直接发布到线上，一旦您的 `SECRETKEY` 泄露，攻击者就可以盗用您的腾讯云流量。
> - 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的 App 向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。


[](id:step3)
### 步骤三：旁路直播

TUIPusher & TUIPlayer 实现的快直播和标准直播依托于腾讯云 [云直播服务](https://intl.cloud.tencent.com/document/product/267)，因此支持快直播和标准直播线路需要您开启旁路推流功能。

1. 在 [**实时音视频控制台**](https://console.cloud.tencent.com/trtc) 中为您正在使用的应用开启旁路推流配置，可按需开启指定流旁路或全局自动旁路。
   ![](https://main.qcloudimg.com/raw/b9846f4a7f5ce1e39b3450963e872c90.png)
2. 请在 [**域名管理**](https://console.cloud.tencent.com/live/domainmanage) 页面添加自有播放域名，具体请参见 [添加自有域名](https://intl.cloud.tencent.com/document/product/267/35970)。
3. 在 `TUIPlayer/src/config/basic-info-config.js` 配置文件中配置播放域名。

完成以上配置，您可以体验 TUIPusher & TUIPlayer 支持超低延时直播，快直播以及标准直播的所有功能。

[](id:step4)
### 步骤四：生产环境应用

当您将 TUIPusher & TUIPlayer 用于生产应用时，在接入 TUIPusher & TUIPlayer 之外，您需要：

- 创建用户管理系统，用于管理产品用户信息，包括但不限于用户 ID，用户名，用户头像等。
- 创建房间管理系统，用于管理产品直播间信息，包括但不限于直播间 ID、直播间名称，直播间主播信息等。
- 服务端生成 UserSig。

> !
>
> - 本文生成 UserSig 的方式，是在客户端根据您填入的 sdkAppId 及 secretKey 生成 userSig，该方式的 secretKey 很容易被反编译逆向破解，一旦您的密钥泄露，攻击者就可以盗用您的腾讯云流量，因此**该方法仅适合本地跑通 TUIPusher & TUIPlayer 进行功能调试**。
> - 正确的 UserSig 签发方式是将 UserSig 的计算代码集成到您的服务端，并提供面向 App 的接口，在需要 UserSig 时由您的应用向业务服务器发起请求获取动态 UserSig。更多详情请参见 [服务端生成 UserSig](https://intl.cloud.tencent.com/document/product/647/35166)。

- 参考 `TUIPusher/src/pusher.vue` 及 `TUIPlayer/src/player.vue` 文件，将用户信息、直播间信息、SDKAppId 及 UserSig 等账号信息提交到 vuex 的 store 进行全局存储，您就可以跑通推拉流两个客户端的所有功能。

## 相关问题

1. Web 端如何实现美颜功能？
   请参考 [开启美颜](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)。

2. Web 端如何实现屏幕共享？
   请参考 [屏幕分享](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)。

3. Web 端如何实现云端录制?
   开启 云端录制，请参考 [实现云端录制与回放](https://intl.cloud.tencent.com/document/product/647/35426)。
   开启【云端录制】> 【指定用户录制】之后，Web 端可通过在调用 [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient) 接口时传入 userDefineRecordId 参数开启录制。

4. Web 端如何实现推流到 CDN ？
   Web 端推流到 CDN 请参考 [实现推流到 CDN](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html)。


## 注意事项

###  平台支持

| 操作系统 | 浏览器类型                   | 浏览器最低版本要求 | TUIPlayer | TUIPusher | TUIPusher 屏幕分享           |
| -------- | ---------------------------- | ------------------ | --------- | --------- | ---------------------------- |
| Mac OS   | 桌面版 Safari 浏览器         | 11+                | 支持      | 支持      | 支持（需要 Safari13+ 版本）  |
| Mac OS   | 桌面版 Chrome 浏览器         | 56+                | 支持      | 支持      | 支持（需要 Chrome72+ 版本）  |
| Mac OS   | 桌面版 Firefox 浏览器        | 56+                | 支持      | 支持      | 支持（需要 Firefox66+ 版本） |
| Mac OS   | 桌面版 Edge 浏览器           | 80+                | 支持      | 支持      | 支持                         |
| Mac OS   | 桌面版微信内嵌网页           | -                  | 支持      | 不支持    | 不支持                       |
| Mac OS   | 桌面版企业微信内嵌网页       | -                  | 支持      | 不支持    | 不支持                       |
| Windows  | 桌面版 Chrome 浏览器         | 56+                | 支持      | 支持      | 支持（需要 Chrome72+ 版本）  |
| Windows  | 桌面版 QQ 浏览器（极速内核） | 10.4+              | 支持      | 支持      | 不支持                       |
| Windows  | 桌面版 Firefox 浏览器        | 56+                | 支持      | 支持      | 支持（需要 Firefox66+ 版本） |
| Windows  | 桌面版 Edge 浏览器           | 80+                | 支持      | 支持      | 支持                         |
| Windows  | 桌面版微信内嵌网页           | -                  | 支持      | 不支持    | 不支持                       |
| Windows  | 桌面版企业微信内嵌网页       | -                  | 支持      | 不支持    | 不支持                       |

### 域名要求

出于对用户安全、隐私等问题的考虑，浏览器限制网页在 HTTPS 协议下才能正常使用 TUIPusher & TUIPlayer 的全部功能。为确保生产环境用户顺畅接入和体验 TUIPusher & TUIPlayer 的全部功能，请使用 HTTPS 协议访问音视频应用页面。

>! 本地开发可以通过 `http://localhost` 协议进行访问。

URL 域名及协议支持情况请参考如下表格：

| 应用场景     | 协议               | TUIPlayer | TUIPusher | TUIPusher 屏幕分享 | 备注 |
| ------------ | ------------------ | --------- | --------- | ------------------ | ---- |
| 生产环境     | HTTPS 协议         | 支持      | 支持      | 支持               | 推荐 |
| 生产环境     | HTTP 协议          | 支持      | 不支持    | 不支持             | -    |
| 本地开发环境 | `http://localhost` | 支持      | 支持      | 支持               | 推荐 |
| 本地开发环境 | `http://127.0.0.1` | 支持      | 支持      | 支持               | -    |
| 本地开发环境 | `http://[本机IP]`  | 支持      | 不支持    | 不支持             | -    |

### 防火墙限制

TUIPusher & TUIPlayer 依赖以下端口进行数据传输，请将其加入防火墙白名单。

- TCP 端口：8687
- UDP 端口：8000，8080，8800，843，443，16285
- 域名：qcloud.rtc.qq.com

## 结语

在后续的迭代中, 本文的 Web 端推拉流组件会逐渐与 iOS、Andriod 等各端连通，并在 Web 端利用实现观众连麦、高级美颜、自定义布局、转推多平台、上传图片文字音乐等能力，针对电商直播场景，计划利用 [即时通信IM](https://intl.cloud.tencent.com/product/im) 实现商城上下架、口令抽奖、答题抽奖等多样性的玩法。欢迎大家多多使用、提出您的宝贵意见。

如果有任何需要或者反馈，请[联系我们](https://intl.cloud.tencent.com/contact-us)。

